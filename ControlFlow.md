# Control Flow

Python's control flow is similar to other languages with some twists.

## `if`

`if` is the most basic control flow statement. It takes a boolean expression and executes the code block if the expression is `True`.

```python
if 1 == 1:
    print("1 is equal to 1")
# Output:
# 1 is equal to 1

x = int(input("Enter a number: "))
if x > 0:
    print("x is positive")
elif x < 0:
    print("x is negative")
else:
    print("x is zero")
```

## `while`

`while` is a loop that executes the code block while the expression is `True`.

```python
i = 0
while i < 10:
    print(i)
    i += 1
# Output:
# 0
# 1
...
# 9
```

## `for`

Python's for statements interates over a sequence (list, tuple, string, etc.) or other iterable object in the order that they appear in the sequence.

```python
words = ["hello", "world", "this", "is", "a", "list"]
for word in words:
    print(word)
# Output:
# hello
# world
# this
# is
# a
# list

# interate over a map

users = {"Alice": 21, "Bob": 22, "Charlie": 23}
for name, age in users.items():
    print(name, age)
# Output:
# Alice 21
# Bob 22
# Charlie 23
```

## `range`

`range` is a built-in function that returns a sequence of numbers, starting from 0 by default, and increments by 1 (by default), and stops before a specified number. 

It is possible to specify the start, stop, and step size. `range` does not store all the values in memory, it would be inefficient. `range` is just an object that returns the next number in the sequence on demand.

```python
for i in range(5):
...   print(i)
0
1
2
3
4

for i in range(2, 5):
...   print(i)
2
3
4
```

Combining `range` with a `list` you can create a list of numbers.

```python
list(range(5))
[0, 1, 2, 3, 4]
```
To interate over the indices of a sequence, you can combine `range` and `len` as follows:

```python
a = ["Mary", "had", "a", "little", "lamb"]
for i in range(len(a)):
...   print(i, a[i])
0 Mary
1 had
2 a
3 little
4 lamb
```

It is however recommended to use the `enumerate` function instead.

`range` behaves like a list but it really isn't. It is an object that returns the next number in the sequence on demand. This makes it more memory efficient.

We say that `range` is an iterable object. An iterable object is an object that can return its members one at a time. We can iterate over an iterable object using a `for` loop.

```python
>>> sum(range(4))  # sum of 0 + 1 + 2 + 3
6
```

## `break` and `continue`

`break` and `continue` are used to control the flow of a loop. `break` exits the loop and `continue` skips the current iteration.

```python
for n in range(2, 10):
    for x in range(2, n):
        if n % x == 0:
            print(n, 'equals', x, '*', n//x)
            break
    else:
        # loop fell through without finding a factor
        print(n, 'is a prime number')

# Output:
# 2 is a prime number
# 3 is a prime number
# 4 equals 2 * 2
# 5 is a prime number
# 6 equals 2 * 3
# 7 is a prime number
# 8 equals 2 * 4
# 9 equals 3 * 3
```

## `pass`

`pass` is a null statement. It does nothing. It is used as a placeholder when a statement is required syntactically but the program requires no action.

```python
while True:
    pass  # Busy-wait for keyboard interrupt (Ctrl+C)
```

This is commonly used for creating minimal classes:

```python
class MyEmptyClass:
    pass
```

## `match`

`match` is a new control flow statement in Python 3.10. It is similar to `switch` in other languages.

```python
match x:
    case 0:
        print("x is zero")
    case 1:
        print("x is one")
    case 2:
        print("x is two")
    case _:
        print("x is something else")
```

Note the last case. It is a wildcard case. It matches any value. It is similar to the `default` case in `switch`.

You can also match multiple values in a single case.

```python
match x:
    case 0, 1:
        print("x is zero or one")
    case 2:
        print("x is two")
    case _:
        print("x is something else")
```

You can combine several literals in a single cas using `|`.

```python
match x:
    case 0 | 1:
        print("x is zero or one")
    case 2:
        print("x is two")
    case _:
        print("x is something else")
```

You can combine `if` and `match` to create a more powerful control flow statement.

```python
match x:
    case 0:
        print("x is zero")
    case 1:
        print("x is one")
    case 2:
        print("x is two")
    case _ if x > 2:
        print("x is greater than two")
    case _:
        print("x is something else")
```

You can use patterns to match more complex values. Patterns are a new feature in Python 3.10. Patterns can look like regular expressions and can be used to bind values to variables. For example, the following pattern matches a list of two elements and binds the first element to `x` and the second element to `y`.

```python
match [1, 2]:
    case [x, y]:
        print(x, y)
# Output:
# 1 2
```

Another example:

```python
# point is a tuple of two numbers (x, y)
match point:
    case (0, 0):
        print("The point is at the origin")
    case (0, y):
        print(f"The point is on the y-axis at y={y}")
    case (x, 0):
        print(f"The point is on the x-axis at x={x}")
    case (x, y):
        print(f"The point is at ({x}, {y})")
    case _:
        print("I don't know where the point is")
```

Unpacking the above example:

1. `case (0, 0):` matches a tuple of two elements where the first element is `0` and the second element is `0`.
2. `case (0, y):` matches a tuple of two elements where the first element is `0` and the second element is bound to the variable `y`.
3. `case (x, 0):` matches a tuple of two elements where the first element is bound to the variable `x` and the second element is `0`.
4. `case (x, y):` matches a tuple of two elements where the first element is bound to the variable `x` and the second element is bound to the variable `y`.
5. `case _:` matches any value.

You can use `match` to match classes.

```python
class Point:
    x: int
    y: int

def where_is(point):
    match point:
        case Point(0, 0):
            print("The point is at the origin")
        case Point(0, y):
            print(f"The point is on the y-axis at y={y}")
        case Point(x, 0):
            print(f"The point is on the x-axis at x={x}")
        case Point(x, y):
            print(f"The point is at ({x}, {y})")
        case _:
            print("I don't know where the point is")
```

Patterns can be arbitrarily complex. For example, the following pattern matches a list of two elements where the first element is a list of two elements and the second element is a list of two elements.

```python
match [[1, 2], [3, 4]]:
    case [[x, y], [z, w]]:
        print(x, y, z, w)
# Output:
# 1 2 3 4
```
Patterns may use named constants. These must be dotted names to prevent them from being interpreted as variables.

```python
from enum import Enum
class Color(Enum):
    RED = `red
    GREEN = `green`
    BLUE = `blue`

color = Color(input("Enter a color (red, blue or green): "))

match color:
    case Color.RED:
        print("You chose red")
    case Color.GREEN:
        print("You chose green")
    case Color.BLUE:
        print("You chose blue")
    case _:
        print("I don't know what color that is")
```

## Functions

Below functions writes the fibonacci series up to `n`.

```python
>>> def fib(n):    # write Fibonacci series up to n
        """Print a Fibonacci series up to n."""
        a, b = 0, 1
        while a < n:
            print(a, end=' ')
            a, b = b, a+b
        print()
>>> fib(2000)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597
```

The keyword `def` introduces a function definition. It must be followed by the function name and the parenthesized list of formal parameters. The statements that form the body of the function start at the next line, and must be indented.

The first statement of the function body can optionally be a string literal; this string literal is the function’s documentation string, or docstring. There are tools which use docstrings to automatically produce online or printed documentation, or to let the user interactively browse through code; it’s good practice to include docstrings in code that you write, so make a habit of it.

The execution of a function introduces a new symbol table used for the local variables of the function. More precisely, all variable assignments in a function store the value in the local symbol table; whereas variable references first look in the local symbol table, then in the local symbol tables of enclosing functions, then in the global symbol table, and finally in the table of built-in names. Thus, global variables and variables of enclosing functions cannot be directly assigned a value within a function (unless, for global variables, named in a global statement, or, for variables of enclosing functions, named in a nonlocal statement), although they may be referenced.


The arguments to a function call are passed using call by value (where the value is always an object reference, not the value of the object). When an argument is passed to a function, a new local variable is created in the function’s local symbol table. This new variable is bound to the object referenced by the corresponding function argument. The object referenced by a parameter is never changed by a function. For instance, when the following function is called with a list argument, the function changes the value of `arg1`, but not the value of the list object referred to by `mylist`:

```python
>>> def f(arg1, arg2):
        arg1 = 99
        arg2[0] = 'spam'

>>> mylist = [1, 2]
>>> f(mylist[:], mylist)
>>> mylist
[1, 2]
```

When a function calls another function, a new local symbol table is created for that call.

There are four rules to tell whether a variable is local or global:

1. If a variable is being used in the global scope (that is, outside of all functions), then it is always a global variable.
2. If there is a global statement for that variable in a function, it is a global variable.
3. Otherwise, if the variable is used in an assignment statement in the function, it is a local variable.
4. But if the variable is not used in an assignment statement, it is a global variable.

If a variable is referenced in a function but not assigned a value, it is a global variable. If a variable is assigned a value anywhere within the function’s body, it’s assumed to be a local variable.

```python
>>> def f():
        global s
        print(s)
        s = "I love London!"
        print(s)
        
>>> s = "I love Paris!"
>>> f()
I love Paris!
I love London!
>>> s
'I love London!'
```

### Default Argument Values

The default value is evaluated at the point of function definition. This is important to understand when the default is a mutable object such as a list, dictionary, or instances of most classes. For example, the following function accumulates the arguments passed to it on subsequent calls:

```python
>>> def f(a, L=[]):
        L.append(a)
        return L
    
>>> print(f(1))
[1]
>>> print(f(2))
[1, 2]
>>> print(f(3))
[1, 2, 3]

If you dont want default values to be shared between subsequent calls, you can write the function like this instead:

```python
>>> def f(a, L=None):
        if L is None:
            L = []
        L.append(a)
        return L
```

### Keyword Arguments

Functions can also be called using keyword arguments of the form `kwarg=value`. For instance, the following function:

```python
>>> def parrot(voltage, state='a stiff', action='voom', type='Norwegian Blue'):
        print("-- This parrot wouldn't", action, end=' ')
        print("if you put", voltage, "volts through it.")
        print("-- Lovely plumage, the", type)
        print("-- It's", state, "!")
```

accepts one required argument (voltage) and three optional arguments (state, action, and type). This function can be called in any of the following ways:

```python
>>> parrot(1000)                                          # 1 positional argument
-- This parrot wouldn't voom if you put 1000 volts through it.
-- Lovely plumage, the Norwegian Blue
-- It's a stiff !

>>> parrot(voltage=1000)                                  # 1 keyword argument
-- This parrot wouldn't voom if you put 1000 volts through it.
-- Lovely plumage, the Norwegian Blue
-- It's a stiff !

>>> parrot(voltage=1000000, action='VOOOOOM')             # 2 keyword arguments
-- This parrot wouldn't VOOOOOM if you put 1000000 volts through it.
-- Lovely plumage, the Norwegian Blue
-- It's a stiff !

>>> parrot(action='VOOOOOM', voltage=1000000)             # 2 keyword arguments
-- This parrot wouldn't VOOOOOM if you put 1000000 volts through it.
-- Lovely plumage, the Norwegian Blue
-- It's a stiff !

>>> parrot('a million', 'bereft of life', 'jump')         # 3 positional arguments
-- This parrot wouldn't jump if you put a million volts through it.
-- Lovely plumage, the Norwegian Blue
-- It's bereft of life !

>>> parrot('a thousand', state='pushing up the daisies')  # 1 positional, 1 keyword
-- This parrot wouldn't voom if you put a thousand volts through it.
-- Lovely plumage, the Norwegian Blue
-- It's pushing up the daisies !
```

In a function call, keyword arguments must follow positional arguments. All the keyword arguments passed must match one of the arguments accepted by the function. This includes arguments with default values. No argument may receive a value more than once. Here’s an example that fails due to this restriction:

```python
>>> parrot(voltage=5.0, 'dead')  # non-keyword argument after a keyword argument
  File "<stdin>", line 1, in <module>
TypeError: parrot() got multiple values for argument 'voltage'

>>> parrot(110, voltage=220)  # duplicate value for the same argument
  File "<stdin>", line 1, in <module>
TypeError: parrot() got multiple values for argument 'voltage'

>>> parrot(actor='John Cleese')  # unknown keyword argument
  File "<stdin>", line 1, in <module>
TypeError: parrot() got an unexpected keyword argument 'actor'
```

### Arbitrary Argument Lists

Sometimes you may want to make a function that takes a variable number of arguments. These arguments will be wrapped up in a tuple. For example, the built-in function `range()` can be called with 1, 2, or 3 arguments:

```python
>>> range(3)
range(0, 3)
>>> range(2, 5)
range(2, 5)
>>> range(3, 10, 2)
range(3, 10, 2)
```

In the first form, the given end point is excluded (just like the slice notation). The built-in function `len()` also accepts a variable number of arguments:

```python
>>> len(range(10))
10
```

If you want to write a function that takes a variable number of arguments, you can define it like this:

```python
>>> def write_multiple_items(file, separator, *args):
        file.write(separator.join(args))
```

The special syntax `*args` in the function definition is used to denote this kind of argument. The word `args` is a convention, you could also use `*whatever`. The `*` must be placed before the formal parameter name to denote this kind of special syntax, otherwise the `*` would be processed like an arithmetic multiplication operator.

The `write_multiple_items()` function can be called with any number of arguments. For example:

```python
>>> write_multiple_items(sys.stdout, ' ', 'spam', 'eggs', 'ham')
spam eggs ham
```

The `*args` parameter in the function definition is bound to a tuple containing the arguments beyond the formal parameter list. Within the function, the arguments are referred to as the contents of the tuple `args`. So, in the example, `args` would have the value `('spam', 'eggs', 'ham')`. (It is just a shorthand that you can use instead of having to manually create a tuple containing the arguments.)

### Unpacking Argument Lists

The reverse situation occurs when the arguments are already in a list or tuple but need to be unpacked for a function call requiring separate positional arguments. For instance, the built-in `range()` function expects separate start and stop arguments. If they are not available separately, write the function call with the `*` operator to unpack the arguments out of a list or tuple:

```python
>>> args = [3, 6]
>>> range(*args)
range(3, 6)
```

### Lambda Expressions

Small anonymous functions can be created with the `lambda` keyword. This function returns the sum of its two arguments: `lambda a, b: a+b`. Lambda functions can be used wherever function objects are required. They are syntactically restricted to a single expression. Semantically, they are just syntactic sugar for a normal function definition. Like nested function definitions, lambda functions can reference variables from the containing scope:

```python
>>> def make_incrementor(n):
        return lambda x: x + n
>>> f = make_incrementor(42)
>>> f(0)
42
>>> f(1)
43
```

### Documentation Strings

Functions can have documentation strings, which can be accessed via the `__doc__` attribute. It is good practice to include documentation strings in code that you write, so make a habit of it.

```python
>>> def my_function():
        """Do nothing, but document it.
        No, really, it doesn't do anything.
        """
        pass
>>> print(my_function.__doc__)
Do nothing, but document it.
No, really, it doesn't do anything.
```

### Function Annotations

Function annotations are completely optional metadata information about the types used by user-defined functions (see PEP 3107). Annotations are stored in the `__annotations__` attribute of the function as a dictionary and have no effect on any other part of the function. Annotations are available at runtime via the `__annotations__` attribute of the function or method object and have no effect on any other part of the function. For example:

```python
>>> def f(ham: str, eggs: str = 'eggs') -> str:
        print("Annotations:", f.__annotations__)
        print("Arguments:", ham, eggs)
        return ham + ' and ' + eggs
>>> f('spam')
Annotations: {'ham': <class 'str'>, 'return': <class 'str'>, 'eggs': <class 'str'>}
Arguments: spam eggs
'spam and eggs'
```

### Intermezzo: Coding Style

The style recommendations in this section are intended to improve the readability of code and make it consistent across the wide spectrum of Python code. The most important point is to be consistent. Consistency with this style guide is important. Consistency within a project is more important. Consistency within one module or function is the most important.

### Whitespace in Expressions and Statements

Use 4 spaces per indentation level. For long expressions, you can add line breaks after binary operators. The preferred way of wrapping long lines is by using Python’s implied line continuation inside parentheses, brackets and braces. Long lines can be broken over multiple lines by wrapping expressions in parentheses. These should be used in preference to using a backslash for line continuation.

```python
>>> my_list = [
        1, 2, 3,
        4, 5, 6,
        ]
>>> result = some_function_that_takes_arguments(
        'a', 'b', 'c',
        'd', 'e', 'f',
        )
```

When using a hanging indent the following should be considered; there should be no arguments on the first line and further indentation should be used to clearly distinguish itself as a continuation line.

```python
>>> foo = long_function_name(var_one, var_two,
                             var_three, var_four)
```

### When to Use Trailing Commas

Trailing commas are helpful when a version control system is used, when a list, tuple, or argument parameters are expected to be extended over time. The pattern is to put each value (including the last) on a line by itself, always adding a trailing comma even after the last one:

```python
>>> my_list = [
        1, 2, 3,
        4, 5, 6,
        ]
```

### Comments

Comments that contradict the code are worse than no comments. Always make a priority of keeping the comments up-to-date when the code changes!

Comments should be complete sentences. The first word should be capitalized, unless it is an identifier that begins with a lower case letter (never alter the case of identifiers!).

Block comments generally consist of one or more paragraphs built out of complete sentences, with each sentence ending in a period.

Inline comments are rare and should be separated by at least two spaces from the statement. They should start with a # and a single space.

### Naming Conventions

#### Function Names

Function names should be lowercase, with words separated by underscores as necessary to improve readability.

```python
>>> def my_function():
        pass
```

#### Variable Names

Variable names follow the same convention as function names.

```python
>>> my_variable = 10
```

#### Class Names

Class names should normally use the CapWords convention.

```python
>>> class MyClass:
        pass
```

#### Module Names

Module names should have short, all-lowercase names. Underscores can be used in the module name if it improves readability.

```python
>>> import my_module
```

#### Constants

Constants are usually defined on a module level and written in all capital letters with underscores separating words. Examples include `MAX_OVERFLOW` and `TOTAL`.