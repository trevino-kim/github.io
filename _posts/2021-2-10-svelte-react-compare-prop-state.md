---
title: "Svelte 와 React 차이점 - Prop, 상태관리, 컴포넌트 만드는 방법"
excerpt: "Svelte 와 React 차이점, Prop, State, if else for 문 작성하는 방법, 상태관리, 컴포넌트 만드는 방법"
header:
  overlay_color: "#7515F2"
  overlay_filter: rgba(0, 0, 0, 0.5)
categories:
- Web
tags:
- 웹개발
- 프론트엔드
---



### Svelte Prop 사용법
: 부모 파일에서 자식 컴포넌트를 import 하고 prop 을 넘겨준다. 리액트와 동일한 방식이다.

```html
// Parent.svelte
<script>
	import Child from '/Child.svelte';
</script>

<Child prop_title={title} />
```

다른 점은 자식 파일에서는 해당 prop 이름을 export 해주어야 하는 것이다.

리액트에서는 자식 컴포넌트 전체를 export 하여 여러가지 미사여구를 많이 붙여야 하는 단점이 있는데 스벨트는  아래 코드에서 보다시피 굉장히 단순하고 코드도 적고 보기에 깔끔하다.

```html
// Child.svelte
<script>
	export let prop_title;
</script>

<h1>{prop_title}</h1>
```




### Svelte State 사용법
: 아래 코드에서 items 는 export 했으므로 부모 컴포넌트에서 prop 으로 받아오는 변수이다. 이 prop 을 상태로 바인딩하려면 `$: 상태이름 = 함수` 이런식으로 사용할 수 있다. 스벨트에서  `$: ` 표시가 state 로 관리하겠다고 선언해주는 부분이다. html 에서는 `${상태이름}` 으로 표기하면 상태가 바뀔때마다 화면에서 값이 바뀐다.

리액트에서는 `useState()`를 사용하는데, `const [isTrue, setIsTrue] = useState(true)` 이런 식으로 상태 관리를 하는데, 항상 상태 변수와 상태를 변경하는 set 변수를 따로 기입해줘야해서 코드가 길어지는 불편함이 있다. (이외에도 리액트에서 상태 관리하는 다른 방법이 있으나 위 방법이 가장 간단한 방식인 것 같다.)


### if else for 문
: 스벨트에서 if/else/for 문 등은 템플릿 엔진과 비슷한 방식이다. 예를 들면 if 문은   `{#if }`로 열고 `{/if} ` 로 닫아주어야 한다. For 반복문은 `{#each items as item}` `{/each}` 으로 사용한다.

```html
// Child.svelte
<script>
	export let items;
	$: state_total = items.reduce((sum, currentValue) => {
		return sum + currentValue.price;
	}, 0)
</script>

{#if items.length === 0}
	<p>No items</p>
{:else}
	{#each items as item}
		<h1>{item.title} - ${item.price}</h1>
	{/each}
	<h1>TOTAL: ${state_total}</h1>
{/if}
```




### Svelte 컴포넌트 만들어서 사용하는 법
: 스벨트에서는 아주 적은 량의 코드로 컴포넌트를 만들고 사용할 수 있다. Button 이라는 스벨트 컴포넌트를 만들어 사용하고자 한다면, Button.svelte 파일을 생성하고 컴포넌트를 작성하는데, 이때 넘겨주고 싶은 클릭 이벤트는 버튼 태그 내에 `on:click` 이라고 명시만 해주면 된다.

그리고 버튼 컴포넌트를 사용하고자 하는 파일에서 컴포넌트를 import 하고 `import Button from './Button.svelte';`, 해당 컴포넌트를 사용하면 된다.  `<Button on:click={add}>Add</Button>`

리액트에서는 click 같은 이벤트들은 prop 으로 따로 명시하고 넘겨주어야 하는데 스벨트에서는 `on:click` 과 같이 html 태그에 붙이기만 하면 되는 아주 간단한 방식으로 컴포넌트의 이벤트를 넘겨받을 수 있다.


```html
// Button.svelte
<style>
	// button style here
</style>

<button on:click>
	</slot>
</button>

// Child.svelte
<script>
	import Button from './Button.svelte';
	export let prop_title;

	const add = (e) => {
		console.log(e);
	}
</script>

<h1>{prop_title}</h1>
<Button on:click={add}>Add</Button>
```
