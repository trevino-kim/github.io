---
title: "서버와 통신하여 JSON 데이터 불러오기"
excerpt: "파이썬 및 자바스크립트로 서버와 통신하여 JSON 데이터 불러오는 방법을 알아보자."
header:
  overlay_color: "#F2E315"
  overlay_filter: rgba(0, 0, 0, 0.5)
categories:
- Web
tags:
- 웹개발
- 프론트엔드
---



## JSON: JavaScript Object Notation
### 제이슨은 자바스크립트 오브젝트 노테이션의 약자이다.

사용자의 브라우저(클라이언트 사이드)에서 서버로 데이터를 요청 하면, 서버가 응답하여 데이터를 다시 웹으로 보내게 된다. 이렇게 서버와 클라이언트 사이드가 데이터를 교환할 때, 데이터 뭉치(object)를 JSON 포맷으로 주고 받으면 편리하다.


서버에서 다음과 같은 JSON 을 클라이언트 사이드로 보내면,

```
person = {
  “name”: “data1”,
  “city”: “data2”,
  “email”: “data3”,
  “phone”: 1234
}
```

자바스크립트에서 아래와 같이 값을 불러올 수 있다.

```
person.name
person.city
person.email
person.phone
```

### Python: 파이썬에서 제이슨 데이터 가져오는 방법

```
import json

dir(json)
#jason methods 확인하는 명령어
json.load(f)

파일로 부터 JSON 데이터 load 하기

json.load(s)

string으로 부터 JSON 데이터 포맷으로 convert 하기

json.dump(j, f)

파일에 JSON object 만들기(write)

json.dupms(제이슨포맷)

JSON 포맷을 string으로 output 내기

json_file = open(“파일주소”, “r”, encoding=“utf-8”)
movie = json.load(json_file)
json_file.close()
movie = {}
movie[“title”] = “movie title”
movie[“director”] = “movie director”

file = open(“파일주소”,”w”, encoding=“utf=8”)
json.dump(movie, file, ensure_ascii=False)
file.close()

```


### 자바스크립트: 서버에 존재하는 JSON 파일을 XMLHttpRequest() 자바스크립트로 불러오기

```
    var xmlhttp = new XMLHttpRequest();
    xmlhttp.onreadystatechange = () => { // This is async & will only run when the service returns a value.
      if (xmlhttp.readyState == 4 && xmlhttp.status == 200) {
          var myjson = JSON.parse(xmlhttp.responseText);
          var userid = myjson.user_id;
          var userpw = myjson.user_pw;
      }
    }
```


XMLHttpRequest() 로 서버의 제이슨 파일을 불러오는 방법이다. `JSON.parse(xmlhttp.responseText)`

xmlhttp 요청으로 응답한 텍스트 string 을 JSON 형식으로 변환한다. 아래 코드는 제이슨 파일 내에 많은 데이터 중에서 마지막 데이터만 불러온다.

```
var xmlhttp = new XMLHttpRequest();
    xmlhttp.onreadystatechange = () => { /
      if (xmlhttp.readyState == 4 && xmlhttp.status == 200) {
          var myArray = JSON.parse(xmlhttp.responseText);
          this.myjson = myArray[myArray.length-1];
      }
    }
```
