# 다형성(Polymorphism)

#### 사전적 의미 : 같은 종의 생물에서 다양한 성질이 나타나는 현상 

#### Java : 클래스 형변환을 지원하는 것

	예시) 부모 - 자식관계 클래스에서 데이터 타입은 부모에서 선언, 인스턴스 생성은 자식클래스 하는 것.

```java
//A와 B클래스가 부모-자식 관계인 경우
A objRef = new B(); // 클래스 형변환(자동 형변환)
Animal animal = new Dog();
Animal animal = new Cat();
Animal animal = new Cow();
```

즉, 객체의 형변환은 상속관계에서만 가능하다는 것이다.

예제 코드와 함께 다형성이 특징살펴보자.

```java
package polymorphism;
import Inheritance.Circle;
import Inheritance.RectAngle;
import Inheritance.Shape;

public class PolymorphismExam {

	public static void main(String[] args) {
		//클래스 형변환(Upcasting)
		Shape shape = null;
		shape = new Shape();
		shape = new Circle(10, 10, 20); //Shape의 자식 클래스
		System.out.println(shape);
		shape = new RectAngle(10, 10, 20 , 50); //Shape의 자식클래스
		System.out.println(shape);
```

Shape의 디폴트 생성자에 shape가 아닌 자식 클래스의 Circle과 RectAngle로 초기화 시킬 수 있다.



### 그럼, 다형성은 왜 필요한걸까 ?

쉽게 생각해보자. 다형성이 지원되지 않는다면 dog 변수에는 dog만, cat 변수에는 cat만 할당할 수 있다. 하지만, 다형성으로 인해 부모 클래스의 animal 변수에는 dog, cat 등 여러 동물을 선언할 수 있다.

아래 코드를 살펴보자.

```
//animal이 부모 클래스, dog, horse, cat이 자식 클래스일 경우.
Animal animal = new dog();
Animal animal = new horse();
Animal animal = new cat();
```

이게 바로 JAVA에서 지원하는 자동형변환(Upcasting)이다. 반대인 강제형변환(Down casting)은 추후 살펴보자.



### 제약사항(자식에 새롭게 추가된 변수, 메소드는 접근 불가)

1.  메모리 구조 상 같은 객체의 상위 객체로만 접근가능하다.
2.  다형성 메커니즘 상 오버라이딩 한 메소드는 접근하여 호출 가능

```java
System.out.println(shape.getX());
//System.err.println(shape.getwidth()); 새로 추가된 메서드는 호출 불가
System.out.println(shape.getArea()); // 오버라이딩 메소드
```

이를 JVM머신 작동원리에 접목시켜 그림으로 알아보자.

![](C:\Users\kosta\AppData\Local\Temp\1535104874412.png)

Shape 클래스는 메모리 구조상 같은 객체인 자기 자신과, 상위 객체인 Object 클래스로만 접근가능하다.

(모든 클래스는 조상격인 Object클래스로부터 암시적인 상속을 받고 있다.) 

(* 참고 문서 : https://opentutorials.org/module/516/6241)



![](C:\Users\kosta\AppData\Local\Temp\1535105143033.png)

다음은 예외적인 상황이다. Circle Class는 Shape class의 riding() 메서드를 오버라이딩 하고 있다. 이럴 경우,

임시적으로 Shape 클래스뿐 아니라 Circle클래스도 탐색, 참조하게 된다. 



### DownCasting

#### 정의 : 새롭게 추가된 속성, 메소드를 접근 및 사용하고자 할 때, 형변환하고자 하는 (타입)으로 변환하는 것

코드로 살펴보자.

```java
//추가된 속성이나 메소드를 접근하기 위해 Down Casting 필요
RectAngle rectAngle = (RectAngle)shape;


public static void main(String[] args) {
	//클래스 형변환(Upcasting)
	Shape shape = null;
    shape = new Circle(10, 10, 20); //Shape의 자식 클래스
    
    //추가된 속성이나 메소드를 접근하기 위해 Down Casting 필요
    Circle circle = (Circle)shape;
    System.out.println(Circle.getradian()); // 제약이 있었던 getradian() 메서드 호출 가능
```



### Instanceof 연산자

- 레퍼런스 변수가 어떤 인스턴스를 참조하고 있는지, 특정 클래스로 캐스트 연산 가능한지를 검사하는 연산자 

- 리턴 값은 boolean 타입이다. 강제 형변환 오류 방지 용도로 사용

- 레퍼런스_변수 instanceof type 사용법

  ```
  //위의 코드와 연계하여 출력 메서드를 호출하면,
  	System.out.println(shape instanceof Object);
  	System.out.println(shape instanceof Shape);
  	System.out.println(shape instanceof Circle);
  	
  //결과값은 모두 true로 출력된다.
  ```

   즉, 위 코드의 경우 Circle 클래스를 강제형변환 해주었기 때문에 마지막 코드로 true로 출력되는 것이다.