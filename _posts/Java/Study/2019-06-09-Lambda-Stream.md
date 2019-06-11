---
layout: customize-posts
title: "자바의정석 - 람다와 스트림"
date: 2019-06-09
last_modified_at: 2019-06-09
description: "남궁성님의 자바의정석을 읽고 중요하다고 생각하는 내용 정리 및 리마인드, 객체지향 프로그래밍에 대한 내용 chapter7입니다. jvm 메모리 구조에 대해서도 정리 함. 자바의정석, 남궁성, 자바, java, 객체지향, 프로그래밍, JVM, 메모리구조, memory, 클래스, 인스턴스, 객체화, 클래스 변수, 컬렉션, 지네릭스, 인스턴스 변수, 초기화,
초기화 블럭, 명시적 초기화, 명시적, 생성자, 매개변수, 추상클래스, abstract, 이너클래스, innerclass, 익명클래스, anonymous, 예외처리, 예외, try, catch, exception, throw, finaly java.lang package, util class, object, String, literal, 리터럴, Objects, wrapper, StringBuffer, String, date, calendar, simpledateformat, format, Collection, list, set, map, hash, hashMap, iterator, arraylist, linkedlist, stack, queue, Generics, 지네릭스, 람다, 스트림, Lambda, Stream"
header:
    teaser: /assets/images/blog/java-logo.png
    og_image: /assets/images/blog/java-logo.png
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
    - 예외처리
    - 예외
    - exception
    - try
    - catch
    - finaly
    - throw
    - Object
    - equals
    - wrapper
    - String
    - StringBuffer
    - Date
    - Calendar
    - format
    - 지네릭스
    - generics
    - Thread
    - 스레드
    - 쓰레드
    - Daemon
    - 데몬
    - ThreadGroup
    - Lambda
    - Stream
    - 람다
    - 스트림
category:
    - Java
    - Study
tags:
    - java
published: false
sitemap:
    changefreq: daily
    priority: 1.0
---

## 람다식이란?

메서드를 하나의 **'식(expression)'** 으로 표현한 것이다. 메서드를 람다식으로 표현하면 메서드의 이름과 반환값이 없어지므로, 람다식을 **'익명 함수'** 라고도 한다.  
```java
// Method 표현
int method(int i) {
    return (int) (Math.random()*5) +1 ;
}

// Lambda 표현
int[] arr = new int[5];
Arrays.setAll(arr, i -> (int) (Math.random()*5) +1);
```
메서드로 표현한 것과 람다식으로 표현한 것의 차이점은, 모든 메서드는 클래스에 포함되어야 한다는 것과 람다식은 그렇지 않다는 것이 있다. 게다가 람다식은 메서드의 매개변수로 전달되어지는 것이 가능하고, 메서드의 결과로 반홚될 수도 있다. 한마디로 메서드를 변수처럼 다루는 것이 가능한 것이다.  

## 람다식 작성하기

첫째, 람다식은 **'익명 함수'** 답게 메서드에서 이름과 반환타입을 제거하고 매개변수 선언부와 몸통{} 사이에 '->' 를 추가한다. 참고로 알아둘 사항은 람다**식** 이므로 끝에 ';'를 붙이지 않고 매개변수의 타입은 추론이 가능한 경우는 생략할 수 있다. 또한 배개변수가 하나뿐인 경우에는 괄호()를 생략할 수 있다. 단, 매개변수의 타입이 있으면 괄호()를 생략할 수 없다.  
```java
// Method 표현
반환타입 메서드이름(매개변수 선언) {
    문장들..
}

// Mthod 예제
int max(int a, int b) {
    return a > b ? a : b;
}

// Lambda 표현
(매개변수 선언) -> {
    문장들
}

// Lambda 예제
(a,b) -> a > b ? a : b
```

## 람다식 사용해보기

```java
public class Main {

    public static void main(String[] args) {

        // Lamda 식
        int[] arr = new int[5];
        Arrays.setAll(arr, i -> (int) (Math.random() * 5) + 1);

        for (int i : arr) {
            System.out.println(i);
        }

    }
    // Method 표현
    static int method(int i) {
        return (int) (Math.random()*5) +1 ;
    }
}
```

```java
public class FunctionMethod {

    @FunctionalInterface
    public interface Sum {

        int sum(int num1, int num2);
    }

    public static void main(String[] args) {
        Sum function = (num1, num2) -> num1 + num2;

        System.out.println(function.sum(10, 20));
    }
}
```



#### 위의 모든 정리내용은 자바의 정석을 공부하며 복습차 정리한 내용입니다. 
