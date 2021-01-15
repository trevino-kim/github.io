---
title: "리액트로 전자 서명 터치 패드 구현하기"
excerpt: "브라우저, 아이오닉 모바일 앱, 하이브리드 모바일 앱에서 리액트 라이브러리 react-signature-canvas 를 사용하여 전자 서명 터치 패드 기능을 구현하는 방법 및 소스 코드 공유"
header:
  overlay_color: "#48CBFA"
  overlay_filter: rgba(0, 0, 0, 0.5)
categories:
- Hybrid-App
tags:
- 모바일앱
- React
- Ionic-react
---

#### 2021년 1월 7일 개발일지 - 현재 진행 중인 일과 기술 스택:
안드로이드와 iOS 를 한 번에 빌드하는 하이브리드 모바일 앱의 프론트엔드를 개발하고 있으며 프레임워크로 아이오닉 (Ionic) 과 리액트 (React) 를 사용하고 있다.

## 리액트로 전자 서명 터치 패드 구현 하는 단계
1. React 라이브러리 `react-signature-canvas` 를 설치한다.
`npm i -S react-signature-canvas`
2. 리액트 타입스크립트를 사용한다면 타입 패키지를 추가 설치한다.
 `npm install —save @types/react-signature-canvas`
3. react-signature-canvas 를 import 한다.
```ts
import React, { useRef, useState } from 'react'
import ReactSignatureCanvas from 'react-signature-canvas'
import SignatureCanvas from 'react-signature-canvas'
```

4. 아래 소스 코드 예제처럼 `SignatureCanvas` 컴포넌트를 사용할 수 있다.

```tsx
// ref 와 useRef 를 활용하여 컴포넌트 지정하기
const canvas = useRef<ReactSignatureCanvas>(null)

// 서명 패드에 서명한 내용 지우기
const clear = () => {
    canvas.current?.clear()
    setOnSign(false)
  }

// 서명 사진 데이터 url 얻는 방법
const getUrl = () => canvas.current!.toDataURL()

// 서명 패드 컴포넌트 사용 예시
// 400 x 300 사이즈의 캔버스 서명 패드를 만든다.
return (
		<SignatureCanvas
          ref={canvas}
          penColor="black"
          canvasProps={{
            width: 400,
            height: 300,
            className: 'sigCanvas',
          }}
          onBegin={() => setOnSign(true)}
        />
)
```

SignatureCanvas 컴포넌트의 프로퍼티와 메소드는 [react-signature-canvas 라이브러리 문서 웹사이트](https://www.npmjs.com/package/react-signature-canvas)에서 확인할 수 있다. 위 예시에 쓰인 메소드 중 `onBegin()` 은 서명을 시작했을 때 사용할 수 있다.
