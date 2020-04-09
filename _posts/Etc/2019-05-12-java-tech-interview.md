---
layout: customize-posts
title: "Java 웹개발 기술면접 정리해보기"
date: 2019-05-12
description: "자바 웹개발자 기술면접을 위해 개념정리 해보기"
header:
    teaser: /assets/images/K.png
    og_image: /assets/images/K.png
keywords:
    - java
    - web
    - developer
    - interview
    - 인터뷰
    - 기술면접
    - 자바
    - 웹개발자
category:
    - Etc
tags:
    - interview
published: true
sitemap: 
    changefreq: daily
    priority: 1.0
---

>기술면접 정리차원에서 간단한 용어 및 개념 정리를 위한 목적입니다.

# 기본단답
### java 언어의 장단점
**장점** :  
운영체제에 독립적이다(JVM) : 자바로 만든 애플리케이션은 JVM하고 통신을 하기에 운영체제에 종속되지 않는다.  
객체지향언어 : 상속, 캡슐화, 다형성, 추상화  
자동 메모리 관리 : Garbage Collector에 의해 자동적으로 메모리를 관리해준다.  
멀티쓰레드 구현의 용이성 : 운영체제마다 구현하는 방식과 처리되는 방식이 상이하지만 java는 시스템에 관계없이 구현이 가능  
동적로딩 지원 : 여러 클래스로 구성되어있으며, 실행 시에 모든 클래스가 로딩되지 않고 필요시점에 클래스를 로딩하여 사용할 수 있다.  
**단점** : 속도가 느리다 JVM을 통해 운영체제에 종속적이지 않지만 하드웨어에 맞게 완전히 컴파일된 상태가 아니며, 실행 시에 interpret 되기 때문에 속도가 느리다.

### Java8 특징
**람다 표현식** : 람다 표현식(lambda expression)이란 간단히 말해 메소드를 하나의 식으로 표현한 것입니다. 즉, 식별자 없이 실행할 수 있는 함수 표현식을 의미하며, 따라서 익명 함수(anonymous function)라고도 부릅니다.  
**스트림** : 간결하게 컬렉션의 데이터를 처리하며 한번 선언 후 사용을 하면 사라진다.  

### JVM
java와 os 사이에서 중개자 역할을 수행하며 바이트코드(.class)로 컴파일 된 상태를 class loader를 통해 .class 파일들을 JVM으로 interpret한다. 해석된 바이트 코드는 Runtime Data Area에 올라 실질적인 수행을 한다.  
**Method (Static) Area** : JVM이 읽어들인 클래스와 인터페이스 대한 런타임 상수 풀, 멤버 변수(필드), 클래스 변수(Static 변수), 생성자와 메소드를 저장하는 공간이다.  
**Heap Area** : JVM이 관리하는 프로그램 상에서 데이터를 저장하기 위해 런타임 시 동적으로 할당하여 사용하는 영역이다.  
**Stack Area** : 각 쓰레드마다 고유한 영역, 기본(원시)타입 변수는 스택 영역에 직접 값을 가진다. 참조타임 변수는 힙 영역이나 메소드 영역의 객체 주소를 가진다.  

### HotSpot JVM
Sun Microsystem사의 Java 엔진 이름이다. Java VM의 엔진은 다양하지만 크게 HotSpot(Sun/Oracle), J9(IBM), JRocket(Oracle) 정도가 기업용자바 환경에서 주로 사용되는 것들이다. JRocket은 서버쪽 성능개선에 집중된 것으로 HostSpot에 그 핵심기능이 옮겨져있기에 현재 대새는 Oracle Hotspot이다. HotSpot은 오픈소스 자바 프로젝트인 OpenJDK의 JVM엔진이기도 하다.

### Interpreter
javac로 컴파일한 바이트코드를 JVM을 통해 해석할때 필요하며 한줄단위로 읽는다. 이로인해 속도가 느리다는 단점이 있다.

### JIT
interperter의 속도를 보안하기 위해 컴파일러이며, 인터프리터 방식으로 실행되나 적절한 시점에 바이트코드 전체를 컴파일한다. JIT는 한번에 모두 컴파일하는 방식이기에 시간이 오래걸린다. JVM은 내부적으로 어떠한 메서드가 얼마나 빈번하게 사용되는지를 체크하고 설정된 수치이상으로 실행이 될 경우 JIT로 컴파일을 한다.

### 데이터 타입
**기본(원시)타입** : 자료형이라고도 불리며 대상은 byte, short, int, char, float, double, boolean이 있다. 기본타입은 Stack영역에 저장된다.  
**참조타입** : 기본타입을 제외한 모든 타입은 참조형이다. new로 인해 인스턴스화 시키는 객체데이터가 생기는 주소를 참조하는 타입이다. 참조타입은 데이터 크기가 가변적이기에 동적으로 관리되는 Heap 영역에 저장된다. GC처리로 인해 처리되는 영역  

### 상수와 리터럴
**상수** : 변수 선언과 동일하며, final을 붙인다는 차이가 있다. 한번 정의되면 변경하지 못한다.  
**리터럴** : 상수의 값들을 리터럴이라고 표현한다.  

### 클래스 메서드(static 메서드)와 인스턴스 메서드
**클래스 메서드** : static을 붙여 정의하며 애플리케이션 실행시 메모리에 올라간다. new를 통해 객체화 시키지 않고 바로 클래스명.메서드명 을 통해 사용이 가능하다.  
**인스턴스 메서드** : 클래스 메서드와 달리 실행시 메모리에 올라가지 않으며, 사용 시 new를 통한 객체화를 시켜 메모리에 올리고 사용을 해야한다.  

### 절차지향과 객체지향의 차이
보통 절챠지향의 경우 순서라고들 표현한다. 순차적으로 로직흐름이 진행이되며 중간에 하나가 동작을 안하게되거나 순서가 틀리게 되면 해당 로직은 수행을 하지 못한다는 특징이 있다. 반면 객체지향실 세계를 모델링하여 개발하는 방법이라고 표현을 한다. 특정 기능 하나하나를 분리하여 필요 시 호출하여 사용하는 재사용성이 높은 개발방법이라고 표현을 한다.  
위의 설명으로 보면 뭔가 추상적인 감이 있다. C언어도 그럼 객체지향적이지 않을까 라는 생각이 들 수 있다고 본다. 그래서 다른분이 정리한 내용을 인용하자면 **절차지향은 데이터 중심으로 구현이 이루어지며, 객체지향은 기능 중심으로 구현이 된다.** 라는 말이 와 닿았다. 어떠한 기능이 데이터를 공유하며 그를 기준으로 구현하는 방법을 절차지향적인 방법, 하지만 데이터를 은닉화 하여 기느응로 구현하여 외부에서 그 기능을 사용하는 방법을 객체지향적 방법이라고 한다.  

### OOP 4가지 특징
**추상화** : 공통적인 특징을 하나의 집합으로 나누는 것  
**캡슐화** : 낮은 응집도와 낮은 결합도가 가능하게 설계, 외부에서 데이터의 접근을 막기위해서 ```private```를 사용하여 은닉시키는 개념  
**상속화** : 기존의 클래스를 재정의하여 사용하는 것이며 키워드로 ```extends```를 사용한다.  
**다형성** : 서로다른 클래스의 객체가 같은 메시지를 받았을 때 각자의 방식으로 동작하는 것.  

### 오버딩과 오버라이딩
**오버로딩** : 오버로딩은 동일한 메서드명을 사용하며 인자(매개변수)의 개수 또는 타입을 달리하여 정의를 하는 것이다. 오버로딩의 대표적인 메서드는 printf()이다. 타입을 어떤것을 넣어도 출력이 되는것에 알 수 있듯이 오버로딩된 메서드이며 매개변수는 args로 정의되어 개수는 상관이 없고 타입별로 정의가 되어있어 동일한 메서드이름으로 여러타입을 사용할 수 있는 것이다.  
**오버라이딩** : 상위 클래스의 상속화를 통해 메서드 이름과 매개변수가 동일한 메서드를 하위 클래스에 재정의 하는 것이다.

### Call By Value와 Call By Reference
**Call By Value** : 인자로 전달되는 변수의 ```값을 복사```하여 전달하고 전달된 변수의 값은 지역적으로 사용된다. 그래서 함수의 인자값이 변경되어도 외부의 변수의 값은 변경되지 않는 특징이 있다.  
**Call By Reference** : 인자로 전달되는 변수의 ```주소값```을 전달하며, 인자값이 변경되면 전달된 변수도 함께 변깅이 된다.

### GC 영역별 동작
**Young GC** : 새롭게 생성된 객체는 대부분 Young 영역에 위치한다. 해당 영역에서 객체가 사라질때는 Minor GC가 발생한다.  
**Old GC** : Young 영역에서 살아남은 객체가 복사되며 해당 영역에서 객체가 사라질때 Major GC, Full GC가 발생한다.

### final 
**기본타입** : 기본타입에 final을 붙이게 되면 ```상수```로 데이터의 변경이 불가능하다.  
**참조변수** : 참조변수에 final을 붙이게 되면 참조변수가 바라보는 Heap 영역의 주소를 변경할 수 없다.  
**메서드** : 메서드에 final을 붙이게 되면 오버라이드를 할 수 없다.  
**클래스** : 하위 클래스를 정의 할 수 없다.  

### String, StringBuilder, StringBuffer
**String** : 주소값은 Stack에 쌓이며 주소값이 바라보는 데이터는 Heap에 저장된다. 참고로 String 변수에 글자를 append 하는 형식인 ```String += "a"```와 같이 사용하게 될 경우 기존의 String으로 선언한 변수는 Heap에 그대로 유지되며 새로운 String 변수가 생성되기에 메모리 관리에 비효율적이다.  
**StringBuilder** : StringBuilder의 경우 String과는 달리 .append()를 사용하여 메모리상의 데이터에 직접 append하기에 증식되지 않는다.  
**StringBuffer** : StringBuilder와 마찬가지로 메모리에 증식되지 않으며, Thread Safe한 특징을 갖고 있다. 동기처리에 사용한다.  

### Collection 종류 및 특징
**ArrayList** : 크기가 동적으로 조절되는 배열이다, 새 원소를 삽입하면 크기가 늘어난다. 중복과 null을 허용한다.
**Vector** : ArrayList와 비슷하지만 동기화가 되어있다는 차이가 있다.
**Hashtable** : key, value 형태 이며, 각각에 null 을 허용하지 않습니다. 중요한 포인트는 ```synchronized```가 선언되어 있어 동기화를 보장한다.  
**HashMap** : key, value 형태이며, 각각에 null을 허용한다. key는 정렬되지않은 임의의 순서로 되어있고 중요한 포인트는 ```synchronized```가 선언되어 있지 않아 동기화를 보장하지 않는다.  
**ConcurrentHashMap** : key, value 형태이며, 각각에 null을 허용하지 않는다. HashMap의 동기화 부분을 보완한 컬렉션으로 동기화를 보장한다. 별도로 .putIfAbsent() 메서드가 있는데 저장하려는 key값이 있으면 기존 key에 매핑된 value를 반환한 뒤 저장하며, key에 매핑된 value가 없을 경우 값을 저장한뒤 저장한 값을 반환한다.  
**TreeMap** : key, value 형태이며, 정렬된 key로 되어있으므로, 정렬된 순서로 key를 순회할 수 있다.  
**LinkedHashMap** : key, value 형태이며, key는 삽입된 순서로 정렬이 되어있다.

동기화 이슈가 있다면 동기화를 보장하는 컬렉션을 사용하거나, HashMap에 synchronized 키워드를 통해 동기화 처리를 해주면 된다.  

### Process와 Thread
**process** : 운영체제로 부터 CPU시간이나 메모리 등의 독립적인 공간(자원-code, data, stack, heap)을 할당받아 작업하는 단위이며 최소 메인쓰레드 하나를 갖고 있다. 또한 다른 프로세스의 공간(자원)을 기본적으로는 참조할 수 없으며, 참조가 필요할 경우 소켓통신을 이용해야 한다.  
멀티프로세스 환경에서는 하나의 작업을 OS 스케줄링에 의해 수행을 하게된다. 단점으로는 프로세스는 각각의 공간을 할당 받아 작업을 하기에 문맥전환 비용이 크다는 점이다.  
**Thread** : 쓰레드는 프로세스안에서 stack영역을 할당받아 작업을 진행하며 나머지 영역은 다른 쓰레드와 공유한다. stack을 쓰레드마다 독립적으로 할당하는 이유는 함수호출시 전달되는 인자, return될 주소값 등 함수 내에 선언된 변수들을 저장하기 위해 사용되는 메모리 공간이므로 스택 메모리 공간이 독립적인 것이다. stack을 제외한 다른 자원을 공유할 수 있기에 동기화 문제에 신경을 써야하며, 프로세스와 달리 멀티쓰레드 환경에서의 문맥전환은 stack영역만을 하면되기에 비용이 작다.  

### 스케줄러
**Job Queue** : 현재 시스템 내에 있는 모든 프로세스의 집합  
**Ready Queue** : 현재 메모리 내에 있으면서 CPU를 잡아서 실행되기를 기다리는 프로세스의 집합  
**Device Queue** : Device I/O 작업을 대기하고 있는 프로세스의 집합  
**장기 스케줄러** : 메모리 Pool에 저장되어있는 프로세스 중 어떤 프로세스에 메모리를 할당하여 Ready Queue로 보낼지 결정하는 역할  
**단기 스케줄러** : Ready Queue에 있는 프로세스 중 어떤걸 Running 시킬지 결정하는 역할  
**중기 스케줄러** : 메모리에 너무 많은 프로그램이 동시에 올라가는 것을 조절하는 역할  

### CPU 스케줄러
**FCFS** : First Come First Served Scheduling 먼저온 것을 먼저 순서대로 처리, 비선점형, 오래걸리는 프로세스가 먼저 올 경우 효율이 떨어진다.  
**SJF** : Shortest Job First Scheduling CPU사용률이 낮은 프로세스 먼저 처리, 제일 긴 프로세스는 순서가 계속적으로 밀리는 경우가 발생할 수 있다.  
**HRRN** : Highest response ratio next 스케줄링은 프로세스 처리의 우선 순위를 CPU 처리 기간과 해당 프로세스의 대기 시간을 동시에 고려해 선정하는 스케줄링 알고리즘이다. SJF 스케줄링의 문제점을 보완해 개발된 스케줄링이다. (우선순위 = (대기시간 + 처리시간) / 처리시간)  
**SRT** : 최소 잔류 시간 우선 스케줄링 (shortest remaining time) 은 SJF 스케줄링을 비선점에서 선점 형태로 수정한 스케줄링 알고리즘으로 현재 작업 중인 프로세스를 중단시키고 새로 들어온 프로세스의 처리를 시작하는 방식이다. SRT 스케줄링 ,SRTF 스케줄링이라고도 한다.  
**Priority Scheduling** : 우선순위가 가장 높은 프로세스에게 CPU 할당, 선점형  
**Round Robin** : 시분할 시스템을 위해 설계된 선점형 스케줄링의 하나로서, 프로세스들 사이에 우선순위를 두지 않고, 순서대로 시간단위(Time Quantum)로 CPU를 할당하는 방식의 CPU 스케줄링 알고리즘이다.  

### ThreadLocal
일반적인 변수의 수명은 블록 ```{}```이다. 선언된 블록이 완료된 시점에 해당 변수는 사용을 할 수 없게되는데 ThreadLocal을 사용하게 되면 동일 쓰레드 영역에서는 파라미터로 변수를 전달하지 않아도 다른 블록영역 (같은 쓰레드 일경우 만)에서 사용이 가능하다.  
사용법은 간단하다 선언, set(), get(), remove()를 활용하여 사용한다. 단, 사용이 완료되었을 경우 ThreadLocal을 통해 선언한 변수는 remove()를 시켜주어야 한다. 그렇지 않으면 재사용되는 쓰레드에 의해 정확하지 않은 데이터가 사용될 수 있다.  
또한, ThreadLocal은 사용자 인증정보 전파나 트랜잭션 컨텍스트 전파에 주로 사용이 된다.  

### Java transient
transient는 Serialize하는 과정에서 제외하려는 필드에 정의하면 데이터 전송할때 null로 전송이 된다.  
개인정보와 같은 데이터를 제외할때 사용할 수 있다.

### HTTP
**HTTP** : 비연결 구조로 사용자의 연결을 유지하지 않는 방식이다. 사용자 요청 -> 응답 -> 연결해제 되는 흐름이다. 특징은 주로 HTML문서를 주고 받는데 사용되며 80포트를 사용한다.  
**HTTP 메서드** :  GET, PUT, POST, DELETE, PUSH, OPTIONS 등.. 이 있으며, GET은 Read, PUT은 Update, POST는 Insert, DELETE는 Delete

### HTTP2
HTTP1은 Request를 날릴때마다 Connection을 새로 맺어 Response를 전달하고 있다. 매번 요청이 있을때마다 Connection을 맺는 비효율적인 방법이여서 HTTP1.1에서는 지속 컨넥션, 파이프라이닝 이라는 개념이 들어가게되고 이로인해 컨넥션을 재사용 할 수 있고 Request를 미리 여러개 보낼 수 있게되었다. 하지만 Request를 여러개 보내도 보낸 순서에 따라 Response를 받기 때문에  하나의 먼저 보낸 Request에 팬딩이라던지 지연이 발생하게 되면 후속 Response에 지연이 발생한다. 이러한 문제점을 개선하기 위해 HTTP2가 나오게되었으며 Multiplexing 개념이 도입되어 동시에 여러 response를 받을 수 있게 된다.

### HTTPS
**HTTPS** : 웹 통신 프로토콜인 HTTP의 보안강화된 버전의 프로토콜이다. 특징은 443포트를 사용하며, 소켓 통신에서 일반 텍스트를 이용하는 대신에 웹 상에서 정보를 암호화하는 SSL, TLS 프로토콜을 통해 세션 데이터를 암호화한다.

### TCP, UDP
**TCP** : 연결형 서비스로 가상 회선 방식을 제공한다. 3-way handshaking과정을 통해 연결을 설정하고, 4-way handshaking을 통해 연결을 해제한다.  
**UDP** : 정보를 주고 받을 때 정보를 보내거나 받는다는 신호절차를 거치지 않는다.  
**연결 handshake** : 3 way -> 연결 해달라고 요청, 연결요청 승인, 연결
**종료 handshake** : 4 way -> 해제 해달라고 요청, 해제요청 승인, 해제, 해제완료 되었다고 알림
**응용 계층** : HTTP, SMTP, FTP로 HTTP가 널리 사용된다.  
**표현 계층** : 소켓을 통해 전달받은 데이터(바이트)를 시스템에서 데이터를 인지할 수 있게 컨버터 해주는 역할이다.  
**세션 계층** : TCP/IP 세션을 만들고 없애는 책임을 수행하는 계층이며, 소켓을 통해 통신을 한다.  
**전송 계층** : TCP, UDP 프로토콜를 이용한 세그먼트를 목적지까지 전달을 한다. TCP프로토콜은 연결지향성, 신뢰성 있는 전송으로 연결된 컨넥션을 통해 여러 소켓 데이터를 전달한다. 이때 전달하는 세그먼트의 헤더에 출발지의 포트와 목적지의 포트를 기재하여 전달한다. 여기서 연결된 통로를 통해 여러개의 세그먼트를 전달하는 것을 Multiplexiong이라고 한다. 신뢰성있는 통신인 TCP의 경우 전달한 순서또한 유지가 되야한다. 이때 Sequence Number를 부여하여 전달을 하게된다. 이러한 순서번호를 통해 중복수신을 방지할 수 있게된다. UDP의 경우에는 수신지가 정상적으로 메시지를 받았는지 확인 절차가 없으며 순서또한 없다. 단지 송신자의 던지기를 받을 수 있으면 받는 것이다.  
**네트워크 계층** : 전송 계층에서 보내려는 패킷을 목적지 까지 도착시키는 역할을 하며, 그 과정에 라우팅과 포워딩이 필요하다. 라우팅은 라우팅 알고리즘을 통해 연결된 라우터들의 최적의 경로를 결정하며 그 결과를 포워딩 테이블로 만들어 진다. 포워딩 테이블을 기반으로 다른 라우터로 전달을 하며 목적지인 서브넷까지 이동한다.  

### 쿠키와 세션
**쿠키** : 브라우저에 저장되는 객체이다.  
**세션** : 서버의 메모리에 존재하는 객체이다.  
사용자의 브라우저(컴퓨터)에서는 많은 정보를 가지고 있지 못하기에 서버의 메모리를 활용한 세션에 데이터를 저장해두고 사용자 브라우저에서는 세션을 요청할 수 있는 ID를 쿠키(브라우저)에 저장하여 필요시 요청을 한다. (브라우저의 *SEESIONID가 그에 해당한다.)  

### Spring MVC 패턴
Model, View, Controller를 분리한 디자인 패턴이다.  
**Model** : Application의 data를 나타낸다.  
**View** : Model data의 랜더링 담당 -> JSP  
**Controller** : View와 Model 사이의 인터페이스 역할을하며 Controller -> Service -> Dao -> DB를 통해 Model을 가공하여 View로 전달한다.  
**DispatcherServlet** : Spring Framework가 제공하는 Servlet 클래스이며 Dispatcher가 받은 요청은 HandlerMapping으로 전달된다.  
**HandlerMapping** : 요청 url에 해당하는 Controller 정보를 저장한 Table을 갖고 있으며, 사용자의 요청 url을 Controller에 매핑시킨다.  
**ViewResolver** : prefix, suffix로 Controller에서 view로 전달할때 View구현체 저장위치(Prefix)와 확장자(suffix)와 같이 설정하여 전달.

### Spring Bean
Beans는 애플리케이션의 핵심을 이루는 객체이며, Spring IoC(Inversion of Control) 컨테이너에 의해 인스턴스화, 관리, 생성된다.  
Bean Scope의 종류로는 **Singleton, prototype**이 있다. singleton은 Spring 컨테이너에서 한 번 생성된다. scope를 명시하지 않으면 default로 singleton으로 설정이 된다. prototype은 모든 요청에서 새로운 객체를 생성하는 것을 의미한다. bean에 주입 될 때 새로운 객체가 생성되어 주입되는 것이다. singleton을 사용할때는 장시간에 걸쳐 많은 객체가 생성될때 설정하는 것이 좋다. 보통 prototype으로 설정한 bean이 여러곳에서 주입되어 여러번 생성이 된 후 완료되면 GC에 의해 bean이 제거 된다.  

### 스프링 프레임워크의 특징
경량컨테이너로 라이프사이클을 관리하고 필요한 객체를 스프링으로부터 받아옵니다.  
DI지원하여 객체간의 의존관계 설정이 가능합니다.  
AOP지원합니다.  
POJO방식으로 자바객체는 특정한 인터페이스를 구현하고 클라스 상속이 필요치 않습니다.  
트랜젝션 처리를 위한 일관된 방법을 제공합니다.  
영속성 관련 다양한 API를 지원합니다.  
API연동을 지원합니다.  

### IoC, DI
**IoC** : application의 제어권을 framework가 갖는다. 개발자는 xml과 어노테이션을 설정해 주면 framework에서 알아서 설정대로 주입을하는 것이다.  
**DI** : framework에 의해 의존성이 주입되는 패턴. 의존성 주입에는 생성자를 통한 주입, 메서드(setter)를 통한 주입.  

### REST
**Uniform** : URI로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일  
**Stateless** : 무상태성 성격을 갖는다. 세션 정보나 쿠키 정보를 별도로 저장하고 관리하지 않기 때문에 API서버는 들어오는 요청만을 단순히 처리하면 된다.  
**Cacheable** : HTTP 프로토콜 기준으로 사용하며 기존 인프라를 그대로 활용이 가능하다.  
**Client - Server** : REST 서버는 API제공, 클라이언트는 사용자 인증이나 컨텍스트등을 직접 관리하는 구조로 역할 구분이 되기때문에 서버와 클라이언트 개발 영역이 명확해지고 서로간의 의존성이 줄어들게 된다.  

### HTTP Method
**GET** : (select) 리소스 조회한다.  
**POST** : (insert) 리소스를 생성시킨다.  
**PUT** : (update) 리소스를 수정한다.  
**DELETE** : (delete) 리소스를 삭제한다.  

### HTTP 응답코드
**200** : 클라이언트의 요청을 정상적으로 수행.  
**201** : 리소스 생성 요청이 성공정으로 됨 (POST)  
**301** : 요청한 리소스에 대한 URI가 변경 되었을때 (redirect)  
**400** : 요청이 부적절 할 경우  
**401** : 인증되지 않은 상태에서 보호된 리소스를 요청했을 때  
**403** : 인증상태와 관계 없이 응답하고 싶지 않은 리소스를 클라이언트가 요청했을 때  
**405** : 요청한 리소스에서 사용 불가능한 Method를 이용했을 경우  

### 디자인패턴
**싱글톤 패턴** : 어떤 클래스가 오직 하나의 객체만을 갖도록 하며, 프로그램 전반에 걸쳐 그 객체 하나만 사용되도록 보장해야 한다. 이렇듯 싱글톤은 전역객체를 구현해야하며 한번 생성 후에 공용으로 사용하기에 단위테스트에는 어려움이 있다.  
**팩토리 메서드** : 어떤 클래스의 객체를 생성하기 위한 인터페이스를 제공하되, 하위 클래스에서 어떤 클래스를 생성할지 결정할 수 있도록 도와준다.  
**파사드 패턴** : 어떤 서브시스템의 일련의 인터페이스에 대한 통합된 인터페이스를 제공한다. 퍼사드에서 고수준 인터페이스를 정의하기 때문에 서브시스템을 더 쉽게 사용할수 있다. 대표적으로 slf4j가 그에 해당한다. 
**어댑터 패턴** : 한 클래스의 인터페이스를 클라이언트에서 사용하고자 하는 다른 인터페이스로 변환. 자바에서는 다중 상속이되지 않기에 사용자는 인터페이스에 접근을 하고 인터페이스를 implements하여 구현한 adaptor에서는 상속한 adaptee를 호출한다. 아래와 같은 구조가 된다. 
```java
public class User {
    public void run() {
        AdaptorInterface interface = new Adaptor();
        interface.call();
    }
}
interface AdaptorInterface {
    public void call();
}

public class Adaptee {
    public void print() {
        System.out.println("User -> Call -> Print");
    }
}

public class Adaptor extends Adaptee implements AdaptorInterface {
    public void call() {
        super.print();
    }
}
```

### HA 구성
고가용성 솔루션을 이용하면, 각 시스템 간에 공유 디스크를 중심으로 집단화 하여 클러스터로 엮어지게 만들 수 있다. 동시에 다수의 시스템을 클러스터로 연결할 수 있지만 주로 2개의 서버를 연결하는 방식을 많이 사용한다. 만약 클러스터로 묶인 2개의 서버 중 1대의 서버에서 장애가 발생할 경우, 다른 서버가 즉시 그 업무를 대신 수행하므로, 시스템 장애를 불과 수 초에서 수 분 안에 복구할 수 있다.  
**데이터 복제 기능** : 서버 중 1번 서버가 장애가 발생시, 2번 서버가 대상 서비스를 바로 서비스를 하기 위해서는 양쪽의 데이터는 항상 100% 동일 해야 하는 무결성을 보장 해야 한다.  
**장애 감시 기능** : 1번 서버는 서비스 운영을 맞게 되며, 2번 서버는 1번 서버가 장애 발생시 서비스를 운영하기 위한 대기 생태로 구성이 된다. 이러한 구성은 Active – Stand By HA 구성이라고 한다.  

### SLB(Server Load Balancer)
서버부하분산 방법이며, 여러대의 서버를 한대의 서버처럼 사용할 수 있게해준다. 하나의 서버가 이슈로인해 중단이 생길경우 나머지 서버가 대응 할 수 있는 구조이다.  
**Round Robin** : Real Server로 session을 순차적으로 만들어 준다. 현재 각 서버의 연결된 세션수와 상관없이 순차적으로 각 서버에 전달해주기 때문에 5:5로 균등하게 분배할 수 있다. 하지만 경로보장이 되지 않는 문제가 있다.  
**Least Connection** : Real Server의 Open 세션 수를 고려한 다음, 가장 적은수의 open session을 가진 Real Server로 session을 맺어주는 방식. 거의 5:5로 분산이 가능하지면 경로보장이 되지않는다.  
**Response Time** : 각 Real Server들이 서로 상이한 resource와 connectino에 부수되는 시간과 데이터 양이 서로 다른 환경에서 사용할 수 있다. 알테온이 서버와 통신을 하면서 그 응답시간에 대한 학습을 통하여 응답시간이 빠른 쪽으로 많은 세션을 보내주고 응답이 느린쪽으로 세션을 적게 보내는 방식.  
**Hash** : hashing algorithm을 사용한 밸런싱방법이며, 동일한 사용자는 동일한 값을 받기떄문에 경로 보장이되어 서버에 밸런싱이 되는 기법이다.    

### InnoDB
MySQL을 위한 데이터베이스 엔진이며, MySQL AB가 배포하는 모든 바이너리에 내장되어 있다. MySQL과 사용할 수있는 다른 데이터베이스 엔진에 대한 개선 사항으로 PostgreSQL을 닮은 ACID 호환 트랜잭션에 대응하고 있는 것이 있다. 또한 외래 키(FK)도 지원하고 있다. (이것을 선언적 참조 무결성이라 한다.)

### Array
논리적 저장순서와 물리적 저장 순서가 일치 한다. index를 통해 접근이 가능하다는 뜻. 하지만 index로 데이터에 접근하는 자료구조 같은 경우 마지막 index를 삭제하는 게 아닌 시작~중간 지점의 index를 삭제 시 재배열하는 비용이 발생한다. (추가는 삭제와 반대로 보면 됨.)  

### LinkedList
index의 추가 삭제에 대한 재배열 비용을 보안한 자료구조이다. 다음 node의 index를 이전 node가 가지고 있는 방식이며 중간에 삭제 될 경우 이전 node에 다음 node값으로 대체해주면된다. 하지만 Array와 달리 논리적 저장 순서와 물리적 저장순서가 일치하지 않아 중간의 node를 확인하려면 처음부터 순차탐색을 해야 한다.  

### Stack
(선형) LIFO으로 마지막에 들어온 데이터가 먼저 나가는 구조이다.  

### Queue
(선형) FIFO으로 처음으로 들어온 데이터가 먼저 나가는 구조이다.  

### Tree
(비선형) 계층적 관계를 표현하는 자료구조이다.   
**node** : 트리를 구성하고 있는 각각의 요소.  
**edge** : 트리를 구성하기 위해 노드와 노드를 연결하는 선.  
**Root Node** : 트리 구조에서 최상위에 있는 노드를 의미.  
**Terminal Node** : 하위에 다른 노드가 연결되어 있지 않은 노드.  
**Internal Node** : 단말 노드를 제외한 모든 노드로 루트 노드를 포함.  

### Binary Heap
Tree 중에서 배열에 기반한 완전 이진 트리이다. 배열에 트리의 값을 넣어줄 때 0 번 index는 건너띄고 1번 index부터 루트노드가 시작 된다.  

### Database Index
데이터베이스에 저장된 데이터와 index를 key, value 형식으로 매핑하여 빠른 접근이 가능하게 하는 것. 빠른 접근을 위해 모든 속성에  index를 정의할 경우 데이터가 추가되거나 수정되거나 삭제될때 index로 같이 정의가 되기 때문에 속도 이슈가 있다.  
기본키(primary key)나 unique로 설정된 컬럼에 대해서는 index가 자동으로 생성이된다. index의 경우는 where절이나 join절에 자주사용되는 컬럼에 정의를 하면 효율이 좋다, 하지만 index된 필드에서 데이터를 업데이트하거나, 레코드를 추가 또는 삭제할 때 성능이 떨어집니다.

### DML, DDL, DCL
**DML** : 데이터 조작어로 SELECT, INSERT, UPDATE, DELETE가 있다.  
**DDL** : 데이터 정의어로 CREATE, DROP, ALTER, TRUNCATE가 있다.  
**DCL** : 데이터 제어어로 GRANT, REVOKE가 있다.

### Database Key의 종류
**슈퍼 키(Super Key)** : 유일성을 만족하는 키. 예를 들면, {학번 + 이름}, {주민등록번호 + 학번}  
**복합 키(Composite Key)** : 2개 이상의 속성(attribute)를 사용한 키.  
**후보 키(Candidate key)** : 유일성과 최소성을 만족하는 키. 기본키가 될 수 있는 후보이기 때문에 후보키라고 불린다. 예를 들면, 주민등록번호, 학번 등  
**기본 키(Primary key)** : 후보 키에서 선택된 키. NULL값이 들어갈 수 없으며, 기본키로 선택된 속성(Attribute)은 동일한 값이 들어갈 수가 없다.  
**대체 키(Surrogate key)** : 후보 키 중에 기본 키로 선택되지 않은 키.  
**외래 키(Foreign Key)** : 어떤 테이블(Relation) 간의 기본 키(Primary key)를 참조하는 속성이다. 테이블(Relation)들 간의 관계를 나타내기 위해서 사용된다.

### Database의 정규화
데이터베이스 정규화란 데이터의 중복을 줄이고 무결성을 향상 시키기 위해 관계형 데이터베이스를 정규화된 형태로 재구성하는 것을 말한다.

|이름|나이|과목|띠|
|-|-|-|-|
|권|30|알고리즘,데이터베이스|말띠|
|병|29|자료구조|양띠|
|윤|28|데이터베이스|원숭이띠|

**1차정규화** : 각 row마다 컬럼의 데이터가 1개만 존재해야 한다. 이를 원자값을 갖는다고 표현함. 한개만 갖을 수 있을때 불가피하게 중복된 데이터를 허용해야 할 때가 있다.

|이름|나이|과목|띠|
|-|-|-|-|
|권|30|알고리즘|말띠|
|병|29|자료구조|양띠|
|윤|28|데이터베이스|원숭이띠|
|권|30|데이터베이스|말띠|

**2차정규화** : 테이블의 모든 컬럼이 완전 함수적 종속을 만족한다.(부분 함수적 종속을 모두 제거되었다.) 함수적 종속이란 x와 y의 값이 있을때 x가 y의 값을 결정할때 y는 함수적 종속이라고 한다. 위의 테이블표에서는 나이는 이름에 완전 함수적 종속을 만족하지만 나이는 과목에 함수적 종속을 갖지 못한다. 고로 나이는 부분 함수적 종속이다. 2차 정규화를 하기위해서는 이름과 과목을 분리해야 한다는 의미이다.

|이름|나이|띠|
|-|-|-|
|권|30|말띠|
|병|29|양띠|
|윤|28|원숭이띠|

|이름|과목|
|-|-|
|권|알고리즘|
|권|데이터베이스|
|병|자료구조|
|윤|데이터베이스|

**제3정규화** : 제 2 정규형에 속하면서, 기본키가 아닌 모든 속성이 기본키에 이행적 함수 종속이 되지 않으면 제 3 정규형이다. 이행적 함수 종속이란 x -> y 이고 y -> z 이면 x -> z이다.

|이름|나이|
|-|-|
|권|30|
|병|29|
|윤|28|

|나이|띠|
|-|-|
|30|말띠|
|29|양띠|
|28|원숭이띠|

**BCNF** : 3NF 를 만족하는 릴레이션 R의 후보키가 1개 밖에 없고, R의 후보키가 기본키가 되고, 3NF를 만족하면 항상 BCNF 를 만족한다. 

# 자바관련 응용한 서술
### 상속 관점에서 생성자를 private으로 선언하면 어떤 효과가 있나
private은 선언된 클래스 내부에서만 접근이 가능하다. 그로인해 외부 클래스에서 접근이 불가능하여 생성할 수 없게된다. 하지만 다음과 같은 상황에선 접근할 수 있다.  
<script src="https://gist.github.com/sksggg123/a6db8f0c9dc29f88f4022f4715a69ef1.js"></script>
PrivateInner의 내부로 TestInner가 있다면 TestInner의 private생성자에 접근하여 사용할 수 있다. 이렇게 할 경우 은닉화를 하여 TestInner를 사용할 수 있다.

### try-catch-finally 의 구조에서 try or catch에 return을 하게 되면 finally가 수행 되는가
결론은 된다. try, catch 블록을 벗어나려 할때 finally블록은 실행되고 끝이난다.
<script src="https://gist.github.com/sksggg123/4181ac18dba5ea7b8896e4804905f33c.js"></script>

### final, finally, finalize의 차이
final의 경우 기본타입, 참조변수, 메소드, 클래스에 사용할 경우 각각의 제한이 다르다. 기본타입에 선언할 경우 값 변경이 불가능항 상수로 된다. 참조변수에 선언할 경우 메모리에 올라간 주소값을 변경하지 못한다. 메소드에 선언할 경우 오버라이딩 할 수 없다. 클래스에 선언할 경우 상속할 수 없다.  
finally의 경우 try-catch 구문에서 실행 후 필수적으로 수행되는 블록 영역이다.  
finalize 메서드의 경우 GC가 객체를 해제하기전에 호출하는 메서드다. Object클래스의 finalize() 메서드를 오버라이딩해서 GC를 정의할 수 있다.

### HashMap, TreeMap, LinkedHashMap의 차이를 설명하고 언제사용하면 좋을까
HashMap의 경우 정렬되지 않은 key값, TreeMap의 경우 정렬된 key값, LinkedHashMap의 경우 삽입된 순서의 key값으로 되어있다.  
TreeMap의 경우 날짜를 key로 객체를 가지고 올때나, 이름 또는 나이순서로 객체를 가지고 올때 사용하면 좋다.  
LinkedHashMap의 경우 삽입된 순서(Queue 개념으로) 그대로 이기에 캐시를 구현할때 사용하기에 적합하다.  
HashMap의 경우는 그 외에 보편적으로 사용된다.
아래의 소스 출력 결과는 다음과 같다.
```java
/**
hashMap (수행마다 다름!)
key : A valuePerson{name='A', age=10}
key : B valuePerson{name='B', age=12}
key : C valuePerson{name='C', age=11}
treeMap
key : A valuePerson{name='A', age=10}
key : B valuePerson{name='B', age=12}
key : C valuePerson{name='C', age=11}
linkedHashMap
key : A valuePerson{name='A', age=10}
key : C valuePerson{name='C', age=11}
key : B valuePerson{name='B', age=12}
*/
```
<script src="https://gist.github.com/sksggg123/9b7540c372719e4e3c3424cbf3cb5e83.js"></script>

### 자바의 객체 리플렉션을 설명하고 유용한 이유를 나열하시오
1. 프로그램 실행(Runtime)에 클래스 내부의 메서드와 필드에 대한 정보를 얻을 수 있다.
2. 클래스의 객체를 생성할 수 있다.
3. 객체 필드의 접근 제어자에 관계없이, 그 필드에 대한 참조를 얻어내어 값을 가져오가나 설정할 수 있다.
<script src="https://gist.github.com/sksggg123/71ef536f507dba5ff20fbbecb911327a.js"></script>

# 객체지향설계 관련 서술


# 데이터베이스 관련 서술
### 묵시적 JOIN, 명시적 JOIN
```sql
-- 묵시적 JOIN
SELECT  *
FROM    USER U,
        STORE S
WHERE   1 = 1
AND     U.ID = S.USER

-- 명시적 JOIN
SELECT  *
FROM    USERS U 
            INNER JOIN STORE S ON U.ID = S.USER
```

### 비정규화, 정규화 데이터베이스
**비정규화 데이터베이스**는 읽는 시간을 최적화되도록 설계된 데이터베이스.  
**정규화 데이터베이스**는 중복을  최소화하도록 설계된 데이터베이스.
정규화 데이터베이스는 **USER(사람정보)** 테이블과 **STORE(점포정보)** 테이블이 있다고 가정을 할 경우 STORE에 USERID를 갖는 외래키를 갖는 컬럼이 있다. 사람정보는 **한번의 저장**으로 사용가능하다는 장점이 있지만 일반적으로 점포정보에 **운영하는 사람정보를 갖는 쿼리를 만들때 JOIN**을 해야하는 단점이 있다.  
대신에 비정규화 데이터베이스에서는 데이터를 중복해서 저장할 수 있다. 반복적인 쿼리를 만들때는 USER를 STORE에 중복해 저장하는 방식을 비정규화 데이터베이스 라고 한다.  
비정규화의 경우 join하는 연산비용을 줄이는 효과는 있지만 데이터의 갱신이 있을 경우 정규화 상태보다 비용소모가 심하다. 또한 중복된 데이터를 허용하기에 데이터의 일관성이 깨질 위험이 있고, 그에 따라 저장공간이 많이 필요하다.

### 모든학생의 목록을 뽑고 수강한 강의의 수를 확인하는 쿼리를 작성하시오
Table : STUDENT(학생), STUDENTCOURSES(수강신청한 학생의 수)
```sql
-- 초기 쿼리작성
SELECT  COUNT(ST.STUDENTID),
        ST.STUDENTID
FROM    STUDENTCOURSE STC 
            LEFT JOIN STUDENT ST ON ST.STUDENTID = STC.STUDENTID
WHERE   1 = 1
GROUP BY ST.STUDENTID
```
left join을 통해 학생ID가 수강목록에 없더라도 출력이 되게 쿼리를 만들었지만 위의 쿼리에는 문제가 있다. 첫 번째로 GROUP BY에 ST.STUDENTID로 그룹을 정할 경우 카운팅 되는 값은 최소 1이상이 된다. 그렇기에 STUDENTCOURSES의 STUDENTID를 그룹으로 지정해야 한다. 또한 ST.STUDENTNAME을 바로 사용하지 못하며, SELECT절에 MAX() 집계함수를 붙여서 MAX(STUDENTNAME)으로 명시하면 된다. 아래는 수정된 결과조회 쿼리문이다.
```sql
-- 수정쿼리
SELECT  ST.STUDENTNAME,
        ST.STUDENTID,
        TMP.CNT
FROM    STUDENT ST
            JOIN {
                SELECT  COUNT(ST.STUDENTID) AS CNT,
                        ST.STUDENTID AS STID
                FROM    STUDENTCOURSE STC 
                            LEFT JOIN STUDENT ST ON ST.STUDENTID = STC.STUDENTID
                WHERE   1 = 1
                GROUP BY ST.STUDENTID
            } TMP ON ST.STUDENTID ON TMP.STID
```

### 서로 다른 종류의 JOIN은 어떤 것들이 있는가? 각각 어떻게 다르고, 어떤 상황에서 어떤 JOIN과 어울리는지 설명하라
내부조인(INNER JOIN)과 외부조인(OUTER JOIN)이 있다. 내부조인은 테이블 2개의 교집합으로 두 테이블에 모두 존재해야 출력이 되며 외부조인에는 LEFT JOIN, RIGHT JOIN, FULL OUTER JOIN으로 3가지의 경우가 있다. LEFT JOIN의 경우 좌측 테이블을 기준으로 조건에 부합한 좌측의 데이터를 출력하고 출력된 데이터와 우측의 테이블의 존재하면 출력, 존재하지 않으면 NULL로 출력이 된다. RIGHT JOIN은 LEFT JOIN의 반대입니다. FULL OUTER JOIN의 경우 2개의 테이블에 존재하는 모든 데이터를 출력하며 각 테이블에 없을 시 NULL을 출력 합니다.
```sql
--   TABLE A        TABLE B
-- NAME |  NUM  NAME    |  NUM
-- ONE  |   1   ONE     |   1
-- TWO  |   2   THREE   |   3

SELECT  *
FROM    A a
            JOIN B b on a.NAME = b.NAME
-- a.NAME   |   a.NUM   |   b.NAME  |   b.NUM
--  ONE     |   1       |   ONE     |   1

SELECT  *
from    A a
            LEFT JOIN B b on a.NAME = b.NAME
-- a.NAME   |   a.NUM   |   b.NAME  |   b.NUM
--  ONE     |   1       |   ONE     |   1
--  ONE     |   1       |   NULL    |   NULL

SELECT  *
from    A a
            RIGHT JOIN B b on a.NAME = b.NAME
-- a.NAME   |   a.NUM   |   b.NAME  |   b.NUM
--  ONE     |   1       |   ONE     |   1
--  NULL    |   NULL    |   THREE   |   3

SELECT  *
from    A a
            FULL OUTER JOIN B b on a.NAME = b.NAME
-- a.NAME   |   a.NUM   |   b.NAME  |   b.NUM
--  ONE     |   1       |   ONE     |   1
--  TWO     |   2       |   NULL    |   NULL
--  NULL    |   NULL    |   THREE   |   3
```

```A a LEFT JOIN B b on a.NAME = b.NAME``` 과 ```B b RIGHT JOIN A a on a.NAME = b.NAME```의 데이터가 출력되는 것은 같다.

# 알고리즘 
### 버블정렬
인접한 두 개의 데이터를 비교해가면서 정렬을 진행하는 방식이다. 가장 큰 값을 배열의 맨 끝에다 이동시키면서 정렬하고자 하는 원소의 개수 만큼을 두 번 반복하게 된다.  
**시간복잡도** : O(N^2)  
**공간복잡도** : O(1)  
<script src="https://gist.github.com/sksggg123/cfe7ebe57f4b0f5c69248267e0bf45e0.js"></script>  

### 선택정렬
n 개의 원소를 가진 배열을 정렬할 때, 계속해서 바꾸는 것이 아니라 비교하고 있는 값의 index 를 저장해둔다. 그리고 최종적으로 한 번만 바꿔준다.  
**시간복잡도** : O(N^2)  
**공간복잡도** : O(1)  
<script src="https://gist.github.com/sksggg123/74f61c14b7689524e4378055e4ab9866.js"></script>

### 삽입정렬
삽입 정렬은 두 번째 자료부터 시작하여 그 앞(왼쪽)의 자료들과 비교하여 삽입할 위치를 지정한 후 자료를 뒤로 옮기고 지정한 자리에 자료를 삽입하여 정렬하는 알고리즘이다.  
**시간복잡도** : O(N^2)  
**공간복잡도** : O(1)  
<script src="https://gist.github.com/sksggg123/3dcadff72a662dad3082adf557d509c2.js"></script>  

### 합병정렬
일반적인 방법으로 구현했을 때 이 정렬은 안정 정렬 에 속하며, 분할 정복 알고리즘의 하나 이다. 문제를 작은 2개의 문제로 분리하고 각각을 해결한 다음, 결과를 모아서 원래의 문제를 해결.  
**시간복잡도** : O(N^2)  
**공간복잡도** : O(NlogN)  
<script src="https://gist.github.com/sksggg123/a22555a8726860234c28ae5a7dc981e2.js"></script>  

### 힙정렬
완전 이진 트리의 일종으로 우선순위 큐를 위하여 만들어진 자료구조  
**시간복잡도** : O(NlogN)  
**공간복잡도** : O(NlogN) 
<script src="https://gist.github.com/sksggg123/8e778b856822de048f93487571a9c0b0.js"></script>  

### 퀵정렬
하나의 리스트를 피벗(pivot)을 기준으로 두 개의 비균등한 크기로 분할하고 분할된 부분 리스트를 정렬한 다음, 두 개의 정렬된 부분 리스트를 합하여 전체가 정렬된 리스트가 되게 하는 방법이다.  
<script src="https://gist.github.com/sksggg123/d8e870507ead8094a20522829ba502a6.js"></script>  




### 참고
[https://meetup.toast.com/posts/92](https://meetup.toast.com/posts/92)  
[https://gmlwjd9405.github.io/2018/11/10/spring-beans.html](https://gmlwjd9405.github.io/2018/11/10/spring-beans.html)  
[https://github.com/JaeYeopHan/Interview_Question_for_Beginner](https://github.com/JaeYeopHan/Interview_Question_for_Beginner)  
[https://github.com/WeareSoft/tech-interview/blob/master/contents/network.md#osi-7%EA%B3%84%EC%B8%B5](https://github.com/WeareSoft/tech-interview/blob/master/contents/network.md#osi-7%EA%B3%84%EC%B8%B5)  
[http://tcpschool.com/java/java_intro_java8](http://tcpschool.com/java/java_intro_java8)  
[https://palpit.tistory.com/130](https://palpit.tistory.com/130)  
[https://www.youtube.com/watch?v=aOP81IhPOmw](https://www.youtube.com/watch?v=aOP81IhPOmw)  
[https://hoonmaro.tistory.com/19](https://hoonmaro.tistory.com/19)
[https://www.sharedit.co.kr/posts/53](https://www.sharedit.co.kr/posts/53)  
[https://mani4u.tistory.com/203](https://mani4u.tistory.com/203)  
[https://www.kyobobook.co.kr/](https://www.kyobobook.co.kr/product/detailViewKor.laf?mallGb=KOR&ejkGb=KOR&barcode=9788966263080)
[https://lalwr.blogspot.com/2016/02/db-index.html#comment-form](https://lalwr.blogspot.com/2016/02/db-index.html#comment-form)
[https://brunch.co.kr/@toughrogrammer/16#comment](https://brunch.co.kr/@toughrogrammer/16#comment)