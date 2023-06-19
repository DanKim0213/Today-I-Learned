# List Extend() function

> extend(iterable: Iterable[_T], /) -> None

Extend list by appending elements from the iterable.

## Example

The `extend()` method adds all the elements of an iterable(list, tuple, string, etc) to the end of the list.

```python
# create a list
prime_numbers = [2, 3, 5]

# create another list
numbers = [1, 4]

# add all elements of prime_numbers to numbers
numbers.extend(prime_numbers)


print('List after extend():', numbers)

# Output: List after extend(): [1, 4, 2, 3, 5]
```

## extend() vs append()

The function extend() is used to extend another list to the end of the list while append() is used to append an element.

## Other ways to extend a list

#### 1. the + operator

```python
a = [1, 2]
b = [3, 4]

a += b    # a = a + b


# Output: [1, 2, 3, 4]
print('a =', a)
```

#### 2. the list slicing syntax
```python
a = [1, 2]
b = [3, 4]

a[len(a):] = b


# Output: [1, 2, 3, 4]
print('a =', a)
```
