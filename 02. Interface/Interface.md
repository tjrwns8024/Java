# **인터페이스(Interface )**

## **1. 인터페이스 개념과 역할**

인터페이스는 동일한 목적 하에 동일한 목적 하에 동일한 기능을 수행하게끔 하는 것입니다. 일종의 가이드 라인 이라고 생각하면 편할 것 같습니다. 이것을 좀 더 어려운 말로 말하자면 자바의 다형성을 극대화 하여 개발 코드 수정을 줄이고 프로그램 유지보수성을 높이기 위해 인터페이스를 사용한다고 할 수 있습니다. 

**1-1 예시**  <br/>

자 이번에 서울시는 밤길 여성들의 안전한 귀가를 위해 30억을 투입해 1000개 유명 중국 H사의 CCTV를 설치했다고 치자. 이제 CCTV에서 송출되는 영상을 각 지역 관할 파출소나 경찰서에서 모니터링 할 수 있도록 1년에 걸쳐 10억을 투자해 CCTV 모니터링 프로그램 시스템을 구축했다. 근데,, 문제가 생겼다 H사의 CCTV는 배터리가 불량고 비가 오면 방수처리가 잘 안되어 고장이 나기 시작했다.  
안되겠다 국산 G사의 CCTV로 전부 다 교체하기로 했다. 그런데 맙소사..중국 H사 CCTV의 영상 송출 모듈에만 특화된 프로그램을 만든 것이다. 다시 프로그램을 만들고 시스템을 구축해한다.  
 만약 현재 시중에서 판매되고 있는 CCTV 제조사가 CCTV의 송출 모듈을 모두 공통적으로 규격에 맞는 모듈로 개발했다면 이런 유지보수성의 불편함은 발생되지 않을 것이며 호환성이 높아질 것이다. 정리하면, 제조사가 다른 CCTV여도 영상 송출이라는 동일한 기능을 제공하게 하는 것이 바로 인터페이스이다.

~~생각을 많이 해보았지만, 이보다 좋은 예시를 생각해내기 힘들었다.~~

<br/>

**- 인터페이스란?**  
극단적으로 동일한 목적 하에 동일한 기능을 보장하게 하기 위해 사용합니다

**- 어떻게?**  
자바의 다형성을 이용하여 개발코드 수정을 줄이고 유지보수성을 높입니다. 


<br/>
<br/>

## **2.인터페이스 문법과 다형성 이해**
인터페이스는 **interface** 키워드를 통해 선언 할 수 있으며 implements 키워드를 통해 일반 클래스에서 인터페이스를 구현할 수 있습니다.   

![뷁](https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcQA9s9FPQRjrNQy7p1Ya7Hjq6OsvGR81GQKd9-hnl1rS6ZmYIG3&usqp=CAU)

<br/>


```java
public interface 인터페이스명{
    //상수
    타입 상수명 = 값;

    //추상 메소드
    타입 메소드명(매개변수,..);

    //디폴트 메소드
    default 타입 메소드명(매개변수,...){
        //구현부
    }

    static 타입 메소드명(매개변수){
        //구현부
    }
}
```

- 상수 
    - 인터페이스에서 값을 정해줄터니 함부로 바꾸지 말고 제공해주는 값만 참조하세요.  

- 추상 메소드 
    - 가이드만 제공할 테니 추상 메소드를 오버라이딩해서 재구현해주세요.

- 디폴트 메소드 
    - 인터페이스에서 기본적으로 제공해주지만, 마음에 들지 않으면 각자 구현하여 사용하세요.

- 정적 메소드
    - 인터페이스에서 제공해주는 것으로 무조건 사용하세요
