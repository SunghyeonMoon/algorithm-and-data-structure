# [Leetcode] 136. [Single Number](https://leetcode.com/problems/single-number/)

## 알고리즘 분류
비트

## 풀이

같은 숫자끼리 XOR 연산을 하면 0이 된다는 점을 이용해서 모든 숫자끼리 XOR을 해서 남는 숫자를 리턴하는 풀이

```py
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        answer = 0
        for num in nums:
            answer ^= num
        return answer
```
