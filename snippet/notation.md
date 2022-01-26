# Notation(진법)

number = 변환하려는 수, notation = 진법

## 10진수 > n진수

```py
def convert_notation(number, notation):
    result = ""
    numbers = "0123456789ABCDEF"
    while number:
        number, mod = divmod(number, notation)
        result += numbers[mod]
    return result[::-1]
```

## n진수 > 10진수

```py
int(number, notation)
```
