# Thread (자바 쓰레드)

자바는 멀티 쓰레드를 지원하는 언어입니다. 여기서 멀티 쓰레드란 , 하나의 프로그램에서 여러 개의 실행 흐름을 만들고 실행 할 수 있다는 것입니다. 

**쓰레드** : 프로세스에서 하나의 실행 흐름  

**멀티 쓰레드를 사용하는 이유** : 외부와의 연계같이 대기 시간이 발생했을 때 기다리는 동안 다른 일을 처리할 수 있게 해서 처리 속도를 향상 시켜준다. 

<br/>

## 쓰레드 만드는 방법

1. Runnable 인터페이스를 상속(확장)한 클래스를 만든다. (Runnable 인터페이스를 상속받으면 run()메서드를 구현해야 한다.)

2. 1에서 상속한 클래스 객체를 만든다. (Runnable 객체 / 실행가능한 객체)

3. 2에서 만든 객체를 가진 실행흐름(Thread) 객체를 만든다. (자바에서 제공)

4. 쓰레드를 실행시킨다. (필요에 따라 중지도 시킴)


```java
public class MultiThreadSample implements Runnable{
    private static final String MSG_TEMPLATE = "출력중 [%s][%d회]";
    private final String threadName;
    public MultiThreadSample(String threadName){
        this.threadName = threadName;
    }
    public void run(){
        for(int i =1;i<100;i++){
            System.out.println(String.format(MSG_TEMPLATE, threadName,i));
        }
    }
    public static void main(String[] args){
        MultiThreadSample runnable1 = new MultiThreadSample("thread1");
        MultiThreadSample runnable2 = new MultiThreadSample("thread2");
        MultiThreadSample runnable3 = new MultiThreadSample("thread3");
        
        Thread thread1 = new Thread(runnable1);
        Thread thread2 = new Thread(runnable2);
        Thread thread3 = new Thread(runnable3);
 
        thread1.start();
        thread2.start();
        thread3.start();
    }
}    
```

## 쓰레드 풀(Thread Pool)

위는 쓰레드의 갯수가 한정적이지만 만약 접속한 사람만큼 쓰레드를 생성을 한다면 메모리를 다 잡아먹을 만큼 쓰레드가 생성될 것입니다. 

따라서 **쓰레드풀**을 이용해서 쓰레드 생성할 때 최대 개수를 지정합니다. 

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;
 
public class MultiThreadSample implements Runnable {
    private static final String MSG_TEMPLATE = "출력중 [%s][%d회]";
    private final String threadName;
    public MultiThreadSample(String threadName){
        this.threadName = threadName;
    }
    public void run(){
        for(int i =1;i<100;i++){
            System.out.println(String.format(MSG_TEMPLATE, threadName,i));
        }
    }
    public static void main(String[] args){
        MultiThreadSample runnable1 = new MultiThreadSample("thread1");
        MultiThreadSample runnable2 = new MultiThreadSample("thread2");
        MultiThreadSample runnable3 = new MultiThreadSample("thread3");
        
        ExecutorService executorService = Executors.newFixedThreadPool(3);
        executorService.execute(runnable1);
        executorService.execute(runnable2);
        executorService.execute(runnable3);
        
        executorService.shutdown();
        try{
            if(!executorService.awaitTermination(5, TimeUnit.MINUTES)){
                executorService.shutdownNow();
            }
        }catch(InterruptedException e){
            e.printStackTrace();
            executorService.shutdownNow();
        }
    }
}
```

<br/>

* 쓰레드풀을 3개로 제한하고 많은 Runnable객체를 4개 이상 만든다면 앞에서 Runnable객체가 먼저 실행하고 실행이 끝나면 다음 Runnable객체가 들어가게 된다.

* .shutdown() 메서드는 실행중인 작업 뿐만 아니라 작업 큐에 대기하고 있는 모든 작업들을 다 '처리'하고 쓰레드풀을 중지시킨다. (shutdownNow()는 인터럽트로 즉시 중지시킨다.)

* .awaitTermination은 shutdown()메서드 호출이후 해당 시간만큼안에 쓰레드풀의 작업이 전부 수행하지 못하면 실행중이던 쓰레드에 인터럽트를 발생시키고 false 반환한다. (예제에선 5,TimeUnit.MINUTES 즉 5분이다)

## 쓰레드 세이프(Thread Safe)

쓰레드 세이프를 사용하는 이유는 두 쓰레드에서 하나의 클래스를 동시에 사용하려고 했기 때문입니다.   

이를 해결하기 위해 **synchronized** 를 사용합니다.

```java
import java.util.Date;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Calendar;
 
public class SynchronizedSample {
    public static void main(String[] args){
        //안전하지 않은 객체
        DateFormat unsafeDateFormat = new SimpleDateFormat("yyyy/MM/dd");
        Calendar cal1 = Calendar.getInstance();
        cal1.set(1989,Calendar.MARCH,10);//1989/03/10
        Date date1 = cal1.getTime();
        Calendar cal2 = Calendar.getInstance();
        cal2.set(2020, Calendar.JUNE,20);//2020/06/20
        Date date2 = cal2.getTime();
        
        Thread thread1 = new Thread(() ->{
            for(int i=0;i<100;i++){
                try{
                    String result;
                    synchronized (unsafeDateFormat) {
                        result= unsafeDateFormat.format(date1);
                    }
                    System.out.println("Thread1: " + result);
                }catch(Exception e){
                    e.printStackTrace();
                    break;
                }
            }
        });
        Thread thread2 = new Thread(() ->{
            for(int i=0;i<100;i++){
                try{
                    String result;
                    synchronized (unsafeDateFormat) {
                        result= unsafeDateFormat.format(date2);
                    }
                    System.out.println("Thread2: " + result);
                }catch(Exception e){
                    e.printStackTrace();
                    break;
                }
            }
        });
        
        thread1.start();
        thread2.start();
    }
}

```

synchronized를 통해 unsafeDateFormat에 제한을 두어 쓰레드끼리 동시에 사용하지 못하게 막은 것입니다.  
unsafeDateFormat 객체를 사요하려고 하면 쓰고있는지 검사하여 기다리게 하거나 사용하게 해줍니다. 

하지만 synchronized를 사용하게 되면 그냥 멀티 쓰레드를 사용하는 것 보다 100배 정도 속도가 느리게 나옵니다. 

---

<br/>


출처: https://jeong-pro.tistory.com/71 [기본기를 쌓는 정아마추어 코딩블로그]