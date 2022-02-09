# 다익스트라

```py
import heapq
def dijkstra(graph, start):
    distance = [float("inf")] * (V + 1)
    distance[start] = 0
    queue = [(0, start)]
    while queue:
        cost, node = heappop(queue)
        if distance[node] < cost:
            continue
        for next_cost, next_node in graph[node]:
            next_cost += cost
            if distance[next_node] > next_cost:
                distance[next_node] = next_cost
                heappush(queue, (next_cost, next_node))
```
