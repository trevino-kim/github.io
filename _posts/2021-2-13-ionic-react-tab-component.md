---
title: "아이오닉 리액트 탭 컴포넌트 예제 (깃헙 소스코드 공유)"
excerpt: "아이오닉 리액트 프레임워크에 사용 가능한 탭 컴포넌트 예제 및 깃헙 소스코드 공유 - Ionic React Tab Component"
header:
  overlay_color: "#158BF2"
  overlay_filter: rgba(0, 0, 0, 0.5)
categories:
- Hybrid-App
tags:
- 모바일앱
- Ionic
- React
- Ionic-react
---

## Ionic React Tab Component
현재 아이오닉 UI 프레임워크에서는 한 화면에 2개 이상의 화면을 구성할 수 있도록 하는 탭 컴포넌트 및 탭 뷰 컴포넌트를 지원하지 않는다. 탭을 클릭할 수 있는 Segment 컴포넌트는 지원하지만 탭의 색을 원하는대로 변경하고 탭이 변경되었을 때 뷰가 바뀌는 컴포넌트가 자주 필요했었다. 자주 사용하는 만큼 여러 프로젝트에 쉽게 재사용하기 위해 이번에 탭 컴포넌트와 탭 뷰 컴포넌트를 만들어 깃헙에 소스코드를 공유했다.

### [깃헙 소스코드 및 데모 앱 보기](https://github.com/Jade-Kim/ionic-react-tab-component)

### 아이오닉 리액트 탭 컴포넌트 <TabHeader />

화면 헤더에 고정된(fixed) 탭 헤더를 추가할 수 있는 컴포넌트 `<TabHeader />` 태그

* 필수 Props: titles, selectedTab, onIonChange
* 선택 Props: bgColor, highlight


```ts
interface TabHeaderProps {
  titles: string[]
  selectedTab: string
  onIonChange: Function 
  bgColor?:
      | 'primary'
      | 'secondary'
      | 'tertiary'
      | 'success'
      | 'warning'
      | 'danger'
      | 'light'
      | 'medium'
      | 'dark' 
  highlight?: "light" | "medium" | "dark" = "light"
  [x: string]: any 
}
```

* titles: 모든 탭 제목 이름을 배열로 넣기, 예) ["자기소개서", "이력서", "포트폴리오"]
* selectedTab: 현재 선택한 탭 제목을 state 로 지정하여 넘겨주기
* onIonChange: 탭을 선택했을 때 현재 선택한 탭 제목을 변경하는 setState() 함수로 지정하기
* bgColor?: 탭 배경 색을 지정하고자 할 때
* highlight?: 선택된 탭의 글자 색을 지정하고자 할 때, 디폴트 값은 "light"
* [x: string]: `<ion-segment>` tag 에 추가로 넣을 모든 props 를 적용 가능함



헤더 배경색이 없는 탭은 아래와 같이 구성할 수 있다.

```ts
<TabHeader
    titles={["탭 화면 1", "탭 화면 2", "탭 화면 3"]}
    selectedTab={basicTab}
    onIonChange={(e) => setBasicTab(e.detail.value)}
/>
```


헤더 배경색과 선택된 탭 글자 색을 변경하고 싶다면 선택 Props 를 넣으면 된다.

```ts
<TabHeader
    titles={["탭 화면 1", "탭 화면 2", "탭 화면 3"]}
    selectedTab={colorTab}
    onIonChange={(e) => setColorTab(e.detail.value)}
    bgColor="primary"
    highlight="medium"
/>
```


### 아이오닉 리액트 탭 컴포넌트 <TabView />

탭을 클릭할 때 마다 어떤 화면을 보여줄지 결정하는 컴포넌트 `<TabView />` 태그

필수 Props: show, children

```ts
show: boolean
children: React.Component
```

* show prop 에는 언제 화면을 보여주어야 할 지 불리언으로 정해주면 된다. 현재 선택된 탭 이름을 state 로 두고 탭 제목과 탭 뷰가 일치할 때에만 해당 뷰를 보여준다.
* children prop 에는 아래와 같이 실제로 해당 탭을 클릭했을 때 보여주고 싶은 컴포넌트를 넣는다.

```ts
<TabView show={현재선택된탭이름 === "탭 화면 1"} children={<TabViewOne />} />
<TabView show={현재선택된탭이름 === "탭 화면 2"} children={<TabViewTwo />} />
<TabView show={현재선택된탭이름 === "탭 화면 3"} children={<TabViewThree />} />
```


실제 페이지에서 탭 컴포넌트를 적용하려면 아래와 같이 사용할 수 있다. [전체 소스코드 보기](https://github.com/Jade-Kim/ionic-react-tab-component/blob/master/src/pages/ColorTab.tsx)


```ts
<IonPage id="color-tab-page">
  <TabHeader
    titles={titles}
    selectedTab={colorTab}
    onIonChange={(e) => setColorTab(e.detail.value)}
    bgColor="tertiary"
    highlight="light"
  />

  <IonContent fullscreen={true}>
    <TabView show={colorTab === titles[0]} children={<TabViewOne />} />
    <TabView show={colorTab === titles[1]} children={<TabViewTwo />} />
  </IonContent>
</IonPage>
```


### [깃헙 소스코드 및 데모 앱 보기](https://github.com/Jade-Kim/ionic-react-tab-component)