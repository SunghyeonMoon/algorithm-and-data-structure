# [Leetcode] 787. [Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/)

## 풀이

거리가 짧은 순으로 들어오는데 k가 만족하는지 확인
하지만 k가 더 크게 들어오는 경우는 필요없으므로 노드의 k를 딕셔너리로 저장해서
k보다 크게 들어오는 경우는 skip

```py
class Solution:
    def findCheapestPrice(self, n: int, flights: List[List[int]], src: int, dst: int, K: int) -> int:
        graph = defaultdict(list)
        for flight in flights:
            f, t, p = flight
            graph[f].append((p, t))
        queue = [(0, 0, src)]
        visited = {}
        while queue:
            price, k, node = heappop(queue)
            if node == dst:
                return price
            if k == K + 1:
                continue
            if node not in visited or visited[node] > k:
                visited[node] = k
                for next_price, next_node in graph[node]:
                    cost = price + next_price
                    heappush(queue, (cost, k + 1, next_node))
        return -1
```
