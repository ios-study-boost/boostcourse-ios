#### 구조체와 클래스의 차이

1. 구조체는 상속성 X

2. 구조체 - Value Type 클래스 - reference Type

   Value Type( Array, Int, String , Dic )

   인자로 보내거나 배열에 넣거나 다른 변수에 할당해도 **복사** 된다

   * COW ( Copy on Write )

     swift에서 항상 복사하는 것이 아니라 내용을 **수정했을때만 실제로 복사하는 방식**을 채택



#### Memory Management

Automatic Reference Counting (ARC)

Reference Type은 힙에 저장된다

참조타입에 포인터를 만들때마다 ARC에서 Count += 1  사라질때마다 Count -= 1

카운터 == 0 --> 힙에서 삭제

IBOutlet에서 Weak - Weak의 경우 ARC에서 Count에 포함하지 않는다 

즉, Weak 포인터로 연결된 프로퍼티만 남게되면 힙에서 삭제한다 -> weak는 Optional 포인터임

Strong -> 포인터가 가리키고 있는한 힙에  저장되 있다



