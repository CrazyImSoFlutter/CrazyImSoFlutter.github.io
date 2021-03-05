---
title: "Swift-Strings and Characters"
excerpt: "Swift 공식 문서"
toc: true
toc_sticky: true
toc_label "Swift-Strings and Characters"
categories:
 - iOS 공식문서
tags:
 - iOS
---

String(문자열)은 "Hello World"와 같이 **Character(문자)들이 합쳐진 것이라고 볼 수 있다.**

Swift에서 문자열 및 문자 타입은 코드에서 텍스트를 유니코드 호환 방법으로 제공하고 문법적인 부분은 C와 비슷하다.

문자열의 **연결은 + 연산자를 사용하여 수행할 수 있다.**

물론 문자열도 상수와 변수로 선언하여 변경 가능성을 관리해 주어야한다.

문자열 보간을 통해 어떠한 문자열에서 다른 문자열을 불러올 수도 있다.

Swift의 문자열은 **유니코드 문자**로 구성된다고 한다.

# String Literals

개발자는 미리 정의되어 있는 String 값으로 문자열을 사용할 수 있다.

문자열을 사용할 때는 두 개의 " 안에 원하는 문자열을 써주면 된다.

## Multiline String Literals

만약 문자열을 여러 줄에 쓰고 싶으면 """를 사용해서 쓸 수 있다.

```swift
let quotation = """
The White Rabbit put on his spectacles.  "Where shall I begin,
please your Majesty?" he asked.

"Begin at the beginning," the King said gravely, "and go on
till you come to the end; then stop."
"""
```

여기서 """안의 문장은 특별한 명령어가 없으면 줄바꿈이 발생하지 않는데, 만약 줄바꿈을 사용하고 싶다면 \(백슬래시)를 사용하면 된다.

```swift
let softWrappedQuotation = """
The White Rabbit put on his spectacles.  "Where shall I begin, \
please your Majesty?" he asked.

"Begin at the beginning," the King said gravely, "and go on \
till you come to the end; then stop."
"""
```

여러 줄에 쓸 때는 아래와 같이 시작 줄과 마지막 줄을 빈 줄로 작성하는 것이 좋다.

```swift
let lineBreaks = """

This string starts with a line break.
It also ends with a line break.

"""
```

## Special Characters in String Literals

문자열은 다음과 같은 특수문자들을 포함할 수 있다.

**\0(널 문자),**

**\\(백슬래시를 문자열에서 쓰고 싶을 때),**

**\t(탭 키 한 번 누른 것과 동일한 효과), \n(줄바꿈),**

**\r(carriage return으로 커서의 위치를 줄의 맨 처음으로 보내는 기능),**

**\"(문자열에서 큰따옴표 쓰고 싶을 때),**

**\'(문자열에서 작은따옴표 쓰고 싶을 때)**

또한 유니코드를 사용하고 싶으면 \u{n}을 써주면 되고 n에는 1~8자리의 16진수를 써주면 된다.

```swift
let wiseWords = "\"Imagination is more important than knowledge\" - Einstein"
// "Imagination is more important than knowledge" - Einstein
let dollarSign = "\u{24}"        // $,  Unicode scalar U+0024
let blackHeart = "\u{2665}"      // ♥,  Unicode scalar U+2665
let sparklingHeart = "\u{1F496}" // 💖, Unicode scalar U+1F496
```

"""를 사용해서 여러 줄에 문자열을 쓸 경우에 "는 그냥 쓸 수 있다.

하지만 만약 """를 쓰고 싶다면 아래와 같이 하면 된다.

```swift
let threeDoubleQuotationMarks = """
Escaping the first quotation mark \"""
Escaping all three quotation marks \"\"\"
"""
```

## Extended String Delimiters

특수문자를 사용하는게 귀찮거나 \n과 같은 문자를 쓰고 싶다면 **# 안에 문자열을 넣어주면 된다.**

그러면 그냥 그 문자열 그대로를 사용할 수 있다.

만약 #을 쓰고 그 안에 \n과 같은 기능을 쓰고 싶다면 **#개수와 같은 수의 #을 \n에 써주면 된다**.

```swift
let text = #"Line 1 \nLine 2"# // Line1 \nLine2 출력
let text = #"Line 1 \#nLine 2"# // Line1 개행 Line2 출력
let text = ###"Line 1 \###nLine 2"### // Line1 개행 Line2 출력
```

여러 줄에 문자열을 쓸 때에도 동일하게 사용할 수 있다.

```swift
let threeMoreDoubleQuotationMarks = #"""
Here are three more double quotes: """
"""#
```

# Initializing an Empty String

빈 문자열을 만들 때 두가지 방법이 있는데 아래와 같다.

```swift
var emptyString = ""               // empty string literal
var anotherEmptyString = String()  // initializer syntax
// these two strings are both empty, and are equivalent to each other
```

또한, String 값은 **isEmpty**라는 property를 가지는데 이것은 문자열이 비어있는지를 Boolean값으로 대답한 값이라고 볼 수 있다.

```swift
if emptyString.isEmpty {
    print("Nothing to see here")
}
// Prints "Nothing to see here"
```

# String Mutability

String을 변수로 선언하면 수정할 수 있고, 상수로 선언하면 수정할 수 없다.

String의 특성이라고 하기보단 그냥 let과 var의 차이이다.

아주 당연한 말이다.

```swift
var variableString = "Horse"
variableString += " and carriage"
// variableString is now "Horse and carriage"

let constantString = "Highlander"
constantString += " and another Highlander"
// this reports a compile-time error - a constant string cannot be modified
```

# Strings Are Value Types

Swift의 String 타입은 value타입, 즉 **값 타입이다.**

만약 개발자가 새로운 String 값을 만들어 내면 그 값이 함수나 method에 사용될 때 복사가 되어 사용된다.

즉, 아예 기존의 값과는 다른 새로운 값이 만들어진다고 볼 수 있다.

물론 복사를 한 것이기 때문에 내용은 같다.

**값 타입이기 때문에 함수나 method로 전달된 문자열은 직접적으로 수정하지 않으면 수정되지 않을 것이다.**

**Swift 컴파일러는 문자열 사용을 최적화하여 실제 복사가 꼭 필요한 경우에만 이루어진다고 한다.**

**전달된 문자열이 수정이 되거나 하는 복사가 꼭 필요한 경우에만 복사를 한다는 말이다.**

# Working with Characters

String을 for-in 구문과 함께 사용하면 한 글자씩 사용할 수 있다.

```swift
for character in "Dog!🐶" {
    print(character)
}
// D
// o
// g
// !
// 🐶
```

그리고 한 글자만 사용할 것이라면 아래와 같이 선언해 줄 수도 있다.

```swift
let exclamationMark: Character = "!"
```

String 값은 Character 배열로도 만들 수 있다.

String은 Character의 집합이라 가능하다고 이해하면 된다.

```swift
let catCharacters: [Character] = ["C", "a", "t", "!", "🐱"]
let catString = String(catCharacters)
print(catString)
// Prints "Cat!🐱"
```

# Concatenating Strings and Characters

String은 + 연산자를 사용해서 새로운 String을 만들 수 있다.

```swift
let string1 = "hello"
let string2 = " there"
var welcome = string1 + string2
// welcome now equals "hello there"
```

+= 연산자도 사용할 수 있다.

```swift
var instruction = "look over"
instruction += string2
// instruction now equals "look over there"
```

Character 값을 String 값에 추가하고 싶을 때는 String 타입의 **append()** method를 사용하면 된다.

```swift
let exclamationMark: Character = "!"
welcome.append(exclamationMark)
// welcome now equals "hello there!"
```

Character는 무조건 한 글자만 존재해야 하므로 더하거나 append를 할 수 없다.

```swift
let badStart = """
one
two
"""
let end = """
three
"""
print(badStart + end)
// Prints two lines:
// one
// twothree

let goodStart = """
one
two

"""
print(goodStart + end)
// Prints three lines:
// one
// two
// three
```

여러 줄 String을 사용할 때는 마지막 줄에서는 개행이 일어나지 않기 때문에 위와 같이 해줘야 원하는 대로 문자열을 합칠 수 있다.

# String Interpolation

String Interpolation은 **문자열 보간**이라고 해석되고 이는 String에 상수, 변수, 리터럴, 연산 등의 값을 넣는 것을 말한다.

문자열 보간을 사용할 때는 \()를 문자열에 넣어주면 된다.

```swift
let multiplier = 3
let message = "\(multiplier) times 2.5 is \(Double(multiplier) * 2.5)"
// message is "3 times 2.5 is 7.5"
```

위의 코드에서 보면 multiplier라는 변수의 실제 값이 출력되는 것을 볼 수 있다.

또한 뒤에 Double(multiplier) * 2.5 를 보게 되면 연산의 결과도 문자열로 출력되는 것을 볼 수 있다.

하지만 이런한 문자열 보간도 #을 사용하면 무효화된다.

하지만 앞에 #을 붙이면 사용할 수 있다.

```swift
print(#"Write an interpolated string in Swift using \(multiplier)."#)
// Prints "Write an interpolated string in Swift using \(multiplier)."
print(#"6 times 7 is \#(6 * 7)."#)
// Prints "6 times 7 is 42."
```

# Unicode

유니코드는 텍스트를 인코딩, 표현하기 위한 국제 표준이다.

어떠한 문자와 언어도 표준화된 형식으로 표현할 수 있으며 외부 소스나 웹에서도 읽고 쓸 수 있다.

Swift의 String, Character 타입도 유니코드 형식을 지키며 사용된다.

## Unicode Scalar Values

Swift의 native String 타입은 유니코드 스칼라 값으로 구성된다.

유니코드 스칼라 값은 고유한 21비트 숫자이다.

모든 21비트 유니코드 스칼라 값이 문자에 할당되는 것은 아니고, 향후에 추가가 되거나 UTF-16 인코딩에 사용되도록 예약되어 있다.

간단한게 예를 들어보면 U+0061은 ("a")를 나타내며 U+1F425는("🐥")를 나타낸다.

이 들은 이름도 가지고 있는데 아까 예로 든 ("a")는 "LATIN SMALL LETTER A"이고 ("🐥")는 "FRONT-FACING BABY CHICK"이라고 한다.

## Extended Grapheme Clusters

Swift의 Character 타입은 하나의 Grapheme Cluster를 나타낸다.

확장된 Grapheme Cluster는 유니코드 스칼라 시퀀스로 사람이 읽을 수 있는 문자를 생성한다.

예를 들어 é라는 문자가 있다.

이는 유니 코드 스칼라로는é(LATIN SMALL LETTER E WITH ACUTE, orU+00E9) 이렇게 표현된다.

하지만 é라는문자를 (LATIN SMALL LETTER E, or U+0065), COMBINING ACUTE ACCENT (U + 0301) 로도 표현할 수 있다.

이렇게 되면 COMBINING ACUTE ACCENT는 앞의 스칼라 즉 U + 0065 에 그래픽으로 적용되어 e를é로 바꿔준다.

즉 e는 단일 스칼라를 포함하고é는 두 개의 스칼라가 포함된 것이다.

```swift
let eAcute: Character = "\u{E9}"                         // é
let combinedEAcute: Character = "\u{65}\u{301}"          // e followed by ́
// eAcute is é, combinedEAcute is é
```

한글은 어떻게 표현될까?

"한" 이라는 글자를 예로 들면 "한" 이라고 표현할 수 도 있고 "ㅎ" + "ㅏ" + "ㄴ"이라고도 표현할 수 있다.

```swift
let precomposed: Character = "\u{D55C}"                  // 한
let decomposed: Character = "\u{1112}\u{1161}\u{11AB}"   // ᄒ, ᅡ, ᆫ
// precomposed is 한, decomposed is 한
```

즉, Extended Grapheme Clusters를 사용하면 단일 스칼라에 다른 스칼라 값을 묶어서 보여줄 수 있다.

# Counting Characters

String은 **count**라는 property로 해당 문자열이 포함하는 문자의 수를 나타낼 수 있다.

```swift
let unusualMenagerie = "Koala 🐨, Snail 🐌, Penguin 🐧, Dromedary 🐪"
print("unusualMenagerie has \(unusualMenagerie.count) characters")
// Prints "unusualMenagerie has 40 characters"
```

Extended Grapheme Clusters에서 é는 두개의 스칼라로 이루어져있다고 했는데 이런 문자가 포함된 String의 count property의 값은 얼마일까?

```swift
var word = "cafe"
print("the number of characters in \(word) is \(word.count)")
// Prints "the number of characters in cafe is 4"

word += "\u{301}"    // COMBINING ACUTE ACCENT, U+0301

print("the number of characters in \(word) is \(word.count)")
// Prints "the number of characters in café is 4"
```

**영향을 주지 않는다는 것을 알 수 있다.**

이런 경우에서 볼 수 있는 것은 문자들이 다른 양의 메모리를 요구할 수 있다는 것을 의미한다.

즉 count property에 의해 반환 되는 문자 수는 NSString의 length property와는 동일하지 않을 수 있다.

NSString의 length property는 UTF-16 표현 내 16비트 코드 단위수로 문자의 수를 센다.

# Accessing and Modifying a String

String의 method와 property를 사용해서 문자열에 접근하고 수정할 수 있다.

## String Indices

Stirng 타입은 index 타입이다.

즉 String.Index로 해당 위치에 있는 Character에 접근할 수 있다.

그런데 위에서 말했듯 가각의 **문자가 다른 양의 메모리를 가질 수 있기 때문에 Swift 문자열은 정수 값으로 Index를 생성할 수 없다.**

우선 startIndex는 String의 첫 Character에 접근하는 위치이며 endIndex는 마지막 Character에 접근하는 위치이다.

만약 빈 String이라면 startIndex와 endIndex의 값은 같다.

String의 index(before;), index(after;)을 사용해서 인덱스에 접근할 수 있다.

index(_:offsetBy:) method를 이용해서 여러 문자를 한 번에 뛰어넘을 수 도 있다.

```swift
let greeting = "Guten Tag!"
greeting[greeting.startIndex]
// G
greeting[greeting.index(before: greeting.endIndex)]
// !
greeting[greeting.index(after: greeting.startIndex)]
// u
let index = greeting.index(greeting.startIndex, offsetBy: 7)
greeting[index]
// a
```

만약 String의 범위에서 벗어난 index에 접근하려고 하면 당연하게도 에러를 발생시킨다.

index가 곧 메모리 주소라고 생각을 하면 아주 당연한 이치다.

없는 메모리 주소에 값을 사용하려고 했으니까 말이다.

```swift
greeting[greeting.endIndex] // Error
greeting.index(after: greeting.endIndex) // Error
```

String의 indices property를 통해 문자열의 모든 인덱스에 접근할 수 있다.

```swift
for index in greeting.indices {
    print("\(greeting[index]) ", terminator: "")
}
// Prints "G u t e n   T a g ! "
```

Collection 프로토콜로 만들어진 모든 타입은 위에서 나온 index(before:), index(after:), index(offsetBy:)를 사용할 수 있다.

Collection 타입에는 String, Array, Dictionary, Set이 있다.

# Inserting and Removing

String의 특정 인덱스에 Character를 넣거나 삭제할 수 있다.

특정 인덱스에 하나의 문자만 넣을 때는 insert(_:at:) method를 사용하고,

특정 인덱스에 문자열을 넣을 때는 insert(contentsOf:at:)을 사용하면 된다.

```swift
var welcome = "hello"
welcome.insert("!", at: welcome.endIndex)
// welcome now equals "hello!"

welcome.insert(contentsOf: " there", at: welcome.index(before: welcome.endIndex))
// welcome now equals "hello there!"
```

삭제도 마찬가지인데 특정 인덱스의 하나의 문자만 삭제할 때는 remove(at:)을 사용하면 되고,

문자열이나 특정한 범위를 삭제하고 싶을 때는 removeSubrange(_:) method를 사용하면 된다.

```swift
welcome.remove(at: welcome.index(before: welcome.endIndex))
// welcome now equals "hello there"

let range = welcome.index(welcome.endIndex, offsetBy: -6)..<welcome.endIndex
welcome.removeSubrange(range)
// welcome now equals "hello"
```

물론 이러한 method들도 아까 말한 Collection타입에서 모두 사용할 수 있다.

# Substrings

String에서 prefix(_:)와 같은 메소드로 Substring을 가지고 오면 결과는 Substring 인스턴스가 된다.

Swift에서 Substring과 String은 거의 비슷하기 때문에 개발자는 동일하게 사용할 수 있다.

하지만 Substring은 String과 다르게 String에 대한 작업을 수행하는 아주 짧은 시간동안만 사용한다.

만약 더 길게 사용하고 싶다면 Substring을 아예 새로운 String으로 만들어줘야 한다.

```swift
let greeting = "Hello, world!"
let index = greeting.firstIndex(of: ",") ?? greeting.endIndex
let beginning = greeting[..<index]
// beginning is "Hello"

// Convert the result to a String for long-term storage.
let newString = String(beginning)
```

문자열과 마찬가지로 Substring도 메모리를 가지게 되는데 String과 Substring의 차이는 여기서 발견할 수 있다.

Substring은 기존의 String이 사용하고 있는 메모리를 재사용하거나 다른 Substring이 사용하는 메모리를 사용할 수 있다.

이는 기존의 String이나 Substring을 수정하지 않으면 메모리 복사를 하지 않기 때문에 낭비를 하지 않을 수 있다.

하지만 Substring은 기존의 String의 메모리를 재사용하는데 이러한 방식 때문에 Substring을 사용하는 동안에는 기존의 String을 메모리에 보관해야한다.

즉, Substring을 오래 지속하기엔 적합하지 않다.

![img](https://user-images.githubusercontent.com/65299607/110057840-a74ecd00-7da4-11eb-9171-6b36fa0145af.png)

만약 기존의 String이 "Hello, world!"이고 Substring으로 "Hello"를 가지고 왔다고 하자.

이 때 Substring은 기존의 String의 메모리를 재사용하게 된다.

만약 이 Substring을 새로운 String으로 생성해주게 되면 자체적으로 메모리를 가질 수 있게 된다.

# Comparing Strings

Swift는 텍스트 값을 비교하기 위해 세가지 방법을 제공한다.

**equality, prefix equality, suffix equality** 이다.

이것들을 알아보자.

## String and Character Equality

String and Character Equality는 == 연산자와 != 연산자로 사용할 수 있다.

```swift
let quotation = "We're a lot alike, you and I."
let sameQuotation = "We're a lot alike, you and I."
if quotation == sameQuotation {
    print("These two strings are considered equal")
}
// Prints "These two strings are considered equal"
```

위의 코드와 같이 extended grapheme clusters가 동일한 경우 두 문자열 혹은 문자는 동일한 것으로 간주 된다.

아까 본 é와 같이 두 개의 스칼라로 이루어진 문자인 경우에도 e와 동일한 문자로 간주한다.

```swift
// "Voulez-vous un café?" using LATIN SMALL LETTER E WITH ACUTE
let eAcuteQuestion = "Voulez-vous un caf\u{E9}?"

// "Voulez-vous un café?" using LATIN SMALL LETTER E and COMBINING ACUTE ACCENT
let combinedEAcuteQuestion = "Voulez-vous un caf\u{65}\u{301}?"

if eAcuteQuestion == combinedEAcuteQuestion {
    print("These two strings are considered equal")
}
// Prints "These two strings are considered equal"
```

영어로 사용되는 라틴 대문자는 러시아어로 사용되는 CYRILLIC CAPITAL LETTER A와는 동일하게 보지 않는다.

```swift
let latinCapitalLetterA: Character = "\u{41}"

let cyrillicCapitalLetterA: Character = "\u{0410}"

if latinCapitalLetterA != cyrillicCapitalLetterA {
    print("These two characters are not equivalent.")
}
// Prints "These two characters are not equivalent."
```

## Prefix and Suffix Equality

문자열에 특정 접두사, 접미사가 있는지 확인하려면 hasPrefix(_:), hasSuffix(_:) method를 사용하면 된다.

```swift
let romeoAndJuliet = [
    "Act 1 Scene 1: Verona, A public place",
    "Act 1 Scene 2: Capulet's mansion",
    "Act 1 Scene 3: A room in Capulet's mansion",
    "Act 1 Scene 4: A street outside Capulet's mansion",
    "Act 1 Scene 5: The Great Hall in Capulet's mansion",
    "Act 2 Scene 1: Outside Capulet's mansion",
    "Act 2 Scene 2: Capulet's orchard",
    "Act 2 Scene 3: Outside Friar Lawrence's cell",
    "Act 2 Scene 4: A street in Verona",
    "Act 2 Scene 5: Capulet's mansion",
    "Act 2 Scene 6: Friar Lawrence's cell"
]
var act1SceneCount = 0
for scene in romeoAndJuliet {
    if scene.hasPrefix("Act 1 ") {
        act1SceneCount += 1
    }
}
print("There are \(act1SceneCount) scenes in Act 1")
// Prints "There are 5 scenes in Act 1"
```

위의 코드와 같이 haPrefix(_:) method를 사용해서 해당 문자열에 해당 접두사가 있는 지 확인할 수 있다.

```swift
var mansionCount = 0
var cellCount = 0
for scene in romeoAndJuliet {
    if scene.hasSuffix("Capulet's mansion") {
        mansionCount += 1
    } else if scene.hasSuffix("Friar Lawrence's cell") {
        cellCount += 1
    }
}
print("\(mansionCount) mansion scenes; \(cellCount) cell scenes")
// Prints "6 mansion scenes; 2 cell scenes"
```

hasSuffix(_:) method도 비슷하게 사용할 수 있다.

# Unicode Representations of Strings

유니코드 문자열이 텍스트 파일이나 다른 저장소에 저장될 때 문자열의 유니코드 스칼라 값은 여러가지 Unicode-defined encoding forms에 의해 인코딩 된다.

여기엔 UTF-8(8비트로 인코딩), UTF-16(16비트로 인코딩), UTF-32(32비트로 인코딩)가 있다.

Swift는 문자열의 유니코드 표현을 하는 방법으로 여러 가지를 제공한다.

세 가지의 유니코드 표현 방식으로 String값에 접근할 수 있다.(UTF-8, UTF-16, UTF-32)

```swift
let dogString = "Dog‼🐶"
```

이 코드의 세 가지 유니코드 표현 방식을 살펴보면 다음과 같다.

## UTF-8 Representation

개발자는 String의 UTF-8 property로 UTF-8 Representation에 접근할 수 있다.

이는 String.UTF8View로 접근할 수 있고, 실제 표현을 보면 아래와 같다.

![img](https://user-images.githubusercontent.com/65299607/110058596-efbaba80-7da5-11eb-84a5-1a0e3b080b5c.png)

```swift
for codeUnit in dogString.utf8 {
    print("\(codeUnit) ", terminator: "")
}
print("")
// Prints "68 111 103 226 128 188 240 159 144 182 "
```

3자리 십진수로 문자들을 나타내는 것을 볼 수 있다.

처음의 68, 111, 103은 ASCII 표현과 동일하다.

그 다음 226, 128, 188은 DOUBLE EXCLAMATION MARK 문자의 3바이트 UTF-8표현이다.

마지막 네 개의 값인 240, 159, 144, 182는 DOG FACE 문자의 4바이트 UTF-8표현이다.

## UTF-16 Representation

개발자는 String.UTF16View로 UTF-16 Representation에 접근할 수 있고 각각의 값은 부호가 없는 16비트(UInt16)로 표현된다.

![img](https://user-images.githubusercontent.com/65299607/110058601-f0ebe780-7da5-11eb-8203-74cee3c39078.png)

```swift
for codeUnit in dogString.utf16 {
    print("\(codeUnit) ", terminator: "")
}
print("")
// Prints "68 111 103 8252 55357 56374 "
```

아까와 마찬가지로 68, 111, 103은 UTF-8과 동일하게 표현된다.

느낌표 두 개는 8252로 표현되는데 이는 Unicode scalar U+203C를 10진수로 바꾼 값이다.

마지막 값인 DOG FACE는 UTF-16값으로는 55357, 56374로 표현된다.

## Unicode Scalar Representation

유니코드를 10진수로 바꿀 수 있다.

사실 유니코드가 16진수이니 그냥 16진수를 10진수로 변환한다고 볼 수 있다.

![img](https://user-images.githubusercontent.com/65299607/110058603-f1847e00-7da5-11eb-9319-b1e3ad573d3e.png)

```swift
for scalar in dogString.unicodeScalars {
    print("\(scalar.value) ", terminator: "")
}
print("")
// Prints "68 111 103 8252 128054 "
```

실제로 이러한 스칼라 값으로 문자열을 사용할 수도 있다.

```swift
for scalar in dogString.unicodeScalars {
    print("\(scalar) ")
}
// D
// o
// g
// ‼
// 🐶
```

