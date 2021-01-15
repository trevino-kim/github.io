---
title: "자바스크립트 돔 이란 DOM ?"
excerpt: "자바스크립트 돔 DOM - Document Object Model 에 대  알아보자."
header:
  overlay_color: "#F2E315"
  overlay_filter: rgba(0, 0, 0, 0.5)
categories:
- Web
tags:
- 웹개발
- 프론트엔드
---

# 자바스크립트 DOM - Document Object Model

JavaScript 를 HTML + CSS 와 결합해야 인터렉티브한 웹사이트를 만들 수 있다.
JavaScript 와 HTML + CSS 를 연결해 주는 것이 DOM 이다.

DOM 은 Document Object Model 의 약자이다. 모든 HTML 태그는 document 라는 자바스크립트 object 안에 저장되어 있다. 그러므로 자바스크립트에서 HTML 을 object 로 불러올 수 있다.

자바스크립트에서 HTML 과 CSS 를 연결하여 실행하려면, element를 Select(선택)  하고 manipulate(이용하다, 다루다) 한다. 예를 들어  태그를 선택하여 bodyVar 변수에 저장하는 방법은 아래와 같다.


`var bodyVar = document.querySelector("body")`
﻿
### DOM Selectors - document 객체 선택자

* element를 선택하는 Methods

```
// 하나뿐인 ID를 가진 element 하나를 선택하고자 할 때,
document.getElementById()

// 같은 Class 또는 Tag 이름을 가진 element 여러 개를 선택하고자 할 때
document.getElementsByClassName()
document.getElementsByTagName()
document.querySelector()
document.querySelectorAll()
```

**주의할 점은 Node List 를 Array 처럼 생겼지만 Array 와는 다르다. 노드 리스트(node list)는 Array 와 마찬가지로 각 element 들이 index 를 가지고 있고, length method 를 이용할 수 있지만 forEach method 등의 다른 method 는 이용할 수 없다.  그 이유는 node list 는 모든 node type 을 가질 수 있고, Array 는 element node 만을 데이터로 가질 수 있기 때문이다.**

```
document.getElementsByClassName()
document.getElementsByTagName()
```

이 2가지 selectors 로 element 를 선택하면, 선택한 element 가 가지고 있는 엄청난 양의 모든 nodes 와 child nodes 등을 return 한다. Node List 전체를 forEach loop 하고 싶다면 for/while loop 문을 사용하면 된다.

```
var myNodeList = document.querySelectorAll("img");

for(var i = 0; i < myNodeList.length; i++) {
  myNodeList[i].style.background = "pink";
}
​
```



쿼리셀렉터 `document.querySelector()` 는 선택한 selector 의 첫번째 element 를 return 한다.

```
document.querySelector()
document.querySelector("CSS-style selector")

document.querySelector("#IDname")
document.querySelector(".ClassName")
document.querySelector("TagName")

```

CSS 에서 사용 가능한 거의 모든 Selector 를 사용할 수 있다. 예를 들어, li 태그 내에 있는 모든 a 태그의 모든 myClass 클래스이름 element 를 선택하려면,

`document.querySeletor("li a.myClass")`
​

쿼리셀렉터올 document.querySelectorAll() 는 선택한 selector 의 모든 element list 를 return 한다.

`document.querySelectorAll()`

---

### DOM Manipulation document 객체 다루기

* CSS Style 추가/변경하기: .style.속성이름 = "";

```
var myID = document.getElementById("IDname");

myID.style.color = "blue";
myID.style.border = "10px solid red";
myID.style.backgroundcolor = "blue";
myID.style.fontSize = "100px";
myID.style.marginTop = "200px";
```




* classList 로 CSS Style 더하는 방법: .classList.add("클래스이름")
* CSS Style 제거하는 방법: .classList.remove("클래스이름")
* CSS Style 자동으로 추가/제거하는 방법: .classList.toggle("클래스이름")

```
/* 먼저 CSS 파일에 class 를 정의한다. */
.newClass {
  color: blue;
  border: 10px solid red;
}
 var myID = document.getElementById("IDname");

// 자바스크립트로 선택한 element 에 새로운 class 를 더하거나 제거한다.
myID.classList.add("newClass")
myID.classList.remove("newClass")

myID.classList.toggle("newClass")
```

토글 사용 예로 체크박스를 선택하면 체크되고, 한번 더 선택하면 체크 해제 되는 버튼 만들 때 유용하다.

**※ classList는 array 가 아니다.**

​

* 텍스트 내용 선택/변경하기: .textContent = "";

```
<p> I <strong>love</strong> you! </p>

var loveU = document.querySelector("p");
loveU.textContent // "I love you!"
loveU.textContent = "I love you too!"
// <p> I love you too! </p>
```

textContent 는 텍스트 내용물만 선택하며, 만약 textContent 로 텍스트 컨텐츠를 업데이트 할 경우 HTML 속성은 모두 다 사라져 버린다. 대신 innerHTML 을 사용할 수 있다.

​
* .innerHTML

```
<p> I <strong>love</strong> you! </p>

var loveU = document.querySelector("p");
loveU.innerHTML // "I <strong>love</strong> you!"
loveU.innerHTML = "<p>I <strong>love</strong> you too! </p>"
// <p> I <strong>love</strong> you too! </p>
```




* Attributes 선택하기: .getAttribute("attribute이름");
* Attributes 변경하기: .setAttribute("attribute이름", "변경할 내용");

​
```
document.querySelector("a").getAttribute("href");
document.querySelector("a").setAttribute("href, "http://www.google.com");

document.querySelector("img").getAttribute("src");
document.querySelector("img").setAttribute("src, "abc.png");
```



### DOM events

버튼을 클릭한다, 사진 또는 링크를 호버하면 오버레이 효과가 나타난다, 드래그 앤 드랍, 엔터키를 누른다, 등등…

element 를 선택하고 event listener 를 추가하여 실행할 수 있다. ​addEventListener 라는 method 를 이용하며 Syntax는 아래와 같다.

```
element.addEventListener("type", fuctionToCall);

var button = document.querySelector("button");
button.addEventListener("click", function() {
  console.log("You clicked the button!");
});

button.addEventListener("mouseover", function() {
  console.log("Mouseover affect!");
});

button.addEventListener("mouseout", function() {
  console.log("Mouseout affect!");
});
```
 ​
이 밖에 더 다양한 event 타입 종류는 아래 웹사이트에서 확인 가능하다.  

[자바스크립트 이벤트 타입 종류](https://developer.mozilla.org/ko/docs/Web/Events)
