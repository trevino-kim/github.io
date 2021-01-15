---
title: "Xcode  Constraints & Alignment 자동으로 레이아웃 설정하는 방법"
excerpt: "Xcode Constraints & Alignment 자동으로 레이아웃 설정하기, Xcode View & Stack View 이해하기"
header:
  overlay_color: "#1364DE"
  overlay_filter: rgba(0, 0, 0, 0.5)
categories:
- iOS
tags:
- Swift
- 모바일앱
---


## Xcode Constraints & Alignment - 자동으로 레이아웃 설정하기
아이폰은 종류에 따라 스크린 사이즈가 다양하고 Portrait 또는 Landscape Orientation에 따라 화면 넓이와 높이가 달라지기 때문에 Xcode 에서 레이아웃을 자동으로 설정해주는 constraints 와 Alignment 를 이해 할 필요가 있다.

## Xcode Constraints
constraints 의 개념은 화면의 크기와 관계 없이 화면의 위, 아래, 오른쪽, 왼쪽에서 항상 지정한 픽셀 숫자 만큼 margin 을 주도록 설정 하는 것이다. 예를 들면, 바탕화면으로 쓰고 싶은 바탕화면 이미지는 어떤 화면의 크기 이든지간에 이미지가 바탕 화면을 100% 가려야 한다. 이때 위, 아래, 오른쪽, 왼쪽 모두 constraints 를 0 픽셀로 주면, 어떤 화면이든지 margin(=0) 없이 바탕화면 이미지가 화면을 꽉 채우게 된다. 바탕화면 이미지를 constraints 설정하기 위해 스토리보드에서 원하는 이미지를 선택하고 화면 오른쪽 아래의 아이콘 중에 lㅁl 처럼 생긴 아이콘을 클릭한다.

constraints 를 원하는 픽셀 숫자(0)와 위치(위, 아래, 오른쪽, 왼쪽)를 클릭하면 아래 화면 처럼 빨간색 바가 실선으로 나타나고, 아래의 Add 4 constraints 버튼을 클릭한다.

아이폰 X 이후 버전은 Safe Area 를 따로 두는데, Safe Area 를 무시하고 앱 화면 전체에 백그라운드 이미지를 넣고 싶다면, Constraints - Tailing 과 Leading 의 Attributes Inspector 에서 설정을 Superview 로 지정하고 Constant 를 0 으로 둔다.

## Xcode Alignment
바탕화면에 로고를 항상 가운데에 두고 싶을 때, 아래의 Alignment 아이콘을 클릭하고 Horizontally in container, Vertically in Container 를 체크하면 어떤 오리엔테이션이든지 어떤 화면 크기이던지 상관없이 항상 화면 가운데에 로고가 나타난다.


## Xcode View & Stack View 이해하기

Stack View 는 하나 이상의 아이템 또는 여러가지 View 를 깔끔히 정렬하고 싶을 때 사용할 수 있다. 아래 사진 처럼 Stack View 내에 여러 개의 View 를 넣고 또 View 안에 Stack View 를 넣어 여러가지 아이템을 정렬할 수 있다.

Stack View 의 Attributes 의 Axis, Distribution, Spacing 을 활용해보자. 특히 Distribution 의 Fill Equally, Equal Spacing 등의 옵션을 활용하면 편하다.

전체 화면 Stack View 의 Constraints 설정은 보통 Safe Area 에서 0 으로 주고, 필요하다면 각각의 View 도 Constraints 와 Alignment 를 적절히 활용하여 원하는 아이템 정렬을 해준다.

View 안에 아이템을 하나(예를 들어 로고 이미지 1개)를 넣고 alignment 를 설정하면 항상 가운데에 로고가 위치하게 된다. 만약 View 안에 이미지가 2개 있다면, 이미지 2개를 또 다른 Stack View 내에 담고 정렬해보자.

View 또는 Stack View 를 설정하고자 한다면 원하는 아이템 또는 여러가지 아이템을 선택(command 키로 여러 아이템 선택 가능)하고 아래 하단의 Embed in View 아이콘 버튼 클릭 후 원하는 View 를 선택한다.

* Tip: View 의 Background 컬러를 Default 로 지정하면 투명하게 설정할 수 있다.

* Tip: 버튼에 width / height constraints 를 설정하면 아래와 같은 노란색 경고가 뜰 수 있다. 만약 버튼의 텍스트가 길어지면 길어진 텍스트는 잘려지고 보이지 않게 된다는 경고문인데, 오른쪽과 같이 Set Constraint to >= Current Width 를 설정하면 위 문제를 해결할 수 있다. (만약 버튼 내에 텍스트가 설정한 width constraint 보다 길어지면 constraint 를 무시하고 텍스트를 모두 표시하도록 설정하는 것이다.)
