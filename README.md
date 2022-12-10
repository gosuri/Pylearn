# Python Tutorial

Python is a programming language that lets you work quickly and integrate systems more effectively. This tutorial is derived from the [Python Tutorial](https://docs.python.org/3/tutorial/index.html) and is intended to be a quick reference for the language.

## Invoking the interpreter

Calling `python3` on when installed using homebrew invokes the interpreter.

You can exit the interpreter with a zero status by hitting `Control-D` on Unix or executing `quit(`)`. 

### Passing arguments to the interpreter

You can access arguments passed to the interpreter using the `sys` module. The arguments are stored in the `sys.argv` list. The first argument is the name of the script, so the length of the list is at least one. Few important cases are as follows:

- When the script name is passed as `-` the script is read from standard input and `sys.argv[0]` is set to `'-'`. 
- When the script name is passed as `-c` the script is read from the next argument and `sys.argv[0]` is set to `'-'`. 
- When the script name is passed as `-m` the script is read from the next argument and `sys.argv[0]` is set to the name of the module.

```python
import sys
print(sys.argv)
```

### Source Code Encoding

The default encoding for Python source code is UTF-8. This means that you can use Unicode identifiers in your Python programs (yay emojis! 🙌). To declare another encoding, you can use a comment at the top of the file:

```python
# -*- coding: encoding -*-
```
One exception to the first line rule when declaring the encoding is when the first line is a shebang line. In this case, the encoding declaration must be on the second line. For example:

```python
#!/usr/bin/env python3
# -*- coding: cp1252 -*-
```


## Informal Introduction

### Basic Syntax

Some quick pointers:

* Input and output are distinguished by the presence or absence of prompts `>>>` and `...` respectively.
* Comments are indicated by `#` and extend to the end of the line.
* Indentation is used to group statements. The standard indentation is four spaces, although tabs and any other space size will work, as long as it is consistent.
* Statements are terminated by a newline character.
* Strings are enclosed in either single or double quotes. Triple quotes can be used to span multiple lines.

```python
# this is a comment
spam = 1 # and so is this
         # ... and this
text = "# This is not a comment because it's inside quotes."
``` 

### Numbers and Operators

Start the python interpreter and try out some calculations:

```python
>>> 2 + 2
4
>>> 50 - 5*6
20
>>> (50 - 5*6) / 4
5.0
>>> 8 / 5  # division always returns a floating point number
1.6
>>> 17 / 3  # classic division returns a float
5.666666666666667
>>> 17 // 3  # floor division discards the fractional part
5
>>> 17 % 3  # the % operator returns the remainder of the division
2
>>> 5 * 3 + 2  # result * divisor + remainder
17
>>> 5 ** 2  # 5 squared
25
>>> 2 ** 7  # 2 to the power of 7
128
>>> width = 20
>>> height = 5 * 9
>>> width * height
900
>>> n  # try to access an undefined variable
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'n' is not defined
>>> 4 * 3.75 - 1

```

* The integer numbers (e.g. 2, 4, 20) have type `int`, the ones with a fractional part (e.g. 5.0, 1.6) have type `float`. We will see more about numeric types later in the tutorial.
* Division (`/`) always returns a `float`. To do floor division and get an integer result (discarding any fractional result) you can use the `//` operator; to calculate the remainder you can use `%`.
* Use the `**` operator to calculate powers.
* The equal sign (`=`) is used to assign a value to a variable. Afterwards, no result is displayed before the next interactive prompt.
* If a variable is not "defined" (assigned a value), trying to use it will give you an error.
* There is full support for floating point; operators with mixed type operands convert the integer operand to floating point.

In interactive mode, the last printed expression is assigned to the variable `_`. This means that when you are using Python as a desk calculator, it is somewhat easier to continue calculations, for example:

```python
>>> tax = 12.5 / 100
>>> price = 100.50
>>> price * tax
12.5625
>>> price + _
113.0625
>>> round(_, 2)
113.06
```
Needless to say, `_` should be used only for calculating the result of the last expression. Don't try to use it for anything else or assign a value to it, as it is a special variable in Python.

In addtion to the `int` and `float` types, Python supports other types of numbers, such as `Decimal` and `Fraction`. Python also has built-in support for complex numbers, and uses the `j` or `J` suffix to indicate the imaginary part (e.g. `3+5j`).

