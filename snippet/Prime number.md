# 소수 판별(에라토스테네스의 체)

구하려는 수의 제곱근 까지 반복해서 앞의 소수들의 배수들을 삭제해가는 방법
2부터 n까지의 소수 확인을 위한 arr를 반환

```py
def get_prime_number(n):
    ck = [False] * 2 + [True for i in range(n - 1)]
    for i in range(2, int((n + 1) ** 0.5) + 1):
        if ck[i] == True:
            for j in range(i * i, n + 1, i):
                ck[j] = False
    return ck
```