---
title: "Capacitor Local Notifications 을 세팅하면서 마주한 문제점 해결"
excerpt: "문제점: iOS 에서 LocalNotifications 가 실행되지 않음"
header:
  image: /assets/images/2020-11-24.jpg
  teaser: /assets/images/2020-11-24.jpg
categories:
    - Hybrid-App
tags:
    - 모바일앱
    - 프론트엔드
    - Ionic
    - Capacitor
---


## 문제점: iOS 에서 LocalNotifications 가 실행되지 않음
* 먼저 Android 에서 모든 LocalNotifications 관련 로직을 테스트 및 디버깅 완료하고 iOS 테스트를 진행하였더니 알람이 아예 셋팅되지 않았다.
 
* 로컬 알림을 세팅하기 전에 `requestPermission()` 을 먼저 하고 `granted` 받은 다음에 진행해야 한다. 특히 iOS 에서 permission 허가를 받지 않으면 로컬 알림은 아예 설정되지 않는다.

* LocalNotification Object 를 생성할 때 Android / iOS 를 각각 다르게 설정해야 하는 Properties 가 있으므로 주의해서 작성한다. 예를 들면 아래의 프로퍼티 이름은 두 플랫폼이 각각 다르다.

iOS 만 적용 되는 프로퍼티
```
threadIdentifier: string // 지역 로컬 알림 그룹 이름
summaryArgument: string // 지역 로컬 알림 그룹 내용
```

Android 만 적용 되는 프로퍼티
```
group: string // 지역 로컬 알림 그룹 이름
groupSummary: boolean // 지역 로컬 알림 그룹의 summary 로 설정할지 여부
channelId: string // 지역 로컬 알림 채널 이름
```


* iOS 에서는 Channel 자체를 사용할 수 없기 때문에 Channel 과 관련된 모든 methods 는 사용 불가하다. `createChannel(), deleteChannel(), listChannels()` 모두 iOS 에서 사용할 시 에러 발생한다. Capacitor 공식 홈페이지에 LocalNotification 인터페이스를 보면 플랫폼 별로 사용가능한 프로퍼티가 나와있지만, api methods 엔 언급되어 있지 않아서 조금 헤맸었던 부분이다.

