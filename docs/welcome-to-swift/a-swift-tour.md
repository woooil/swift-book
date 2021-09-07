---
layout: default
title: Swift 둘러보기
description: A Swift Tour
parent: 환영합니다
nav_order: 2
---

# Swift 둘러보기

전통적으로, 새로운 언어를 배우는 과정은 "Hello, world!"라는 문구를 화면에 출력해보는 것으로 시작하곤 합니다. Swift에서는 다음과 같이 한 줄이면 됩니다.

```swift
print("Hello, world!")
// "Hello, world!"를 출력한다.
```

C나 Objective-C로 코드를 작성해본 경험이 있다면, 이런 문법은 이미 익숙할 것입니다. Swift에서는 이 코드 자체가 하나의 온전한 프로그램입니다. 입력/출력이나 문자열 처리와 같은 기능을 사용하기 위해 별도의 라이브러리를 불러들이지 않아도 됩니다. 전역으로 작성된 코드가 프로그램의 시작 지점으로 사용되니 `main()` 함수도 필요 없습니다. 문장이 끝날 때마다 세미콜론을 적지 않아도 됩니다.

이 장을 통해 다양한 프로그래밍 작업이 어떻게 수행되는지 둘러보세요. Swift를 시작하는 데 필요한 정보를 충분히 얻게 될 것입니다. 이해가 가지 않는 부분이 있어도 걱정하지 마세요. 여기 둘러보기에서 소개된 모든 내용은 책의 나머지 부분이 자세히 설명해줍니다.

> **참고**
>
> 이 장은 Xcode에서 playground로 열었을 때 가장 잘 즐길 수 있습니다. Playground에서 코드들을 마음껏 수정하고 그 결과를 바로 확인해보세요.
>
> [**Playground 다운로드\(영문\)**](https://docs.swift.org/swift-book/GuidedTour/GuidedTour.playground.zip)

## 간단한 값

`let`을 사용하여 상수를 만들고, `var`를 사용하여 변수를 만드세요. 상수의 값은 컴파일할 때 알려줄 필요는 없지만, 어디선가 정확히 한 번 할당해야 합니다. 처음 한 번만 설정하고 여러 번 재사용하는 값에 이름을 붙여 상수로 사용하세요.

```swift
var myVariable = 42
myVariable = 50
let myConstant = 42
```

상수나 변수는 할당하려는 값과 그 자료형이 같아야 합니다. 그렇다고 항상 자료형을 명시해야 하는 것은 아닙니다. 상수나 변수를 생성할 때 값을 함께 전달하면, 컴파일러가 알아서 자료형을 추론합니다. 위의 예시에서는 컴파일러가 `myVariable`의 자료형을 초기 값과 같은 정수형이라고 추론합니다.

초기 값이 없거나 자료형을 추론하기에 불충분하다면, 변수 뒤에 콜론을 붙이고 자료형을 명시하세요.

```swift
let implicitInteger = 70
let implicitDouble = 70.0
let explicitDouble: Double = 70
```

> **도전**
>
> 명시적 자료형이 `Float`이고 값이 `4`인 상수를 만들어보세요.

값들은 절대 묵시적으로 다른 자료형으로 바뀌지 않습니다. 값의 자료형을 변환해야 한다면, 명시적으로 원하는 자료형의 인스턴스를 만드세요.

```swift
let label = "The width is "
let width = 94
let widthLabel = label + String(width)
```

> **도전**
>
> 마지막 줄에서 `String`으로 변환하는 부분만 지워보세요. 어떤 오류가 생기나요?

값을 더 간단하게 문자열에 포함할 수도 있습니다. 값을 괄호 안에 넣고 괄호 앞에 백슬래시\(`\`\)를 입력하세요. 예를 들면 이런 식입니다.

```swift
let apples = 3
let oranges = 5
let appleSummary = "I have \(apples) apples."
let fruitSummary = "I have \(apples + oranges) pieces of fruit."
```

> **도전**
>
> `\()`를 사용하여 문자열에 부동 소수점 계산을 포함하고, 인사말에 이름을 포함해보세요.

삼중 큰따옴표\(`"""`\)를 사용하면 여러 줄의 문자열을 작성할 수 있습니다. 닫는 따옴표의 들여쓰기와 일치하는 각 줄의 들여쓰기는 무시됩니다. 예를 들어:

```swift
let quotation = """
I said "I have \(apples) apples."
And then I said "I have \(apples + oranges) pieces of fruit."
"""
```

대괄호\(`[]`\)를 이용하여 배열과 딕셔너리를 생성하고, 대괄호 안에 인덱스나 키를 적어 각각의 원소들에 접근하세요. 마지막 원소 다음에 쉼표가 올 수도 있습니다.

```swift
var shoppingList = ["catfish", "water", "tulips"]
shoppingList[1] = "bottle of water"

var occupations = [
    "Malcolm": "Captain",
    "Kaylee": "Mechanic",
]
occupations["Jayne"] = "Public Relations"
```

배열에 원소를 추가하면 배열은 자동적으로 길어집니다.

```swift
shoppingList.append("blue paint")
print(shoppingList)
```

비어 있는 배열이나 딕셔너리를 생성하려면 이니셜라이저 문법을 사용하세요.

```swift
let emptyArray: [String] = []
let emptyDictionary: [String: Float] = [:]
```

자료형을 묵시해도 괜찮다면, 비어 있는 배열은 `[]`으로, 비어 있는 딕셔너리는 `[:]`로 표현할 수 있습니다. 예를 들어, 변수에 새로운 값을 할당하거나 함수로 인자를 전달할 때 그렇게 할 수 있겠지요.

```swift
shoppingList = []
occupations = [:]
```

## 제어 흐름

조건문에는 `if` 또는 `switch`를 사용하며, 반복문에는 `for`-`in`이나 `while`, `repeat`-`while`을 사용합니다. 조건에 해당하는 변수는 괄호로 감싸도 좋고, 감싸지 않아도 좋습니다. 대신 몸체는 항상 중괄호로 감싸야 합니다.

```swift
let individualScores = [75, 43, 103, 87, 12]
var teamScore = 0
for score in individualScores {
    if score > 50 {
        teamScore += 3
    } else {
        teamScore += 1
    }
}
print(teamScore)
// "11" 출력
```

`if` 구문의 조건문은 항상 불 표현식이어야 합니다. 즉, `if score { ... }`와 같은 코드는 묵시적으로 변수를 `0`과 비교하는 것이 아니라 오류를 일으킵니다.

다루는 값이 비어 있을 수도 있다면 `if`와 `let`을 함께 사용하세요. 그런 값들을 옵셔널이라고 합니다. 옵셔널 값은 실제 값을 가질 수도 있지만, 값이 없다면 없다는 의미의 `nil`을 가집니다. 값의 자료형 다음에 물음표\(`?`\)를 적어 그 값이 옵셔널임을 나타냅니다.

```swift
var optionalString: String? = "Hello"
print(optionalString == nil)
// "false" 출력

var optionalName: String? = "John Appleseed"
var greeting = "Hello!"
if let name = optionalName {
    greeting = "Hello, \(name)"
}
```

> **도전**
>
> `optionalName`을 `nil`로 바꿔보세요. 인사말이 어떻게 달라지나요? `else` 절을 추가해 `optionalName`이 `nil`일 때 해당하는 인사말을 설정해보세요.

옵셔널이 `nil`이라면 조건문이 `false`이므로 중괄호 내부의 코드는 생략됩니다. 옵셔널에 값이 들어 있다면 그 값은 밀봉되어 있던 상태에서 개봉되어 `let` 뒤에 적힌 상수에 할당됩니다. 이제 몸체 안에서 값을 사용할 수 있습니다.

옵셔널 값을 다루는 또 다른 방법으로는 `??` 연산자를 사용하여 기본 값을 설정하는 것이 있습니다. 옵셔널 값이 없다면 이 기본 값이 대신 사용되는 식입니다.

```swift
let nickname: String? = nil
let fullName: String = "John Appleseed"
let informalGreeting = "Hi \(nickname ?? fullName)"
```

스위치는 정수에 한정되지도, 동등 연산자에 한정되지도 않습니다. 모든 종류의 데이터는 물론, 다양한 비교 연산자까지 지원합니다.

```swift
let vegetable = "red pepper"
switch vegetable {
case "celery":
    print("Add some raisins and make ants on a log.")
case "cucumber", "watercress":
    print("That would make a good tea sandwich.")
case let x where x.hasSuffix("pepper"):
    print("Is it a spicy \(x)?")
default:
    print("Everything tastes good in soup.")
}
// "Is it a spicy red pepper?" 출력
```

> **도전**
>
> `default` 케이스를 지워보세요. 어떤 오류가 생기나요?

`let`을 이용하여 패턴과 일치하는 값을 상수로 어떻게 할당하고 있는지 확인해보세요.

일치하는 스위치 케이스 내부의 코드가 실행되고 나면 프로그램은 스위치 구문에서 빠져나옵니다. 다음 케이스로 이어지지 않으니 각각의 케이스가 끝나고 명시적으로 스위치 구문을 빠져나올 필요가 없습니다.

`for`-`in`을 사용하면 딕셔너리의 원소들에 대해 반복을 수행할 수 있습니다. 각각의 키-값 쌍을 이용하려면 이름을 설정하면 됩니다. 딕셔너리는 순서가 없는 컬렉션이기 때문에 키와 값들이 무작위로 등장합니다.

```swift
let interestingNumbers = [
    "Prime": [2, 3, 5, 7, 11, 13],
    "Fibonacci": [1, 1, 2, 3, 5, 8],
    "Square": [1, 4, 9, 16, 25],
]
var largest = 0
for (_, numbers) in interestingNumbers {
    for number in numbers {
        if number > largest {
            largest = number
        }
    }
}
print(largest)
// "25" 출력
```

> **도전**
>
> `_`을 변수 이름으로 바꾸고 어느 종류의 숫자가 가장 큰지 추적해보세요.

조건이 바뀔 때까지 코드를 반복하려면 `while`을 사용하세요. 반복문의 조건은 끝에도 올 수 있습니다. 그렇게 하면 반복문이 적어도 한 번은 실행되게 됩니다.

```swift
var n = 2
while n < 100 {
    n *= 2
}
print(n)
// Prints "128"

var m = 2
repeat {
    m *= 2
} while m < 100
print(m)
// "128" 출력
```

`..<`를 사용하면 일정 범위의 인덱스를 만들고 반복문 내에서 그 인덱스를 다룰 수 있습니다.

```swift
var total = 0
for i in 0..<4 {
    total += i
}
print(total)
// "6" 출력
```

`..<`으로 만든 범위에서는 오른쪽 끝 값이 제외되고, `...`으로 만든 범위에는 양쪽 끝 값이 모두 포함됩니다.

## 함수와 클로저

함수는 `func`를 사용하여 선언합니다. 함수를 호출할 때는 함수의 이름 뒤에 전달 인자들을 괄호로 묶어 적습니다. `->`를 사용하여 매개 변수 이름과 자료형을 함수의 반환형과 구분합니다.

```swift
func greet(person: String, day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet(person: "Bob", day: "Tuesday")
```

> **도전**
>
> `day` 매개 변수를 지워보세요. 다른 매개 변수를 추가해 인사말에 오늘의 점심 특선을 포함해보세요.

기본적으로 함수는 매개 변수 이름을 전달 인자의 레이블로 사용합니다. 원한다면, 별도의 전달 인자 레이블을 매개 변수 이름 앞에 적거나 `_`를 적어 전달 인자 레이블을 생략할 수도 있습니다.

```swift
func greet(_ person: String, on day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet("John", on: "Wednesday")
```

함수에서 여러 값들을 반환할 때처럼 혼합된 값들은 튜플로 만드세요. 튜플의 원소는 이름이나 숫자를 이용해 참조할 수 있습니다.

```swift
func calculateStatistics(scores: [Int]) -> (min: Int, max: Int, sum: Int) {
    var min = scores[0]
    var max = scores[0]
    var sum = 0

    for score in scores {
        if score > max {
            max = score
        } else if score < min {
            min = score
        }
        sum += score
    }

    return (min, max, sum)
}
let statistics = calculateStatistics(scores: [5, 3, 100, 3, 9])
print(statistics.sum)
// "120" 출력
print(statistics.2)
// "120" 출력
```

함수는 중첩될 수 있습니다. 또한 중첩된 함수는 외부 함수에서 선언된 변수에 접근할 수 있습니다. 함수를 중첩하면 길거나 복잡한 함수 내 코드가 정돈됩니다.

```swift
func returnFifteen() -> Int {
    var y = 10
    func add() {
        y += 5
    }
    add()
    return y
}
returnFifteen()
```

함수는 일급 자료형입니다. 따라서 함수가 또 다른 함수를 반환값으로 내보낼 수 있습니다.

```swift
func makeIncrementer() -> ((Int) -> Int) {
    func addOne(number: Int) -> Int {
        return 1 + number
    }
    return addOne
}
var increment = makeIncrementer()
increment(7)
```

함수는 또 다른 함수를 전달 인자로서 받을 수도 있습니다.

```swift
func hasAnyMatches(list: [Int], condition: (Int) -> Bool) -> Bool {
    for item in list {
        if condition(item) {
            return true
        }
    }
    return false
}
func lessThanTen(number: Int) -> Bool {
    return number < 10
}
var numbers = [20, 19, 7, 12]
hasAnyMatches(list: numbers, condition: lessThanTen)
```

재호출될 수 있는 코드 단위를 뜻하는 개념으로 클로저라는 것이 있습니다. 함수는 사실 클로저의 특수한 한 종류입니다. 클로저 내의 코드는 자신이 생성된 영역과 다른 영역에서 실행되더라도 생성될 당시 접근할 수 있었던 변수나 함수에까지 접근할 수 있습니다. 이미 살펴본 중첩 함수에서도 이것이 나타납니다. 클로저는 이름 없이 중괄호\(`{}`\)로만 감싸서 만들 수 있습니다. `in`을 사용하여 전달 인자와 반환형을 몸체와 구분하세요.

```swift
numbers.map({ (number: Int) -> Int in
    let result = 3 * number
    return result
})
```

> **도전**
>
> 모든 홀수에 대해 `0`을 출력하는 클로저를 작성해보세요.

클로저를 더 간단하게 작성할 수 있는 몇 가지 방법들이 있습니다. 위임에서의 콜백과 같이 클로저의 자료형을 이미 알고 있는 경우에는 매개 변수의 자료형이나 반환형을 생략할 수 있습니다. 문장이 하나뿐인 클로저는 그 문장의 값을 묵시적으로 반환합니다.

```swift
let mappedNumbers = numbers.map({ number in 3 * number })
print(mappedNumbers)
// "[60, 57, 21, 36]" 출력
```

이름 대신 숫자로도 매개 변수를 참조할 수 있습니다. 이런 방식은 매우 짧은 클로저를 쓸 때 특히 유용합니다. 함수의 마지막 전달 인자로 넘겨지는 클로저는 닫힌 괄호 바로 다음에 작성해도 됩니다. 클로저가 함수의 유일한 전달 인자라면 괄호를 아예 생략해도 됩니다.

```swift
let sortedNumbers = numbers.sorted { $0 > $1 }
print(sortedNumbers)
// Prints "[20, 19, 12, 7]"
```

## 객체와 클래스

클래스를 생성하려면 `class` 뒤에 클래스의 이름을 적으세요. 클래스에서의 프로퍼티 선언은 클래스 내부라는 점을 제외하고선 일반적인 상수나 변수 선언과 동일합니다. 메서드와 함수 선언도 같은 방법으로 작성합니다.

```swift
class Shape {
    var numberOfSides = 0
    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
```

> **도전**
>
> `let`을 사용하여 상수 프로퍼티를 만들고, 전달 인자를 받는 메서드를 하나 더 만들어보세요.

클래스의 인스턴스를 생성할 때는 클래스의 이름 뒤에 괄호를 붙이세요. 인스턴스의 프로퍼티와 메서드에 접근할 때는 점 표기법을 사용하세요.

```swift
var shape = Shape()
shape.numberOfSides = 7
var shapeDescription = shape.simpleDescription
```

이 `Shape` 클래스 버전은 중요한 부분을 하나 놓치고 있습니다. 바로 인스턴스 생성과 동시에 클래스를 설정해주는 이니셜라이저입니다. `init`으로 이니셜라이저를 생성하세요.

```swift
class NamedShape {
    var numberOfSides: Int = 0
    var name: String

    init(name: String) {
        self.name = name
    }

    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
```

`name` 프로퍼티와 이니셜라이저의 `name` 인자를 `self`를 사용하여 구분하고 있습니다. 이니셜라이저의 전달 인자들은 함수 호출에서와 같이 클래스의 인스턴스가 생성될 때 전달됩니다. 모든 프로퍼티는 할당된 값을 가지고 있어야 합니다. 즉, \(`numberOfSides`처럼\) 선언과 함께 할당하든지, \(`name`처럼\) 이니셜라이저를 통해 할당해야 합니다.

객체의 할당이 해제되기 전에 정리가 필요하다면 `deinit`으로 디이니셜라이저를 만드세요.

하위 클래스는 자신의 클래스 이름 뒤에 콜론과 함께 상위 클래스 이름을 붙여 선언합니다. 표준 최상위 클래스라는 것은 없으므로 필요에 따라 상위 클래스를 포함할 수도, 생략할 수도 있습니다.

상위 클래스에서 구현된 메서드를 하위 클래스에서 재정의할 때는 `overriede`를 함께 적습니다. `override` 없이 실수로 메서드를 재정의하면 컴파일러가 오류로 판단합니다. 컴파일러는 또한 메서드에 `override`가 명시되어 있음에도 실제로는 상위 클래스의 메서드를 재정의하지 않는 경우까지 확인합니다.

```swift
class Square: NamedShape {
    var sideLength: Double

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 4
    }

    func area() -> Double {
        return sideLength * sideLength
    }

    override func simpleDescription() -> String {
        return "A square with sides of length \(sideLength)."
    }
}
let test = Square(sideLength: 5.2, name: "my test square")
test.area()
test.simpleDescription()
```

> **도전**
>
> 이름이 `Circle`인 `NamedShape`의 하위 클래스를 하나 만들고 그 이니셜라이저가 반지름과 이름을 인자로 받도록 해보세요. `Circle` 클래스에서 `area()`와 `simpleDescription()` 메서드를 구현해보세요.

프로퍼티는 단순히 값을 저장할 뿐만 아니라 게터와 세터를 가질 수도 있습니다.

```swift
class EquilateralTriangle: NamedShape {
    var sideLength: Double = 0.0

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 3
    }

    var perimeter: Double {
        get {
            return 3.0 * sideLength
        }
        set {
            sideLength = newValue / 3.0
        }
    }

    override func simpleDescription() -> String {
        return "An equilateral triangle with sides of length \(sideLength)."
    }
}
var triangle = EquilateralTriangle(sideLength: 3.1, name: "a triangle")
print(triangle.perimeter)
// "9.3" 출력
triangle.perimeter = 9.9
print(triangle.sideLength)
// "3.3000000000000003" 출력
```

`perimeter`의 세터 내에서 새로운 값은 `newValue`라는 묵시적 이름으로 사용됩니다. `set` 뒤에 괄호를 붙여 명시적 이름을 적어줄 수도 있습니다.

`EquilateralTriangle`의 이니셜라이저는 세 가지 단계로 이루어집니다.

1. 하위 클래스가 선언한 프로퍼티의 값 설정
2. 상위 클래스의 이니셜라이저 호출
3. 상위 클래스에 의해 정의된 프로퍼티의 값 변경. 메서드나 게터, 세터를 사용하는 다른 설정 작업들도 이 시점에 진행될 수 있습니다.

프로퍼티를 가지고 계산할 필요는 없지만 프로퍼티에 새로운 값이 설정된 전후로 어떤 코드를 실행하고 싶다면, `willSet`과 `didSet`을 사용하세요. 작성된 코드는 초기화를 제외한 값이 변하는 순간마다 실행됩니다. 예를 들어, 아래 클래스는 삼각형의 한 변의 길이가 항상 사각형의 한 변의 길이와 같은 상태로 유지됩니다.

```swift
class TriangleAndSquare {
    var triangle: EquilateralTriangle {
        willSet {
            square.sideLength = newValue.sideLength
        }
    }
    var square: Square {
        willSet {
            triangle.sideLength = newValue.sideLength
        }
    }
    init(size: Double, name: String) {
        square = Square(sideLength: size, name: name)
        triangle = EquilateralTriangle(sideLength: size, name: name)
    }
}
var triangleAndSquare = TriangleAndSquare(size: 10, name: "another test shape")
print(triangleAndSquare.square.sideLength)
// "10.0" 출력
print(triangleAndSquare.triangle.sideLength)
// "10.0" 출력
triangleAndSquare.square = Square(sideLength: 50, name: "larger square")
print(triangleAndSquare.triangle.sideLength)
// "50.0" 출력
```

옵셔널 값을 다룰 때는 메서드나 프로퍼티, 첨자와 같은 연산 앞에 `?`를 붙일 수 있습니다. `?` 앞의 값이 `nil`이라면 `?` 뒤의 모든 부분은 무시되며 전체 표현식의 값이 `nil`이 됩니다. 그렇지 않다면 옵셔널 값이 개봉되고 `?` 뒤의 부분은 개봉된 값에 대해 수행됩니다. 이 두 가지 경우 모두, 전체 표현식의 값은 옵셔널 값입니다.

```swift
let optionalSquare: Square? = Square(sideLength: 2.5, name: "optional square")
let sideLength = optionalSquare?.sideLength
```

## 열거형과 구조체

`enum`을 사용하여 열거형을 생성하세요. 클래스를 포함한 모든 명명 자료형들과 마찬가지로 열거형도 자신과 연관된 메서드를 가질 수 있습니다.

```swift
enum Rank: Int {
    case ace = 1
    case two, three, four, five, six, seven, eight, nine, ten
    case jack, queen, king

    func simpleDescription() -> String {
        switch self {
        case .ace:
            return "ace"
        case .jack:
            return "jack"
        case .queen:
            return "queen"
        case .king:
            return "king"
        default:
            return String(self.rawValue)
        }
    }
}
let ace = Rank.ace
let aceRawValue = ace.rawValue
```

> **도전**
>
> 두 `Rank` 값을 그들의 원시 값을 사용하여 비교하는 함수를 작성해보세요.

기본적으로 Swift는 원시 값을 `0`부터 `1`씩 키워가면서 할당합니다. 명시적으로 값을 특정해주면 이런 기본값을 바꿀 수 있습니다. 위의 예시에서 `ace`는 명시적으로 원시 값 `1`을 가지며, 나머지 원시 값들도 그에 맞춰 차례대로 할당됩니다. 문자열이나 부동 소수점 수를 열거형의 원시 값으로 사용해도 됩니다. 열거형 케이스의 원시 값에 접근할 때는 `rawValue` 프로퍼티를 사용하세요.

특정 원시 값의 열거형 인스턴스를 만들 때는 `init?(rawValue:)`를 사용하세요. 일치하는 원시 값에 맞는 열거형 케이스를 반환하거나 일치하는 `Rank`가 없을 경우 `nil`을 반환합니다.

```swift
if let convertedRank = Rank(rawValue: 3) {
    let threeDescription = convertedRank.simpleDescription()
}
```

열거형의 케이스 값들은 원시 값을 작성하는 또 다른 방법에 불과한 것이 아니라, 실제 값입니다. 실제로 의미 있는 원시 값들이 없다면 굳이 명시하지 않아도 됩니다.

```swift
enum Suit {
    case spades, hearts, diamonds, clubs

    func simpleDescription() -> String {
        switch self {
        case .spades:
            return "spades"
        case .hearts:
            return "hearts"
        case .diamonds:
            return "diamonds"
        case .clubs:
            return "clubs"
        }
    }
}
let hearts = Suit.hearts
let heartsDescription = hearts.simpleDescription()
```

> **도전**
>
> `Suit`에 `color()` 메서드를 추가해 스페이드와 클럽에 대해서는 "black"을, 하트와 다이아몬드에 대해서는 "red"를 반환하도록 해보세요.

위에서 보인 열거형의 `hearts` 케이스를 참조하는 방법 두 가지를 살펴보세요. `hearts` 상수에 값을 할당할 때는 상수의 자료형이 명시되어 있지 않으므로 열거형 케이스 `Suit.hearts`의 전체 이름을 적어 참조합니다. 스위치 안에서는 `self`의 값이 이미 알려져 있기 때문에 열거형 케이스가 축약형인 `.hearts`로 적혀 참조됩니다. 값의 자료형이 알려져 있는 경우라면 언제나 축약형을 사용할 수 있습니다.

열거형에 원시 값이 지정되어 있다면 그 값들은 선언될 때 결정됩니다. 즉, 특정 열거형 케이스의 모든 인스턴스는 항상 같은 원시 값을 가집니다. 대신 열거형 케이스에 대한 또 다른 선택지로, 해당 케이스와 연관된 값을 지정할 수 있습니다. 이 값들은 인스턴스가 생성될 때 결정되며, 따라서 인스턴스마다 달라도 됩니다. 이 연관 값들이 열거형 케이스 인스턴스의 저장 프로퍼티처럼 행동한다고 받아들여도 좋습니다. 예를 들어, 서버로부터 일출, 일몰 시간을 요청하는 경우를 생각해봅시다. 서버는 요청한 정보로써 응답하거나, 무언가 잘못되었다는 안내로 응답할 것입니다.

```swift
enum ServerResponse {
    case result(String, String)
    case failure(String)
}

let success = ServerResponse.result("6:00 am", "8:09 pm")
let failure = ServerResponse.failure("Out of cheese.")

switch success {
case let .result(sunrise, sunset):
    print("Sunrise is at \(sunrise) and sunset is at \(sunset).")
case let .failure(message):
    print("Failure...  \(message)")
}
// "Sunrise is at 6:00 am and sunset is at 8:09 pm." 출력
```

> **도전**
>
> `ServerResponse`와 스위치에 세 번째 케이스를 추가해보세요.

스위치 케이스와 일치하는 값을 찾고 `ServerResponse` 값에서 일출, 일몰 시간을 추출하는 과정을 확인해보세요.

구조체를 만들 때는 `struct`를 사용하세요. 메서드와 이니셜라이저처럼 구조체 또한 클래스에서와 동일한 동작을 상당수 지원합니다. 구조체와 클래스의 가장 중요한 차이점은, 코드 내에서 구조체가 전달될 때는 항상 복사되지만 클래스는 참조로 전달된다는 점입니다.

```swift
struct Card {
    var rank: Rank
    var suit: Suit
    func simpleDescription() -> String {
        return "The \(rank.simpleDescription()) of \(suit.simpleDescription())"
    }
}
let threeOfSpades = Card(rank: .three, suit: .spades)
let threeOfSpadesDescription = threeOfSpades.simpleDescription()
```

> **도전**
>
> 카드의 전체 덱을 포함하고 있는 배열을 반환하는 함수를 작성해보세요. 각각의 카드는 `rank`와 `suit`의 조합으로 구성되어야 합니다.

## 프로토콜과 확장

프로토콜을 선언할 때는 `protocol`을 사용하세요.

```swift
protocol ExampleProtocol {
    var simpleDescription: String { get }
    mutating func adjust()
}
```

클래스와 열거형, 구조체 모두 프로토콜을 채택할 수 있습니다.

```swift
class SimpleClass: ExampleProtocol {
    var simpleDescription: String = "A very simple class."
    var anotherProperty: Int = 69105
    func adjust() {
        simpleDescription += "  Now 100% adjusted."
    }
}
var a = SimpleClass()
a.adjust()
let aDescription = a.simpleDescription

struct SimpleStructure: ExampleProtocol {
    var simpleDescription: String = "A simple structure"
    mutating func adjust() {
        simpleDescription += " (adjusted)"
    }
}
var b = SimpleStructure()
b.adjust()
let bDescription = b.simpleDescription
```

> **도전**
>
> `ExampleProtocol`에 다른 요구 사항을 추가해보세요. `SimpleClass`와 `SimpleStructure`가 계속 프로토콜을 준수하기 위해서는 어떤 변화를 주어야 하나요?

`SimpleStructure`의 선언 내부에서, 메서드가 구조체를 수정하고 있음을 나타내기 위해 `mutating` 키워드를 사용했습니다. 반면 클래스의 메서드는 항상 클래스를 수정할 수 있습니다. 즉, `SimpleClass`의 선언에서는 `mutating`을 표시할 필요가 없습니다.

이미 존재하는 자료형에 새로운 메서드나 계산 프로퍼티와 같은 기능을 추가하려면 `extension`을 사용하세요. 다른 곳에서 선언된 자료형이나 라이브러리, 프레임워크에서 불러온 자료형이 프로토콜을 준수하도록 하는 데에도 확장을 사용할 수 있습니다.

```swift
extension Int: ExampleProtocol {
    var simpleDescription: String {
        return "The number \(self)"
    }
    mutating func adjust() {
        self += 42
    }
}
print(7.simpleDescription)
// "The number 7" 출력
```

> **도전**
>
> `Double` 형에 `absoluteValue` 프로퍼티를 추가하는 확장을 작성해보세요.

프로토콜의 이름을 다른 명명 자료형들처럼 사용할 수도 있습니다. 예를 들어 서로 자료형은 다르지만 모두 동일한 프로토콜을 따르는 객체들의 집합을 생성하는 경우가 있습니다. 자료형이 프로토콜인 값들을 다룰 때 프로토콜 정의 외부에 있는 메서드는 사용할 수 없습니다.

```swift
let protocolValue: ExampleProtocol = a
print(protocolValue.simpleDescription)
// "A very simple class.  Now 100% adjusted." 출력
// print(protocolValue.anotherProperty) // 주석을 해제하여 오류를 확인해보세요.
```

변수 `protocolValue`가 `SimpleClass`의 런타임 자료형을 가지고 있긴 하지만 컴파일러는 `ExampleProtocol`의 자료형으로 취급합니다. 따라서 클래스가 구현한 메서드나 프로퍼티에 실수로 접근하거나 프로토콜 준수에 접근할 일이 없습니다.

## 오류 처리

오류는 `Error` 프로토콜을 채택한 아무 자료형이나 사용하여 표현합니다.

```swift
enum PrinterError: Error {
    case outOfPaper
    case noToner
    case onFire
}
```

오류를 던지는 데 `throw`를 사용하고 오류를 던질 수 있는 함수를 표시하는 데 `throws`를 사용하세요. 함수에서 오류를 던지면 함수는 즉시 반환되고 함수를 호출한 코드가 오류를 처리합니다.

```swift
func send(job: Int, toPrinter printerName: String) throws -> String {
    if printerName == "Never Has Toner" {
        throw PrinterError.noToner
    }
    return "Job sent"
}
```

오류는 몇 가지 방법으로 처리할 수 있습니다. 그 중 하나는 `do-catch`를 사용하는 것입니다. `do` 내부에서, 오류를 던지는 코드를 `try` 다음에 작성하세요. `catch` 내부에서는 오류의 이름을 특별히 지정하지 않는 이상 자동적으로 `error`라는 이름으로 오류가 주어집니다.

```swift
do {
    let printerResponse = try send(job: 1040, toPrinter: "Bi Sheng")
    print(printerResponse)
} catch {
    print(error)
}
// "Job sent" 출력
```

> **도전**
>
> 프린터 이름을 "`Never Has Toner`"로 바꾸어 `send(job:toPrinter:)` 함수가 오류를 던지도록 해보세요.

특정 오류를 처리하도록 `catch` 단위를 여러 개 만들 수도 있습니다. 스위치에서 `case` 다음에 작성한 것처럼, `catch` 다음에도 패턴을 작성할 수 있습니다.

```swift
do {
    let printerResponse = try send(job: 1440, toPrinter: "Gutenberg")
    print(printerResponse)
} catch PrinterError.onFire {
    print("I'll just put this over here, with the rest of the fire.")
} catch let printerError as PrinterError {
    print("Printer error: \(printerError).")
} catch {
    print(error)
}
// "Job sent" 출력
```

> **도전**
>
> `do` 내부에서 오류를 처리하는 코드를 추가해보세요. 오류가 첫 번째 `catch` 단위에서 처리되려면 어떤 오류를 던져야 하나요? 마찬가지로 두 번째나 세 번째 `catch`에는 어떤 오류가 필요한가요?

오류를 처리하는 또 다른 방법은 `try?`를 사용하여 결과를 옵셔널로 변환하는 것입니다. 함수가 오류를 던진다면, 특정 오류는 버려지고 결과값이 `nil`이 됩니다. 그렇지 않다면 결과값은 함수가 반환한 값을 밀봉한 옵셔널이 됩니다.

```swift
let printerSuccess = try? send(job: 1884, toPrinter: "Mergenthaler")
let printerFailure = try? send(job: 1885, toPrinter: "Never Has Toner")
```

함수 내의 다른 모든 코드가 실행되고 함수가 반환되기 직전에 실행되는 코드 단위에는 `defer`를 사용하세요. 그 코드는 함수가 오류를 던지든 말든 반드시 실행됩니다. 설정 코드와 정돈 코드가 서로 다른 시간에 실행되어야 하더라도 둘을 나란히 작성하는 데 `defer`를 사용할 수 있습니다.

```swift
var fridgeIsOpen = false
let fridgeContent = ["milk", "eggs", "leftovers"]

func fridgeContains(_ food: String) -> Bool {
    fridgeIsOpen = true
    defer {
        fridgeIsOpen = false
    }

    let result = fridgeContent.contains(food)
    return result
}
fridgeContains("banana")
print(fridgeIsOpen)
// "false" 출력
```

## 제네릭

제네릭 함수나 자료형을 만들기 위해서는 부등호 안에 이름을 적으세요.

```swift
func makeArray<Item>(repeating item: Item, numberOfTimes: Int) -> [Item] {
    var result: [Item] = []
    for _ in 0..<numberOfTimes {
        result.append(item)
    }
    return result
}
makeArray(repeating: "knock", numberOfTimes: 4)
```

클래스나 열거형, 구조체는 물론 함수나 메서드까지 제네릭 형태로 만들 수 있습니다.

```swift
// Swift 표준 라이브러리의 옵셔널 타입을 재구현
enum OptionalValue<Wrapped> {
    case none
    case some(Wrapped)
}
var possibleInteger: OptionalValue<Int> = .none
possibleInteger = .some(100)
```

요구 사항 목록을 특정하려면 몸체 앞에 `where`를 적으세요. 예를 들면 자료형이 프로토콜을 구현하도록 하거나, 두 자료형이 같도록 하거나, 클래스가 특정 상위 클래스를 가지도록 하려면 다음처럼 표시할 수 있습니다.

```swift
func anyCommonElements<T: Sequence, U: Sequence>(_ lhs: T, _ rhs: U) -> Bool
    where T.Element: Equatable, T.Element == U.Element
{
    for lhsItem in lhs {
        for rhsItem in rhs {
            if lhsItem == rhsItem {
                return true
            }
        }
    }
    return false
}
anyCommonElements([1, 2, 3], [3])
```

> **도전**
>
> `anyCommonElements(_:_:)` 함수를 수정하여 두 `Sequence` 인스턴스가 공통으로 가지는 원소들의 배열을 반환하는 함수를 만들어보세요.

`<T: Equatable>`은 `<T> ... where T: Equatable`과 동일한 표현입니다.

