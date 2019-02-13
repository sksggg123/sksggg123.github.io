---
layout: customize-posts
title: "LeetCode - Sort Array By Parity"
date: 2019-02-06
last_modified_at: 2019-02-06
description: "코딩문제 알고리즘 leetCode SortArrayByParity"
header:
    teaser: /assets/images/blog/leetcode/LeetCode.png
    og_image: /assets/images/blog/leetcode/LeetCode.png
keywords:
    - array
    - list
    - linked
    - linkedlist
    - number
    - coding
    - sum
    - two
    - algorithm
    - leetcode
    - 알고리즘
    - jewel
    - stone
    - collection
    - set
    - list
    - hash
    - sort
category:
    - Algorithm
    - LeetCode
tags:
    - algorithm
published: true
sitemap:
    changefreq: daily
    priority: 1.0
---

## LeetCode

[문제설명]

Given an array A of non-negative integers, return an array consisting of all the even elements of A, followed by all the odd elements of A.

You may return any answer array that satisfies this condition.

Example 1:
```java
Input: [3,1,2,4]

Output: [2,4,3,1]

The outputs [4,2,3,1], [2,4,1,3], and [4,2,1,3] would also be accepted.
```


## 문제풀이

```java
class Solution {
    public int[] sortArrayByParity(int[] A) {
        
        int[] returnArray = new int[A.length];
        List<Integer> even = new ArrayList<Integer>();
        List<Integer> odd = new ArrayList<Integer>();
        
        int loopSize = 0;
            
        for(int temp : A) {
            if(temp % 2 == 0) {
                even.add(temp);
            } else {
                odd.add(temp);
            }
        }
        
        for(int i=0; i<even.size(); i++) {
            returnArray[loopSize] = even.get(i);
            loopSize++;
        }
        
        for(int i=0; i<odd.size(); i++) {
            returnArray[loopSize] = odd.get(i);
            loopSize++;
        }
        
        return returnArray;
    }
}
```

### [수행시간]
![submit](/assets/images/blog/leetcode/Sort_Array_By_Parity.png)

주어진 Array A에 임의의 Element들이 있다. 각 Element를 비교하여 홀수인지, 짝수인지를 판단하여 List에 각각 넣은 뒤 return Array에 셋팅 해주면 끝이난다.  
별도로 정렬은 요구하지 않았으며, 단지 짝수를 index 0 부터 시작하여 셋팅을 하고 짝수 셋팅이 완료된 후 홀수 셋팅을 하면된다. 짝수와 홀수의 분기는 loopSize 변수를 공유하여 셋팅되게 풀어 보았다.

##### 혹시 다른 효율적인 풀이방법이 있으시면 피드백 부탁드립니다.!
