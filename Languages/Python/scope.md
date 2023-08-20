# Python Scope

```python
# a variable initialized within if statement
a = 9
if a == 9:
    x = "hoi"
print(x) # "hoi"

# a variable initialized within for statement
for _ in range(3):
    y = 4536
print(y) # 4536
```

## NameError: name 'x' is not defined

Note that the existence of the variable x is checked only at runtime.

```python
# a variable not initialized within if statement
a = 9
if a == 1234:
    x = "hoi"
print(x) # "hoi"
```

## Furthermore

- [What's the scope of a variable initialized in an if statement?](https://stackoverflow.com/questions/2829528/whats-the-scope-of-a-variable-initialized-in-an-if-statement)
- [Python Scopes and Namespaces](https://docs.python.org/3/tutorial/classes.html#python-scopes-and-namespaces)
