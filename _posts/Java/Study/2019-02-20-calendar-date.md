---
layout: customize-posts
title: "자바의정석 - 자바(날짜와 시간 & 형식화)"
date: 2019-02-20
last_modified_at: 2019-02-25
description: "남궁성님의 자바의정석을 읽고 중요하다고 생각하는 내용 정리 및 리마인드, 객체지향 프로그래밍에 대한 내용 chapter7입니다. jvm 메모리 구조에 대해서도 정리 함. 자바의정석, 남궁성, 자바, java, 객체지향, 프로그래밍, JVM, 메모리구조, memory, 클래스, 인스턴스, 객체화, 클래스 변수, 인스턴스 변수, 초기화,
초기화 블럭, 명시적 초기화, 명시적, 생성자, 매개변수, 추상클래스, abstract, 이너클래스, innerclass, 익명클래스, anonymous, 예외처리, 예외, try, catch, exception, throw, finaly java.lang package, util class, object, String, literal, 리터럴, Objects, wrapper, StringBuffer, String, date, calendar, simpledateformat, format"
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

## Calendar와 Date

Date는 날짜와 시간을 다룰 목적으로 JDK1.0 부터 제공되어온 클래스이다. 앞으로 정리할 날짜 관련된 클래스는 java.util패키지에 속한 것이다. java.sql패키지의 Date클래스와는 다른 내용이다.

### Calendar와 GregorianCalendar
Calendar는 추상클래스이기때문에 직접 객체를 생성할 수 없고 메서드를 통해서 완전히 구현된 클래스의 인스턴스를 얻어야 한다.

Calendar를 상속받아 완전히 구현한 클래스로는 GregorianCalendar, BuddhistCalendar가 있는데 getInstance()는 시스템의 국가와 지역설정을 확인해서 태국인 경우에는 BuddistCalendar의 인스턴스를 반환, 그 외에는 GregorianCalendar를 반환한다.

```java
// 인스턴스를 생성하려고 하면 IDE에서 알아서 메서드를 구현하라고 오버라이딩 해준다.
Calendar cal = new Calendar() {
    @Override
    protected void computeTime() {
        
    }

    @Override
    protected void computeFields() {

    }

    @Override
    public void add(int field, int amount) {

    }

    @Override
    public void roll(int field, boolean up) {

    }

    @Override
    public int getMinimum(int field) {
        return 0;
    }

    @Override
    public int getMaximum(int field) {
        return 0;
    }

    @Override
    public int getGreatestMinimum(int field) {
        return 0;
    }

    @Override
    public int getLeastMaximum(int field) {
        return 0;
    }
};

// getinstance()메서드는 Calendar클래스를 구현한 클래스의 인스턴스를 반환한다.
// 앞으로 Calendar클래스를 사용하려면 아래와 같이 사용하자.
Calendar cal2 = Calendar.getInstance();
```

### Date와 Calendar간의 변환

```java
public static void main(String[] args) {

    // 1. Calendar를 Date로 변환
    Calendar cal1 = Calendar.getInstance();
    Date date1 = new Date(cal1.getTimeInMillis());

    p(cal1.getTime());
    p(date1);

    // 2. Date를 Calendar로 변환
    Date date2 = new Date();
    Calendar cal2 = Calendar.getInstance();
    cal2.setTime(date2);

    p(cal2.getTime());
    p(date2);
}

public static void p(Object obj) {
    System.out.println(obj);
}

/**
출력 결과
Mon Feb 25 19:10:22 KST 2019
Mon Feb 25 19:10:22 KST 2019

Mon Feb 25 19:10:22 KST 2019
Mon Feb 25 19:10:22 KST 2019
*/
```

Calendar의 메서드를 현재시간이 아닌 지정된 시간으로 변경을 하려면 ``cal.set()``을 사용하면 된다. 위를 활용하면 오늘부터 지정된 날짜까지의 차이를 구할 수 있다.

```java
public static void main(String[] args) {

    Calendar cal1 = Calendar.getInstance();
    Date date1 = new Date(cal1.getTimeInMillis());

    p(cal1.getTime());
    p(date1);

    Date date2 = new Date();
    Calendar cal2 = Calendar.getInstance();
    cal2.setTime(date2);

    p(cal2.getTime());
    p(date2);

    cal1.set(2019, Calendar.AUGUST, date1.getDate());
    long diff = Math.abs(cal1.getTimeInMillis() - cal2.getTimeInMillis());
    p(diff);
    p(diff/(24*60*60*1000));
}

public static void p(Object obj) {
    System.out.println(obj);
}

/**
출력 결과
Mon Feb 25 19:18:48 KST 2019
Mon Feb 25 19:18:48 KST 2019

Mon Feb 25 19:18:48 KST 2019
Mon Feb 25 19:18:48 KST 2019

15638399968
180
*/
```

그 밖의 메서드는 참고사항으로 알아두면 좋다. ``add(int field, int amount)`` 지정한 필드의 값을 원하는 만큼 증가 또는 감소 시킬 수 있으며, ``roll(int field, amount)``  지정한 필드의 값을 증가 또는 감소를 시킬 수 있지만 ``add``와의 차이점은 다른 필드에 영향을 미치지 않는다.  

예를 들면 ``add(Calendar.Date, 31)``으로 설정을 하면 월이 변경이되며 Month의 값도 1증가가 되지만 ``roll(Calendar.Date, 31)``으로 설정을 하면 월 변경이 없다.


## 형식화 클래스

### DecimalFormat

형식화 클래스 중에서 숫자를 형식화하는데 사용되는 것이다. DecimalFormat을 이요하면 숫자 데이터를 정수, 부동소수점, 금액 등의 다양한 형식으로 표현할 수 있으며, 반대로 일정한 형식의 텍스트 데이터를 숫자로 쉽게 변환하는 것도 가능하다.

```java
public static void main(String[] args) {

    DecimalFormat df = new DecimalFormat("#.#E0");
    double number = 1234567.89;
    String result = df.format(number);
    p(result);

    DecimalFormat df2 = new DecimalFormat("#,###.#");
    double number2 = 1234567.89;
    String result2 = df2.format(number2);
    p(result2);
}

public static void p(Object obj) {
    System.out.println(obj);
}

/**
 출력결과 
 1.2E6
 1,234,567.9
*/
```

### SimpleDateFormat

Date와 Calendar만으로는 날짜 데이터를 원하는 형태로 다양하게 출력하는 것은 불편하고 복잡하다. 위의 SimpleDateFormat을 사용하면 이러한 문제들이 해결된다. 형식변화에 사용되는 메서드는 ``.format(pattern)``이다. ``.parse(String)``도 추가로 알아두면 좋다. parse의 경우 문자열을 날짜 Date인스턴스로 변환해 준다.

```java
public static void main(String[] args) {

    SimpleDateFormat sf = new SimpleDateFormat("yyyy-MM-dd");
    String dFormat = sf.format(date);

    Calendar cal = Calendar.getInstance();
    cal.setTime(date);
    String cFormat = sf.format(cal.getTime());

    p(dFormat);
    p(cFormat);
}

public static void p(Object obj) {
    System.out.println(obj);
}

/**
 출력결과
 2019-02-25
 2019-02-25
*/

public static void main(String[] args) {

    DateFormat df = new SimpleDateFormat("yyyy년 MM월 dd일");
    DateFormat df2 = new SimpleDateFormat("yyyy/MM/dd");
    Date date1 = new Date();
    p("before: " + date1);
    try{

        Date date2 = df.parse("2019년 02월 26일");
        p("after: " + df2.format(date2));
    }catch (Exception e) {
        e.getStackTrace();
    }
}

public static void p(Object obj) {
    System.out.println(obj);
}
/**
 출력결과
 before: Mon Feb 25 19:53:35 KST 2019
 after: 2019/02/26
*/
```

### ChoiceFormat

ChoiceFormat클래스는 특정 범위에 속하는 값을 문자열로 변환해준다. 연속적 또는 불연속적인 범위의 값들을 처리하는 데 있어서 if문이나 switch문은 적절하지 못한 경우가 많다. 이럴때 ChoiceFotmat을 사용하면 복잡하게 처리될 수 밖에 없었던 코드를 간단하게 처리할 수 있다.

여기서 주의할 점은 range값은 반드시 **double향 오름차순**으로 정렬이 되어있는 상태여야 하며, 치환될 문자열의 개수는 range와 동일해야 한다.

```java
public static void main(String[] args) {

    double[] range = {10,20,30,40,50,60,70,80,90,100};
    String[] grades = {"J","I", "H", "G", "F", "E", "D", "C" ,"B", "A"};
    int[] score = {40,50,70,30,90,100};

    ChoiceFormat cf = new ChoiceFormat(range, grades);

    for (int i = 0; i < score.length; i++) {
        p(score[i] + " : " + cf.format(score[i]));
    }
}

public static void p(Object obj) {
    System.out.println(obj);
}
/**
출력결과
40 : G
50 : F
70 : D
30 : H
90 : B
100 : A
*/
```

### MessageFormat

MessageFormat은 데이터를 정해진 양식에 맞게 출력할 수 있도록 도와준다. 다수의 데이터를 같은 양식으로 출력할때 주로 사용을 한다. 예를 들면 같은 안내문 양식에 받는 사람의 이름과 같은 데이터만 달리자도록 출력할 때 사용한다. 또한 SimpleDataFormat의 Parse처럼 MessageFormat의 Parse를 이용하면 지정된 양식에서 필요한 데이터만을 손쉽게 추출해 낼 수도 있다.

```java
public static void main(String[] args) {
    String msg = "Name: {0} \nTel: {1} \nAge: {2} \nBirthday: {3}";
    Object[] arguments = {"sksggg123", "010-9286-7958", "30", "02-02"};
    String result = MessageFormat.format(msg, arguments);
    p(result);
}

public static void p(Object obj) {
    System.out.println(obj);
}

/**
출력결과
Name: sksggg123 
Tel: 010-9286-7958 
Age: 30 
Birthday: 02-02
*/
```

## java.time패키지

Date와 Calendar가 가지고 있던 단점들을 해소하기 위해 ``java.time패키지``가 추가되었다. 핵심 클래스느는 날짜에 사용되는 **LocalDate**와 시간에 사용되는 **LocalTime**이다. 두개 모두 필요할때는 **LocalDateTime**클래스를 사용하면 된다.

```java
LocalDate + LocalTime -> LocalDateTime
   날짜         시간         날짜 & 시간
```

추가로 시간대(time-zone)까지 다뤄야 한다면, **ZonedDateTime**클래스를 사용하면된다.
```java
LocalDate + 시간대 -> ZonedDateTime
```

### Period와 Duration

날짜와 시간의 간격을 표현할때는 **Period** 두 날짜간의 차이를 표현할떄는 **Duration**을 사용
```java
날짜 - 날짜 = Period
시간 - 시간 = Duration
```
Period의 between() 메서드는 날짜와 날짜의 차이를 반환하며 Duration의 between() 메서드는 시간과 시간의 차이를 반환하다.
```java
LocalDate date1 = LocalDate.of(2019,2,27);
LocalDate date2 = LocalDate.of(2019,2,25);

Period pe = Period.between(date1, date2);

LocalTime time1 = LocalTime.of(00,00,00);
LocalTime time2 = LocalTime.of(12,34,56);

Duration du = Duration.between(time1, time2);
```



### 객체 생성하기 - now(), of()

java.time패키지에 속한 클래스의 객체를 생성하는 방법은 now()와 of()를 사용하는 것이다.
```java
public static void main(String[] args) {

    LocalDate date = LocalDate.now();
    LocalTime time = LocalTime.now();
    LocalDateTime dateTime = LocalDateTime.now();
    ZonedDateTime dateTimeInKr = ZonedDateTime.now();

    LocalDate date2 = LocalDate.of(2019, 02, 26);
    LocalTime time2 = LocalTime.of(22, 00, 00);
    LocalDateTime dateTime2 = LocalDateTime.of(date2, time2);
    ZonedDateTime dateTimeInKr2 = ZonedDateTime.of(dateTime2, ZoneId.of("Asia/Seoul"));

    p(date);
    p(time);
    p(dateTime);
    p(dateTimeInKr);

    p(date2);
    p(time2);
    p(dateTime2);
    p(dateTimeInKr2);
}

public static void p(Object obj) {
    System.out.println(obj);
}
/**
출력결과
2019-02-25
21:14:01.017
2019-02-25T21:14:01.017
2019-02-25T21:14:01.018+09:00[Asia/Seoul]

2019-02-26
22:00
2019-02-26T22:00
2019-02-26T22:00+09:00[Asia/Seoul]
*/
```

## 파싱과 포맷

날짜와 시간을 원하는 형식으로 출력하고 해석하는 방법에 대해 말하자면 형식화와 관련된 클래스들은 java.time.format패키지에 들어있는데 이 중에서 DateTimeFormatter가 핵심이다. 

```java
LocalDate date = LocalDate.of(2019, 02, 25);
String format = DateTimeFormat.ISO_LOCAL_DATE.format(date);
String format2 = date.format(DateTimeFormatter.ISO_LOCAL_DATE);
```

출력형식을 직정 정의하려면 ``ofPattern()``으로 원하는 출력형식을 직접 작성할 수 있다.
```java
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy/MM/dd");
```

###### 위의 모든 정리내용은 자바의 정석을 공부하며 복습차 정리한 내용입니다. 