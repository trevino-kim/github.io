---
title: "Xcode 프로젝트 생성 및 아이폰 앱 테스트하는 방법"
excerpt: "PC로 Xcode iOS 개발하는 방법, Xcode 프로젝트 git clone 하는 방법"
header:
  image: /assets/images/2019-10-21.jpg
  teaser: /assets/images/2019-10-21.jpg
categories:
    - iOS
tags:
    - 모바일앱
    - Xcode
---

##### 2019년 10월 21일 개발 일지

### Xcode 프로젝트 생성하는 방법
Create a new Xcode project 선택 또는 [ File - New - Project ] 선택 후 iOS 탭의 Single View App 템플릿을 선택한 후 아래를 참고하여 Xcode 프로젝트를 생성한다.

* Product Name: 앱 이름
* Organization Identifier: com.도메인
* 아직 운영하는 웹 사이트 도메인이 없다면 com.jade.kim 처럼 본인의 이름을 넣던지 해서 organization identifier를 지정하면 된다. unique 하기만 하면 상관없다.
* Bundle Identifier: com.도메인.ProductName
* Language: Swift
* User Interface: Storyboard


### Xcode 프로젝트 git clone 하는 방법
Xcode 런칭 화면에서 clone an existing project 클릭 또는 Source Control - Clone 클릭한다. git hub project 주소를 복사하여 붙여넣은 후 clone 버튼을 클릭하면 프로젝트를 어느 폴더에 저장할 것인지 지정하면 프로젝트 클론 된다.

### PC로 Xcode iOS 개발하는 방법
Windows PC 로 Xcode 를 설치하거나 iOS 를 개발할 수 있을까?

* macincloud: 맥을 클라우드에 저장해서 사용하는 방법
* Hackintosh: Dual Boot/iATKOS, VMWare, Delphi XE4 (hackintosh.com)

위의 방법으로 iOS 개발과 Xcode 를 사용한다면 테스트 과정에서 아이폰으로 직접 테스트 해볼 수는 없고, 시뮬레이터로만 테스트 가능하다.

위 방법은 셋업 하기 복잡할 수 있고 버그도 많기 때문에 정말 마지막에 최후의 수단으로 쓸 수 있다. 하지만 제대로 iOS 를 개발하고자 한다면 Mac 을 구입하여 투자하는 것을 추천한다. 맥은 최신 사양을 구매할 필요는 없고, 2-3년 전의 중고를 구입하면 저렴하게 투자하여 시작할 수 있다. 맥을 구입하면 가장 최신 버전의 맥 OS 로 업데이트 하고 Xcode 를 사용하자.

::macOS 맥 버전 찾는 방법은? 왼쪽 상단의 애플 아이콘 - About This Mac::



### Xcode 로 아이폰 앱을 테스트하는 방법
Xcode 로 앱을 만들고 Simulator 로 간단하게 테스트 할 수 있지만, 더 정확한 앱 테스트를 위해 아이폰 디바이스에 직접 테스트 앱을 설치하고 앱 기능들을 테스트 할 수 있다. 물론 Simulator 로 테스트 해도 되지만 하이브리드 앱 개발 경험상, 시뮬레이터에 존재하지 않는 에러가 디바이스에 뜨기도 하고, 디바이스에 없는 에러가 시뮬레이터에 나타나기도 해서 디바이스에 테스트해보는 것이 더 믿을만 한 것 같아 디바이스 테스트를 추천한다.


1. Xcode 버전과 디바이스 iOS 버전을 체크한다. 디바이스 OS 버전이 Xcode 보다 항상 높아야 한다.(ex: Xcode 11.1 v / iOS 13) 팁은 평소에 Xcode 와 디바이스 모두 항상 최신 버전의 iOS 로 업그레이드 하고 사용하면 문제없이 사용할 수 있다.
	* Xcode 버전 체크하는 방법: Xcode - About Xcode
	* 아이폰 디바이스 체크하는 방법: Settings - General - About - Software Version
2. Apple Developer 계정을 추가한다. 기존에 사용하던 무료 애플 계정도 사용할 수 있다.
	* Xcode - Preferences - Accounts - 왼쪽 하단의 + 버튼 - Apple ID
3. 앱 등록 하기(sign the app)
	* Project 폴더 클릭 - TARGETS - Signing & Capabilities - Team - Add an account 에 계정을 추가한다.
4. 아이폰 USB 케이블을 맥과 연결한 후 알림이 뜨면 Trust 신뢰하기를 누른다.
5. Xcode 화면 상단 좌측에 simulators 버튼(ex: iPhone 11)을 클릭하고 본인의 맥에 연결된 디바이스를 선택한 후 왼쪽의 플레이(Run) 버튼을 누른다.

**App is busy 라는 메세지가 뜨면 2-15분 정도 기다린 후 자동으로 앱 설치 됨**

이렇게 처음에 애플 계정을 등록하고 앱 등록을 하면, 그 이후에는 Xcode 화면에서 디바이스를 선택한 후 Run 버튼을 누르기만 하면 된다.

#### 와이파이로 연결하기
Cable 을 이용하지 않고 Wireless 로 Device 테스트 하는 방법도 있다. 먼저 위의 절차를 모두 시행하고, 테스트 할 디바이스를 선택한다. Window - Device and Simulators 를 클릭하면 연결된 디바이스를 확인할 수 있다. connect via network 에 체크 하면 아이폰 디바이스와 맥이 같은 와이파이를 사용하고 있을 때에 Wireless 로 앱 run 이 가능하다.
