---
title: "리액트 useEffect 사용법"
excerpt: "React useEffect 를 사용하여 메인 화면을 클릭 할 때 마다 함수 실행하기, 로그인 상태가 변경될 때 마다 특정 함수 실행하기"
header:
  teaser: /assets/images/2021-1-3.jpg
  overlay_image: /assets/images/2021-1-3.jpg
  overlay_filter: rgba(0, 0, 0, 0.5)
categories:
    - Hybrid-App
tags:
    - 프론트엔드
    - React
    - Ionic-react
---

### React 의 useEffect 훅 이란?
* 리액트 프레임워크에서 useEffect 라는 아주 유용한 훅이 있다. 컴포넌트가 화면에 나타날 때, 사라질 때, 업데이트 될 때 다시 렌더링을 해주는 함수이다.
* 리액트에서 컴포넌트를 작성할 때 크게 2가지를 사용하는데 클래스형 컴포넌트와 함수형 컴포넌트이다. 클래스형 컴포넌트에서 사용하는 `componentDidMount, componentWillUnmount, componentDidUpdate` 라이프 사이클 대신에 함수형 컴포넌트에서는 `useEffect` 을 사용한다.
* useEffect 사용 방법 예시
  
```tsx
useEffect(() => {
	// componentDidMount
	// 컴포넌트가 화면에 나타날 때 실행하고 싶은 함수를 이 곳에 넣는다.
  return () => {
	// componentWillUnmount
	// 컴포넌트가 화면에 사라질 때 실행하고 싶은 함수를 이 곳에 넣는다.
	// 클린업 함수 라고도 한다.
	}
}, [state1, prop1]) // componentDidUpdate
```

* [] 배결을 deps 배열이라고 하며 이 배열 안에 추가한 state 또는 prop 이 변경될 때 마다 useEffect 훅이 실행된다.
* `deps` 배열을 비워서 `[]` 처리하면 컴포넌트가 맨 처음 화면에 나타날 때만 useEffect 함수가 호출되며 `deps` 를 아예 생략해버리면 컴포넌트가 렌더링 될 때마다 호출 된다.
  
```tsx
useEffect(() => {
	// componentDidMount
	// 컴포넌트가 렌더링 될 때마다 호출하고 싶은 함수를 이 곳에 넣는다.
  return () => {
		// componentWillUnmount
	}
})
```

#### 2021년 1월 3일 개발 일지
`useEffect` 훅을 여러 개 사용하면 된다는 것을 왜 생각하지 못했을까? 처음에는 이걸 깨닫지 못하고 하나의 `useEffect` 훅에 여러 개의  `deps` 를 끼워넣다 보니 불필요하게 다른 함수가 재실행되는 문제점이 있었다. 특정 state 가 변경될 때 마다 특정 함수를 실행하려면 아래와 같이 `useEffect` 훅을 여러 개 사용하고 `deps`를 각각 지정하면 된다.

아래는 메인 화면을 클릭 할 때 마다 실행되는 useEffect 함수와 user 의 isLoggedin 프로퍼티가 변경될 때 마다 실행되는 함수 예시이다. user 는 앱 전역의 state 로 설정 되어있다.

```tsx
  useEffect(() => {
    if (location.pathname === '/main') {
      console.log('메인 화면을 클릭 할 때 마다 실행되는 함수')
    }
  }, [location.pathname])

  useEffect(() => {
	  // user 의 isLoggedin 프로퍼티가 변경될 때 마다 실행되는 함수
    if (user.isLoggedin) {
		// user 의 isLoggedin 프로퍼티가 true 일 때 마다 실행되는 함수
		loadUserData()
	  }
  }, [user.isLoggedin])

```
