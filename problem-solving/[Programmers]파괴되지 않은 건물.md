# [프로그래머스] [파괴되지 않은 건물](https://programmers.co.kr/learn/courses/30/lessons/92344)

## 알고리즘 분류

2차원 배열, imos알고리즘

## 1차 풀이(시간 초과)

시뮬레이션으로 2차원 배열 값 하나씩 수정하였더니, 시간 초과가 나왔다.

```py
def solution(board, skill):
    answer = 0
    for s in skill:
        r1, c1, r2, c2, degree = s[1:]
        if s[0] == 1:
            degree *= -1
        for x in range(r1, r2 + 1):
            for y in range(c1, c2 + 1):
                board[x][y] += degree
        
    for x in range(len(board)):
        for y in range(len(board[0])):
            if board[x][y] > 0:
                answer += 1

    return answer
```

## 2차 풀이

검색을 통해 imos 알고리즘을 사용하여 재풀이

```py
def solution(board, skill):
    answer = 0
    imos = [[0 for _ in range(len(board[0]) + 1)] for _ in range(len(board) + 1)] 
    
    for s in skill:
        cmd, r1, c1, r2, c2, degree = s
        if cmd == 1:
            degree = -degree
        imos[r1][c1] += degree
        imos[r2 + 1][c2 + 1] += degree
        imos[r1][c2 + 1] -= degree
        imos[r2 + 1][c1] -= degree
        
    for x in range(0, len(imos)):
        now = 0
        for y in range(0, len(imos[0])):
            now += imos[x][y]
            imos[x][y] = now
            
    for y in range(0, len(imos[0])):
        now = 0
        for x in range(0, len(imos)):
            now += imos[x][y]
            imos[x][y] = now
            
    for x in range(len(board)):
        for y in range(len(board[0])):
            if board[x][y] + imos[x][y] > 0:
                answer += 1
                
    return answer
```
