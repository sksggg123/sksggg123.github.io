---
layout: customize-posts
title: "자바의정석 - 자바(예외처리 Exception)"
date: 2019-02-10
last_modified_at: 2019-02-10
description: "남궁성님의 자바의정석을 읽고 중요하다고 생각하는 내용 정리 및 리마인드, 객체지향 프로그래밍에 대한 내용 chapter7입니다. jvm 메모리 구조에 대해서도 정리 함. 자바의정석, 남궁성, 자바, java, 객체지향, 프로그래밍, JVM, 메모리구조, memory, 클래스, 인스턴스, 객체화, 클래스 변수, 인스턴스 변수, 초기화, 초기화 블럭, 명시적 초기화, 명시적, 생성자, 매개변수, 추상클래스, abstract, 이너클래스, innerclass, 익명클래스, anonymous, 예외처리, 예외, try, catch, exception, throw, finaly"
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
category:
    - Study
tags:
    - java
published: true
sitemap:
    changefreq: daily
    priority: 1.0
---

## 예외처리 (Exception handling) 정의

프로그램이 실행준비 또는 실행중에 에러, 오류가 발생할 수 있다. 이를 발생시점에 따라 ``컴파일 에러(compile-time error), 런타임 에러(runtime error), 논리적 에러(logical error)`` 가 있다. 컴파일 에러는 말 그대로 컴파일할때 발생하는 에러이고 프로그램 실행 시에 발생하는 에러는 런타임 에러가이다. 그리고 논리적 에러는 컴파일도 잘되고 프로그램 실행도 잘되지만 의도한 것과 다르게 동작하는 것을 말한다. 예를 들면 어떠한 int를 매개변수로 받는 로직이 있다고 가정할때 해당 매개변수가 양수로 들어와야하지만 음수로 들어오게 되어 로직상 에러가 발생한다던가 의도한 대로 수행이 되지 않을때를 말한다.

>컴파일 에러 - 컴파일 시에 발생하는 에러  
>런타임 에러 - 실행 시에 발생하는 에러  
>논리적 에러 - 실행은 되지만, 의도와 다르게 동작하는 것

컴파일에러는 기본적으로 잘못된 구문이나 자료형 체크 등의 기본적인 검사를 수행을 한다. 자바에서 소스코드의 기본적인 사항을 컴파일 시 모두 걸러줄수 있지만, 실행도중 발생할 수 있는 잠재적인 오류(런타임 에러)는 잡을 수 가 없다. 이러한 런타임 에러를 방지하기 위해서는 프로그램의 실행도중 발생할 수 있는 모든 경우의 수를 고려하여 대비하는 것이 필요하다.

자바에서 실행 시 발생할 수 있는 런타임 에러를 ``'에러'와 '예외'`` 두가지로 구분하였다.

보통 에러로는 메모리부족 OOM(Out Of Memory)와 StackOverFlowError와 같이 발생하면 복구할 수 없는 심각한 에러가 있다. 정리와는 상관없지만.. 회사에서 유지보수하는 WAS서버 환경에서 죽는 경우가 있다. 이러한 현상이 있을때 서버 로그를 보면 10 중 7~8은 GC가 많이 발생한 흔적도 있으며, 최종 로그에는 Out Of Memory가 발생한 것을 종종 볼수가 있다. OOM으로 인해 프로세스가 강제로 중지된 것이다.

>에러 - 프로그램 코드에 의해서 수습될 수 없는 심각한 오류  
>예외 - 프로그램 코드에 의해서 수습될 수 있는 다소 미약한 오류

예외 클래스의 계층 구조는 아래와 같다.

```
Object
|_______ Throwable
            |_______ Excpetion 
                        |_______ IOException
                        |_______ RuntimeException
                        |_______ .......
            |_______ Error
                        |_______ .......
                        |_______ OutOfMemory
```

최상위에는 Object로 되어있으며 Exception은 Runtime, IO 등... 예외들이 있다. 세세하게 들어가면 RuntimeException 하위에는 ``ArithmeticExcpetion, ClassCastException, NullPointerException 등...``이 있다. 참고로 알아두자.

>RuntimeException클래스들은 주로 프로그래머의 실수에 의해서 발생될 수 있는 예외로 자바의 프로그래밍 요소들과 관계가 깊다.  
>Exception클래스들은 주로 외부의 영향으로 발생할 수 있는 것들로서, 프로그램의 사용자들의 동작에 의해서 발생하는 경우가 많다.

## 예외처리하기 - try catch문 (finally)

예외처리란 프로그램 실핼 시 발생할 수 있는 예기치 못한 예외의 발생에 대비한 코드를 작성하는 것이며, 예외처리의 목적은 예외의 발생으로 인한 실행중인 프로그램의 갑작스런 종료를 막고, 정상적인 실행상태를 유지할 수 있도록 하는 것이다.

```java
try {
    // 예외가 발생한 요지가 있는 소스코드..
} catch(RuntimeException re) {
    // 예외가 발생시 이를 처리하기 위한 소스코드..
} catch(IOException ie) {
    // 예외가 발생시 이를 처리하기 위한 소스코드..
} catch(Exception e) {
    // 예외가 발생시 이를 처리하기 위한 소스코드..
} finally {
    // 예외가 발생하든 안하든 무조건 터리되는 소스코드..
}
```

try블럭 안에는 예외 발생가능한 소스코드가 있을 경우 감싸주는 곳이며, catch블럭을 통해 예외발생가능 종류별로 잡아내어 예외발생 시 처리하기 위한 문이다. catch문이 없을 경우 예외처리를 하지 못한다. 여기서 IOException에 관련된 예외가 발생했을때는 첫번째 catch문을 무시하며 2번째 catch문을 받게되는데 이는 내부적으로 예외클래스의 인스턴스에 instanceof연산자를 이용해 검사를 하게되는데 true가 발생한 2번째 catch문인 IOEcption의 처리로직을 타게된다.

참고로 위의 예외 클래스의 계층 구조를 보면 Exception 안에 IOException, RuntimeException이 있다고 하였다. 3번째 catch문을 하나만 사용하여도 위의 모든 예외를 다 잡아 낼 수가 있다.

``finally``는 예외가 발생을 하게되든 안하게 되든 무조건 마지막에 수행되는 블럭 영역이다.

## 예외 발생시키기

키워드 ``throw``를 사용해서 프로그래머가 고의로 예외를 발생시킬 수 있으며 방법은 아래와 같다

```java 
Exception e = new Exception("예외 발생")
throw e;
```

## Checked와 Unchecked Exception

Checked Exception은 컴파일 단계에서 확인 가능한 예외이다. 다른 말로는 ``"Compiletime Exception"``이라고 한다. Checked Exception은 try/catch로 감싸거나 throw로 던지는 처리를 반드시 해주어야 한다. 예외처리를 컴파일러가 강제하는 것이다.

Unchecked Exception은 컴파일 단계에서 확인불가하며, 프로그램의 로직 실행중 발생한다. 다른 말로는 ``"Runtime Exception"``이라고도 한다. Unchecked Exception은 명시적인 예외처리를 하지 않아도 된다. 미리 예측하지 못했던 상황에서 발생하는 예외가 아니기 때문에 굳이 로직으로 처리를 할 필요가 없도록 만들어져 있다.

#### 참고로 Error와 그 자손도 Unchecked Exception이다. try/catch로 처리할 수 없기 때문이다.


## 메서드에 예외 선언하기

메서의 선언부에 키워드 ``throws``를 통하여 메서드 내에 발생할 수 있는 예외를 정의하면 된다. 그리고 예외가 여러 개일 경우 " , "로 구분하여 정의하면 된다.

메서드 내에서 발생할 가능성이 있는 예외를 메서드의 선언부에 명시하여 이 메서드를 사용하는 쪽에서는 이에 대한 처리를 하도록 강요한다. 메서드에 예외를 선언할 때 일반적으로 ``RuntimeException(Unchecked Exception)``클래스 들은 적지 않는다. 이들은 메서드 선언부의 throws에 선언한다고 해서 문제가 되지는 않지만 보통 반드시 처리해주어야 하는 예외들만 선언한다.

```java
// 첫 번째 예외 처리 방법
class Main {
	
	public static void main(String[] args) {
		
		try {
			int a = method();
		} catch(RuntimeException re) {
			System.out.println("Runtime Exception");
			re.getStackTrace();
		} catch(Exception e) {
			System.out.println("Exception");
			e.getStackTrace();
		}
	}
	
	static int method() throws Exception { // throws 예외 종류
		throw new Exception("예외 만들기!");
	}
}

// 두 번째 예외 처리 방법
class Main {
	
	public static void main(String[] args) throws Exception { // method() 호출 시 정의
		
		int a = method();
	}
	
	static int method() throws Exception { // throws 예외 종류
		throw new Exception("예외 만들기!");
	}
}

// Uncheced Exception(RuntimeException) 처리 방법
class Main {
	
	public static void main(String[] args) {
		
			int a = method();
	}
	
	static int method() throws RuntimeException {
		throw new RuntimeException("예외 만들기!");
	}
}
```

method()에 Exception으로 정의해두어 main메서드에서 호출 시 try/catch 혹은 호출을 하려는 곳의 메서드 선언부에 동일한 예외를 thorws 선언을 해주어야 한다. but Checked Exception만 필수로 해주어야하며 Unchecked Exception인 ``RuntimeException``은 별도로 try/catch 혹은 호출하는 곳의 메서드 선언부에 정의할 필요가 없다.

## 사용자정의 예외 만들기

프로그래머가 새로운 예외 클래스를 정의하여 사용할 수 있다. 보통 Exception 클래스로부터 상속받는 클래스를 만들지만 필요에 따라서 알맞은 예외 클래스를 선택할 수 있다. 참고로 Exception클래스는 생성 시에 String값을 받아서 메시지로 저장 할 수 있다.

```java
class MyException extends Exception {
    MyExecption(String msg) { // 문자열을 매개변수로 받는 생성자
        super(msg); // 부모클래스인 Exception클래스의 생성자를 호출
    }
}
```

## 예외 되던지기(Exception re-throwing)

한 메서드에서 발생할 수 있는 예외가 여럿인 경우, 몇 개는 try/catch문을 통해서 메서드 내에서 자체적으로 처리하고, 나머지는 선언부에 지정하여 호출한 메서드에서 처리하도록 한다. 단 하나의 예외에 대해서도 예외가 발생한 메서드와 호출한 메서드 양쪽에서 처리하도록 할 수 있다. catch문에서 필요한 작업을 수행 한 후 ``throw``문을 사용해서 예외를 다시 발생시킨다. 중요한 점은 선언부에 발생할 예외를 throws에 지정해줘야 한다.

```java
class Main {
	
	public static void main(String[] args) {
		try {
			method(); // method() 에서 1차예외 발생 시 처리 후 재처리 요청 
		} catch (Exception e) {
			e.printStackTrace(); // 2차 예외처리 
		}
	}
	
	static int method() throws Exception { // 선언부에 thorws 정의 중요!
		try {
			throw new Exception("새로운 예외 발생!!"); // 강제로 예외 생성하여 catch문으로 이
		} catch(Exception e) {
			// 1차로 예외처리 한다.
			// 예를 들어 발생시킨 예외이기에 처리로직이 따로 없음..
			
			e.getStackTrace();
			throw e; // try에서 발생한 예외를 위에서 1차 로직으로 처리한후 다시 예외를 발생시킨다.
		}
	}
}
```

###### 위의 모든 정리내용은 자바의 정석을 공부하며 복습차 정리한 내용입니다. 