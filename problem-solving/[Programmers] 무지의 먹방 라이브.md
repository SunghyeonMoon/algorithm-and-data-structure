# [Programmers] [무지의 먹방 라이브](https://programmers.co.kr/learn/courses/30/lessons/42891)

## 1차 풀이

```py
from collections import deque

def solution(food_times, k):
    food_times = deque([[value, idx] for idx, value in enumerate(food_times)])
    for _ in range(k):
        food_times[0][0] -= 1
        if food_times[0][0]:
            food_times.rotate(-1)
        else:
            food_times.popleft()
            if not food_times:
                return -1
    return food_times[0][1] + 1
```

## 2차 풀이

```py
import heapq

def solution(food_times, k):
    if sum(food_times) <= k:
        return -1
    heap = []
    for idx, food_time in enumerate(food_times):
        heapq.heappush(heap, (food_time, idx))
    cum = 0
    complete = set()
    while True:
        if (heap[0][0] - cum) * len(heap) <= k:
            time, idx = heapq.heappop(heap)
            time -= cum
            cum += time
            complete.add(idx)
            k -= time * (len(heap) + 1)
        else:
            return sorted(heap, key = lambda x: x[1])[k % len(heap)][1] + 1
```
