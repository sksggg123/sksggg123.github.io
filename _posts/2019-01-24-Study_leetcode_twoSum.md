---
layout: customize-posts
title: "LeetCode - Two Sum"
date: 2019-01-24
last_modified_at: 2019-01-24
description: "코딩문제 알고리즘 leetCode two sum"
keywords:
    - array
    - sum
    - two
    - algorithm
    - leetcode
    - 알고리즘
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

## LeetCode

[문제설명]  
Given an array of integers, return indices of the two numbers such that they add up to a specific target.  

You may assume that each input would have exactly one solution, and you may not use the same element twice.  

Example:

```java
Given nums = [2, 7, 11, 15], target = 9,
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1]
```

## 문제풀이

```java
class Solution {
    
    public int[] twoSum(int[] nums, int target) {
        
        int len = nums.length;
        int[] rtn = new int[2];
        
        loop : for(int i=0; i<len; i++) {
            
            for(int j=0; j<len; j++) {
                
                if(i != j) {
                    
                    int sum = nums[i] + nums[j];
                    
                    if(sum == target) {
                        
                        if( i < j) {
                            
                            rtn[0] = i;
                            rtn[1] = j;
                            
                        } else {
                            
                            rtn[0] = j;
                            rtn[1] = i;
                            break loop;
                            
                        }   
                    }   
                }   
            }           
        }
        
        return rtn;
    }   
}
```

반복문을 이중으로 수행하였다. 예제 테스트케이스는 통과되어 코드를 제출하여 다수의 테스트 케이스를 체크했을때 정답은 통과되었다. 하지만 수행시간이 아무래도 반복문을 이중으로 돌리다보니 **RunTime이 0.83ms**가 나왔으며 문제를 제출한 명단에 하위범주에 속하였다.

![first submit](/assets/images/blog/leetcode/two_sum_1.jpeg)

소스코드를 다시 읽어봤을때 안에있는 반복문 변수 초기화 부분과, 조건문 하나가 필요가 없어보였다.  
- ``for(int j=0; j<len; j++) -> for(int j=i; j<len; j++)`` 변경
- ``if( i != j )`` 제거

```java
class Solution {
    
    public int[] twoSum(int[] nums, int target) {
        
        int len = nums.length;
        int[] rtn = new int[2];
        
        loop : for(int i=0; i<len; i++) {
            
            for(int j=i+1; j<len; j++) {
                   
                int sum = nums[i] + nums[j];

                if(sum == target) {

                    if( i < j) {

                        rtn[0] = i;
                        rtn[1] = j;

                    } else {

                        rtn[0] = j;
                        rtn[1] = i;
                        break loop;

                    }
                }                   
            }
        }
        
        return rtn;
    }
}
```

![second submit](/assets/images/blog/leetcode/two_sum_2.jpeg)


굳이 비교하려는 초기값을 '0'부터 시작하고 조건문까지 사용하여 로직을 처리할 필요가 없기에 삭제처리를 하였고 코드제출 결과 위의 캡처와 같은 RunTime을 얻었다. 그래도 여전히 수행시간은 길었고, 하위 16% 정도의 소스코드로 되어있다. 반복문을 걷어내자.. 그래야 RunTime이 중상위권 으로 올라갈 것 같다...

```java
class Solution {
    
    public int[] twoSum(int[] nums, int target) {
        
        final int len = nums.length;
        Map<Integer, Integer> cloneMap = new HashMap<Integer, Integer>();
        
        for(int i=1; i<len; i++) {
            cloneMap.put(nums[i], i);
        }
        
        for(int i=0; i<len; i++) {
            int key = target - nums[i];
            if(cloneMap.containsKey(key) && cloneMap.get(key) != i) {
                return new int[] {i, cloneMap.get(key)};
            }
        }       
        return new int[] {0};
    }
}
```
![third submit](/assets/images/blog/leetcode/two_sum_3.jpeg)

최종소스는 위와 같다. Map을 통해 Key와 Value를 활용해보았다. 
- ``Key -> nums 배열의 원소 값``
- ``Value -> 배열의 Index 값``

``int key = target - nums[i]``를 통해 Key(nums배열의 원소 값)을 얻어 Map에 해당 Key값이 포함되어있는지 확인 and 동일한 index값은 논외이기에 ``Map.get(key) != i``를 통해 걸러내어 return 시키면 원하는 값을 얻을 수 가 있고 반복문을 한번만 사용했기에 RunTime이 대폭 줄었다.

##### 혹시 다른 효율적인 풀이방법이 있으시면 피드백 부탁드립니다.!
