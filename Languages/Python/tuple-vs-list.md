# Tuple vs List

TL;DR;

- Tuple is immutable whereas List is mutable.
- Tuple can be used as key in dictionary whereas Lists cannot.
- Tuple with only one element requires a trailing comma.

## Mutability

Tuple is immutable whereas List is mutable:

```python
lst = [1,2,3,4]
tpl = (1,2,3,4)

print(lst) # [1,2,3,4]
print(tpl) # (1,2,3,4)

lst[0] = 5
tpl[0] = 5 # TypeError: 'tuple' object does not support item assignment
```

## Tuple as Key

Tuple can also be used as key in dictionary due to their hashable and immutable nature whereas Lists cannot because list can’t handle `__hash__()` and have mutable nature.

Tuple Directory:

```python
dir(tpl)

'''
output:
['__add__',
'__class__',
'__contains__',
'__delattr__',
'__dir__',
'__doc__',
'__eq__',
'__format__',
'__ge__',
'__getattribute__',
'__getitem__',
'__getnewargs__',
'__gt__',
'__hash__',
'__init__',
'__init_subclass__',
'__iter__',
'__le__',
'__len__',
'__lt__',
'__mul__',
'__ne__',
'__new__',
'__reduce__',
'__reduce_ex__',
'__repr__',
'__rmul__',
'__setattr__',
'__sizeof__',
'__str__',
'__subclasshook__',
'count',
'index']
'''

```

## Tuple vs Grouping

A tuple with only one element still requires a trailing comma to be recognized as a tuple.

This is a syntactic requirement to differentiate between parentheses used for grouping and those used to define a tuple:

```python
# X: Mistake could be made
a = ((0))
b = ([0])
c = [(0)]
d = [[0]]
for val in [a, b, c, d]:
  print(val)
'''
output:
0
[0]
[0]
[[0]]
'''

# O: Tuple with one element
my_tuple = (1,)
print(type(my_tuple))  # Output: <class 'tuple'>

# Parentheses for grouping
my_other_tuple = (1)
print(type(my_other_tuple))  # Output: <class 'int'>


# Real Example from Baekjoon_15683
UP = (0, -1)
DOWN = (0, 1)
data = [(UP,), (UP, DOWN)]

for val in data:
    print(val)
# ((0, -1),)
# ((0, -1), (0, 1))
```
