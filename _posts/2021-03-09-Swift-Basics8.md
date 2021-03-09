---
title: "Swift-Enumerations"
excerpt: "Swift 공식 문서"
toc: true
toc_sticky: true
toc_label: "Swift-Enumerations"
categories:
 - iOS 공식문서
tags:
 - iOS
---

Enumerations(열거형)는 연관성이 있는 값들을 모아놓은 것을 말한다.

C언어에서의 열거형과 비슷하게 열거형 속 각각의 값에 Int 타입 값을 줄 수 있다.

Swift에서의 열거형은 좀 더 융통성이 있어서 열거의 각 경우에 값을 꼭 제공할 필요는 없다.

Raw value라고 알려진 각 케이스의 값은 String, Character, Int, Float, Double과 같은 값 일 수 있다.

Swift의 열거형은 일급 객체이다.

또한 클래스와 비슷하게 property를 계산하고 추가적인 정보를 처리하고 관려된 기능을 제공하는 인스턴스 method를 지원한다.

생성자를 정의할 수도 있고 원래 구현된 기능 이상의 것을 추가할 수 있도록 확장 기능도 제공한다.

프로토콜을 채택해서 표준 기능을 사용할 수도 있다.

참고로 **열거형은 값타입**이다.

# <span style="color:blue">Enumeration Syntax</span>

열거형을 선언하기 위해서는 enum 키워드를 사용하면 된다.

```swift
enum CompassPoint {
    case north
    case south
    case east
    case west
}
```

열거형은 위의 코드와 같이 선언될 수 있다.

여기서 보이는 north, south, east, west가 enumeration cases(열거 케이스)입니다.

더 추가하고 싶다면 case 키워드를 사용해서 추가해 주면 된다.

Swift 열거형에서는 C언어와 Ojective-C와 다르게 기본적으로 정숫값이 설정되어 있지 않다.

```swift
enum Planet {
    case mercury, venus, earth, mars, jupiter, saturn, uranus, neptune
}
```

위의 코드와 같이 한 줄에 나열할 수 있다.

열거형을 만들게 되면 하나의 새로운 타입처럼 사용할 수 있다.

그렇기 때문에 열거형은 Swift의 이름 규칙에 따라 이름을 대문자로 시작해야한다.

```swift
var directionToHead = CompassPoint.west
```

위의 코드와 같이 열거형의 하나의 케이스에 접근할 수도 있다.

또한 이제 directionToHead는 선언됐기 때문에 CompassPoint타입이므로 아래와 같이 수정이 가능하다.

```swift
directionToHead = .east
```

# <span style="color:blue">Matching Enumeration Values with a Switch Statement</span>

열거형은 switch 구문과 함께 사용하면 다양하게 활용할 수 있다.

```swift
directionToHead = .south
switch directionToHead {
case .north:
    print("Lots of planets have a north")
case .south:
    print("Watch out for penguins")
case .east:
    print("Where the sun rises")
case .west:
    print("Where the skies are blue")
}
// Prints "Watch out for penguins"
```

위의 코드를 보면 directionToHead는 아까 만든 열거형의 .south 케이스이다.

따라서 switch 구문의 케이스 중 맞는 것으로 명령을 수행한다.

Switch구문의 케이스가 CompassPoint 열거형의 케이스를 모두 포함하기 때문에 default는 굳이 사용하지 않아도 된다.

하지만 하나라도 빼먹으면 아래와 같이 default를 사용해야한다.

```swift
let somePlanet = Planet.earth
switch somePlanet {
case .earth:
    print("Mostly harmless")
default:
    print("Not a safe place for humans")
}
// Prints "Mostly harmless"
```

# <span style="color:blue">Iterating over Enumeration Cases</span>

열거형을 사용할 때 모든 케이스에 바로 접근할 수 있으면 굉장히 편리하다.

Swift 열거형에서는 이 기능을 지원하지만 열거형에서 기본적으로 제공하지는 않는다.

Caselterable 프로토콜을 사용해야 이 기능을 사용할 수 있다.

```swift
enum Beverage: CaseIterable {
    case coffee, tea, juice
}
let numberOfChoices = Beverage.allCases.count
print("\(numberOfChoices) beverages available")
// Prints "3 beverages available"
```

위의 코드와 같이 열거형에서 CaseIterable 프로토콜을 채택하고 allCases property를 사용하면 케이스들이 Array로 반환되게 된다.

Array타입은 count property로 값의 개수를 구할 수 있기 때문에 이렇게 열거형의 케이스 개수를 구할 수 있게 된다.

```swift
for beverage in Beverage.allCases {
    print(beverage)
}
// coffee
// tea
// juice
```

물론 개수 말고도 위와 같이 for-in 구문과 함께 사용하면 case의 종류에도 접근할 수 있다.

# <span style="color:blue">Associated Values</span>

앞에서의 예는 모두 열거형의 케이스가 명시적으로 정의되는 것들이다.

하지만 가끔은 다른 타입의 값과 열거형의 케이스 값을 함께 저장할 수 있는게 유용할 때가 있다.

이렇게 열거형의 케이스와 저장되는 다른 값을 Associated Value라고 한다.

어떠한 타입의 값도 열거형과 함께 사용될 수 있고, 각각의 열거 케이스마다 다른 타입을 사용할 수 있다.

이러한 열거형을 discriminated unions, tagged unions, variants in other programming language라고 한다.

에를 들어 재고 관리 시스템이 서로 다른 두 종류의 바코드로 재고를 관리한다고 하자.

일부 제품에는 UPC 형태의 1D 바코드가 있고, 0~9 까지의 숫자를 사용해 제조업체 코드 숫자와 제품 코드 숫자를 나타낸다고 가정하겠다.

! [img1](https://user-images.githubusercontent.com/65299607/110441022-a5ff0680-80fc-11eb-983d-9de09029d154.png)

또 어떠한 제품은 QR코드 타입의 2D 바코드로 표시되며 이는 ISO 8859-1문자를 사용할 수 있고 최대 2953길이의 문자열을 인코딩 가능하다고 가정하겠다.

![img2](https://user-images.githubusercontent.com/65299607/110441029-a8616080-80fc-11eb-9d61-0a645b4ad369.png)

이와 같이 다른 두 가지 타입의 케이스를 열거형에서 한 번에 다루려면 다음과 같이 나타낼 수 있다.

```swift
enum Barcode {
    case upc(Int, Int, Int, Int)
    case qrCode(String)
}
```

upc 바코드 케이스는 Int 타입을 4개 사용하는 튜플의 형태로 만들었고, QR코드 케이스는 String 타입으로 만들었다.

이렇게 해서 각각의 타입마다 새로운 값을 생성할 수 있다.

```swift
var productBarcode = Barcode.upc(8, 85909, 51226, 3)
productBarcode = .qrCode("ABCDEFGHIJKLMNOP")
```

이렇게 되면 productBarcode 변수에느 한 시점에 하나의 값만 저장할 수 있게 된다.

즉 upc바코드 타입이나 QR코드 둘 중 하나만 저장할 수 있다는 것이다.

```swift
switch productBarcode {
case .upc(let numberSystem, let manufacturer, let product, let check):
    print("UPC: \(numberSystem), \(manufacturer), \(product), \(check).")
case .qrCode(let productCode):
    print("QR code: \(productCode).")
}
// Prints "QR code: ABCDEFGHIJKLMNOP."
```

즉 위와 같이 switch와 함께 사용해서 해당 값에 있는 값을 추출할 수 있다.

또한 여러 값이 들어있는 associated value를 위해 값들마다 변수 또는 상수로 정해 이름을 붙여 사용할 수도 있다.

# <span style="color:blue">Raw Value</span>

위에서 본 Associated Value가 열거형 타입이 여러 타입으로 이루어진 값을 저장하는 방법이었다면, Raw Value는 **기본값으로 미리 선언해 둘 수 있는 타입**이다.

```swift
enum ASCIIControlCharacter: Character {
    case tab = "\t"
    case lineFeed = "\n"
    case carriageReturn = "\r"
}
```

위의 코드에서 ASCIIControlCharacter 열거형은 Character 타입으로 정의된다.

Raw Value는 위와 같이 Character일 수도 있고 Int, Float, Double, String 타입이 될 수 있다.

하지만 각각의 케이스마다 Raw Value는 고유한 값이어야 한다.

Raw Value는 Associated Value와는 다르다.

Raw Value는 열거형을 정의할 때 미리 채워진 값으로 설정하는 것이고,

Associated Value는 타입만 정해두고 나중에 채워주는 것이다.

Raw Value는 새로운 인스턴스가 모두 같은 값을 가지지만, Associated Value는 변할 수 있다.

## Implicity Assigned Raw Value

Int, String으로 열거형의 Raw Value를 선언하면 모든 케이스에 대해 Raw Value를 선언하지 않아도 된다.

선언하면 자신이 선언한 값으로 Raw Value가 되긴하지만, 선언안하면 Swift가 알아서 값을 할당해준다.

```swift
enum Planet: Int {
    case mercury = 1, venus, earth, mars, jupiter, saturn, uranus, neptune
}
let earthsOrder = Planet.earth.rawValue
// earthsOrder is 3
```

예를 들어 위의 코드에서 보면 Raw Value를 mercury에만 1이라고 선언해줬다.

그 뒤의 케이스들에는 Raw Value를 선언하지 않았다.

하지만 Swift가 알아서 venus에는 2, earth에는 3이라는 값을 할당해준다.

```swift
enum CompassPoint: String {
    case north, south, east, west
}
let sunsetDirection = CompassPoint.west.rawValue
// sunsetDirection is "west"
```

만약 위의 코드처럼 아무것도 선언해주지 않으면 케이스의 이름이 String 타입으로 Raw Value가 된다.

말이 헷갈릴 수 있는데 **케이스의 이름이 곧 값으로 들어간다는 것**이다.

## Initializing from a Raw Value

열거형의 새로운 인스턴스를 생성할 때 변수나 상수에 rawValue라는 매개 변수로 초기화 할 수 있는데,

이렇게 되면 반환값으로 해당 Raw Value가 존재하면 해당 케이스의 값이 나오고 존재하지 않는 Raw Value라면 nil이 반환된다.

즉, 옵셔널 타입으로 반환된다는 것이다.

```swift
let possiblePlanet = Planet(rawValue: 7)
// possiblePlanet is of type Planet? and equals Planet.uranus
```

위의 Planet처럼 값을 미리 선언해놓았으면 어찌되었건 값은 나오겠지만, 없는 경우에는 nil이 반환되기 때문에 이렇게 초기화를 하면 안된다.

if let 구문을 이용한 옵셔널 바인딩을 사용해서 안전하게 추출해야한다.

```swift
let positionToFind = 11
if let somePlanet = Planet(rawValue: positionToFind) {
    switch somePlanet {
    case .earth:
        print("Mostly harmless")
    default:
        print("Not a safe place for humans")
    }
} else {
    print("There isn't a planet at position \(positionToFind)")
}
// Prints "There isn't a planet at position 11"
```

위의 코드와 같이 11이라는 Raw Value는 없으므로 if let 구문에서 else에 있는 명령을 수행하게 된다.

# <span style="color:blue">Recursive Enumerations</span>

재귀 열거형은 어떤 열거형의 케이스에 Associated Value 타입으로 자신의 열거형 타입이 들어간 경우를 말한다.

이렇게 자신의 열거형 타입을 사용하게 되면 해당 케이스 앞에 indirect라는 키워드를 사용해야한다.

예를 보면 아래와 같다.

```swift
enum ArithmeticExpression {
    case number(Int)
    indirect case addition(ArithmeticExpression, ArithmeticExpression)
    indirect case multiplication(ArithmeticExpression, ArithmeticExpression)
}
```

여러 번 반복해서 쓰는 것이 싫다면 아래와 같이 제일 처음에 써주는 방법도 존재한다.

```swift
indirect enum ArithmeticExpression {
    case number(Int)
    case addition(ArithmeticExpression, ArithmeticExpression)
    case multiplication(ArithmeticExpression, ArithmeticExpression)
}
```

위의 예제에서 addition,multiplication 케이스에서 recursive enumeration이 사용됐고 해당 케이스에서는 Associated Value 타입으로 자시의 열거형 타입을 가지고 있다.

```swift
let five = ArithmeticExpression.number(5)
let four = ArithmeticExpression.number(4)
let sum = ArithmeticExpression.addition(five, four)
let product = ArithmeticExpression.multiplication(sum, ArithmeticExpression.number(2))
```

이는 위의 코드와 같이 사용할 수 있다.

이를 실제 재귀 함수에서 사용할 수 있다.

아래의 예와 같다.

```swift
func evaluate(_ expression: ArithmeticExpression) -> Int {
    switch expression {
    case let .number(value):
        return value
    case let .addition(left, right):
        return evaluate(left) + evaluate(right)
    case let .multiplication(left, right):
        return evaluate(left) * evaluate(right)
    }
}

print(evaluate(product))
// Prints "18"
```

