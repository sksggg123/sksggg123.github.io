---
layout: customize-posts
title: "개인공부 - 자바(추상클래스, 인터페이스, 내부클래스, 익명클래스)"
date: 2019-02-08
last_modified_at: 2019-02-08
description: "남궁성님의 자바의정석을 읽고 중요하다고 생각하는 내용 정리 및 리마인드, 객체지향 프로그래밍에 대한 내용 chapter7입니다. jvm 메모리 구조에 대해서도 정리 함. 자바의정석, 남궁성, 자바, java, 객체지향, 프로그래밍, JVM, 메모리구조, memory, 클래스, 인스턴스, 객체화, 클래스 변수, 인스턴스 변수, 초기화, 초기화 블럭, 명시적 초기화, 명시적, 생성자, 매개변수, 추상클래스, abstract, 이너클래스, innerclass, 익명클래스, anonymous"
header:
    teaser: /assets/images/blog/java-logo.png
    og_image: /assets/images/blog/java-logo s.png
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
    - 다형성
    - Polymorphism
    - casting
    - cast
    - 추상클래스
    - abstract
    - 이너클래스
    - innerclass
    - 익명클래스
    - anonymous
category:
    - Study
tags:
    - java
published: true
sitemap:
    changefreq: daily
    priority: 1.0
---

## 추상클래스(abstract class)

**추상클래스**는 "미완성 설계도"에 비유할 수 있다. 클래스가 미완성이라는 거은 멤버의 개수에 관계된 것이 아니라 단지 미완성 메서드(추상 메서드)를 포함하고 있다는 의미이다. 중요한 점은 ``추상클래스는 인스턴스를 생설할 수 없다.`` 또한 ``상속을 통해서 자식클래스에 의해서만 완성(구현)될 수 있다.`` 생성 키워드는 class 앞에 ``"abstract"``를 붙이기만 하면 된다. 이렇게 함으로써 이 클래스를 사용할 때는 상속을 받아 구현을 해주어야 된다는 의미이다.

**추상메서드**는 역시 키워드 ``abstract``를 앞에 붙여 주고, 추상메서드는 구현부가 없으므로 ``괄호{}``대신 문장의 끝을 알리는 ``';'``을 적어준다. 상속받은 추상메서드 중 하나라도 구현하지 않는다면, 자식클래스 역시 추상클래스로 지정해 주어야 한다. 기본적으로 추상클래스를 작성할때는 우선 클래스 구조를 잡은 뒤 **공통적**으로 사용하는 메서드가 있을 경우 추출하여 부모클래스로 생성하는 것이 기본작성방식이다.

>추상화 - 클래스간의 공통점을 찾아내서 공통의 부모클래스를 만드는 작업  
>구체화 - 상속을 통해 클래스를 구현 확장하는 작업  

아래는 추상클래스와 추상메서드를 작성하는 예제이다.

```java
abstract class AbstractClassSample {
// 키워드             클래스 이름
    abstract void abstractMethod1();
    // 키워드 리턴타입   메서드 이름

    abstract void abstractMethod2(int a);
}

class SampleClass1 extends AbstractClassSample {
    void abstractMethod1() {

    }
    void abstractMethod2(1) {

    }
}

abstract class SampleClass2 extends AbstractClassSample {
    void abstractMethod1() {

    }
    // 상속받은 추상클래스 AbstractClassSample의 메서드 abstractMethod2()를 구현하지 않았기에
    // SampleClass2 앞에 키워드 'abstract'를 붙여 준 것이다.
}
```

추상클래스를 보았을때는 굳이(?) class를 생성할때 ``abstrac``를 붙여주어 작성해야 할까? 라는 의문이 들 수가 있다. 기본적은로 class를 작성하여 필요한 곳에 extends를 하여 사용하여도 같은 의미겠으나 abstract를 붙여줌으로써 상속받은 class에서 추상메서드의 구현을 강제할 수 있기에 필수 공통부분을 구현해야할 경우 사용에 적합하다.

## 인터페이스(interface)

인터페이스는 일종의 추상클래스이다. 추상클래스보다 추상의 정도가 높아 ``구현이 없는 메서드``와 ``멤버변수를 구성원으로 가질 수 없다.`` 오직 추상메서드와 상수만을 멤버로 가질 수 있으며 그외에 어떠한 요소도 허용하지 않는다. ``추상클래스 = "미완성 설계도" 라면, 인터페이스 = "기본 설계도"``라고 생각을 하면 된다.

인터페이스의 작성은 키워드 class 대신에 ``interface``로 선언하면 되며 접근제어자로는 public과 default를 사용하면 된다. 단지 class와의 차이인 제약조건이 있다.
1. 모든 멤버변수는 public abstraact final 이어야 하며, 생략할 수 있다.
2. 모든 메서드는 public abstract 이어야 하며, 생략할 수 있다.

이전에 정리한 글[[자바(객체지향프로그래밍2)](https://sksggg123.github.io/study/Study_java_oop2/)] 에서 언급한 다중상속이 있다. 상속은 단일 상속밖에 안되지만 인터페이스의 경우 다중으로 선언할 수 있다.

```java
interface Movable {
    void move(int x, int y);
}

interface Attackable {
    void attack(Unit u);
}

interface Fightable extends Movable, Attackable {

}
```

인터페이스 선언후 구현은 ``implements``를 사용하면 된다. 일부만을 구현한다면 ``abstract``을 붙여 추상클래스로 선언을 하고 상속과 인터페이스 구현을 하나의 class에서 선언할 수 있다.  
예를 들면 이렇게 사용을 하면 된다. ``class Fighter extends Unit implements Fightable { }``

### 인터페이스를 이용한 다형성

인터페이스 역시 이를 구현한 클래스의 부모라 할 수 있으므로 해당 인터페이스 타입의 참조변수로 이를 구현한 클래스의 인스턴스를 참조할 수 있으며, 인터페이스 타입으로의 형변환도 가능하다. 그리고 메서드의 리턴타입으로 인터페이스의 타입을 지정한것이 가능하다. 리턴타입이 인터페이스 곧 객체이기에 인스턴스화 하여 반환을 하게된다.

인터페이스의 장점으로는 아래와 같다.
1. 개발시간 단축
2. 표준화 가능
3. 서로 관계없는 클래스들에겍 관계를 맺어 줌
4. 독립적인 프로그래밍 가능

## 내부 클래스(inner class)

내부 클래스는 클래스 내에 선언된 클래스 이다. 두 클래스의 멤버들 간에 서로 쉽게 접근할 수 있다는 장점과 외부에는 불필요한 클래스를 감춤으로 객체지향의 특징인 **캡슐화**가 가능하다. 내부 클래스의 경우 AWT나 Swing과 같은 GUI어플리케이션에서 사용되지 그 외에서는 잘 사용하지 않는다고 한다. 그냥 이런 개념이 있다 정도로만 숙지하면 될 것으로 판단된다.

```java
// 일반적인 class의 구조
class A {
    // ...
}
class B {
    // ...
}

// 내부 클래스를 사용한 구조
class A {
    // ...
    class B {
        // .....
    }
}
```

[내부 클래스의 종류와 특징 표]
내부 클래스의 종류는 변수의 선언위치에 따른 종류와 같다. 변수의 선언위치에 따라 인스턴스변수, 클래스변수(static 변수), 지역변수로 구분 된다.

|내부 클래스|특  징|
|--------|-----|
|인스턴스 클래스|외부 클래스의 멤버변수 선언위치, 외부 클래스의 인스턴스 멤버들과 관련 된 작업에 사용될 목적으로 선언|
|스태틱 클래스|외부 클래스의 멤버변수 선언위치에 선언, static멤버처럼 다루어지며 static변수, static메서드에서 사용 될 목적으로 선언|
|지역 클래스|외부 클래스의 메서드나 초기화 블럭안에 선언, 선언된 영역 내부에서만 사용|
|익명 클래스|클래스의 선언과 객체의 생성을 동시에 하는 이름없는 클래스(일회용)|

## 익명 클래스(anonymous class)

익명 클래스는 특이하게도 다른 내부 클래스들과는 달리 이름이 없다. 생성자도 가질 수 없으며 오로지 단 하나의 클래스를 상속받고나 단 하나의 인터페이스만을 구현할 수 있다.

```java
class EventHandler implements ActionListener {
    public void actionPerformed(ActionEvent e) {
        System.out.println("ActionEvent occurred");
    }
}

class main {
    public static void main(String[] args) {
        Button b = new Button("Start");
        b.addActionListener(new EventHandler());
    }
}

// 익명 클래스로 바꾸면
class main {
    public static void main(String[] args) {
        Button b = new Button("Start");
        b.addActionListener(new ActionListener() {
                public void actionPerformed(ActionEvent e) {
                    System.out.println("ActionEvent occurred");
                }
            } // 익명 클래스의 끝
        );
    }
}


```

###### 위의 모든 정리내용은 자바의 정석을 공부하며 복습차 정리한 내용입니다. 