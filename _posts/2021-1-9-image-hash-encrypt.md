---
title: "이미지 파일을 해시 및 암호화 하는 과정에서 발생한 문제점 해결 방법"
excerpt: "전자 동의서 서명 암호화 서버 통신과의 오류 발생한 원인 파악 및 문제 해결 과정"
header:
  overlay_color: "#F2E315"
  overlay_filter: rgba(0, 0, 0, 0.5)
categories:
- Web
tags:
- 웹개발
- 프론트엔드
---

#### 2021년 1월 9일 개발 일지

### 전자동의서 및 서명 파일을 전송하는 클라이언트와 서버 통신 과정
화면에 전자 동의서를 이미지 파일을 보여주고 서명란에 사용자가 터치패드로 직접 서명할 수 있도록 한 후 서명 사진을 저장하여 서버로 전송할 때 정보 보호를 위해 클라이언트와 서버 간에 해시 값 검증 및 사진 파일 암호화를 하는 클라이언트 구현 작업을 했다. 작업 순서는 아래와 같다.

1. 클라이언트에서 전자동의서 정보 요청
2. 서버에서 전자동의서 이미지 목록 제공 (동시에 암호화 키 제공)
3. 클라이언트에서 전자동의서 이미지를 순서대로 보여주고 사용자의 서명이 필요한 마지막 장에 서명할 수 있는 터치 패드 컴포넌트 넣기
4. 사용자가 터치 패드에서 서명한 사진 저장하기
5. 서명된 사진을 해시하여 사진 파일을 서버에서 제공한 암호화 키로 암호화하여 서버로 전송
6. 서버에서 해시 값을 검증하는 과정을 거친 후 서명 사진을 저장


### MD5 해시 및 암호화 하는 방법
클라이언트에서 서명 파일을 저장하여 MD5 해시 값을 만들고 서버에서 제공 받은 암호화된 퍼블릭 키(publicKeyEncoded)로 MD5 해시를 암호화하여 해시 값과 이미지 파일을 서버로 전송하는 과정은 아래와 같다.

1. CryptoJS 라이브러리를 설치한 후
`npm install crypto-js`
`npm install --save @types/crypto-js`

2. 이미지 파일을 MD5 해시하여 해시 값을 추출한다.

```ts
let CryptoJS = require("crypto-js");
const getMd5Hash = (dataUrl: string) => {
    const hash = CryptoJS.MD5(CryptoJS.enc.Latin1.parse(dataUrl));
    const md5 = hash.toString(CryptoJS.enc.Hex)
    console.log(md5);
    return md5
}
```

3. 프로젝트 폴더에 /public/assets/ 폴더에 `jsencrypt.min.js` 를 추가한다.

4. `Index.html `에 스크립트를 추가한다.
`<script src=“%PUBLIC_URL%/assets/jsencrypt.min.js”></script>`

5. 서버에서 받은 암호화된 퍼블릭 키(publicKeyEncoded)로 MD5 해시를 암호화하여 해시 값을 추출한다.

```ts
const rsaEncrypt = (publicKey: string, md5: string) => {
    //전자동의서 파일 조회 API 에서 받은 "publicKeyEncoded"
    let jsEncrypt = new JSEncrypt();
    jsEncrypt.setPublicKey(publicKey);
    let fileHash = jsEncrypt.encrypt(md5);
    console.log("이미지 파일 hash값 RSA 암호화 : " + fileHash);
    return fileHash
  }
```

6. 암호화한 해시 값과 이미지 파일을 서버로 전송한다.

```ts
const md5 = Utils.getMd5Hash(signDataUrl)
const fileHash = Utils.rsaEncrypt(data.publicKeyEncoded, md5)
let formData = new FormData()
formData.append('signatureCaptureFileBase64', signDataUrl)
formData.append('signatureCaptureFileHashRsa', fileHash)

const res = await API.sendMyTrialSign(formData)
if (res && res.success) {
    setAlert(true, '서명을 제출하였습니다.')
    close()
}

```


### 파일 암호화 하는 과정에서 발생한 문제점
클라이언트에서 추출한 해시 값과 서버에서 재검증하는 해시 값이 달라서 계속 해시 인증에 실패하게 되었다. 백엔드 개발자와 이야기 해보니 **클라이언트와 서버에서 해시할 때 각각 사용하는 파일 타입이 달랐던게 문제**가 되었다. 서명 이미지 파일의 데이터 방식이 클라이언트에서는 base64 로 해시 값을 추출하였고 서버에서는 bytes array 파일을 해시 값으로 재검증 하여 같은 파일임에도 불구하고 해시 값이 달라 서버에서 해시 검증을 하지 못하였다. 따라서 **파일 타입을 base64 로 통일하여 클라이언트와 서버 간의 이미지 전송 및 파일 해시 검증에 성공**하게 되었다.


[crypto-js  -  npm](https://www.npmjs.com/package/crypto-js)
[JSEncrypt](https://travistidwell.com/jsencrypt/)
