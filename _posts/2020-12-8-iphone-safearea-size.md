---
title: "아이폰의 안전 영역 Safe area 픽셀 사이즈 정리"
excerpt: "iPhone X (iPhone 10) 이상 부터 Safe area 라는 것이 있으므로 아이폰의 안전 영역 Safe area 를 고려해야 한다."
header:
  overlay_color: "#1364DE"
  overlay_filter: rgba(0, 0, 0, 0.5)
categories:
- Hybrid-App
tags:
- iOS
- 모바일앱
- React
- Ionic-react
---

#### 2020/12/8 개발 일지
Ionic 하이브리드 모바일 앱에서 iOS 를 개발할 때 iOS safearea 를 고려하여 위치를 설정해야 한다. iPhone X (iPhone 10) 이상 부터 Safe area 라는 것이 새로 생겼기 때문이다.

만약 요소의 위치를 CSS  `position: absolute;`  로 설정하면 top, bottom, left, right 의 위치를 직접 설정해주어야 요소가 자리한다. 이때 아이폰 X 이상 Safe area 가 필요한 폰은 추가로 플러스 패딩을 줘야 자리를 제대로 잡을 수 있다.

### Portrait Mode 세로 모드 안전영역 사이즈
1. top: +50px
2. bottom +40px

### Landscape Mode 가로 모드 안전영역 사이즈
1. left: +44px
2. right: +44px
3. bottom: +25px

![아이폰의 안전 영역 Safe area](/assets/images/2020-12-8-1.png)


### 안전 영역이 필요한지 체크하는 방법
* Ionic-React 프레임워크와 Capacitor 를 사용하는 방법: Capacitor 의 `Device.getInfo()` API 를 사용하여 모바일 플랫폼 종류를 확인하여 만약 `ios` 라면 화면의 길이(Height)를 체크하여 안전 영역이 필요한지 아닌지 세팅할 수 있다.
```ts
const [isNeedSafearea, setIsNeedSafearea] = useState(false)
const getPlatform = async () => {
  const deviceInfo = await Device.getInfo()
  if (deviceInfo.platform === 'ios') {
    if (window.innerHeight > 770) {
      setIsNeedSafearea(true)
    }
  }
}
```

