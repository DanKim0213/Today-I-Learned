# Logical Operators

## Use `()` to set priority.

```python
print(False or True and False) # False
print(True or False and False) # True
```

- `False or True and False` works like (`False` -> `or`) and then look (`True` -> `and`) since it is `False`. Finally, (`True` -> `and`) followed by `False`. Thus, `False`.
- However, `True or False and False` works like (`True` -> `or`) and returns `True` right away since it is `True` regardless of what follows behind.
- In order to avoid confusion, `(True or False) and False` gives you what you intend :)

## Where it comes from

I tried to solve SWEA 1767

```python
    grid = []
    positions = []
    edges = 0  # to check the grid is surrounded by cores
    for i in range(N):
        row = list(map(int, input().split()))
        grid.append(row)
        for j in range(N):
            if (i == 0 or i == N - 1 or j == 0 or j == N - 1) and row[j] == 1:
                edges += 1
            if 0 < i < N - 1 and 0 < j < N - 1 and row[j] == 1:
                positions.append((i, j))
```

The upper code could be better:
```python
    grid = []
    positions = []
    edges = 0  # to check the grid is surrounded by cores
    for i in range(N):
        row = list(map(int, input().split()))
        grid.append(row)
        for j in range(N):
            if row[j] != 1:
                continue
            elif 0 < i < N - 1 and 0 < j < N - 1:
                positions.append((i, j))
            else:
                edges += 1
```
