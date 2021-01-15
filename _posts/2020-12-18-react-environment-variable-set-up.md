---
title: "리액트 환경 변수 설정하고 사용하는 방법"
excerpt: "리액트 프레임워크에서는 scripts 에 환경 변수를 추가하여 쉽게 사용 가능할 수 있다."
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

#### 2020/12/4 개발일지
### 현재 진행 중인 일과 기술 스택:
안드로이드와 iOS 를 한 번에 빌드하는 하이브리드 모바일 앱의 프론트엔드를 개발하고 있으며 프레임워크로 아이오닉 (Ionic) 과 리액트 (React), 네이티브 프레임워크는 캐파시터(Capacitor) 를 사용하고 있다.

안드로이드 앱을 구글 플레이스토어에 업데이트 할 때, 애플 앱을 앱 스토어에 업데이트 할 때는 테스트용 빌드와 서버 환경이 달라야 한다. 즉 release 용 빌드를 만들 때는 운영 서버를 api end point 로 잡아야 하고, dev 용 테스트 빌드를 만들 때는 개발 서버를 api end point 로 설정해야 한다. 또한 현재 개발하고 테스트 진행 중인 기능들은 release 용 앱에 포함되지 않도록 주의하여야 한다.

releae 용 인지, development 용인지 환경 변수를 설정해야 실수하지 않고 출시용 앱과 디버깅용 앱을 빌드할 수 있다. 리액트에서는 package.json 파일에서 scripts 에 환경 변수를 추가하면 쉽게 사용 가능하다.

package.json
```json
"scripts": {
    "start": "REACT_APP_STAGE=dev react-scripts start",
    "prod": "REACT_APP_STAGE=prod react-scripts start",
    "build": "REACT_APP_STAGE=dev ionic capacitor copy",
    "build-prod": "REACT_APP_STAGE=prod ionic capacitor copy",
    "build-adr": "REACT_APP_STAGE=prod ionic capacitor build android --prod",
    "build-ios": "REACT_APP_STAGE=prod ionic capacitor build ios --prod",
  },
```

위 예제에서 `REACT_APP_STAGE` 라는 환경 변수를 만들었다. 실제로 앱에서 사용하려면 아래와 같이 리액트 환경 변수에 접근할 수 있다. `process.env["REACT_APP_STAGE"]`

constant.ts
```ts
static baseUrl = process.env["REACT_APP_STAGE"] === "prod" ? "https://운영_서버_api_url" : "https://개발_서버_api_url";

static onProd: boolean = process.env["REACT_APP_STAGE"] === "prod" ? true : false;
```
