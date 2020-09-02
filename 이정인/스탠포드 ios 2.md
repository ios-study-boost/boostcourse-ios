# [스탠포드] Swift를 활용한 iOS 11 앱 개발 

## 1.MVC 

- Model 
  - What is your application about
  - UI와 독립
  - KVO , notification : 통신하여 연결
- Controller
  - How your Model is presented to ther user
  - UI User
  - 모델의 정보를 해석하고 구성해서 뷰에게 전달
- View
  - controller's minions
  - 컨트롤러가 모델과 통신해 UI에서 데이터를 가져와야할 때 필요함
  - 일반적인 객체들 예) 버튼..
  - View -> Controller
    - Target action  
    - delegate
      - Controller sets itself as the View's delegate
      - set via a protocol
    - data source
      - ex) table view 페이징처럼 범위 내의 데이터만 요청 

- 다른 MVC와 통신
  - controller는 다른 MVC를 View로 취급 





## 2. 모델 만들기



- 구조체

  - 값 타입  = 복사, 변경 가능
  - 인수가 있는 init이 자동으로 생김 

- 클래스

  - 참조 타입 = 복사해서 값 변경하면 원본 데이터도 변경됨
  - 모든 변수가 초기화 됐을때 인수가 없는 init 을 자동으로 가진다.

- 핵심 기능 (카드 선택)

  ```swift
  var indexOfOneAndOnlyFaceUpCard : Int? 
  func chooseCard(at index: Int){
          if !cards[index].isMatched{
              if let matchIndex = indexOfOneAndOnlyFaceUpCard, matchIndex != index{
                  //check if cards match
                  if cards[matchIndex].identifier == cards[index].identifier{
                      cards[matchIndex].isMatched = true
                      cards[index].isMatched = true
                  }
                  cards[index].isFaceUp = true
                  indexOfOneAndOnlyFaceUpCard = nil
              }else{
                  //either nocards or cards are face up
                  for flipDownIndex in cards.indices{
                      cards[flipDownIndex].isFaceUp = false
                  }
                  cards[index].isFaceUp = true
                  indexOfOneAndOnlyFaceUpCard = index
              }
          }
      }
  ```

  

- 카드를 선택했을 때 매칭된 상태가 아니라면 (한 개는 이미 선택해서 플립된 상태)
  1. 플립된 카드와 선택한 카드가 매칭 되는지 이미 플립된 카드를 선택한 건 아닌지 체크
  2. 매칭 되었으면 두 카드의 isMatched를 모두 true로 업데이트
  3. 현재 카드의 플립 상태 true로 업데이트
  4. indexOfOneAndOnlyFaceUpCard = nil (플립된 카드 없으니까)



- 아무 카드도 안 뒤집어져 있거나  indexOfOneAndOnlyFaceUpCard = nil 일때
  1. 다 뒤집음
  2. 현재 카드만 앞면 보이게 상태 업데이트
  3. indexOfOneAndOnlyFaceUpCard   = 현재 카드 인덱스











### 3. 스위프트 문법 새로 안 사실들

- for range
  - .. 마지막 포함 X
  - ... 마지막 포함
  - _ : ignore, 안 쓸 거니까 무시하라는 뜻

- lazy
  - 누가 사용하기 전까지 초기화 하지 않음
  - Did set 쓸 수 없음

- .count
  - 배열 데이터 갯수 세줌

- indices
  - return countable range



- arc4random_uniform
  - 랜덤 생성 (0~ Upper bound)
  - UInt32만 인자로 받을 수 있음 
    - UInt32(Int:) 이용
  - 0을 받을 수 없음

- ?? 
  - `emoji[card.identifier] ?? "?"`
  - nil이면 오른쪽 아니면 왼쪽