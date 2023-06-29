# Algorithms 

Table of Content

- Recurion Error
- input

## Recursion Error

[BOJ Help](https://help.acmicpc.net/judge/rte/RecursionError)

> sys.setrecursionlimit()을 사용하는 것입니다. 이 함수를 사용하면, Python이 정한 최대 재귀 갚이를 변경할 수 있습니다. 소스 1의 최대 재귀 깊이를 1,000,000 정도로 크게 설정하면 런타임 에러 없이 실행이 됩니다.

```python
import sys
sys.setrecursionlimit(10**6) 

def calc(n): 
    if n == 0: return 0 
    else: return n + calc(n-1) 

n = int(input()) 
print(calc(n))
```

## Input

Input을 읽는 속도가 느려서 때로는 시간 초과 에러가 날 수 있다. 이를 해결하고자 `stdin`을 쓰자  

```python
import sys
input = sys.stdin.readline
```

## TODO

Union-find, Binary-tree(Graph)
