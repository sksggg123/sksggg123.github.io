---
layout: customize-posts
title: "자바의정석 - 컬렉션 프레임워크"
date: 2019-03-02
last_modified_at: 2019-03-02
description: "남궁성님의 자바의정석을 읽고 중요하다고 생각하는 내용 정리 및 리마인드, 객체지향 프로그래밍에 대한 내용 chapter7입니다. jvm 메모리 구조에 대해서도 정리 함. 자바의정석, 남궁성, 자바, java, 객체지향, 프로그래밍, JVM, 메모리구조, memory, 클래스, 인스턴스, 객체화, 클래스 변수, 인스턴스 변수, 초기화,
초기화 블럭, 명시적 초기화, 명시적, 생성자, 매개변수, 추상클래스, abstract, 이너클래스, innerclass, 익명클래스, anonymous, 예외처리, 예외, try, catch, exception, throw, finaly java.lang package, util class, object, String, literal, 리터럴, Objects, wrapper, StringBuffer, String, date, calendar, simpledateformat, format, Collection, list, set, map, hash, hashMap, iterator, arraylist, linkedlist, stack, queue"
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

## 컬렉션 프레임워크

컬렉션 프레임워크 란 ``데이터 군을 저장하는 클래스들을 표준화한 설계``를 뜻한다. 컬렉션은 크게 3가지 타입이 존재한다고 보면 되며 다루는데 필요한 기능을 가진 3가지 인테퍼이스로 정의되어있다. [**List, Set, Map**]  

```java
Collection
    |_ List
    |_ Set

Map
```

List와 Set을 구현한 컬렉션 클래스들은 서로 공통부분이 있어서 공통부분을 뽑아 Collection인터페이스를 정의할 수 있었지만 Map인터페이스는 이들과는 다른 형태로 컬렉션을 다루기 때문에 같은 상속계층도에 포함되지 못한다.

|인터페이스|특   징|
|-------|------|
|List|순서가 있는 데이터 집합, 중복 허용O [ArrayList, LinkedList, Stack, Vector]|
|Set|순서를 유지하지 않는 데이터 집합, 중복 허용X [HashSet, TreeSet]|
|Map|Key, Value의 쌍으로 이루어진 데이터 집합, Key 중복 허용X / Value 중복 허용O [HashMap, TreeMap, HashTable, Properties]|

## List 인터페이스
List 인터페이스의 경우 중복을 허용하면서 저장된 순서가 유지되는 컬렉션이다. 계층구조도 및 구현된 메서드는 아래 참고  

```java
List
  |_ Vector
        |_ Stack
  |_ ArrayList
  |_ LinkedList
```

|메서드|설  명|
|----|-----|
|void add(Object o)|객체를 List에 저장 (Index로 순차저장)|
|object get(int index)|지정된 위치에 있는 객체 반환|
|int indexOf(Object o)|지정된 객체의 위치를 반환|
|int lastIndexOf(Object o)|지정된 객체의 위치를 반환한다 (역방향 검색)|
|ListIterator listIterator()|List의 객체에 접근할 수 있는 ListIterator를 반환한다.|
|Object remove(int index)|지정된 위치(Index)에 있는 객체를 삭제하고 삭제된 객체를 반환한다.|
|Object set(int index, Object element)|지정된 위치에 객체를 저장한다.|
|void sort(Comparator c)|지정된 비교자로 List를 정렬한다. Collections.sort(List)|
|List subList(int fromIndex, int toIndex)|지정된 범위에 있는 객체를 반환한다.|

## set 인터페이스
Set 인터페이스는 중복을 허용하지 않고 저장된 순서가 유지되지 않는 컬렉션이다. 계층구조도 아래 참고

```java
Set
  |_ HashSet
  |_ SortedSet
        |_ TreeSet
```

## Map 인터페이스

Map 인터페이스는 Key, Value의 쌍으로 이루어진 컬렉션이며, Key는 중복을 허용하지않으며 중복으로 입력시 기존 Key의 Value값이 오버라이딩 된다. Value의 경우는 중복허용이 가능하다. 계층구조도 및 구현된 메서드는 아래 참고

```java
Map
  |_ HashTable
  |_ HashMap
        |_ LinkedHashMap
  |_ SortedMap
        |_ TreeMap
```

|메서드|설  명|
|----|-----|
|void clear()|Map의 모든 객체를 삭제한다.|
|boolean containsKey(Object Key)|지정된 Key객체와 일치하는 Map의 key가 있는지 확인|
|boolean containsValue(Object Value)|지정된 Value객체와 일치하는 Map의 Value가 있는지 확인|
|Set entrySet()|Map에 저장되어 있는 Key-Value쌍을 Map.Entry타입의 객체로 저장한 Set으로 반환|
|boolean equals(Object o)|동일한 Map인지 비교|
|Object get(Object Key)|지정한 Key객체에 대응하는 Value객체를 찾아서 반환|
|int hashCode()|해시코드를 반환|
|boolean isEmpty()|Map이 비어있는지 확인한다.|
|Set keySet()|Map에 저장된 모든 Key객체를 반환|
|Object put(Object key, Object value)|Map에 Value객체를 Key객체에 연결하여 저장|
|void putAll(Map t)|지정된 Map의 모든 Key-Value쌍을 추가|
|Object remove(Object key)|지정된 Key객체와 일치하는 Key-Value객체를 삭제한|
|int size()|Map에 저장된 Key-Value쌍의 개수를 반환|
|Collection values()|Map에 저장된 모든 Value객체를 반환|

values()에서는 반환타입이 Collection이고 ketSet()에서는 반환타입이 Set인 것에 주목하자. 이유는 Map에서 Value는 중복이 허용되며, Key는 중복이 허용되지 않기에 Set 타입인 것이다.

## ArrayList

List 컬렉션 중 가장 많이 쓰이는 클래스 이다. Vector와 기본적으로 구현원리, 기능적인 측면에서 동일하다. 아래 소스로 기본적인 동작원리에 대해 알아보자.  

여기서 중요하게 볼것은 **반복문을 통한 삭제처리**이다. 시작을 Index 마지막``(int i=list2.size() -1)``을 시작으로 Counting값을 감소처리하여 반복이 되어야하는 부분을 기억해야 한다. 만일 변수 i를 증가시켜가면서 삭제를 한다면 빈 공간을 채우기 위해 나머지 요소들이 자리이동을 하기 때문에 올바른 결과를 얻을 수 없다.

```java
public String arrayInteger() {
    String rtnValue = "";

    // 임의의 정수 list에 셋팅 (불규칙적)
    List<Integer> list1 = new ArrayList<>();
    list1.add(5);
    list1.add(4);
    list1.add(2);
    list1.add(0);
    list1.add(1);
    list1.add(3);

    // list1 copy -> list2
    List<Integer> list2 = new ArrayList(list1.subList(1, 4));
    rtnValue = printService.print(rtnValue, list1); // -> print 1
    rtnValue = printService.print(rtnValue, list2); // -> print 2


    // Sort -> list1, list2
    Collections.sort(list1);
    rtnValue = printService.print(rtnValue, list1); // -> print 3

    Collections.sort(list2);
    rtnValue = printService.print(rtnValue, list2); // -> print 4


    // ContainsAll : boolean
    Boolean temp = list1.containsAll(list2);
    rtnValue = printService.print(rtnValue, temp); // -> print 5


    // row add, Index:0 modify element:9
    list2.add(7);
    list2.add(8);
    list2.add(0, 9);
    rtnValue = printService.print(rtnValue, list2); // -> print 6


    // retainAll : list 1개를 비교하여 겹치는 부분을 삭제
    list1.retainAll(list2);
    rtnValue = printService.print(rtnValue, list1); // -> print 7
    rtnValue = printService.print(rtnValue, list2);

    // 반복문을 통한 동일 value 삭제 처리
    for (int i = list2.size()-1; i >= 0 ; i--) {
        if(list1.contains(list2.get(i))) {
            list2.remove(i);
        }
    }
    rtnValue = printService.print(rtnValue, list1); // -> print 8
    rtnValue = printService.print(rtnValue, list2); // -> print 9

    return rtnValue;
}

public class PrintService {

    public String print(Object obj1, Object obj2) {

        obj1 += obj2.toString() + "\n\n";
        return obj1.toString();
    }
}

/**
출력결과
[5, 4, 2, 0, 1, 3]

[4, 2, 0]

[0, 1, 2, 3, 4, 5]

[0, 2, 4]

true

[9, 0, 2, 4, 7, 8]

[0, 2, 4]

[9, 0, 2, 4, 7, 8]

[0, 2, 4]

[9, 7, 8]

*/
```

## LinkedList

배열은 가장 기본적인 형태의 자료구조로 구조가 간단하며 사용하기 쉽고 데이터를 읽고 오는데 걸리는 시간이 가장 빠르다는 장점을 가지고 있지만 단점도 있다.

>크기를 변경할 수 없다.  
>비순차적인 데이터의 추가 또는 삭제에 시간이 많이 걸린다.

기본적으로 링크드 리스트의 각 요소들은 아래가 핵심이다.
```java
class Node {
    Node next;  // 다음 요소의 주소를 저장
    Object obj; // 데이터를 저장
}
```

위의 ``Node``요소로 인해 어떠한 값을 삭제 시 이전 Node의 주소 값을 삭제할 Node의 다음 Node의 주소값을 넣어주면 연결된 고리가 끊기면서 삭제가 되는 것이다.

이러한 링크드 리스트는 단방향이기에 마지막 Index까지 이동한 후 이전 Node를 확인하려면 다시 처음 Node부터 순차탐색이 이루어져야 한다. 이를 개선한 것이 ``더블 링크드 리스트``이다. 

```java
class Node {
    Node next;      // 다음 요소의 주소를 저장
    Node previous;  // 이전 요소의 주소를 저장
    Object obj;     // 데이터를 저장
}
```

더블 링크드 리스트는 이전 Node의 주소도 저장하기에 뒤로도 탐색이 가능하다. 하지만 위의 언급한 상황인 마지막 Node에서 처음 Node를 탐색할 경우가 생길 경우 이전 Node를 알기에 접근이 가능하지만 효율적이지 못하다. 이를 해결하기 위해 개선된 것인 ``더블 서큘러 링크드 리스트``이다. 더블 링크드 리스트의 첫 Node와 마지막 Node를 연결한 것이다.  

```java
public String linkedList() {

    String rtnValue = "";

    List<Integer> list = new LinkedList<>();

    list.add(1);
    list.add(2);
    list.add(3);
    list.add(4);
    list.add(5);
        rtnValue = printService.print(rtnValue, list);

    // 마지막 Node부터 검색하며 매개변수로 입력한 값의 Index를 return한다.
    list.lastIndexOf(3);
        rtnValue = printService.print(rtnValue, list);

    // 지정된 위치의 값을 변경한다.
    list.set(2,6);
        rtnValue = printService.print(rtnValue, list);

    // LinkedList에 저장된 값을 배열로 반환
    Object[] array = list.toArray();
        rtnValue = printService.print(rtnValue, array.toString());

    // 전달된 매개변수를 요소의 끝에 추가
    ((LinkedList<Integer>) list).offer(7);
        rtnValue = printService.print(rtnValue, list);

    // LinkedList의 첫번째 요소를 반환
    int temp = ((LinkedList<Integer>) list).element();
        rtnValue = printService.print(rtnValue, temp);
        rtnValue = printService.print(rtnValue, list);

    // LinkedList의 첫번째 요소를 반환
    temp = ((LinkedList<Integer>) list).peek();
        rtnValue = printService.print(rtnValue, temp);
        rtnValue = printService.print(rtnValue, list);

    // LinkedList의 첫번째 요소를 반환 -> List에서는 제거된다.
    temp = ((LinkedList<Integer>) list).poll();
        rtnValue = printService.print(rtnValue, temp);
        rtnValue = printService.print(rtnValue, list);

    return rtnValue;
}
public class PrintService {

    public String print(Object obj1, Object obj2) {

        obj1 += obj2.toString() + "\n\n";
        return obj1.toString();
    }
}

/**
출력결과
[1, 2, 3, 4, 5]

[1, 2, 3, 4, 5]

[1, 2, 6, 4, 5]

[Ljava.lang.Object;@6070c680

[1, 2, 6, 4, 5, 7]

1

[1, 2, 6, 4, 5, 7]

1

[1, 2, 6, 4, 5, 7]

1

[2, 6, 4, 5, 7]
*/
```

참고로, 순차적으로 추가/삭제 하는 경우에는 ArrayList가 LinkedList보다 빠르다. 그 이유는 ArrayList의 경우 index 순으로 알아서 저장이 된다. 그리고 마지막 Index부터 삭제가 이루어 진다면 단순 Index의 Value값을 Null 처리하는 방식이기에 빠르다 ``(단, 첫번째 부터 삭제 시 재배열이 이루어지므로 비효윺)``  

반면 중간 데이터를 추가/삭제하는 경우에는 LinkedList가 ArrayList보다 빠르다. 그 이유는 LinkedList의 경우 삭제하려는 Node를 찾아 이전 Node를 다음 Node로 연결만 해주면 되기에 ``재배열 처리를 하지 않아``도 되기에 시간 및 효율적이다. 

아래는 ArrayList -> LinkedList의 변환 방법이다. 중간값을 대량변경할 일이 있을경우 수행시간을 낮추기 위해 참고로 알아두자.
```java
List<Integer> al = new ArrayList<>();
for(int i=0; i<10000; i++) {
    al.add(i);
}

List<Integer> li = new LinkedList(al);
for(int j=0; j<10000; j++) {
    li.add(500, 0);
}
```

## Stack과 Queue

스택은 마지막에 저장한 데이터를 가장 먼저 꺼내는 방식인 ``LIFO(Last In First Out)`` 큐는 처음에 저장한 데이터를 가장 먼저 꺼내는 방식인 ``FIFO(First In First Out)`` 구조로 되어있다.  
순차적으로 저장을하고 마지막 Index를 삭제하는 **Stack**의 경우에는 ArrayList로 적합하다. 하지만 큐의 경우에는 항상 첫번째 데이터를 꺼내기 때문에 ArrayList같은 배열기반의 컬렉션 클래스를 사용한다면 데이터를 꺼낼 때마다 빈 공간을 채우기 위해 데이터의 복사가 발생하므로 비효율 적이다. 그래서 큐의 경우에는 추가/삭제가 쉬운 LinkedList로 구현하는 것이 적합하다.


**Stack**

|메서드|설  명|
|----|-----|
|boolean empty()|Stack이 비어있는지 알려준다.|
|Object peek()|Stack의 맨 위에 저장된 객체를 반환. pop()과 달리 Stack에서 객체를 꺼내지는 않음.|
|Object pop()|Stack의 맨 위에 저장된 객체를 꺼낸다.|
|Object push(Object item)|Stack에 객체(item)를 저장한다.|
|int search(Objecy o)|Stack에서 주어진 객체(o)를 찾아서 그 위치를 반환. 못찾으면 -1을 반환한다|

**Queue**

|메서드|설  명|
|----|-----|
|boolean add(Object o)|지정된 객체를 Queue에 추가한다.|
|Object remove()|Queue에서 객체를 꺼내 반환|
|Object element()|삭제없이 요소를 읽어 온다.|
|boolean offer(Object o)|Queue에 객체를 저장.|
|Object poll()|Queue에서 객체를 꺼내서 반환|
|Object peek()|삭제없이 요소를 읽어 온다.|

```java
public String stackAndQueue() {

    String rtnValue = "";

    Stack st = new Stack();
    Queue q = new LinkedList();

    st.push(0);
    st.push(1);
    st.push(2);
    rtnValue = printService.print(rtnValue, st);

    q.offer(0);
    q.offer(1);
    q.offer(2);
    rtnValue = printService.print(rtnValue, q);

    int temp = (int) st.peek();
    rtnValue = printService.print(rtnValue, temp);
    rtnValue = printService.print(rtnValue, st);

    temp = (int) st.pop();
    rtnValue = printService.print(rtnValue, temp);
    rtnValue = printService.print(rtnValue, st);

    temp = (int) q.element();
    rtnValue = printService.print(rtnValue, temp);
    rtnValue = printService.print(rtnValue, q);

    temp = (int) q.peek();
    rtnValue = printService.print(rtnValue, temp);
    rtnValue = printService.print(rtnValue, q);

    temp = (int) q.poll();
    rtnValue = printService.print(rtnValue, temp);
    rtnValue = printService.print(rtnValue, q);


    return rtnValue;

public class PrintService {

    public String print(Object obj1, Object obj2) {

        obj1 += obj2.toString() + "\n\n";
        return obj1.toString();
    }
}

/**
출력결과
[0, 1, 2]

[0, 1, 2]

2  // -> Stack peek()

[0, 1, 2]

2  // -> Stack pop()

[0, 1]

0  // -> Queue element()

[0, 1, 2]

0 // -> Queue peek()

[0, 1, 2]

0 // -? Queue poll()

[1, 2]
*/
```
## PriorityQueue

Queue인테페이스의 구현제 중의 하나로 저장한 순서에 관계없이 우선순위가 높은 것부터 꺼내며 Null로 저장할 수 없다. PriortyQueue는 저장공간으로 배열을 사용하며, 각 요소를 ``'힙(heap)'``이라는 자료구조 형태로 저장한다.  저장순서가 3,1,5,2,4 인데도 출력결과는 1,2,3,4,5이다. 우선순위는 숫자가 작을수록 높은 것이므로 1이 가장먼저 출력된 것이다.

```java
class PriortyQueue {
    public static void main(String[] args) {
        Queue pq = new PriorityQueue();
        pq.offer(3);
        pq.offer(1);
        pq.offer(4);
        pq.offer(2);
        pq.offer(4);

        System.out.println(pq);

        Object obj = null;

        while((obj = pq.poll()) != null) {
            System.out.println(obj);
        }
    }
}

/**
출력결과
[1,2,5,3,4]
1
2
3
4
5
*/
```

## Deque
Queue의 변형으로, 한ㅈ 쪽 끝으로만 추가/삭제할 수 있는 Queue와 달리, Deque(덱, 디큐)은 양쪽 끝에 추가/삭제가 가능하다. 또한, Deque는 스택과 큐를 하나로 합쳐놓은 것과 같으며 스택으로 사용할수도 있고, 큐로 사용할 수도 있다.

## Iterator

컬렉션 프레임웍에서는 컬렉션에 저장된 요소들을 읽어오는 방법을 표준화하였다. 컬렉션에 저장된 각 요소에 접근하는 기능을 가진 Iterator인터페이스를 정의하고, Collection인터페이스dpsms ``Iterator``를 반환하는 iterator()를 정의하고 있다. Iterator는 주로 while문을 사용하여 컬렉션 클래스 요소들을 읽어 온다. 별도로 Map 컬렉션에서는 Key, Value를 하나의 쌍으로 저장하고 있기 때문에 iterator()를 직접 호출할 수 없고 ketSet(), entrySet()과 같은 메서드를 통해서 호출해야 한다. 

참고로 Set 컬렉션은 순서가 유지 되지 않기 때문에 iterator()를 통하여 순서대로 호출을 하여도 처음에 저장한 순서가 유지되지 않는다.

```java
List<Integer> list = new ArrayList<>();

Iterator it1 = list.iterator();

while(it1.hasNext()) {
    System.out.println(it1.next());
}


Map<Integer, Integer> map = new HashMap<>();

Iterator it2 = map.keySet().iterator();

while(it1.hasNext()) {
    System.out.println(it1.next());
}
```

## ListIterator

ListIteratorsms Iterator를 상속받아서 기능을 추가한 것으로, ``단방향(hasNext())``으로 접근하는 iterator와는 달리 **양방향**으로 접근이 가능하다. 단, ArrayList, LinkedList와 같이 List인터페이스를 구현한 컬렉션에서만 사용할 수 있다. iterator는 단방향으로만 이동하기 때문에 컬렉션의 마지막 요소에 다다르면 더이상 사용할 수 없지만, ListIterator는 양방향으로 이동하기 때문에 각 요소간의 이동이 자유롭다. 다만 이동하기 전에 반드시 hasNext(), hasPrevious()를 호출해서 체크하는 것이 필요하다.

|메서드|설  명|
|----|-----|
|boolean hasNext()|다음에 읽어 올 다음 요소가 있는지 확인|
|boolean hasPrevious()|이전에 읽어 올 요소가 있는지 확인|
|Object next()|다음 요소 반환|
|Object previous()|이전 요소 반환|

```java
public static void main(String[] args) {
    ArrayList list = new ArrayList();
    list.add("1");
    list.add("2");
    list.add("3");
    list.add("4");
    list.add("5");

    ListIterator it = list.listIterator();

    while(it.hasNext()) {
        System.out.print(it.next());
    }

    System.out.println();

    while(it.hasPrevious()) {
        System.out.print(it.previous);
    }
}

/**
출력결과
12345
54321
*/
```

## Arrays

Arrays는 배열을 다루는데 유용한 메서드가 정의되어 있다. 주로 사용하는 메서드만 정리해보자

**copyOf(), copyOfRange()**  
copyOf()는 배열의 전체를 복사하는 것이며 copyOfRange()는 배열의 일부를 복사하는 것이다.

```java
int[] arr = {0,1,2,3,4};
int[] arr2 = Arrays.copyOf(arr, arr.length);    // arr2=[0,1,2,3,4]
int[] arr3 = Arrays.copyOf(arr, 3);             // arr3=[0,1,2]
int[] arr4 = Arrays.copyOf(arr, 7);             // arr4=[0,1,2,3,4,0,0]

int[] arr5 = Arrays.copyOfRange(arr, 2, 4);     // arr5=[2,3] <- 4는 포함되지 않는다.
int[] arr6 = Arrays.copyOfRange(arr, 0, 7);     // arr4=[0,1,2,3,4,0,0]
```
**fill(), setAll()**  

fill()은 배열의 모든 요소를 지정된 값으로 채운다. setAll()은 배열을 채우는데 사용할 함수형 인터페이스르 매개변수로 받는다. 이 메서드를 호출할 때는 함수형 인터페이스를 구현한 객체를 매개변수로 지정하던가 아니면 람다식을 지정해야한다.

```java
int[] arr = new int[5]
Arrays.fill(arr, 9)                                 // arr=[9,9,9,9,9]
Arrays.setAll(arr, i -> (int) (Math.random()*5)+1); // arr=[1,5,2,1,1]
```
**sort(), binarySearch()**  
sort()는 배열을 정렬할 때 그리고 배열에 저장된 용소를 검색할 때는 binarySearch()를 사용한다. binarySearch()는 배열에서 지정된 값이 저장된 위치(index)를 찾아서 반환하는데 반드시 배열이 정렬된 상태여야지 한다. 

```java
int[] arr = {3, 2, 0, 1, 4};                // 정렬되지 않은 배열
int idx = Arrays.binarySearch(arr, 2);      // idx=-5 <- 잘못된 결과

Arrays.sort(arr);                           // [0, 1, 2, 3, 4]
int idx = Arrays.binarySearch(arr, 2);      // idx=2 <- 올바른 결과
```

**equals(), toString(), deppEquals(), deppToString()**  
간단하게 비교하자면 toString() 1차원, deepToString() 다차원 배열 equals()도 1차원 deppEquals()는 다차원 비교 이다. 아래 소스를 보면 이해가 갈 것이다.
```java
int[] arr = {0, 1, 2, 3, 4};
int[][] arr2D = { {11,12}, {21,22} };

Arrays.toString(arr)        // [0,1,2,3,4]
Arrays.deepToString(arr2D)  // [[11,12],[21,22]]
```

**asList(Object o)**  
asList()는 배열을 List에 담아서 변환한다. 한가지 주의할 점은 asList()가 변환한 List의 크기를 변경할 수 없다는 것이다.  
```java
List list = Arrays.asList(new Integer[]{1,2,3,4,5})
List list = Arrays.asList(1,2,3,4,5)
list.add(6);        // 에외 발생 List size 추가 및 삭제 불가
```
만일 추가 or 삭제를 하려면 ``List list = new ArrayList(Arrays.asList(1,2,3,4,5))``의 형식으로 선언을 하면 list에 추가를 할 수 있다. 참고로 알아두자.

## HashSet
HashSet은 Set인터페이스의 특징대로 중복된 요소를 저장하지 않는다. 만일 중복된 요소를 추가하게 될 경우 ``boolean(false)``를 반환한다. Set을 활용하여 저장된 순서를 유지하고자 한다면 ``LinkedHashSet``을 사용해야 한다. 아래는 중복을 허용하지 않는 HashSet을 활용한 로또 번호 추출이다. 초기 set에 저장된 값을 LinkedList클래스로 복사를 하고 Collections.sort(list)를 활용하여 저장된 값을 정렬 처리하였다.

```java
public static void main(String[] args) {
    Set set = new HashSet();

    for(int i=0; set.size() < 6; i++) {
        int num = (int) (Math.random()*45) +1;
        set.add(new Integer(num));
    }

    List list = new LInkedList(set);    // LinkedList(Collection c)
    Collections.sort(list);
    System.out.println(list);
}
/**
출력결과 (매 수행시 다른 값이 반환 됨)
[7,11,17,18,24.,28]
*/
```

## TreeSet
TreeSet은 이진 검색 트리라는 자료구조의 형태로 데이터를 저장하는 컬렉션 클래스이다. 이진 검색 트리는 정렬, 검색, 범위검색에 높은 성능을 보이는 자료구조이며 TreeSet은 이진 검색 트리의 성능을 향상시킨 ``'레드-블랙 트리'``로 구현되어 있다. 중요한 점은 **중복된 데이터의 저장을 허용하지 않으며, 정렬된 위치에 저장하므로 저장순서를 유지하지도 않는다.**  
구조는 아래와 같은 Tree를 갖는다.
```java
                    (T1)

       (T1-1)                   (T1-2)

(T1-1-1)    (T1-1-2)    (T1-2-1)    (T1-2-2)
```

>T1은 최상위 부모노드이며, 그 아래 T1-1, T1-2의 자식노드를 갖고있다.  
>T1-1은 T1-1-1, T1-1-2의 부모노드  
>T1-2은 T1-2-1, T1-2-2의 부모노드  

왼쪽 마지막 값에서부터 오른쪽 값까지 값을 ``왼족노드 -> 부모노드 -> 오른쪽노드`` 순으로 읽어오면 오름차순으로 정렬된 순서를 얻을 수 있다. 바로 위의 HashSet예제에서 컬렉션 클래스만 바꾸면 정렬된 값을 얻을 수 있다. 저장(TreeSet.add(Object o)를 할때 정렬이 된 상태의 순서로 저장을 하기때문이다.

```java
public static void main(String[] args) {
    Set set = new TreeSet();

    for(int i=0; set.size() < 6; i++) {
        int num = (int) (Math.random()*45) +1;
        set.add(new Integer(num));
    }

    System.out.println(set);
}
/**
출력결과 (매 수행시 다른 값이 반환 됨)
[7,11,17,18,24.,28]
*/
```

참고적으로 알아두면 좋은 메서드는 아래와 같다. 

|메서드|설  명|
|----|-----|
|SortedSet headSet(Object to)|지정된 객체보다 작은 값의 객체들을 반환한다.|
|SortedSet headSet(Object to, boolean inclusive)|지정된 객체보다 작은 값의 객체들을 반환한다. inclusive가 true이면 같은 값도 반환|
|SortedSet subSet(Object from, Ojbect to)|범위 검색의 결과를 반환한다.|
|SortedSet tailSet(Object from)|지정된 객체보다 큰 값의 객체들을 반환한다.|

```java
public static void main(String[] args) {
    TreeSet set = new TreeSet();
    int[] score = {80, 95, 50, 35, 45, 65, 10, 100};

    for(int i=0; i< score.length; i++) {
        set.add(new Integer(score[i]));
    }

    System.out.println(set.headSet(new Integer(50)));
    System.out.println(set.tailSet(new Integer(50)));
}
/**
출력결과
[10,35,45]
[50,65,80,95,100]
*/
```




#### 위의 모든 정리내용은 자바의 정석을 공부하며 복습차 정리한 내용입니다. 