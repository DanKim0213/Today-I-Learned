# Parameter and Argument

One of the basics in Python is Parameter and Arugment. What we are used to in defining a function is *positional-or-keyword*. However, *positional-only* and *keyword-only* is frequently used in docs, too.  

## Parameter

A named entity in a function (or method) definition that specifies an argument (or in some cases, arguments) that the function can accept. There are five kinds of parameter:

- positional-or-keyword: specifies an argument that can be passed either positionally or as a keyword argument. This is the default kind of parameter, for example foo and bar in the following:

> def func(foo, bar=None): ...

- positional-only: specifies an argument that can be supplied only by position. Positional-only parameters can be defined by including a / character in the parameter list of the function definition after them, for example posonly1 and posonly2 in the following:

> def func(posonly1, posonly2, /, positional\_or\_keyword): ...

- keyword-only: specifies an argument that can be supplied only by keyword. Keyword-only parameters can be defined by including a single var-positional parameter or bare * in the parameter list of the function definition before them, for example kw\_only1 and kw\_only2 in the following:  

> def func(arg, \*, kw\_only1, kw\_only2): ...

- var-positional: specifies that an arbitrary sequence of positional arguments can be provided (in addition to any positional arguments already accepted by other parameters). Such a parameter can be defined by prepending the parameter name with \*, for example args in the following:

> def func(\*args, \*\*kwargs): ...

- var-keyword: specifies that arbitrarily many keyword arguments can be provided (in addition to any keyword arguments already accepted by other parameters). Such a parameter can be defined by prepending the parameter name with \*\*, for example kwargs in the example above.

Parameters can specify both optional and required arguments, as well as default values for some optional arguments.

## Argument 

A value passed to a function (or method) when calling the function. There are two kinds of argument:

- keyword argument: an argument preceded by an identifier (e.g. name=) in a function call or passed as a value in a dictionary preceded by \*\*. For example, 3 and 5 are both keyword arguments in the following calls to complex():

> complex(real=3, imag=5) <br>
> complex(\*\*{'real': 3, 'imag': 5})

- positional argument: an argument that is not a keyword argument. Positional arguments can appear at the beginning of an argument list and/or be passed as elements of an iterable preceded by \*. For example, 3 and 5 are both positional arguments in the following calls:

> complex(3, 5) <br>
> complex(\*(3, 5))

Arguments are assigned to the named local variables in a function body. See the Calls section for the rules governing this assignment. Syntactically, any expression can be used to represent an argument; the evaluated value is assigned to the local variable.

## Furthermore

- [term-parameter](https://docs.python.org/3/glossary.html#term-parameter) 
- [term-argument](https://docs.python.org/3/glossary.html#term-argument)
- [Using Python Optional Arguments When Defining Functions](https://realpython.com/python-optional-arguments/)
