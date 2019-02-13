---
layout: customize-posts
title: "LeetCode - Unique Email Addresses"
date: 2019-02-04
last_modified_at: 2019-02-04
description: "코딩문제 알고리즘 leetCode UniqueEmailAddresses"
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
published: true
sitemap:
    changefreq: daily
    priority: 1.0
---

## LeetCode

[문제설명]

Every email consists of a local name and a domain name, separated by the @ sign.  

For example, in ``alice@leetcode.com``, alice is the local name, and ``leetcode.com`` is the domain name.  

Besides lowercase letters, these emails may contain '.'s or '+'s.  

If you add periods ('.') between some characters in the local name part of an email address, mail sent there will be forwarded to the same address without dots in the local name.  For example, ``"alice.z@leetcode.com"`` and ``"alicez@leetcode.com"`` forward to the same email address.  (Note that this rule does not apply for domain names.)  

If you add a plus ('+') in the local name, everything after the first plus sign will be ignored. This allows certain emails to be filtered, for example ``m.y+name@email.com`` will   be forwarded to ``my@email.com.``  (Again, this rule does not apply for domain names.)  

It is possible to use both of these rules at the same time.  

Given a list of emails, we send one email to each address in the list.  How many different addresses actually receive mails?  

Example 1:
```java
Input: ["test.email+alex@leetcode.com","test.e.mail+bob.cathy@leetcode.com","testemail+david@lee.tcode.com"]

Output: 2

Explanation: "testemail@leetcode.com" and "testemail@lee.tcode.com" actually receive mails
```


## 문제풀이

```java
class Solution {
    public int numUniqueEmails(String[] emails) {
                
        Set<String> setEmail = new HashSet<String>();
        
        for(int i=0; i<emails.length; i++) {
            
            String[] dummy = emails[i].split("@");
            String[] dummyAliceOne = dummy[0].split("\\+");
            String[] dummyAliceTwo = dummyAliceOne[0].split("\\.");
            String sb = "";
            
            for(int j=0; j<dummyAliceTwo.length; j++) {
                sb += dummyAliceTwo[j];
            }
            
            setEmail.add(sb+"@"+dummy[1]);
        }
        
        Iterator<String> it = setEmail.iterator();
		while(it.hasNext()) {
			
			String temp = it.next();
			System.out.print(temp+ " ");
		}
		
		return setEmail.size();
        
    }
}
```

![submit](/assets/images/blog/leetcode/Unique_Emali_Address.png)

이번 문제는 주어진 Email Address Array값을 조건 ``" + "``와 ``" . "``의 경우 제거와 붙이기 작업을 해주면 된다. 위의 소스에서 dummyAliceOne의 경우는 첫번째 Index만 사용 하면되고 ( " + " 일경우 뒤에는 버리면 됨.) dummyAliceTwo의 경우에는 " . " 은 합치는 작업을 해야하기에 반복문을 하나 더 추가하여 처리를 하였다.  

작업 후 중복된 것을 제거하는 조건(동일 Eamil의 경우 한번 발송)이 있기에, **Collection Set**을 사용하여 처리하였다. Set의 경우 기본적으로 중복된 값을 제거하고 담기에 이번 문제에 적합한 Collection이다.

##### 혹시 다른 효율적인 풀이방법이 있으시면 피드백 부탁드립니다.!
