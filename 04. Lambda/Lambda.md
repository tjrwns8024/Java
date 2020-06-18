# Lambda

람다식이란 **" 식별자없이 실행 가능한 함수 "**  

기존에 함수를 만든다고 하면 따로 함수를 만들어야 했습니다. 하지만 람다식은 함수를 따로 만들지 않고 코드 한줄에 써서 그것을 호출하는 방식이라고 할 수 있습니다.  

<br/>

## 람다식 사용법    

람다식은 매개변수, 실행문 으로 구성됩니다.      (이말은 접근자, 반환명을 생략한다)  

( )->{ }; 형태로 구성되며, 첫 괄호에는 interface의 매개변수를 { } 안에는 실행 코드를 넣어 작성합니다. 


```java
public interface Calculator{
    public int add(int x, int y);
}
```
> 람다식에서 사용할 인터페이스 입니다. 

```java
public static void main(String[] args){
    Calculator cal = (int x, int y) -> {return x + y;};
    System.out.println(cal.add(2,3));
}
//  매개 변수가 없는 경우 
() -> { };

//  중괄호 생략 가능 ( 실행 문이 한개일 경우 )
Calculator cal = (int x, int y) -> return x + y;

```
<br/>


## 3. 람다 사용 조건
람다식을 사용하기 위한 인터페이스에는 조건이 있습니다. 
-> 인터페이스의 **추상 메소드**가 단 1개여야 합니다. 


#### @FunctionallInterface Annotation 
```java
@FunctionallInterface 
public interface Calculator{
    public int cal(int x, int y);
    public void cal2(); // 추상 메소드가 2개 이므로 에러가 난다. 
}
```

위와 같이 람다식으로 표현하기 위해서 사용될 interface위에 @FunctionallInterface 만 붙혀준다면 컴파일 할 때 에러를 잡아줍니다. 

---
