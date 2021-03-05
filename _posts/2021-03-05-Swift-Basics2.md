---
title: "Swift-Basic Operators"
excerpt: "Swift 공식 문서"
toc: true
toc_sticky: true
toc_label: "Swift-Basic Operators"
category:
 - iOS 공식문서
tags:
 - iOS
---

Operators(연산자)는 값을 확인, 변경 또는 결합하는 데 사용하는 특수 기호 또는 Phrase이다.

예를 들어 + 연산자나 && 연산자가 있다.

Swift는 C언어 연산자의 여러 코딩 오류를 제거하기 위해 기능을 향상시킨 연산자를 지원한다.

= 연산자는 값을 반환하지 않는데 이는 == 연산자와의 혼동에 의해 실수로 사용되지 않도록 하기 위해서다.

산술 연산자(+,-,*,/)는 값 오버플로를 감지하고 오류를 발생시키기 때문에 허용된 값보다 크거나 작은 숫자를 사용할 수 없게 도와준다.

Swift는 C에서는 찾을 수 없는 ..<, ... 와 같은 범위 연산자를 제공한다.

이번 글에서는 Swift의 일반 연산자에 대해 설명한다.

나중에 있을 Advanced Operators 단원에서는 사용자 정의 연산자를 정의하고 표준 연산자를 구현하는 방법에 대해 설명한다.

# Terminology

연산자는 **unary(단항)**, **binary(이항)**, 또는 **ternary(삼항)**이다.

## Unary

Unary 연산자는 **한 개의 대상이 있는 연산자**이다.

즉, **단항 연산자** 이다. 예) - 1

Unary prefix 연산자는 대상 앞에 바로 나타나고, unary postfix 연산자는 대상 뒤에 바로 나타난다.

## Binary

Binary 연산자는 두 개의 대상이 있는 연산자이다.

즉, **이항 연산자** 이다. 예) 2 + 3

두 대상 사이에 위치가 고정된다.

## Ternary

Ternary 연산자는 세개의 대상이 있는 연산자이다.

즉, **삼항 연산자** 이다.

Swift에는 C언어와 마찬가지로 하나의 삼항 연산자가 있다.

a ? b : c 라고 쓰이는 조건 연산자만이 유일한 삼항 연산자이다.

## Operators and Operands

연산자가 영향을 주는 값은 Operands(피연산자)이다.

1 + 2 에서 +는 연산자이고 1, 2는 피연산자이다.

## Assignment Operator

Assignment Operator는 대입 연산자로 아래와 같이 쓰인다.

```swift
let b \= 10
var a \= 5
a \= b
// a is now equal to 10
```

a 값을 b 값으로 초기화하거나 업데이트한다.

```swift
let (x, y) \= (1, 2)
// x is equal to 1, and y is equal to 2
```

만약 우변에 여러 값을 가진 튜플인 경우 해당 원소를 위의 코드와 같이 한 번에 여러 상수 또는 변수로 분해할 수 있다.

C, Objective-C의 대입 연산자와 달리 Swift의 대입 연산자는 값을 반환하지 않는다.

# Arithmetic Operators

Arithmetic Operators는 산술 연산자로 모든 숫자 유형에 대해 4가지 표준 산술 연산자를 지원한다.

**덧셈 +, 뺄셈 -, 곱셈 *, 나눗셈 /**

C언어와 Objective-C의 산술 연산자와 달리 **Swift의 산술 연산자는 값 오버 플로우를 허용하지 않는데**, 오버 플로우 연산자를 사용하면 오버 플로우가 발생했을 때의 실행을 제어할 수 있다.

추가로 덧셈 연산자는 String 자료형에서도 사용할 수 있다.

```swift
"hello" + "world"
// equals "hello world"
```

## Remainder Operator

Remainder Operator는 나머지 연산자로 a % b와 같이 사용할 수 있다.

a를 b로 나누었을 때 나머지를 결과로 반환한다.

나머지가 나오게 되는 원리는 다음과 같다.

여기서 곱해질 값은 a를 b로 나눈 몫이 된다.

> a = (b * 곱해질 값) + 나머지

즉, 만약 a = 9, b = 4라면 곱해질 값은 2, 나머지는 1이 된다. (9 = (4 * 2) + 1)

음수일 경우에도 동일하게 나머지를 구할 수 있다.

a = -9, b = 4라면 -9 = (4 * -2) + ( -1) 이 되기 때문에 나머지는 -1이 된다.

계산 시 b의 **부호는 무시되기 때문에** a % b나 a % -b의 결과는 같다.

## Unary Minus Operator

Unary Minus Operator는 숫자 앞에 붙어 바로 해당 숫자에 -1을 곱해준다고 볼 수 있다.

```swift
let three = 3
let minusThree = -three       // minusThree equals -3
let plusThree = -minusThree   // plusThree equals 3, or "minus minus three"
```

## Unary Plus Operator

Unary Plus Operator는 숫자 앞에 붙어 해당 숫자에 +1을 곱해준다고 볼 수 있다.

```swift
let minusSix = -6
let alsoMinusSix = +minusSix  // alsoMinusSix equals -6
```

# Compound Assignment Operators

C언어와 마찬가지로 Swift에서도 Compound Assignment Operators(복합 할당 연산자)를 제공한다.

복합 할당 연산자는 = 기호 앞에 사칙연산 기호와 나머지연산자 기호를 넣어 사용하게 된다.

+= 과 같은 연산자가 이에 해당한다.

```swift
var a = 1
a += 2
// a is now equal to 3
```

a += 2는 a = a + 2의 줄임말이다.

# Comparison Operators

Comparison Operators는 비교 연산자로 다음과 같이 존재한다.

==, !=, > , < , >=, ≤

Swift 연산자에는 ===, !==도 있는데 이는 두 객체 참조가 모두 동일한 객체 인스턴스를 참조하는 지를 알려준다.

다시 돌아와서 어쨌는 비교연산자는 bool값을 반환한다.

그렇기 때문에 if문과 같은 조건문에서 사용할 수 있다.

동일한 타입, 동일한 개수를 가진 튜플 형식을 비교할 수도 있는데 튜플을 비교할 땐 왼쪽에서 오른쪽으로 한 값씩 비교하게 된다.

어떠한 값이라도 바로 비교가 되면 그 결과가 비교 결과가 된다.

```swift
(1, "zebra") < (2, "apple")   // true because 1 is less than 2; "zebra" and "apple" are not compared
(3, "apple") < (3, "bird")    // true because 3 is equal to 3, and "apple" is less than "bird"
(4, "dog") == (4, "dog")      // true because 4 is equal to 4, and "dog" is equal to "dog"
("blue", -1) < ("purple", 1)        // OK, evaluates to true
("blue", false) < ("purple", true)  // Error because < can't compare Boolean values
```

즉 (1, "zebra") < (2, "apple")에서 왼쪽부터 보기 때문에 1, 2를 비교하게 되는데 여기서 2가 더 크기 때문에 바로 true가 반환된다는 것이다.

만약 동일하면 오른쪽의 원소를 가지고 비교를 하게 된다.

Bool 값은 대소 비교가 안되는데 여기서 ("blue", false) < ("purple", true)를 실행하게 되면 오류가 발생한다.

즉, 튜플의 원소들이 모두 비교 연산자를 수행할 수 있는 값이 있을 때에 튜플에 비교 연산자를 적용할 수 있다.

# Ternary Conditional Operator

Ternary Conditional Operator는 삼항 조건 연산자로 **딱 한 가지 연산자만 존재**한다.

question ? answer1 : answer2의 형태로 사용되며 question이 참이면 answer1, 거짓이면 answer2가 반환된다.

아래의 코드의 결과와 같다고 할 수 있다.

```swift
if question {
    answer1
} else {
    answer2
}
```

```swift
let contentHeight = 40
let hasHeader = true
let rowHeight = contentHeight + (hasHeader ? 50 : 20)
// rowHeight is equal to 90
```

5줄 정도 차지하는 if else 코드를 한 줄로 줄여주는 연산자이다.

중첩해서 사용할 수 도 있다.

하지만 중첩해서 사용할 경우 코드의 줄은 줄어들지만 코드의 가독성이 떨어질 수 있다.

# Nil-Coalescing Operator

Nil-Coalescing Operator는 a ?? b와 같은 연산자로 옵셔널을 분석할 때 사용한다.

옵셔널 변수 a가 있고 a ?? b가 있다면, 만약 a가 nil이면 b를 반환하고 a에 값이 있으면 a를 반환한다.

이때 a는 반드시 옵셔널 타입이어야 한다.

이를 풀어쓰면 아래와 같은 코드로 나타낼 수 있다.

```swift
a != nil ? a! : b
```

예를 들어보면 아래의 코드와 같다.

```swift
let defaultColorName = "red"
var userDefinedColorName: String?   // defaults to nil

var colorNameToUse = userDefinedColorName ?? defaultColorName
// userDefinedColorName is nil, so colorNameToUse is set to the default of "red"
```

var colorNameToUse = userDefinedColorName ?? defaultColorName에서 userDefinedColorName 값은 nil이기 때문에 defaultColorName의 값인 "red"가 colorNameToUse에 저장된다.

# Range Operators

Swift는 값의 범위를 쉽게 나타낼 수  있는 range operator를 제공한다.

범위 연산자는 점 3개(...)를 이용하여 표현한다.

## Closed Range Operator

Closed Range Operator는 a ... b와 같이 사용되는 것으로 a와 b 사이의 값을 포함하는데, 이때 a의 값이 b보다 크면 안된다.

이러한 연산자는 for-in 루프와 같이 모든 값을 사용할 때 유용하다.

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

for-in 안의 범위 연산자는 1씩 숫자가 증가하기 때문에, **정수만 사용이 가능하고 실수나 텍스트는 사용이 불가능하다.**

## Half-Open Range Operator

Half-Open Range Operator는 a ..< b와 같이 사용된다.

a와 b 사이의 값을 나타내는데 b는 포함하지 않는다.

즉 a, a+1, ... b - 1 까지만 포함하는 범위를 가지게 된다.

이러한 연산자는 배열과 같은 zero-based list를 사용할 때 유용하게 사용된다.

```swift
let names = ["Anna", "Alex", "Brian", "Jack"]
let count = names.count
for i in 0..<count {
    print("Person \(i + 1) is called \(names[i])")
}
// Person 1 is called Anna
// Person 2 is called Alex
// Person 3 is called Brian
// Person 4 is called Jack
```

## One-Sided Ranges

한 방향으로만 커지거나 작아지는 개념으로 사용 예를 보면 쉽게 이해 가능하다.

```swift
for name in names[2...] {
    print(name)
}
// Brian
// Jack

for name in names[...2] {
    print(name)
}
// Anna
// Alex
// Brian
```

위와 같이 2...은 2번째 인덱스 이후의 값들에 모두 접근하고 ...2는 2번째 인덱스까지의 값들에 모두 접근한다.

이는 아까의 half-open range operator와 함께 사용도 가능하다.

```swift
for name in names[..<2] {
    print(name)
}
// Anna
// Alex
```

One-sided ranges는 다른 곳에서도 사용할 수 있는데 반복이 어디에서 시작해야 하는 지 혹은 끝나는 지 에 대한 부분이 명확하지 않기 때문에 명시적인 종료 조건을 추가해야한다.

```swift
let range = ...5
range.contains(7)   // false
range.contains(4)   // true
range.contains(-1)  // true
```

위의 코드와 같이 값이 존재하는지도 확인할 수 있다.

# Logical Operators

Logical Operators는 논리 연산자로 Bool 타입을 반환한다.

Swift는 오로지 세 개의 논리 연산자만 제공한다.

Logical NOT (!a)

Logical AND (a && b)

Logical OR (a || b)

## Logical NOT Operator

!a 와 같이 쓰이며 true는 false로, false는 true로 바꾸어준다.

이는 prefix operator로 피연산자 바로 앞에 붙는다.

```swift
let allowedEntry = false
if !allowedEntry {
    print("ACCESS DENIED")
}
// Prints "ACCESS DENIED"
```

## Logical AND Operator

a && b와 같이 쓰이며 a, b 모두 true 일 때만 true를 반환한다.

하나라도 false 이면 false가 반환된다.

```swift
let enteredDoorCode = true
let passedRetinaScan = false
if enteredDoorCode && passedRetinaScan {
    print("Welcome!")
} else {
    print("ACCESS DENIED")
}
// Prints "ACCESS DENIED"
```

## Logical OR Operator

a || b와 같이 쓰이며, 둘 중 하나라도 true라면 true를 반환한다.

둘 다 false 일 때 false가 반환된다.

만약 a가 참이면 b는 확인하지 않고 바로 true를 반환한다.

## Combining Logical Operators

개발자는 위의 여러 논리 연산자를 조합해서 함께 사용할 수 있다.

```swift
if enteredDoorCode && passedRetinaScan || hasDoorKey || knowsOverridePassword {
    print("Welcome!")
} else {
    print("ACCESS DENIED")
}
// Prints "Welcome!"
```

여러 && , || 를 사용해서 복합 표현식을 작성했다.

이렇게 여러 개로 작성해도 논리 연산자는 두 개씩 보기 때문에 크게는 3개의 식이 합쳐진 것이라고 볼 수 있다.

enteredDoorCode && passedRetinaScan의 값은 false가 나오고 false || hasDoorKey도 false가 나오게 되는데 결국 false || knowOverridePassword를 연산하게 되면 true가 나와서 Welcome! 이 출력되게 된다.

즉 Swift는 왼쪽에 있는 하위 표현식을 먼저 연산한다는 것을 알 수 있다.

## Explicit Parentheses

Explicit Parentheses는 명시적 괄호라고 해석되며 복잡한 식을 보기 쉽게 하기 위해 사용한다.

위의 코드를 괄호를 넣어 다시 짜면 아래와 같다.

```swift
if (enteredDoorCode && passedRetinaScan) || hasDoorKey || knowsOverridePassword {
    print("Welcome!")
} else {
    print("ACCESS DENIED")
}
// Prints "Welcome!"
```

