---
title: "안드로이드 네이버 지도 API 에러 - https 보안 정책"
excerpt: "안드로이드 9.0 이상에서 http평문통신을 허용하지 않고 https만 허용하는 보안정책이 있어 networkSecurityConfig 파일을 생성하여 예외처리를 해주어야 한다."
header:
  overlay_color: "#15F215"
  overlay_filter: rgba(0, 0, 0, 0.5)
categories:
- Hybrid-App
tags:
- 안드로이드
- 네이버 API
- 디버깅
---

#### 2020/12/28 개발일지
주요 문제점은 ::안드로이드 9 이상에서 네이버 지도 API 에러::였고 해결한 과정은 아래와 같다.

### 처음 내가 생각했던 문제점: 안드로이드 특정 기기에서 특정 기능이 먹통으로 지원 되지 않음

1. 갤럭시 s6, s7 에서는 구동이 잘 되었고 갤럭시 노트 9 에서 구동되지 않음을 확인하였고, 추후 갤럭시 s9 Plus 에서도 구동이 되지 않는 것을 확인하였다.
2. 따라서 안드로이드 특정 디바이스에서만 에러가 뜨는 것이 아님을 확인하였고 각 디바이스의 안드로이드 소프트웨어 버전을 확인해보았다.
3. 구동에 문제 없었던 갤럭시 s6, s7 는 안드로이드 8.0.0 오레오 였고, 구동 에러가 난 디바이스는 비교적 최신으로 안드로이드 10.0.0 인 것으로 확인했다.
4. 안드로이드 스튜디오 에뮬레이터에서 8.0.0 과 10.0.0 인 AVD 를 각각 설치하고 구동해보니 역시 8.0.0 은 구동이 되었고 10.0.0 은 구동되지 않았다. 구동되지 않는 이유는 네이버 지도 api 에 오류가 있는 것을 안드로이드 스튜디오 디버그 콘솔을 통해 확인하였다.

`Error Code 500 / Internal Server Error (내부 서버 오류)`
`일시적인 서비스 오류입니다. 잠시 후 다시 시도해 주세요.`
`NAVER Maps JavaScript API v3`
![안드로이드 네이버 지도 API 에러](/assets/images/2020-12-28-1.jpg)

5. 따라서 버전에 따른 문제점이라는 것을 확인하였고 네이버 지도 api 를 적용하는 과정에서 문제가 발생한 것이었다.
6. Naver 개발자 공식 문서 확인 및 여러가지 관련된 문제를 서칭해보았다.
7. 하이브리드 앱은 웹 서비스 url 에  `location.href` 을 넣어주어야 한다고 해서 앱에서 href 확인해보고 네이버 개발자 콘솔에서 등록한 web 서비스 url 을 확인해보았지만 모두 등록된 url 이었다. `http://localhost`
8. 그러므로 웹 서비스 url 등록 문제는 아니라고 판단했다.

### 다시 제대로 파악한 문제점: 안드로이드 10.0.0 이상에서 네이버 지도 기능이 먹통되는 현상

1. 안드로이드 9 이상에서 http평문통신을 허용하지 않고 https만 허용하는 보안정책이 있어 예외처리를 해주어야 한다는 것을 확인했다.
2. `networkSecurityConfig` 파일을 생성하고, AndroidManifest 에 등록하는 방법으로 해결하였다.

### network_security_config.xml 생성하기
```xml
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <domain-config cleartextTrafficPermitted="true">
        <domain includeSubdomains="true">map.naver.com</domain>
        <domain includeSubdomains="true">map.naver.net</domain>
    </domain-config>
</network-security-config>
```

### AndroidManifest.xml 수정하기
```xml
...
<application
	android:networkSecurityConfig=“@xml/network_security_config”
	... >

</application>
```
![안드로이드 네이버 지도 API 에러](/assets/images/2020-12-28-2.jpg)


### 네이버 지도 로드 성공한 화면 스크린샷
![안드로이드 네이버 지도 API 적용한 화면](/assets/images/2020-12-28-3.jpg)
