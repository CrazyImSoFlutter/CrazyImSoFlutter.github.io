---
title: "Swift-The Basics"
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

# Type Safety and Type Inference

Swift는 **Type-safe** 언어이다.

즉, 잘못된 자료형을 사용하면 컴파일러가 에러를 출력한다.

**Type-Checking**은 다른 타입을 사용하려고 할 때 오류를 발생시켜서 오류를 피할 수 있다.

하지만 미리 자료형을 선언하지 않으면 Swift는 **Type-inference**를 통해 적절한 타입을 찾는다.

Type-inference를 통해 컴파일러는 코드를 컴파일할 때 자동으로 자료형을 추론할 수 있다.

Type-inference 덕분에 C와 Objective-C와는 다르게 자료형 선언이 필수적이지 않지만, 상수, 변수 선언을 위한 **let**, **var**는 꼭 써줘야 한다.

```swift
let meaningOfLife = 43
// meaningOfLife is inferred to be of type Int

let pi = 3.14159
// pi is inferred to be of type Double

let anotherPi = 3 + 0.14159
// anotherPi is also inferred to be of type Double
```

**Swift는 부동 소수점을 추론할 때는 항상 Double로 추론한다.**

# Numeric Literals(정수형 리터럴)

정수형 리터럴은 아래와 같이 나타낼 수 있다.

10진수는 접두사가 없고, 2진수는 0b, 8진수는 0o, 16진수는 0x의 접두사를 가진다.

```swift
let decimalInteger = 17
let binaryInteger = 0b10001       // 17 in binary notation
let octalInteger = 0o21           // 17 in octal notation
let hexadecimalInteger = 0x11     // 17 in hexadecimal notation
```

부동 소수점 숫자에서는 10진수는 접두사가 없고, 16진수일 때 0x 접두사가 붙는다.

부동 소수점에는 e로 표시되는 지수를 가질 수 있다.

```swift
// 모두 10진수로 12.1875를 나타내는 부동 소수점 숫자이다.
let decimalDouble = 12.1875
let exponentDouble = 1.21875e1
let hexadecimalDouble = 0xC.3p0
```

숫자 리터럴에는 읽기 쉽게 추가적인 형식이 포함될 수 있다.

0으로 채워질 수도 있고, 가독성을 위해 밑줄이 포함될 수 있다.

이런 식으로 추가적인 형식이 붙어도 기본값에는 영향을 주지 않는다.

```swift
let paddedDouble = 000123.456
let oneMillion = 1_000_000
let justOverOneMillion = 1_000_000.000_000_1
```

# Numeric Type Conversion(정수 타입 변환)

## Integer Conversion

각자의 정수 타입마다 저장할 수 있는 값이 다르기 때문에, 적절한 사용을 위해 다른 정수 타입으로 변환을 해주어야 할 때가 있다.

아래의 코드와 같이 다른 타입의 정수형을 직접 더할 수 없기 때문에 UInt16()을 사용하여 UInt8을 UInt16으로 변환해 준 뒤 더해주었다.

당연하게도 twoThousandAndOne의 타입도 UInt16이 된다.

```swift
let twoThousand: UInt16 = 2_000
let one: UInt8 = 1
let twoThousandAndOne = twoThousand + UInt16(one)
```

## Integer and Floating-Point Conversion

정수와 부동 소수점 숫자의 변환은 명시적으로 작성해야한다.

**다른 언어와 달리 Swift는 묵시적 형변환을 허용하지 않는다.**

```swift
let three = 3
let pointOneFourOneFiveNine = 0.14159
let pi = Double(three) + pointOneFourOneFiveNine
// pi equals 3.14159, and is inferred to be of type Double
```

하지만 아래와 같이 부동소수점 숫자를 정수형으로 바꿔주면 **소수점 아래 숫자를 모두 버리게 된다.**

```swift
let integerPi = Int(pi)
// integerPi equals 3, and is inferred to be of type Int
```

## Type Conversion

모든 연산에 사용되는 데이터들은 타입이 정확하게 일치해야한다.

```swift
let big = 1000
let small : Int8 = 10

var sum = big + Int(small)
```

어느 쪽으로든 한 쪽으로 맞춰주면 되는데, 데이터 타입의 크기가 작은 쪽으로 맞춰 줄 때는 **오버플로우**를 조심해야한다.

# Type Aliases

Type Aliases는 타입의 별명이라고 볼 수 있다.

정확히는 기존 타입을 다른 이름으로 선언하는 것이다.

```swift
typealias AudioSample = UInt16
```

이렇게 다른 이름을 선언해주면 UInt16 타입을 AudioSample 이라는 이름으로도 접근 할 수 있게 된다.

**Type Aliases는 새로운 타입을 생성하는 것이 아니다.**

단순히 별칭을 사용했을 때 실제 타입을 참조, 대신해서 사용하는 것을 허용해주는 것이다.

# Booleans(논리값)

Swift에는 기본적인 Boolean type으로 Bool을 가지고 있다.

이는 오로지 **true, false**만을 값으로 가질 수 있다.

```swift
let bool1 = true
let bool2 = false
```

위의 코드처럼 상수나 변수를 생성하자마자 true, false로 설정하면 Bool로 선언할 필요가 없다.

# Tuples(튜플)

Tuple(튜플)은 여러 개의 값을 하나의 복합 값으로 그룹화하는 것을 말한다.

튜플 내의 값은 모든 자료형이 가능하다.

하나의 자료형만 가능한 것이 아니고 여러 개의 자료형이 함께 존재해도 상관 없다.

## Basic Use

Swift에서 튜플을 사용하고 싶으면 상수를 선언한 뒤 원하는 데이터 값들을 ()에 묶어서 넣어주면 된다.

tuple은 compound type으로 named type뿐만 아니라, compound type도 담을 수 있다.

따라서 tuple에는 compound type인 tuple type이나, function type을 담을 수 있다.

```swift
var tuple : (Int, String) = (10, "ten")
```

튜플에서도 Swift에서의 타입 추론이 적용되기 때문에 데이터 타입을 생략해도 상관없다.

```swift
var tuple = (10, "ten")
```

다른 튜플의 사용법으로는 tuple의 원소에 **이름**을 줄 수 있다.

```swift
var tuple = (name: "corani", age: 1000, learn : ["Swift","iOS"])
```

## Substituting constant and variable to Tuple

튜플의 값들을 변수나 상수에 넣어주는 방법도 있다.

변수나 상수도 괄호로 묶어서 선언한 뒤 튜플을 넣어주면 된다.

여기서 주의할 점은 튜플의 구성요소 개수 만큼 **변수나 상수도 똑같이 선언해줘야 한다는 것**이다.

```swift
var tuple : (String, String, Bool) = ("ten", "eleven", true)
var (num1, num2, bools) = tuple //튜플의 값의 순서대로 변수에 지정된다.
```

## Call Tuple

튜플의 값들은 배열(Array)과 마찬가지로 순서대로 0부터 개수만큼 인덱스가 부여된다.

**인덱스를 통해 원하는 값을 가져올 수 있다**.

```swift
var tuple : (String, String, Bool) = ("ten", "eleven", true)
print ("십 : \(tuple.0), 십일 : \(tuple.1), 참인가? \(tuple.2)")
```

또한 튜플의 각 타입에 이름을 붙여서 해당 **이름을 통해 값을 호출할 수 있다**.

```swift
var tuple : (num1 : String, num2 : String, bools : Bool) = ("ten", "eleven", true)
print ("십 : \(tuple.num1), 십일 : \(tuple.num2), 참인가? \(tuple.bools)")
```
# Optionals

Swift는 안전한 코딩을 할 수 있게 해주는 언어라고 알려져 있다.

그리고 이 안전성을 책임지는 중요한 요소 중 하나가 바로 Optional이다.

개발자는 Optional(옵셔널)을 비어있는 값을 표현할 때 사용할 수 있다.

**자료형 뒤에 ?를 붙이면 옵셔널 타입으로 선언하는 것이다.**

> 이 변수에는 값이 있을 수도 있고, 없을 수도 있다.

옵셔널은 **값이 있거나, 없거나**의 두 가지 상태를 표현한다.

개발자는 옵셔널을 사용할 때 옵셔널을 뜯어봐서 값이 있는 지 없는 지를 확인해야 한다.

```swift
let possibleNumber = "123"
let convertedNumber = Int(possibleNumber)
// convertedNumber is inferred to be of type "Int?", or "optional Int"
```

String 타입의 값을 Int 타입으로 바꿔줄 수 있는데, 항상 바꿀 수 있는 것은 아니다.

정수로 이루어진 String 타입의 값만 바꿔줄 수 있지만 문자가 섞인 String 타입의 값은 바꿀 수 없다.

따라서 이런 실패할 수 있는 상황에서 Int대신 Int?를 사용하면, 성공하면 Int를 넣고 실패하면 nil을 넣음으로써 오류를 방지 할 수 있다.

하지만 Int?로 선언하면 Int형과 nil만 들어갈 수 있지 String이나 Bool과 같은 다른 타입들은 들어갈 수 없다.

## nil

```swift
var num1: Int? = 404
// num1 contains an actual Int value of 404
num1 = nil
// num1 now contains no value
```

위와 같이 정수형 옵셔널로 선언된 값에 nil을 넣어주면 더 이상 num1에는 값이 존재하지 않게 된다.

```swift
var surveyAnswer: String?
// surveyAnswer is automatically set to nil
```

만약 옵셔널 변수를 선언한 뒤 아무것도 넣지 않으면 Swift에서 자동적으로 nil을 넣는다.

## If Statements and Forced Unwrapping

개발자는 옵셔널에 값이 있는 지 없는 지를 확인하기 위해 뜯어봐야 하는데 이 때 if를 사용할 수 있다.

```swift
if convertedNumber != nil {
    print("convertedNumber has an integer value of \(convertedNumber!).")
}
// Prints "convertedNumber has an integer value of 123."
```

이렇게 convertedNumber이라는 변수가 nil이 아니면 조건 문의 코드가 실행하게 된다.

또한 해당 변수 뒤에 !를 붙이게 되면 nil이 아닌 그 변수에 존재하는 값을 추출하여 사용하게 된다.

```swift
var number: Int = 10
print(\(number!))
```

하지만 값이 없는데 !를 붙여 꺼내려고 하면 오류가 발생하므로, 

위와 같이 옵셔널이 nil인지 아닌지를 확인 후 사용해야 한다.

## Optional Binding

Optional Binding(옵셔널 바인딩)은 옵셔널에 값이 있는 지 본 뒤, 있다면 해당 값을 가지는 상수나 변수를 만들고 사용할 수 있게 하는 것이다.

옵셔널 바인딩에는 if, while 문이 사용될 수 있고 사용법은 아래와 같다.

```swift
if let actualNumber = Int(possibleNumber) {
    print("The string \"\(possibleNumber)\" has an integer value of \(actualNumber)")
} else {
    print("The string \"\(possibleNumber)\" could not be converted to an integer")
}
// Prints "The string "123" has an integer value of 123"
```

possibleNumber는 옵셔널 변수이다.

if let을 사용하여 만약 possibleNumber에 값이 있다면 actualNumber라는 상수에 값을 넣어 조건문에서만 사용할 수 있게 한다.

만약 nil이라면 actualNumber는 만들어지지 않는다.

이때  앞의 글에서 본 것 처럼 !를 사용하지 않아도 actualNumber에는 possibleNumber의 값이 존재하게 된다.

물론 let말고 var를 사용하여 변수처럼 사용할 수도 있다.

```swift
if let firstNumber = Int("4"), let secondNumber = Int("42"), firstNumber < secondNumber && secondNumber < 100 {
    print("\(firstNumber) < \(secondNumber) < 100")
}
// Prints "4 < 42 < 100"

if let firstNumber = Int("4") {
    if let secondNumber = Int("42") {
        if firstNumber < secondNumber && secondNumber < 100 {
            print("\(firstNumber) < \(secondNumber) < 100")
        }
    }
}
// Prints "4 < 42 < 100"
```

여러 개의 옵셔널 바인딩을 한 번에 사용할 수도 있다.

## Implicity Unwrapped Optional

앞의 글에서처럼 옵셔널을 사용하려면 if를 사용하여 값이 존재하는 지 확인한 뒤 옵셔널 바인딩으로 값에 접근할 수 있었다.

**만약 절대로 nil이 아닌 값이 존재하는 값이 존재한다면 어떨까?**

이럴 때는 if let과 같은 구문을 사용하지 않고 바로 접근하면 편하다.

이럴 때 바로 값에 접근할 수 있는 방법이 **!를 붙이는 것이다.**

옵셔널 변수 선언시 ?를 붙이면 암시적 옵셔널, !를 붙이면 명시적 옵셔널이 된다.

!를 붙인 옵셔널은 처음 정의된 후에는 값이 존재한다고 보고 앞으로 모든 시점에서 존재한다고 확신할 수 있을 때 유용하다.

Swift에서는 주로 클래스 초기화를 할 때 사용된다.

```swift
let possibleString: String? = "An optional string."
let forcedString: String = possibleString! // requires an exclamation point

let assumedString: String! = "An implicitly unwrapped optional string."
let implicitString: String = assumedString // no need for an exclamation point
```

forcedString에서 possibleString에 !를 붙여주는 이유는 possibleString이 ?를 붙여준 암시적 옵셔널 변수이기 때문이다.

하지만 처음 선언부터 !를 붙여 정의한 assumedString같은 경우에는 다른 변수에서 사용할 때 !를 붙여주지 않아도 되는 걸 볼 수 있다.

```swift
let optionalString = assumedString
// The type of optionalString is "String?" and assumedString isn't force-unwrapped.
```

만약 암시적으로 선언된 옵셔널이 nil인데 명시적 옵셔널이 접근하려고 하면 런타임 오류가 발생한다.

```swift
if assumedString != nil {
    print(assumedString!)
}
// Prints "An implicitly unwrapped optional string."
```

이러한 런타임 오류를 방지하기 위해 위와 같이 사용하면 된다.

# Error Handling

프로그램에서 오류가 발생하면 오류 처리를 사용하여 해결해야 한다.

오류 처리를 통해 실패 원인을 알아내고 발생한 오류를 다른 부분으로도 전파할 수 있다.

만약 함수에서 에러가 발생되면 throws를 사용하여 오류를 던질 수 있다.

그런 뒤 catch를 사용해 던져진 오류를 잡아 반응할 수 있다.

```swift
func canThrowAnError() throws {
    // this function may or may not throw an error
}
do {
    try canThrowAnError()
    // no error was thrown
} catch {
    // an error was thrown
}
```

만약 canThrowAnError에서 오류가 발생하면 오류를 던져 catch 구문을 실행한다.

오류가 발생하지 않으면 그냥 함수를 수행한다.

여기서 do try구문은 한 번 실행해볼까?하고 실행을 했는데 실행한 함수가 throws로 오류를 던지면 catch로 받아 처리한다는 느낌으로 이해하면 쉽다.

```swift
func makeASandwich() throws {
    // ...
}

do {
    try makeASandwich()
    eatASandwich()
} catch SandwichError.outOfCleanDishes {
    washDishes()
} catch SandwichError.missingIngredients(let ingredients) {
    buyGroceries(ingredients)
}
```

조금 더 구체적인 예를 보면 위와 같다.

makeASandwich 함수를 실행하려고 했는데 만약 오류가 발생하면 catch 구문을 ,

아니면 그냥 makeASandwich 실행 후 eatASandwich 함수를 실행한다는 의미이다.

여기서 SandwichError.outOfCleanDishes나 SandwichError.missingIngredients(let ingredients)는 위에서는 생략되었지만 개발자가 미리 선언한 에러의 종류이다.

**즉, 에러의 종류에 따라 실행할 코드를 달리 하는 것이라고 볼 수 있다.**

# Assertions and Preconditions

Assertions and Preconditions는 **런타임 시 발생하는 것들을 확인**하는 것이다.

추가 코드를 실행하기 전에 사용해서 조건들이 맞는 지 확인할 수 있다.

만약 조건들이 false로 나오게 되면 코드 실행이 중단되고 프로그램이 종료된다.

**Assertion은 개발 과정**에서 실수를 잡고 **Preconditions는 문제를 감지**하는데 도움을 준다.

앞에서 본 Error Handling과는 다르게 Assertions and Preconditions는 복구 가능하거나 예상되는 오류에는 사용되지 않는다.

이는 발견 즉시 프로그램을 종료하기 때문이다.

하지만 바로 종료하기 때문에 잘못된 상태로 인한 피해를 줄일 수 있다.

또한 종료가 되어버리기 때문에 오류를 쉽게 디버깅할 수 있다.

Assertions과 Preconditions은 조건들을 확인할 때 차이가 난다.

**Assertions는 디버그 빌드에서만 체크를 하지만,**

**Preconditions는 디버그, 프로덕션 빌드 모두 체크를 한다.**

프로덕션 빌드에서는 Assertions가 체크되지 않기 때문에 프로덕션 성능에 영향을 주지 않으면서 Assertion을 사용할 수 있다.

## Debugging with Assertions

Assertion은 **'코드가 실행될 때 반드시 만족해야 하는 조건을 코드 상에 명시해 놓는 것'** 이다.

그래서 코드가 정상적으로 실행되면 문제가 없는 것이고, 만약 Assertion을 통해 문제가 발생한다면 코드의 어딘가에 문제가 있다는 의미가 되어서 디버깅에 좋은 자료가 된다.

Assertions는 assert(_: _: file:line:)함수로 사용할 수 있다.

```swift
let age = -3
assert(age >= 0, "A person's age can't be less than zero.")
// This assertion fails because -3 is not >= 0.
```

assert함수는 조건을 확인한다.

true면 그냥 진행하고, false면 프로그램을 종료하며 만약 오류 구문을 적어뒀다면 그것이 출력된다.

```swift
if age > 10 {
    print("You can ride the roller-coaster or the ferris wheel.")
} else if age >= 0 {
    print("You can ride the ferris wheel.")
} else {
    assertionFailure("A person's age can't be less than zero.")
```

만약 조건이 이미 체크됐다면 assertionFailure(_:file:line:)함수를 사용해 실패를 알릴 수 있다.

# Enforcing Precondtions

precondition은 '조건이 거짓이 될 가능성이 있지만 코드가 실행되기 위해선 반드시 참이어야할 때' 사용한다.

precondition(_: _: file:line:)함수로 사용할 수 있고 만약 조건이 false라면 설정해둔 오류 구문을 출력한다.

```swift
// In the implementation of a subscript...
precondition(index > 0, "Index must be greater than zero.")
```

preconditionFailure(_:file:line:)함수를 사용해서 실패가 발생했다는 것을 표시할 수 있습니다.

만약 uncheckedmode(-Ounchecked)라면 preconditions는 체크되지 않는다.

이때 컴파일러는 조건들이 모두 참이라고 생각하고 진행한다.

그러나 fatalError(_:file:line:)함수는 이와 관계없이 항상 체크되고 프로그램을 중지시킨다.

개발자는 fatalError(_:file:line)함수를 개발 초기에 사용하여 치명적인 오류에 대해 항상 중지되도록 설정할 수 있다.

