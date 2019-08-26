---
layout: customize-posts
title: 인터페이스와 추상클래스 정리
date: 2019-08-26
last_modified_at: 2019-08-26
description: "인터페이스와 추상클래스의 공통점과 차이점을 알고 넘어가기 위한 글"
header:
    teaser: /assets/images/K.png
    og_image: /assets/images/K.png
keywords:
    - java
    - interface
    - abstract
    - 인터페이스
    - 추상클래스
    - 공통점
    - 차이점
category:
    - Java
    - Study
tags:
    - java
sitemap: 
    changefreq: daily
    priority: 1.0
---

> 인터페이스와 추상클래스의 목적과 공통점, 차이점이 모호해 정리해보고자 한다. 

## 인터페이스
인터페이스는 아직 구현되지 않은 상태, input과 output만 정의된 상태의 메소드를 갖고 있고 갖고 있는 메소드의 구현을 강제하는데 목적이 있다. 인터페이스에 정의한 메소드의 경우에는 해당 인터페이스를 구현(implemnets) 한 클래스에서는 메소드의 구현을 꼭 해주어야 한다. 또한, 인터페이스에서는 public defualt 접근제어자만 사용이 가능하며 정의된 모든 메소드는 abstract가 붙는다. (암묵적으로 붙기때문에 따로 붙여주지 않아도 됨.) 그리고 인터페이스는 인스턴스화를 할 수 가없다. 인스턴스화를 하기위해서는 구현을 강요받은 클래스를 활용해서 ```인터페이스명 a = new 강요받은클래스명()``` 이렇게 사용하면 된다.  

- 메소드를 input(파라미터), output(리턴타입)만 정의한다.
- public, default 접근제어자만 가능하다.
- 정의한 메소드는 암묵적으로 abstract가 붙는다.
- 인스턴스화는 구현을 강요받은 클래스를 활용해서 가능하다.

예를 들어 상태(State)라는 인터페이스가 있다. 이 상태 클래스에는 상태를 나태내는 기능인 **display**와 상태를 변경하는 **change** 기능을 정의하면 아래와 같은 인터페이스가 될 것이다.  

```java
public interface State {

    (abstract) String display();

    (abstract) void change(String changeValue);
}
```

위의 인터페이스를 implements 하여 구현을 강요받게 되면 아래와 같이 된다. 아래와 같이 implements하게 되면 IDE에서 State인터페이스에서 정의한 메소드 구현을 하라는 Error Message를 볼수 있다.  
> 참고) 1번은 Error Message가 노출되는 소스이며, 2번은 정상적으로 implemnets한 인터페이스를 구현한 소스이다.

```java

1) 메소드 구현 강요 Message 노출
public class StateImplemnetClass implements State {
}

2) 메소드 Override를 통한 구현
public class StateImplemnetClass implements State {

    private String state;

    public StateImplemnetClass(String state) {
        this.state = state;
    }

    @Override
    public String display() {
        return this.state;
    }

    @Override
    public void change(String changeValue) {
        this.state = changeValue;
    }
}
```

위의 인터페이스를 인스턴스화 하기 위해서는 아래의 형식으로 인스턴스화 해주어야 한다.
```java
State stateClass = new StateImplemnetClass("StateImplemnets");
```

## 추상클래스
추상클래스는 메소드가 없거나 하나 이상의 추상메소드를 갖고 있어야한다. 하나 이상의 추상메소드를 갖게 된다면 class앞에 abstract를 붙여 주어야 한다. 추상클래스의 경우 추상메소드만 있을 수도 있고 일반 구현이 된 메소드가 있을 수 있다. 추상클래스도 인터페이스와 마찬가지로 다른 클래스에서 상속을 받게 된다면 추상메소드로 정의한 부분은 상속받은 자식클래스에서는 필수로 구현해 주어야한다. 만일 추상클래스 -> 추상클래스가 상속을 받는다면 구현해줄 필요는 없다. 또한 추상클래스에서 인터페이스를 구현할 수가 있는데 이때는 인터페이스에 정의된 클래스를 굳이 구현을 하지 않아도 Error Message가 노출되지 않는다. 그 이유는 **인터페이스에 정의된 모든 메소드는 암묵적으로 abstract가 정의되어있기 때문에 추상클래스에서 구현을 강제받아도 추상메소드로 인식이 되기 때문이다.** 또한 추상클래스도 인터페이스와 동일하게 인스턴스화를 직접적으로는 못하지만 상속받은 자식클래스를 활용해 ```추상클래스명 a = new 상속받은자식클래스명()```으로 인스턴스화가 가능하다. 

- 하나이상의 추상메소드를 갖고 있고, 일반 구현된 메소드를 갖을 수 있다.
- 추상클래스를 상속받을 시 자식클래스에서는 추상메소드를 필수로 구현해 주어야한다.
- 추상클래스 -> 추상클래스, 인터페이스 -> 추상클래스 를 상속 및 구현받더라도 추상메소드는 필수로 구현을 하지 않아도 된다.
- 인스턴스화는 상속받은 자식클래스를 활용해서 가능하다.

예를 들어 상태(StateAbstract)라는 추상클래스가 있다. 이 상태 추상클래스에는 상태를 나태내는 추상메소드인 **display**와 상태를 변경하는 일반메소드인 **change** 기능을 정의하면 아래와 같은 클래스가 될 것이다.  

```java
abstract public class StateAbstract {

    private String state;

    public StateAbstract(String state) {
        this.state = state;
    }

    abstract String display();

    void change(String changeValue) {
        this.state = changeValue;
    }
}
```

위의 추상클래스를 extends하여 사용하면 아래와 같이 된다. 아래와 같이 extends하게 되면 IDE에서 StateAbstract클래스에서 정의한 추상메소드 구현을 하라는 Error Message를 볼수 있다.  
> 참고) 1번은 Error Message가 노출되는 소스이며, 2번은 정상적으로 extends한 소스이다.

```java
1) 추상메소드 구현을 강요하는 Mesaage 노출
public class StateExtendsClass extends StateAbstract {    
}

2) 추상메소드를 Override를 통한 소스
public class StateExtendsClass extends StateAbstract {

    // StateAbstract에 생성자
    public StateExtendsClass(String state) {
        super(state);
    }

    @Override
    String display() {
        return null;
    }
}
```

위의 추상클래스를 인스턴스화 하기 위해서는 아래의 형식으로 인스턴스화 해주어야 한다.
```java
StateAbstract stateAbstractClass = new StateExtendsClass("StateExtends");
```

## 추상클래스와 인터페이스를 같이사용한 짧은 예제..
위의 정리한 내용 기반으로 예제소스를 작성해 보았다. 소스는 Run된 상태와 시간, 그리고 Stop된 상태와 시간을 출력하는 간단한 소스이고 인터페이스 -> 추상클래스 -> 클래스 구조로 잡고 구현을 하였다. 간략한 구조의 의도는 아래와 같다.
1. State 인터페이스에 display() 메소드를 정의하여 하위 클래스에 구현을 위임.
2. RunState, StopState 추상클래스에 State인터페이스를 implements한 뒤 각각의 일반메소드를 추가하여 2개의 추상클래스의 사용목적을 달리함.
3. Run, Stop 클래스에서는 RunState, StopState를 extends하여 추상클래스의 일반메소드는 그대로 사용, 최상단의 State인터페이스는 출력문구를 달리하기위해 override하여 커스터마이징(다형성)

#### 1. 인터페이스 : display 메소드만 정의
```java
public interface State {

    String display();
}
```

#### 2. 추상클래스 : RunState와 StopState 추상클래스 2개를 만들고 각각의 시작과 종료된 시간을 넘기는 일반메소드 구현
```java
abstract class RunState implements State {

    private static final String RUN_STATE = "Run!!";
    protected String state;
    protected static Date date = new Date();

    public RunState() {
        this.state = RUN_STATE;
    }

    public String startRunTime() {
        SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        return format.format(date);
    }
}

abstract class StopState implements State {

    private static final String STOP_STATE = "Stop!!";
    protected String state;
    protected static Date date = new Date();

    public StopState() {
        this.state = STOP_STATE;
    }

    public String endStopTime() {
        SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        return format.format(date);
    }
}
```

#### 3. 일반클래스 : Run, Stop class 2개를 만들고 알맞는 추상클래스를 extends하여 인터페이스의 display() 메소드만 구현
```java
public class Run extends RunState {

    @Override
    public String display() {
        return String.format("현재 상태 %s, 상태가 시작된 시간은 %s 입니다.", state, startRunTime());
    }
}

public class Stop extends StopState {

    @Override
    public String display() {
        return String.format("현재 상태 %s, 상태가 종료된 시간은 %s 입니다.", state, endStopTime());
    }
}
```

#### 위의 구조를 확인하기 위한 애플리케이션
```java
@SpringBootApplication
public class InterfacevsabstractApplication {

    private static StateImplemnetClass normal;

    public static void main(String[] args) {
        SpringApplication.run(InterfacevsabstractApplication.class, args);

        // 시작상태 설정
        Run run = new Run();

        // sleep으로 시간과 종료 시간을 주기위한 로직
        for (int i = 0; i <3 ; i++) {
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

        // 종료상태 설정
        Stop stop = new Stop();

        // 시작상태값
        System.out.println(run.display());
        System.out.println(run.startRunTime());

        // 종료상태값
        System.out.println(stop.display());
        System.out.println(stop.endStopTime());
    }
}
/**
 * [ 출력 결과 ]
 * 현재 상태 Run!!, 상태가 시작된 시간은 2019-08-26 14:43:10 입니다.
 * 2019-08-26 14:43:10
 * 현재 상태 Stop!!, 상태가 종료된 시간은 2019-08-26 14:43:13 입니다.
 * 2019-08-26 14:43:13
 * /
```

## 마무리하며..
정리한 내용을 바탕으로 내생각을 요약하자면.....  
기본적으로 인터페이스는 다중상속(implements)이 가능하고 추상클래스는 단일 상속(extends)만 가능하며, 인터페이스의 경우에는 public과 같은 제약이 없는 접근제어자를 통한 오픈이 되어있어야 하위 클래스에서 구현이 가능하다. 반면 추상클래스는 제약을 줄 수 있으며, 인터페이스와 달리 멤버변수를 사용할 수 가 있다. 실무에서 인터페이스는 협업을 위해서 많이 사용하는 것 같다. 공통 개발을 하게 될 경우 인터페이스로 input, output을 정의하여 각각의 개발자들이 API규약을 정해놓고 사용하기에 적합하게 보이며, 추상클래스의 경우에는 아직까진 피부로 와닿지는 않지만 분산 구현된 같은 로직들을 하나로 묶어주고 같지 않은 로직들을 하위 클래스에 구현을 강제할때 사용하면 좋을 것 같다고 생각한다.  

#### [정리하며 작성한 예제소스](https://github.com/sksggg123/blog_repositroy/tree/master/interfacevsabstract/src/main/java/com/sksggg123/interfacevsabstract)