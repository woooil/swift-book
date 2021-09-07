---
layout: default
title: 문자열과 문자
description: Strings and Characters
parent: Swift 안내서
nav_order: 3
---

# 문자열과 문자

**문자열**은 "hello, world", "albatross"와 같은 문자들의 나열을 말합니다. Swift에서 문자열은 `String` 형으로 표현합니다. `String`의 내부 원소로의 접근은 `Character` 컬렉션을 포함하여 여러 방법으로 할 수 있습니다.

Swift의 `String`과 `Character` 형은 빠를 뿐만 아니라 유니코드를 따릅니다. 문자열을 생성하고 조작하는 문법은 가볍고 읽기도 편하고, C와 비슷한 문자열 리터럴 문법을 사용합니다. 두 문자열을 연결할 때에는 `+` 연산자를 붙이기만 하면 되고, 문자열이 수정될 수 있는지의 여부는 상수나 변수 중 하나를 고름으로써 설정할 수 있습니다. 다른 Swift 자료형들과 똑같지요. 문자열 삽입을 이용하면 긴 문자열에 상수나 변수, 리터럴을 삽입할 수 있습니다. 이러한 특징들 덕분에 문자열 값을 더 쉽게 표현하고, 저장하고, 출력할 수 있습니다.

문법이 간단함에도 불구하고 Swift의 `String` 형은 빠르고 현대적으로 문자열을 구현하도록 해줍니다. 모든 문자열은 인코딩에 무관한 유니코드 문자로 구성되어 있습니다. 또한 여러 유니코드 표현 방식으로 그 문자들에 접근할 수 있습니다.

> **참고**
> 
> Swift의 `String` 형은 Foundation의 `NSString` 클래스와 연결됩니다. Foundation 역시 `NSString`으로 정의된 메서드를 노출하고자 `String`을 확장합니다. Foundation을 불러오면, 이렇게 `String`이 사용된 `NSString` 메서드에 형 변환 없이 접근할 수 있습니다.

Foundation이나 Cocoa와 함께 `String`을 사용하는 것에 관한 자세한 정보는 [`String`과 `NSString`의 연결]()을 참고하세요.

## 문자열 리터럴

미리 정의된 `String` 값을 코드에 삽입할 수 있습니다. 이러한 값을 **문자열 리터럴**이라고 부릅니다. 문자들을 나열하고 큰따옴표(`"`)로 감싸면 문자열 리터럴이 됩니다.

문자열 리터럴로 상수나 변수의 초기 값을 설정하세요.

```swift
let someString = "Some string literal value"
```

`someString` 상수가 문자열 리터럴 값으로 초기화되었기 때문에 Swift는 상수의 자료형을 `String`으로 추론합니다.

### 다행 문자열 리터럴

여러 줄로 이어진 문자열이 필요하다면 다행 문자열 리터럴을 사용하세요. 삼중 큰따옴표로 문자열을 감싸면 됩니다.

```swift
let quotation = """
그 말을 들은 호랑이는 얼른 도끼를 가져와서, 도끼로 나무를 찍으며 성큼성큼
위로 올라갔어요. 오누이는 하느님께 간절히 기도했어요.

"하느님, 저희를 살리시려거든 튼튼한 동아줄을 내려 주시고, 죽이시려거든 썩은
동아줄을 내려 주세요."
"""
```

다행 문자열 리터럴은 여는 따옴표와 닫는 따옴표 사이에 위치한 모든 줄을 값으로 받아들입니다. 문자열은 여는 따옴표(`"""`) 바로 다음 줄부터 시작해 닫는 따옴표 직전의 줄에서 끝납니다. 즉, 아래의 두 문자열 모두 개행으로 시작하지도, 끝나지도 않습니다.

```swift
let singleLineString = "These are the same."
let multilineString = """
These are the same.
"""
```

소스 코드에서 다행 문자 리터럴이 개행을 포함하고 있다면, 문자열의 값에도 개행이 그대로 포함됩니다. 가독성을 높이기 위해 개행을 사용하고는 싶지만 문자열 값에는 개행을 포함하고 싶지 않다면, 줄 끝에 백슬래시(`\`)를 적으세요.

```swift
let softWrappedQuotation = """
그 말을 들은 호랑이는 얼른 도끼를 가져와서, 도끼로 나무를 찍으며 성큼성큼 \
위로 올라갔어요. 오누이는 하느님께 간절히 기도했어요.

"하느님, 저희를 살리시려거든 튼튼한 동아줄을 내려 주시고, 죽이시려거든 썩은 \
동아줄을 내려 주세요."
"""
```

다행 문자열 리터럴 앞이나 뒤에 라인 피드를 포함하려면 첫 줄이나 마지막 줄을 비워두세요. 예를 들면 이렇게요.

```swift
let lineBreaks = """

This string starts with a line break.
It also ends with a line break.

"""
```

다행 문자열을 둘러싸고 있는 코드에 맞춰서 문자열에도 들여쓰기를 할 수 있습니다. Swift는 닫는 따옴표(`"""`) 앞에 있는 공백을 보고 이전의 모든 줄에서 무시할 공백을 결정합니다. 닫는 따옴표 앞의 공백 외에 추가적인 공백을 다른 줄 앞에 추가하면 그 공백은 **포함됩니다.**

![](../.gitbook/assets/multilineStringWhitespace.png)

위의 예시에서는, 전체 다행 문자열 리터럴이 들여쓰기 되었음에도 문자열의 처음과 마지막 줄은 공백으로 시작하지 않습니다. 중간 줄은 닫는 따옴표보다 들여쓰기가 더 많으므로 추가적인 네 개의 공백으로 시작합니다.

### 문자열 리터럴에서의 특수 문자

스트링 리터럴에는 다음과 같은 특수 문자들이 있습니다.

* 이스케이프 특수 문자 `\0` (널 문자), `\\` (백슬래시), `\t` (수평 탭), `\n` (라인 피드), `\r` (캐리지 리턴), `\"` (큰따옴표), `\'` (작은따옴표)
* 유니코드 스칼라 값. 1~8자리의 십육진수 n을 사용해 `\u{`n`}`으로 표기. (유니코드는 아래 [유니코드]()에서 다룹니다.)

아래 코드에 특수 문자를 사용하는 예시가 네 가지 나와 있습니다. `wiseWords` 상수는 이스케이프 큰따옴표 두 개를 포함하고 있습니다. `dollarSign`, `blackHearts`, `sparklingHeart` 상수는 유니코드 스칼라 형식을 보여주고 있습니다.

```swift
let wiseWords = "\"Imagination is more important than knowledge\" - Einstein"
// "Imagination is more important than knowledge" - Einstein
let dollarSign = "\u{24}"        // $,  유니코드 스칼라 U+0024
let blackHeart = "\u{2665}"      // ♥,  유니코드 스칼라 U+2665
let sparklingHeart = "\u{1F496}" // 💖, 유니코드 스칼라 U+1F496
```

다행 문자열 리터럴은 삼중 큰따옴표를 사용하므로 이스케이프 큰따옴표 대신 큰따옴표(`"`)를 바로 삽입할 수 있습니다. 다행 문자열에 문자 `"""`을 포함하려면 하나 이상의 큰따옴표를 이스케이프 문자로 대체하면 됩니다. 예를 들면 다음과 같습니다.

```swift
let threeDoubleQuotationMarks = """
Escaping the first quotation mark \"""
Escaping all three quotation marks \"\"\"
"""
```

### 확장 문자열 구분자

문자열 리터럴을 **확장 구분자** 안에 작성하면 특수 문자를 특수 효과 없이 문자 그대로 사용할 수 있습니다. 문자열은 따옴표(`"`) 안에 작성하고 전체를 샵 기호(`#`)로 감싸세요. 예를 들어 문자열 리터럴 `#"Line 1\nLine 2"#`은 두 줄을 띄워 출력하지 않고 라인 피드 이스케이프 문자(`\n`)를 그대로 출력합니다.

문자열 리터럴 내의 문자에 특수 효과를 주고 싶다면, 문자열을 둘라싸고 있는 샵 기호의 개수와 이스케이프 문자(`\`) 뒤에 오는 샵 기호의 개수를 똑같이 맞추세요. 예를 들어 `"#"Line 1\nLine 2"#`이라는 문자열에 개행을 활성화하려면 `#"Line 1\#nLine 2"#`이라고 작성하면 됩니다. 같은 원리로 `###"Line1\###nLine2"###` 또한 개행이 이루어집니다.

다행 문자열 리터럴에도 확장 구분자를 사용할 수 있습니다. 다행 문자열에 문자 `"""`를 포함하고 싶을 때 다음과 같이 확장 구분자를 사용하세요.

```swift
let threeMoreDoubleQuotationMarks = #"""
Here are three more double quotes: """
"""#
```

## 빈 문자열 초기화

문자열을 길게 만들기 전에 미리 비어 있는 `String` 값을 만들어 둘 수 있습니다. 변수에 비어 있는 문자열 리터럴을 할당하거나, 이니셜라이저 문법을 사용해 새로운 `String` 인스턴스를 초기화하면 됩니다.

```swift
var emptyString = ""                // 비어 있는 문자열 리터럴
var anotherEmptyString = String()   // 이니셜라이저 문법
// 두 문자열 모두 비어 있으며 서로 동등합니다.
```

`String` 값이 비어 있는지 확인하려면 문자열이 가진 불 `isEmpty` 프로퍼티를 검사하세요.

```swift
if emptyString.isEmpty {
    print("Nothing to see here")
}
// "Nothing to see here" 출력
```

## 문자열의 변경

특정 `String`이 수정될 수 있는지(즉, **변경될** 수 있는지)의 여부는 그 값이 변수로 할당되거나(수정이 가능한 경우) 상수로 할당되는지(수정이 불가능한 경우)에 따라 결정됩니다.

```swift
var variablstring = "Horse"
variableString += " and carriage"
// 이제 variableString "Horse and carriage"가 됩니다.

let constantString = "Highlander"
constantString += " and another highlander"
// 상수 문자열은 수정될 수 없다는 컴파일 시간 오류가 발생합니다.
```

> **참고**
> 
> 이런 방식은 Objective-C나 Cocoa에서 두 클래스(`NSString`과 `NSMutableString`) 중 하나를 골라 문자열의 변경 가능 여부를 정하는 것과 다릅니다.

## 문자열은 값형이다

Swift에서 `String` 형은 **값형**입니다. 새로운 `String` 값을 생성하면, 그 `String` 값이 함수나 메서드로 전달되거나 상수나 변수에 할당될 때, 값이 **복사**됩니다. 각각의 경우 기존의 `String` 값의 복제본이 생성됩니다. 기존 버전이 아닌 이 복제본이 전달되거나 할당되는 것입니다. 값형은 [구조체와 열거형은 값형이다]()에 설명되어 있습니다.

Swift가 기본적으로 `String`을 복사하는 까닭은, 함수나 메서드가 `String` 값을 전달할 때 그 값의 출처에 무관하게 그 `String` 값을 정확하고 온전하게 전달받도록 하기 위함입니다. 덕분에 문자열을 어딘가로 전달하더라도 직접 수정하지 않는 한 수정되는 일은 없으리라 확신할 수 있습니다.

내부적으로 Swfit 컴파일러는 문자열 처리를 최적화하여 꼭 필요한 상황에서만 실제 복사가 일어나도록 합니다. 즉, 문자열이 값형이더라도 성능은 언제나 최상으로 유지됩니다.

## 문자 다루기

`for`-`in` 반복문으로 문자열을 반복하여 `String`의 각 `Character` 값에 접근할 수 있습니다.

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

`for`-`in` 반복문은 [For-In 반복분]()을 참고하세요.

또는 독립적인 `Character` 상수나 변수를 만들 수도 있습니다. 하나의 문자로 이루어진 문자열 리터럴을 생성하고 `Character` 형이라고 명시하세요.

```swift
let exclamationMark: Character = "!"
```

`String` 이니셜라이저에 `Character` 값 배열을 인자로 전달하면 `String` 값이 만들어집니다.

```swift
let catCharacters: [Character] = ["C", "a", "t", "!", "🐱"]
let catString = String(catCharacters)
print(catString)
// "Cat!🐱" 출력
```

## 문자열과 문자 연결

덧셈 연산자(`+`)로 `String` 값들을 합치면(즉, **연결하면**) 새로운 `String` 값이 생성됩니다.

```swift
let string1 = "hello"
let string2 = " there"
var welcome = string1 + string2
// 이제 welcome은 "hello there"와 같습니다.
```

덧셈 할당 연산자(`+=`)를 사용하면 기존의 `String` 값에 또 다른 `String` 값을 덧붙일 수 있습니다.

```swift
let string1 = "hello"
let string2 = " there"
var welcome = string1 + string2
// welcome은 이제 "hello there"와 같습니다.
```

`String` 형이 가진 `append()` 메서드를 사용하면 `String` 변수에 `Character` 값을 덧붙일 수도 있습니다.

```swift
let exclamationMark: Character = "!"
welcome.append(exclamationMark)
// welcome은 이제 "hello there!"와 같습니다.
```

> **참고**
> 
> `Character` 값은 하나의 문자만 가질 수 있으므로 기존의 `Character` 변수에는 `String`이나 `Character`를 덧붙일 수 없습니다.

다행 문자열 리터럴을 사용해 더 긴 문자열을 만들 때에는 마지막 줄을 포함해 모든 줄을 개행으로 끝나게 할 수도 있습니다. 예를 들면 이렇습니다.

```swift
let badStart = """
one
two
"""
let end = """
three
"""
print(badStart + end)
// 두 줄 출력:
// one
// twothree

let goodStart = """
one
two

"""
print(goodStart + end)
// 세 줄 출력:
// one
// two
// three
```

위의 코드에서 `badStart`와 `end`를 연결하면 두 줄짜리 문자열이 만들어집니다. 원하는 결과가 아니지요. `badStart`의 마지막 줄이 개행으로 끝나지 않으므로 `end`의 첫 번째 줄과 바로 합쳐져 버립니다. 반면에 `goodStart`는 두 줄 모두 개행으로 끝나므로 `end`와 결합했을 때 바라던 대로 세 줄 짜리 결과가 나옵니다.

## 문자열 삽입

**문자열 삽입**은 상수와 변수, 리터럴, 표현식들을 문자열 리터럴과 섞어 그 값들을 포함하는 새로운 `String` 값을 만드는 방법입니다. 단행 문자열 리터럴과 다행 문자열 리터럴 모두에 문자열 삽입을 사용할 수 있습니다. 문자열 리터럴 안에 삽입하려는 각각의 값들을 괄호로 감싸고 앞에 백슬래시(`\`)를 붙이세요.

```swift
let multiplier = 3
let message = "\(multiplier) times 2.5 is \(Double(multiplier) * 2.5)"
// message는 "3 times 2.5 is 7.5"와 같습니다.
```

위의 예시에서는 `multiplier`의 값이 `\(multiplier)`의 형태로 문자열 리터럴에 삽입되었습니다. 이 표현은 문자열 삽입이 평가되어 실제 문자열로 만들어질 때 `multiplier`의 실제 값으로 교체됩니다.

`multiplier`의 값은 문자열 뒤쪽에서 더 긴 표현식의 일부로 다시 등장합니다. 이 표현식은 `Double(multiplier) * 2.5`의 값을 계산하고 그 결과인 `(7.5)`를 문자열에 삽입합니다. 이 경우에는 `\(Double(multiplier) * 2.5)`의 형태로 표현식을 문자열 리터럴에 작성합니다.

확장 문자열 구분자를 사용하면 문자열 삽입을 수행하는 문자를 그 자체로 문자열에 포함할 수 있습니다. 예를 들면 다음과 같습니다.

```swift
print(#"Write an interpolated string in Swift using \(multiplier)."#)
// "Write an interpolated string in Swift using \(multiplier)." 출력
```

확장 구분자를 사용하는 문자열에서 문자열 삽입을 사용하고 싶다면 백슬래시 뒤에 나오는 샵 기호의 개수와 문자열 앞 뒤에 나오는 샵 기호의 개수를 맞추세요. 예를 들면 이렇습니다.

```swift
print(#"6 times 7 is \#(6 * 7)."#)
// "6 times 7 is 42." 출력
```

> **참고**
> 
> 문자열 삽입이 포함된 문자열에서, 괄호 안에 작성하는 표현식은 이스케이프 문자가 아닌 백슬래시(`\`)나 캐리지 리턴, 라인 피드를 포함할 수 없습니다. 대신 다른 문자열 리터럴을 포함합니다.

## 유니코드

**유니코드**는 다양한 글자 체계에서 문자를 인코딩하고 표현하고 처리하기 위한 국제적인 표준입니다. 유니코드를 이용하면 모든 언어의 문자 대부분을 표준화된 형식으로 표현할 수 있습니다. 그런 문자들을 텍스트 파일이나 웹 페이지와 같은 외부 자료에 작성하거나 외부 자료로부터 읽어들일 수도 있습니다. 이 절에서 설명하고 있듯이, Swift의 `String`과 `Character` 형은 유니코드를 온전히 따릅니다.

### 유니코드 스칼라 값

내부적으로 Swift의 기본 `String` 형은 **유니코드 스칼라 값**으로 구현되어 있습니다. 유니코드 스칼라 값은 문자나 수정자에 대응되는 고유한 21비트 수입니다. 예를 들면 `LATIN SMALL LETTER A`(`"a"`)에는 `U+0061`가, `FRONT-FACING BABY CHICK`(`"🐥"`)에는 `U+1F425`가 대응됩니다.

모든 21비트 유니코드 스칼라 값이 문자에 할당되어 있는 것은 아닙니다. 일부 스칼라 값들은 나중을 위해 예약되어 있거나 UTF-16 인코딩에 사용됩니다. 문자에 할당된 스칼라 값들은 일반적으로 위에서의 `LATIN SMALL LETTER A`나 `FRONT-FACING BABY CHICK`처럼 이름을 가지고 있습니다.

### 확장 문자소 단위

Swift `Character` 형의 모든 인스턴스들은 하나의 **확장 문자소 단위**를 나타냅니다. 확장 문자소 단위는 결합되어 사람이 읽을 수 있는 문자 하나를 만들어내는 한 개 이상의 유니코드 스칼라들의 나열을 말합니다.

예를 들면 이렇습니다. 문자 `é`는 하나의 유니코드 스칼라 `é`(`LATIN SMALL LETTER E WITH ACUTE` 또는 `U+00E9`)로 나타낼 수 있습니다. 그러나 같은 문자를 두 스칼라의 **쌍**으로 나타낼 수도 있습니다. 표준 문자 `e`(`LATIN SMALL LETTER E` 또는 `U+0065`)와 `COMBINING ACUTE ACCENT` 스칼라(`U+0301`)를 결합하면 됩니다. `COMBINING ACUTE ACCENT` 스칼라는 앞에 위치한 스칼라에 시각적으로 작용합니다. 따라서 유니코드를 지원하는 문자 렌더링 시스템으로 렌더링하면 `e`가 `é`로 변합니다.

두 가지 경우에서 모두 문자 `é`는 확장 문자소 단위를 나타내는 하나의 Swift `Character` 값으로 표현됩니다. 첫 번째 경우는 문자소는 하나의 스칼라를 포함하고, 두 번째 경우는 문자소가 두 개의 스칼라로 이루어집니다.

```swift
let eAcute: Character = "\u{E9}"                         // é
let combinedEAcute: Character = "\u{65}\u{301}"          // e 다음에 ́
// eAcute는 é이고, combinedEAcute는 é입니다.
```

확장 문자소 단위는 여러 복잡한 문자를 하나의 `Character` 값으로 표현해주는 유연한 방법입니다. 예를 들어, 우리나라의 한글 음절은 합쳐진 하나의 스칼라로 표현할 수도, 분리된 스칼라들의 나열로 표현할 수도 있습니다. 두 표현 방식 모두 Swift에서는 하나의 `Character` 값으로 취급됩니다.

```swift
let precomposed: Character = "\u{D55C}"                  // 한
let decomposed: Character = "\u{1112}\u{1161}\u{11AB}"   // ᄒ, ᅡ, ᆫ
// precomposed는 "한", decomposed는 "한"입니다.
```

확장 문자소 단위를 사용하면 (`COMBINING ENCLOSING CIRCLE` 또는 `U+20DD`처럼) 유니코드 스칼라를 감싸는 하나의 원 문자를 만들 수도 있습니다.

```swift
let enclosedEAcute: Character = "\u{E9}\u{20DD}"
// enclosedEAcute는 é⃝와 같습니다.
```

지역 표시자 기호에 해당하는 유니코드 스칼라들이 결합하면 하나의 `Character` 값을 만들어냅니다. 예를 들면 `REGIONAL INDICATOR SYMBOL LETTER K`(`U+1F1F0`)와 `REGIONAL INDICATOR SYMBOL LETTER R`(`U+1F1F7`)의 조합이 가능합니다.

```swift
let regionalIndicatorForKR: Character = "\u{1F1F0}\u{1F1F7}"
// regionalIndicatorForKR은 🇰🇷입니다.
```

## 문자 세기

문자열에 포함된 `Character` 값들의 개수를 구하려면 문자열이 가진 `count` 프로퍼티를 사용하세요.

```swift
let unusualMenagerie = "Koala 🐨, Snail 🐌, Penguin 🐧, Dromedary 🐪"
print("unusualMenagerie has \(unusualMenagerie.count) characters")
// "unusualMenagerie has 40 characters" 출력
```

Swift가 `Character` 값에 대해 확장 문자소 단위를 사용함에 따라 문자열 연결이나 변경이 문자 개수에 항상 영향을 주지 않을 수 있습니다.

예를 들어, 네 글자 단어인 `cafe`로 새로운 문자열을 초기화한 뒤 끝에 `COMBINING ACUTE ACCENT`(`U+0301`)을 덧붙여보세요. 네 번째 글자가 `e`에서 `é`로 바뀌어도 여전히 문자의 개수는 `4`일 것입니다.

```swift
var word = "cafe"
print("the number of characters in \(word) is \(word.count)")
// "the number of characters in cafe is 4" 출력

word += "\u{301}"    // COMBINING ACUTE ACCENT, U+0301

print("the number of characters in \(word) is \(word.count)")
// "the number of characters in café is 4" 출력
```

> **참고**
> 
> 확장 문자소 단위는 여러 개의 유니코드 스칼라로 이루어질 수 있습니다. 이것은 문자를 저장하기 위해 필요한 메모리가 문자마다 (같은 문자를 표시하더라도, 여러 표현마다) 다를 수 있음을 의미합니다. 이로 인해 Swift에서 문자열 표현에 사용된 각각의 문자들은 같은 양의 메모리를 차지하지 않습니다. 문자열을 반복하면서 확장 문자소 단위의 경계를 파악하는 것 외에는 문자열에 포함된 문자의 수를 계산할 방법이 없습니다. `count` 프로퍼티는 항상 전체 문자열의 유니코드 스칼라를 반복하여 문자의 개수를 알아냅니다. 특별히 긴 문자열을 다룰 때에는 이 점을 유념하세요.
> 
> `count` 프로퍼티가 반환하는 문자의 개수가, 같은 문자들을 포함한 `NSString`의 `length` 프로퍼티의 값과 항상 같지는 않습니다. `NSString`의 길이는 문자열의 UTF-16 표현상의 16비트 코드 단위의 개수에 기반하며, 문자열의 유니코드 확장 문자소 단위의 개수와는 무관합니다.

## 문자열에의 접근과 문자열 수정

문자열에 접근하고 문자열을 수정할 때는 문자열이 가진 메서드와 프로퍼티를 사용하거나, 첨자 문법을 사용합니다.

### 문자열 인덱스

각각의 `String` 값은 연관된 **인덱스 형**인 `String.Index`를 가지고 있습니다. 이것은 문자열 내의 각각의 `Character`의 위치에 대응합니다.

상술하였듯이 문자마다 차지하는 메모리의 크기가 다릅니다. 따라서 특정 위치에 어떤 `Character`가 있는지 판단하려면 그 `String`의 처음이나 끝에서부터 유니코드 스칼라를 하나씩 반복해야 합니다. 이런 이유로 Swift 문자열은 정수 형태의 인덱스를 가질 수 없습니다.

`String`의 첫 번째 `Character`의 위치에 접근하려면 `startIndex` 프로퍼티를 사용하세요. `endIndex` 프로퍼티는 `String`의 마지막 문자 다음의 위치를 알려줍니다. 즉 `endIndex` 프로퍼티는 문자열의 첨자로서 유효한 인자가 아닙니다. 만약 `String`이 비어 있다면, `startIndex`와 `endIndex`는 서로 같을 것입니다.

`String`의 `index(before:)`와 `index(after:)` 메서드를 사용하면 주어진 인덱스의 앞과 뒤 인덱스에 접근할 수 있습니다. 주어진 인덱스로부터 멀리 떨어진 인덱스에 접근하려면 그 메서드를 여러 번 호출하지 말고 `index(_:offsetBy:)` 메서드를 사용하세요.

특정 `String` 인덱스에 위치한 `Character`에 접근할 때는 첨자 문법을 사용하세요.

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

문자열의 범위 바깥에 있는 인덱스나 그런 인덱스에 있는 `Character`로의 접근을 시도하면 런타임 오류가 발생하게 됩니다.

```swift
greeting[greeting.endIndex] // 오류
greeting.index(after: greeting.endIndex) // 오류
```

문자열 내 모든 문자의 인덱스에 접근하려면 `indices` 프로퍼티를 사용하세요.

```swift
for index in greeting.indices {
    print("\(greeting[index]) ", terminator: "")
}
// "G u t e n   T a g ! " 출력
```

> **참고**
> 
> `startIndex`와 `endIndex` 프로퍼티, `index(before:)`와 `index(after:)`, `index(_:offsetBy:)` 메서드는 `Collection` 프로토콜을 따르는 모든 자료형에서 사용할 수 있습니다. 그런 자료형에는 여기에 제시된 `String`과 컬렉션형인 `Array`, `Dictionary`, `Set` 등이 포함됩니다.

### 삽입과 제거

문자열의 특정 인덱스에 문자 하나를 삽입하려면 `insert(_:at:)` 메서드를 사용하세요. 다른 문자열의 내용을 특정 인덱스에 삽입하려면 `insert(contentsOf:at:)` 메서드를 사용하세요.

```swift
var welcome = "hello"
welcome.insert("!", at: welcome.endIndex)
// welcome은 "hello!"와 같습니다.

welcome.insert(contentsOf: " there", at: welcome.index(before: welcome.endIndex))
// welcome은 "hello there!"와 같습니다.
```

문자열의 특정 인덱스에 위치한 문자 하나를 제거하려면 `remove(at:)` 메서드를 사용하세요. 특정 범위의 부분 문자열을 제거하려면 `removeSubrange(_:)` 메서드를 사용하세요.

```swift
welcome.remove(at: welcome.index(before: welcome.endIndex))
// welcome은 "hello there"와 같습니다.

let range = welcome.index(welcome.endIndex, offsetBy: -6)..<welcome.endIndex
welcome.removeSubrange(range)
// welcome은 "hello"와 같습니다.
```

> **참고**
> 
> `insert(_:at:)`과 `insert(contentsOf:at:)`, `remove(at:)`, `removeSubrange(_:)` 메서드는 `RangeReplaceableCollection` 프로토콜을 따르는 모든 자료형에서 사용할 수 있습니다. 여기서 보였듯이 `String` 뿐만 아니라 `Array`, `Dictionary`, `Set`과 같은 컬렉션형이 여기에 포함됩니다.

## 부분 문자열

문자열에서 부분 문자열을 얻어내면 (예를 들어, 첨자나 `prefix(_:)` 등의 메서드를 사용하면) 그 결과로 새로운 문자열이 아닌 [부분 문자열(영문)](https://developer.apple.com/documentation/swift/substring)이 반환됩니다. Swift에서 부분 문자열은 문자열과 동일한 메소드를 대부분 가지고 있습니다. 부분 문자열도 문자열과 같은 방식으로 다루면 됩니다. 그러나 문자열과 달리 부분 문자열은 문자열에 대해 작업을 수행하는 짧은 시간 동안만 사용할 수 있습니다. 더 오랫동안 결과를 저장하려면 부분 문자열을 `String`의 인스턴스로 변환하세요. 예를 들면 이렇습니다.

```swift
let greeting = "Hello, world!"
let index = greeting.firstIndex(of: ",") ?? greeting.endIndex
let beginning = greeting[..<index]
// beginning은 "Hello"와 같습니다.

// 결과를 장기간 저장하기 위해 String으로 변환합니다.
let newString = String(beginning)
```

문자열처럼 부분 문자열도 자신을 이루는 문자들이 저장되어 있는 메모리의 범위가 있습니다. 문자열과 다르게 부분 문자열은 성능 최적화에 따라, 기존 문자열을 저장하는 데 사용된 메모리나 다른 부분 문자열을 저장하는 데 사용된 메모리의 일부를 재사용할 수 있습니다. (문자열도 비슷하게 최적화되지만 두 문자열이 메모리를 공유하고 있다면 둘은 같은 것으로 취급됩니다.) 이런 성능 최적화 덕분에 문자열이나 부분 문자열을 수정하기 전까지 메모리를 복사하는 데 드는 비용을 아낄 수 있습니다. 위에서 설명하였듯이 부분 문자열은 장기간 저장에 적절하지 않습니다. 부분 문자열이 기존 문자열의 저장 공간을 재사용하므로, 기존 문자열은 자신의 부분 문자열이 사용되는 동안 메모리에 통째로 저장되어 있어야 합니다.

위 예시에서 `greeting`은 문자열입니다. 즉, 문자열을 이루는 문자들이 저장된 메모리의 범위가 정해져 있습니다. `beginning`은 `greeting`의 부분 문자열이므로 `greeting`이 사용하는 메모리를 재사용합니다. 반면 `newString`은 문자열이므로 부분 문자열로부터 만들어질 때 자신만의 저장 공간을 가지게 됩니다. 아래 그림이 이 관계를 보여줍니다.

![](../.gitbook/assets/stringSubstring.png)

> **참고**
> 
> `String`과 `Substring` 모두 [StringProtocol](https://developer.apple.com/documentation/swift/stringprotocol) 프로토콜을 따릅니다. 즉, 문자열을 조작하는 함수가 `StringProtocol` 값을 받아들이도록 하면 편리할 수도 있습니다. 그런 함수를 `String`이나 `Substring` 값과 함께 호출하세요.

## 문자열 비교

Swift는 문자로 이루어진 값을 비교하는 데 다음 세 가지 방법을 제공합니다. 문자열 및 문자 동등 연산자, 접두사 동등 연산자, 접미사 동등 연산자.

### 문자열 및 문자 동등 연산자

문자열과 문자가 동등한지 여부는 [비교 연산자](basic-operators.md#undefined-4)에 기술되었듯이 동등 연산자(`==`)와 부등 연산자(`!=`)로 확인합니다. 

```swift
let quotation = "We're a lot alike, you and I."
let sameQuotation = "We're a lot alike, you and I."
if quotation == sameQuotation {
    print("These two strings are considered equal")
}
// "These two strings are considered equal" 출력
```

두 `String` 값은 (또는 두 `Character` 값은) 자신의 확장 문자소 단위들이 **정규적으로 동등**해야 같은 것으로 평가됩니다. 확장 문자소 단위들이 정규적으로 동등하다는 것은 내부적으로 다른 유니코드 스칼라로 이루어졌더라도 언어학적으로 같은 의미와 모습을 지니고 있음을 의미합니다.

예를 들어, `LATIN SMALL LETTER E WITH ACUTE`(`U+00E9`)는 `LATIN SMALL LETTER E`(`U+0065`), `COMBINING ACUTE ACCENT`(`U+0301`) 조합과 정규적으로 동등합니다. 두 확장 문자소 단위들 모두 문자 `é`를 표현하는 유효한 방법이므로 정규적으로 동등하다고 평가할 수 있습니다.

```swift
// LATIN SMALL LETTER E WITH ACUTE를 사용한 "Voulez-vous un café?"
let eAcuteQuestion = "Voulez-vous un caf\u{E9}?"

// LATIN SMALL LETTER E와 COMBINING ACUTE ACCENT를 사용한 "Voulez-vous un café?"
let combinedEAcuteQuestion = "Voulez-vous un caf\u{65}\u{301}?"

if eAcuteQuestion == combinedEAcuteQuestion {
    print("These two strings are considered equal")
}
// "These two strings are considered equal" 출력
```

반대로 영어에서 쓰는 `LATIN CAPITAL LETTER A`(`U+0041` 또는 `"A"`)는 러시아어에서 쓰는 `CYRILLIC CAPITAL LETTER A`(`U+0410` 또는 `"А"`)와 같지 **않습니다.** 시각적으로는 비슷해 보이지만, 언어학적으로 의미가 다릅니다.

```swift
let latinCapitalLetterA: Character = "\u{41}"

let cyrillicCapitalLetterA: Character = "\u{0410}"

if latinCapitalLetterA != cyrillicCapitalLetterA {
    print("These two characters aren't equivalent.")
}
// "These two characters aren't equivalent." 출력
```

> **참고**
> 
> Swift에서의 문자열과 문자 비교는 지역성을 띠지 않습니다.

### 접두사 및 접미사 동등 연산자

문자열이 특정 문자열을 접두사나 접미사로 가지는지 검사하려면 문자열의 `hasPrefix(_:)`와 `hasSuffix(_:)` 메서드를 사용하세요. 둘 다 `String` 형의 전달 인자를 하나 받아 불 값을 반환합니다.

아래 예시는 셰익스피어의 『로미오와 줄리엣』의 처음 두 막에서 각 장들의 장소를 나타낸  문자열들의 배열입니다.

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
```

`romeoAndJuliet` 배열과 `hasPrefix(_:)`를 함께 사용하여 극 중 1막의 장소들의 수를 셀 수 있습니다.

```swift
var act1SceneCount = 0
for scene in romeoAndJuliet {
    if scene.hasPrefix("Act 1 ") {
        act1SceneCount += 1
    }
}
print("There are \(act1SceneCount) scenes in Act 1")
// "There are 5 scenes in Act 1" 출력
```

마찬가지로 `hasSuffix(_:)` 메서드를 사용하면 `Capulet's mansion`과 `Friar Lawrence's cell`에서 일어나는 막의 수를 셀 수 있습니다.

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
// "6 mansion scenes; 2 cell scenes" 출력
```

> **참고**
> 
> `hasPrefix(_:)`와 `hasSuffix(_:)` 메서드는 [문자열 및 문자 동등 연산자]()에서처럼 문자열의 확장 문자소 단위의 각각의 문자에 대해 정규적 동등 비교를 수행합니다. 

## 문자열의 유니코드 표현

텍스트 파일이나 다른 저장 공간에 유니코드 문자열을 작성하면 그 문자열의 유니코드 스칼라는 유니코드에 의해 정의된 몇 가지 **인코딩 형식** 중 하나로 인코딩됩니다. 각각의 형식들은 문자열을 **코드 단위**로 알려진 작은 조각들로 인코딩합니다. 이런 형식에는 UTF-8 인코딩 형식(8비트 코드 단위로 인코딩), UTF-16 인코딩 형식(16비트 코드 단위로 인코딩), UTF-32 인코딩 형식(32비트 코드 단위로 인코딩) 등이 있습니다.

Swift에는 문자열의 유니코드 표현에 접근하는 방법이 몇 가지 있습니다. `for`-`in` 구문으로 문자열을 반복하여 각각의 `Character` 값들을 유니코드 확장 문자소 단위로 구분하여 접근할 수 있습니다. 이런 과정은 [문자 다루기]()에 나와 있습니다.

또는 다음 세 가지 유니코드 표현 방식에 따라 `String` 값에 접근해보세요.

* UTF-8 코드 단위의 컬렉션 (문자열의 `utf8` 프로퍼티 사용)
* UTF-16 코드 단위의 컬렉션 (문자열의 `utf16` 프로퍼티 사용)
* UTF-32 인코딩 형식과 동등한 21비트 유니코드 스칼라 값의 컬렉션 (문자열의 `unicodeScalars` 프로퍼티 사용)

아래 예시들에서 문자 `D`, `o`, `g`, `‼`(`DOUBLE EXCLAMATION MARK` 또는 유니코드 스칼라 `U+203C`), `🐶`(`DOG FACE` 또는 유니코드 스칼라 `U+1F436`)로 만들어진 문자열을 여러 방식으로 표현하고 있습니다.

```swift
let dogString = "Dog‼🐶"
```

### UTF-8 표현

`String`의 UTF-8 표현은 문자열의 `utf8` 프로퍼티를 반복하여 접근할 수 있습니다. 이 프로퍼티는 `String.UTF8View` 형으로, UTF-8 표현에서 각각의 바이트에 해당하는 부호 없는 8비트(`UInt8`) 값들을 컬렉션 형태로 가집니다.

![](../.gitbook/assets/UTF8.png)

```swift
for codeUnit in dogString.utf8 {
    print("\(codeUnit) ", terminator: "")
}
print("")
// "68 111 103 226 128 188 240 159 144 182 " 출력
```

위 예시에서 처음 세 십진수 `codeUnit` 값(`68`, `111`, `103`)은 각각 문자 `D`, `o`, `g`를 나타냅니다. 이들의 UTF-8 표현은 전부 자신들의 아스키 표현과 동일합니다. 다음 세 십진수 `codeUnit` 값(`226`, `128`, `188`)은 `DOUBLE EXCLAMATION MARK`를 나타내는 3바이트짜리 UTF-8 표현입니다. 마지막 네 `codeUnit` 값(`240`,`159`, `144`, `182`)는 `DOG FACE` 문자를 나타내는 4바이트짜리 UTF-8 표현입니다.

### UTF-16 표현

`String`의 `utf16` 프로퍼티를 반복하여 문자열의 UTF-16 표현에 접근할 수 있습니다. 이 프로퍼티는 `String.UTF16View` 형으로, UTF-16 표현에서 각각의 16비트 코드 단위에 해당하는 부호 없는 16비트(`UInt16`) 값들을 컬렉션 형태로 가집니다.

![](../.gitbook/assets/UTF16.png)

```swift
for codeUnit in dogString.utf16 {
    print("\(codeUnit) ", terminator: "")
}
print("")
// "68 111 103 8252 55357 56374 " 출력
```

이번에도 처음 세 십진수 `codeUnit` 값(`68`, `111`, `103`)은 각각 문자 `D`, `o`, `g`를 나타냅니다. 이들의 UTF-16 코드 단위는 UTF-8 표현에서와 같은 값을 가집니다. (유니코드 스칼라가 곧 아스키 문자를 나타내기 때문에 그렇습니다.)

네 번째 `codeUnit` 값(`8252`)는 십진수로서, `DOUBLE EXCLAMATION MARK` 문자를 나타내는 유니코드 스칼라 `U+203C`에서 십육진수 값 `203C`와 그 값이 동일합니다. 이 문자는 UTF-16에서 하나의 코드 단위로 표현할 수 있습니다.

다섯 번째와 여섯 번째 `codeUnit` 값(`55357`, `56374`)은 `DOG FACE` 문자에 대한 UTF-16 대리 쌍 표현입니다. 이 표현은 `U+D83D`(십진 값 `55357`)의 상위 대리 값과 `U+DC36`(십진 값 `56374`)의 하위 대리 값으로 구성됩니다.

### 유니코드 스칼라 표현

`String`의 유니코드 스칼라 표현은 문자열의 `unicodeScalars` 프로퍼티를 반복하여 접근할 수 있습니다. 이 프로퍼티는 `UnicodeScalarView` 형으로, `UnicodeScalar` 값들을 컬렉션 형태로 가집니다.

각각의 `UnicodeScalar`는 `value` 프로퍼티를 가지고 있습니다. 이 프로퍼티가 `UInt32` 값으로 표현되는 스칼라의 21비트 값을 반환합니다.

![](../.gitbook/assets/UnicodeScalar.png)

```swift
for scalar in dogString.unicodeScalars {
    print("\(scalar.value) ", terminator: "")
}
print("")
// "68 111 103 8252 128054 " 출력
```

처음 세 십진수 `codeUnit` 값(`68`, `111`, `103`)은 이번에도 각각 문자 `D`, `o`, `g`를 나타냅니다.

네 번째 `codeUnit` 값(`8252`)는 마찬가지로, `DOUBLE EXCLAMATION MARK` 문자를 나타내는 유니코드 스칼라 `U+203C`의 십육진 값 `203C`와 그 값이 동일합니다.

`UnicodeScalar`의 다섯 번째이자 마지막 `value` 프로퍼티인 `128054`는 `DOG FACE` 문자를 나타내는 유니코드 스칼라 `U+1F436`의 십육진 값 `1F436`과 같은 값을 가집니다. 

`UnicodeScalar`의 `value` 프로퍼티를 사용하지 않아도, 그 자체가 문자열 삽입과 같은 데에서 새로운 `String` 값을 만드는 데 사용될 수 있습니다.

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