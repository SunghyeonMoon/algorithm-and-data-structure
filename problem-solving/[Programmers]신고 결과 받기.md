# [Programmers][신고 결과 받기](https://programmers.co.kr/learn/courses/30/lessons/92334)

## 풀이

문제 자체는 쉽지만 자료구조와 변수명 관리 등에서 깔끔하게 구현하기가 까다로웠던 문제였다.

```py
from collections import defaultdict

def solution(id_list, report, k):
    dic = defaultdict(list)
    counter = defaultdict(int)
    banned_user = set()
    # 중복 신고를 없애기위해 set(report) 사용
    for r in set(report):
        from_id, to_id = r.split()
        dic[from_id].append(to_id)
        counter[to_id] += 1
        if counter[to_id] >= k:
            banned_user.add(to_id)

    answer = []
    for user_id in id_list:
        temp = 0
        for report_to in dic[user_id]:
            if report_to in banned_user:
                temp += 1
        answer.append(temp)
    return answer
```
