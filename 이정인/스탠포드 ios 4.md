# [스탠포드] Swift 프로그래밍 언어 - Part 2

## mutating

class 를 struct로 바꾸면 인스턴스 메소드에서 self 변수를 수정할 수 없음

mutating 키워드 필요

- 왜 struct에서만 필요?

  struct는 **값 타입**임 따라서 힙 내부에 존재하지 않기 때문에 구조체를 전달할 때 계속해서 복사됨  

  ➡️ 매번 전체를 복사하는 건 비효율적 

  효율성을 위해서 내용이 변경되었을때 (mutated)만 복제함 

  ➡️ **쓰기시 복사 (copy on write)**

  클래스는 전달될 때 힙 안에 있기 때문에 포인터만 전달함 

  

- 변수에 안 쓰는 이유?

  변수는 수정이 가능한지 아닌지가 이미 명시되어 있음 ex) private(set) var..

  계산 프로퍼티의 경우 get,set으로 수정 가능한지 판별할 수 있음 

   let일때는 수정할 수 없으므로 수정하고 싶다면 mutating 을 붙임



## 프로토콜

별도의 구현이 없는 메소드와 변수의 리스트 , **프로토콜은 타입이다**

- 블라인드 커뮤니케이션에서 유용함

  MVC 구조 

- @objc를 프로토콜 앞에 붙이면 스위프트 프로토콜이 아닌 오브젝티브 C의 프로토콜처럼 사용할 수 있음 (오브젝트 C에서는 프로토콜 내부의 메소드의 구현이 선택적임) 

  - IOS API가 오브젝트 C로 구현되었을때
  - 델리게이션의 경우 블라인드 형식의 뷰와 컨트롤러 사이의 커뮤니케이션에서 오브젝트 c 스타일 프로토콜을 사용함

- 선언

  ```swift
  protocol SomeProtocol:InheritedProtocol1, InheritedProtocol2{
  	var someProperty : int {get set}
  	func aMethod(arg1: Double, anotherArg: string )-> someType
    mutating func changeIt()
    init(arg: Type)
  }
  ```

  상속받을 수 있다. 상속 받았을 경우 부모 프로토콜들도 전부 구현해줘야함 

  구조체에 의해 구현되어서 값을 수정하는 함수가 있다면 `mutating` 키워드 필요함 

  - 만약 구조체에서 절대 구현되지 않을거라면 (클래스에서만 구현할 거라면) 안 붙여도 됨 대신 클래스만 받는 프로토콜임을 표시하기 위해서 `class` 키워드 필요 

    `protocol SomeProtocol:class,InheritedProtocol1..`

- 프로토콜 설정

  `struct someStruct: SomeProtocl,AnotherProtocol{}`

  다중 상속 가능 

  `init` 가 있고 클래스로 구현할 경우 `required ` 붙여야함 서브 클래스의 오버라이드 방지 

  ```swift
  class someClass : SuperClass,someProtocol{
    required init(..)
  }
  ```

- 익스텐션

  사용 가능

- 프로토콜을 타입에 맞게 쓰기 

  ```swift
  protocol Moveable {
       mutating func move(to point: CGPoint)
   }
   class Car : Moveable {
  func move(to point: CGPoint) { ... }
       func changeOil()
   }
  struct Shape : Moveable {
  mutating func move(to point: CGPoint) { ... } func draw()
  }
   let prius: Car = Car()
   let square: Shape = Shape()
  
  var thingToMove: Moveable = prius 
  thingToMove.move(to: ...) 
  thingToMove.changeOil()//error 
  
  ```

  ```swift
  var thingToMove: Moveable = prius thingToMove.move(to: ...) thingToMove.changeOil() thingToMove = square
  let thingsToMove: [Moveable] = [prius, square]
  func slide(slider: Moveable) {
  let positionToSlideTo = ... slider.move(to: positionToSlideTo)
  }
  slide(prius)
  slide(square)
  ```

  실행하면 각각의 클래스와 구조체에서 구현된 move(to:) 이 실행됨 swift 자체적으로 타입 추적 

  여러개 프로토콜을 묶어서 사용할 수도 있음 

  ```swift
  func slipAndSlide(x: Slippery & Moveable)
  slipAndSlide(prius)
  ```





## 델리게이션

프로토콜



## Hashable

Hashable프로토콜은 구분 가능한 해쉬 값을 가져야하고 다른 것과 동일한지 어떤지 비교해야 하므로 Equatable 프로토콜을 따름

```swift
//Deprecated
protocol Hashable : Equatable{
	var hashValue: Int{get}
}
```

근데 Deprecated돼서 hashValue 없어짐  자동으로 프로토콜 사항을 맞춰주긴하는데 

아래 사항 따라야함 

- For a `struct`, 모든 저장 프로퍼티는  `Hashable` 를 준수해야한다.
- For an `enum`,  모든 associated values `Hashable` 을 준수해야한다.. (associated 없으면 conformance 없어도 이미 `Hashable` 준수)

hash(into:)를 써서 프로토콜 사항을 커스터마이징 할 수 있음  

```swift
func hash(into hasher: inout Hasher) {
        hasher.combine(x)
        hasher.combine(y)
    }
```



```swift
protocol Equatable {
static func ==(lhs: Self, rhs: Self) -> Bool }
```



해시 가능하다  = 딕셔너리의 키가 될 수 있다.

딕셔너리는 제너릭 타입  : 값, 키 두개를 가짐 

```swift
Dictionary<Key:Hashable, Value>	
```

키가 해시 가능할 때만 구현된다는 뜻 (제너릭 타입으로 제한)





## 익스텐션 

프로토콜 메소드를 구현하고 싶을 때 활용할 수 있다.  프로토콜이나 상속 받는 프로토콜 내에 있는 메소드 뿐임 



## 다중 상속

collection들이 sequence 프로토콜을 상속 받아 동일한 기능 메소드들을 실행하듯이 (next, foreach, join ... ) 프로토콜을 다중 상속할 수 있는데 이때 메소드들은 부모 프로토콜 익스텐션에서 구현됨 (기본 구현)



## 프로토콜 사용의 장점

- 함수형 프로그래밍 

  기초 프레임워크들이 함수형 프로그래밍으로 만들어있음 (딕셔너리 ... )



## 문자열

문자열 구조체와 별개로 문자가 있음 

문자열은 문자로 구성하는 것이 아닌 유니코드로 구성

데이터로 언어를 나타냄

유니코드와 문자를 이어줄 필요가 있음 



문자열은 정수로 색인할 수 없음 

- String.Index

- startIndex, endIndex, idex(of:)

- index(String.Index, offsetBy: Int)

  - 4번째 문자 얻기 

    index(firstCharacterIndex, offsetBy: 3)

제네릭?



.components(separatedBy: “ “)

sepratedBy로 나눠진 문자열 (split)





## NSAttributedString

문자열 관련 클래스 

문자열의 모든 문자가 딕셔너리(폰트,컬러..)를 가지고 있음 

키는 문서에서 값은 그것의 타입과 관련이 있음 

`let attributes: [NSAttributedStringKey : Any] = [ `

Any 절대 쓰지 말것 enum으로 대체 가능

var 가변 변수 만들 수 없어 

string Nsstring 자동 연결됨



IBOutlet은 아울렛이 iOS에 설정될때 연결되므로 didSet을 호출할 수 있음





## Function Types

함수를 타입으로 사용할 수 있음 

타입을 쓸 수 있는 어느 곳이든 

`var operation: (Double) -> Double`



### 클로저

함수형 타입을 간단하게 쓰고 싶을때 

함수를 인자로 넘겨줌

인라인 함수

참조 타입 

func changeSign(operand: Double) -> Double { return -operand }

```swift
We could use it instead of sqrt ...
 var operation: (Double) -> Double
 operation = changeSign
 let result = operation(4.0) 
```

클로저로 변경

```swift
var operation: (Double) -> Double
operation = { (operand: Double) -> Double in return -operand }
let result = operation(4.0)
```

축약

```swift
var operation: (Double) -> Double
operation = { -$0 }
let result = operation(4.0)
```

#### map

```swift
let primes = [2.0, 3.0, 5.0, 7.0, 11.0]
let negativePrimes = primes.map({ -$0 }) // [-2.0, -3.0, -5.0, -7.0, -11.0]
let invertedPrimes = primes.map() { 1.0/$0 } // [0.5, 0.333, 0.2, etc.]
let primeStrings = primes.map { String($0) }
```

마지막 인자가 함수면 밖으로 뺄 수 있다 .

#### 속성 초기화 

속성을 원하는 대로 초기화해서 올바른 변수만 return 하면 됨



