---
layout: default
title: 제어 흐름
description: Control Flow
parent: Swift 안내서
nav_order: 5
---

# 컬렉션형

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

Swift는 다양한 제어 흐름 구문을 제공합니다. 작업을 여러 번 반복하도록 하는 `while` 반복문, 상황에 따라 다른 분기를 실행하는 `if`, `guard`, `switch` 구문, 실행 흐름을 코드 내의 다른 부분으로 옮기는 `brack`와 `continue` 구문 등이 있습니다.

Swift는 배열, 딕셔너리, 범위, 문자열 등을 쉽게 반복할 수 있도록 `for`-`in` 반복문도 제공합니다.

Swift의 `switch` 구문은 C와 유사한 다른 언어들에서 사용되는 것보다 훨씬 강력합니다. 케이스는 구간 일치, 튜플, 특정 자료형으로의 캐스팅을 포함한 여러 패턴 일치를 지원합니다. `switch` 케이스에서 일치하는 값은 임시 상수나 변수로서 케이스 몸체 내부에서 사용될 수 있습니다. 각각의 케이스마다 복잡한 일치 조건도 `where` 절로 표현할 수 있습니다.

## For-In 반복문

`for`-`in` 반복문은 배열, 수의 범위, 문자열 내의 문자와 같은 순열을 반복하는 데 사용됩니다.

아래 예시는 배열의 원소들을 `for`-`in` 반복문을 이용하여 반복하고 있는 상황을 보여줍니다.

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

딕셔너리의 키-값 쌍도 반복할 수 있습니다. 딕셔너리의 각각의 원소는 반복될 때 `(key, value)` 튜플로 반환되며, 이를 이름을 가진 상수로 분해하여 `for`-`in` 반복문 몸체에서 사용할 수 있습니다. 아래 예시 코드에서 딕셔너리의 키들은 `animalName`이라는 이름의 상수로, 값들은 `legCount`라는 이름의 상수로 분해됩니다.

```swift
let numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
for (animalName, legCount) in numberOfLegs {
    print("\(animalName)s have \(legCount) legs")
}
// cats have 4 legs
// ants have 6 legs
// spiders have 8 legs
```

`Dictionary`의 내용은 애초에 순서가 없기 때문에 반복할 때 어느 원소부터 참조될지 보장하지 않습니다. `Dictionary`에 원소를 삽입한 순서도 반복되는 순서를 정하는 것이 아닙니다. 배열과 딕셔너리에 관한 자세한 설명은 [컬렉션형](collection-types.md)을 참고하세요.

`for`-`in` 반복문을 수의 범위와 함께 사용할 수도 있습니다. 아래 예시는 구구단 5단의 처음 몇 단계를 출력합니다.

```swift
for index in 1...5 {
    print("\(index) times 5 is \(index * 5)")
}
// 1 times 5 is 5
// 2 times 5 is 10
// 3 times 5 is 15
// 4 times 5 is 20
// 5 tiems 5 is 25
```

여기서 반복되는 순열은 양끝을 포함하여 `1`부터 `5`까지의 수로, 닫힌 범위 연산자(`...`)로 표현합니다. `index`의 값이 범위의 처음에 해당하는 `1`로 설정된 상태로 반복문 내부의 문장이 실행됩니다. 지금은 반복문 안에는 `index`의 현재 값에 대한 5단을 출력하는 문장 하나뿐입니다. 이 문장이 실행되고 나면 `index`의 값은 범위의 두 번째 값에 해당하는 `2`로 업데이트되고 `print(_:separator:terminator:)` 함수가 다시 호출됩니다. 이 과정이 범위의 끝에 도달할 때까지 계속됩니다.

위의 예시에서 `index`는 반복할 때마다 처음에 자동으로 설정되는 상수입니다. 따라서 `index`는 사용하기 전에 미리 선언할 필요가 없습니다. 반복문의 정의에 포함만 하면 `let` 선언 키워드 없이 묵시적으로 선언됩니다.

순열의 각각의 값이 필요 없다면 변수 이름 대신 밑줄을 입력해 값을 무시하세요.

```swift
let base = 3
let power = 10
var answer = 1
for _ in 1...power {
    answer *= base
}
print("\(base) to the power of \(power) is \(answer)")
// "3 to the power of 10 is 59049" 출력
```

이 예시는 어떤 수의 거듭제곱(지금은 `3`의 `10`제곱)을 계산합니다. `1`부터 `10`까지의 닫힌 범위에 따라 (`3`의 `0`제곱인) `1`에서 시작하여 `3`을 열 번 곱합니다. 이 계산에서는 각각의 반복이 몇 번째인지 셀 필요가 없습니다. 단순히 주어진 횟수만큼 반복을 실행합니다. 반복 변수 자리에 밑줄 문자(`_`)를 입력하면 각각의 값이 무시되어 매 반복에서 현재 값에 대한 접근이 불가능해집니다.

어떤 상황에서는 범위의 양끝을 포함하는 닫힌 범위가 부적절하기도 합니다. 시계 위에 매 분마다 눈금을 그린다고 생각해보세요. 눈금은 `0`분에서부터 시작해 총 `60`개가 필요합니다. 반 열린 범위 연산자(`..<`)를 사용하면 시작 값은 포함하지만 마지막 값은 포함하지 않는 범위가 만들어집니다. 범위에 관해서는 [범위 연산자](basic-operators.md/범위-연산자)를 참고하세요.

```swift
let minutes = 60
for tickMark in 0..<minutes {
    // 매 분마다 눈금 렌더 (60회)
}
```

사용자에 따라 UI에 눈금이 더 적어야 한다고 생각할 수도 있습니다. `5`분마다 눈금 하나를 그리기로 해봅시다. `stride(from:to:by)` 함수를 사용해 필요 없는 눈금을 건너뛰세요.

```swift
let minuteInterval = 5
for tickMark in stride(from: 0, to: minutes, by: minuteInterval) {
    // 5분마다 눈금 렌더 (0, 5, 10, 15 ... 45, 50, 55)
}
```

닫힌 범위도 `stride(from:through:by:)` 함수를 사용하면 됩니다.

```swift
let hours = 12
let hourInterval = 3
for tickMark in stride(from: 3, through: hours, by: hourInterval) {
    // 3시간마다 눈금 렌더 (3, 6, 9, 12)
}
```

지금까지 범위와 배열, 딕셔너리, 문자열을 반복하는 데 `for`-`in` 반복문을 사용했습니다. 그러나 [`Sequence`(영문)](https://developer.apple.com/documentation/swift/sequence) 프로토콜을 따르는 컬렉션이라면, 직접 정의한 클래스나 컬렉션형이든 **무엇이든** 반복하는 데 이 문법을 사용할 수 있습니다.

## While 반복문

`while` 반복문은 조건이 `false`가 될 때까지 내부 문장들을 수행합니다. 이런 형태의 반복문은 반복 횟수를 모른 채 반복을 시작해야 할 때 주로 사용됩니다. Swift는 두 가지 `while` 반복문을 지원합니다.

* `while`은 매 반복에 앞서 조건을 평가합니다.
* `repeat`-`while`은 매 반복이 끝나고 조건을 평가합니다.

### While

`while` 반복문은 하나의 조건문을 평가하는 것으로 시작합니다. 조건이 `true`라면 `false`가 될 때까지 내부의 문장들을 반복합니다.

`while` 반복문의 일반적인 형태는 이렇습니다.

```swift
while (condition) {
    (statements)인
}
```

아래에 간단한 뱀 사다리 게임이 나와 있습니다. 

![](../../assets/images/snakesAndLadders.png)

게임의 규칙은 다음과 같습니다:

* 보드 판에는 25개의 칸이 있으며, 게임의 목표는 25번 칸에 도달하거나 이를 넘어가는 것입니다.
* 플레이어는 보드 판의 왼쪽 아래 코너인 "0번 칸"에서 시작합니다.
* 매 턴마다 주사위를 굴려 나온 수만큼 위에 표시된 점선을 따라 이동합니다.
* 사다리 아래 끝에서 멈추면 사다리를 타고 올라갑니다.
* 뱀의 머리에서 멈추면 뱀을 타고 미끄러져 내려옵니다.

보드 판은 `Int` 값의 배열로 표현됩니다. 배열의 크기는 `finalSquare`라는 상수에 따릅니다. `finalSquare` 상수는 배열을 초기화하고 추후에 승리 조건을 검사하는 데 사용됩니다. 플레이어는 보드 판 바로 밖에 있는 "0번 칸"에서 시작하므로 보드 판은 26개의 `Int` 값 `0`으로 초기화됩니다.

```swift
let finalSquare = 25
var board = [Int](repeating: 0, count: finalSquare + 1)
```

뱀과 사다리를 고려하여 일부 칸들은 특별한 값들을 가지도록 설정합니다. 사다리 아래 끝에 해당하는 칸은 플레이어가 위로 올라가도록 양수 값을 가지고, 뱀 머리에 해당하는 칸은 플레이어가 아래로 내려가도록 음수 값을 가집니다.

```swift
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
```

3번 칸은 사다리 아래 끝으로서, 플레이어를 11번 칸으로 올립니다. 이걸 나타내고자 `board[03]`에 (`3`과 `11`의 차이인) 정수 값 `8`과 같은 의미의 `+08`을 할당합니다. 값과 문장들을 정렬하기 위해 단항 마이너스 연산자(`-i`)와 함꼐 단항 플러스 연산자(`+i`)도 명시적으로 사용했으며, `10`보다 작은 수들도 `0`을 사용하여 두 자리로 맞추었습니다. (스타일링에 관한 기술은 꼭 필요한 것은 아니지만 코드를 더 깔끔하게 만듭니다.)

```swift
var square = 0
var diceRoll = 0
while square < finalSquare {
    // 주사위 굴리기
    diceRoll += 1
    if diceRoll == 7 { diceRoll = 1}
    // 나온 눈의 수만큼 이동
    square += diceRoll
    if square < board.count {
        //아직 보드 판 위에 있다면 뱀이나 사다리를 타고 이동
        square += board[square]
    }
}
print("Game over!")
```

위 예시는 주사위를 매우 단순한 방식으로 굴리고 있습니다. 난수를 생성하는 것 대신 `diceRoll` 값을 `0`으로 하여 시작합니다. `while` 반복문을 통과할 때마다 `diceRoll`을 하나씩 늘리면서 너무 커지지 않았는지 검사합니다. `7`이 될 때마다 다시 `1`로 초기화됩니다. 결과적으로 `diceRoll`의 값은 항상 `1`, `2`, `3`, `4`, `5`, `6`, `1`, `2` 순서로 반복됩니다.

주사위를 굴린 후 플레이어는 `diceRoll`만큼 칸을 움직입니다. 이때 플레이어가 25번 칸을 넘어가 게임이 종료될 수도 있습니다. 이 상황을 다루기 위해 코드에서는 `square`가 `board` 배열의 `count` 프로퍼티보다 작은지 검사하고 있습니다. `square`가 유효하다면 `board[square]`에 저장된 값만큼 `square` 값에 더해져 플레이어가 사다리나 뱀을 따라 움직이게 됩니다.

> **참고**
> 
> 이 검사가 이루어지지 않으면 `board[square]`가 `board` 배열의 범위를 넘어서 접근하려 할 수 있으며, 이때 런타임 오류가 발생합니다.

해당 `while` 반복문은 종료되고 다시 반복되어야 하는지 반복 조건을 검사하게 됩니다. 플레이어가 `25`번 칸 이후로 이동했다면 반복 조건은 `false`로 평가되어 게임이 종료됩니다.

`while` 반복문이 시작할 시점에는 게임의 길이가 명확하지 않으므로, 이런 상황에서는 `while` 반복문이 적합합니다. 특정 조건이 만족되기 전까지 반복을 진행할 수 있습니다.

### Repeat-While

`while` 반복문의 변형인 `repeat`-`while` 반복문은 반복 조건을 따지기 **전에** 우선 반복 단위를 한 번 통과합니다. 그리고 나서 조건이 `false`가 될 때까지 반복을 이어나갑니다.

> **참고**
> 
> Swift의 `repeat`-`while` 반복문은 다른 언어의 `do`-`while` 반복문과 유사합니다.

`repeat`-`while` 반복문의 일반적인 형태는 이렇습니다:

```swift
repeat {
    (statements)
} while (condition)
```

다시 뱀 사다리 게임을 살펴봅시다. `while` 반복문 대신 `repeat`-`while` 반복문으로 작성할 수 있습니다. `finalSquare`, `board`, `square`, `diceRoll`의 값은 `while` 반복문에서와 동일한 방식으로 초기화됩니다.

```swift
let finalSquare = 25
var board = [Int](repeating: 0, count: finalSquare + 1)
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
var square = 0
var diceRoll = 0
```

이번 버전에서는 반복 내에서의 **첫 번째** 동작이 사다리나 뱀을 검사하는 것입니다. 플레이어를 25번 칸으로 올리는 사다리는 없으므로 사다리를 올라감으로써 게임에서 승리하는 경우는 불가능합니다. 그러므로 뱀이나 사다리를 먼저 검사해도 안전합니다.

게임이 시작하면 플레이어는 "0번 칸"에 위치합니다. `board[0]`는 항상 `0`이므로 효과가 없습니다.

```swift
repeat {
    // 뱀이나 사다리를 타고 이동
    square += board[square]
    // 주사위 굴리기
    diceRoll += 1
    if diceRoll == 7 { diceRoll = 1 }
    // 나온 눈만큼 이동
    square += diceRoll
} while square < finalSquare
print("Game over!")
```

뱀과 사다리를 검사하고 나면 주사위가 굴려지고 플레이어가 `diceRoll`만큼 앞으로 이동합니다. 해당 반복문은 이렇게 종료됩니다.

반복 조건(`while square < finalSquare`)는 이전과 같으나 이번에는 반복문의 **끝**에 처음 도달하기 전까지 평가되지 않습니다. `repeat`-`while` 반복문의 구조는 이전의 `while` 반복문보다 더 게임에 어울립니다. `repeat`-`while` 반복문에서 `square += board[square]`는 `whiie` 조건이 `square`가 아직 보드 판 위에 있음을 확인한 **직후**에 항상 실행됩니다. 이런 방식에서는 `while` 반복문을 사용한 이전 버전에서와 같이 배열의 범위를 검사할 필요가 없습니다.

## 조건문

특정 조건에 따라 다른 코드 단위를 실행해야 할 때가 있습니다. 오류가 발생했을 때 따로 코드 단위를 실행시켜야 할 수도 있고, 어떤 값이 너무 작거나 클 때 메시지를 띄워야 할 수도 있습니다. 이럴 때, 코드 단위들을 **조건부로** 만들면 됩니다.

Swift는 코드에 조건 분기를 추가하는 방법을 두 가지 제공합니다. 하나는 `if` 구문, 다른 하나는 `switch` 구문입니다. 일반적으로 가능한 결과의 가짓수가 몇 안 되는 단순한 조건문을 평가할 때 `if` 구문을 사용합니다. `switch` 구문은 가능한 가짓수가 많은 복잡한 조건문을 평가하거나, 평가해야 할 코드 분기를 패턴 일치를 사용하여 고를 때 적합합니다. 

### If

가장 단순한 `if` 구문은 `if` 조건문이 하나뿐인 경우입니다. 오직 그 조건이 `true`일 때만 내부의 문장들을 실행합니다.

```swift
var temperatureInFahrenheit = 30
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
}
// "It's very cold. Consider wearing a scarf." 출력
```

이 예시는 온도가 화씨 `32`도(물의 어는점) 이하인지 검사합니다. 만약 그렇다면, 메시지가 출력됩니다. 그렇지 않다면 메시지는 출력되지 않고 `if` 구문의 닫는 괄호 다음의 코드가 이어집니다.

`if` 구문에는 `if` 조건문이 `false`인 경우에 대해, **else 절**이라고 하는 다른 문장 단위를 추가할 수 있습니다. 이 문장들은 `else` 키워드로 표시됩니다.

```swift
temperatureInFahrenheit = 40
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
} else {
    print("It's not that cold. Wear a t-shirt.")
}
// "It's not that cold. Wear a t-shirt." 출력
```

언제나 이 두 분기 중에 하나가 실행됩니다. 온도가 화씨 `40`도로 증가했으므로 더 이상 스카프를 둘러야 할 만큼 춥지 않습니다. 따라서 `else` 분기가 대신 실행됩니다.

`if` 구문을 여러 개 연결해 더 다양한 절을 만들 수도 있습니다.

```swift
temperatureInFahrenheit = 90
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
} else if temperatureInFahrenheit >= 86 {
    print("It's really warm. Don't forget to wear sunscreen.")
} else {
    print("It's not that cold. Wear a t-shirt.")
}
// "It's really warm. Don't forget to wear sunscreen." 출력
```

특히 따뜻한 온도에 응답하는 `if` 구문을 추가했습니다. 남아 있는 마지막 `else` 절은 너무 따뜻하거나 춥지 않은 모든 온도에 대해 응답을 출력합니다.

그러나 마지막 `else` 절은 필수가 아니므로 조건들이 완전할 필요가 없다면 생략해도 됩니다.

```swift
temperatureInFahrenheit = 72
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
} else if temperatureInFahrenheit >= 86 {
    print("It's really warm. Don't forget to wear sunscreen.")
}
```

`if`나 `else if` 조건에 부합할 정도로 온도가 너무 춥거나 따뜻하지 않으므로 메시지가 출력되지 않습니다.

### 스위치

`switch` 구문은 주어진 값을 정해둔 패턴들과 일치하는지 비교합니다. 처음으로 일치하는 패턴에 따라 그에 대응하는 코드 단위를 실행합니다. `switch` 구문은 여러 상태에 대응해야 하는 `if` 구문에 대한 보완책입니다.

`switch` 구문의 가장 간단한 형태는 값을 같은 자료형의 하나 이상의 값과 비교하는 것입니다.

```swift
switch (some value to consider) {
case (value 1):
    (respond to value 1)
case (value 2), (value 3):
    (respond to value 2 or 3)
default:
    (otherwise, do something else)
}
```

모든 `switch` 구문은 `case` 키워드로 시작하는 여러 **케이스**로 이루어져 있습니다. Swift에서는 케이스마다 특정 값과 비교할 뿐만 아니라 더 복잡한 패턴 일치를 지정할 수 있습니다. 이 옵션들은 아래에서 소개될 예정입니다.

`if` 구문의 몸체처럼 각각의 `case`도 개별적으로 실행되는 코드 분기입니다. `switch` 구문은 어느 분기를 선택할지 결정합니다. 이 과정을 주어진 값에 대한 **스위칭**이라고 합니다.

모든 `switch` 구문은 반드시 **포괄적**이어야 합니다. 즉, 다루고 있는 자료형의 어떤 값이든 하나의 `switch` 케이스와 일치해야 합니다. 가능한 모든 값에 대해 케이스를 전부 제공하기 어렵다면, 명시적으로 다뤄지지 않는 모든 값을 처리할 기본 케이스를 정의하세요. 기본 케이스는 `default` 키워드로 나타내며, 항상 마지막에 나타나야 합니다.

이 예시에서 `switch` 구문은 `someCharacter`라고 하는 소문자 하나를 다루고 있습니다.

```swift
let someCharacter: Character: "z"
switch someCharacter {
case "a":
    print("THe first letter of the alphabet")
case "z":
    print("The last letter of the alphabet")
default:
    print("Some other character")
}
// "The last letter of the alphabet" 출력
```

`switch` 구문의 첫 번째 케이스는 첫 알파벳인 `a`와 일치하고, 두 번째 케이스는 마지막 알파벳인  `z`와 일치합니다. `switch`는 알파벳 뿐만 아니라 모든 문자에 대한 케이스를 가지고 있어야 하므로 이 `switch` 구문은 `a`나 `z` 이와의 모든 문자와 일치하는 `default` 케이스를 사용하고 있습니다. 이로써 `switch` 구문이 포괄적임이 보장됩니다.

## 묵시적 계속의 부재

C나 Objective-C의 `switch` 구문과 다르게 Swift의 `switch` 구문은 각각의 케이스가 끝나도 자동적으로 다음 케이스를 계속하지 않습니다. 대신 처음으로 일치하는 `switch` 케이스가 완료되는 대로 명시적인 `breack` 문장 없이도 `switch` 구문 전체가 종료됩니다. 이로써 `switch` 구문이 C에서보다 더 안전하고 사용하기 쉬워지며, 실수로 다른 `switch` 케이스까지 실행되는 것을 막습니다.

> **참고**
> 
> Swift에서 `break`가 필요 없긴 하지만, 특정 케이스와 일치하는 경우를 무시하거나 일치한 케이스가 완전히 끝나기 전에 빠져나오는 데 `break`를 사용할 수 있습니다. 자세한 내용은 [스위치 구문에서의 Break](스위치-구문에서의-Break)를 참고하세요.

모든 케이스의 몸체는 **반드시** 실행할 문장을 하나 이상 포함하고 있어야 합니다. 다음 코드는 첫 번째 케이스가 비어 있으므로 유효하지 못합니다.

```swift
let anotherCharacter: Character = "a"
switch anotherCharacter {
case "a": // 케이스 몸체가 비어 있으므로 무효
case "A":
    print("The letter A")
default:
    print("Not the letter A")
}
// 컴파일 시간 오류가 발생합니다.
```

C에서와 다르게 Swift에서는 이 `switch` 구문이 `"a"`와 `"A"` 모두와 일치하지 않습니다. 오히려 `case "a":`가 실행할 문장을 하나도 가지고 있지 않아 컴파일 시간 오류가 발생합니다. 실수로 인해 한 케이스에서 다른 케이스로 계속되는 경우를 피하고, 코드의 의도를 명확하게 해 더 안전해집니다.

`"a"`와 `"A"` 모두와 일치하는 케이스 만들려면 두 값을 쉼표로 분리하여 혼합 케이스를 만드세요.

```swift
let anotherCharacter: Character = "a"
switch anotherCharacter {
case "a", "A":
    print("The letter A")
default:
    print("Not the letter A")
}
// "The letter A" 출력
```

가독성을 위해 혼합 케이스를 여러 줄에 걸쳐 적어도 됩니다. 자세한 내용은 [혼합 케이스](혼합-케이스)를 참고하세요.

> **참고**
> 
> 특정 `switch` 케이스 끝에서 명시적으로 계속하려면, [계속](계속)에 설명된 `fallthrough` 키워드를 사용하세요.

## 구간 일치

`switch` 케이스의 값이 구간에 포함되는지 검사할 수 있습니다. 아래 예시에서는 수 구간을 사용하여 어떤 크기의 수를 셀 때의 영어 표현을 계산하고 있습니다.

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
// "There are dozens of moons orbiting Saturn." 출력
```

위 예시의 `switch` 구문에서는 `approximateCount`가 평가됩니다. 각각의 `case`는 이 값을 어떤 수나 구간과 비교합니다. `approximateCount`의 값이 12와 100 사이에 있으므로 `naturalCount`에 `"dozens of"`이라는 값이 할당되고 `switch` 구문이 종료됩니다.

## 튜플

튜플을 사용하면 같은 `switch` 구문에서 여러 값들을 검사할 수 있습니다. 튜플의 원소들은 저마다의 값이나 값의 구간과 비교됩니다. 와일드카드 패턴이라고도 부르는 밑줄 문자(`_`)는 모든 값들과 일치하게 됩니다.

아래 예시에서는 `(Int, Int)`형의 단순한 튜플로 표현된 (x, y) 점을 받아 제시된 그래프 위에서의 위치에 따라 분류합니다.

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
    print("\(somePoint) is outside the box")
}
// "(1, 1) is inside the box" 출력
```

![](../../assets/images/coordinateGraphSimple.png)

`switch` 구문은 점이 원점 (0, 0)에 있는지, 빨간색 x축 위에 있는지, 주황색 y축 위에 있는지, 원점을 중심으로 하는 파란색 4x4 상자 안에 있는지, 아니면 상자 밖에 있는지 판단합니다.

C와 다르게 Swift는 여러 `switch` 케이스에서 같은 값을 다루는 것을 허용합니다. 점 (0, 0)은 사실 예시에 나온 **네 가지** 케이스와 전부 일치합니다. 그러나 여러 케이스와 일치한다면, 항상 첫 번째로 일치하는 케이스가 사용됩니다. 점 (0, 0)은 `case (0, 0)`과 처음 일치하므로 다른 일치하는 케이스는 무시됩니다.

## 값 연결

일치하는 값을 임시 상수나 변수로 이름 붙이면 `switch` 케이스 몸체 안에서 값을 사용할 수 있습니다. 값들을 케이스 몸체 내부에서의 임시 상수나 변수에 연결하므로, 이를 **값 연결**이라고 부릅니다.

아래 예시에서는 `(Int, Int)`형의 튜플로 표현된 (x, y) 점을 받아 제시된 그래프 위에서의 위치에 따라 분류합니다.

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
\\ "on the x-axis with an x value of 2" 출력
```

![](../../assets/images/coordinateGraphMedium.png)

`switch` 구문은 점이 빨간색 x축 위에 있는지, 주황색 y축 위에 있는지, 아니면 (두 축 위가 모두 아닌) 다른 곳에 있는지 결정합니다.

세 `switch` 케이스는 `anotherPoint`로부터 하나 또는 두 개의 값을 임시로 받는 임시 상수 `x`와 `y`를 선언합니다. 첫 번째 케이스인 `case (let x, 0)`는 `y` 값이 `0`인 모든 점과 일치하며 그 점의 `x` 값을 임시 상수 `x`에 할당합니다. 마찬가지로 두 번째 케이스인 `case (0, let y)`는 `x` 값이 `0`인 모든 점과 일치하며 그 점이 `y` 값을 임시 상수 `y`에 할당합니다.

임시 상수가 선언된 후에는 그 값을 케이스의 코드 단위 내부에서 사용할 수 있습니다. 여기서는 점이 분류된 결과를 출력하는 데 사용하고 있습니다.

이 `switch` 구문은 `default` 케이스가 필요 없습니다. 마지막 케이스인 `case let (x, y)`가 모든 값과 일치할 수 있도록 두 개의 임시 상수로 이루어진 튜플을 선언하고 있습니다. `anotherPoint`는 언제나 두 개의 값으로 이루어진 튜플이므로 이 케이스가 남아 있는 모든 값들과 일치하며, 따라서 `switch` 구문을 포괄적으로 만드는 데 `default` 케이스가 필요하지 않습니다.

## Where











wip...!