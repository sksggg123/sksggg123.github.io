---
layout: customize-posts
title: "자바의정석 - 쓰레드의 동기화"
date: 2019-03-25
last_modified_at: 2019-03-25
description: "남궁성님의 자바의정석을 읽고 중요하다고 생각하는 내용 정리 및 리마인드, 객체지향 프로그래밍에 대한 내용 chapter7입니다. jvm 메모리 구조에 대해서도 정리 함. 자바의정석, 남궁성, 자바, java, 객체지향, 프로그래밍, JVM, 메모리구조, memory, 클래스, 인스턴스, 객체화, 클래스 변수, 컬렉션, 지네릭스, 인스턴스 변수, 초기화,
초기화 블럭, 명시적 초기화, 명시적, 생성자, 매개변수, 추상클래스, abstract, 이너클래스, innerclass, 익명클래스, anonymous, 예외처리, 예외, try, catch, exception, throw, finaly java.lang package, util class, object, String, literal, 리터럴, Objects, wrapper, StringBuffer, String, date, calendar, simpledateformat, format, Collection, list, set, map, hash, hashMap, iterator, arraylist, linkedlist, stack, queue, Generics, 지네릭스, 쓰레드, 동기화, wait, synchronized"
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
    - synchronized
    - 동기화
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

## 쓰레드의 동기화

#### [전편](https://sksggg123.github.io/java/study/Thread/)에 이어 쓰레드의 동기화 관련해서 정리하고자 한다. 

싱글쓰레드 환경에서는 프로세스 내에 하나의 쓰레드로 작업이 수행되기에 데이터의 사용에 문제가 없지만 멀티쓰레드의 환경에서는 이야기가 달리진다. 여러 쓰레드가 자원을 공유하여 작업을 하기에 서로의 작업에 영향을 주게 된다. 1,2번 2개의 쓰레드가 있고, 동일한 자원(객체)를 활용하여 작업이 진행된다고 가정해보자. 이때 1번 쓰레드의 작업 진행 2번 쓰레드에 제어권이 넘어가게 되고 동일 자원(객체)에 변경에 이루어 진다면 1번 쓰레드의 작업결과가 원하는 값이 도출되지 못 할 것이다. 이러한 발생을 방지하기 위해 자원을 방해받지 않는 개념이 ``임계 영역(critical section)``과 ``잠금(Lock)`` 개념이다.

공유할 자원에 대한 소스코드 영역을 임계 영역으로 지정해놓고 공유 자원(객체)에 Lock을 하나의 쓰레드가 획득하여 사용하게 하는 것이며 Lock을 획득한 쓰레드 이외에는 다른 쓰레드에서는 자원을 사용하지 못하게 하는 것이다. Lock을 획득한 쓰레드가 자원 사용을 완료하여 Lock을 반납하게되면 다른 쓰레드에서 접근하여 사용할 수 있게 된다. 이러한 방법으로 하나의 쓰레드가 진행중일때 다른 쓰레드가 자원에 간섭하지 못하게 막는 것을 ``쓰레드의 동기화(Syncronization)``이라고 한다.

## synchronized를 이용한 동기화

동기화 방법에는 몇가지가 있지만 가장 간단한 ``synchronized``키워드를 이용한 동기화에 대해 살펴보면 사용법은 2가지가 있다. 메서드 앞에 키워드를 붙이게 되면 메서드 자체가 임계 영역으로 설정이되며, 메서드 호출시점부터 영역내의 모든 객체에 lock을 얻어 작업을 수행하게 되며 메서드 종료시 lock을 반환한다. 두번째로는 코드의 일부를 임계영역으로 설정하고 **객체의 참조변수**를 붙이는 방법인데 lock을 걸고자 하는 객체를 정의해주면 된다.

```java
// 메서드 전체를 임계 영역으로 지정
public synchronized void A() {

}

public void A() {
    // 특정한 영역을 임계 영역으로 지정
    synchronized(객체의 참조변수) {

    }
}
```

## wait()과 notify()

synchronized를 통해 동기화하여 공유 자원을 보호하는 것은 좋지만 lock을 잡고 오랫동안 반환하지 않게 되면 다른 쓰레드는 무한정 대기하게 되는 상황이 발생하게 된다. 이러한 상황을 개선하기위해 개발된 것이 ``wait()``과 ``notify()``이다. 임계 영역내 작업을 진행시 일부 지연이 걸리는 경우이거나 더이상 작업 진행이 어려울 경우 다른 쓰레드가 lock을 얻을 수 있게 wait()을 호출하여 lock을 반환하고 기다린다. wait()으로 lock을 반환한 쓰레드가 다시 작업을 진행할 수 있는 상황이 되면 notify()를 호출하여 lock을 획득하게 되며 작업을 재개할 수 있다. 하지만 notify()를 호출하게 되면 공유 자원(객체)를 사용하길 기다리돈 다른 쓰레드 들이 순서대로 lock을 획득하진 못한다. 동일한 ``waiting pool``에 대기하던 임의의 쓰레드에게 사용할 수 있는 상황이다 라는 통보를 한 후 lock을 획득하여 자원을 사용하게 된다. ``notifyAll()``은 waiting pool에 대기 중인 모든 쓰레드에게 통보할 수 있다. 하지만 뭐가됐든 임계 영역이 정의된 블럭엔 하나의 쓰레드만 올 수 있기에 임의의 하나의 쓰레드만 lock을 획득하고 나머지의 쓰레드는 다시 waiting pool에 대기하게 된다.

>**wait(), notify(), notifyAll()**  
>- Objecy에 정의되어 있다.  
>- 동기화 블록 내에서만 사용할 수 있다.  
>- 보다 효율적인 동기화를 가능하게 한다.  


## 기아 현상과 경쟁 상태 

![waitingPool](/assets/images/blog/waitingPool.png)
A, B의 쓰레드가 동기화 블럭으로 감싸져있는 공유 자원을 사용한다고 가정해보자. 
1. A쓰레드가 lock을 획득하여 사용, waiting pool에는 B쓰레드가 대기 (첫번째 그림)
2. wait()호출 하여 A쓰레드 대기 상태로 전환 -> waiting pool에 A,B 쓰레드 (가운대 그림)
3. notify() 호출
4. A쓰레드가 lock을 획득하여 사용, waiting pool에는 B쓰레드가 대기 (세번째 그림)


notify()를 통해 waiting pool에 대기 중인 쓰레드들에게 자원 사용할 기회를 주지만 그림 flow처럼 B쓰레드는 lock을 획득하지 못하는 경우가 발생한다. 이러한 현상을 ``기아 현상``이라고 한다. 이러할 경우 notifyAll()을 통해 waiting pool에 대기중인 모든 쓰레드에게 통보를 하여 쓰레드간 lock을 획득하기 위해 ``경쟁 상태``에 놓기에 된다. 이처럼 기아 현상, 경쟁 상태를 개선하기 위해 아래에 정리할 ``Lock``과 ``Confition``을 이용하여 쓰레드에 선별을 주어 lock획득을 컨트롤 할 수 있다.

## Lock과 Condition을 이용한 동기화

```java
ReentrantLock           // 재진입이 가능한 lock, 가장 일반적으로 사용되는 lock
ReentrantReadWriteLock  // 읽기에는 공유적이고, 쓰기에는 배타적인 lock
StampedLock             // ReentrantReadWriteLock에 낙관적인 lock의 기능을 추가
```

**ReentrantLock**은 위에 설명한 synchronized와 거의 유사하다 단지 선언하는 부분이 다를뿐이다. **ReentrantReadWriteLock**은 읽기를 위한 lock과 쓰기를 위한 lock을 제공한다. 임계 영역에 읽기 lock이 걸려 있으면 다른 쓰레드에서 중복으로 읽을 수 있지만 쓰기lock이 걸려 있으면 허용되지 않는다. **StampedLock**은 보통 동기화가 걸린 lock은 읽기 lock이 걸려 있으면, 쓰기 lock을 얻기 위해 읽기 lock이 풀릴 떄까지 기다려야하는데 반해 쓰기 lock에 의해 읽기 lock이 바로 풀려버린다. ``무조건 읽기 lock을 걸지 않고, 쓰기와 읽기가 충돌할 때만 쓰기가 끝난 후에 읽기 lock을 거는 것이다.``

일반적으로 사용하는 **ReentrantLock**에 대해서만 정리해보자.

```java
// synchronized
synchronized(lock) {
    // 임계영역
}

// ReentrantLock
lock.lock();
try {
    // 임계영역
} finally {
    lock.unlock();
}
```
일반 적으로 ``.unlock();``의 경우에는 혹시 예외가 발생하여 lock을 반환하지 못할 경우가 있기에 임계영역을 try로 감싸고 finally에 unlock()을 선언해 주어야 한다.

```java
private ReentrantLock lock = new ReentrantLock();   // lock 생성

private Condition aThread = lock.newCondition();    // a 쓰레드용 Condition 생성
private Condition bThread = lock.newCondition();    // b 쓰레드용 Condition 생성

// 사용시
// synchronized
wait();     // lock 반환 -> 쓰레드 대기로 전환
notify();   // 쓰레드가 lock 획득 가능

// ReentrantLock
aThread.await();    // a 쓰레드 대기로 전환
aThread.signal();   // a 쓰레드 lock 획득 시키기
```

## volatile

volatile


#### 위의 모든 정리내용은 자바의 정석을 공부하며 복습차 정리한 내용입니다. 
