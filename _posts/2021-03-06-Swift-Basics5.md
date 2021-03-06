---
title: "Swift-Control Flow"
excerpt: "Swift 공식 문서"
toc: true
toc_sticky: true
toc_label: "Swift-Control Flow"
categories:
 - iOS 공식문서
tags:
 - iOS
---

Swift는 여러 가지 제어 흐름 구문을 제공한다.

**while, if, guard, switch, break, continue**가 제어 흐름 구문에 해당한다.

Swift는 Array, Dictionary, ranges, String 등을 쉽게 다룰 수 있는 for-in 구문도 제공한다.

Swift의 switch 구문은 C언어의 것보다 더 강력한 기능들을 제공한다.

case들을 tuple, 특정 타입에 대한 cast를 포함해서 좀 더 많은 패턴으로 구성할 수 있다.

Switch의 case 일치 값은 임시 상수 혹은 변수에 담길 수 있다.

복잡한 조건은 각 케이스의 where 절로 표현될 수 있다.

# <span style="color:blue">For-In Loops</span>

for-in loop 구문은 Array의 값들, String의 Character 값들과 같은 값들에 사용할 수 있다.

```swift
let names = ["Anna", "Alex", "Brian", "Jack"]
for name in names {
    print("Hello, \(name)!")
}
// Hello, Anna!
// Hello, Alex!
// Hello, Brian!
// Hello, Jack!
```

위의 코드는 Array를 for-in 구문을 통해 사용해 본 예시이다.

물론 Dictionary에도 사용할 수 있는데, 이때는 key-value 쌍에 접근할 수 있다.

이는 (key, value)의 튜플로 반환되게 되는데 이는 명시적으로 선언한 상수로 나누어 나타낼 수도 있다.

```swift
let numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
for (animalName, legCount) in numberOfLegs {
    print("\(animalName)s have \(legCount) legs")
}
// cats have 4 legs
// ants have 6 legs
// spiders have 8 legs
```

Dictionary는 순서가 없는 타입이기 때문에 검색 순서가 보장되는 것은 아니다.

즉, 삽입되는 순서가 for-in 구문에 의해 접근되는 순서는 아닐 수 있다는 것이다.

for-in 구문으로 숫자 범위에도 사용할 수 있다.

```swift
for index in 1...5 {
    print("\(index) times 5 is \(index * 5)")
}
// 1 times 5 is 5
// 2 times 5 is 10
// 3 times 5 is 15
// 4 times 5 is 20
// 5 times 5 is 25
```

위의 코드에서 index는 루프의 각 반복이 시작될 때 마다 값이 자동으로 설정되는 상수이다.

즉, let을 사용하여 선언할 필요가 없다는 것이다.

만약 반복을 할 때 굳이 각각의 값들이 필요 없다면 아래와 같이 코드를 만들면된다.

```swift
let base = 3
let power = 10
var answer = 1
for _ in 1...power {
    answer *= base
}
print("\(base) to the power of \(power) is \(answer)")
// Prints "3 to the power of 10 is 59049"
```

_를 사용하여 for-in 구문을 사용하면 반복은 원하는 횟수만큼 해주지만 반복을 시작할 때마다 설정되던 상숫값을 만들지 않겠다는 말이다.

즉, 범위 내에 있는 값이 필요없다면 밑줄로 값을 무시할 수 있다는 것이다.

for-in 구문을 사용할 때 stride(from:to:by), stride(from:through:by:) 함수를 사용하면 반복을 몇 단계씩 건너뛰고 수행할 수 있다.

이때 stride(from:to:by)는 to값에 어디까지 수행하라는 뜻이고,

stride(from:through:by:)는 through 값 까지 수행하라는 뜻이다.

```swift
let minuteInterval = 5
for tickMark in stride(from: 0, to: minutes, by: minuteInterval) {
    // render the tick mark every 5 minutes (0, 5, 10, 15 ... 45, 50, 55)
}

let hours = 12
let hourInterval = 3
for tickMark in stride(from: 3, through: hours, by: hourInterval) {
    // render the tick mark every 3 hours (3, 6, 9, 12)
}
```

# <span style="color:blue">While Loops</span>

while loop는 조건이 거짓이 될 때 까지 명령문을 수행하는 loop이다. 

이러한 loop는 시작할 때 몇번을 수행해야 하는 지 모를 때 사용하면 좋다.

Swift에서는 두 가지의 while loop를 제공한다.

처음부터 조건을 확인한 뒤 명령을 수행하는 while구문과 처음에 한 번은 조건 없이 명령을 수행하고 그 다음부터 조건을 확인하는 repat-while 구문이 있다.

## While

While loop는 시작할 때부터 조건을 확인한다.

만약 조건이 true라면 조건이 false가 될 때 까지 명령을 수행한다.

```swift
var age = 20
while age < 30{
    print("현재 나이는 \(age)")
    age += 1
}
```

위의 코드에서 반복을 할 때마다 age는 계속해서 1씩 증가하고 age < 30 이라는 조건이 false가 될 때 까지 명령을 수행한다.

## Repeat-While

Repeat-while loop는 시작할 때 조건을 확인하지 않고 명령을 한 번 수행한 뒤 조건을 확인한다.

사실 확실한 개념은 명령을 수행하고 조건을 확인하는 것이다.

```swift
var age = 30
repeat {
    print("현재 나이는 \(age)")
    age += 1
} while age < 30
```

즉, 위와 같은 코드를 실행하면 조건이 age < 30인데 처음부터 age가 30이므로 기존의 while에서는 명령문이 한 번도 실행되지 않지만 repeat-while 구문에선 명령문을 수행 후 조건을 보기 때문에 한 번 수행 뒤 while 문이 종료되게 된다.

# <span style="color:blue">Conditional Statements</span>

특정 조건에 따라 코드를 수행하는 것은 유용하다.

이렇게 조건에 따라 코드를 수행하게 만드는 것이 Conditional Statements이다.

Swift는 조건문을 만드는 방법을 2가지 제공한다.

하나는 if문이고, 다른 하나는 switch문이다.

if는 몇개 안되는 간단한 조건들을 확인할 때 쓰이고 switch는 좀 더 많고 복잡한 조건을 확인할 때 쓰이면 좋다.

## If

if 문의 가장 간단한 모양은 if 하나만 사용한 것이다.

if 문의 조건이 true일 때만 조건문을 실행한다.

```swift
var temperatureInFahrenheit = 30
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
}
// Prints "It's very cold. Consider wearing a scarf."
```

위의 코드에서 temperatureInFahrenheit ≤ 32라는 조건을 만족하기 때문에 명령문이 수행된다.

만약 조건을 만족하지 않아서 명령이 수행되지 않아도 종료되는 것이 아닌 그 뒤의 코드들이 수행된다.

if는 else와 함께 사용할 수 있다.

이때 else에는 if의 조건이 false일 때 실행하는 명령문이 들어간다.

```swift
temperatureInFahrenheit = 40
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
} else {
    print("It's not that cold. Wear a t-shirt.")
}
// Prints "It's not that cold. Wear a t-shirt."
```

위의 코드를 보면 if의 조건이 false로 나오게 된다.

이럴 때 else가 있다면 else의 명령문을 수행하게 된다.

만약 조건을 여러 개 사용하고 싶다면 else if를 사용하면 된다.

```swift
temperatureInFahrenheit = 90
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
} else if temperatureInFahrenheit >= 86 {
    print("It's really warm. Don't forget to wear sunscreen.")
} else {
    print("It's not that cold. Wear a t-shirt.")
}
// Prints "It's really warm. Don't forget to wear sunscreen."
```

이렇게 if-else를 사용할 때 마지막에 else만 사용하는 구문은 선택사항이며 제외할 수 도 있다.

## Switch

Switch 구문은 특정 값을 몇 가지 조건으로 비교하여 true로 나오는 조건들 중 첫번째 패턴의 명령을 수행하는 구문이다.

가장 간단한 switch 구문은 switch와 case만 사용한 구문이다.

```swift
let someCharacter: Character = "z"
switch someCharacter {
case "a":
    print("The first letter of the alphabet")
case "z":
    print("The last letter of the alphabet")
default:
    print("Some other character")
}
// Prints "The last letter of the alphabet"
```

위의 코드에서 someCharacter가 조건들에 확인될 값이다.

someCharcter는 "z"인데 이러한 조건이 있기 때문에 해당 조건의 명령이 수행된다.

switch에서 default 구문은 만약 값이 모든 조건에 false가 결과로 나오게 되면 수행될 명령을 선언하는 구문이다.

## No Implicit Fallthrough

C언어와 Objective-C와 다르게 Swift에서의 switch문은 기본적으로 어떤 경우에 만족할 경우 해당 경우의 아랫부분을 확인하지 않는다.

또한 switch 문에서 break문을 요구하지 않는다.

즉, 첫번째로 일치하는 조건을 만나서 명령을 수행하자마자 switch문을 빠져나온다.

> break문이 Swift에서 필수인건 아니지만 case안의 특정 지점에서 멈추도록 하기 위해서 break문을 사용할 수 있다.

이렇기 때문에 두 개 이상의 조건에 만족하는 경우를 방지할 수 있다.

각각의 조건은 하나 이상의 실행문이 포함되어야한다.

```swift
let anotherCharacter: Character = "a"
switch anotherCharacter {
case "a": // Invalid, the case has an empty body
case "A":
    print("The letter A")
default:
    print("Not the letter A")
}
// This will report a compile-time error.
```

위의 코드는 case "a" : 의 조건에서 아무런 실행문이 없기 때문에 잘못된 코드이다.

```swift
let anotherCharacter: Character = "a"
switch anotherCharacter {
case "a", "A":
    print("The letter A")
default:
    print("Not the letter A")
}
// Prints "The letter A"
```

위의 코드와 같이 여러 조건을 함게 사용할 수도 있다.

## Interval Matching

switch에서는 어떠한 간격에 대한 조건을 줄 수도 있다.

```swift
let approximateCount = 62
let countedThings = "moons orbiting Saturn"
let naturalCount: String
switch approximateCount {
case 0:
    naturalCount = "no"
case 1..<5:
    naturalCount = "a few"
case 5..<12:
    naturalCount = "several"
case 12..<100:
    naturalCount = "dozens of"
case 100..<1000:
    naturalCount = "hundreds of"
default:
    naturalCount = "many"
}
print("There are \(naturalCount) \(countedThings).")
// Prints "There are dozens of moons orbiting Saturn."
```

## Tuples

여러 값들을 같은 switch 구문에서 사용하고 싶다면 tuple을 사용하면 된다.

튜플의 각각의 원소는 각각 다른 조건에 의해 테스트 될 수 있다.

만약 튜플에 _를 사용하면 이는 wildcard pattern이라고 하며 어떠한 값도 허용한다는 뜻이다.

```swift
let somePoint = (1, 1)
switch somePoint {
case (0, 0):
    print("\(somePoint) is at the origin")
case (_, 0):
    print("\(somePoint) is on the x-axis")
case (0, _):
    print("\(somePoint) is on the y-axis")
case (-2...2, -2...2):
    print("\(somePoint) is inside the box")
default:
    print("\(somePoint) is outside of the box")
}
// Prints "(1, 1) is inside the box"
```

위의 코드에서 보면 주어진 점은 (1, 1)이다.

이 점이 해당되는 조건은 (-2...2, -2...2)이다.

위의 코드에서 볼 수 있듯, 튜플의 각각의 원소에 대해 조건을 확인할 수 있다.

# <span style="color:blue">Value Bindings</span>

switch의 case에서 일시적인 상수나 변수를 선언해서 사용할 수 있다.

```swift
let anotherPoint = (2, 0)
switch anotherPoint {
case (let x, 0):
    print("on the x-axis with an x value of \(x)")
case (0, let y):
    print("on the y-axis with a y value of \(y)")
case let (x, y):
    print("somewhere else at (\(x), \(y))")
}
// Prints "on the x-axis with an x value of 2"
```

위의 코드에서 let x, let y와 같이 일시적으로 상수나 변수를 선언하여 사용할 수 있고 이렇게 선언되면 다음 케이스에서 사용할 때에는 다시 선언해 줄 필요가 없다.

위의 코드에서 마지막에 선언된 let(x, y)는 마치 default와 비슷한 역할을 하게 된다.

따라서 default 케이스가 필요하지 않게 된다.

Value Binding은 단독 사용보단 주로 where와 사용한다.

```swift
let a = 1

switch a {
case var x where x > 100:
    x = 200
		print(x)
default:
    break
}
```

# <span style="color:blue">Where</span>

switch 구문에서는 where절을 사용하여 추가 조건을 확인할 수 있다.

```swift
let yetAnotherPoint = (1, -1)
switch yetAnotherPoint {
case let (x, y) where x == y:
    print("(\(x), \(y)) is on the line x == y")
case let (x, y) where x == -y:
    print("(\(x), \(y)) is on the line x == -y")
case let (x, y):
    print("(\(x), \(y)) is just some arbitrary point")
}
// Prints "(1, -1) is on the line x == -y"
```

위의 코드와 같이 추가적인 조건을 주어 switch 구문을 사용할 수 있다.

+) where절이란?

- 특정 패턴과 결합하여 조건을 추가하는 역할을 한다.
- 조건 추가 또는 특정 타입을 제한할 때 사용한다.

→ 특정 패턴에 Bool타입 조건을 지정하거나 어떤 타입의 특정 프로토콜 준수 조건을 추가하는 등의 기능이다.

# <span style="color:blue">Compound Cases</span>

' , '로 구분하여 여러 케이스들을 하나의 body와 공유할 수 있다.

어느 하나라도 맞게 되면 해당 케이스의 명령이 수행된다.

만약 조건들이 많다면, 여러 줄에 걸쳐 작성해도 무방하다.

```swift
let someCharacter: Character = "e"
switch someCharacter {
case "a", "e", "i", "o", "u":
    print("\(someCharacter) is a vowel")
case "b", "c", "d", "f", "g", "h", "j", "k", "l", "m",
     "n", "p", "q", "r", "s", "t", "v", "w", "x", "y", "z":
    print("\(someCharacter) is a consonant")
default:
    print("\(someCharacter) is not a vowel or a consonant")
}
// Prints "e is a vowel"
```

물론 Compound Cases에서도 value binding을 사용할 수 있다.

```swift
let stillAnotherPoint = (9, 0)
switch stillAnotherPoint {
case (let distance, 0), (0, let distance):
    print("On an axis, \(distance) from the origin")
default:
    print("Not on an axis")
}
// Prints "On an axis, 9 from the origin"
```

# <span style="color:blue">Control Transfer Statements</span>

Control Transfer Statements는 코드가 실행될 때 다른 코드로 명령을 줘서 실행되는 순서를 바꾸는 역할을 한다.

Swift에서는 continue, break, fallthrough, return, throw의 5가지 Control Transfer Statements를 제공한다.

## Continue

Continue 문은 루프가 수행 중인 작업을 중지하고 다음 반복의 시작 지점부터 다시 시작하라는 의미이다.

현재 반복에서는 할 일을 다 했으니 다음 반복을 수행하자라는 의미와 같다.

```swift
let puzzleInput = "great minds think alike"
var puzzleOutput = ""
let charactersToRemove: [Character] = ["a", "e", "i", "o", "u", " "]
for character in puzzleInput {
    if charactersToRemove.contains(character) {
        continue
    }
    puzzleOutput.append(character)
}
print(puzzleOutput)
// Prints "grtmndsthnklk"
```

위의 코드에서 보면 if문의 조건을 만족할 때 마다 바로 다음 반복으로 넘어가게 된다.

## Break

Break문은 control flow를 즉시 종료하는 기능을 가지고 있다.

Break문은 switch또는 loop문의 실행을 다른 경우보다 빨리 종료하고 싶을 때 사용할 수 있다.

# <span style="color:blue">Break in a Loop Statement</span>

만약 loop문 안에서 break를 사용하면 루프는 즉시 종료되고 루프의 마지막 글자인 " } "로 이동한다.

현재 루프가 반복 중인 곳에서 종료되고 더 이상 반복이 진행되지 않는다.

## Break in a Switch Statement

Break가 switch문에서 사용되면 switch문은 즉시 종료되고 바로 switch 문의 마지막 글자인 "}"로 이동한다.

이러한 코드는 switch문에서 몇 가지 케이스를 무시할 때 사용할 수 있다.

Swift의 switch문은 케이스마다 반드시 실행문이 존재해야 하기 때문에 무시하고 싶은 케이스에 break를 사용하면 된다.

```swift
let numberSymbol: Character = "三"  // Chinese symbol for the number 3
var possibleIntegerValue: Int?
switch numberSymbol {
case "1", "١", "一", "๑":
    possibleIntegerValue = 1
case "2", "٢", "二", "๒":
    possibleIntegerValue = 2
case "3", "٣", "三", "๓":
    possibleIntegerValue = 3
case "4", "٤", "四", "๔":
    possibleIntegerValue = 4
default:
    break
}
if let integerValue = possibleIntegerValue {
    print("The integer value of \(numberSymbol) is \(integerValue).")
} else {
    print("An integer value could not be found for \(numberSymbol).")
}
```

## Fallthrough

Swift의 switch문은 한 케이스를 만족하면 바로 switch문을 빠져나온다.

하지만 C언어에서는 한 케이스를 만족해도 break 코드가 없다면 다음 케이스도 확인을 하는데 이 때문에 오류가 발생한다.

그래서 늘 케이스의 마지막에 break를 넣어줘야한다.

하지만 swift에서도 C언어에서처럼 한 케이스를 만족하더라도 다음 케이스도 보고 싶다면 fallthrough를 사용하면 된다.

```swift
let integerToDescribe = 5
var description = "The number \(integerToDescribe) is"
switch integerToDescribe {
case 2, 3, 5, 7, 11, 13, 17, 19:
    description += " a prime number, and also"
    fallthrough
default:
    description += " an integer."
}
print(description)
// Prints "The number 5 is a prime number, and also an integer."
```

위의 코드에서 integerToDescribe = 5이므로 첫 번째 케이스의 조건에 맞게 된다.

하지만 fallthrough가 있기 때문에 다음에 있는 default 구문의 명령도 수행하게 된다.

## Labeled Statements

Swift에서는 다른 loop와 조건문 안에 또 다른 loop와 조건문을 중첩하여 복잡한 제어 흐름 구조를 만들 수 있다.

이렇게 만든 루프와 조건문은 break를 사용해서 조기에 종료할 수 있다.

이럴 때 종료할 loop와 조건문을 명시적으로 나타내주는게 효과적일 수 있다.

마찬가지로 continue문도 어떤 루프에 적용되는 것인지 명시하는 것이 유용하다.

이러한 방법을 사용하기 위해 명령문 레이블을 사용하여 루프와 조건문을 표시할 수 있다.

명령문 레이블은 해당 루프 혹은 조건문 앞에 명시해주면 된다.

```swift
var age = 20
var name = "Ick"
checkage: while age < 30{
    if name == "Ick"{
        break checkage
    }
    else{
        age += 1
    }
}
```

위의 코드와 같이 사용할 수 있다.

# <span style="color:blue">Early Exit</span>

If문과 비슷하게 guard문도 조건의 결과에 따라 명령문을 실행한다.

guard문의 명령문은 **반드시 조건이 true여야 실행 가능하다.**

그렇기 때문에 guard문에는 항상 else문이 함께 있어야 한다.

```swift
func greet(person: [String: String]) {
    guard let name = person["name"] else {
        return
    }

    print("Hello \(name)!")

    guard let location = person["location"] else {
        print("I hope the weather is nice near you.")
        return
    }

    print("I hope the weather is nice in \(location).")
}

greet(person: ["name": "John"])
// Prints "Hello John!"
// Prints "I hope the weather is nice near you."
greet(person: ["name": "Jane", "location": "Cupertino"])
// Prints "Hello Jane!"
// Prints "I hope the weather is nice in Cupertino."
```

만약 guard문의 조건이 true라면 guard문의 " } " 부분 뒤의 코드들이 실행된다.

guard문에서도 binding을 사용할 수 있는데 이때 선언된 변수나 상수는 guard문이 선언된 나머지 코드에서도 사용할 수 있다.

 만약 조건이 false라면 else문의 명령을 수행한다.

이때 else문의 명령은 코드를 종료하기 위해 return, break, continue, throw와 같은 제어 전송 명령문으로 작성되거나 fatalError(_:file:line:)과 같이 리턴되지 않는 함수 또는 method를 호출해야한다.

guard문은 조건이 반드시 true가 되어야 하는 곳에서 사용하면 좋다.

if문과의 차이점을 얘기하자면, else 구문이 반드시 필요하다는 점과 참일때의 실행 코드 블럭이 없다는 것이 있다.

**+) guard문의 장점**

1. 코드의 중첩을 막아준다.
2. guard 구문을 많이 사용해도 코드의 depth가 깊어지지 않는다.

# <span style="color:blue">Checking API Availability</span>

Swift는 API 사용 가능성 확인을 지원하기 때문에 실수로 사용할 수 없는 API를 사용하는 일을 방지할 수 있다.

컴파일러는 SDK의 사용 가능 정보를 사용하여 코드에 사용된 모든 API가 프로젝트에 지정된 배포 대상에서 사용가능한 지 확인해준다.

만약 사용할 수 없는 API를 사용하려고 하면 컴파일 오류를 발생시킨다.

개발자는 if, guard문을 사용해서 availability condition을 사용할 수 있다.

```swift
if #available(iOS 10, macOS 10.12, *) {
    // Use iOS 10 APIs on iOS, and use macOS 10.12 APIs on macOS
} else {
    // Fall back to earlier iOS and macOS APIs
}
```

위의 코드는 사용 가능 조건이 iOS 10 이상, macOS 10.12 이상에서만 실행되도록 만든 것이다.

마지막 인수 *는 필수 이고 다른 플랫폼에서 if에서 지정한 최소 배포 버전 이상의 버전에서만 실행되도록 지정한다.

