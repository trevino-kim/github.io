---
title: "아이오닉 앱 스크롤 먹통 문제점 해결"
excerpt: "문제점: 모바일 화면 스크롤이 on & off 로 되다/안되다 하는 현상"
header:
  overlay_color: "#158BF2"
  overlay_filter: rgba(0, 0, 0, 0.5)
categories:
    - Hybrid-App
tags:
    - 모바일앱
    - 프론트엔드
    - Ionic
    - Capacitor
---

##### 2019년 10월 31일 개발 일지

### 📱Capacitor 프레임웍을 이용하여 하이브리드 모바일 앱 CartLogic 을 개발중에 있다.

### ❗문제점 발견: 모바일 화면 스크롤이 on & off 로 되다/안되다 하는 현상.
: 하이브리드로 제작한 앱을 아이폰으로 빌드하여 사용해보니 모바일 스크롤이 잘 되다가 갑자기 안되기도 하고, 겉으로 느끼기에는 불연속적으로 스크롤이 먹통 되는 것 처럼 보였다. 하지만 계속 앱을 만지작거리고 기능들을 사용해보면서 문제의 원인이 무엇인지 알게되었다.

#### 💬문제점 이유: input 사용자 입력란 또는 select 선택을 하면  iOS 키보드가 자동으로 나타나게 되는데, 키보드를 오픈한 후 닫으면 스크롤이 먹통되는 것이다.

#### 🐞문제 해결 방법: 모바일 키보드는 네이티브 앱 플러그인 Capacitor 에서 기능이 연동되므로 바로 Capacitor 문서의 키보드 API 를 확인해보았다. setScroll 이라는 api 가 있는데, 이를 disabled true/false 를 지정할 수 있었다.

### 🔑setScroll
```
setScroll(options: { isDisabled: boolean }): Promise<void>
Programmatically enable or disable the WebView scroll
options { isDisabled: boolean }
returns: Promise<void>
```

https://capacitor.ionicframework.com/docs/apis/keyboard

아마도 디폴트 세팅이 `isDisabled: true` 라고 되어있는 모양이다. 키보드를 닫기 전에 ::setScroll 을 isDisabled: false 로 설정::하여 스크롤 먹통 문제를 해결했다.

``` ts
// app-root.tsx 파일에서 capacitor keyboard 플러그인을 불러온 후,
import { Plugins } from '@capacitor/core';
const { Keyboard } = Plugins;

// componentWillLoad() 라이프 훅에 아래 코드를 추가했다.
Keyboard.addListener('keyboardWillHide', () => {
      Keyboard.setScroll({ isDisabled: false });
    });
```
