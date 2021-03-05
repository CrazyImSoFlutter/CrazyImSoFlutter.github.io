---
title: "The Basics"
excerpt: "Swift 공식 문서"
toc: true
toc_sticky: true
toc_label: "Swift-The Basics"
categories:
 - iOS
tags:
 - iOS
 - Basics
---

# The Basics

Swift는 IOS, macOS, watchOS, tvOS를 만들기 위한 새로운 프로그래밍 언어이다.

기초적인 자료형으로는 Int, Double, Float, Bool, String, Array, Set, Dictionary가 있다.

C언어와 마찬가지로 Swift는 값을 저장하고 참조하기 위해 변수를 사용하고 이름으로 변수를 구분한다.

Swift에는 변수 중에서도 값을 변경할 수 없는 **Constant(상수)**를 제공하고 이로 인해 C에서 보다 더 많은 기능을 수행할 수 있다.

Swift에는 Objective-C에서는 볼 수 없는 **tuple(튜플)** 형식도 제공한다.

튜플을 사용해서 여러 값을 하나의 값으로 반환할 수도 있다.

Swift에서는 Optional Type(옵셔널 타입)을 제공하는데, 이는 값이 없을 때를 제어할 수 있다. 

만약 값이 있다면 값을, 값이 없다면 **nil**을 사용한다. 

이는 클래스뿐만 아니고 모든 유형에 대해 사용할 수 있습니다. Swift는 **type-safe** 언어다.

즉, 사용자가 잘못된 자료형을 사용하면 경고를 줘서 인지하게 해준다. 

이는 **옵셔널 타입**에도 적용된다. 예를 들어 일반 String 변수에 옵셔널 String 변수를 사용하려고 하면 오류를 발생시킨다.

# Constants and Variables (상수와 변수)

## Declaring constants and variables (상수와 변수의 선언)

상수는 **let**으로 선언되고, 변수는 **var**로 선언된다.

```swift
let maximumNumberOfLoginAttempts = 10 // 상수
var currentLoginAttemp = 0 // 변수
```

아래와 같이 한 줄로 선언도 가능하다.

```swift
var x = 0.0, y = 0.0, z = 0.0
```

## Type Annotations(자료형 명시)

변수나 상수를 선언할 때 **type annotation**을 사용할 수 있다.

이는 어떠한 자료형으로 변수나 상수로 선언할지 명확하게 하기 위해 사용된다.

```swift
var welcomeMessage: String
```

물론 한 줄로도 선언이 가능하다.

```swift
var red, greem, blue: Double
```

## Naming Constants and Variables(상수와 변수에 이름 짓기)

변수와 상수는 유니코드에 있는 **모든 문자열**로 이름을 지을 수 있다.

```swift
let π = 3.14159
let 你好 = "你好世界"
let 🐶🐮 = "dogcow"
```

변수와 상수의 이름규칙

1. **띄어쓰기(공백)이 존재할 수 없다.**
2. **수학기호, 화살표, private-use Unicode scalar values, line- and box- drawing 문자를 사용할 수 없다.**
3. **숫자로 시작할 수 없다. 하지만 시작이 아니라면 다른 곳에는 포함될 수 있다.**
4. **한 번 선언되면 같은 이름으로 다른 변수나 상수를 만들 수 없다.**
5. **한 번 선언되면 자료형을 바꿀 수 없다.**
6. **상수에서는 한 번 선언된 값을 바꿀 수 없다.**

## Printing Constants and Variables(상수와 변수 출력)

상수나 변수는 **print(_:separator:terminator:)함수**로 출력할 수 있다.

```swift
var str = "Hello, playgroundwww"

print("hello " + str)
print("hello \(str)") //변수 바인딩

//상수 선언
let a : Int = 5
let b : Int = 6

print("a는 \(a)")  //상수 출력
print("b는 \(b)")
print("a+b 는 \(a+b)")   //연산식 출력
```

![img](https://user-images.githubusercontent.com/65299607/110048221-c5abcd00-7d92-11eb-9f10-a824d25d9fa6.png)

그런데 우리는 개행문자(\n)를 넣어주지 않았는데 자동으로 개행이 되어 출력됐다.

그 이유는 아래에 나와있다.

```swift
func print(_ items:Any..., separator: String = " ", terminator: String = "\n")
```

Apple의 개발자 문서에서 print함수는 단순히 하나의 인자만 받는게 아니라 여러가지 인자를 받을 수 있는데,

 기본으로 입력되는 terminator 인자에 \n이 기본으로 할당되어 있다.

이 때문에 terminator를 지정하지 않을 때 자동으로 newline을 출력해 주는 것이다.

아래와 같이 terminator에 빈 문자열을 넣어주면 더 이상 개행되어 출력되지 않는다.

```swift
var str = "Hello, playgroundwww"

print("hello " + str, terminator:"")
print("hello \(str)", terminator:"")
let a : Int = 5
let b : Int = 6

print("a는 \(a)", terminator:"")
print("b는 \(b)", terminator:"")
print("a+b 는 \(a+b)", terminator:"")
```

![img2](https://user-images.githubusercontent.com/65299607/110048228-c80e2700-7d92-11eb-87ee-aa287e48c5b9.png)

# Comments(주석)

주석을 사용해서 실행되지 않는 텍스트를 추가해서 메모를 하거나 설명을 할 수 있다.

```swift
// This is a comment.
```

위와 같이 // 로 한 줄을 주석 처리 할 수 도 있고,

```swift
/* This is also a comment
but is written over multiple lines. */
```

이런 식으로 여러 줄을 주석 처리를 할 수 도 있다.

```swift
/* This is the start of the first multiline comment.
 /* This is the second, nested multiline comment. */
This is the end of the first multiline comment. */
```

C언어와는 다르게 주석 안에 주석이 중첩 될 수 있다.

# Semicolons(;)

C언어와 Java와는 다르게 Swift에서는 코드 마지막에 세미콜론(;)을 쓰지 않아도 된다.

그런데 정 쓰고 싶다면 써도 되긴 하다.

하지만 한 줄에 여러 개의 실행문을 쓰고 싶다면 세미콜론을 꼭 써줘야 한다.

```swift
let cat = "🐱"; print(cat)
```
# Integers(정수)

## Integers(정수)

Integerssms 42, -24와 같이 분수 성분이 없는 수이다.

양수, 0, 음수가 정수에 포함된다.

Swift는 8, 16, 32, 64비트 형식의 부호 있는 정수와 부호 없는 정수를 제공한다.

C언어와 비슷하게 부호 없는 정수는 UInt8과 같이 나타내며 부호 있는 정수는 Int8 과 같이 나타낸다.

Swift의 모든 타입과 마찬가지로 정수 타입도 **대문자로 시작**된다.

## Integer Bounds(정수의 한계값)

min, max property를 사용하여 각 정수 타입의 최대값과 최솟값에 접근할 수 있다.

```swift
let minValue = UInt8.min  // minValue is equal to 0, and is of type UInt8
let maxValue = UInt8.max  // maxValue is equal to 255, and is of type UInt8
```

## Int

대부분의 경우에서 정수형으 사용할 때 크기를 선택할 필요는 없고 Int만 사용하면 된다.

Int를 사용할 때 컴퓨터가 32비트 환경이라면 Int32로, 64비트 환경이라면 Int64로 알아서 정의된다.

## UInt

부호가 없는 정수도 제공된다.

UInt도 Int와 마찬가지로 환경에 따라 알아서 정의된다.

# Floating-Point Numbers(부동 소수점)

부동 소수점 숫자는 3.14, 0.1, -42.42와 같이 분수형 숫자이다.

부동 소수점 숫자는 정수형보다 더 넓은 범위의 값을 나타낼 수 있다.

Swift에서는 **Double**, **Float**의 두가지 부동 소수점 타입을 제공한다.

Double은 64비트 부동 소수점, Float는 32비트 부동 소수점이다.

Double의 정밀도는 십진수 15자리 이상이고, Float의 정밀도는 십진수 6자리 이다.

적절한 부동 소수점 타입은 코드에서 작업해야 하는 값의 특성과 범위에 따라 달라진다고 한다.


