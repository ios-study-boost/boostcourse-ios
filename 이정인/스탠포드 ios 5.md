# [스탠포드] 5



## 예외 처리

```swift
func save() throws
do {
	try context.save() 
}catch let error {
throw error 
}

```



### NSError

`try!`

`try?`

에러가 발생하면 값을 옵셔널로 변환하여 리턴해줌





## Any

어느 타입이든지 될 수 있음

하위 호환 API를 쓸 때는 제외하고 안 쓸 예정



- 어케 쓰나요 

  as?를 사용하여 변환 

  ```swift
  if let foo = unknown as? MyType {
  }
  ```





## 타입 캐스팅

```swift
let vc: UIViewController = ConcentrationViewController()

if let cvc = vc as? ConcentrationViewController {
cvc.flipCard(...) // this is okay 
}//하위호환 변환 (다운캐스팅)
```



## 쫌쫌따리 클래스들

- NSObject
  - 오브젝트 c 클래스는 반드시 상속 받아야 하는 것
- NSNumber
  - 숫자를 넘기고 싶을때
  - swift와 자동으로 연결됨 
- Date
  - 정밀한 시간으로 측정해서 가져오기 좋음

- Data
  - 데이터 처리할때





## View(MVC에서)

- 뷰
- 계층적 구조



### 뷰 코드로 추가하기

`func addSubView(_ view:UIView) `:

컨테이너한테

`func removeFromSuperview()`:

삭제될 뷰한테

### 뷰 초기화

`init(frame: CGReat)`

`init(coder: NSCoder)`

```swift
func setup() { ... }
override init(frame: CGRect) { // a designated initializer 
  super.init(frame: frame)
setup() // might have to be before 
  super.init }
requiredinit?(coderaDecoder:NSCoder){ //arequired,failableinitializer
super.init(coder: aDecoder)
setup()
}
```

`awakeFromNib() `



### 2차원 드로잉 시스템 (코어 그래픽스)

- CGFloat

  부동 소수점 좌표를 나타내는 기본 타입

- CGPoint

- CGSize

- CGRect

  

### 좌표 체계

(0,0)  ➡️

⬇️

- point != pixel
- frame: CGReat 슈퍼뷰 중심
- center: CGReat 슈퍼뷰 중심
- bounds: CGReat 
  - 어디를 그리고 있는지





### Custom Views

1. UIGraphicsGetCurrentContext() 컨텍스트 얻기

2. Path 만들기

   `let path = UIBezierPath()`

3. 그리기 속성 세팅

4. 선 그리거나 채움 

```swift
let path = UIBezierPath()
path.move(to: CGPoint(80, 50)) path.addLine(to: CGPoint(140, 150)) path.addLine(to: CGPoint(10, 150)) 
path.close() 

UIColor.green.setFill() UIColor.red.setStroke() path.linewidth = 3.0 path.fill()	
```



- addClip()
  - 처음 그린 드로잉 안에 다 들어감 
  - 처음 그린 드로잉을 넘어가면 다 무시됨





##  Drawing Text







## 폰트

선호 폰트 카테고리에서  고르기

폰트 크기는 가변적 

커스텀했을때는 자동적으로 폰트 크기가 바뀌지 않으므로 UIFontMetrics 를 통해 설정해줘야함





## 이미지 그리기

### 이미지 가져오기 

- asset	
  - 옵셔널





## bound가 변경 되었을때

예) 기기 회전 

UIcontentMode 사용





## 서브뷰에서 bound 변경

layoutSubView 사용하면 돌릴 수 있음 

오토레이아웃 쓰지 않았을때만 



