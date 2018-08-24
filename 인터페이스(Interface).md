# 인터페이스(Interface)

#### - 정의 : 인스턴스 생성 목적이 아닌 서로 다른 클래스 간 상호작용을 위한 수평적 표준 규격

	UML모델링 파일을 통해 쉽게 이해해보자.

![](C:\Users\kosta\Desktop\인터페이스 UML클래스 예.png)

어떤 Unit 클래스에서 각각 Gun, Sword, Club 클래스마다 Attack() 메소드를 호출하여야 사용한다고 치자.

무기가 3개면 그나마 가능하겠다. 허나 무기가 300개라면? 얼마나 복잡할까? 300개의 다른 이름을 지닌 클래스의 

메소드를 호출한다면 메모리 사용 뿐 아니라, 일일이 기억도 못할 것이다. 그때 Weapon 인터페이스로 연결한다.

##### ** Weapon Interface를 코드로 작성해보자.**

```java
/**
 * 무기에 대한 수평적 규격 역할의 인터페이스. 
 * 마치 실제 현실의 벤더사와 같다. 규격에 맞게 제품을 제조한다고 생각하기
 */
interface Weapon {
	public static final int weight = 10; // 자동 상수처리(public static final 자동추가)
	
	public abstract void attack(); //public abstract은 컴파일 시 자동으로 추가됨.
}
```

위의 코드를 보며 인터페이스의 기본 특징을 살펴보자.

1.  인터페이스 내 모든 메소드는 추상 메소드이다. attack()은 선언부만 있고, 구현부가 없는 추상 메소드
   - 메소드의 바디(몸체) 부분을 기술하지 않아야 한다.
   - 서브 클래스에서 어떻게 동작할지 구현(재정의)해줘야 한다. 그러므로, 오버라이딩은 필수.
   - 접근 지정자를 명시하지 않는 인터페이스 내 메소드를 오버라이딩 할 경우에는 서브 클래스에서 접근 지정자를 축소시켜 지정할 수 없으므로 public으로 지정해줘야 한다.
2.  인터페이스 내 모든 변수는 상수로 인식한다. 주석을 참고하면 좋다.

다음은 Weapon Interface를 구현(Implement)하는 Gun, Sword 클래스를 생성해보자.

### Gun.class / Weapon.class

```java
public class Gun implements Weapon {

	@Override
	public void attack() {
		System.out.println("총으로 쏜다.");
	}
}
```

```java
public class Sword implements Weapon {

	@Override
	public void attack() {
		System.out.println("칼로 벤다");
	}
}
```

인터페이스를 구현하는 두 클래스는 인터페이스의 attack() 메서드를 오버라이딩 하고 있다. 쉽게 말하면, 총과 검은 무기라는 통일된 표준 규격에 해당하고, 각 무기에 맞는 공격법을 구현부에 선언하여 사용하는 것이다.  이제 Unit.class를 만들어 인터페이스에 맞게 만든 무기(클래스)들을 사용해보자.

### Unit.class

```java
public class Unit {
	private Weapon weapon; // UML상 Weapon과 Unit은 연관관계(UML모델링 참고)
						   // Weapon 인터페이스는 데이터타입으로도 선언가능
	private String name;

	public Unit() {
	}

	public Unit(String name) {
		this.name = name;

''' //getter,setter 메소드 생략
	
	public static void main(String[] args) {
		Unit unit =new Unit("SCV"); //새로운 유닛 생성자 생성
		Weapon weapon = null; //생성자가 없기 때문에 선언만 해줌
		weapon = new Gun(); //업캐스팅
		unit.setWeapon(weapon);
		unit.attack();
	}
}
```

unit.attack()을 호출하면 Gun()의 attack 메소드인 ''총으로 쏜다.''가 출력된다. 

```java
		weapon = new Sword(); //업캐스팅
		unit.setWeapon(weapon);
		unit.attack();
```

이 경우 unit.attack()을 호출하면 Gun()의 attack 메소드인 ''칼로 벤다.''가 출력된다.



## 인터페이스의 다중 구현, 다중 상속

### 1) 다중구현 : 여러 인터페이스를 하나의 클래스에서 구현할 수 있다.

```java
public abstract class SumInterface implements AInterface, BInterface, CInterface {
	@Override
	public void a() {
	}

	@Override
	public void c() {
	}

	@Override
	public void b() {	
	}
}

```

다중 구현할 경우, 각각의 인터페이스의 추상 메서드를 반드시 오버라이딩 해야 한다.

(까먹어서 안할 경우, 빠른 오류 실행 지원해주니 너무 걱정말자 !)



### 2) 다중 상속 : 하나의 인터페이스가 여러 개를 상속받을 수 있다.

```java
/**
 * 인터페이스 다중상속
 * 저장하고자 하는 파일명 인터페이스에만 Public  선언
 * 실제 클래스 파일은 생성된다.(프로젝트 폴더 > src > bin)
 */
public interface AInterface {
	public void a();
}

interface BInterface {
	public void b();
}

interface CInterface extends AInterface, BInterface {
	public void c();
	
}

```



## 추상 클래스와 인터페이스의 차이점

![](C:\Users\kosta\AppData\Local\Temp\1535109091744.png)