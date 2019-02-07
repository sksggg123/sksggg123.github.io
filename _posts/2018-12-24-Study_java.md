---
layout: customize-posts
title: "개인공부 - 자바란?"
date: 2018-12-24
last_modified_at: 2018-12-25
description: "2018.12 4째주 공부내용. java 시작. 자바의 특징, 캡슐화, 상속화, 다형성, jvm 공부하며 기록삼아 정리한 내용"
header:
    teaser: /assets/images/blog/java-logo.png
    og_image: /assets/images/blog/java-logo.png
keywords:
    - study
    - 공부
    - java
    - 캡슐화
    - 모듈화
    - 다형성
    - 상속화
    - jvm
category:
    - Study
tags:
    - java
published: true
sitemap:
changefreq: daily
priority: 1.0
---

## **자바의 특징**

## **첫째, 운영체제에 독립적이다.**  
자바는 한곳의 OS를 대상으로 Application을 만들어도 다른 OS에 적용이 가능하다.  
**JVM(Java Virtual Machine)** 이 OS와의 통신을 담당하기 때문이다.  

|Dept| Java Application         | 다른 Application |
|----|--------------------------|------------------|
|1   |Application               |Application       |
|2   |JVM (Java Virtual Machine)|OS                |
|3   |OS                        |HardWare          |
|4   |HardWare                  |                  |

위처럼 자바의 실행 과정을 보면 중간에 **JVM**이 있다. 자바에서 작성한 코드 즉, Application은 오로지 JVM만을 보며 JVM은 각 OS별로 구분이 된다. 일반 적으로 우리가 자바 Application을 만들기위해 환경설정을 할떼 JDK를 설치하는 것이 JVM 설정을 하는 것으로 이해하면 된다.  

단점으로는 Application을 실행하는 Dept가 다른 Application보다 하나가 더 있기에 속도적인 문제가 분명있다. 현재 많이 개선되고 개선중이라고는 하지만 절차가 하나가 더있는 것은 기타 다른 언어로 작성된 Application에 비해 속도가 느릴 수 밖에는 없다. 

> 결론: Write Once, run anywhere 한번 작성하면 어디스든 실행이 된다.

## **둘째, 객체지향적인 언어이다.**  
객체지향의 3요소인 **상속성**, **캡슐화**, **다형성**이 있다.

**상속성**의 개념은,  
부모 Class에 정의된 필드와 메소드를 자식 Class가 물려받는 개념이다.

|부모 A class|자식 A Class|
|-|-|
|A|A -> 부모 Class로 부터 받은 속성|
|B|B -> 부모 Class로 부터 받은 속성|
|C|C -> 부모 Class로 부터 받은 속성|
||D -> 자식 Class만의 속성|

|부모 A class|자식 B Class|
|-|-|
|A|A -> 부모 Class로 부터 받은 속성|
|B|B -> 부모 Class로 부터 받은 속성|
|C|C -> 부모 Class로 부터 받은 속성|
||F -> 자식 Class만의 속성|

|자식 A class|자식 C Class|
|-|-|
|A|A -> 자식 A Class로 부터 받은 속성|
|B|B -> 자식 A Class로 부터 받은 속성|
|C|C -> 자식 A Class로 부터 받은 속성|
|D|D -> 자식 A Class로 부터 받은 속성|
||G -> 자식 C Class만의 속성|

**캡슐화**의 개념은,  
관련있는 것들을 한곳으로 모아두며, 외부에서는 실제로 구현한 내용을 모르게 하기위해 캡슐로 감싼다(?)로 이해하면 된다.  

[캡슐화X]
```java
class A {
    public int a, b
    public int sum;
}

public class main {
    public static void main(String[] args) {
        A a = new A();
        a.sum = a.a + a.b;
    }
}
```

여기서 Class A에는 a,b 변수를 sum하는 로직으로 구현되어있다. 하지만 캡슐화가 되어있지는 않다.  
그 이유는, 외부에서 실제로 ```java a.sum = a.a + a.b; ``` 부분을 보면 로직 자체를 알게 된다. 더군다나 sum의 public 제어접근자를 사용해서 어디서든 변경이 가능하게 되어있다.  

[캡슐화O]
```java
class A {
    public int a, b
    private int sum;

    public int cap() {
        this.sum = a + b;
        return this.sum;
    }
}

public class main {
    public static void main(String[] args) {
        A a = new A();
        a.a = 10;
        a.b = 10;
        a.sum = a.cap();

        System.out.printf("a와 b의 sum:" + a.sum );
    }
}

---
출력결과 : a와 b의 sum:20
---
```
여기서 핵심은 ```java  a.sum = a.cap(); ```이다.  
class A의 cap() 메소드가 sum이라는 로직을 가지고 있으며 Application에서는 cap의 내부로직은 모른체 호출을 하면 된다.  

참고) 접근제어자의 범주

||default|private|protected|public|
|-|-|-|-|-|
|같은 패키지의 클래스|O|X|O|O|
|다른 패키지의 클래스|X|X|X|O|
|같은 패키지의 서브 클래스|O|X|O|O|
|다른 패키지의 서브 클래스|X|X|O|O|

**다형성**의 개념은,  
하나의 메소드나 클래스가 있을 때 이것들이 다양한 방법으로 동작하는 것을 의미한다.  
키보드의 키를 통해서 비유를 많이들 하고있다. 키보드의 키를 사용하는 방법은 '누른다'이지만, Insert, Delete의 목적은 각각 삽입과 삭제의 기능을 한다.   다형성이란 동일한 조작방법으로 동작시키지만 동작방법은 다른 것을 의미한다.  

다형성에는 **Overriding, Overloading**이 있다.  
Overriding은 기존에 정의되어있는 class의 메소드를 extends 받아 동일한 메소드지만 다른 역할을 하게 구현하는 것이다.

```java
class A {
    public int a, b
    private int sum;

    public int cap() {
        this.sum = a + b;
        return this.sum;
    }
}

class B extends A {
    public int a, b
    private int sum;

    public int cap() {
        this.sum = a * b;
        return this.sum;
    }
}

public class main {
    public static void main(String[] args) {
        A a = new B();
        a.a = 10;
        a.b = 10;
        a.sum = a.cap();

        System.out.printf("a와 b의 sum(곱셈):" + a.sum );
    }
}

---
출력결과 : a와 b의 sum:400
---
```

여기서 class A에서는 ```java sum = a + b ```으로 사용되었다.  
하지만 class B에서는 ```java sum = a * b ```으로 사용하고 싶다.
sum이지만 나는 sum으로 사용을 안하고 곱하기로 사용하고 싶을때는 extends를 받아 overriding을 하여 사용할 수 있다.

Overloading은 class 내에 동일한 이름의 메소드를 여러개 갖는 개념이다. 단, 인자값(파라미터)는 달라야 한다.  
인자들의 타입이나 개수가 다르면 메소드 이름은 갖더라도 인자값의 구분을 확인하여 호출이 가능하다.

## **셋째, 자동메모리 관리가 가능하다**  
자바로 작성된 프로그램이 실행이 될 경우 **Garbage Collection**이 자동적으로 메모리 관리를 해준다.  
만일 **Garbage Collection**없다면 프로그램을 구현할때 메모리 관리해주는 로직도 추가가 되야 하기에 수동으로 관리를 해줘야 된다. 

## **넷째, 멀티쓰레드(Multi-Thread)가 가능하다**  
**멀티쓰레드(Multi-Thread)**의 경우에는 지원하는 운영체제에 따라 구현하는 방법이 다르다.  
하지만 자바에서는 JVM에 의해 운영체제와 상관없이 구현이 가능하다.

## **자바의 동작원리**  
```java
class A {
    public int a, b
    public int sum;
}

public class main {
    public static void main(String[] args) {
        A a = new A();
        a.sum = a.a + a.b;
    }
}
```

위의 예제 소스가 Test.java 파일이라고 가정해보자  
Test.java를 작성이 완료되어 실행을 시키려면 우선 **컴파일**(javac.exe)을 하여 Test.class 파일을 생성해야 한다.  
그 후 자바의 인터프리터(java.exe)로 실행을 하게 된다.  

참고로 ```java public static void main(String[] args)```는 main메서드의 선언부이다. 프로그램을 실행 할 때(java.exe) 호출이 될 수 있도록 약속된 부분이기에 항상 똑같이 적어 주어여 한다.

[java application 실행 절차]
1. 프로그램 작성
    * 고급업어
    * Test.java
2. 기계어로의 번역
    * 컴파일
    * javac Test.java -> Test.class 생성
3. 프로그램 실행
    * Test.class 파일을 로드한다.
    * 클래스파일 검사 (파일형식, 악성코드 등...)
    * ```public static void main(String[] args)``` 를 호출한다.
    * java Test -> 결과물 출력

main 메서드의 첫 줄부터 코드가 실행되기 시작하여 마지막 코드까지 모두 실행되면  프로그램이 종료되고, 프로그램에서 사용했던 자원들은 모두 반환된다.

## **변수의 명명 규칙**

변수의 이름은 식별자라고도 하며, 같은 영역내에서는 서로 다른 식별자로 되어있어야 한다.  
아래에는 식별자 생성 규칙이다.

1. 대소문자가 구분되며, 길이에 제한이 없다.
2. 예약어를 사용해서는 안 된다.
3. 숫자로 시작해서는 안 된다.
4. 특수문자는 " _ " 와 " $ " 만 가능하다.

|예약어의 종류|||||
|-|-|-|-|-|
|abstract|default|if|package|this|
|assert|do|goto|privae|throw|
|boolean|double|implements|protected|throws|
|break|else|import|public|transient|
|byte|enum|instanceof|return|true|
|case|extends|int|short|try
|catch|false|interface|static|void|
|char|final|long|strictfp|volatile|
|class|finally|native|super|while|
|const|float|new|switch|
|contine|for|null|sysnchronized|

이 외에도 꼭 지켜야 하는 것은 아니지만 많은 선후배 개발자 분들과의 암묵적인 규칙이 있다.
1. 클래스 이름의 첫 글자는 항상 대문자
2. 여러 단어로 이루어진 이름은 단어의 첫 글자를 대줌자로 한다
    * ex) currentDate
3. 상수의 이름은 모두 대문자, 여러 단어로 이루어진 경우 " _ " 로 구분
    * PI, CURRENT_DATE

변수의 명명 규칙은 반드시 지켜야하는 규칙은 아니지만 가독성적인 면에서나 위의 규칙들로 생성을 하는것이 좋다.

