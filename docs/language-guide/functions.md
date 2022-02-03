---
layout: default
title: 함수
description: Functions
parent: Swift 안내서
nav_order: 6
---

# 함수

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

**함수**는 독립적으로 특정 작업을 수행하는 코드 덩어리입니다. 함수에는 이름을 붙여 그 함수가 무슨 일을 하는지 설명합니다. 필요할 때 이 이름으로 함수를 "호출"하여 정해진 작업을 실행합니다.

Swift의 함수 문법은 통일되어 있으면서도 상당히 유연합니다. C 스타일의 매개 변수 이름이 없는 단순한 함수부터, 각 매개 변수마다 이름과 인자 레이블을 붙이는 Objective-C 스타일의 복잡한 메서드까지 모두 표현할 수 있습니다. 매개 변수에 기본 값을 지정해 함수 호출을 단순화할 수도 있고, 인-아웃 매개변수를 사용해 함수가 실행되고 나면 전달된 변수가 수정되도록 할 수도 있습니다.

Swift의 모든 함수는 매개 변수의 자료형과 반환형으로 이루어진 자료형을 가집니다. 따라서 함수를 Swift의 다른 자료형처럼 취급하여 다른 함수에 매개 변수로 전달하거나 다른 함수에서 함수를 반환할 수 있습니다. 함수 내부에 다른 함수를 작성하여 중첩 함수 영역 내에서 유용한 기능을 캡슐화하는 것도 가능합니다.

## 함수 정의 및 호출

함수를 정의할 때, 필요에 따라 하나 이상의 값에 이름과 자료형을 지정하여 함수가 그 값을 입력받도록 할 수 있습니다. 그런 값을 **매개 변수**라고 부릅니다. 함수가 종료될 때 출력으로 내보낼 값의 자료형을 지정할 수도 있습니다. 이 자료형은 **반환형**이라고 합니다.

모든 함수는 자신이 수행하는 작업을 묘사하는 **함수 이름**을 가지고 있습니다. 함수를 사용하려면, 함수의 이름으로 "호출"하고 그 함수의 매개 변수형과 일치하는 입력 값(**전달 인자**)을 함께 전달하세요. 전달 인자는 매개 변수 목록과 같은 순서로 작성해야 합니다.

아래 함수는 `greet(person:)`으로 불립니다. 사람의 이름을 입력으로 받아 그 사람에 대한 인삿말을 반환하기 때문입니다. 매개 변수 하나(`String`값인 `person`)와 그 사람에 대한 인삿말을 포함하는 반환형 `String`을 정의하면 됩니다.

```swift
func greet(person: String) -> String {
    let greeting = "Hello, " + person + "!"
    return greeting
}
```

이 모든 정보는 `func` 키워드로 시작하는 함수의 **정의**에 담깁니다. 함수의 반환형은 **반환 화살표** `->` (하이픈과 오른쪽 부등호)와 반환형의 이름을 순서대로 적어 나타냅니다.

함수의 정의는 함수가 무엇을 하고, 무엇을 받아야 하고, 무엇을 반환하는지 묘사합니다. 정의는 코드 어디서든 함수를 분명히 호출할 수 있도록 해줍니다.

```swift
print(greet(person: "Anna"))
// "Hello, Anna!" 출력
print(greet(person: "Brian"))
// "Hello, Brian" 출력
```

`greet(person:)`을 호출할 때는 `greet(person: "Anna")`처럼 `person`이라는 인자 레이블 다음에 `String` 값을 전달합니다. 함수는 `String` 값을 반환하므로, 위에서처럼 `print(_:separator:terminator:)` 함수로 `greet(person:)`을 감싸 그 문자열을 출력하고 반환 값을 확인할 수 있습니다.

> **참고**
> 
> `print(_:separator:terminator:)` 함수는 첫 번째 인자에 대한 레이블이 없으며 나머지 인자는 기본 값을 가지므로 필수가 아닙니다. 이런 변형 문법은 아래 [함수 인자 레이블 및 매개 변수 이름](#함수-인자-레이블-및-매개-변수-이름), [기본 매개 변수 이름](#기본-매개-변수-이름)에 나와 있습니다.

`greet(person:)` 함수의 몸체는 새로운 `String` 상수 `greeting`을 정의하고 이를 간단한 인삿말로 설정하면서 시작됩니다. 그리곤 `return` 키워드로 이 인삿말을 함수 밖으로 내보냅니다. `return greeting`이 적힌 줄에서 함수는 실행을 끝내고 `greeing`의 현재 값을 반환합니다.

`greet(person:)` 함수는 입력 값을 바꿔가며 여러 번 호출할 수 있습니다. 위 예시에서는 입력 값이 `"Anna"`와 `"Brian"`일 때 각각 어떻게 되는지 보여줍니다. 함수는 각 경우에 대해 맞춤 인삿말을 반환합니다.

함수의 몸체를 더 짧게 만들려면 인삿말 생성과 반환 문장을 한 줄로 합치면 됩니다.

```swift
func greetAgain(person: String) -> String {
    return "Hello again, " + person + "!"
}
print(greetAgain(person: "Anna"))
// "Hello again, Anna!" 출력
```

## 함수 매개 변수 및 반환 값

Swift의 함수 매개 변수와 반환 값은 무척이나 유연합니다. 이름 없는 매개 변수 하나를 가진 단순한 함수부터 표현적인 매개 변수 이름과 다양한 매개 변수 옵션을 가진 복잡한 함수까지 다 정의할 수 있습니다.

### 매개 변수가 없는 함수

함수에 입력 매개 변수를 반드시 정의할 필요는 없습니다. 아래가 그 예시입니다. 함수가 호출될 때마다 항상 동일한 `String` 메시지를 반환합니다.

```swift
func sayHelloWorld() -> String {
    return "hello, world"
}
print(sayHelloWorld())
// "hello, world" 출력
```

함수가 매개 변수를 받지 않더라도 정의할 때에는 함수 이름 뒤에 괄호를 꼭 적어야 합니다. 함수를 호출할 때에도 이름 뒤에 빈 괄호 쌍을 적습니다.

### 매개 변수를 가지는 함수

함수는 입력 매개 변수를 여러 개 가질 수 있습니다. 함수의 괄호 안에 쉼표로 구분하여 적으면 됩니다.

이 함수는 사람의 이름과, 그 사람이 이미 인사 받은 적 있는지 여부를 입력으로 받아 그 사람에게 알맞은 인삿말을 반환합니다.

```swift
func greet(person: String, alreadyGreeted: Bool) -> String {
    if alreadyGreeted {
        return greetAgain(person: person)
    } else {
        return greet(person: person)
    }
}
print(greet(person: "Tim", alreadyGreeted: true))
// "Hello again, Tim!" 출력
```

`greet(person:alreadyGreeted:)` 함수를 호출할 때, `person` 레이블의 `String` 인자 값과 `alreadyGreeted` 레이블의 `Bool` 인자 값을 괄호로 묶어 함께 전달합니다. 이 함수는 이전의 `greet(person:)` 함수와는 다른 것임에 주의하세요. 둘 다 이름이 `greet`으로 시작하지만, `greet(person:alreadyGreeted:)`는 인자를 두 개 받고 `greet(person:)`은 인자를 하나만 받습니다.

### 반환 값이 없는 함수

함수에 반환형이 필수인 것은 아닙니다. 이번 버전의 `greet(person:)` 함수는 `String` 값을 반환하지 않고 바로 출력합니다.

```swift
func greet(person: String) {
    print("Hello, \(person)!")
}
greet(person: "Dave")
// "Hello, Dave!" 출력
```

함수가 값을 반환할 필요가 없으므로 반환 화살표(`->`)나 반환형도 정의에 없습니다.

> **참고**
> 엄밀히 말해 이 `greet(person:)` 함수도 값을 **반환합니다**. 반환형이 정의되지 않은 함수는 `Void`형의 특수한 값을 반환합니다. 여기서 특수한 값이란, `()`으로 나타내는 빈 튜플을 말합니다.

함수를 호출할 때 반환값은 무시해도 됩니다.

```swift
func printAndCount(string: String) -> Int {
    print(string)
    return string.count
}
func printWithoutCounting(string: String) {
    let _ = printAndCount(string: string)
}
printAndCount(string: "hello, world")
// "hello, world"을 출력하고 값 12를 반환
printWithoutCounting(string: "hello, world")
// "hello, world"을 출력하고 값은 반환하지 않음
```

첫 번째 함수인 `printAndCount(string:)`은 문자열을 출력하고 문자열이 가진 문자의 개수를 `Int`로 반환합니다. 두 번째 함수인 `printWithoutCounting(string:)`은 첫 번째 함수를 호출하고 그 반환 값을 무시합니다. 두 번째 함수가 호출되면 첫 번째 함수에 의해 메시지는 출력되지만 반환 값은 사용되지 않습니다.

> **참고**
> 반환 값은 무시할 수 있지만, 반환 값을 가진 함수는 항상 값을 반환해야 합니다. 그런 함수가 값을 반환하지 않고 중간에 제어 흐름을 빠져나오려 한다면 컴파일 시간 오류가 발생합니다.


### 여러 반환 값을 가지는 함수

반환형으로 튜플형을 사용하면 함수가 여러 값을 하나의 혼합된 값으로 묶어 반환하도록 할 수 있습니다.

아래 예시에서는 `Int` 값 배열에서 가장 작은 수와 가장 큰 수를 찾는 함수 `minMax(array:)`를 정의하고 있습니다.

```swift
func minMax(array: [Int]) -> (min: Int, max: Int) {
    var currentMin = array[0]
    var currentMax = array[0]
    for value in array[1..<array.count] {
        if value < currentMin {
            currentMin = value
        } else if value > currentMax {
            currentMax = value
        }
    }
    return (currentMin, currentMax)
}
```

`minMax(array:)` 함수는 두 개의 `Int` 값으로 이루어진 튜플을 반환합니다. 이 값들은 각각 `min`과 `max`로 레이블되어 있으므로, 함수의 반환 값을 찾을 때 이름을 사용하면 됩니다.

`minMax(array:)`의 몸체는 두 작업 변수 `currentMin`과 `currentMax`를 배열의 첫 정수 값으로 설정하며 시작합니다. 그리곤 배열의 남아 있는 값들을 반복하며 그 값이 `currentMin`보다 작거나 `currentMax`보다 큰지 매번 확인합니다. 마지막에 전체적인 최솟값과 최댓값을 두 `Int` 값의 튜플로 반환합니다.

튜플의 원소 값들은 함수의 반환형의 일부로 지정됩니다. 따라서 점 표기법으로 찾아진 최솟값과 최댓값을 얻을 수 있습니다.

```swift
let bounds = minMax(array: [8, -6, 2, 109, 3, 71])
print("min is \(bounds.min) and max is \(bounds.max)")
// "min is -6 and max is 109" 출력
```

함수가 반환하는 시점에 튜플의 원소들은 이름을 갖지 않아도 됩니다. 이름은 함수의 반환형의 일부로 이미 지정되어 있습니다.


## 옵셔널 튜플 반환형

만약 함수가 반환하는 튜플형 전체가 아무 값도 가지지 "않을" 가능성이 있다면, **옵셔널** 튜플 반환형을 사용해 전체 튜플이 `nil`일 수도 있음을 반영하세요. `(Int, Int)?`, `(String, Int, Bool)?`처럼 튜플형의 닫는 괄호 뒤에 물음표를 붙이면 됩니다.

> **참고**
> 
> `(Int, Int)?`와 같은 옵셔널 튜플형은 `(Int?, Int?)`처럼 옵셔널형을 포함하는 튜플과 다릅니다. 옵셔널 튜플형의 경우, 튜플 내부의 각각의 값이 아니라 튜플 전체가 옵셔널입니다.

위의 `minMax(array:)` 함수는 두 `Int` 값을 포함하는 튜플을 반환합니다. 그러나 전달받는 배열에 대한 안정성 검사는 전혀 하지 않습니다. 만약 `array` 인자가 빈 배열을 가지고 있다면 위에서 정의된 `minMax(array:)` 함수는 `array[0]`에 접근하려 할 때 런타임 오류를 발생시킬 것입니다.

빈 배열을 안전하게 다루기 위해 `minMax(array:)` 함수에 옵셔널 튜플 반환형을 적용해 배열이 비어 있을 때 `nil` 값을 반환하도록 합니다.

```swift
func minMax(array: [Int]) -> (min: Int, max: Int)? {
    if array.isEmpty { return nil }
    var currentMin = array[0]
    var currentMax = array[0]
    for value in array[1..<array.count] {
        if value < currentMin {
            currentMin = value
        } else if value > currentMax {
            currentMax = value
        }
    }
    return (currentMin, currentMax)
}
```

이 버전의 `minMax(array:)` 함수가 실제 튜플 값을 반환하는지, `nil`을 반환하는지 검사할 때는 옵셔널 연결을 사용합니다.

```swift
if let bounds = minMax(array: [8, -6, 2, 109, 3, 71]) {
    print("min is \(bounds.min) and max is \(bounds.max)")
}
// "min is -6 and max is 109" 출력
```

### 함수의 묵시적 반환

함수의 전체 몸통이 표현식 하나라면 함수는 그 표현식을 묵시적으로 반환합니다. 예를 들어 아래 두 함수는 같은 동작을 수행합니다.

```swift
func greeting(for person: String) -> String {
    "Hello, " + person + "!"
}
print(greeting(for: "Dave"))
// "Hello, Dave!" 출력

func anotherGreeting(for person: String) -> String {
    return "Hello, " + person + "!"
}
print(anotherGreeting(for: "Dave"))
// "Hello, Dave!" 출력
```

`greeting(for:)` 함수의 전체 정의가 반환하려는 인삿말 자체입니다. 따라서 이렇게 보다 짧은 형식을 사용할 수 있습니다. `anotherGreeting(for:)`는 같은 인삿말을 `return` 키워드를 사용하여 반환하고 있습니다. `return` 줄 하나만 작성하는 코드는 항상 `return`을 생략해도 됩니다.

[축약식 게터 선언](properties.md#축약식-게터-선언)에서 설명하듯이, 프로퍼티 게터도 묵시적 반환을 사용할 수 있습니다.

> **참고**
> 
> 묵시적 반환 값으로 사용하는 코드는 반드시 어떤 값을 반환해야 합니다. 예를 들어 `print(13)`을 묵시적 반환 값으로 사용할 수는 없습니다. 그러나 `fatalError("Oh no!")`처럼 결코 반환할 일이 없는 함수는 묵시적 반환 값으로 사용할 수 있습니다. Swift가 묵시적 반환이 일어나지 않음을 알고 있기 때문입니다.

## 함수 인자 레이블 및 매개 변수 이름

함수의 각 매개 변수는 **전달 인자 레이블**과 **매개 변수 이름**을 모두 갖습니다. 인자 레이블은 함수를 호출할 때 각 인자 앞에 붙어 사용됩니다. 매개 변수 이름은 함수를 구현할 때 사용됩니다. 기본적으로 매개 변수는 매개 변수 이름을 인자 레이블로 사용합니다.

```swift
func someFunction(firstParameterName: Int, secondParameterName: Int) {
    // 함수 몸체에서 firstParameterName과 secondParameterName은
    // 각각 첫 번째와 두 번째 매개 변수에 대응하는 인자 값을 참조합니다.
}
someFunction(firstParameterName: 1, secondParameterName: 2)
```

매개 변수 이름은 겹쳐선 안 됩니다. 여러 매개 변수가 같은 인자 레이블을 가지는 것은 가능하지만, 고유한 인자 레이블을 사용하는 것이 가독성에 도움이 됩니다.

### 인자 레이블 지정

인자 레이블은 매개 변수 이름 앞에 공백으로 구분하여 적습니다.

```swift
func someFunction(argumentLabel parameterName: Int) {
    // 함수 몸체에서 parameterName은 자신에 대응하는 인자를 참조합니다.
}
```

이번 `greet(person:)` 함수는 사람의 이름과 고향을 받아 인삿말을 반환합니다.

```swift
func greet(person: String, from hometown: String) -> String {
    return "Hello \(person)! Glad you could visit from \(hometown)."
}
print(greet(person: "Bill", from: "Cupertino"))
// "Hello Bill! Glad you could visit from Cupertino." 출력
```

인자 레이블을 사용하면 함수를 더 표현적이고 실제 문장과 유사한 방식으로 호출할 수 있습니다. 그럼에도 함수 몸체는 여전히 가독성과 명확성을 유지합니다.

### 인자 레이블 생략

매개 변수에 대한 인자 레이블이 필요 없다면 명시적인 인자 레이블 대신 밑줄(`_`)을 사용하세요.

```swift
func someFunction(_ fisrtParameterName: Int, secondParameterName: Int) {
    // 함수 몸체에서 firstParameterName과 secondParameterName은
    // 각각 첫 번째와 두 번째 매개 변수에 대응하는 인자 값을 참조합니다.
}
someFunction(1, secondParameterName: 2)
```

매개 변수가 인자 레이블을 가지고 있다면, 함수를 호출할 때 그 레이블을 **반드시** 적어야 합니다.

### 기본 매개 변수 값

매개 변수에 자료형과 함께 값을 할당하면 매개 변수가 가지는 **기본 값**을 정의할 수 있습니다. 기본 값이 정의되면 함수를 호출할 때 그 매개 변수를 생략할 수 있습니다.

```swift
func someFunction(parameterWithoutDefault: Int, parameterWithDefault: Int = 12) {
    // 이 함수를 호출할 때 두 번째 인자를 생략하면
    // 함수 내부에서 parameterWithDefault는 12의 값을 가집니다.
}
someFunction(parameterWithoutDefault: 3, parameterWithDefault: 6) // parameterWithDefault는 6
someFunction(parameterWithoutDefault: 4) // parameterWithDefault는 12
```

매개 변수 목록에서, 기본 값이 있는 매개 변수보다 기본 값이 없는 매개 변수를 앞에 놓으세요. 기본 값이 없는 매개 변수는 대개 더 중요한 의미를 가집니다. 그런 변수를 앞에 적음으로써 어떤 기본 매개 변수가 생략되어도 같은 함수가 호출되었음을 더 쉽게 파악할 수 있습니다.

### 가변 매개 변수
**가변 매개 변수**는 특정 자료형의 값을 하나도 안 받을 수도, 여러 개 받을 수도 있습니다. 함수를 호출할 때마다 매개 변수로 전달하는 입력 값의 개수가 다르다면 가변 매개 변수를 사용하세요. 매개 변수의 자료형 다음에 마침표 세 개(`...`)를 붙여 가변 매개 변수임을 나타냅니다.

가변 매개 변수로 전달되는 값들은 적당한 자료형의 배열로 함수 내에서 사용합니다. 예를 들어, 이름이 `numbers`이고 자료형이 `Double...`인 가변 매개 변수는 함수 몸체 안에서 `[Double]`형의 상수 배열 `numbers`로 사용할 수 있습니다.

아래 예시는 임의의 개수의 수들에 대한 **산술 평균**(일반적으로 **평균**)을 계산합니다.

```swift
func arithmeticMean(_ numbers: Double...) -> Double {
    var total: Double = 0
    for number in numbers {
        total += number
    }
    return total / Double(numbers.count)
}
arithmeticMean(1, 2, 3, 4, 5)
// 위의 다섯 수에 대한 산술 평균인 3.0 반환
arithmeticMean(3, 8.25, 18.75)
// 위의 세 수에 대한 산술 평균인 10.0 반환
```

함수는 여러 개의 가변 매개 변수를 가질 수 있습니다. 가변 매개 변수 다음에 오는 첫 번째 매개 변수는 반드시 인자 레이블을 가져야 합니다. 인자 레이블이 있어야 어느 인자들이 가변 매개 변수로 전달되고 어느 인자들이 그 다음 매개 변수로 전달되는지 명확해집니다.

### 인-아웃 매개 변수

함수 매개 변수는 기본적으로 상수입니다. 함수 몸체 내부에서 매개 변수의 값을 수정하려 하면 컴파일 시간 오류가 발생합니다. 즉, 실수로라도 매개 변수의 값을 바꿀 일이 없습니다. 만약 함수 내에서 매개 변수의 값을 수정하고, 함수 호출이 끝난 후에도 그 변화가 유지되어야 한다면 **인-아웃 매개 변수**로 정의하세요.

인-아웃 매개 변수는 매개 변수의 자료형 바로 앞에 `inout` 키워드를 붙여 정의합니다. 인-아웃 매개 변수는 함수로 **들어오는** 값을 함수 내에서 수정하여 함수 밖으로 **내보내** 기존 값을 대체하도록 합니다. 인-아웃 매개 변수의 동작과 연관된 컴파일러 최적화에 관한 구체적인 논의는 [인-아웃 매개 변수](../language-reference/declarations.md#인-아웃-매개-변수)를 참고하세요.

인-아웃 매개 변수에 대한 인자로는 변수만 전달할 수 있습니다. 상수나 리터럴 값은 수정될 숭 벗으므로 인자로 전달하지 못합니다. 인-아웃 매개 변수로 전달하는 변수 이름 바로 앞에 앰퍼샌드(`&`)를 붙여 함수에 의해 수정될 수 있음을 나타내세요.

> **참고**
> 
> 인-아웃 매개 변수는 기본 값을 가질 수 없으며, 가변 매개 변수는 `inout`으로 정할 수 없습니다.

아래 `swapTwoInt(_:_:)`라고 하는 예시 함수는 두 인-아웃 정수 매개 변수 `a`와 `b`를 가집니다.

```swift
func swapTwoInts(_ a: inout Int, _ b: inout Int) {
    let temporaryA = a
    a = b
    b = temporaryA
}
```

`swapTwoInts(_:_:)` 함수는 단순히 `b`의 값을 `a`로, `a`의 값을 `b`로 바꿉니다. 그 과정에서 `a`의 값을 임시 상수인 `temporaryA`에 저장하고 `b`의 값을 `a`에 할당한 뒤, `temporaryA`의 값을 `b`에 할당합니다.

`Int`형의 두 변수의 값을 서로 바꾸는 데 이 `swapTwoInts(_:_:)` 함수를 사용할 수 있습니다. `someInt`와 `anotherInt`를 `swapTwoInts(_:_:)` 함수로 전달할 때, 이름 앞에 앰퍼샌드를 붙인 것을 확인하세요.

```swift
var someInt = 3
var anotherInt = 107
swapTwoInts(&someInt, &anotherInt)
print("someInt is now \(someInt), and anotherInt is now \(anotherInt)")
// "someInt is now 107, and anotherInt is now 3" 출력
```

위 예시는 `someInt`와 `anotherInt`가 `swapTwoInts(_:_:)` 함수 밖에서 정의되었음에도 이 함수에 의해 수정되고 있음을 보여줍니다.

> **참고**
> 
> 인-아웃 함수는 함수가 값을 반환하는 것과 다릅니다. 위 예시였던 `swapTwoInts`는 반환형을 정의하지도, 값을 반환하지도 않지만 `someInt`와 `anotherInt`의 값을 수정합니다. 인-아웃 매개 변수는 함수가 몸체의 범위 바깥에 영향을 주는 방법 중 하나입니다.

## 함수형

모든 함수는 매개 변수의 자료형과 함수의 반환형으로 이루어진 명확한 **함수형**을 가집니다.

예를 들어:

```swift
func addTwoInts(_ a: Int, _ b: Int) -> Int {
    return a + b
}
func multiplyTwoInts(_ a: Int, _ b: Int) -> Int {
    return a * b
}
```

이 예시는 `addTwoInts`와 `multiplyTwoInts`라고 하는 간단한 수학 함수 두 개를 정의하고 있습니다. 두 함수 모두 두 `Int` 값을 받아 적당한 연산의 결과로 `Int` 값을 반환합니다.

두 함수의 자료형 모두 `(Int, Int) -> Int`이며, 다음과 같이 읽습니다:

"`Int`형의 매개 변수 두 개를 가지며 `Int`형의 값을 반환하는 함수"

다른 예시로는 매개 변수와 반환 값 모두 없는 함수가 있습니다.

```swift
func printHelloWorld() {
    print("hello, world")
}
```

이 함수의 자료형은 `() -> Void`, 즉 "매개 변수를 가지지 않으며 `Void`를 반환하는 함수"입니다.

### 함수형 사용

함수형은 Swift에서 다른 자료형들과 똑같이 사용합니다. 예를 들어 상수나 변수를 함수형으로 지정하고 적당한 함수를 할당할 수 있습니다.

```swift
var mathFunction: (Int, Int) -> Int = addTwoInts
```

이것은 다음과 같이 읽을 수 있습니다:

"'두 `Int` 값을 받아 `Int` 값을 반환하는 함수'의 자료형을 가지는 변수 `mathFunction`을 정의하라. 이 새로운 변수가 함수 `addTwoInts`를 참조하도록 설정하라."

`addTwoInts(_:_:)` 함수는 `mathFunction` 변수와 자료형이 같으므로 Swift의 자료형 검사기가 위와 같은 할당을 허용합니다.

이제 할당된 함수를 `mathFunction`라는 이름으로 호출할 수 있습니다.

```swift
print("Result: \(mathFunction(2, 3))")
// "Result: 5" 출력
```

다른 함수도 자료형만 일치한다면, 함수형이 아닌 자료형들과 마찬가지로, 같은 변수에 할당할 수 있습니다.

```swift
mathFunction = multiplyTwoInts
print("Result: \(mathFunction(2, 3))")
// "Reuslt: 6" 출력
```

다른 자료형들과 마찬가지로 상수나 변수에 함수를 선언할 때 Swift가 함수형을 추론하게끔 할 수 있습니다.

```swift
let anotherMathFunction = addTwoInts
// anotherMathFunction은 (Int, Int) -> Int형으로 추론됩니다.
```

### 매개 변수형으로서의 함수형

`(Int, Int) -> Int`와 같은 함수형을 다른 함수의 매개 변수의 자료형으로 사용할 수 있습니다. 함수 구현의 일부분을 해당 함수가 호출될 때 호출자가 제공하도록 내버려 두는 것입니다.

위의 수학 함수들의 결과를 출력하는 예시입니다.

```swift
func printMathResult(_ mathFunction: (Int, Int) -> Int, _ a: Int, _ b: Int) {
    print("Result: \(mathFunciton(a, b))")
}
printMathResult(addTwoInts, 3, 5)
// "Result: 8" 출력
```

이 예시는 세 개의 매개 변수를 가지는 함수 `printMathResult(_:_:_:)`를 정의하고 있습니다. 첫 번쨰 매개 변수는 `mathFunction`으로 `(Int, Int) -> Int`형을 가집니다. 이 자료형의 어떤 함수든 이 첫 매개 변수에 대한 인자로 전달할 수 있습니다. 두 번째와 세 번째 매개 변수는 각각 `a`, `b`로, 둘 다 `Int`형입니다. 이들은 주어진 수학 함수에 대한 입력 값으로서 사용됩니다.

`printMathResult(_:_:_:)`는 호출되면서 `addTwoInts(_:_:)` 함수와 정수 값 `3`, `5`를 전달받습니다. 전달받은 함수를 `3`, `5`와 함께 호출하여 그 결과인 `8`을 출력합니다.

`printMathResult(_:_:_:)`의 역할은 알맞은 자료형의 수학 함수의 호출 결과를 출력하는 것입니다. 그 함수의 구현이 실제로 어떤지는 중요하지 않습니다. 오직 함수의 자료형만 중요합니다. 이로써 `printMathResult(_:_:_:)`는 자료형 안전 방법으로 기능성의 일부를 함수의 호출자에게 떠넘길 수 있습니다.

### 반환형으로서의 함수형

함수형을 다른 함수의 반환형으로 사용할 수 있습니다. 완전한 함수형을 반환하는 함수의 반환 화살표(`->`) 바로 뒤에 적으세요.

다음 예시는 두 가지 간단한 함수인 `stepForward(_:)`와 `stepBackward(_:)`를 정의하고 있습니다. `stepForward(_:)` 함수는 입력 값보다 하나 큰 값을 반환하며, `stepBackward(_:)` 함수는 입력 값보다 하나 작은 값을 반환합니다. 두 함수의 자료형 모두 `(Int) -> Int`형입니다.

```swift
func stepForward(_ input: Int) -> Int {
    return input + 1
}
func stepBackward(_ input: Int) -> Int {
    return input - 1
}
```

다음 함수 `chooseStepFunction(backward:)`는 반환형이 `(Int) -> Int`입니다. `chooseStepFunction(backward:)` 함수는 불형 매개 변수인 `backward`에 따라 `stepForward(_:)` 함수 또는 `stepBackward(_:)` 함수를 반환합니다.

```swift
func shooseStepFunction(backward: Bool) -> (Int) -> Int {
    return backward ? stepBackward : stepForward
}
```

이제 `chooseStepFunction(backward:)`를 사용하여 특정 방향으로 작동할 함수를 얻을 수 있습니다.

```swift
var currentValue = 3
let moveNearerToZero = chooseStepFunction(backward: currentValue > 0)
// moveNearerToZero는 이제 stepBackward() 함수를 참조합니다.
```

위 예시는 변수 `currentValue`가 `0`으로 다가가기 위해 양의 움직임이 필요한지 음의 움직임이 필요한지 결정합니다. `currentValue`의 초기 값이 `3`이므로 `currentValue > 0`은 `true`를 반환, `chooseStepFunction(backward:)`는 `stepBackward(_:)` 함수를 반환합니다. 반환된 함수에 대한 참조가 상수 `moverNearerToZero`에 저장됩니다.

`moveNearerToZero`가 올바른 함수를 참조함에 따라 이를 사용하여 `0`까지 셀 수 있습니다.

```swift
print("Counting to zero:")
// 0까지 세기
while currentValue != 0 {
    print("\(currentValue)...")
    currentValue = moveNearerToZero(currentValue)
}
print("zero!")
// 3...
// 2...
// 1...
// zero!
```

## 중첩 함수

이 장에서 접한 모든 함수는 전역에서 정의된 **전역 함수**들이었습니다. 다른 함수의 몸체 내부에서 정의되는 **중첩 함수**도 있습니다.

중첩 함수는 기본적으로 외부 세계에서는 가려져 있지만, 이를 감싸고 있는 함수를 사용하여 호출할 수 있습니다. 감싸는 함수는 또한 중첩 함수를 반환하여 다른 영역에서 사용되도록 해주기도 합니다.

위의 `chooseStepFunction(backward:)` 예시를 중첩 함수를 사용하고 반환할 수 있도록 다시 작성합니다.

```swift
func chooseStepFunction(backward: Bool) -> (Int) -> Int {
    func stepForward(input: Int) -> Int { return input + 1 }
    func stepBackward(input: Int) -> Int { return input - 1 }
    return backward ? stepBackward : stepForward
}
var currentValue = -4
let moveNearerToZero = chooseStepFunction(backward: currentValue > 0)
// moveNearerToZero는 이제 중첩된 stepForward() 함수를 참조합니다.
while currentValue != 0 {
    print("\(currentValue)... ")
    currentValue = moveNearerToZero(currentValue)
}
print("zero!")
// -4...
// -3...
// -2...
// -1...
// zero!
```