# OOP(Object Oriented Programming)
**OOP**는 **Object Oriented Programming**의 줄임말로 객체지향 프로그래밍을 뜻합니다. 

## OOP의 특징 4가지
- [캡슐화](##캡슐화(Encapsulation))
- [추상화](##추상화(Abstraction))
- [다형성](##다형성(Polymorphism))
- [상속성](##상속성(Inheritance))

<br/>

코드의 **재사용성**을 증가하고 **유지보수**를 쉽게 하기 위해 객체지향 프로그래밍을 사용합니다. 

---

## **캡슐화(Encapsulation)**
 **캡슐화** 란, 쉽게 말하면 말 그대로 캡슐처럼 감싸는 개념입니다.   
 - 객체의 변수, 메소드 등 **실제 구현 내용을 보이지 않게 감싸는 개념**입니다. 
 <br/>

 - 따라서, 외부 객체가 함부로 내부 객체를 건드리지 못하게 하는 것입니다. 
 - 변수 앞에 private을 선언하는 것을 떠올리면 될 것입니다. 

 <br/>

 ## **추상화(Abstraction)**
 **추상화** 란, 공통의 속성이나 기능을 묶어 이름을 붙이는 것입니다. 

- 예를 들자면, 삼각형, 사각형, 원 이라는 객체가 있습니다. 

- 이 객체들을 하나로 묶을 때 객체들의 **공통 특징**인 도형으로 묶어 이름을 붙이는 것을 **추상화** 라고 합니다.

<br/>

## **다형성(Polymorphism)**
**하나의 객체가 여러 가지 타입**을 가질 수 있는 것을 의미합니다. 
- 상위 클래스의 참조 변수가 하위 클래스의 객체를 참조하게 하는 것입니다. 

- **오버로딩, 오버라이딩, 업캐스팅, 다운캐스팅, 인터페이스, 추상메소드, 추상클래스** 방법이 있다고 생각하면 된다.

<br/>

## **상속성(Inheritance)**
상위 클래스의 속성(변수)과 기능(메소드)을 재사용(상속)하여 하위 클래스가 전부 물려받는 것입니다. 

- 물려받는 것 외에 속성과 기능을 추가할 수 있습니다. 


<br/>

<br/>


## **OOP의 5대 원칙 (SOLID 원칙)**

![solid 법칙](https://image.slidesharecdn.com/oopdesignprinciple-100626012938-phpapp02/95/oop-design-principle-3-728.jpg?cb=1277515810)
---

### **SRP(단일 책임의 원칙 : Single Responsibility Principle)**
 ### 1. 정의  
 
 작성된 클래스는 **하나의 기능**만 가지며 클래스가 제공하는 모든 서비스는 그 하나의 책임을 수행하는 데 집중되어 있어야 한다는 **원칙**입니다. 이는 어떤 변화에 의해 클래스를 변경해야 하는 이유는 오직 하나뿐이어야 함을 의미합니다. 
 SRP 원리를 적용하면 무엇보다도 **책임 영역**이 확실해지기 때문에 한 책임의 변경에서 다른 책임의 변경으로의 연쇄작용에서 자유로울 수 있습니다. 뿐만 아니라 책임을 적절히 분배함으로써 **코드의 가독성 향상**, **유지보수 용이**라는 이점까지 누릴 수 있습니다. 이 원리는 다른 원리들에 비해서 개념이 비교적 단순하지만, 이 원리를 적용해서 직접 클래스를 설계하기가 그리 쉽지만은 않습니다. 왜냐하면, 실무의 프로세스는 매우 복잡 다양하고 변경 또한 빈번하기 때문에 경험이 많지 않거나 도메인에 대한 업무 이해가 부족하면 나도 모르게 SRP원리에서 멀어져 버리게 됩니다. 따라서 평소에 많은 연습과 경험이 필요한 원칙입니다.   

 ### 2. 적용 방법
 ```java
 class Guitar(){
     public Guitar(String serialNum, double price, Maker maker, Type type, String model, Wood backWood, Wood topWood, int stringNum){
         this.serialNum = serialNum;
         this.price = price;
         this.maker = maker;
         this.type = type;
         this.model = model;
         this.backWood = backWood;
         this.topWood = topWood;
         this.stringNum = stringNum;

     }

     private String serialNum;
     private double price;
     private Maker maker;
     private Type type;
     private String model;
     .
     .
     .
 }
 ```
 위의 코드는 특정 정보군에 변화가 발생하면 항상 해당 클래스를 수정해야 하는 부담이 발생하게 됨으로 이 부분이 SRP적용의 대상이 됩니다. 

 ```java
 class Guitar(){
     public Guitar(String serialNum, GuitarSpec spec){
         this.serialNum = serialNum;
         this.spec = spec;
     }

     private String serialNum;
     private GuitarSpec spec;

     ...
 }
 class GuitarSpec(){
     double price;
     Maker maker;
     Type type;
     String model;

     ...
 }
 ```

 위의 코드를 보면 특성 정보군을 분리한 것을 확인 할 수 있습니다. 따라서 특성 정보에 변경이 일어나면 GuitarSpec 클래스만 변경하면 됩니다. 

 <br/>

 ### **OCP(개방폐쇄의 원칙 : Open Close Principle)**

 ### 1. 정의
 버틀란트 메이어박사가 1998년 객체지향 소프트웨어 설계 라는 책에서 정의한 내용으로 **소프트웨어의 구성요소(컴포넌트, 클래스, 모듈, 함수)는 확장에는 열려있고, 변경에는 닫혀있어야 한다는 원리입니다.** 이것은 변경을 위한 비용은 간으한 줄이고 확장을 위한 비용은 가능한 극대화 해야 한다는 의미로, 요구사항의 변경이나 추가사항이 발생하더라도, 기존 구성요소는 수정이 일어나지 말아야 하며, 기존 구성요소를 쉽게 확장해서 재사용할 수 있어야 한다는 뜻입니다. 

  ### 2. 적용 방법

 ![짱짱 그림](https://t1.daumcdn.net/cfile/blog/245E674158ED329B1E)

 저는 이 그림보고 단번에 이해해버렸어요..


### **LSP(리스코브 치환의 원칙 : The Liskov Substitution Principle)**

### 1. 정의

LSP를 한마디로 한다면, "서브 타입은 언제나 기반 타입으로 교체할 수 있어야 한다." 라고 할 수 있습니다. 즉, 서브타입은 언제나 기반 타입과 호환될 수 있어야 합니다. 달리 말하면 서브 타입은 기반 타입이 약속한 규약(public 인터페이스 , 메소드가 던지는 예외까지 포함)을 지켜야 합니다. 상속은 구현상속(extends)이든 인터페이스 상속(implements)이든 궁극적으로는 다형성을 통한 확장성을 획득을 목표로 합니다. 다형성과 확장성을 극대화 하려면 하위 클래스를 사용하는 것보다는 상위의 클래스(인터페이스)를 사용하는 것이 더 좋습니다

### 2. 적용 방법

컬렉션 프레임워크

```java 
void f(){
    LinkedList list = new LinkedList();
    //...
    modify(list);
}

void modify(LinkedList list){
    list.add(...);
}
```

LinkedList를 다시 HashSet으로 바꿔야 한다면 LinkedList와 HasghSet은 모두 Collection인터페이스를 상속하고 있으므로 다음과 같이 작성하는 것이 바람직 합니다. 

```java
void f(){
    Collection collection = new HashSet();
    // ... 
    modify(collection);
}

void modify(Collection collection){
    collection.add(...);
}
```

이제 컬렉션 생성 부분만 고치면 마음대로 어던 컬렉션 구현 클래스드 사용할 수 있습니다. 


### **ISP(인터페이스 분리의 원칙 : Interface Segregation Principle)**

### 1. 정의
ISP 원리는 한 클래스는 자신이 사용하지 않는 인터페이스는 구현하지 말아야 한다는 원리입니다. 즉, 어떤 클래스가 다른 클래스에 종속될 때에는 가능한 최소한의 인터페이스만을 사용해야합니다. ISP를 '하나의 일반적인 인터페이스보다는, 여러 개의 구체적인 인터페이스가 낫다'라고 정의할 수도 있습니다. 만약 어떤 클래스를 이용하는 클라이언트가 여러 개고 이들이 해당 클래스의 특정 부분 집합만을 이용한다면, 이들을 따로 인터페이스로 빼내어 클라이언트가 기대하는 메시지만을 전달할 수 있도록 합니다. 하지만 ISP는 어떤 클래스 혹은 인터페이스가 여러 책임 혹은 역할을 갖는 것을 인정합니다. 이러한 경우 ISP가 사용되는데 SRP가 클래스 분리를 통해 변화에의 적응성을 획득하는 반면 ISP에서는 인터페이스 분리를 통해 같은 목표에 도달합니다. 

### 2. 적용방법
![SRP](https://sehun-kim.github.io/sehun/assets/images/1541913074849.png)
SRP 예제 중 남자를 단일 책임을 갖는 클래스로 나누었다. 이것은 너무 많은 클래스를 불러온다. 그래서 다양한 역할을 인터페이스로 만들고 남자라는 클래스는 그 인터페이스를 구현한 클래스이면 된다. 

![ISP](https://img1.daumcdn.net/thumb/R720x0.q80/?scode=mtistory2&fname=http%3A%2F%2Fcfile1.uf.tistory.com%2Fimage%2F99FF0A435BBEF3130BC45A)

```java
남자친구 홍길동 = new 남자();
아들 홍길동 = new 남자();
사원 홍길동 = new 남자();
소대원 홍길동 = new 남자();
```

### **DIP( Dependency Inversion Principle) 의존 역전 원칙**

### 1. 정의
: 자신보다 변하기 쉬운 것에 의존하지 마라  

> "고차원 모듈은 저차원 모듈에 의존하면 안 된다. 이 두 모듈 모두 다른 추상화된 것에 의존해야 한다."  
<br/>
> "추상화된 것은 구체적인 것에 의존하면 안된다. 구체적인 것이 추상화 된 것에 의존해야 한다."      
<br/>
> "자주 변경되는 구체 클래스에 의존하면 안된다. "
- 로버트 C 마틴

의존 관계의 역전 Dependecy Inversion 이란 구조적 디자인에서 발생하던 하위 레벨 모듈의 변경이 상위 레벨 모듈의 변경을 요구하는 위계관계를 끊는 의미의 역전입니다. DIP는 복잡하고 지난한 컴포넌트 간의 커뮤니케이션 관계를 단순화 하기 위한 원칙입니다. 

### 2. 적용 방법
![의존 역전 원칙 적용 전](https://img1.daumcdn.net/thumb/R720x0.q80/?scode=mtistory2&fname=http%3A%2F%2Fcfile25.uf.tistory.com%2Fimage%2F995AA1425B1015A1318594)
위의 사진은 의존 역전 원칙을 적용하기 전이다. 자동차는 자주 변경되는 구체 클래스에 의존한다.   
<br/>

해당 의존 관계를 아래와 같이 타이어 인터페이스를 사용하여 역전시켰습니다. : 구체적인 스노우 타이어에 의존하던 것을 추상적인 타이어에 의존하는 것으로 변경했습니다. 

![의존 역전 원칙 적용 후](https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F991509425B1015A122)

```java
//기존 코드
class Car{
    SnowTire tire = new SnowTire();
}

// DIP 적용
class Car{
    Tire tire;

    void setTire(Tire tire){
        this.tire = tire;
    }
}
```


---
SOLID 원칙을 적용하면 소스 파일의 객수는 오히려 늘어납니다. 하지만 그만큼 유지 보수와 코드에 대한 이해가 쉬워진다는 장점이 있습니다. 😊