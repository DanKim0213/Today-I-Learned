# Sorting

## Features

- `list.sort()` modifies the list in-place whereas `sorted(list)` returns a new list. (`list.sort()` is slightly faster)
- Sorts are guaranteed to be stable. That means that when multiple records have the same key, their original order is preserved.
- Sorts are in ascending order. But, both list.sort() and sorted() accept a reverse parameter with a boolean value. For example, `sorted(students, key=attrgetter('age'), reverse=True)` 

## How to sort by multiple attributes?

```python
"""
1. sort by length of string
2. If the length of the string is same, sort by alphabetical order
"""

data = [ "ccc", "aaa",  "dd", "bb"]

# 1.
data.sort(key=lambda x: (len(x), x))

# 2. 
data.sort()
data.sort(key=lambda x: len(x))

print(data) # ['bb', 'dd', 'aaa', 'ccc']
```
