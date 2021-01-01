---
title: "GS인증을 위한 XSS 라이브러리 조사 - dompurify"
categories:
  - Hybrid_App
tags:
  - 프론트엔드 
  - 프론트엔드개발자 
  - Frontend 
  - Developer 
  - Ionic
  - React
---

#### 2020/11/19 개발일지
GS인증 관련 - XSS 라이브러리 조사 - dompurify 설치 및 적용 https://www.npmjs.com/package/dompurify

XSS attack 관련:
    - Ionic 프레임웍에서 아이오닉 컴포넌트에는 Sanitizing 제공함. [https://ionicframework.com/docs/techniques/security](https://ionicframework.com/docs/techniques/security)
    - React 프레임웍에서 JSX 로 데이터를 렌더링 할 때는 Sanitizing 제공함.
    - 주의 사항: DOM 에 데이터를 직접 넣는 것은 피해야 함 - 이 경우 React 에서 dangerouslySetInnerHTML 을 사용해야 하고 Sanitize 라이브러리로 데이터를 클린업 한 후 렌더링.

### XSS 라이브러리 조사

1. sanitize-html
	* 아이오닉 문서에서는 sanitize-html 이라는 라이브러리를 사용하도록 권장하고 있다.
	* 다운로드 수도 많고 유명한 라이브러리이지만 7 dependencies 가 있고, 내가 확인했을 때 최근 업데이트가 2년 전 이었어서 정기적으로 유지보수가 되지 않는 것 같아서 다른 xss 라이브러리를 찾아보게 되었다.
	* 링크: [sanitize-html  -  npm](https://www.npmjs.com/package/sanitize-html)

2. dompurify
	*  sanitize-html 의 주간 다운로드 수에 미치진 않지만 근접하게 많은 다운로드 수를 보유한 굉장히 유명한 라이브러리이다.
	* 0 dependencies 에 현재까지 유지보수가 잘 되고 있는 라이브러리이다.
	* 다양한 모던 브라우저에서 동작하고 옛날 브라우저에선 서포트 되지 않는 부분이 있다.
	* 웹 어택 및 XSS 에 지식을 보유한 보안 전문가들이 만든 라이브러리이고 무엇보다 사용이 간단해보였기 때문에 이 라이브러리를 선택하였다.
	* 링크: [dompurify  -  npm](https://www.npmjs.com/package/dompurify)
