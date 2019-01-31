---
layout: customize-posts
title: "LeetCode - Adad Two Numbers"
date: 2019-01-27
last_modified_at: 2019-01-27
description: "코딩문제 알고리즘 leetCode add two numbers"
header:
    teaser: /assets/images/blog/leetcode/add_two_numbers.png
    og_image: /assets/images/blog/leetcode/add_two_numbers.png
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
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:

```java
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

## 문제풀이

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    
    List<ListNode> link = new ArrayList<ListNode>();
   int cnt = 0;
   ListNode rtnNode;
    
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        
        ListNode list = settingNode(l1, l2);
                
        return list;
        
        
    }
    
    ListNode settingNode(ListNode nodeOne, ListNode nodeTwo) {
      
        if(nodeOne.val >= 0 && nodeTwo.val >= 0) {
            
            if((nodeOne.val + nodeTwo.val) / 10 >= 1) {
                
                nodeOne.val = (nodeOne.val + nodeTwo.val) % 10;
                
                if(nodeOne.next != null && nodeTwo.next != null) {
                    
                    nodeOne.next.val++;
                    settingNode(nodeOne.next, nodeTwo.next);
                    
                } else if(nodeOne.next != null && nodeTwo.next == null) {
                    
                    nodeOne.next.val++;
                    nodeTwo.next = new ListNode(0);
                    settingNode(nodeOne.next, nodeTwo.next);
                } else if(nodeOne.next == null && nodeTwo.next != null) {
                    
                    nodeTwo.next.val++;
                    nodeOne.next = new ListNode(0);
                    settingNode(nodeOne.next, nodeTwo.next);
                } else {
                    
                    nodeOne.next = new ListNode(1);
                    return nodeOne;
                }
                
            } else {
                
                nodeOne.val = nodeOne.val + nodeTwo.val;
                
                if(nodeOne.next != null && nodeTwo.next != null) {
                    
                    settingNode(nodeOne.next, nodeTwo.next);
                    
                } else if(nodeOne.next != null && nodeTwo.next == null) {
                    
                    nodeTwo.next = new ListNode(0);
                    settingNode(nodeOne.next, nodeTwo.next);
                } else if(nodeOne.next == null && nodeTwo.next != null) {
                    
                    nodeOne.next = new ListNode(0);
                    settingNode(nodeOne.next, nodeTwo.next);
                }
                
            }
            
            return nodeOne;
        } else {
            return new ListNode(0);
        }
      
   }
}
```

두개의 LinkedList 형태의 객체를 매개변수로 받아 자릿수 끼리 Sum하는 문제이다. 풀이는 재귀호출를 통하여 작성하였으며, 매개변수로 전달한 node의 value값에 Sum한 값으로 재정의 하여 기존 node를 return 하였다.  

매개변수를 재사용한 이유는 최초 문제 작성하여 제출하였을때 **Memory Limit Exccede**가 발생하여 오류로 떨어지고 있어 혹시 Test Case에 Value값이 많은 Case로 인해 복사 or 신규 생성한 Node 객체가 원인이지 않을까 하여 기존 매개변수를 재사용 하였다. 

위의 로직은 20ms 정도로 평균정도 수행속도로 측정되었다.

![submit](/assets/images/blog/leetcode/add_two_numbers.png)

위의 로직에서 난잡하게되어있는 ```settingNode```메서드의 ``if``조건을 정리할 필요가 있다.  


##### 혹시 다른 효율적인 풀이방법이 있으시면 피드백 부탁드립니다.!
