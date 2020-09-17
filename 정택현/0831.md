### Introduction to iOS 11, Xcode 9 and Swift 4

* Xcode

  * 도큐먼트 (⇧ + ⌘ + 0)

    Read Document, Check Overview

  * 네비게이션 바 (⌘ + 0 , 1 , 2 ,3 ~ 9)

    프로젝트 계층구조, 디버그 세션, 브레이크 포인트 등 

  * 유틸리티 바 (⌘ + ⌥ + 0 , 1 , 2 ,3 ~ 9)

    객체 속성, 아이덴티티 

    

* Property Oberserver

  ```swift
  var flipCount = 0 {        //속성이 설정될때마다 이안의 코드가 실행됨       
  	didSet{           
    	flipCountLabel.text = "Flip: \(flipCount)"       
     			 }   
  }
  ```



* Naming

  1. 모든 파라메터는 이름을 갖는다
  2. 함수 호출시 사용하는 이름, 코드 내부에서 사용하는 이름
  3. 이름은 영어처럼 읽히게 작성해야 한다 -> **flip card with emoji 👻 on button1**

  ```swift
  func flipCard(withEmoji emoji: String, on button: UIButton){
  		print("\(emoji)")
  }
  flipCard(withEmoji: "👻" ,on: UIButton)
  ```

  

