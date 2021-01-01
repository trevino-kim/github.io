---
title: "Ionic + Capacitor 프로젝트에 코도바 플러그인 및 아이오닉 네이티브 플러그인을 설치하면서 발생하는 문제점"
categories:
- Hybrid App
tags:
  - 모바일앱
  - 프론트엔드개발자 
  - Ionic
  - Capacitor
---

#### 2020/11/11 개발일지
* local notification 플러그인을 capacitor 를 사용하다 로직 작동이 이상한 것 같아 cordova 플러그인으로 변경했으나 capacitor 프로젝트와 연동이 안되어 다시 capacitor 플러그인으로 되돌리는 과정에서 빌드 에러 디버깅 하느라 시간이 많이 소요 되었음. (이틀 정도…)

* Ionic + React + Capacitor  를 활용한 모바일 앱


## 🐞 디버깅

### Ionic + Capacitor 프로젝트에 코도바 플러그인 및 아이오닉 네이티브 플러그인을 설치하면서 발생하는 문제점

💡 알아둬야 하는 점 1: capacitor 프로젝트에 코도바 플러그인을 설치하려면 npm 으로 설치 가능하며 `cordova add plugin` 명령어는 사용 불가능하다.

💡 알아둬야 하는 점 2: capacitor 프로젝트에 코도바 플러그인을 설치하려면 해당 플러그인이 capacitor 와 호환 가능한지 알아보아야 한다. 아래 capacitor 공식 사이트에 예시되어 있는 호환 불가능 플러그인 외에도 capacitor 가 제공하는 기능의 플러그인을 cordova 플러그인으로 설치하는 것은 불가능한 것 같다. 나는 cordova-plugin-local-notification 플러그인을 설치하고자 했지만 결국 호환이 되지 않았다. 설치는 되지만 앱에서 실행이 되지 않는다.

[Known Incompatible Cordova Plugins - Capacitor](https://capacitorjs.com/docs/cordova/known-incompatible-plugins)

	1. Ionic + Capacitor 프로젝트에 Cordova Plugin 을 설치 한 후(아래 설치 커맨드 예시 참고),  안드로이드 스튜디오 빌드 에러 발생:  `cannot find symbol import android.support.v4.app.NotificationManagerCompat;`
	2. 안드로이드 스튜디오 ::Refactor - AndroidX:: 로 변경한 후, 빌드를 하면 다른 에러 발생: `cannot find symbol import androidx.core.util.ArraySet;`
	3. Jetifier 를 설치한 후 에러 없이 빌드 성공! (아래 jetifier 설치 커맨드 참고)
	
< 아이오닉 네이티브, 코도바 플러그인 설치 커맨드 예시 >
```
npm install @ionic-native/core
npm install cordova-plugin-local-notification
npm install @ionic-native/local-notifications
npm install cordova-plugin-device
npm install @ionic-native/device
npm install cordova-plugin-badge
npm install @ionic-native/badge

// 플러그인을 설치한 후 항상 실행해줘야 하는 capacior 명령어
npx cap sync
Ionic cap sync
```

< jetifier 설치 커맨드 >
```
npm install --save-dev jetifier
npx jetify
npx cap sync
```

[jetifier  -  npm](https://www.npmjs.com/package/jetifier)
