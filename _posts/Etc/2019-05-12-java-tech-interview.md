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

### OOP 4가지 특징
**추상화** : 공통적인 특징을 하나의 집합으로 나누는 것  
**캡슐화** : 낮은 응집도와 낮은 결합도가 가능하게 설계, 외부에서 데이터의 접근을 막기위해서 ```private```를 사용하여 은닉시키는 개념  
**상속화** : 기존의 클래스를 재정의하여 사용하는 것이며 키워드로 ```extends```를 사용한다.  
**다형성** : 서로다른 클래스의 객체가 같은 메시지를 받았을 때 각자의 방식으로 동작하는 것.  

### 오버로딩과 오버라이딩
**오버로딩** : 오버로딩은 동일한 메서드명을 사용하며 매개변수의 개수 또는 타입을 달리하여 정의를 하는 것이다. 오버로딩의 대표적인 메서드는 printf()이다. 타입을 어떤것을 넣어도 출력이 되는것에 알 수 있듯이 오버로딩된 메서드이며 매개변수는 args로 정의되어 개수는 상관이 없고 타입별로 정의가 되어있어 동일한 메서드이름으로 여러타입을 사용할 수 있는 것이다.
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

### Hashtable, HashMap, ConcurrentHashMap
**Hashtable** : key, value 형태 이며, 각각에 null 을 허용하지 않습니다. 중요한 포인트는 ```synchronized```가 선언되어 있어 동기화를 보장한다.  
**HashMap** : key, value 형태이며, 각각에 null을 허용한다. 중요한 포인트는 ```synchronized```가 선언되어 있지 않아 동기화를 보장하지 않는다.  
**ConcurrentHashMap** : key, value 형태이며, 각각에 null을 허용하지 않는다. HashMap의 동기화 부분을 보완한 컬렉션으로 동기화를 보장한다. 별도로 .putIfAbsent() 메서드가 있는데 저장하려는 key값이 있으면 기존 key에 매핑된 value를 반환한 뒤 저장하며, key에 매핑된 value가 없을 경우 값을 저장한뒤 저장한 값을 반환한다.  

동기화 이슈가 있다면 동기화를 보장하는 컬렉션을 사용하거나, HashMap에 synchronized 키워드를 통해 동기화 처리를 해주면 된다.  

### Process와 Thread
**process** : 운영체제로 부터 독립적인 공간(자원-code, data, stack, heap)을 할당받아 작업하는 단위이며 최소 메인쓰레드 하나를 갖고 있다. 또한 다른 프로세스의 공간(자원)을 기본적으로는 참조할 수 없으며, 참조가 필요할 경우 소켓통신을 이용해야 한다.  
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
**FCFS** : 먼저온 것을 먼저 순서대로 처리, 비선점형, 오래걸리는 프로세스가 먼저 올 경우 효율이 떨어진다.  
**SJF** : CPU사용률이 낮은 프로세스 먼저 처리, 제일 긴 프로세스는 순서가 계속적으로 밀리는 경우가 발생할 수 있다.  
**SRT** : 새로운 프로세스가 올 때마다 CPU사용시간이 낮은 프로세스로 제어권을 뺏긴다.  
**Priority Scheduling** : 우선순위가 가장 높은 프로세스에게 CPU 할당, 선점형  
**Round Robin** : 각 프로세스마다 동일한 시간을 할당  

### ThreadLocal
일반적인 변수의 수명은 블록 ```{}```이다. 선언된 블록이 완료된 시점에 해당 변수는 사용을 할 수 없게되는데 ThreadLocal을 사용하게 되면 동일 쓰레드 영역에서는 파라미터로 변수를 전달하지 않아도 다른 블록영역 (같은 쓰레드 일경우 만)에서 사용이 가능하다.  
사용법은 간단하다 선언, set(), get(), remove()를 활용하여 사용한다. 단, 사용이 완료되었을 경우 ThreadLocal을 통해 선언한 변수는 remove()를 시켜주어야 한다. 그렇지 않으면 재사용되는 쓰레드에 의해 정확하지 않은 데이터가 사용될 수 있다.  
또한, ThreadLocal은 사용자 인증정보 전파나 트랜잭션 컨텍스트 전파에 주로 사용이 된다.  

### HTTP
**HTTP** : 비연결 구조로 사용자의 연결을 유지하지 않는 방식이다. 사용자 요청 -> 응답 -> 연결해제 되는 흐름이다. 특징은 주로 HTML문서를 주고 받는데 사용되며 80포트를 사용한다.  
**HTTP 메서드** :  GET, PUT, POST, DELETE, PUSH, OPTIONS 등.. 이 있으며, GET은 Read, PUT은 Update, POST는 Insert, DELETE는 Delete

### HTTP2
HTTP1은 Request를 날릴때마다 Connection을 새로 맺어 Response를 전달하고 있다. 매번 요청이 있을때마다 Connection을 맺는 비효율적인 방법이여서 HTTP1.1에서는 지속 컨넥션, 파이프라이닝 이라는 개념이 들어가게되고 이로인해 컨넥션을 재사용 할 수 있고 Request를 미리 여러개 보낼 수 있게되었다. 하지만 Request를 여러개 보내도 보낸 순서에 따라 Response를 받기 때문에  하나의 먼저 보낸 Request에 팬딩이라던지 지연이 발생하게 되면 후속 Response에 지연이 발생한다. 이러한 문제점을 개선하기 위해 HTTP2가 나오게되었으며 Multiplexing 개념이 도입되며 동시에  여러 response를 받을 수 있게 된다.

### HTTPS
**HTTPS** : 웹 통신 프로토콜인 HTTP의 보안강화된 버전의 프로토콜이다. 특징은 443포트를 사용하며, 소켓 통신에서 일반 텍스트를 이용하는 대신에 웹 상에서 정보를 암호화하는 SSL, TLS 프로토콜을 통해 세션 데이터를 암호화한다.

### TCP, UDP
**TCP** : 연결형 서비스로 가상 회선 방식을 제공한다. 3-way handshaking과정을 통해 연결을 설정하고, 4-way handshaking을 통해 연결을 해제한다.  
**UDP** : 정보를 주고 받을 때 정보를 보내거나 받는다는 신호절차를 거치지 않는다.  
**연결 handshake** : 3 way -> 연결 해달라고 요청, 연결요청 승인, 연결
**종료 handshake** : 4 way -> 해제 해달라고 요청, 해제요청 승인, 해제, 해제완료 되었다고 알림


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