# [Leetcode] [Merge Intervals](https://leetcode.com/problems/merge-intervals/)

## Description

Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

## Constraints

- 1 <= intervals.length <= 104
- intervals[i].length == 2
- 0 <= starti <= endi <= 104

## Example

### Example1

Input: intervals = [[1,3],[2,6],[8,10],[15,18]]  
Output: [[1,6],[8,10],[15,18]]

### Example2

Input: intervals = [[1,4],[4,5]]  
Output: [[1,5]]

## Main Idea

1. Front Interval의 끝보다 Back Interval의 시작이 빠르다면 두 Interval은 합쳐진다.

![Idea1](https://user-images.githubusercontent.com/75469212/151913109-747c4289-2b64-4773-ad5e-49d28f0665cb.png)

2. Idea 1의 로직을 순서대로 시행하기 위해서는 Intervals의 Sort가 필요하다.

![정렬이 안된 경우](https://user-images.githubusercontent.com/75469212/151913141-de1a4aec-51e3-41a5-a0df-2c6ec42677f3.png)  
정렬 하지 않은 경우

![정렬이 된 경우](https://user-images.githubusercontent.com/75469212/151913259-4b97d660-c3b4-41e0-8941-afe78a5e6d22.png)  
정렬 한 경우

### 결론 - Intervals를 정렬해서 Interval을 선형적으로 즉, 순서대로 합쳐가면 되겠다.

## 구현

## 시각화

![구현설명1](https://user-images.githubusercontent.com/75469212/151921472-34f64463-d6d7-478a-8afb-af21b40ba4f1.png)  
answer[-1]의 끝이 interval의 시작보다 뒤라면
![구션설명2](https://user-images.githubusercontent.com/75469212/151921521-352374ab-4313-469f-ac3c-92bbcf44ae05.png)  
두 interval을 합친다
![구현설명3](https://user-images.githubusercontent.com/75469212/151921522-df900ce4-cd8c-4450-8cbd-216ea031a979.png)  
더 이상 합칠 수 없다면, 현재 interval을 answer[-1]로 설정

```py
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        intervals.sort()
        # 합쳐가는 now interval을 따로 변수로 관리 하지 않고, answer의 마지막 요소로 사용하면서, 변수를 하나 줄일 수 있다.
        answer = [intervals[0]]
        for interval in intervals[1:]:
            # answer[-1][1]은 현재 합치고 있는 interval의 끝점
            if answer[-1][1] >= interval[0]:
                # 합쳐지는 과정에서 반드시 뒤의 interval의 끝이 더 뒤라는 보장이 없으므로 두 interval의 끝을 비교해서 합친다.
                answer[-1][1] = max(answer[-1][1], interval[1])
            else:
                # 합칠 수 없다면, 현재의 interval을 시작으로 다시 로직을 시작한다.
                answer.append(interval)
        return answer
```

## 시간 복잡도

### intervals를 정렬하는 데 O(NlogN) 소요

파이썬 기본 sort 함수는 Merge Sort와 Insertion Sort의 장점을 합친 Tim Sort Algorithm을 사용한다.

- 참고: Tim Sort Algorithm에 대해서 추가적으로 설명 드리면, 실제로 사용되는 데이터들이 어느정도 정렬 되어있는 상태에 있을 것이라는 생각을 기반으로 합니다. Merge Sort를 끝까지 쪼개지 않고 임의의 배열로 쪼갠 후, 대부분 정렬되어 있으며 O(N)에 가깝게 정렬이 가능한 Insertion Sort를 사용하여 정렬 후에 합친다는 논리로 만들어진 알고리즘입니다.

| Algorithm | Best    | Average | Worst   |
| --------- | ------- | ------- | ------- |
| QuickSort | Nlog(N) | Nlog(N) | N^2     |
| MergeSort | Nlog(N) | Nlog(N) | Nlog(N) |
| Tim Sort  | N       | Nlog(N) | Nlog(N) |

### Intervals를 선형 탐색 하면서 O(N) 소요

### 결과적으로 O(NlogN)으로 풀이

## 풀이 회고

정렬 단원을 공부하면서 풀게된 문제라서 "정렬을 사용하면 쉽게 풀리지않을까?" 라는 힌트를 통해 실제 문제 난이도보다 쉽게 아이디어를 떠올릴 수 있었다.
