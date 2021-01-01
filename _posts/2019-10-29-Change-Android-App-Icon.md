---
title: "안드로이드 앱 아이콘 변경하는 방법 및 디버그용 APK 생성하는 방법"
header:
  image: /assets/images/2019-10-29.png
categories:
    - Android
tags:
    - 모바일앱
    - 안드로이드 스튜디오
---

##### 2019년 10월 29일 개발 일지

**Image Assets Studio 를 오픈하여 앱 아이콘, 푸시 알림 아이콘 등을 설정할 수 있다.**
* 안드로이드 스튜디오 프로젝트 오픈
* 왼쪽 상단의 Android 뷰 선택
* app - res 폴더 우클릭 - New - Image Asset 선택
* Launcher Icons - 아이콘 path 선택

![안드로이드 앱 아이콘 변경하는 방법](/assets/image/2019-10-29-1.png)

더 자세한 내용은 [안드로이드 개발자 홈페이지](https://developer.android.com/studio/write/image-asset-studio)를 참고할 것.


* Splash Screen 스플래스 스크린 이미지 변경하려면, Android 프로젝트 폴더 - app - src - main - res 폴더에서 splash screen 이미지 변경하기



### APK 파일 이란?
APK 는 Android Application Package의 약자로 안드로이드 운영체제에 사용되는 파일 포맷이다. 앱 개발이 끝나고 퍼블릭으로 보낼 때 안드로이드 스튜디오에서 프로젝트를 컴파일하고 APK 파일로 패킹한다. APK 파일 안에는 모바일 앱을 설치하는 패키지, 모든 프로그램 코드, 리소스, manifest 파일, certificate, assets 가 포함되어 있고 안드로이드 운영체제에 설치될 수 있다.

### 안드로이드 스튜디오에서 개발자 디버그용 APK 파일을 생성하는 방법
1. 안드로이드 스튜디오에서 프로젝트 폴더를 연다.
2. Build - Build APK 를 클릭한다.
3. APK 가 생성되면 오른쪽 하단에 아래와 같은 알림이 뜨는데 locate 를 선택한다.
4. 폴더에 개발자 테스트를 위한 apk 파일이 생성된 것을 확인할 수 있다.
