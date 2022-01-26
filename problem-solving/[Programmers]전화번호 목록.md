# [프로그래머스] [전화번호 목록](https://programmers.co.kr/learn/courses/30/lessons/42577)

## 알고리즘 분류

해시, 문자열

## 1차 풀이(시간 초과)

이중 반복문과 startswith 함수를 이용해서 완전 탐색

```py
def solution(phoneBook):
    phoneBook.sort(key = lambda x: len(x))
    for i in range(len(phoneBook) - 1):
        for j in range(i + 1, len(phoneBook)):
            if phoneBook[j].startswith(phoneBook[i]):
                return False
    return True
```

## 2차 풀이

set의 in 연산이 O(1)인 점을 이용한 풀이

```py
def solution(phone_book):
    phone_book_set = set(phone_book)
    for phone_number in phone_book:
        # 가장 중요한 논리(전체(자기자신)을 제외하고 확인)
        for index in range(len(phone_number) - 1):
            if phone_number[:index + 1] in phone_book_set :
                return False
    return True
```

## 다른 사람 풀이

문자열 순으로 정렬하면 앞 뒤로만 체크해도 startswith가 존재하는지 확인이 가능하다.

```py
def solution(phoneBook):
    phoneBook.sort()
    for p1, p2 in zip(phoneBook, phoneBook[1:]):
        if p2.startswith(p1):
            return False
    return True
```
