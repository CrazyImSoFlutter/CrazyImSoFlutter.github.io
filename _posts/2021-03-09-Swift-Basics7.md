---
title: "Swift-Closures"
exercpt: "Swift 공식 문서"
toc: true
toc_sticky: true
toc_label: "Swift-Closures"
categories:
 - iOS 공식문서
tags:
 - iOS
---

Closure(클로저)는 코드에서 함수적인 것을 독립적으로 사용할 수 있는 코드이다.

다른 프로그래밍 언어의 lambda와 비슷한 역할을 한다.

이러한 클로저는 정의된 상수나 변수에 대해 값을 저장하고 캡쳐할 수 있다.

Swift는 이러한 동작을 위해 모든 메모리 관리를 처리해준다.

전역 함수, 중첩 함수(Nested function)가 Function 단원에서 설명되었었는데 이는 클로저의 특별한 케이스 중 하나이다.

그럼 클로저가 어떤 모양을 가질 수 있는 지 부터 살펴보겠다.

클로저는 다음 3개의 모양 중 하나를 가지게 된다.

1. 전역 함수는 이름을 가지고 어떠한 값도 캡쳐를 하지 않는 클로저다.
2. 중첩 함수는 이름을 가지고 그것을 포함하는 enclosing 함수의 값들을 캡쳐할 수 있는 클로저다.
3. 클로저 표현식은 이름이 없는 클로저로 주변의 코드에서 값들을 캡쳐할 수 있는 클로저다.

Swift의 클로저는 깔끔한 구문을 위해 최적화 기능이 있다.

1. 구문에서 매개 변수, 리턴 값 타입 유추를 할 수 있다.
2. 클로저에서 암시적으로 반환값을 반환할 수 있다.
3. 매개변수의 인수 이름을 간단히 할 수 있다.
4. Trailing Closure Syntax (함수의 마지막을 클로저로 마무리할 수 있다.)

# <span style="color:blue">Closure Expressions</span>

중첩 함수는 그것을 감싸고 있는 함수 안에서 함수를 정의하여 정의한 함수를 이름으로 쉽게 사용할 수 있는 수단이다.

하지만 이름도 없고 선언도 없이 사용할 수 있다면 좀 더 편리하지 않을까.

보통 함수나 method가 하나 이상의 매개 변수를 가질 때 이름과 선언 없이 사용하면 코드를 짧게 작성할 수 있기 때문에 좋다.

Closure Expressions(클로저 표현식)은 간단하게 클로저를 작성하는 방법이다.

이렇게 간단하게 작성하기 위해서는 몇가지 최적화 방법을 제공한다.

다음에 소개할 정렬 method로 이런 방법을 알아보겠다.

## The Sorted Method

Swift의 기본 라이브러리에서 제공하는 sorted(by:) method는 사용자가 정의한 값들을 Array 타입으로 반환해주는 클로저이다.

sorted(by:) method는 Array를 반환해주는 method이기 때문에 Array를 정렬하고 저장하고 싶다면 새로운 변수나 상수에 할당해줘야한다.

```swift
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
```

다음과 같은 String Array를 정렬해보겠다.

sorted(by:) method는 반환할 Array 타입과 동일한 타입의 함수 타입을 매개변수로 받고 값이 오름차순으로 정렬할 지 내림차순으로 정렬할 지에 대한 부분을 결정하는 Bool 값을 반환하는 클로저를 입력받는다.

즉, 클로저는 위의 Array를 정렬하기 위해서는 (String, String) -> Bool의 함수 타입을 필요로 하는 것이다.

```swift
func backward(_ s1: String, _ s2: String) -> Bool {
    return s1 > s2
}
var reversedNames = names.sorted(by: backward)
// reversedNames is equal to ["Ewa", "Daniella", "Chris", "Barry", "Alex"]
```

위와 같은 모습으로 나타낼 수 있다.

만약 s1문자열이 s2보다 크다면 backward함수는 true를 반환해서 최종적으로 반환할 Array에서는 s1이 s2보다 앞에 있어야 한다는 것을 나타낸다.

하지만 이렇게 작성하면 조금 비효율적이기 때문에 클로저 표현식 구문을 사용하여 인라인 표현 방식으로 나타내는 게 더 좋다.

## Closure Expression Syntax

클로저를 사용하는 방법을 보겠다.

```swift
{ ( parameters ) -> return type in
    statements
}
```

위의 방식이 클로저 표현식을 사용하는 방법이다.

여기서 사용되는 매개 변수에는 in-out 매개 변수가 쓰여도 된다.

하지만 그렇게 하면 당연히 default 값은 가질 수 없다. 

Variadic 매개 변수를 사용할 수 있고, Tuple도 매개 변수나 반환 값에 사용될 수 있다.

위의 backward(_:_:)함수를 클로저 표현식 구문으로 나타내 보겠다.

```swift
reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in
    return s1 > s2
})
```

backward(_:_:)라는 함수를 아예 매개 변수를 써주는 ()속에 집어넣었다.

클로저의 실행문은 in 키워드 다음에 쓰면 된다.

만약 위의 코드처럼 짧은 코드라면 한 줄에 써도 된다.

```swift
reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in return s1 > s2 } )
```

## Inferring Type From Context

Swift는 sorted(by:) method에서 매개 변수로 함수 타입을 받기 때문에 결과적으로 반환할 값의 타입을 유추할 수 있다.

즉, 위의 예에서는 String Array를 정렬할 것이기 때문에 (String, String) -> Bool 이라는 함수 타입을 받을 것이란 것을 유추할 수 있으므로 굳이 써주지 않아도 되는 것이다.

```swift
reversedNames = names.sorted(by: { s1, s2 in return s1 > s2 } )
```

위의 코드는 더 짧아졌지만 아까 작성한 코드와 동일한 기능을 한다.

이렇게 하면 코드를 이해할 때 어려울 수 있기 때문에 아까처럼 타입을 명시하는 방법이 더 좋을 수 있다.

## Implicit Returns from Single-Expression Closures

이번엔 클로저에서 return 키워드도 생략해보겠다.

```swift
reversedNames = names.sorted(by: { s1, s2 in s1 > s2 } )
```

이 코드를 보면 s1 > s2의 결과가 Bool이기 때문에 Bool 값을 반환한다고 유추할 수 있다.

그래서 return 키워드를 생략해도 큰 문제가 없게 된다.

## Shortand Argument Names

Swift는 인라인 클로저에서 인수 이름(위의 코드에서는 s1, s2)을 간단하게 사용하는 방법을 제공한다.

인수 이름은 순서에 따라 $0, $1, $2와 같이 사용될 수 있다.

즉, 인수 이름을 $0, $1과 같이 단순화할 수 있고 Swift가 이를 어떤 인수인지 유추하여 잘 수행할 수 있다.

여기서 in 키워드도 생략할 수 있는데 생략한 코드를 보면,

```swift
reversedNames = names.sorted(by: { $0 > $1 } )
```

위의 코드가 in 키워드 마저 생략해버린 클로저다.

여기서 $0, $1은 아까 s1, s2와 같은 의미로 String 타입의 인수 이름을 나타낸다.

## Operator Methods

Swift의 String은 비교 연산자(<, >)를 사용해서 비교할 수 있다.

그렇게 하면 Bool 값이 반환되는데 이러한 것을 사용해서 클로저 구문을 짧게 만들면 다음과 같아진다.

```swift
reversedNames = names.sorted(by: >)

// first code
reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in
    return s1 > s2
})
```

# <span style="color:blue">Trailing Closures</span>

만약 함수에서 마지막 인수로 클로저 표현식을 사용하고 싶은데 표현식이 긴 경우에는 후행 클로저로 작성할 수 있다.

후행 클로저가 함수의 인수인 경우에도 함수 호출의 괄호 뒤에 후행 클로저를 작성하면 된다.

```swift
func someFunctionThatTakesAClosure(closure: () -> Void) {
    // function body goes here
}

// Here's how you call this function without using a trailing closure:

someFunctionThatTakesAClosure(closure: {
    // closure's body goes here
})

// Here's how you call this function with a trailing closure instead:

someFunctionThatTakesAClosure() {
    // trailing closure's body goes here
}
```

즉, 위와 같이 함수를 호출할 때 함수의 () 뒤에 클로저를 써주면 된다는 것이다.

만약 아까 만든 정렬 함수에 후행 클로저로 사용하면 다음과 같아진다.

```swift
reversedNames = names.sorted() { $0 > $1 }
```

만약 클로저 표현식이 함수, method의 유일한 매개 변수이며 후행 클로저로 쓸 경우에는 함수, method이름 뒤에 ()를 쓰지 않아도 된다.

후행 클로저는 클로저의 길이가 많이 길 때 사용하면 좋다.

예를 들어 Array타입이 가지고 있는 map(_:) method는 하나의 클로저 표현식을 매개 변수로 받는 method이다.

클로저는 Array의 각 항목을 한 번씩 호출하고 해당 항목에 대한 매핑 값을 반환한다.

map에 전달되는 클로저에서는 매핑의 특성과 반환될 값의 타입을 지정하게 된다.

모든 항목에 대해 클로저를 적용한 뒤에 map(_ :) method는 새로운 매핑 값을 가진 새로운 Array를 반환하게 된다.

```swift
let digitNames = [
    0: "Zero", 1: "One", 2: "Two",   3: "Three", 4: "Four",
    5: "Five", 6: "Six", 7: "Seven", 8: "Eight", 9: "Nine"
]
let numbers = [16, 58, 510]
```

우리는 numbers라는 Array를 digitNames를 사용해서 숫자를 String 타입으로 바꾸고 싶다.

이럴 때 map(_ :) method를 사용하면 가능하며 매개변수에는 클로저를 넣어주면 된다.

```swift
let strings = numbers.map { (number) -> String in
    var number = number
    var output = ""
    repeat {
        output = digitNames[number % 10]! + output
        number /= 10
    } while number > 0
    return output
}
// strings is inferred to be of type [String]
// its value is ["OneSix", "FiveEight", "FiveOneZero"]
```

위의 코드처럼 만들면 Array의 모든 항목에 대해 클로저 구문을 수행하게 된다.
여기서도 클로저의 매개변수인 number의 타입을 써주지 않았는데 이것 역시 Swift가 유추할 수 있기 때문이다.

위의 코드에서 digitNames[number % 10]! 에 보면 dictionary의 Value는 옵셔널 값이기 때문에 이와 같이 강제로 추출해 준 것이다.

이처럼 후행 클로저를 사용하면 깔끔하게 코드를 완성할 수 있는 것을 볼 수 있다.

그렇다면 만약 하나의 함수에서 여러 개의 클로저를 사용하고 싶다면 어떻게 해야 할까.

첫 번째 후행 클로저의 사용할 클로저의 인수는 생략하고 그 후의 후행 클로저들에는 인수 레이블을 지정하면 된다.

예를 보도록 하자.

```swift
func loadPicture(from server: Server, completion: (Picture) -> Void, onFailure: () -> Void) {
    if let picture = download("photo.jpg", from: server) {
        completion(picture)
    } else {
        onFailure()
    }
}
```

함수 호출은 아래 코드와 같이 하면 된다.

```swift
loadPicture(from: someServer) { picture in
    someView.currentPicture = picture
} onFailure: {
    print("Couldn't download the next picture.")
}
```

loadPicture 함수를 호출하면 completion, onFailure 클로저가 사용된다.

즉, 아까 말한 첫 번째 후행 클로저에서 인수를 생략하라는 말은 completion 클로저를 사용할 때는 위의 코드와 같이 인수를 생략해도 된다는 말이다.

그 후의 onFailure 클로저는 인수를 생략하면 안되기 때문에 명시해 주었다.

위의 코드를 보면 completion클로저와 onFailure 클로저 둘 다 후행 클로저로 사용된 것을 볼 수 있다.

하지만 loadPicture 함수는 두 개의 클로저 중 조건에 따라 하나의 클로저를 호출해서 사용한다.

즉, server에서 다운로드가 성공하면 completion클로저를, 실패하면 onFailure클로저를 사용하게 되는 것이다.


# <span style="color:blue">Capturing Values</span>

클로저가 주변 코드에서 상수와 변수를 캡쳐하면 그 뒤에 상수와 변수가 접근할 수 없게 되더라도 클로저는 해당 상수 및 변수의 값을 참조하고 수정할 수 있다.

Swift에서 가장 쉽게 값을 캡쳐하는 방법은 중첩 함수를 사용하는 것이다.

중첩된 함수는 바깥 함수의 인수를 캡쳐할 수 있고, 또한 바깥 함수에 정의된 상수와 변수도 캡쳐할 수 있다.

```swift
func makeIncrementer(forIncrement amount: Int) -> () -> Int {
    var runningTotal = 0
    func incrementer() -> Int {
        runningTotal += amount
        return runningTotal
    }
    return incrementer
}
```

위의 예와 같이 중첩 함수인 incrementer()에서 외부 함수인 makeIncrementer의 매개변수인 amount와 함수 내에서 정의된 runningTotal 변수를 캡쳐하여 사용하는 것을 볼 수 있다.

실제로는 incrementer 함수에는 이러한 변수나 상수가 정의되어 있지 않지만 캡쳐하여 사용할 수 있는 것이다.

여기서 makeIncrementer의 반환 타입이 () ->인데 반환하는 값이 incrementer이므로 결국에는 incrementer의 반환 타입인 Int형을 반환하게 된다.

실제 사용은 아래와 같다.

```swift
let incrementByTen = makeIncrementer(forIncrement: 10)
incrementByTen()
// returns a value of 10
incrementByTen()
// returns a value of 20
incrementByTen()
// returns a value of 30
```

incrementer 함수를 호출할 때 마다 runningTotal의 값이 10씩 증가하는 것을 볼 수 있다.

즉, 값이 사라지지 않고 계속 유지되는 것이다.

클래스의 인스턴스 타입에 클로저를 할당하고 클로저가 클래스의 인스턴스를 참조하면 클로저와 인스턴스 갑에 강력한 참조 주기가 생성된다.

Swift는 캡쳐 목록을 사용하여 참조 주기를 중단하게 된다.

# <span style="color:blue">Closures Are Reference Types</span>

앞의 Capturing Values에서 본 incrementByTen은 상수로 선언된 값이지만 계속해서 그 안의 값들이 변하는 것을 볼 수 있었다.

그 이유는 함수와 클로저는 참조 타입이기 때문이다.

함수나 클로저를 상수나 변수에 할당하게 되면 상수나 변수에 복사되는 것이 아닌 메모리 주소만 참조하게 되고, 이를 만약 다른 상수나 변수에 incrementByTen을 할당하면 다음과 같은 일이 일어나게 된다.

```swift
let alsoIncrementByTen = incrementByTen
alsoIncrementByTen()
// returns a value of 40

incrementByTen()
// returns a value of 50
```

아까 증가된 값이  그대로 유지되는 것을 볼 수 있다.

# <span style="color:blue">Escaping Closures</span>

클로저는 함수에 대한 인수로 클로저가 전달될 때 함수를 Escape 한다고 하지만 사실은 함수가 반환된 후에 호출된다.

함수의 인자가 함수의 영역을 탈출하여 함수 밖에서 사용할 수 있는 개념은 기존에 우리가 알고 있던 변수의 scope 개념을 무시한다.

왜냐하면 함수에서 선언된 로컬 변수가 로컬 변수의 영역을 넘어 함수 밖에서도 유효하기 때문이다.

클로저를 매개 변수 중 하나로 사용하는 함수를 선언하면 매개 변수 타입 앞에 @escaping 키워드를 작성해서 클로저가 Escape 될 수 있음을 나타낼 수 있다.

클로저가 escape할 수 있는 한 가지 방법은 함수 외부에 정의된 변수에 클로저를 저장하고 이를 매개변수로 사용하는 것이다.

일반 로컬 변수(주로 Int, String 등등)가 함수 밖에서 살아있는 것은 전역 변수를 함수에 가져와서 값을 새로 주는 것과 크게 달라보이지 않는다. 하지만 클로저의 Escaping은 A 함수가 마무리된 상태에서만 B 함수가 실행 되도록 함수를 작성할 수 있다는 점에서 유용하다.

> Escaping Closure를 활용하면 함수 사이에 실행 순서를 정할 수 있다.

비동기 작업을 시작하는 많은 함수는 완료 핸들러로 클로저를 사용한다.

함수는 작업을 시작한 후 반환되지만 작업이 완료될 때 까지 클로저가 호출되지 않는다.

클로저는 Escape해야 나중에 호출할 수 있는데 예를 들면 다음과 같다.

```swift
var completionHandlers = [() -> Void]()
func someFunctionWithEscapingClosure(completionHandler: @escaping () -> Void) {
    completionHandlers.append(completionHandler)
}
```

someFunctionWithEscapingClosure(_ :)함수는 매개 변수로 클로저를 받고 완료된 작업을 외부에서 선언된 Array에 추가하는 함수이다.

이때 @escaping을 사용하지 않으면 컴파일 오류를 갖게 된다.

self를 참조하는 Escaping 클로저는 좀 더 신중하게 사용해야 한다.

Escape 클로저에서 ㄴㄷ

강한 참조를 만들게 되면 Swift의 ARC로 인해 메모리 낭비가 발생할 수 있다.

일반적으로 클로저는 변수를 사용해서 암시적으로 변수를 캡쳐하지만 self를 사용하는 경우 명시적으로 캡쳐를 해야한다.

```swift
var completionHandlers = [() -> Void]()
func someFunctionWithEscapingClosure(completionHandler: @escaping () -> Void) {
    completionHandlers.append(completionHandler)
}

func someFunctionWithNonescapingClosure(closure: () -> Void) {
    closure()
}

class SomeClass {
    var x = 10
    func doSomething() {
        someFunctionWithEscapingClosure { self.x = 100 }
        someFunctionWithNonescapingClosure { x = 200 }
    }
}

let instance = SomeClass()
instance.doSomething()
print(instance.x)
// Prints "200"

completionHandlers.first?()
print(instance.x)
// Prints "100"
```

위의 코드를 보면 someFunctionWithEscapingClosure 함수에 전달된 클로저는 명시적으로 self를 나타냈다.

반대로 someFunctionWithNonescapingClosure에 전달된 클로저는 Escape클로저가 아니기 때문에 암시적으로 self를 참조할 수 있다.

```swift
class SomeOtherClass {
    var x = 10
    func doSomething() {
        someFunctionWithEscapingClosure { [self] in x = 100 }
        someFunctionWithNonescapingClosure { x = 200 }
    }
}
```

위의 코드는 클로저의 캡쳐 목록에 포함해서 self를 캡쳐하고 암시적으로 self를 참조하는 방법이다.

self가 구조체, 열거형의 인스턴스인 경우 언제나 self에 참조할 수 있다.

하지만 Escape 클로저는 이러한 가변적인 것에는 캡쳐를 할 수 없다.

구조체와 열거형은 값 타입이기 때문에 이러한 참조가 일어날 수 없는 것이다.

```swift
struct SomeStruct {
    var x = 10
    mutating func doSomething() {
        someFunctionWithNonescapingClosure { x = 200 }  // Ok
        someFunctionWithEscapingClosure { x = 100 }     // Error
    }
}
```

즉, 위와 같이 escape 클로저를 사용하지 않은 클로저만 구조체의 인스턴스를 참조할 수 있다.

# <span style="color:blue">Autoclosures</span>

Autoclosures는 함수에 인수로 전달되는 표현식을 감싸기 위해 자동으로 생성되는 클로저이다.

매개변수를 가지지 않으며 호출될 때 그 안에 있는 표현식의 값을 반환한다.

편의를 위해 Autoclosure를 사용할 때는 명시적인 클로저 대신 정규 표현식을 작성해서 함수의 매개 변수를 감싸는 괄호를 생략할 수 있다.

Autoclosure를 수행하는 함수를 호출하는 것은 일반적이지만 이러한 함수를 구현하는 것은 일반적이지 않다.

예를 들어 assert(condition:message:file:line:)함수는 condition, message 매개 변수를 위해 Autoclosure를 사용한다.

condition 매개 변수는 디버그 빌드에서만 사용되고 message 매개 변수는 condition이 false일 경우에만 사용된다.

Autoclosure를 사용하면 클로저를 호출할 때까지 내부 코드가 실행되지 않기 때문에 사용이 지연된다.

이렇게 지연되는 것은 계산 비용이 크거나 부작용이 있는 곳에서 유용하게 쓰일 수 있는데, 이는 코드의 사용 시점을 제어할 수 있기 때문이다.

```swift
var customersInLine = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
print(customersInLine.count)
// Prints "5"

let customerProvider = { customersInLine.remove(at: 0) }
print(customersInLine.count)
// Prints "5"

print("Now serving \(customerProvider())!")
// Prints "Now serving Chris!"
print(customersInLine.count)
// Prints "4"
```

위와 같은 코드에서 customersInLineArray에 있는 항목을 customProvider에서 클로저 내부 코드로 제거하지만 실제로는 제거가 되지 않는 것을 볼 수 있다.

즉, 클로저가 실제로 호출되지 않는 이상 수행이 되지 않는 것이다.

실제로 호출을 하게 되면 클로저 내부 코드를 수행해 Array의 항목이 하나 제거되는 것을 볼 수 있다.

```swift
// customersInLine is ["Alex", "Ewa", "Barry", "Daniella"]
func serve(customer customerProvider: () -> String) {
    print("Now serving \(customerProvider())!")
}
serve(customer: { customersInLine.remove(at: 0) } )
// Prints "Now serving Alex!"
```

위의 코드에서 serve 함수는 매개 변수로 명시적으로 클로저를 받고 Array의 항목을 하나 제거하면 제거된 값을 반환받아 print로 출력하는 함수이다.

```swift
// customersInLine is ["Ewa", "Barry", "Daniella"]
func serve(customer customerProvider: @autoclosure () -> String) {
    print("Now serving \(customerProvider())!")
}
serve(customer: customersInLine.remove(at: 0))
// Prints "Now serving Ewa!"
```

위의 코드는 이전에 선언한 serve에 @autoclosure 키워드를 사용해 autoclosure를 사용한 것이다.

이렇게 하면 클로저를 호출할 때 마치 String 타입을 사용한 것 처럼 함수를 호출할 수 있다.

@autoclosure를 붙이게 되면 인수가 자동으로 클로저로 변환된다.

만약 autoclosure와 escape클로저를 함께 사용하고 싶다면 둘 다 사용할 수 있다.

```swift
// customersInLine is ["Barry", "Daniella"]
var customerProviders: [() -> String] = []
func collectCustomerProviders(_ customerProvider: @autoclosure @escaping () -> String) {
    customerProviders.append(customerProvider)
}
collectCustomerProviders(customersInLine.remove(at: 0))
collectCustomerProviders(customersInLine.remove(at: 0))

print("Collected \(customerProviders.count) closures.")
// Prints "Collected 2 closures."
for customerProvider in customerProviders {
    print("Now serving \(customerProvider())!")
}
// Prints "Now serving Barry!"
// Prints "Now serving Daniella!"
```

위와 같이 collectCustomerProviders의 매개 변수 customProvider로 전달된 클로저를 호출하는 대신 collectCustomerProviders 함수는 클로저를 customProvidersArray에 추가한다.

Array는 collectCustomProviders 밖에서 선언되었기 때문에 함수가 반환된 후 Array의 클로저가 실행될 수 있다.

즉, 매개 변수 customProvider의 값이 함수의 범위를 벗어날 수 있어야 하는 것이다.

