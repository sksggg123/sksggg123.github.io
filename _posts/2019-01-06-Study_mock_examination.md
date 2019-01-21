---
layout: customize-posts
title: "완전탐색(Broute Force Search) - 모의고사"
date: 2019-01-21
last_modified_at: 2019-01-21
description: "코딩문제 알고리즘 완전탐색을 통해 모의고사의 정답률이 높은 수험생 return"
keywords:
    - 완전탐색
    - 탐색
    - alogrithm
    - array
    - coding
    - test
    - 코딩테스트
    - 테스트
    - 자바
    - java
    - 모의고사
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

## 완전탐색(Broute Force Search) - 모의고사

>[문제 설명]  
>수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다. 수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다.  
> 
>1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...  
>2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...  
>3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...  
>
>1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.  
>
>[제한 조건]  
>시험은 최대 10,000 문제로 구성되어있습니다.  
>문제의 정답은 1, 2, 3, 4, 5중 하나입니다.  
>가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.  
>
>[입출력 예]  
>
>|answers|	return|
>|-------|--------|
>|[1,2,3,4,5]|	[1]|
>|[1,3,2,4,2]|	[1,2,3]|
>
>[입출력 예 설명]
>입출력 예 #1
>1. 수포자 1은 모든 문제를 맞혔습니다.
>2. 수포자 2는 모든 문제를 틀렸습니다.
>3. 수포자 3은 모든 문제를 틀렸습니다.
>따라서 가장 문제를 많이 맞힌 사람은 수포자 1입니다.
>
>입출력 예 #2
>1.수포자 1은 [1, 4]번 문제를 맞혔습니다.
>2.수포자 2는 다섯 번째 문제를 맞혔습니다.

## 문제풀이

```java
import java.util.ArrayList;
import java.util.List;
import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;

class Solution {
    int[] one;
    int[] two;
    int[] three;

    public int[] solution(int[] answers) {
        
        if(answers.length > 10000) {
            int[] answer = {0};
            return answer;
        }
        
        int[] value = new int[3];
        List<Integer> threeAnswerList = new ArrayList<Integer>();
        threeAnswerList.add(3);
        threeAnswerList.add(1);
        threeAnswerList.add(2);
        threeAnswerList.add(4);
        threeAnswerList.add(5);
        
        int answerSize = answers.length;
        
        // 첫번째 수험생 답
        int oneStart = 0;
        one = new int[answerSize];
        for(int i=0; i<answerSize; i++) {
            if(oneStart < 5 && oneStart >= 0) {
                oneStart++;
                one[i] = oneStart;
            } else {
                oneStart = 1;
                one[i] = oneStart;
            }
            if(one[i] == answers[i]) {
                value[0]++;
            }
        }
        
        // 두번째 수험생 답
        int twoStart = 0;
        two = new int[answerSize];
        for(int i=0; i<answerSize; i++) {
            // 홀수 array index
            if(i % 2 == 1) {
                if(twoStart < 5 && twoStart >= 0) {
                    twoStart++;
                    if(twoStart == 2) {
                        twoStart++;
                    }
                    two[i] = twoStart;
                } else {
                    twoStart = 1;
                    two[i] = twoStart;
                }
            }
            // 짝수 array index
            else {
                two[i] = 2;
            }
            if(two[i] == answers[i]) {
                value[1]++;
            }
        }
        
        // 세번째 수험생 답
        int threeStart = 0;
        three = new int[answerSize];
        for(int i=0; i<answerSize; i++) {
            three[i] = threeAnswerList.get(threeStart%4);
            
            if(i%2 == 1) {
                if (!(threeStart < 5 && threeStart >= 0)) {
                    threeStart = 0;
                } else {
                    threeStart++;
                }
            }
            if(three[i] == answers[i]) {
                value[2]++;
            }
        }
        
        return returnValue(answers, value);
    }
    
    int[] returnValue(int[] answers, int[] value) {
        
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        map.put(1, value[0]);
        map.put(2, value[1]);
        map.put(3, value[2]);
        
        int max = 0;
        int dup = 0;
        for(int i=0; i<map.size(); i++) {
            if(max < map.get(i+1)) {
                max = map.get(i+1);
                dup = 1;
            } else if (max == map.get(i+1)) {
                dup++;
            }
        }
        
        int[] answer = new int[dup];
        int cnt = 1;
		for( int key : map.keySet() ) { 
            if(max == (int) map.get(key)) {
                answer[cnt-1] = cnt; 
            }
            cnt++;
        }
        
        return answer;
    }
}
```

처음에는 주어진 문제를 위와 같이 접근하여 풀어보았다.  
의식의 흐름따라 쭉 코딩해본결과 120 라인정도 되었고, 그 과정과정마다의 반복문이 늘어났다. 다행인건 O(n) 복잡도로 구현이 되었다.  

구현과정은  
첫째, 수험색 3명 답지 패턴을 직접 계산하여 수험색 답안지 구현   
둘쨰, 첫째에서 구현한 답안지와  ```answer```를 비교  
셋쨰, 둘째에서 비교 시 Map Collection을 통하여 우선순위 정렬  

기본적으로 코딩과정에 주어진 테스트 케이스는 통과되었다. 그 후 코드채점을 해본결과 탈락... 뭔가 쉽게 된다 싶었다.    
아래 이미지는 코드 채점 후 ```런타임 에러 7건```과 ```실패 1건```이 발생하였다.  

![알고리즘 테스트 케이스](/assets/images/blog/알고리즘_모의고사_채점결과.png)

코드를 쭉 다시 읽어본 결과.. 위의 구현 과정 중 **첫째 로직**은 전혀 필요없는 로직이였고, **둘째 로직** 또한 ```Math.Max()```를 통하여 한줄로 끝나는 문제였다.   
다시 한번 한심한 실력이란걸 느낀 문제풀이였다.  

```java
import java.util.ArrayList;
import java.util.List;

class Solution {

    public int[] solution(int[] answers) {
        
        // 수험생 답지 패턴
		int[] one = {1, 2, 3, 4, 5}; 
		int[] two = {2, 1, 2, 3, 2, 4, 2, 5}; 
		int[] three = {3, 3, 1, 1, 2, 2, 4, 4, 5, 5};
		
		// 수험생 별 답지 채점 결과 변수
		int oneCnt = 0;
		int twoCnt = 0;
		int threeCnt = 0;
		
		// 답지 패턴이 동일하기에 "%" 연산을 통해 나머지 값을 index로 활용
		for(int i=0; i<answers.length; i++) {
			if(answers[i] == one[i%5]) {
				oneCnt++;
			}
			if(answers[i] == two[i%8]) {
				twoCnt++;
			}
			if(answers[i] == three[i%10]) {
				threeCnt++;
			}
		}
		
		// Math메서드를 통하여 Max 값 계산
		int max = Math.max(oneCnt, Math.max(twoCnt, threeCnt));
		List<Integer> tempList = new ArrayList<Integer>();
		if (max == oneCnt) {
			tempList.add(1);
		}
		if (max == twoCnt) {
			tempList.add(2);
		}
		if (max == threeCnt) {
			tempList.add(3);
		}
        
        // tempList -> return Array로 복사 
        int[] answer = new int[tempList.size()];
		for(int i=0; i<tempList.size(); i++) {
			answer[i] = tempList.get(i);
		}
        
        return answer;
    }
}
```

위의 코드로는 코드 채점결과 모두 통과되었다.  
마무리하며 정리를 하자면 이미 주어진 패턴이 있었고 패턴에 따른 ```%``` 연산자를 확용하여 패턴을 ```answers```배열의 사이즈만큼 반복을 돌릴 수 있었고 Math메서드를 통하여 최대값을 손쉽게 구할 수 있었다. 

##### 혹시 다른 효율적인 풀이방법이 있으시면 피드백 부탁드립니다.