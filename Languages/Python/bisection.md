# Bisect algorithm

a.k.a. Binary Search

It means ***divide into two usually equal parts***.

- `bisect_left`: find\_ge -> thus, a[i-1] could be lt
- `bisect_right`: find\_gt -> thus, a[i-1] could be le


## Example

According to [Python docs](https://docs.python.org/3/library/bisect.html):

```python
from bisect import bisect_left, bisect_right

students = [10, 20]

# find an exact value
print(bisect_left(students, 10))  # 0
print(bisect_right(students, 10))  # 1

# find an approximate value
print(bisect_left(students, 15))  # 1
print(bisect_right(students, 15))  # 1


def index(a, x):
    'Locate the leftmost value exactly equal to x'
    i = bisect_left(a, x)
    if i != len(a) and a[i] == x:
        return i
    raise ValueError

def find_lt(a, x):
    'Find rightmost value less than x'
    i = bisect_left(a, x)
    if i:  # i > 0 cuz of less
        return a[i-1]
    raise ValueError

def find_le(a, x):
    'Find rightmost value less than or equal to x'
    i = bisect_right(a, x)
    if i:  # i > 0 cuz of less
        return a[i-1]
    raise ValueError

def find_gt(a, x):
    'Find leftmost value greater than x'
    i = bisect_right(a, x)
    if i != len(a):  # cuz of greater
        return a[i]
    raise ValueError

def find_ge(a, x):
    'Find leftmost item greater than or equal to x'
    i = bisect_left(a, x)
    if i != len(a):  # cuz of greater
        return a[i]
    raise ValueError

```


