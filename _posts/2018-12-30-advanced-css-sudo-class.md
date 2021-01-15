---
title: "CSS 고급 셀렉터 pseudo 클래스"
excerpt: "CSS 고급 셀렉터와 수도 클래스를 알아보자."
header:
  overlay_color: "#F2E315"
  overlay_filter: rgba(0, 0, 0, 0.5)
categories:
- Web
tags:
- 웹개발
- 프론트엔드
---



# CSS 고급 셀렉터 CSS3 Advanced Selectors and pseudo class


```
<style>
  div p {   } // div 내의 모든 p 선택
  h3 - p {  } // h3가 포함되어 있는 div 내의 모든 p 선택
  h3 + p {  } // h3가 포함되어 있는 div 내의 첫번째 p 선택
</style>

<div>
  <p>a</p>
  <p>b</p>
  <p>c</p>
</div>

<div>
  <h3>H3 heading</h3>
  <p>d</p>
  <p>e</p>
  <p>f</p>
</div>

```


* div p {   } // div 내의 모든 p 선택: a,b,c,
* h3 - p {  } // h3가 포함되어 있는 div 내의 모든 p 선택: d,e,f
* h3 + p {  } // h3가 포함되어 있는 div 내의 첫번째 p 선택: d


```
<style>
  a[target] {   } // a 의 target attribute 가 있는 모든 a 선택
  a[href*=“google”] {   } // a 의 href attribute 가 google 이 포함되어 있는 모든 a 선택
</style>

<div>
  <a href=“” target=“_blank”> target blank1 </a>
  <p>b</p>
  <a href=“http://www.google.net”> google.net </a>
</div>

<div>
  <h3>H3 heading</h3>
  <a href=“http://www.google.com”> google.com </a>
  <p>e</p>
  <a href=“” target=“_blank”> target blank2 </a>
</div>

```


* a[target] {   } // a 의 target attribute 가 있는 모든 a 선택: target blank1, target blank2
* a[href=“google”] { } // a 의 href attribute 가 google 이 포함되어 있는 모든 a 선택: google.net, google.com

* *=    : begin with
* $=    : end with
* -=     : has the value between two spaces
* |=      : has the value separated by hyphens (-)


# pseudo class 수도 클래스

```
<style>
  a:hover { text-decoration: none; }
  input:focus { background-color: blue; }
  input:enabled {}
  input:disabled {}
  input:checked {}

  p:first-child {} //각 div 의 첫번째 p element를 선택
  p:last-child {} //각 div 의 마지막 p element를 선택
  p:only-child {} //각 div 내에 p 하나만 있는 p element를 선택
  p:first-of-type {} //각 div 의 첫번째 p 타입을 선택
  p:last-of-type {} //각 div 의 마지막 p 타입을 선택
  p:only-of-type {} //각 div 내에 p 하나만 있는 p 타입을 선택

  tr:nth-child(2n) {} //테이블의 짝수 행 선택
  tr:nth-child(2n-1) {} //테이블의 홀수 행 선택
  tr:nth-last-child(2n-1) {} //테이블 뒤에서 부터 카운트
  tr:nth-of-type {} //특정한 타입만 선택

  div:empty { display: none; } //아무 것도 없는 div 는 보여주지 않기
  p:not(.green) {} //green 클래스가 아닌 모든 p 선택
  :not(div) {} //div가 아닌 모든 개체 선택

  p:first-letter {}
  p:first-line {}

  a:after { content: attr(href); }
  a:after { content: “I am a link”; }
  a:before {}

</style>
```
