# [스탠포드] Swift를 활용한 iOS 11 앱 개발 



## 1. IOS의 층 구성

 	1. **Cocoa Touch**
     - UI layer, ex) slider, button ... 
 	2. Media
 	3. **Core Services**
 	4. Core Os





## 2. Demo

1. 프로젝트 생성

   - [new project] - [sing app view]
   - User Interface를 Storyboard로 해야 Main.storyboard 파일 생성됨

   

2. 내비게이터 정리

   - 사용하지 않는 Asset, LaunchScreen, AppDelegate 파일은 Supporting files 폴더 만들어 넣기
   -  Mainstoryboard -> UI 그래픽으로 구현

   

3. UI 만들기

- 유틸리티 상단에 + 누르고 객체 골라서 드래그
- 유틸리티 창에서 배경색, 글씨 크기 등 설정



4. ViewController

   - 카드를 뒤집기 위해 코드와 연결함 

   UIKit - 버튼, 슬라이등이 있는 프레임 워크 cocotouch

   ```swift
   class ViewController: UIViewController {
     //클래스명 : 슈퍼 클래스
   ```

   - mainstory board 와 ViewController 분할하여 띄우기

     - code 11 이상은 수동 옵션이 표시 되지 않음 ☹️ 
     - option+ 파일 클릭하면 Assistant Editor 창에서 열림

   - control + 드래그 하여 버튼을 ViewController에 연결

     - Action = call the method 선택 
     - outlet  = property
     - touchCard  method 생성
     - 인자를 sender로 설정
     - **Type button 으로 변경** 

     ``` swift
      @IBAction func touchCard(_ sender: UIButton)
     //어떤 버튼인지 표시| 함수 키워드 | 메소드 이름 | 인수이름 : 인수 
     //메소드 호출할 때 인수 이름 붙여야함 (외부 이름 : 내부 이름)
     ```

   - 카드 뒤집는 swift 함수 만들기

   - 클래스 인자 뭔지 모를때 option 눌러서 설명서 읽기

   - 복붙할 경우 선택 범위가 중첩됨 -> 오른쪽 버튼 눌러서 메소드 하나만 연결 되도록 지움 

   - 클릭 수 추척하는 인스턴스 변수(=property) 만들기 

     - 반드시 초기화 되어야 함

       - initialzier 이용하기 -> 상속 받아서 복잡함
       - 초기값 넣기 ex) var flipCard  = 0

       

   - didset (속성 감시자) : 속성 값이 변경될 때다 코드 블럭 실행

     ```swift
     var flipCount = 0{
             didSet{
                 flipCounterLabel.text = "Flips : \(flipCount)"
             }
         }
     ```

   - 여러개 선택하고 타입이 같으면 동시에 편집할 수 있음 

5. 코드 효율성 높이기 

   - 메소드 하나로 합치기
   - 배열을 만들어 카드를 만들고 해당 인덱스로 이모지 배열에서 값을 리턴한다.
   - ctrl + 드래그  후에 outlet collection (프로퍼티 배열)
   - 이름 바꾸고 싶을때 cmd + 클릭 -> rename 프로젝트 전체에 있는 것들을 한꺼번에 바꿀 수 있음
   - cardButton.index(Of:UIButton) 으로 인덱스 값을 찾을 수 있지만 옵셔널 값으로 넘어옴 
   - if-let 조건부 설정으로 충돌 방지 
   - MVC 로 업그레이드 할 수 있음