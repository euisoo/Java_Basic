# 상속(Inheritance)

##### 의미 : 사전 정의(Built-in)된 클래스 속성이나 메서드를 새로 정의할 클래스에 그대로 내려받는 것 = 재사용 

##### 특징 : 사전정의 클래스(이하 부모클래스)에는 없는 새 속성이나 메소드를 추가(확장), 재정의(수정) 가능 

##### ![](C:\Users\kosta\Desktop\상속.PNG)

### 클래스 다이어 그램을 이용한 상속관계 표현

##### ![](C:\Users\kosta\Desktop\7.상속.jpg)

![](C:\Users\kosta\Desktop\7.상속(UML).png)

### 상속 예제 코드

![](C:\Users\kosta\Desktop\7.상속 예제코드.png)



### 상속 제약 사항

- 다중 상속을 지원하지 않는다. 즉, 부모 클래스가 여러개일 수 없다. (직계존속만 있다고 생각하자)
- 은닉화(private)되어있는 속성, 메소드는 상속되지 않는다. (getter & setter method 활용)
- 생성자는 상속되지 않는다. 
  - super : 슈퍼클래스의 인스턴스를 가리키는 참조(래퍼런스) 변수
  - super() : 슈퍼클래스의 생성자 호출



### 메서드 오버라이딩(Overriding)

##### 정의 :  슈퍼클래스에 정의된 메소드를 서브클래스에서 활용, 재정의(기능 수정)하는 것

##### 	    예를 들어, 같은 변수가 선언되었을 때 부모가 아닌 자식 클래스 변수를 사용하는 것.

##### 주의사항 (★★★)

1. 기본 - 기본적으로 메소드 선언부가 동일	

2. 접근제한자의 경우 같거나, 넓어야 함. 

3. 예외선언의 경우, 같거나 더 구체적(자식클래스)이어야 한다.


### 상속 실습

#### 1. Circle.class (부모 클래스)

```java
public abstract class Shape {
	protected double x, y; // 같은 패키지, 자식 클래스 상속

	// 추상 메소드
	// 서브 클래스가 반드시 구현(재정의)해야 할 수직적 규약
	public abstract void draw(); // 추상 메서드

	public abstract double getLength();

	public abstract double getArea();

	// 재사용 클래스
	public void xxx() {
	}
}
```

### 2. Circle. class / Rectangle.class (자식 클래스)

```java
public class Circle extends Shape {
	private double radian;

	public Circle() {
		this(0.0, 0.0, 0.0);
	}

	public Circle(double x, double y, double radian) {
		this.radian = radian;
	}

	public double getRadian() {
		return radian;
	}

	public void setRadian(double radian) {
		this.radian = radian;
	}

	@Override
	public void draw() {
		System.out.println(x + " ," + y + ", " + getRadian() + "의 원입니다.");
	}

	@Override
	public double getLength() {
		return 2 * Math.PI * radian;
	}

	@Override
	public double getArea() {
		return Math.PI * Math.pow(radian, 2);
	}

	@Override
	public String toString() {
		return getRadian() + ", " + super.toString();
	}
}
```

```java
public class RectAngle extends Shape{
	private double width;
	private double height;
	
	
	public RectAngle() {
		this(0.0, 0.0, 0.0, 0.0);
	}
	public RectAngle(double x, double y, double width, double height) {
		super();
		this.width = width;
		this.height = height;
	}
	public double getWidth() {
		return width;
	}
	public void setWidth(double width) {
		this.width = width;
	}
	public double getHeight() {
		return height;
	}

	public void setHeight(double height) {
		this.height = height;
	}

	@Override
	public void draw() {
		System.out.println(x + ", " + y + ", " + getHeight() + ", " + getLength() + "의 사각형입니다.");
	}
	@Override
	public double getLength() {
		return 2 * (height * width);
	}
	@Override
	public double getArea() {
		return height * width;
	}
	@Override
	public String toString() {
		return "RectAngle [width=" + width + ", height=" + height + ", toString()=" + super.toString() + ",]";
	}	
}
```



### 3. ShapeApp.class

```java
/**
 * UML상 의존관계(defendency)인 어플리케이션 클래스
 * @author 박의수
 */
public class ShapeApp {

	public static void main(String[] args) {
		//Shape shape = new Shape(23.1, 44.2);
		Shape shape = null;
		Circle circle = new Circle(15.1, 22.1, 30);
		RectAngle rectAngle = new RectAngle(24, 24, 48, 24);
		circle.draw();
		System.out.println("원의 면적 : " + circle.getArea());
		System.out.println("원의 둘레 : " + circle.getLength());

		System.out.println("사각형의 면적 : " + rectAngle.getArea());
		System.out.println("사각형의 둘레 : " + rectAngle.getLength());

		System.out.println(shape);
		System.out.println(shape.toString());

		System.out.println(circle);

		String str = "Java Programming";
		System.out.println(str);
	}
}
```



## < 부록 >

### 1) [기타제한자] Final의 사용법

1. ##### [static final] 변수 = 재사용금지

2. [final] 클래스 = 상속 금지

3. [final] 메소드 = 오버라이딩(재정의) 금지



### 2) [접근 제한자] protected

1. ##### 스코프 : public > protected < (생략) < private

2. ##### 자신의 패키지 내 클래스만 접근 가능 (단, 다른 패키지라도 상속관계면 가능)



### 3) Object class

1. ##### toString() - [class명]@21df21 에 저장되어있는 스트링 객체를 반환하는 메서드

   - 자기 패키지에서만 사용 가능 (단, 다른 패키지라도 상속관계면 가능)

2. ##### 객체 지향 프로그래밍의 4대 속성 : 추상화, 캡슐화, 다형성, 상속