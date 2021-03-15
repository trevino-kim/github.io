---
title: "자바스크립트 이메일 & 비밀번호 정규표현식 Regex 예제 코드"
excerpt: "자바스크립트의 RegExp constructor 로 이메일과 비밀번호, 전화번호를 validation 하는 방법 예제 코드"
header:
  overlay_color: "#F2E315"
  overlay_filter: rgba(0, 0, 0, 0.5)
categories:
- Web
tags:
- 프론트엔드
---


#### 이메일 validation
조건: 입력하지 않았거나 이메일 형식이 아닌 경우

```
// RegExp 오브젝트 생성
const emailRegex = new RegExp("([\\w-\\.]+)@((?:[\\w]+\\.)+)([a-zA-Z]{2,4})");

// 사용자 입력값
const userEmail = "abc@gmail.com";

// validation
if (!emailRegex.test(userEmail)){
	// setAlert(true, "아이디는 이메일 형식으로 입력해주세요.")
}

```


#### 비밀번호 validation
조건: 영문 및 숫자 조합 8자리 이상 ~ 15자리 이하

```
// RegExp 오브젝트 생성
const passwordRegex = new RegExp("^(?=.*[0-9])(?=.*[a-zA-z]).{8,15}$")

// 사용자 입력값
const userPassword = "12123sq";

// validation
if (!passwordRegex.test(userPassword)){
	// setAlert(true, "비밀번호는 영문, 숫자 조합으로 8~15자리로 입력해 주세요.")
}

```


#### 연락처 번호 validation
조건: 숫자만 입력

```
// RegExp 오브젝트 생성
const numberRegex = new RegExp("^[0-9]+$")

// 사용자 입력값
const userPhoneNumber = "1231212";

// validation
if (! numberRegex.test(userPhoneNumber)){
	// setAlert(true, "숫자만 입력해 주세요.")
}

```
