# [Programmers] [괄호 변환](https://programmers.co.kr/learn/courses/30/lessons/60058)

## 구현

```py
def solution(p):

    def split_string(string):
        left = right = 0
        for idx, s in enumerate(string):
            if s == '(': left += 1
            else: right += 1
            if left == right:
                return [string[:idx + 1], string[idx + 1:]]

    def is_correct(string):
        stack = 0
        for s in string:
            if s == '(':
                stack += 1
                continue
            if not stack:
                return False
            stack -= 1
        if stack:
            return False
        return True

    def reverse_string(string):
        answer = ''
        for s in string[1:-1]:
            if s == '(':
                answer += ')'
            else:
                answer += '('
        return answer

    def convert_string(string):
        if not string:
            return ''
        u, v = split_string(string)
        if is_correct(u):
            return u + convert_string(v)
        else:
            return '(' + convert_string(v) + ')' + reverse_string(u)

    return convert_string(p)
```
