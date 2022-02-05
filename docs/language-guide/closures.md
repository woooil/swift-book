---
layout: default
title: 클로저
description: Closures
parent: Swift 안내서
nav_order: 7
---

# 클로저

{: .no_toc }

<details markdown="block">
  <summary>
    목차
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

**클로저**는 독립적으로 기능성을 가져 코드 내에서 전달하고 사용하는 단위입니다. Swift의 클로저는 C나 Objective-C의 블록, 다른 프로그래밍 언어의 람다와 비슷합니다.

클로저는 자신이 정의된 주위에서 상수나 변수를 포획해 이에 대한 참조를 저장할 수 있습니다. 이것을 상수나 변수 **둘러싸기**라고 합니다. Swift는 포획의 메모리 관리를 전부 대신해줍니다.

> **참고**
> 
> 포획이라는 개념에 익숙하지 않아도 괜찮습니다. 아래 [값 포획](#값-포획)에서 자세히 설명합니다.

[함수](functions.md)에서 소개된 전역 함수나 중첩 함수 모두 사실은 클로저의 특수한 예시입니다. 클로저는 다음 세 가지 형식 중 하나를 취합니다:

* 전역 함수는 이름이 있고 어느 값도 포획하지 않는 클로저입니다.
* 중첩 함수는 이름이 있고 둘러싸는 함수로부터 값을 포획할 수 있는 클로저입니다.
* 클로저 표현식은 이름이 없고 주위로부터 값을 포획할 수 있는 가벼운 문법의 클로저입니다.

Swift의 클로저 표현식은 깔끔하고 명확한 스타일을 지녔으며, 최적화를 통해 일반적인 상황에서 간결하고 모호함이 없는 문법을 유지합니다. 이 최적화는 다음을 말합니다:

* 문맥에 따른 매개 변수형 및 반환형 추론
* 단일 표현식 클로저의 묵시적 반환
* 전달 인자 이름의 축약
* 후행 클로저 문법

## 클로저 표현식

[중첩 함수](functions.md#중첩-함수)에 소개된 중첩 함수는 큰 함수 내부에서 독립적인 코드 단위에 이름을 붙이고 정의하는 편리한 방법입니다. 그러나 가끔은 함수와 유사한 구조를 완전한 정의와 이름 없이 짧게 작성하는 것이 필요하기도 합니다. 특히 함수나 메서드가 전달 인자로 하나 이상의 함수를 받을 때 더 그렇습니다.

**클로저 표현식**은 간결하고 집중적인 문법으로 인라인 클로저를 작성하는 방법입니다. 클로저 표현식은 명확성이나 의도를 유지한 채 짧은 형식으로 클로저를 작성하기 위해 몇 가지 문법 최적화를 제공합니다. 아래 클로저 표현식 예시를 통해 `sorted(by:)` 메서드 하나에 최적화를 하나씩 적용해가면서, 동일한 기능을 더 간결하게 표현해봅니다.

### 정렬 메서드

Swift의 표준 라이브러리는 `sorted(by:)`라는 메서드를 제공합니다. `sorted(by:)` 메서드는 전달받은 정렬 클로저의 결과에 따라 알려진 자료형의 값 배열을 정렬합니다. 정렬이 끝나고 나면 원소들을 기존과 동일한 자료형과 크기의 새로운 배열에 정렬된 순서로 담아 반환합니다. 기존 배열은 `sorted(by:)` 메서드로 수정되지 않습니다.


아래 클로저 표현식 예시는 `String` 값들의 배열을 `sorted(by:)` 메서드를 이용하여 알파벳 역순으로 정렬합니다. 정렬할 배열의 초기 상태는 이렇습니다:

```swift
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
```

`sorted(by:)` 메서드는 한 클로저를 받습니다. 이 클로저는 배열의 원소와 같은 자료형의 인자 두 개를 받아, 두 값 중 무엇이 앞에 와야 하는지 `Bool` 값을 반환하여 알려줍니다. 정렬 클로저는 첫 번째 값이 두 번째 값보다 **앞에** 있어야 하면 `true`를, 그렇지 않으면 `false`를 반환하도록 되어 있습니다.

이 예시는 `String` 값들의 배열을 정렬하므로 정렬 클로저는 `(String, String) -> Bool`형의 함수여야 합니다.

정렬 클로저를 제공하는 방법으로 첫 번째는 해당 자료형의 일반 함수를 작성하여 `sorted(by:)` 메서드에 인자로 전달하는 것입니다.

```swift
func backward(_ s1: String, _ s2: String) -> Bool {
    return s1 > s2
}
var reveredNames = names.sorted(by: backward)
// reversedNames는 ["Ewa", "Daniella", "Chris", "Barry", "Alex"]와 같습니다.
```

첫 번째 문자열(`s1`)이 두 번째 문자열(`s2`)보다 크면 `backward(_:_:)` 함수는 `true`를 반환하여 정렬된 배열에서 `s1`이 `s2`보다 먼저 나타나야 한다고 알려줍니다. 문자열의 문자에 대해 "크다"는 것은 "알파벳순에서 뒤에 온다"는 것을 말합니다. 즉, 문자 `"B"`는 문자 `"A"`보다 "크고, 문자열 `"Tom"`은 문자열 `"Tim"`보다 큽니다. 이로써 `"Barry"`가 `"Alex"` 앞에 오는 식으로 알파벳 역순이 만들어집니다.

그러나 아직까지는 핵심적인 단일 표현식 함수(`a > b`)를 너무 길게 적고 있습니다. 이 예시에서는 클로저 표현식 문법을 사용해 정렬 클로저를 인라인으로 적는 것이 낫습니다.

### 클로저 표현식 문법

클로저 표현식 문법은 다음과 같은 일반 형식을 가집니다:

```swift
{ ((parameters)) -> (return type) in
    (statements)
}
```

클로저 표현식 문법에서 **매개 변수**는 인-아웃 매개 변수도 가능하지만, 기본 값을 가질 수는 없습니다. 가변 매개 변수는 이름을 붙여준다면 사용할 수 있습니다. 매개 변수형이나 반환형에 튜플도 사용할 수 있습니다.

아래 예시는 위의 `backward(_:_:)` 함수의 클로저 표현식 버전입니다.

```swift
reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in
    return s1 > s2
})
```

매개 변수와 반환 형의 선언이 `backward(_:_:)` 함수에서와 같습니다. 두 경우 모두 `(s1: String, s2: String) -> Bool`로 적습니다. 그러나 인라인 클로저 표현식에서 매개 변수와 반환형은 중괄호 밖이 아닌 **안에** 적게 됩니다.

클로저 몸체는 `in` 키워드로 시작합니다. 이 키워드는 클로저의 매개 변수와 반환형의 정의가 끝났고 몸체가 시작함을 나타냅니다.

클로저의 몸채가 매우 짧으므로 한 줄에 적어도 됩니다.

```swift
reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in return s1 > s2 } )
```

`sorted(by:)` 메서드를 호출하는 전체적인 상황은 같습니다. 괄호 쌍이 여전히 메서드의 전체 인자를 감싸고 있습니다. 그러나 인자가 이제는 인라인 클로저입니다.

### 문맥에 따른 자료형 추론

정렬 클로저가 메서드의 인자로서 전달되므로, Swift는 클로저의 매개 변수형과 반환형을 추론할 수 있습니다. `sorted(by:)` 메서드는 문자열 배열에 대해 호출되므로 인자는 반드시 `(String, String) -> Bool`형의 함수여야 합니다. `(String, String)`과 `Bool`형을 클로저 표현식의 정의에 명시할 필요가 없다는 의미입니다. 모든 자료형이 추론 가능하므로 반환 화살표(`->`)와 매개 변수 이름을 감싸는 괄호까지 생략할 수 있습니다.

```swift
reversedNames = names.sorted(by: { s1, s2 in return s1 > s2 } )
```

함수나 메서드에 인라인 클로저 표현식을 전달할 때라면 언제든 매개 변수형과 반환형을 추론할 수 있습니다. 함수나 메서드의 인자로 인라인 클로저를 전달할 때 굳이 완전한 형식을 갖출 필요가 없지요.

그렇지만 원한다면 물론 자료형을 명시할 수 있고, 코드의 모호함을 없애준다면 그렇게 하는 편이 더 낫습니다. `sorted(by:)` 메서드의 경우에는 정렬이 진행된다는 점에서 클로저의 목적이 명확하고, 문자열 배열을 정렬하고 있기에 클로저가 `String` 값을 다룰 것임을 안전하게 가정할 수 있습니다.

### 단일 표현식 클로저의 묵시적 반환

단일 표현식 클로저는 다음 버전에서 보이듯이 선언에서 `return` 키워드를 생략해도 그 유일한 표현식의 결과를 묵시적으로 반환합니다.

```swift
reversedNames = names.sorted(by: { s1, s2 in s1 > s2 } )
```

`sorted(by:)` 메서드의 인자의 함수형에 따라 클로저는 분명히 `Bool` 값을 반환해야 합니다. 클로저의 몸체는 `Bool` 값을 반환하는 단일 표현식(`s1 > s2`)이므로 모호함이 없어 `return` 키워드를 생략할 수 있습니다.

### 전달 인자 이름의 축약

Swift는 기본적으로 인라인 클로저의 인자 이름에 대한 축약형을 제공합니다. 클로저의 인자 값을 `$0`, `$1`, `$2`와 같은 식의 이름으로 참조할 수 있습니다.

클로저 표현식에 이 축약형 인자 이름을 사용하면 정의에서 인자 목록을 생략할 수도 있습니다. 축약된 인자들의 자료형은 예상되는 함수형으로부터 추론되며, 사용된 축약형 이름 중 가장 높은 번호가 클로저가 받는 인자의 수를 결정합니다. 클로저 몸체 자체가 클로저 표현식을 이루므로, `in` 키워드 또한 생략 가능합니다.

```swift
reversedNames = names.sorted(by: { $0 > $1 } )
```

여기서 `$0`과 `$1`은 각각 클로저의 첫 번째, 두 번째 `String` 인자를 참조합니다. `$1`이 가장 번호가 높은 축약형 인자이므로 클로저는 두 개의 인자를 받기로 판단합니다. `sorted(by:)` 함수가 두 문자열을 인자로 하는 클로저를 받으므로, `$0`과 `$1` 모두 `String` 형입니다.

### 연산자 메서드

사실 위 클로저 표현식을 **더 짧게** 줄일 수 있습니다. Swift의 `String`형은 크다 연산자(`>`)에 대한 자신만의 구현을 따로 정하고 있습니다. 문자열에서 크다 연산자는 메서드로, 두 `String`형 매개 변수를 받아 `Bool`형 값을 반환합니다. 이것은 `sorted(by:)` 메서드에 필요한 메서드형과 정확히 일치합니다. 따라서 단순히 크다 연산자를 전달하면 Swift가 이를 문자열 전용 구현으로 사용하려 함을 추론합니다.

```swift
reversedNames = names.sorted(by: >)
```

연산자 메서드에 관해서는 [연산자 메서드](advanced-operators.md#연산자-메서드)를 참고하세요.

## 후행 클로저

함수의 마지막 인자로 클로저 표현식을 전달하려 하는데 그 표현식이 길다면, **후행 클로저**를 사용하세요. 함수 호출의 괄호 다음에 후행 클로저를 작성해도 클로저는 여전히 함수의 인자로 전달됩니다. 후행 클로저 문법을 사용하여 함수를 호출할 때에는 첫 클로저에 대한 인자 레이블을 적지 않습니다. 함수는 여러 후행 클로저를 포함할 수 있습니다. 다만 처음 몇 예시에서는 하나의 후행 클로저만을 사용합니다.

```swift
func someFunctionThatTakesAClosure(closure: () -> Void) {
    // 함수 몸체
}

// 후행 클로저 없이 이 함수를 호출하면

someFunctionThatTakesAClosure(closure: {
    // 클로저 몸체
})

// 후행 클로저를 사용하여 이 함수를 호출하면

someFunctionThatTakesAClosure() {
    // 후행 클로저 몸체
}
```

위의 [클로저 표현식 문법](#클로저-표현식-문법)에서 보인 문자열 정렬 클로저는 후행 클로저로서 `sorted(by:)` 메서드의 괄호 밖에 적을 수도 있습니다.

```swift
reversedNames = names.sorted() { $0 > $1 }
```

클로저 표현식이 함수나 메서드의 유일한 인자라면, 후행 클로저를 사용하고 호출 시 함수나 메서드 이름 다음에 오는 괄호 쌍 `()`을 생략할 수 있습니다.

```swift
reversedNames = names.sorted { $0 > $1 }
```

후행 클로저는 클로저가 너무 길어 한 줄에 인라인으로 적을 수 없을 때 가장 유용합니다 .예를 들어, Swift의 `Array`형은 클로저 표현식 하나만을 인자로 받는 `map(_:)` 메서드를 가지고 있습니다. 그 클로저는 배열의 각 원소에 대해 매번 호출되어 그 원소에 대응되는 다른 값(다른 자료형도 가능)을 반환합니다. 이 대응 관계의 특성과 반환형을 클로저로 작성하여 `map(_:)`에 전달하면 됩니다.

`map(_:)` 메서드는 전달받은 클로저를 각 원소에 적용하여 얻은 값들로 이루어진 새로운 배열을 그 순서를 보존하여 반환합니다.

다음 예시에서는 `map(_:)`와 후행 클로저를 함께 사용해 `Int` 값 배열을 `String` 값 배열로 바꾸고 있습니다. 배열 `[16, 58, 510]`으로부터 새로운 배열 `["OneSix", "FiveEight", "FiveOneZero"]`를 만듭니다.

```swift
let digitNames = [
    0: "Zero", 1: "One", 2: "Two",   3: "Three", 4: "Four",
    5: "Five", 6: "Six", 7: "Seven", 8: "Eight", 9: "Nine"
]
let numbers = [16, 58, 510]
```

위 코드는 한 자리 자연수와 영어 이름 간의 대응 관계를 나타내는 딕셔너리를 생성합니다. 문자열로 바꿀 정수 배열도 정의합니다.

이제 배열의 `map(_:)` 메서드로 후행 클로저 표현식을 전달하여 `numbers` 배열로부터 `String` 값 배열을 만들 수 있습니다.

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
// strings는 [String]형으로 추론되며 그 값은
// ["OneSix", "FiveEight", "FiveOneZero"]입니다.
```

`map(_:)` 메서드는 배열의 각 원소에 대해 매번 클로저 표현식을 호출합니다. 클로저의 입력 매개 변수 `number`에 자료형을 명시할 필요는 없습니다. 대응되는 배열의 값들로부터 자료형을 추론할 수 있습니다.

이 예시에서 변수 `number`는 클로저의 `number` 매개 변수 값으로 초기화되어 클로저 몸체에서 수정됩니다. 함수와 클로저의 매개 변수는 항상 상수입니다. 클로저 표현식은 또한 반환형을 `String`으로 지정하여 대응되는 출력 배열에 저장될 자료형을 정합니다.

클로저 표현식은 호출될 때마다 `output`이라는 문자열을 만듭니다. 나머지 연산자로 `number`의 마지막 자리를 계산하고(`number % 10`) 이 숫자를 이용하여 `digitNames` 딕셔너리에서 적당한 문자열을 찾습니다. 클로저는 `0`보다 모든 정수에 대한 문자열 표현을 만드는 데 사용될 수 있습니다.

> **참고**
> 
> `digitNames` 딕셔너리의 첨자 다음에는 느낌표(`!`)가 따라옵니다. 키가 존재하지 않을 수도 있으므로 딕셔너리 첨자가 옵셔널 값을 반환하는 것입니다. 위 예시에서는 `number % 10`이 항상 `digitNames` 딕셔너리의 유효한 첨자 키임이 보장됩니다. 따라서 느낌표를 사용하여 첨자의 옵셔널 반환 값에 저장된 `String` 값을 강제 개봉합니다.

`digitNames` 딕셔너리에서 얻은 문자열은 `output` **앞에** 추가되어 수의 문자열 표현을 거꾸로 만들어갑니다. (`number % 10`은 `16`에 대해 `6`을, `58`에 대해 `8`을, `510`에 대해 `0`을 반환합니다.)

그 다음 `number` 변수는 `10`으로 나누어집니다. 값이 정수이므로 결과는 내림되어 `16`은 `1`이, `58`은 `5`가, `510`은 `51`이 됩니다.

`number`가 `0`이 될 때까지 이 과정이 반복됩니다. 클로저가 `output` 문자열을 반환하면 이를 `map(_:)` 메서드가 출력 배열에 추가합니다.

위에서 사용한 후행 클로저 문법은 `map(_:)` 메서드의 바깥 괄호로 전체 클로저를 감싸지 않고도 클로저 기능을 깔끔하게 캡슐화합니다.

함수가 클로저를 여러 개 받는다면, 첫 번째 후행 클로저에 대한 인자 레이블은 생략하고 나머지 후행 클로저들에 레이블을 붙이세요. 예를 들어, 앨범에서 사진을 불러오는 함수를 봅시다.

```swift
func loadPicture(from server: Server, completion: (Picture) -> Void, onFailure: () -> Void) {
    if let picture = download("photo.jpg", from: server) {
        completion(picture)
    } else {
        onFailure()
    }
}
```

사진을 불러오기 위해 이 함수를 호출할 때는 클로저를 두 개 제공해야 합니다. 첫 번째 클로저는 다운로드가 성공했을 때 사진을 띄우는 완료 처리자입니다. 두 번째 클로저는 사용자에게 오류를 띄우는 오류 처리자입니다.

```swift
loadPicture(from: someServer) { picture in
    someView.currentPicture = picture
} onFailure: {
    print("Couldn't download the next picture.")
}
```

여기서 `loadPicture(from:completion:onFailure:)` 함수는 네트워크 작업을 백그라운드로 보내 작업이 끝났을 때 두 완료 처리자 중 하나를 호출합니다. 함수를 이렇게 작성하면, 네트워크 실패를 처리하는 코드와 다운로드 성공 후 UI를 업데이트하는 코드를 한 클로저에 담지 않고 깔끔하게 분리할 수 있습니다.

## 갑 포획

클로저는 정의된 곳 주위에서 상수나 변수를 **포획**할 수 있습니다. 상수나 변수가 처음 정의된 영역에서 벗어나더라도 클로저 몸체 안에서는 그 값들을 참조하고 수정할 수 있습니다.

Swift에서 값을 포획할 수 있는 가장 간단한 클로저 형태는 다른 함수 몸체 내부에 작성하는 중첩 함수입니다. 중첩 함수는 감싸는 함수의 모든 인자와 그 함수에서 정의된 모든 상수와 변수를 포획할 수 있습니다.

이 예시에서 함수 `makeIncrementer`는 `incrementer`라고 하는 중첩 함수를 가지고 있습니다. 중첩된 `incrementer()` 함수는 주위에서 두 값 `runningTotal`과 `amount`를 포획합니다. 이 값을 포획한 `incrementer`는 호출될 때마다 `runningTotal`을 `amount`만큼 증가시키는 클로저로서 `makeIncrementer`에 의해 반환됩니다.

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

`makeIncrementer`의 반환형은 `() -> Int`입니다. 즉, 단순 값이 아니라 **함수**를 반환합니다. 반환되는 함수는 매개 변수 없이 호출될 때마다 `Int` 값을 반환합니다. 함수가 다른 함수를 반환하는 것에 관해서는 [반환형으로서의 함수형](functions.md#반환형으로서의-함수형)을 참고하세요.

`makeIncrementer(forIncrement:)` 함수는 `runningTotal`이라는 정수 변수를 정의하고 반환되는 증감자의 현재 실행 합계를 이 변수에 저장합니다. 변수는 처음에 `0`으로 초기화됩니다.

`makeIncrementer(forIncrement:)` 함수는 인자 레이블이 `forIncrement`이고 매개 변수 이름이 `amount`인 `Int` 매개 변수 하나를 가집니다. 인자 값은 이 매개 변수로 전달되어 반환되는 `incrementer` 함수가 호출될 때마다 `runningTotal`을 얼마씩 증가시킬지 지정합니다. `makeIncrementer` 함수는 증가시키는 작업을 실제로 수행하는 중첩 함수 `incrementer`를 정의합니다. 이 함수는 단순히 `runningTotal`에 `amount`를 더해 그 결과를 반환합니다.

중첩된 `incrementer()` 함수를 별개로 생각하면 이상해 보일 수 있습니다.

```swift
func incrementer() -> Int {
    runningTotal += amount
    return runningTotal
}
```

`incrementer()` 함수는 어떤 매개 변수도 가지고 있지 않은데 몸체 내에서 `runningTotal`과 `amount`를 참조합니다. 이 함수는 둘러싸는 함수로부터 `runningTotal`과 `amount`에 대한 참조를 포획하여 자신의 몸체 안에서 이를 사용하고 있습니다. 참조를 포획함으로써 `makeIncrementer` 호출이 끝나도 `runningTotal`과 `amount`가 사라지지 않게 되며, 다음 `incrementer` 함수를 호출했을 때에도 `runningTotal`을 사용할 수 있게 됩니다.

> **참고**
> 
> Swift는 최적화의 일환으로, 값이 클로저에 의해 변경되지 않고 클로저가 생성된 이후에도 변경되지 않는다면 값의 **복사본**을 포획하여 저장할 수 있습니다.
> 
> Swift는 또한 변수가 더 이상 필요 없을 때 이를 버리는 것까지 모든 메모리 관리를 제어합니다.

다음은 `makeIncrementer`를 사용하는 예시입니다:

```swift
let incrementByTen = makeIncrementer(forIncrement: 10)
```

이 예시에서는 `incrementByTen`이라는 상수가, 호출될 때마다 자신의 `runningTotal` 변수에 `10`을 더하는 증감자 함수를 참조합니다. 이 함수를 여러 번 호출하면 다음과 같은 결과가 나타납니다.

```swift
incrementByTen()
// 값 10 반환
incrementByTen()
// 값 20 반환
incrementByTen()
// 값 30 반환
```

다른 두 번째 증감자를 만들면 또 다른 저만의 `runningTotal` 변수에 대한 참조를 저장하게 됩니다.

```swift
let incrementBySeven = makeIncrementer(forIncrement: 7)
incrementBySeven()
// 값 7 반환
```

기존 증감자(`incrementByTen`)을 호출하면 다시 자신만의 `runningTotal` 변수를 증가시키며, `incrementBySeven`이 포획한 변수에는 영향을 주지 않습니다.

```swift
incrementByTen()
// 값 40 반환
```

> **참고**
> 
> 클로저를 클래스 인스턴스의 프로퍼티로 할당하고 인스턴스나 멤버를 참조하여 그 인스턴스를 포획하면, 클로저와 인스턴스 간의 강한 순환 참조가 형성됩니다. Swift는 **포획 목록**을 사용해 이 강한 순환 참조를 깹니다. 자세한 설명은 [클로저의 강한 순환 참조](automatic-reference-counting.md#클로저의-강한-순환-참조)를 참고하세요.

## 클로저는 참조형이다

위 예시에서 `incrementBySeven`이나 `incrementByTen`은 상수이지만 이들이 참조하는 클로저는 여전히 포획한 `runningTotal` 변수를 증가시킬 수 있습니다. 함수와 클로저가 **참조형**이기 때문입니다.

상수나 변수에 함수나 클로저를 할당할 때, 실제로는 상수나 변수가 그 함수나 클로저를 **참조하도록** 설정됩니다. 위 예시에서, `incrementByTen`이 **참조하는** 클로저를 선택하는 것은 클로저 자체의 내용이 아닌 어떤 상수를 고르는 것입니다.

따라서 다른 두 가지 상수나 변수에 하나의 클로저를 할당하면 두 상수나 변수 모두 같은 클로저를 참조합니다.

```swift
let alsoIncrementByTen = incrementByTen
alsoIncrementByTen()
// 값 50 반환

incrementByTen()
// 값 60 반환
```

위 예시에서 `alsoIncrementByTen`을 호출하는 것이나 `incrementByTen`을 호출하는 것이나 다를 바가 없음을 알 수 있습니다. 두 개 모두 같은 클로저를 참조하므로 같은 `runningTotal`을 증가시키고 반환합니다.

## 탈출 클로저

클로저가 함수에 인자로 전달되지만 함수가 반환된 후에 호출되는 경우, 클로저가 함수를 **탈출한다**고 표현합니다. 함수를 선언할 때 매개 변수인 클로저가 탈출할 수 있음을 나타내려면 매개 변수형 앞에 `@escaping`을 적으세요.

클로저가 탈출하는 방법 중 하나는 함수 바깥에서 정의된 변수에 저장되는 것입니다. 예를 들어, 비동기 연산을 사용하는 많은 함수는 완료 처리자로서 클로저 인자를 받습니다. 함수는 연산을 시작하고 나서 반환하지만 연산이 완료되기 전까지 클로저는 호출되지 않습니다. 클로저는 탈출하여 추후에 호출되어야 합니다. 예를 들어:

```swift
var completionHandlers: [() -> Void] = []
func someFunctionWithEscapingClosure(completionHandler: @escaping () -> Void) {
    completionHandlers.append(compeltionHandler)
}
```

`someFunctionWithEscapingClosure(_:)` 함수는 클로저를 인자로 받아 함수 외부에 선언된 배열에 추가합니다. 이 함수의 매개 변수에 `@escaping`을 적지 않으면 컴파일 시간 오류가 일어납니다.

탈출 클로저가 `self`를 참조하고, `self`가 클래스의 인스턴스를 참조하는 경우에는 별도의 주의가 필요합니다. 탈출 클로저에서 `self`를 포획하면 의도치 않게 강한 순환 참조가 형성되기 쉽습니다. 순환 참조에 대해서는 [자동 참조 카운팅](automatic-reference-counting.md)을 참고하세요.

일반적으로 클로저는 몸체에서 변수를 사용함으로써 이들을 묵시적으로 포획하지만, 이 경우에는 포획을 명시해야 합니다. `self`를 포획하고 싶다면 사용할 때 `self`를 명시적으로 적거나 클로저의 포획 목록에 `self`를 추가하세요. `self`를 명시함으로써 의도를 명확히 하고 순환 참조가 없어야 함을 강조할 수 있습니다. 예를 들어, 아래 코드에서는 `someFunctionWithEscapingClosure(_:)`로 전달되는 클로저가 `self`를 명시적으로 참조하고 있습니다. 반면 `someFunctionWithNonescapingClosure(_:)`로 전달되는 클로저는 비탈출 클로저로, `self`를 묵시적으로 참조합니다.

```swift
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
// "200" 출력

completionHandlers.first?()
print(instance.x)
// "100" 출력
```

이번 `doSomething()` 버전은 `self`를 클로저의 포획 목록에 포함시켜 `self`를 묵시적으로 포획, 참조하고 있습니다.

```swift
class SomeOtherClass {
    var x = 10
    func doSomething() {
        someFunctionWithEscapingClosure { [self] in x = 100 }
        someFunctionWithNonescapingClosure { x = 200 }
    }
}
```

`self`가 구조체나 열거형의 인스턴스라면 항상 `self`를 묵시적으로 참조할 수 있습니다. 그러나 그런 `self`에 대한 변경 가능한 참조는 탈출 클로저가 포획할 수 없습니다. 구조체와 열거형은 변경 가능성을 공유하지 않습니다. 자세한 설명은 [구조체와 열거형은 값형이다](classes-and-structures.md#구조체와-열거형은-값형이다)를 참고하세요.

```swift
struct SomeStruct {
    var x = 10
    mutating func doSomething() {
        someFunctinoWithNonescapingClosure { x = 200 }  // Ok
        someFunctionWithEscapingClosure { x = 100 }     // 오류
    }
}
```

`someFunctionWithEscapingClosure` 함수는 변경 가능한 메서드 내부에 있어 `self`도 변경 가능하므로 이를 호출하는 것이 오류를 발생합니다. 탈출 클로저는 구조체의 `self`에 대한 변경 가능한 참조를 포획할 수 없다는 규칙을 위반합니다.

## 자동 클로저

**자동 클로저**는 함수에 인자로 전달되는 표현식을 감싸기 위해 자동으로 만들어지는 클로저입니다. 자동 클로저는 어떤 인자도 받지 않으며, 호출되었을 때 감싸고 있는 표현식의 값을 반환합니다. 이런 문법적인 편리함 덕분에 함수의 매개 변수로 명시적인 클로저 대신 일반 표현식을 사용하면서 중괄호를 생략할 수 있습니다.

자동 클로저를 받는 함수를 **호출**하는 것은 흔하지만, 그런 류의 함수를 **구현**하는 것은 흔치 않습니다. 예를 들어, `assert(condition:message:file:line:)` 함수는 `condition`과 `message` 매개 변수로 자동 클로저를 받습니다. `condition` 매개 변수는 오직 디버그 빌드 시에만 평가되고 `message` 매개 변수는 `condition`이 `false`일 때만 평가됩니다.

자동 클로저는 호출되기 전까지 내부 코드를 실행하지 않으므로 평가를 늦출 수 있습니다. 평가를 늦추는 것은 평가할 시점을 제어할 수 있음을 의미하므로 부작용이 있거나 계산 비용이 많이 드는 코드에 특히 유용합니다. 아래 코드는 클로저가 평가를 늦추는 모습을 보여줍니다.

```swift
var customersInLine = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
print(customersInLine.count)
// "5" 출력

let customerProvider = { customersInLine.remove(at: 0) }
print(customersInLine.count)
// "5" 출력

print("Now serving \(customerProvider())!")
// "Now serving Chris!" 출력
print(customersInLine.count)
// "4" 출력
```

`customersInLine` 배열의 첫 번째 원소가 클로저의 코드에 의해서 지워지더라도, 클로저가 실제로 호출되기 전까지는 지워지지 않습니다. 클로저가 계속 호출되지 않으면 내부의 표현식도 영영 평가되지 않아 배열 원소도 지워지지 않습니다. `customerProvider`의 자료형은 `String`이 아니라 `() -> String`임에 유의하세요. 매개 변수가 없고 문자열을 반환하는 함수입니다.

클로저를 함수에 인자로 넘겨줄 때에도 평가를 지연하는 같은 결과를 얻습니다.

```swift
// customersInLine은 ["Alex", "Ewa", "Barry", Daniella"]
func serve(customer customerProvider: () -> String) {
    print("Now serving \(customerProvider())!")
}
serve(customer: { customersInLine.remove(at: 0) } )
// "Now serving Alex!" 출력
```

`serve(customer:)` 함수는 고객의 이름을 반환하는 명시적 클로저를 받습니다. 아래 `serve(customer:)` 버전은 같은 연산을 수행하지만 명시적 클로저 대신 매개 변수형에 `@autoclosure` 속성을 표시해 자동 클로저를 받습니다. 이제 이 함수를 클로저 대신 `String` 인자를 받는 것처럼 호출할 수 있습니다. `customerProvider` 매개 변수형이 `@autoclosure` 속성으로 표시되어 있으므로 인자가 자동으로 클로저로 변환됩니다.

```swift
// customersInLine은 ["Ewa", "Barry", Daniella"]
func serve(customer customerProvider: @autoclosure () -> String) {
    print("Now serving \(customerProvider())!")
}
serve(customer: customersInLine.remove(at: 0))
// "Now serving Ewa!" 출력
```

> **참고**
> 
> 자동 클로저의 남용은 코드를 이해하기 어렵게 만듭니다. 문맥과 함수 이름으로 평가가 지연됨을 명확히 나타내야 합니다.

탈출을 허용하는 자동 클로저를 만들려면 `@autoclosure`과 `@escaping` 속성을 동시에 사용하세요. `@escaping` 속성은 [탈출 클로저](#탈출-클로저)를 참고하세요.

```swift
// customersInLine은 ["Barry", "Daniella"]
var customerProviders: [() -> String] = []
func collectCustomerProviders(_ customerProvider: @autoclosure @escaping () -> String) {
    customerProviders.append(customerProvider)
}
collectCustomerProviders(customersInLine.remove(at: 0))
collectCustomerProviders(customersInLine.remove(at: 0))

print("Collected \(customerProviders.count) closures.")
// "Collected 2 closures." 출력
for customerProvider in customerProviders {
    print("Now serving \(customerProvider())!")
}
// "Now serving Barry!" 출력
// "Now serving Daniella!" 출력
```

위 코드에서 `collectCustomerProviders(_:)` 함수는 `customerProvider` 인자로 전달된 클로저를 호출하는 것 대신 `customerProviders` 배열에 클로저를 덧붙입니다. 이 변수는 함수 바깥 영역에서 선언되므로 함수가 반환한 뒤에 배열 내의 클로저가 실행될 수 있습니다. 따라서 `customerProvider` 인자의 값은 반드시 함수 영역을 탈출하도록 허락되어야 합니다.