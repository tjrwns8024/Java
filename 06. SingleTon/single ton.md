# 싱글톤 패턴(Java Singleton Pattern)

**싱글톤 패턴**이란 디자인 패턴 중 하나로 처음 한 번만 객체를 생성해서 메모리에 할당하는 기법입니다.   

우리는 동일한 객체를 지속적으로 사용해야 할 때가 있습니다.   
여러분들은 매번 인스턴스를 생성하는 것이 좋다고 생각하시나요? 아니면 하나의 인스턴스를 사용하는 것이 좋다고 생각하십니까?  
당연히 동일한 객체를 지속적으로 사용한다면 하나의 인스턴스를 사용하는 것이 리소스 절약면에서 유리합니다.  

<br/>

<br/>


## 구현 방법

### 기본적인 방법

최초 한 번 객체를 초기화 하기 때문에 Thread-Safe를 보장합니다.  
하지만, 객체를 사용하지도 않는 경우에도 이미 생성되어 있어서 사용하지 않는다면 리소스 낭비가 있을 수 있습니다. 

```java
public class Singleton{
    private Singleton(){
        System.out.println("Hello Singleton");
    }

    private static Singleton singleton = new Singleton();

    public static Singleton getInstance(){
        return singleton;
    }
}
```

<br/>

### LazyHolder 방법

- LazyHolder는 순수하게 자바만 사용하는 경우 가장 인기있는 방법이라고 합니다.
<br/>

- getInstance() 메소드를 호출 할 때 LazyHolder 클래스를 로딩하고 Singleton 객체를 초기화 합니다.  
 
- 또한, 클래스를 로딩하는 시점에는 Thread-Safe를 보장하여 인스턴스가 여러 개 생길 수 없습니다. 

<br/>


```java
public class Singleton {

	private Singleton() {
		System.out.println("Hello singleton");
	}

	private static class LazyHolder {
		public static final Singleton INSTANCE = new Singleton();
	}

	public static Singleton getInstance() {
		return LazyHolder.INSTANCE;
	}

}

```

<br/>

---

<br/>

싱글톤 패턴으로 클래스를 구현하셨다면 해당 클래스는 **new Singleton**으로 객체를 생성할 수 없습니다.   
getInstance 메서드를 이용해서 사용하면 됩니다. 

```java
public static void main(String[] args){
    Singleton singleton = Singleton.getInstance();
}
```
<br>
 
 ### 테스트

 ```java
 public static void main(String[] args){
     Singleton singleton = Singleton.getInstance();
     Singleton singleton1 = Singleton.getInstance();
     Singleton singleton2 = Singleton.getInstance();
 }


//출력결과

Hello singleton
 ```