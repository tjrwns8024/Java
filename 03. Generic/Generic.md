# 제네릭 (Generic)

제네릭(Generic)은 코드 블럭 내부에서 쓸 자료형을 외부에서 지정하는 방법입니다. 여러가지 자료형을 허용하고 싶을 때 **Object**로 선언해버리면 많은 자료형을 받을 수 있기 때문에 깔끔하지만, 원하지 않는 자료형이 입력되었을 때 오류를 컴파일 시점에서 잡아낼 수 없다는 단점이 있습니다. 

## 1. Generic Class
 
 클래스 내부에서 사용될 자료형을 지정하는 것입니다.   대표적인 예는 ArrayList가 있습니다. 

 ```class Foo<T>{
     private T t;

     public void set(T t){
         this.t = t;
     }

     public T get(){
         return t;
     }
 }
 ```
 <br/>
 

 ## 2. Generic Method
 
 굳이 클래스에 제네릭을 선언하지 않고, 메소드에만 제네릭을 선언하는 방법도 있습니다. 이때 주의해야할 점이 있는데, 파라미터 타입 또는 리턴 타입에 제네릭을 선언했으면 **메소드의 리턴타입 앞에도 똑같이 선언**해 주어야 합니다. 

 ```java
 class Koo {
    // 두개 이상의 파라미터에도 각각 제네릭을 설정할 수 있다.
    public <N1, N2> Integer exampleOne(N1 t, N2 e) {
        return (Integer)t + (Integer)e;
    }
 
    // 먼저 나왔던 Foo 클래스를 리턴타입으로 정의한 메소드
    public <String> Foo<String> exampleTwo() {
        return new Foo<>();
    }
}
 ```
 <br/>


 ## 3. Generic Interface

 클래스에서 인터페이스를 좀 더 유연하게 구현할 수 있습니다. 

 ```java
 interface Roo <T1, T2, T3> {
    T1 implementThis(T1 t1);
    T2 implementThis();
    T3 maintainGeneric(T3 t3);
}
 
// 제네릭에 어떤 자료형의 정의하느냐에 따라 유연하게 구현 가능.
class roo <String, Integer, T3> implements Roo<String,Integer,T3> {
 
    @Override
    public String implementThis(String s) {
        return s;
    }
 
    @Override
    public Integer implementThis() {
        return null;
    }
 
    // 이렇게 제네릭을 유지하는 방법도 있음.
    @Override
    public T3 maintainGeneric(T3 t3) {
        return null;
    }
}
 ```
 <br/>

 ## 4. 제네릭 타입

 사용할 타입을 외부에서 받을 건데, 이때 인스턴스를 생성하는 시점 또는 메소드를 호출하는 시점에 정할 수 있습니다.   

 ```java
public class Car<T>{
    private T t;
    public void set(T t){ this.t = t;}
    public T get() {return t;}
}

// 사용
Car<String> car1 = new Car<String>();
car1.set("Black");
String color = car1.get();
 ```

 제네릭 타입은 두개 이상의 타입 파라미터를 사용가능합니다. 
 ```java
//1. 
class<K,V,..>{...}
//2.
interface<K,V,..>{...}
 ```

 | <center>타입 인자</center> | 의미 |
|:--------|:--------:|
|   <center>E</center>  | Element | 
| <center>K</center> | Key | 
| <center>N</center> | Number | 
| <center>T</center> | Type | 
| <center>V</center> | Value | 
| <center>R</center> | Result | 

<br/>

 ## 5.와일드 카드 Type

 와일드 카드 타입은 3가지로 구분되며  ? 키워드로 표시합니다. 

 - 제네릭타입<?> 
 타입 파라미터를 대신하는 것으로 모든 클래스나 인터페이스 타입이 올 수 있습니다.

 - 제네릭타입<? extends 상위타입>
 와일드 카드의 범위를 특정 객체의 하위로 제한하는 것입니다. 

 - 제네릭타입<? super 하위타입>
 위의 반대로 상위클래스만 올 수 있게 합니다. 