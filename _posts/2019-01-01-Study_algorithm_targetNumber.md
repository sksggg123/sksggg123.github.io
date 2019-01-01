---
layout: customize-posts
title: "깊이/너비 우선 탐색(DFS/BFS) - 타겟 넘버"
date: 2019-01-01
last_modified_at: 2019-01-01
description: "깊이/너비 우선 탐색(DFS/BFS)"
keywords:
    - DFS
    - BFS
    - 타겟 넘버
    - 깊이
    - 너비
    - 탐색
    - 우선
    - java
    - 자바
    - 알고리즘
    - 재귀
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

## 깊이/너비 우선 탐색(DFS/BFS) - 타겟 넘버

>[문제 설명]
>
>n개의 음이 아닌 정수가 있습니다. 이 수를 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다.
>예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.
>
>- -1+1+1+1+1 = 3
>- +1-1+1+1+1 = 3
>- +1+1-1+1+1 = 3
>- +1+1+1-1+1 = 3
>- +1+1+1+1-1 = 3
>
>사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.
>
>[제한사항]
>
>- 주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
>- 각 숫자는 1 이상 50 이하인 자연수입니다.
>- 타겟 넘버는 1 이상 1000 이하인 자연수입니다.
>
>[입출력 예]
>
>|numbers|target|return|
>|-------|------|------|
>|[1, 1, 1, 1, 1]|	3|	5|

## 문제풀이

```java
>1 class Solution {
>2
>3    static int ANSWER = 0;
>4    public int solution(int[] numbers, int target) {
>5
>6
>7        dfs(numbers, target, 0);
>8
>9        return ANSWER;
>10    }
>11
>12    private void dfs(int[] numbers, int target, int num) {
>13
>14		if ( num == numbers.length ) {
>15			int sum = 0;
>16			for (int i = 0; i < numbers.length; i++) {
>17				sum += numbers[i];
>18			}
>19			if ( sum == target ) {
>20				ANSWER++;
>21			}
>22		} else {
>23			numbers[num] *= 1;
>24			dfs(numbers, target, num+1);
>25
>26			numbers[num] *= -1;
>27			dfs(numbers, target, num+1);
>28		}
>29	}
>30 }
```

재귀호출을 이용하여 위의 문제를 풀어보았다. 재귀의 경우 Stack으로 보면 편한 것 같다.
특정 break poit를 기점으로 메소드 호출이 중단되며 가장 마지막에 호출한 이력이 가장먼저 처리해서 나오게 된다. (LIFO - Last In, First Out)

위의 소스에서는 Line 14번의 if 조건일 경우가 break point로 보면 된다.

위의 로직을 수행하게되면 재귀호출 시 **stack에 쌓인 num**변수의 상태 값은 아래와 같다.
Line 24번에서 우선적으로 재귀호출이 되며, Link 14번에서 ```num == numbers.length``` 값이 true가 되는 시점에 ANSWER의 전역변수를 1 증가 시킨다. 그 후 Line 27번의 재귀호출을 하게 된다.

첫 step에 출력된 상태를 보면 Number에 담긴 값은 모두 양수이며, 다음 step의 마지막이 음수인 것을 확인 할  수있다.

아래는 ```numbers={1,1,1,1,1}, target=3```의 조건으로 로직을 step별로 출력한 결과이다.

|Number[0]|Number[1]|Number[2]|Number[3]|Number[4]|Sum|Answer|
|---------|---------|---------|---------|---------|---|------|
| Number[0] : 1| Number[1] : 1| Number[2] : 1| Number[3] : 1| Number[4] : 1| Sum: 5 | Answer: 0|
| Number[0] : 1| Number[1] : 1| Number[2] : 1| Number[3] : 1| Number[4] : -1| Sum: 3 | Answer: 1|
| Number[0] : 1| Number[1] : 1| Number[2] : 1| Number[3] : -1| Number[4] : -1| Sum: 1 | Answer: 1|
| Number[0] : 1| Number[1] : 1| Number[2] : 1| Number[3] : -1| Number[4] : 1| Sum: 3 | Answer: 2|
| Number[0] : 1| Number[1] : 1| Number[2] : -1| Number[3] : -1| Number[4] : 1| Sum: 1 | Answer: 2|
| Number[0] : 1| Number[1] : 1| Number[2] : -1| Number[3] : -1| Number[4] : -1| Sum: -1 | Answer: 2|
| Number[0] : 1| Number[1] : 1| Number[2] : -1| Number[3] : 1| Number[4] : -1| Sum: 1 | Answer: 2|
| Number[0] : 1| Number[1] : 1| Number[2] : -1| Number[3] : 1| Number[4] : 1| Sum: 3 | Answer: 3|
| Number[0] : 1| Number[1] : -1| Number[2] : -1| Number[3] : 1| Number[4] : 1| Sum: 1 | Answer: 3|
| Number[0] : 1| Number[1] : -1| Number[2] : -1| Number[3] : 1| Number[4] : -1| Sum: -1 | Answer: 3|
| Number[0] : 1| Number[1] : -1| Number[2] : -1| Number[3] : -1| Number[4] : -1| Sum: -3 | Answer: 3|
| Number[0] : 1| Number[1] : -1| Number[2] : -1| Number[3] : -1| Number[4] : 1| Sum: -1 | Answer: 3|
| Number[0] : 1| Number[1] : -1| Number[2] : 1| Number[3] : -1| Number[4] : 1| Sum: 1 | Answer: 3|
| Number[0] : 1| Number[1] : -1| Number[2] : 1| Number[3] : -1| Number[4] : -1| Sum: -1 | Answer: 3|
| Number[0] : 1| Number[1] : -1| Number[2] : 1| Number[3] : 1| Number[4] : -1| Sum: 1 | Answer: 3|
| Number[0] : 1| Number[1] : -1| Number[2] : 1| Number[3] : 1| Number[4] : 1| Sum: 3 | Answer: 4|
| Number[0] : -1| Number[1] : -1| Number[2] : 1| Number[3] : 1| Number[4] : 1| Sum: 1 | Answer: 4|
| Number[0] : -1| Number[1] : -1| Number[2] : 1| Number[3] : 1| Number[4] : -1| Sum: -1 | Answer: 4|
| Number[0] : -1| Number[1] : -1| Number[2] : 1| Number[3] : -1| Number[4] : -1| Sum: -3 | Answer: 4|
| Number[0] : -1| Number[1] : -1| Number[2] : 1| Number[3] : -1| Number[4] : 1| Sum: -1 | Answer: 4|
| Number[0] : -1| Number[1] : -1| Number[2] : -1| Number[3] : -1| Number[4] : 1| Sum: -3 | Answer: 4|
| Number[0] : -1| Number[1] : -1| Number[2] : -1| Number[3] : -1| Number[4] : -1| Sum: -5 | Answer: 4|
| Number[0] : -1| Number[1] : -1| Number[2] : -1| Number[3] : 1| Number[4] : -1| Sum: -3 | Answer: 4|
| Number[0] : -1| Number[1] : -1| Number[2] : -1| Number[3] : 1| Number[4] : 1| Sum: -1 | Answer: 4|
| Number[0] : -1| Number[1] : 1| Number[2] : -1| Number[3] : 1| Number[4] : 1| Sum: 1 | Answer: 4|
| Number[0] : -1| Number[1] : 1| Number[2] : -1| Number[3] : 1| Number[4] : -1| Sum: -1 | Answer: 4|
| Number[0] : -1| Number[1] : 1| Number[2] : -1| Number[3] : -1| Number[4] : -1| Sum: -3 | Answer: 4|
| Number[0] : -1| Number[1] : 1| Number[2] : -1| Number[3] : -1| Number[4] : 1| Sum: -1 | Answer: 4|
| Number[0] : -1| Number[1] : 1| Number[2] : 1| Number[3] : -1| Number[4] : 1| Sum: 1 | Answer: 4|
| Number[0] : -1| Number[1] : 1| Number[2] : 1| Number[3] : -1| Number[4] : -1| Sum: -1 | Answer: 4|
| Number[0] : -1| Number[1] : 1| Number[2] : 1| Number[3] : 1| Number[4] : -1| Sum: 1 | Answer: 4|
| Number[0] : -1| Number[1] : 1| Number[2] : 1| Number[3] : 1| Number[4] : 1| Sum: 3 | Answer: 5|
