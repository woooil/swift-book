---
layout: default
title: 컬렉션형
description: Collectio Types
parent: Swift 안내서
nav_order: 4
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

Swift는 **컬렉션형**을 사용하여 값들의 묶음, 즉 컬렉션을 저장합니다. 기초 컬렉션형으로는 배열, 집합, 딕셔너리가 있습니다. 배열은 값들이 순서대로 나열된 컬렉션입니다. 집합은 중복되지 않는 값들의 순서 없는 컬렉션입니다. 딕셔너리는 키-값 조합들로 이루어진 순서 없는 컬렉션입니다.

![](../../assets/images/CollectionTypes_intro.png)

Swift의 배열, 집합, 딕셔너리는 저장할 수 있는 값과 키의 자료형이 언제나 명확합니다. 즉, 컬렉션에 잘못된 자료형의 값을 삽입할 일은 실수로라도 일어나지 않습니다. 반대로 컬렉션에서 찾을 값의 자료형도 헷갈리지 않고 확실히 알 수 있습니다.

> **참고**
> 
> Swift의 배열과 집합, 딕셔너리형은 **제네릭 컬렉션**으로 구현되어 있습니다. 제네릭형과 컬렉션에 대한 자세한 정보는 [제네릭](generics.md)를 참고하세요.

## 컬렉션의 변경

배열이나 집합, 딕셔너리를 변수로 생성하면, 그 생성된 컬렉션은 변경될 수 **있습니다.** 즉, 컬렉션이 생성된 후에도 값을 추가하거나, 제거하거나, 바꾸는 식으로 컬렉션을 **변경할** 수 있습니다. 배열, 집합, 딕셔너리를 상수로 생성하면 컬렉션을 변경할 수 **없습니다.** 컬렉션의 크기나 내용물은 바뀔 수 없습니다.

> **참고**
> 컬렉션이 바뀔 필요가 없다면 항상 변경 불가능한 컬렉션으로 생성하도록 하세요. 그렇게 하면 여러분도 코드를 파악하기 쉽고 Swift 컴파일러도 컬렉션의 성능을 최적화할 수 있습니다.

## 배열

**배열**은 같은 자료형의 값들을 정렬하여 목록으로 저장합니다. 배열 내에 다른 위치에서 같은 값이 여러 번 등장할 수도 있습니다.

> **참고**
> 
> Swift의 `Array`형은 Foundation의 `NSArray` 클래스와 연결됩니다.
> 
> `Array`를 Foundation과 Cocoa와 함께 사용하려면 [Array와 NSArray의 연결(영문)](https://developer.apple.com/documentation/swift/array#2846730)을 참고하세요.

### 배열형의 축약형 문법

Swift 배열의 자료형의 완전한 표기법은 `Array<Element>`입니다. (단, `Element`는 배열이 저장할 수 있는 값의 자료형) 그렇지만 배열형을 축약형인 `[Element]`으로 적어도 됩니다. 두 형식 모두 기능적으로는 동등하지만 축약형이 일반적으로 더 선호됩니다. 이 문서에서도 축약형을 계속 사용합니다.

### 빈 배열 생성

이니셜라이저 문법을 사용하면 특정 자료형의 빈 배열을 생성할 수 있습니다.

```swift
var someInts: [Int] = []
print("someInts is of type [Int] with \(someInts.count) items.")
// "someInts is of type [Int] with 0 items." 출력
```

`someInts` 변수의 자료형은 이니셜라이저의 자료형으로부터 `[Int]`형으로 추론됩니다.

함수의 전달 인자나 이미 입력된 변수나 상수처럼 자료형에 관한 정보가 이미 주어진 상황이라면, 빈 배열 리터럴, 즉 `[]`(비어 있는 대괄호 쌍)을 적어 비어 있는 배열을 만들 수 있습니다.

```swift
someInts.append(3)
// someInts는 이제 Int형 값 하나를 가집니다.
someInts = []
// someInts는 이제 비어 있는 배열이지만, 자료형은 여전히 [Int]입니다.
```

### 기본 값을 가지는 배열 생성

Swift의 `Array`가 가진 이니셜라이저를 사용하면 모두 같은 기본 값을 가지는 정해진 크기의 배열을 만들 수 있습니다. 이니셜라이져에 알맞은 자료형의 기본 값(`repeating`)과 새 배열에서 그 값이 반복될 횟수(`count`)를 전달하세요.

```swift
var threeDoubles = Array(repeating: 0.0, count: 3)
// threeDoubles은 [Double]형이며, [0.0, 0.0, 0.0]과 같습니다.
```

### 두 배열을 더한 배열 생성

자료형이 같은 두 자료형을 덧셈 연산자(`+`)로 더하면 새로운 배열을 생성할 수 있습니다. 새 배열의 자료형은 더하는 두 배열의 자료형으로부터 추론됩니다.

```swift
var anotherThreeDoubles = Array(repeating: 2.5, count: 3)
// anotherThreeDoubles은 [Double]형이며, [2.5, 2.5, 2.5]와 같습니다.

var sixDoubles = threeDoubles + anotherThreeDoubles
// sixDoubles은 [Double]형이며, [0.0, 0.0, 0.0, 2.5, 2.5, 2.5]와 같습니다.
```

### 배열 리터럴을 이용한 배열 성성

**배열 리터럴**을 이용해서 배열을 초기화할 수도 있습니다. 배열 리터럴은 하나 이상의 값들로 간편하게 배열 컬렉션을 작성하는 방법입니다. 값들을 쉼표로 분리하여 적고 대괄호로 감싸 작성합니다.

```swift
[value 1, value 2, value 3]
```

아래 예시에서는 `String` 값들을 저장하는 배열 `shoppingList`를 만들고 있습니다.

```swift
var shoppingList: [String] = ["Eggs", "Milk"]
// shoppingList가 두 개의 초기 원소들로 초기화됩니다.
```

선언된 `shoppingList` 변수는 "문자열 값들의 배열"으로, `[String]`으로 표현합니다. 이 배열의 경우에는 `String` 값들로 지정되었기에 오직 `String` 값들만 저장할 수 있습니다. `shoppingList` 배열은 배열 리터럴을 이용하여 두 `String` 값(`"Eggs"`와 `"Milk"`)으로 초기화됩니다.

> **참고**
> 
> 아래 예시에서처럼 쇼핑 목록에는 물품들이 더 추가될 수 있습니다. 따라서 `shoppingList` 배열은 (`let`을 사용하는) 상수가 아닌 (`var`를 사용하는) 변수로 선언되었습니다.

이 경우 배열 리터럴은 오직 두 개의 `String` 값만 포함하고 있습니다. 이는 `shoppingList` 변수의 선언과 일치하며(배열은 `String` 값만 저장할 수 있다), 따라서 배열 리터럴을 이용해 `shoppingList`를 두 개의 초기 원소로 초기화하는 것이 가능합니다.

Swift의 자료형 추론 덕분에 하나의 자료형으로 이루어진 배열 리터럴로 배열을 초기화할 때, 자료형을 적지 않아도 됩니다. `shoppingList`의 초기화도 아래와 같이 더 짧게 가능합니다.

```swift
var shoppingList = ["Eggs", "Milk"]
```

배열 리터럴의 값들이 모두 같은 자료형이므로 Swift는 `shoppingList` 변수의 자료형으로 `[String]`이 알맞다고 추론할 수 있습니다.

### 배열에의 접급과 배열 수정

배열에 접근하거나 배열을 수정할 때는 메서드나 프로퍼티를 이용하거나 첨자 문법을 사용합니다.

배열이 가진 원소의 개수를 알아내기 위해서는 읽기 전용 프로퍼티인 `count`가 사용됩니다.

```swift
print("The shopping list contatins \(shoppingList.count) items.")
// "The shopping list contains 2 items." 출력
```

불형 프로퍼티인 `isEmpty`는 `count` 프로퍼티의 값이 `0`인지 검사하는 것과 같은 결과를 가집니다.

```swift
if shoppingList.isEmpty {
    print("The shopping list is empty.")
} else {
    print("The shopping list isn't empty.")
}
// "The shopping list isn't empty." 출력
```

배열의 `append(_:)` 메서드를 호출하면 배열 끝에 새로운 원소를 추가할 수 있습니다.

```swift
shoppingList.append("Flour")
// 누군가 팬케이크를 만들려나 봅니다. shoppingList는 이제 3개의 원소를 가집니다.
```

덧셈 할당 연산자(`+=`)로도 배열에 원소를 추가할 수 있습니다.

```swift
shoppingList += ["Baking Powder"]
// shoppingList는 이제 4개의 원소를 가집니다.
shoppingList += ["Chocholate Spread", "Cheese", "Butter"]
// shoppingList는 이제 7개의 원소를 가집니다.
```

첨자 문법으로 배열이 가진 원소의 값을 얻어낼 수 있습니다. 얻고 싶은 값의 인덱스를 대괄호로 감싸 배열 이름 바로 뒤에 붙이세요.

```swift
var firstItem = shoppingList[0]
// firstItem은 "Eggs"와 같습니다.
```

> **참고**
> 
> 배열의 첫 번째 원소는 인덱스 값이 `1`이 아니라 `0`입니다. Swift에서 배열의 인덱스는 항상 `0`부터 시작합니다.

첨자 문법은 주어진 인덱스에 위치한 값을 바꾸는 데 사용할 수도 있습니다.

```swift
shoppingList[0] = "Six eggs"
// 목록의 첫 번째 아이템은 이제 "Eggs"가 아닌 "Six eggs"입니다.
```

첨자 문법을 사용할 때는 지정하는 인덱스가 항상 유효해야 합니다. 예를 들어, 배열의 끝에 원소를 추가하기 위해 `shoppingList[shoppingList.count] = "Salt"라고 적는다면 런타임 오류가 발생합니다.

첨자 문법으로 특정 범위의 값들을 한 번에 바꿀 수도 있습니다. 심지어 바꾸려는 범위와 바꾸는 값들의 길이가 달라도 가능합니다. 다음 예시에서는 `"Chocolate Spread"`, `"Cheese"`, `"Butter"`를 `"Bananas"`, `"Apples"`로 바꾸고 있습니다.

```swift
shoppingList[4...6] = ["Bananas", "Apples"]
// shoppingList는 이제 6개의 원소를 가집니다.
```

특정 인덱스에 원소를 삽입하려면 배열이 가진 `insert(_:at:)` 메서드를 호출하세요.

```swift
shoppingList.insert("Maple Syrup", at: 0)
// shoppingList는 이제 7개의 원소를 가집니다.
// "Maple Syrup"은 이제 목록의 첫 번쨰 원소가 됩니다.
```

`insert(_:at:)` 메서드가 `"Maple Syrup"`이라는 값을 가지는 새로운 원소를, 인덱스가 `0`으로 지정됨에 따라, 쇼핑 목록의 맨 처음에 삽입합니다.

배열에서 원소를 제거할 때는 `remove(at:)` 메서드를 사용하면 됩니다. 이 메서드는 특정 인덱스에 위치한 원소를 지우고 그 원소를 반환합니다: (물론, 필요 없다면 반환된 값은 무시할 수 있습니다.)

```swift
let mapleSyrup = shoppingList.remove(at: 0)
// 인덱스 0에 있던 원소가 제거됩니다.
// shoppingList는 이제 Maple Syrup이 빠져 6개의 원소를 가집니다.
// mapleSyrup 상수는 제거된 "Maple Syrup" 문자열과 같습니다.
```

> **참고**
> 
> 배열의 범위를 벗어나는 인덱스를 참조하려고 하면 런타임 오류가 발생합니다. 인덱스를 사용하기 전에 `count` 프로퍼티를 사용하여 그 인덱스가 유효한지 검사할 수 있습니다. 인덱스가 0부터 시작하므로 최대 유효 인덱스는 `count - 1`입니다. `count`가 `0`일 때는(즉, 배열이 비어 있다면) 유효한 인덱스가 없습니다.

원소가 제거되어도 배열은 내부에 공백이 없도록 유지되므로 인덱스 `0`에 위치한 값은 다시 `"Six eggs"`가 됩니다.

```swift
firstItem = shoppingList[0]
// firstItem은 이제 "Six eggs"와 같습니다.
```

배열의 마지막 원소를 제거하고 싶다면 `remove(at:)` 메서드를 사용하여 `count` 프로퍼티를 요청하지 말고, `removeLast()` 메서드를 사용하세요. `remove(at:)` 메서드와 마찬가지로 `removeLast()` 또한 제거된 원소를 반환합니다.

```swift
let apples = shoppingList.removeLast()
// 배열의 마지막 원소가 제거됩니다.
// shoppingList는 이제 apples가 빠져 5개의 원소를 가집니다.
// apples 상수는 제거된 "Apples" 문자열과 같습니다.
```

### 배열 반복

`for`-`in` 반복문으로 배열의 모든 값들을 반복할 수 있습니다.

```swift
for item in shoppingList {
    print(item)
}
// Six eggs
// Mik
// Flour
// Baking Powder
// Bananas
```

원소 각각의 값뿐만 아니라 정수 인덱스까지 필요하다면 반복할 때 `enumerated()` 메서드를 사용하세요. 각각의 원소에 대해 `enumerated()` 메서드는 정수와 원소의 값으로 이루어진 튜플을 반환합니다. 정수는 `0`부터 시작하여 원소마다 하나씩 증가합니다. 배열 전체를 반복한다면, 이 정수들은 원소의 인덱스들과 같게 됩니다. 튜플을 임시 상수나 변수로 분해할 수도 있습니다.

```swift
for (index, value) in shoppingList.enumerated() {
    print("Item \(index + 1): \(value)")
}
// Item 1: Six eggs
// Item 2: Milk
// Item 3: Flour
// Item 4: Baking Powder
// Item 5: Bananas
```

`for`-`in` 반복문에 대해서는 [For-in 반복문](control-flow.md#for-in-반복문)을 참고하세요.

## 집합

**집합**은 같은 자료형의 서로 다른 값들을 정해진 순서 없이 컬렉션에 저장합니다. 원소들의 순서가 중요하지 않거나 원소들이 오직 한 번씩만 등장하는 상황이라면 배열 대신 집합을 사용할 수 있습니다.

> **참고**
> 
> Swift의 `Set` 자료형은 Foundation의 `NSSet` 클래스와 연결됩니다.
> 
> Foundation이나 Cocoa와 함께 `Set`을 사용하는 것에 관한 자세한 정보는 [`Set`과 `NSSet`의 연결(영문)](https://developer.apple.com/documentation/swift/set#2845530)을 참고하세요.

### 집합형의 해시 값

값들을 집합에 저장하기 위해서는 해싱이 가능해야 합니다. 즉, 값들의 자료형마다 해시 값을 계산하는 방법이 있어야 합니다. 해시 값은 동등한 모든 객체에 대해 동일한 `Int` 값을 말합니다. `a == b`라면 `a`와 `b`는 같은 해시 값을 가져야 합니다.

Swift의 모든 기초 자료형(`String`, `Int`, `Double`, `Bool` 등)은 기본적으로 해싱이 가능합니다. 이들이 집합의 값이나 딕셔너리의 키에 사용될 수 있습니다. 연관 값이 없는 열거형 값([열거형](enumerations.md)에성 설명)들도 기본으로 해싱이 가능합니다.

> **참고**
> 
> 직접 정의한 자료형도 집합의 값이나 딕셔너리의 키의 자료형으로 사용할 수 있습니다. 자료형이 Swift의 표준 라이브러리에서 정하는 `Hashable` 프로토콜을 따르도록 하세요. `hash(into:)` 메서드를 구현하는 자세한 방법은 [해시 가능(영문)](https://developer.apple.com/documentation/swift/hashable)을 참고하세요. 프로토콜을 따르도록 하는 방법은 [프로토콜](protocols.md)을 참고하세요.







wip...!!