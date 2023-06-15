# Python Variable Scope

A variable scope specifies the region where we can access a variable. Based on the scope, variables in Python could be one of these types: global, local, or nonlocal variable.

- Global variable: a variable declared in a global scope
- Local variable: a variable declared **within** the current function
- Nonlocal variable: a variable declared **outside** the current function

To explain the variable scopes, I comply with an order.
1. Declare a variable
2. Call an inner function
3. Print the current variable I declared at the first step

Let's give a quick glance at the following code:
```python
def outer_func():
    def inner_func():
        message = "local2 :)"
        print("call from inner function: ", message)

    message = "local1 :)"
    inner_func()
    print("call from outer function: ", message)


message = "global :)"
outer_func()
print("call from global: ", message)

# Output:
# call from inner function:  local2 :)
# call from outer function:  local1 :)
# call from global:  global :) 
```
 
## Read Global, Local, or Nonlocal variable

We can read variables of the three types by complying with the default order in Python. However, sometimes we need to directly read variables using global or nonlocal keyword.  

### Call the global variable 
```python
def outer_func():
    def inner_func():
        # message = "local2 :)"
        print("call from inner function: ", message)

    # message = "local1 :)"
    inner_func()
    print("call from outer function: ", message)


message = "global :)"
outer_func()
print("call from global: ", message)

# Output:
# call from inner function:  global :)
# call from outer function:  global :)
# call from global:  global :) 
```

### Call the global variable with local1 variable
```python
def outer_func():
    def inner_func():
        global message
        # message = "local2 :)"
        print("call from inner function: ", message)

    message = "local1 :)"
    inner_func()
    print("call from outer function: ", message)


message = "global :)"
outer_func()
print("call from global: ", message)

# Output:
# call from inner function:  **global :)**
# call from outer function:  local1 :)
# call from global:  global :) 
```

### Call the local1 within the inner function 
```python
def outer_func():
    def inner_func():
        nonlocal message
        # message = "local2 :)"
        print("call from inner function: ", message)

    message = "local1 :)"
    inner_func()
    print("call from outer function: ", message)


message = "global :)"
outer_func()
print("call from global: ", message)

# Output:
# call from inner function:  **local1 :)**
# call from outer function:  local1 :)
# call from global:  global :) 
```

### SyntaxError: no binding for nonlocal 'message' found
```python
def outer_func():
    nonlocal message # use global instead 
    message = "local1 :)"
    print("call from outer function: ", message)


message = "global :)"
outer_func()
print("call from global: ", message)
```

## Update global or nonlocal variable

We've seen the usage of global and local keywords to read variables. What if we'd like to update the variables?

### global keyword
```python
def outer_func():
    global message
    message = "local1 :)"
    print("call from outer function: ", message)


message = "global :)"
outer_func()
print("call from global: ", message)

# Output:
# call from outer function:  local1 :)
# call from global:  local1 :) 
```

### nonlocal keyword
```python
def outer_func():
    def inner_func():
        nonlocal message
        message = "local2 :)"
        print("call from inner function: ", message)

    message = "local1 :)"
    inner_func()
    print("call from outer function: ", message)


message = "global :)"
outer_func()
print("call from global: ", message)

# Output:
# call from inner function:  local2 :)
# call from outer function:  local2 :)
# call from global:  global :) 
```

### UnboundLocalError: local variable 'message' referenced before assignment
```python
def outer_func():
    # To resolve, **global message** required
    message = message + "local1 :)" 
    inner_func()
    print("call from outer function: ", message)


message = "global :)"
outer_func()
print("call from global: ", message)
```

## Thoughts

[Variable Shadowing](https://en.wikipedia.org/wiki/Variable_shadowing) is not a good practice for coding like we did above. However, we sometimes need to use global or nonlocal keyword to update variables we already declared. 

I think the rule of thumb could be put '_' before the variable name, such as '_message', for global variables. By doing so, I could figure out whether to use a global or local variable.

(Also, declaring variables as capitalized for final static variables is a good practice, too. For example, 'N', 'K', 'NUM_OF_PEOPLE')

## References
- [Python Variable Scope](https://www.programiz.com/python-programming/global-local-nonlocal-variables)
- [Python Global Keyword](https://www.programiz.com/python-programming/global-keyword)

