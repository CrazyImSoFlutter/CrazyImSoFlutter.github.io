---
title: "Swift-Structures and Classes"
excerpt: "Swift 공식 문서"
toc: true
toc_sticky: true
toc_label: "Swift-Structures and Classes"
categories:
 - iOS 공식문서
tags:
 - iOS
---

Structures(구조체)와 Classes(클래스)는 여러 개의 프로퍼티와 메소드를 한 번에 다룰 수 있는 구조이다.

다른 언어들과는 다르게 swift에서는 구조체와 클래스를 만드는데 별도의 인터페이스 및 구현 파일을 만들 필요가 없다.

하나의 파일에 구조체와 클래스를 정의하면 외부 인터페이스에서 해당 구조체와 클래스를 자동으로 사용할 수 있도록 만들어준다.

# <span style="color:blue">Comparing Structures and Classes</span>

Swift의 구조체와 클래스는 공통점이 많다.

- 값을 저장할 프로퍼티를 선언할 수 있다.
- 함수적 기능을 하는 method를 선언할 수 있다.
- 내부 값에 첨자 구문(.)을 사용해서 접근할 수 있다.
- 생성자를 사용해 초기화를 할 수 있다.
- 프로토콜을 채택해서 표준 기능을 제공할 수 있다.

클래스에는 구조체에 없는 몇 가지 기능이 있다.

- 한 클래스가 다른 클래스의 특성을 사용할 수 있는 상속을 지원한다.
- 타입 캐스팅을 통해 클래스 인스턴스의 타입을 런타임에서 확인할 수 있다.
- Deinitializer를 사용하면 클래스 인스턴스의 할당이 해제된다.
- 클래스 인스턴스의 Reference Counting(참조 횟수)은 둘 이상의 참조를 허용한다.

이런 클래스만 지원하는 기능들은 복잡성을 증가시킨다.

그래서 보통은 구조체를 선호하고 이러한 기능이 필요할 때 클래스를 사용한다.

실제로 대부분 사용자 지정 데이터 형식은 구조체와 열거형이다.

## Definition Syntax

구조체와 클래스는 비슷하게 선언할 수 있다.

구조체는 struct 키워드를, 클래스는 class 키워드를 사용하면 된다.

```swift
struct Resolution {
    var width = 0
    var height = 0
}
class VideoMode {
    var resolution = Resolution()
    var interlaced = false
    var frameRate = 0.0
    var name: String?
}
```

구조체나 클래스를 선언할 때는 Swift의 스타일을 따라주는 것이 좋다.

구조체나 클래스는 대문자로 시작하는 것이 좋고, 그 안의 method나 프로퍼티들은 소문자로 시작하는 것이 좋다.

위의 코드에서 변수나 상수를 선언하는 방법은 기존의 방법과 같다.

resolution이라는 변수에는 Resolution 구조체 인스턴스가 만들어졌다.

## Structure and Class Instances

위에서 정의한 Resolution이나 VideoMode는 구조체와 클래스의 모양만 정의한 것이지 실제로 쓰이는 값은 아니다.

정의된 구조체와 클래스를 사용하기 위해서는 인스턴스를 만들어 사용해야한다.

```swift
let someResolution = Resolution()
let someVideoMode = VideoMode()
```

인스턴스를 만드는 방법은 위의 코드와 같다.

가장 간단한 방법은 구조체나 클래스의 이름을 쓰고 뒤에 괄호를 붙이는 것이다.

이렇게 하면 default 값으로 구조체, 클래스 인스턴스를 생성한다.

## Accessing Properties

프로퍼티에 접근하기 위해서는 ' . '을 사용하면 된다.

인스턴스의 이름 뒤에 ' . '을 붙이고 프로퍼티의 이름을 쓰면 프로퍼티에 접근할 수 있다.

```swift
print("The width of someResolution is \(someResolution.width)")
// Prints "The width of someResolution is 0"
```

위에서 선언한 someVideoMode 클래스의 resolution 프로퍼티는 구조체였다.

이럴 때 resolution 프로퍼티의 프로퍼티에 접근하기 위해서는 ' . '을 또 사용하면 된다.

```swift
print("The width of someVideoMode is \(someVideoMode.resolution.width)")
// Prints "The width of someVideoMode is 0"
```

변수 프로퍼티는 값을 변경할 수 있다.

```swift
someVideoMode.resolution.width = 1280
print("The width of someVideoMode is now \(someVideoMode.resolution.width)")
// Prints "The width of someVideoMode is now 1280"
```

## Memberwise Initializers for Structure Types

모든 구조체에는 새로운 구조체 인스턴스의 프로퍼티들을 초기화 하기 위해 자동적으로 생성되는 Memberwise initialize가 존재한다.

새로운 인스턴스의 초기화 값은 프로퍼티 이름으로 초기화할 수 있다.

```swift
let vga = Resolution(width: 640, height: 480)
```

구조체와 다르게 클래스 인스턴스에는 default meberwise initialize가 없다.

그렇기 때문에 생성자로 직접 초기화해야한다.

# <span style="color:blue">Structures and Enumerations Are Value Types</span>

Value Type(값 타입)은 변수, 상수에 할당되거나 함수에 전달될 때 값이 복사되는 것을 말한다.

Int, Double, Float, Bool, String, Array, Dictionary는 모두 값 타입이다.

Swift의 모든 구조체와 열거형은 값 타입이다.

이는 모든 구조체, 열거형 인스턴스는 값 타입이고 그것들의 프로퍼티는 항상 복사되며 전달된다는 것을 의미한다.

> Array, Dictionary, String과 같은 표준 라이브러리에 의해 정의된 컬렉션 타입은 최적화를 통해 복사 비용을 줄였다. 이런 컬렉션은 원본을 즉시 복사를 하지 않고 원본 인스턴스와 복사본 사이에 저장되는 메모리를 공유한다. 컬렉션의 값이 수정되려고 하면 수정 직전에 원본을 복사한다. 이렇게 때문에 코드에서는 즉시 복사된 것 처럼 보인다.

```swift
let hd = Resolution(width: 1920, height: 1080)
var cinema = hd
cinema.width = 2048
print("cinema is now \(cinema.width) pixels wide")
// Prints "cinema is now 2048 pixels wide"
print("hd is still \(hd.width) pixels wide")
// Prints "hd is still 1920 pixels wide"
```

앞에서 선언한 Resolution 구조체의 인스턴스로 hd를 선언한다.

변수 cinema를 선언해서 hd 인스턴스를 할당한다.

그 후에 cinema의 width 프로퍼티를 수정하면 어떻게 될까?

구조체는 값 타입이기 때문에 cinema에 hd 인스턴스를 할당할 때 복사가 일어난다.

그렇기 때문에 cinema와 hd는 서로 다른 인스턴스인 것이다.

같은 메모리를 공유하는 것이 아닌 각자 다른 메모리에 상주해 있는 것이다.

따라서 cinema의 프로퍼티를 수정해도 hd에는 아무런 영향이 없다.

![img](https://user-images.githubusercontent.com/65299607/112917196-25508a80-913d-11eb-9758-d8e61db95c25.png)

이와 같은 현상이 열거형에도 나타난다.

```swift
enum CompassPoint {
    case north, south, east, west
    mutating func turnNorth() {
        self = .north
    }
}
var currentDirection = CompassPoint.west
let rememberedDirection = currentDirection
currentDirection.turnNorth()

print("The current direction is \(currentDirection)")
print("The remembered direction is \(rememberedDirection)")
// Prints "The current direction is north"
// Prints "The remembered direction is west"
```

# <span style="color:blue">Classes Are Reference Types</span>

클래스는 참조타입이다.

참조 타입이란 변수나 상수에 할당될 때 복사가 아닌 메모리의 같은 부분을 보는 것이다.

```swift
let tenEighty = VideoMode()
tenEighty.resolution = hd
tenEighty.interlaced = true
tenEighty.name = "1080i"
tenEighty.frameRate = 25.0

let alsoTenEighty = tenEighty
alsoTenEighty.frameRate = 30.0

print("The frameRate property of tenEighty is now \(tenEighty.frameRate)")
// Prints "The frameRate property of tenEighty is now 30.0"
```

VideoMode 클래스의 인스턴스로 tenEighty를 선언했다.

tenEighty를 상수 alsoTenEighty에 할당한 후 alsoTenEighty의 프로퍼티를 수정하면 어떻게 될까?

alsoTenEighty와 tenEighty의 값 모두 수정되어버린다.

![img](https://user-images.githubusercontent.com/65299607/112917204-284b7b00-913d-11eb-843d-0e9607a47b37.png)

두 클래스 인스턴스는 같은 메모리를 참조만 하기 때문에 둘 중 하나만 수정하더라도 두 개의 인스턴스 모두 수정된다.

## Identity Operators

Swift에는 두 개의 변수나 상수가 같은 인스턴스를 참조하는지 확인하기 위한 연산자가 존재한다.

둘이 같은 지 확인하는 ===연산자와,

같지 않은 지 확인하는 !== 연산자가 있다.

```swift
if tenEighty === alsoTenEighty {
    print("tenEighty and alsoTenEighty refer to the same VideoMode instance.")
}
// Prints "tenEighty and alsoTenEighty refer to the same VideoMode instance."
```

> ===와 ==은 다른 연산자이다.
===는 클래스 인스턴스를 참조하는 것을 확인하는 연산자이다.

## Pointers

C, C++, Objective-C에서처럼 이러한 참조가 포인터를 사용한다.

일부 참조 타입의 인스턴스를 가지는 상수, 변수는 C의 포인터와 비슷하지만 메모리에 대한 직접적인 포인터가 아니기 때문에 *를 써주지 않아도 된다.

표준 라이브러리에서는 포인터 타입을 직접적으로 사용해야하는 포인터와 버퍼 유형을 제공한다.

