---
layout: customize-posts
title: "LeetCode - Jewels and Stones"
date: 2019-02-03
last_modified_at: 2019-02-03
description: "코딩문제 알고리즘 leetCode Jewels and Stones"
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
category:
    - Algorithm
    - LeetCode
tags:
    - algorithm
published: false
sitemap:
    changefreq: daily
    priority: 1.0
---

## LeetCode

[문제설명]

You're given strings J representing the types of stones that are jewels, and S representing the stones you have.  Each character in S is a type of stone you have.  You want to know how many of the stones you have are also jewels.

The letters in J are guaranteed distinct, and all characters in J and S are letters. Letters are case sensitive, so "a" is considered a different type of stone from "A".


Example 1:
```java
Input: J = "aA", S = "aAAbbbb"
Output: 3
```

Example 2:
```java
Input: J = "z", S = "ZZ"
Output: 0
Note:
```

S and J will consist of letters and have length at most 50.
The characters in J are distinct.

## 문제풀이

```java

// 첫번째 풀이
// ===================================================================
class Solution {
    public int numJewelsInStones(String J, String S) {
        
        String[] dummyJ = J.split("");
      String[] dummyS = S.split("");
        int returnCount = 0;
      
      for(int i=0; i<dummyJ.length; i++) {
         for(int j=0; j<dummyS.length; j++) {
            if(dummyS[j].equals(dummyJ[i])) {
               returnCount++;
            }
         }
      }
        
        return returnCount;
    }
}
// ===================================================================


// 두번째 풀이
// ===================================================================
class Solution {
    public int numJewelsInStones(String J, String S) {
        
        int returnCount = 0;
      
      for(int i=0; i<J.length(); i++) {
         for(int j=0; j<S.length(); j++) {
            if(J.charAt(i) == S.charAt(j)) {
               returnCount++;
            }
         }
      }
        
        return returnCount;
    }
}
// ===================================================================
```
[수행시간 비교]
* 16ms -> 첫번째 풀이
* 10ms -> 두번째 풀이

![submit](/assets/images/blog/leetcode/Jewels_and_Stones.png)

J에 들어있는 원소(String)와 S에 들어있는 원소(String)가 같은게 있는지 있으면 몇개가 같은지 확인하는 문제이다. ``첫번째``는 아주 주어진 J, S의 원소를 배열에 담아 배열의 Size 만큼 반복수행하여 비교처리하는 방법이다. ``두번째``방법은  배열(Array)에 별도로 담는 작업을 하지 않고 주어진 J, S를 **charAt(Inext)** 를 사용하여 배열과 같이 비교처리하는 방법이다.


##### charAt 정의
>char java.lang.String.charAt(int index)  
>
>Returns the char value at thespecified index. An index ranges from 0 to length() - 1. The first char value of the sequenceis at index 0, the next at index 1,and so on, as for array indexing.   
>
>If the char value specified by the index is a surrogate, the surrogatevalue is returned.
>
>Specified by : charAt(...) in CharSequence  
>
>Parameters : index the index of the char value.Returns:the char value at the specified index of this string.The first char value is at index  0.  
>Throws : IndexOutOfBoundsException - if the indexargument is negative or not less than the length of thisstring.  


별도로 변수를 선언하지 않아 Heap 메모리의 Resource 차이도 있으며, 배열로 Clone하는 행위를 하지않기에 수행시간도 단축된다.  아래는 다른사람이 푼 경우인데 Collection - Set을 활용하여 처리하였다. 참고하면 좋을 것으로 보여 정리한다.

```java
class Solution {
    public int numJewelsInStones(String J, String S) {
        Set<Character> set = new HashSet<>();
        
        for (int i = 0; i < J.length(); i++) {
            char j = J.charAt(i);
            set.add(j);
            
        }
        
        int result = 0;
        for (int i = 0; i < S.length(); i++) {
            char s = S.charAt(i);
            if (set.contains(s)) {
                result++;
            }
        }
        return result;
    }
}
```

##### 혹시 다른 효율적인 풀이방법이 있으시면 피드백 부탁드립니다.!
