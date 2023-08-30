# Is it critical to declare a list in for-loop?

Basically, it is not since `range(n)` creates a list as declaring a list inside for-loop also creates a list. 

However, it could be critical when it comes to:
- how many times you use elements within a list 
- how large each element is. If each element's size is large 

It is better off refering to lists outside for-loop. By doing so, you don't create lists repeatedly. 

## Example

- A list inside for-loop:

```python
x, y = 0, 0
for i in [(1, 0), (-1, 0)]:
    nx, ny = x + i[0], y + i[1] 
```

- lists outside for-loop:

```python
dx = [1, -1]
dy = [0, 0]
x, y = 0, 0
for i in range(2): # [0, 1]
    nx, ny = x + dx[i], y + dy[i] 
```

## How it works

- I can still refer to the reference of `lst`:

```python
lst = [1, 2]
for i in lst:
    print(i)
    lst.append(3)

'''
output:
1
2
3
3
3
3
...
'''
```

- I cannot refer to `[num, num + 1]` anymore:

```python
num = 0
for i in [num, num + 1]:
    print(i)
    num += 1

print('num is: ", num)

'''
output:
0
1
num is: 2
'''
```

