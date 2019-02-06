---
layout: customize-posts
title: "개인공부 - 자바(객체지향프로그래밍II)"
date: 2019-02-06
last_modified_at: 2019-02-06
description: "남궁성님의 자바의정석을 읽고 중요하다고 생각하는 내용 정리 및 리마인드, 객체지향 프로그래밍에 대한 내용 chapter6입니다. jvm 메모리 구조에 대해서도 정리 함. 자바의정석, 남궁성, 자바, java, 객체지향, 프로그래밍, JVM, 메모리구조, memory, 클래스, 인스턴스, 객체화, 클래스 변수, 인스턴스 변수, 초기화, 초기화 블럭, 명시적 초기화, 명시적, 생성자, 매개변수"
header:
    teaser: /assets/images/blog/자바의정석_객체지향1_1.jpeg
    og_image: /assets/images/blog/자바의정석_객체지향1_1.jpeg
keywords:
    - 자바의정석
    - 남궁성
    - 자바
    - java
    - 객체지향
    - 프로그래밍
    - JVM
    - 메모리구조
    - memory
    - 클래스
    - 인스턴스
    - 객체화
    - 클래스 변수
    - 인스턴스 변수
    - 초기화 
    - 초기화 블럭
    - 명시적 초기화
    - 명시적
    - 생성자
    - 매개변수
    - 상속
    - inheritance
    - 제어자
    - Modifier
    - 오버라이딩
    - Override
category:
    - Study
tags:
    - java
published: false
sitemap:
    changefreq: daily
    priority: 1.0
---


## 상속(Inheritance)

상속이란 기존의 클래스를 재사용하여 새로운 클래스를 작성하는 것이다. 선언은 상속받고자 하는 클래스를 **extends**와 함께 선언해주면 된다. 상속을 받게되면 부모클래스의 멤버변수를 그대로 자식클래스가 상속을 받게되어 사용가능하다.  

자바에서 상속은 단일 상속밖에 되지 않는다. ```class singleExtends extends A``` 으로 정의할 수 있지만 ```class singleExtends extends A, B``` 와 같이 다중으로 상속을 할 수가 없다. 만일 다중상속이 필요할 경우 아래와 같이 표현 할 수는 있다.  

```java
class Computer {
    String mainborad;
    String cpu;
    String graphicCard;
}

class InputDevice {
    String keyboard;
    String mouse;
}

class Display {
    String monitor;
}

class MyComputer extends Computer {
    InputDevice id = new InputDevice();
    Display dp = new Display();
    String sepaker;
}
```

상속은 Computer class 를 받고 InputDevice, Display class는 인스턴스로 내부로 선언하여 사용하면 된다.

## 오버라이딩

부모클래스에 정의된 메서드를 상속받은 자식클래스가 재정의를 하는것을 **오버라이딩** 이라고 한다. 오버라이딩의 조건은 아래와 같다.
1. 이름이 같아야 한다.
2. 매개변수가 같아야 한다.
3. 반환타입이 같아야 한다.

부모클래스와 자식클래스의 선언부가 서로 일치해야한다는 의미인데, 접근제어자와 예외처리의 제한 조간만 다를 수 있다.  

``접근제어자``의 경우에는 더 좋은 범위로 변경을 할 수가 없다. 예를 들면 부모클래스의 메서드가 protected로 선언이 되어있다면 자식클래스의 오버라이딩을 하려는 메서드는 private로 선언을 할 수 없다는 의미이다.  

``예외처리``의 경우에는 부모클래스의 메서드에 선언된 예외처리의 개수보다 많게 오버라이딩을 할 수가 없다. 예를들면 ``부모클래스 메서드에 IOException, SQLexception``가 정의가 되어있다고 하면 ``자식클래스의 오버라이딩할 메서드에는 IOExeption으로 정의``만은 가능하다는 의미이다. 여기서 주의해야할 점은 자식클래스의 오버라이딩할 메서드에 **Exception**과 같이 모든 예외의 최상위를 정의할 경우 문제가 발생한다. 최상위 예외조건은 모든 경우를 포함하기에 부모클래스 메서드에 정의한 예외 개수 2개보다 많은 것이다.

>참고)
>부모클래스에 정의 된 static메서드를 자식클래스에서 똑같은 이름의 static메서드로 정의할 수 있지만 이것은 각 클래스에 별개의 static메서드를 정의한 것일 뿐 오버라이딩이 아님.  
>static멤버들은 자신들이 정의된 클래스에 묶여있다고 생각하면 된다.

## 제어자(Modifier)

제어자는 클래스, 변수 또는 메서드의 선언부에 함께 사용되어 부가적인 의미를 부여한다. 제어자의 종류는 크게 접근 제어자와 그 외의 제어자로 나눌 수 있다.
>접근제어자 - public, protected, default, private  
>그 외 -  static, final, abstract, native, transient, synchronized, volatile, strictfp

### static

static은 클래스에 종속된 걸로 보면 된다. 일반적으로 static이 붙지 않은 변수에 class가 있다고 하면 인스턴스화를 여러번 할 경우 각각의 변수는 멤버변수로 독립적인 값을 갖는다. 하지만 static이 붙은 변수일 경우는 여러번 인스턴스화를 하여도 모든 값이 공유되어 같은 값을 갖는다.

### final

final의 경우 변경될 수 없는 성격을 갖고 있다. 보통 상수를 선언할때 사용을 많이 한다. ``final int MAX = 10;``와 같이 고정적으로 변경하지 않는 값(상수)를 정의할때 많이 사용한다. 추가로 알아둬야할 내용은 메서드에 final이 붙을 경우 자식클래스가 해당 메서드는 오버라이딩을 할 수가 없고, 클래스에 사용할 경우 extends를 애초에 받을 수 가 없다. 이유는 변경을 할 수 없는 성격을 갖고 있기 때문에 오버라이딩을 하여 재구성을 할 수 없기 때문이다. 

### 접근 제어자 (Access Modifier)

접근 제어자는 멤버 또는 클래스에 사용되어 외부에서 접근하지 못하도록 설정을 할때 사용을 한다. 보통 ``접근 제어자``를 사용하는 이유는 클래스 내부에 선언된 데이터를 보호 하려는 목적이다. 객체지향의 개념중 중요한 캡슐화에 해당하는 내용이다. 

> public > protected > default > private  

정확한 범위늰 아래의 표를 보자

[접근제어자 범위 표]

|제어자|같은 클래스|같은 패키지|자식 클래스|전체|
|-|-|-|-|-|
|public|O|O|O|O|
|protected|O|O|O|X|
|default|O|O|X|X|
|private|O|X|X|X|

private은 같은 클래스 내에서만 사용하도록 제한한 가장 높은 조건 이다. protected의 경우 전체적으로 봤을때 자식클래스에서 접근이 가능하다고 보면 된다. public의 경우 모든 곳에서 접근이 가능하다. 위의 접근제어로 정의된 상태를 볼때 현업에서 소스 수정이 이루어졌을 경우 테스트의 범위를 조금이나마 판단하는데 용이 할 것으로 보인다. public으로 설정된 경우 호출된 모든 곳이기에 소스를 전체적으로 봐야겠지만, private로 설정된 경우 같은 클래스 내부를 중적으로 확인하고 추가로 호출된 부분이 있는지만 보면된다. 

위에 정리한 접근 제어자를 소스 코드를 통해 정리를 해보면 아래와 같이 볼 수 있다.

```java
public class AllAccess {
    private String dbConnectUrl;
    private String dbUserId;
    private String dbPassword;

    public setDbConectUrl(String dbConnectUrl) {
        this.dbConnectUrl = dbConnectUrl
    }
    public getDbConectUrl() {
        return this.dbConnectUrl;
    }
    public setDbUserId(String dbUserId) {
        this.dbUserId = dbUserId;
    }
    public getDbUserId() {
        return this.dbUserId;
    }
    public setDbPassword(String dbPassword) {
        this.dbPassword = dbPassword;
    }
    public getDbPassword() {
        return thus.dbPassword
    }
}

public class Main() {
    AllAccess all = new AllAccess();

    all.dbConnectUrl = "https://~" // 이러면 안된다 접근할 수 없다
    all.setDbConnetUrl("https://~"); // 이렇게 public으로 접근할 수 있게 해둔 메서드를 통해 변수에 접근해야 한다.
}
```

아래는 제어자를 조합해서 사용할 때 주의해야 할 사항이다.
1. 메서드에 static과 abstract를 함께 사용할 수 없다.
    - static메서드는 몸통이 있는 메서드에만 사용할 수 있기 때문이다.
2. 클래스에 abstract와 final을 동시에 사용할 수 없다.
    - 클래스에 사용되는 final은 클래스를 확장할 수 없다는 의미이고 abstract는 상속을 통해서 완성되어야 한다는 의미이므로 서로 모순되기 때문이다.
3. abstract메서드의 접근 제어자가 private일 수 없다.
    - abstract메서드는 자식클래스에서 구현해주어야 하는데 접근 제어자가 private이면, 자식 클래스에서 접근할 수 없기 때문이다.
4. 메서드에 private와 final을 같이 사용할 필요는 없다.
    - 접근 제어자가 private인 메서드는 오버라이딩 될 수 없기 때문이다. 이 둘 중 하나만 사용해도 의미가 충분하다.

###### 위의 모든 정리내용은 자바의 정석을 공부하며 복습차 정리한 내용입니다. 