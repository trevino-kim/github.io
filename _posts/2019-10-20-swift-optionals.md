---
title: "스위프트 옵셔널 Safety 체크 하는 방법 5가지"
excerpt: "Swift Optionals 스위프트 옵셔널 !? 기본 개념과 스위프트 옵셔널 Safety 체크 하는 방법 5가지. 알아보자"
header:
  overlay_color: "#F66E2A"
  overlay_filter: rgba(0, 0, 0, 0.5)
categories:
- iOS
tags:
- Swift
- 모바일앱
---


## Swift Optionals 스위프트 옵셔널 !? 기본 개념
iOS 개발을 하다 보면 느낌표 ! 또는 물음표 ? 를 자주 볼 수 있는데, Swift 언어에는 옵셔널 Optional 이란 개념이 있기 때문이다.

예를 들어 변수 myVar 에는 다양한 변수 값이 Input 으로 들어오고 계속 변경될 수 있다. 또 이 변수에 기대하는 변수 데이터 타입이 있는데 하나의 변수에는 항상 같은 데이터 타입이 Input 으로 들어와야 한다. 이렇게 변수는 항상 같은 데이터 타입의 변수 값을 input 으로 기대하고 있는데, 프로그래밍을 하다 보면 기대하는 변수 값이 아니거나 없는 경우가 발생 한다. nil 은 아예 변수 값이 없고 텅 비어있는 경우를 말하며, 기대하는 변수 값이 nil 이거나 데이터 타입이 다른 경우에 앱은 crash 된다. 이러한 앱 crash 를 방지하기 위해 **safety check** 를 하는 것이다.


```
var myVar: String? = nil

myVar = “ABC”
print(myVar) // Optional(“ABC”)

var unwrappedMyVar = myVar!
print(unwrappedMyVar) // ABC
print(MyVar!) // ABC
```


가장 처음 myVar 을 nil 로 지정하고 나중에 myVar 변수 값을 입력하려 하는 상황이라면, myVar 데이터 타입을 Optional String 으로 지정해줘야 한다.

`var myVar: String? = nil`

그리고 후에 myVar 값을 지정하면, myVar = “ABC” , “ABC”의 데이터 타입은 optional String 이 된다. 당연하다. myVar 의 데이터 타입이 optional String 이므로! myVar 의 변수 값 “ABC” 를 String 으로 변경하고 싶다면, myVar 에 느낌표 !를 붙여주면 된다.

`myVar! 또는 var unwrappedMyVar = myVar!`

변수 이름 뒤에 느낌표 ! 를 붙여주는 이유는 이 변수는 확실히 적절한 데이터를 포함하고 있다고 확신시켜 주는 것이다. 즉 nil 이 아니라 변수 값이 있음! 이라고 컴퓨터에 확실히 얘기해주는 것!

만약에 myVar = nil 인 상태에서 myVar! 느낌표를 붙여 사용하면 error 가 뜨고 앱은 crash 된다.

```
if myVar != nil {
  print(myVar!)
}
```


## 스위프트 옵셔널 Safety 체크 하는 방법 5가지
Swift Optionals 데이터 타입 ? 를 Safety 체크 하는 방법 5가지
1. Force Unwrapping
2. if 문으로 nil 체크하기
3. 옵셔널 바인딩 (Optional Binding)
4. nil 에 대비해 디폴트 값 설정하기
5. 옵셔널 체이닝 (Optional Chaining)

```
1. 옵셔널변수이름!
2. if 옵셔널변수이름 != nil {
     옵셔널변수이름!
   }
3. let 변수이름 = 옵셔널변수이름
4. 옵셔널변수이름 ?? 디폴트값
5. 옵셔널클래스이름?.property, 옵셔널클래스이름?.method()
```

1. Force Unwrapping
1번 Force Unwrapping 은 가장 간단하고 쉬운 방법으로 옵셔널 ? 데이터 타입을 확실하게 ! 데이터 타입 정의를 해주는 것이다. 예를 들면, let myVar: String? 데이터 타입을 후에 myVar! 로 지정하면 myVar 은 무조건 String 데이터 타입으로 선언이 되고, 혹여나 nil 이 들어오면 앱이 크래쉬 된다. 이 방법은 코드가 복잡하고 길어질 수록 안전하지 않은 방법이다.

2. if 문으로 nil 체크하기
2번 if 문으로 nil 체크하는 방법이 조금 더 안전할 수 있으나 옵셔널 변수 이름에 다시 unwrapping ! 느낌표를 찍어줘야한다.

3. 옵셔널 바인딩 (Optional Binding)
3번 옵셔널 바인딩은 옵셔널 변수 이름 뒤에 매번 ! 를 붙이지 않도록 바인딩하는 방법이다.

```
let optionalABC: String?
let safeABC = optionalABC
```

일 때 이후로는 safeABC 뒤에 ! 를 붙이지 않아도 safeABC는 String 변수 타입이 된다.

4. nil 에 대비해 디폴트 값 설정하기
4번은 옵셔널 변수 타입에 nil 이 들어올 경우를 대비해 디폴트 값을 지정해주는 방법이다. 옵셔널 변수 이름 뒤에 물음표 2개 ?? 를 넣고 디폴트 값을 써준다. 예를 들면,

```
let optionalNum: Int?
let myNumber: Int = optionalNum ?? 0
// myNumber 에 nil 이 들어오면 디폴트 값 0을 내보낸다.

optionalNum = nil
print(myNumber)
// 0

optionalNum = 25
print(myNumber)
// 25
```

5. 옵셔널 체이닝 (Optional Chaining)
5번은 struct 또는 class 내에 프로퍼티나 메소드에 접근하기 전에 먼저 nil 인지 아닌지 safety check 를 하는 방법이다. 먼저 MyStruct 라는 스트럭쳐가 있다고 가정하자.

```
struct MyStruct {
  var myProp = 123
  func myMethod(){
    print(“myMethod in MyStruct!”)
  }
}
```

myOptional 이란 상수의 데이터 타입을 MyStruct? 로 지정한 후, MyStruct() 를 이니셜라이즈 한다.

```
let myOptional: MyStruct?
myOptional = MyStruct()
```

스트럭쳐 내에 있는 프로퍼티나 메소드에 접근하기 위해서는 보통 myOptional.myProp 또는 myOptinal.myMethod() 와 같이 사용할 수 있다. 하지만 만약에 myOptional 이 nil 이라면 또 앱이 크래쉬되는 상황이 발생하게 된다. 이를 방지하기 위해 myOptional?.myProp 또는 myOptinal?.myMethod() 이렇게 뒤에 ? 를 붙여 myOptional 이 nil 인지 세이프티 체크를 하는 것이다.

```
myOptional?.myProp
myOptional?.myMethod()
```

위 코드의 의미는 myOptional 이 nil 인지 체크하고 nil 이 아니면 myProp 또는 myMethod() 에 접근하라, 라는 뜻이다.
