---
layout: customize-posts
title: "해시(Hash) - 완주하지 못한 선수"
date: 2019-01-03
last_modified_at: 2019-01-03
description: "(programmers)프로그래머스 코딩연습, (Hash)해시를 활용한 완주하지 못한 선수 찾기"
keywords:
    - Hash
    - Map
    - 해시
    - 알고리즘
    - algorithm
category:
    - Algorithm
    - Programmers
tags:
    - algorithm
published: false
sitemap: 
    changefreq: daily
    priority: 1.0
---

>[문제 설명]  
>수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.  
>
>마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.  
>
>[제한사항]  
>마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.  
>completion의 길이는 participant의 길이보다 1 작습니다.  
>참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.  
>참가자 중에는 동명이인이 있을 수 있습니다.  
>
>[입출력 예]  
>
>|participant|	completion|	return|
>|-----------|------------|-------|
>|[leo, kiki, eden]|	[eden, kiki]|	leo|
>|[marina, josipa, nikola, vinko, filipa]|	[josipa, filipa, marina, nikola]|	vinko|
>|[mislav, stanko, mislav, ana]	|[stanko, ana, mislav]|	mislav|
>
>[입출력 예 설명]
>예제 #1  
>leo는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.  
>
>예제 #2  
>vinko는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.  
>
>예제 #3  
>mislav는 참여자 명단에는 두 명이 있지만, 완주자 명단에는 한 명밖에 없기 때문에 한명은 완주하지 못했습니다.  

## 문제풀이

```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.Iterator;
import java.util.List;
import java.util.Map;

class Solution {
    
    static String ANSWER = "";
   static List<String> DUP_LIST = new ArrayList<String>();
    
    public String solution(String[] participant, String[] completion) {
      Map<String, Integer> map = new HashMap<String, Integer>();
     
        for(int i=0; i<participant.length; i++) {
           int value = 0;
           if(map.get(participant[i]) != null && map.get(participant[i]) > 0) {
              value = map.get(participant[i]);
              map.put(participant[i], ++value);
           }else {
              map.put(participant[i], 1);
           }
        }
        
        for(int i=0; i<completion.length; i++) {
           int value = 0;
           value = map.get(completion[i]);
          map.put(completion[i], --value);
        }
     
        Iterator<String> it = map.keySet().iterator();
        while (it.hasNext()) {
           String key = it.next();
           if(map.get(key) >= 1) {
              ANSWER = key;
           }
        }
              
        return ANSWER;
    }
}
```

이번은 제목과 같은 Hash Map을 사용하여 풀어 보았다.  
```participant``` **참여한 명단**과 ```completion``` **완주한 명단**을 Map에 셋팅을하여,  
**Iterator**를 통해 Map의 value값이 ```1```인 ```Key``` 값을 찾아내면 끝나는 문제였다.  
>```key=name, value=카운트(참여 -> ++ | 완주 -> --)```  

처음에 문제를 보고 왜 Hash 카테고리에 있지? 라는 생각을 하였다.  
그렇게 생각한 이유는 ```참여List``` 와 ```완주List```을 사용하여 ```완주List```에서 index별로 차례대로 가져와서 ```참여List.contains()```으로 값이 **true**면 index삭제 하는 형식으로 접근을 하였다.  

작성하고 보면 코딩의 Line도 위에 것과 비교 시 길며, 무엇보다 collection 타입을 2개를 생성하여 ```contains``` 쿼리의 ```LIKE``` 와 같은 느낌이여서 찝찝하였다.  

그리고 Hash카테고리인 만큼 Map을 사용하는게 의도와 부합하다고 생각이 들었다.  

