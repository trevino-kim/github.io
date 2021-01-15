---
title: "자바스크립트 Base64 기본 및 URL 인코딩 개념 알기"
excerpt: "Base64 의 기본 개념과 사용하는 이유를 알아보고 자바스크립트로 Base64 인코딩 및 디코딩 하는 법, URL 인코딩 및 디코딩 하는 방법에 대해 알아보자."
header:
  overlay_color: "#F2E315"
  overlay_filter: rgba(0, 0, 0, 0.5)
categories:
- Web
tags:
- 웹개발
- 프론트엔드
---

## Base64 란 무엇인가?
Base64 는 말 그대로 하면 64진법이다. 각각의 Base64 문자 하나는 6비트를 나타내는데, 64개의 문자를 0부터 63까지의 숫자로 변환하여 전체 데이터를 하나의 `string` 으로 바꾸는 인코딩 방식을 말한다.

참고: [베이스64 - 위키백과, 우리 모두의 백과사전](https://ko.wikipedia.org/wiki/%EB%B2%A0%EC%9D%B4%EC%8A%A464)

### Base64 Encoding & Decoding
* 이미지나 오디오 같은 바이너리 데이터를 HTTP 같은 텍스트로 된 프로토콜로 보내기 위한 작업으로 통신 전송과정에서 데이터의 손실을 막아 텍스트가 변형되지 않고 안전하게 전송될 수 있도록 하기 위해 사용한다. 예를 들어,  바이너리 데이터를 ASCII 로 인코딩하여 전송하면 시스템 별로 처리 방식이 다르거나 일부 문자의 코드 값을 다르게 처리하는 경우가 있어 ASCII 인코딩한 데이터로 통신하면 데이터가 변형된 채로 전달 될 수 있다. 이때 Base64 로 인코딩하여 전송하면 안전하게 전송할 수 있다.

*  Base64로 인코딩하여 여러 개의 파일을 하나로 합쳐서 보낼수 도 있고, Base64 파일을 html 및 css 파일 안에 임베드 할 수 도 있다. 프론트엔드에서 가장 보편적으로 쓰이는  것은 Base64 이미지 파일을 이미지 태그 소스로 넣어 이미지를 화면에 표시하거나  `<img src='BASE64_DATA_URL' />`, 프론엔드에서 이미지를 캡쳐하여 서버로 전송할 때 사용한다.

* 자바스크립트에서 사용하는 Base64 Encoding & decoding 방법
	* `btoa()` -> string 을 base64로 **인코딩**하는 자바스크립트 메소드
	* `atob()` -> 인코딩 된 string 을 base64 로 **디코딩**하는 자바스크립트 메소드

```js
const str = "Jade+Kim";
const encodedBase64string = btoa(str);
const decodedString = atob(encodedBase64string);
console.log(encodedBase64string)
console.log(decodedString)
```

#### 이미지 파일을 Base64 스트링으로 변경하는 방법
* [javascript - Get Base64 encode file-data from Input Form - Stack Overflow](https://stackoverflow.com/questions/6978156/get-base64-encode-file-data-from-input-form)
* [How can I convert an image into Base64 string using JavaScript? - Stack Overflow](https://stackoverflow.com/questions/6150289/how-can-i-convert-an-image-into-base64-string-using-javascript)


### URL Encoding & Decoding
: URL 쿼리 파라미터를 안전하게 전송하기 위한 작업으로 웹 브라우저가 서버로 보내기 전에 URL 을 인코딩 한다. 예를 들면 띄어 쓰기를 쿼리로 보내면 + 로 바뀌고, & 는 %26 으로 바뀌어진다. 서버로 전달될 때 디버깅 콘솔의 네트워크 탭에서 클라이언트에서 보낸 쿼리를 확인 하면 URL 이 디코딩 되어서 Query String Parameters 에 사용자가 보낸 그대로의 문자가 들어있는 것을 확인할 수 있다.

보통은 AJAX 같은 라이브러리 같은 경우 자동으로 URL Encoding 을 해주기 때문에 더블 인코딩 해줄 필요는 없다. URL 인코딩 및 디코딩 개념에 대해 알아보고 자바스크립트에서 `encodeURIComponent()` 과 `decodeURIComponent()` 를 제공한다는 것을 알

```js
const name = "Jade+Kim";
const nameUrlEncoded = encodURIComponent(name);
console.log(nameUrlEncoded)
```
