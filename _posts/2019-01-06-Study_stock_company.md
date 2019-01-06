---
layout: customize-posts
title: "스택/큐(Stack/Queue) - 주식회사"
date: 2019-01-06
last_modified_at: 2019-01-06
description: "코딩문제 알고리즘 스택 큐를 활용하여 주식회사 유지기간 return"
keywords:
    - stack
    - queue
    - alogrithm
    - array
    - coding
    - test
    - 코딩테스트
    - 테스트
    - 자바
    - java
    - 주식회사
    - 프로그래머스
category:
    - Study
tags:
    - java
    - algorithm
published: true
sitemap:
    changefreq: daily
    priority: 1.0
---

## 스택/큐(Stack/Queue) - 주식회사

>[문제 설명] 
>
>초 단위로 기록된 주식가격이 담긴 배열 prices가 매개변수로 주어질 때, 가격이 유지된 기간은 몇 초인지를 return 하도록 solution 함수를 완성하세요.  
>  
>[제한사항]  
>prices의 각 가격은 1 이상 10,000 이하인 자연수입니다.  
>prices의 길이는 2 이상 100,000 이하입니다.  
>[입출력 예]  
>
>|prices|return|
>|------|------|
>|[498,501,470,489]|[2,1,1,0]|  
>
>[입출력 예 설명]
>* 1초 시점의 ₩498은 2초간 가격을 유지하고, 3초 시점에 ₩470으로 떨어졌습니다.
>* 2초 시점의 ₩501은 1초간 가격을 유지하고, 3초 시점에 ₩470으로 떨어졌습니다.
>* 3초 시점의 ₩470은 최종 시점까지 총 1초간 가격이 떨어지지 않았습니다.
>* 4초 시점의 ₩489은 최종 시점까지 총 0초간 가격이 떨어지지 않았습니다.

## 문제풀이

```java
class Solution {
    
    public int[] solution(int[] prices) {
        int[] answer = new int[prices.length];
        
        return result(prices, answer);
    }
    
    public int[] result(int[] price, int[] answer) {
        
        for(int i=0; i<price.length; i++){
            int tmp = price[i];
            int count=0;
            
            for(int j=i; j<price.length; j++){
                if(tmp <= price[j]) {
                    if (j != price.length -1) {
                        ++count;
                    }
                } else {
                    break;
                }
            }   
            answer[i] = count;
        }
        return answer;
    }
}
```

주어진 문제의 타이틀은 스택과 큐에 대한 내용이다.  
하지만 스택, 큐를 활용하여 풀지 않아도 되고 단순 array로 풀어도 쉽게 풀어지는 문제이기에 array를 활용하여 풀어 보았다.  

우선 **return**변수인 ```answer```의 사이즈를 초기화가 필요하다. 
>```int[] answer = new int[prices.length]```

for문을 통하여 주어진 테스트 케이스 배열의 원소를 임시변수에 저장을 해두며 side 원소와 크기 비료를 한다.  
right 원소가 ```tmp```의 원소보다 크면 ```count```값을 증가처리를 해주고,  
right 원소가 ```tmp```의 원소보다 작으면 ```break```를 통하여 다음 step 다음 index 원소를 비교한다.  

```java
if (j != price.length -1) {
    ++count;
}
```
위의 if 조건문은 마지막원소의 위치를 비교하여 count값을 증가처리를 안하는 부분이다.  
입출력 예 설명을 보면 ```"4초 시점의 ₩489은 최종 시점까지 총 0초간 가격이 떨어지지 않았습니다."```  
이 부분을 위해 마지막 원소일 경우 **0초**로 셋팅을 위해 추가를 해두었다.

소스 채점을 한 결과 정합성, 효율성 모두 통과가 되었다.  
효율성이 통과한건 다소 의외였다;; 중첩 for문을 사용해서 효율성 점수가 낮을 것 이라고 생각을 했는데 통과가 되었다.

##### 혹시 다른 효율적인 풀이방법이 있으시면 피드백 부탁드립니다.!
