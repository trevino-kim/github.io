---
title: "리액트 컴포넌트 최적화 방법 useCallback 사용법"
excerpt: "React useCallback 과 React.memo 를 사용하여 함수를  재사용하고 컴포넌트 리렌더링을 방지함으로써 컴포넌트를 최적화하는 방법과 크롬 익스텐션 React Developer Tools 사용법을 간단하게 설명한다."
header:
  overlay_color: "#48CBFA"
  overlay_filter: rgba(0, 0, 0, 0.5)
categories:
- Web
tags:
- 프론트엔드
- React
- Ionic-react
---

<2021년 4월 3일 개발 일지>
### React 의 useCallback 훅 이란?
* 리액트 프레임워크에서 useCallback 이라는 훅이 있다. 컴포넌트가 렌더링 될 때마다 컴포넌트와 관련된 함수가 새로 생성이 되는데, 이때 함수가 업데이트되지 않고 이전에 생성했던 함수를 그대로 사용하고 싶다면 useCallback 훅을 사용하면 불필요한 함수 생성을 방지할 수 있다. 앱의 성능 최적화에 도움을 준다.
* useCallback 을 사용하여 함수를 생성하지 않고 이전의 함수를 그대로 사용하고 싶다면 훅으로 감싸주면 된다.
* `deps` 에는 함수가 업데이트되는 state 또는 prop 값을 추가해야 한다. 아래 예시에서는 inputs 의 값이 변경될 때 마다 onInputChange 의 함수 값이 달라지기 때문에 deps에 inputs 를 추가해준 것 이다.
* 만약 deps 에 inputs 를 넣지 않는다면 onInputChange 함수 내에서 참조하는 모든 값이 함수가 최초에 생성될 때 참고한 e, inputs 값을 가져와서 함수가 실행되기 때문에 정상적으로 작동되지 않을 것이다.
* useCallback 사용 방법 예시


```tsx
const onInputChange = () => {
	// Input 내용이 변경될 때 마다 실행되는 함수
}

// useCallback 으로 감싸기
const onInputChange = useCallback((e) => {
	// Input 내용이 변경될 때 마다 실행되는 함수
	const { name, value } = e.target;
  setInputs({
		...inputs,
		[name]: value
	})
}, [ inputs ])

```

### React.memo 함수 사용법
* React.memo 는 컴포넌트의 prop 이 바뀌었을 때만 리렌더링하고 그렇지 않으면 이전에 기억해둔 컴포넌트를 그대로 사용하도록 해주는 함수이다.
* useCallback 과 함께 사용하면 컴포넌트 내에 함수를  재사용하고 컴포넌트 리렌더링을 방지함으로써 컴포넌트를 최적화할 수 있다.
* React.memo 사용 방법 예시


```tsx
const MyNameCard: React.FC = () => {
	return (
		<div>my name card</div>
	)
}

export default React.memo(MyNameCard);

// 또는 export 를 하지 않는 컴포넌트의 경우에는 React.memo 로 전체 함수를 감싸주면 된다.
const MyNameCardPhoto = React.memo(() => {
	return (
		<div>my name card Photo</div>
	)
})

// 이전 props 의 inputs props 과 새로운 props 의 inputs props 이 같다면 리렌더링 하지 않겠다고 선언하는 방법
const MyNameCard = React.memo(({ inputs }) => {
	return (
		<div>{inputs.name}</div>
	)
})

export default React.memo(MyNameCard, (prevProps, nextProps) => nextProps.inputs === prevProps.inputs);
```

### 크롬 익스텐션 React Developer Tools  
: 컴포넌트 re-rendering 확인하는 방법 useCallback 훅이 제대로 작동하는지 크럼 익스텐션으로 확인할 수 있다.

1. 크롬 브라우저에서 React DevTools 설치 ([React Developer Tools - Chrome Web Store](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en))
2. 크롬 dev tool 열기 (Inspect)
3. React Components 클릭
4. 톱니바퀴 설정 아이콘 버튼 클릭
5. Highlight updates when components render 에 체크
6. 브라우저에서 컴포넌트 테스트를 해보면 컴포넌트가 렌더링 될 때마다 하이라이트 되는 것을 확인할 수 있다.
