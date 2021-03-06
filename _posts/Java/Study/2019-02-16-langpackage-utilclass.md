---
layout: customize-posts
title: "자바의정석 - 자바(lang Package, Uitl Class)"
date: 2019-02-16
last_modified_at: 2019-02-17
description: "남궁성님의 자바의정석을 읽고 중요하다고 생각하는 내용 정리 및 리마인드, 객체지향 프로그래밍에 대한 내용 chapter7입니다. jvm 메모리 구조에 대해서도 정리 함. 자바의정석, 남궁성, 자바, java, 객체지향, 프로그래밍, JVM, 메모리구조, memory, 클래스, 인스턴스, 객체화, 클래스 변수, 인스턴스 변수, 초기화, 초기화 블럭, 명시적 초기화, 명시적, 생성자, 매개변수, 추상클래스, abstract, 이너클래스, innerclass, 익명클래스, anonymous, 예외처리, 예외, try, catch, exception, throw, finaly java.lang package, util class, object, String, literal, 리터럴, Objects, wrapper, StringBuffer, String"
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
category:
    - Java
    - Study
tags:
    - java
published: true
sitemap:
    changefreq: daily
    priority: 1.0
---

## lang Package, Uitl Class

### Object 클래스

|Object클래스의 메서드|설       명|
|-----------------|----------|
|protected Object clone()|객체 자신의 복사본을 반환한다.|
|public boolean equals(Object obj)|객체 자신과 객체 obj가 같은 객체인지 알려준다 (같으면 true)|
|protected void finalize()|객체가 소멸될 떄 가비지 컬렉터에 의해 자동적으로 호출된다., 이때 수행되어야하는 코드가 있을때 오버라이딩한다. (거의 사용안함)|
|public Class getClass()|객체 자신의 클래스 정보를 담고 있는 Class 인스턴스를 반환한다.|
|public int hashCode()|객체 자신의 해시코드를 반환한다.|
|public String toString()|객체 자신의 정보를 문자열로 반환한다.|
|public void notify()|객체 자신을 사용하려고 기다리는 쓰레드를 하나만 깨운다.|
|public void notifyAll()|객체 자신을 사용하려고 기다리는 모든 쓰레드를 깨운다.|
|public void wait()|다른 쓰레드가 notify(), notifyAll()을 호출할 때까지 현재 쓰레드를 무한히 기다리게 한다.|
|public void wait(long timeout)|다른 쓰레드가 notify(), notifyAll()을 호출할 때까지 현재 쓰레드를 지정된 시간 동안 기다리게 한다.|
|public void wait(long timeout, int nanos)|다른 쓰레드가 notify(), notifyAll()을 호출할 때까지 현재 쓰레드를 지정된 시간 동안(timeout, nanos) 기다리게 한다.|


Object 클래스는 모든 클래스의 최고 조상이기 떄문에 모든 클래스에서 바로 사용가능하다. Object 클래스는 멤버변수가 없으며 아래 11개의 메서드만 가지고 있다. 위의 11개의 메서드 중 자주 사용하는 것들에 대해서만 기록하려 한다.  

**equals(Object obj)**  
매개변수로 객체의 참조변수를 받는다. 그 결과를 boolean값으로 반환하는 역할을 한다. 번외로 기록하자면 ``String.equals()``의 경우 Object.equals를 **오버라이딩**하여 값을 비교할 수 있게 구현되어있다.
```java
IntObject i1 = new IntObject(10);
IntObject i2 = new IntObject(10);

boolean first = i1.equals(i2); // false 값 '10'을 비교한것이 아닌 i1, i2의 참조변수를 비교

i2 = i1;
boolean second = i1.equals(i2); // true 위의 'i2 = i1'을 넣어 줌으로써 서로가 같은 참조변수를 바라보고 있음
```

**hashCode()**  
해싱기법에 사용되는 해시함수를 구현한 것이다. 데이터관리기법 중의 하나인데 다량의 데이터를 저장하고 검색하는데 유용하다. 객체의 주소값을 이용해서 해시코드를 만들어 반환하기 때문에 서로 다른 두 객체는 결코 같은 해시코드를 가질 수 없다.

아래 예제는 ``equals(Object obj), hashCode()``를 간단하게 String 클래스와 비교한 내용이다.
```java
Object obj1 = new Object();
Object obj2 = new Object();

String str1 = new String("abc");
String str2 = new String("abc");

System.out.println(obj1.equals(obj2));
System.out.println(obj1.hashCode());
System.out.println(obj2.hashCode());
System.out.println(System.identityHashCode(obj1));
System.out.println(System.identityHashCode(obj2));

System.out.println();

System.out.println(str1.equals(str2));
System.out.println(str1.hashCode());
System.out.println(str2.hashCode());
System.out.println(System.identityHashCode(str1));
System.out.println(System.identityHashCode(str2));

/**
출력결과

false <- 참조변수(주소값) 끼리 비교
1829164700 <- 객체의 주소값을 이요한 해시코드 생성
2018699554 <- 객체의 주소값을 이요한 해시코드 생성
1829164700 <- Ojbect.hashCode()
2018699554 <- Ojbect.hashCode()

true <- 위에 설명한 String 클래스는 equals를 오버라이딩하여 재구현된 상태이기에 '주소값' 비교가 아닌 '값' 비교이다
96354 <- 위에 설명한 String 클래스는 hashCode()를 오버라이딩하여 재구현된 상태이기에 '주소값' 비교가 아닌 '값' 비교이다
96354 <- 위에 설명한 String 클래스는 hashCode()를 오버라이딩하여 재구현된 상태이기에 '주소값' 비교가 아닌 '값' 비교이다
1311053135 <- identityHashCode는 고유의 hashCode를 전달함 Object.hashCode()한 값이다.
118352462 <- identityHashCode는 고유의 hashCode를 전달함 Object.hashCode()한 값이다.
*/
```

### String 클래스

String 클래스는 변경 불가능한 클래스이다. 이게 무슨말이냐면 ``String a = "a";``로 선언된 변수 a 가 있다고 가정을 하자. 그 후 ``a = a + "b";``를 하면 a에는 "ab"라는 값이 들어갈 것이다. 내부적으로는 변수 a 에 ``new String("ab")``가 수행이되어 새로은 문자열 리터럴이 메모리상에 생기게된다. (기존 문자열 "a" 리터럴도 메모리에 상주) 이렇게 String 클래스로 선언된 변수에 '연산자 +' 를 중첩사용할 경우 메모리 낭비가 생기게 된다. 이럴떄는 **StringBuffer or StringBuilder** 클래스를 사용하는게 성능적으로 좋다.

String의 문자열 비교시 두가지 생성 관점에서 다른 값이 도출된다. 첫 번째는 문자열 리터럴을 지정하는 방법과 두 번째는 String클래스의 생성자를 사용해서 만드는 방법이다. String클래스의 생성자를 이용한 경우에는 new연산자에 의해서 메모리할당이 이루어지기 때문에 항상 새로운 String인스턴스가 생성된다. 그렇지만 문자열 리터럴은 이미 존재하는 것을 **재사용**하는 것이다. 아래 예제를 통해 차이점을 확인해 보자.
```java
String a = "abc";
String b = "abc";
String c = new String("abc");
String d = new String("abc");

System.out.println("a: "+ a + " | b: " + b + " | c: " + c + " | d: " + d);
System.out.println("a: "+ System.identityHashCode(a) 
                    + " | b: " + System.identityHashCode(b) 
                    + " | c: " + System.identityHashCode(c) 
                    + " | d: " + System.identityHashCode(d));

/**
출력결과

a: abc | b: abc | c: abc | d: abc 
-> 각 String의 값

a: 1829164700 | b: 1829164700 | c: 2018699554 | d: 1311053135 
-> 문자열 리터럴인 a, b는 동일한 메모리주소값을 갖고 있으며, c,d는 new 생성자를 통해 인스턴스화 되었기에 새로운 메모리주소에 "abc"값이 저장된 상태이다.
*/
```

**문자열 리터럴**
모든 문자열 리터럴은 컴파일 시에 클래스 파일에 저장이 된다. 이떄 같은 문자열 리터럴은 한번만 저장되며 다른 곳에서 동일 리터럴을 사용하게되면 메모리를 공유하게 된다. 또한 리터럴들은 JVM내에 있는 ``'상수 저장소(Constant pool)``에 저장된다.

**String 클래스의 메서드 정리**

|String 클래스의 메서드|설      명|
|------------------|---------|
|charAt(int index)|"sksggg123".charAt(2) -> 's'|
|compareTo(String str)|"ggg".compareTo("ggg") -> 0 (사전순서로 비교하며 같으면 0, 이전이면 -1, 이후면 1|
|concat(String str)|"sks".concat("ggg123") -> "sksggg123"|
|endWith(String str)|"sksggg123".endWith("123") -> true|
|intern()|문자열을 상수풀에 등록하며 이미 상수풀에 같은 내용의 문자열이 있을 경우 그 문자열의 주소값을 반환한다.|

**join()과 StringJoiner**
join()은 여러 문자열 사이에 구분자를 넣어서 결합한다. split()과 반대라고 생각하면 된다. 예제를 보면 바로 이해가 될 것이다.
```java
String a = "a,b,c";
String[] arr = a.split(",");
String b = String.join("|", arr);
System.out.println(b);

StringJoiner c = new StringJoiner("|", "[", "]");
for(String d : arr) {
    c.add(d);
}
System.out.println(c);

/**
출력결과

a|b|c
[a|b|c]
*/
```

## StringBuffer 클래스

String 클래스의 경우 변경 불가능한 클래스라고 하였다. 하지만 StringBuffer 클래스의 경우는 그렇지 않다 내부적으로 문자열 편집을 위한 버퍼를 가지고 있으며, StringBuffer인스턴스를 생성할 때 그 크기를 지정할 수 있다. 크기를 별도로 선언하지 않을경우 기본적으로 16자로 생성을 한다. 내부적으로 StringBuffer 클래스는 아래와 같이 구현되어있다.
```java
public final class StringBuffer extends AbstractStringBuilder implements java.io.Serializable, CharSequence
{
    private char[] value;

    public StringBuffer() {
        super(16);
    }

    .......
}
```

참고로 StringBuffer 클래스는 equals 메서드를 오버라이딩하지 않아서 StringBuffer 클래스의 equals메서드를 사용해도 ``등가비교연산자(==)``로 비교한 것 과 같은 결과를 얻는다. 만일 문자열 비교하기 위해서는 StringBuffer인스턴스에 ``toString()``을 호출해서 String인스턴스를 얻은 다음 equals메서드를 사용해서 비교해야 한다.
```java
StringBuffer sb1 = new StringBuffer("abc");
StringBuffer sb2 = new StringBuffer("abc");

System.out.println(sb1==sb2); // false
System.out.println(sb1.equals(sb2)); // false

System.out.println(sb1.toString().equals(sb2.toString())); // true
```
## 래퍼(wrapper) 클래스 

자바에서는 8개의 기본형(primitive type)이 있다. 그 외에는 모두 객체이다. 이렇게 기본형 type을 매개변수로 사용시 객체로 요구할떄, 기본형 값이 아닌 객체로 저장해야할따, 객체간의 비교가 필요할ㄷ 때 등등의 경우에는 기본형 값들을 객체로 변환하여 작업을 수행해야한다. 이때 사용하는것이 ``래퍼(wrapper)`` 클래스 이다. 

|기본형|래퍼클래스|생성자|활용|
|-|-|-|-|
|boolean|Booleand|Boolean(boolean value)|Boolean b = new Boolean(true);|
|char|Character|Character(char value)|Character c = new Character('a');|
|byte|Byte|Byte(byte value)|Byte b = new Byte(10);|
|short|Short|Short(short value)|Short s = new Short(10);|
|int|Integer|Integer(int value)|Integer i = new Integer(10);|
|long|Long|Long(long value)|Long l = new Long(10);|
|float|Float|Float(float value)|Float f = new Float(10.0);|
|double|Double|Double(double value)|Double d = new Double(10.0);|

래퍼 클래스의 경우 모두 ``equals()`` 메서드가 오버라이딩되어 있어서 주소값이 아닌 실제 객체가 가지고있는 value값을 비교할 수 있다. 참고로 Integer객체에 비교연산자를 사용할 수 없다 비교를 하려면 compareTo() 메서드를 사용해야 한다.
```java
Integer i1 = new Integer(10);
Integer i2 = new Integer(20);

System.out.println(i1.equals(i2)); // false
i2 = 10;

System.out.println(i1.equals(i2)); // true
System.out.println(i1.compareTo(i2)); // 0
```

래퍼 클래스의 ``'타입.parse타입(String s)'``형식의 메서드와 ``'타입.valueOf(String s)'`` 메서드는 차이가 있다. 전자의 parseInt와 같이 사용하면 기본형을 반환하여 Integer.valueOf와 같이 사용하면 래퍼 클래스를 반환한다.

## Objects 클래스
Object클래스의 보조 클래스로 모든 메서드가 ``static``으로 되어있다. 객체의 비교나 Null 체크에 유용하다. 예를 들면 ``Object.isNull(object obj)`` 으로 사용하면 된다. ``requireNonNull()``메서드는 해당 객체가 널이 아니어야 하는 경우에 사용한다. 만일 객체가 널이면, NullPointerException()을 발생시킨다. 아래는 ``Integer i1 = new Integer(10)``으로 인스턴스화 한 Integer 객체로 확인한 사항이다.
```java
System.out.println(Objects.isNull(i1));
System.out.println(Objects.nonNull(i1));

System.out.println(Objects.requireNonNull(i1));
i1 = null;
System.out.println(Objects.requireNonNull(i1));

/**
출력 결과

false
true
10
Exception in thread "main" java.lang.NullPointerException
	at java.util.Objects.requireNonNull(Objects.java:203)
	at Solution.main(main.java:40)
*/
```

참고로 Object클래스의 equals와 Objects클래스의 equals 두 클래스에 메서드가 있는데 차이점이 있다. 전자인 Object클래스의 equals의 경우 Null 체크를 해주어야 하지만 Objects클래스의 equals는 Null 체크를 안해도 된다.
```java
if(a != null && a.equals(b)) {
    ...
}

if(Objects.equals(a, b)) {
    ...
}
```ss

###### 위의 모든 정리내용은 자바의 정석을 공부하며 복습차 정리한 내용입니다. 