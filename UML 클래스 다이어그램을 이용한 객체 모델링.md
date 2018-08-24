# UML 클래스 다이어그램을 이용한 객체 모델링

##### 객체(Object) + 모델링(Modeling) = 요구분석 단계에서 도메인 객체를 식별하고, 객체의 속성과 행위, 객체들간의 관계(상호작용)를 도형과 기호를 이용하여 이해하기 쉬운 형태로 표현 : 개발하고자 하는  객체지향 시스템의 정적 구조 표현

##### UML(Unified Modeling Language) =  개발하려는 소프트웨어 시스템을 시각적으로 쉽게 모델링 언어



## 모델링과 프로그래밍의 비교

![](C:\Users\kosta\Desktop\모델링,프로그래밍 비교.png)



## 구성요소 

- #### 클래스 - 각 객체의 공통요소를 추상화한 설계도(클래스 이름 + 속성 + 메소드)

  - 클래스 다이어 그램은 클래스 간의 상호작용(관계)를 모델링, 시스템의 정적구조를 표현
  - 클래스 이름, 속성, 메소드로 구성된다.

- #### 가시성 - 한 클래스의 속성, 메소드의 공개 정도

  - (public(+), protected(#), package(~), private(-))

![](C:\Users\kosta\AppData\Local\Temp\1535102389222.png)

- #### 스코프 - 속성 및 메소드의 사용범위(구분 : 인스턴스, 클래스)

  - 인스턴스 스코프 : 인스턴스(객체) 단위로 속성이나 메소드 존재
  - 클래스 스코프 : 클래스 단위로 속성이나 메소드 존재
    ![](C:\Users\kosta\AppData\Local\Temp\1535102455042.png)

- #### 관계(★★★) : 클래스 사이의 관계, 인스턴스 사이에 메시지 교환이 발생하는지 의미

  ![](C:\Users\kosta\AppData\Local\Temp\1535102657561.png)

  ##### 다중도 - 관계를 맺고 있는 클래스의 인스턴스 수 를 나타낸다. (복수 = *, 세트 = 2,4,6,8 등)

![](C:\Users\kosta\AppData\Local\Temp\1535102884853.png)

	

- ##### 관계 집합(Aggregation) : 클래스 사이에 전체-부분 관계가 존재함

  ![](C:\Users\kosta\AppData\Local\Temp\1535103709194.png)

- ##### 관계 복합(Composition) 

![](C:\Users\kosta\AppData\Local\Temp\1535103733911.png)

###### 관계 일반화(Generalization) = java에서의 상속

![](C:\Users\kosta\AppData\Local\Temp\1535103746260.png)

###### 관계 의존(Dependency)

![](C:\Users\kosta\AppData\Local\Temp\1535103759775.png)

###### 관계 실현(Realization)

###### ![](C:\Users\kosta\AppData\Local\Temp\1535103459602.png)

###### 추상클래스(abstract class)

![](C:\Users\kosta\AppData\Local\Temp\1535103575813.png)