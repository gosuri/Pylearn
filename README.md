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


### Strings

Strings in python can be enclosed in single quotes or double quotes. Triple quotes can be used to span multiple lines.


```python
>>> 'spam eggs'  # single quotes
'spam eggs'
>>> 'doesn\'t'  # use \' to escape the single quote...
"doesn't"
>>> "doesn't"  # ...or use double quotes instead
"doesn't"
>>> '"Yes," they said.'
'"Yes," they said.'
>>> "\"Yes,\" they said."
'"Yes," they said.'
>>> '"Isn\'t," they said.'
'"Isn\'t," they said.'
>>> """ This is a multi-line string.
... This is the second line.
... """
```

In interactive mode, the prompt string, `>>>`, is considered part of the string, if it is the first line. This means that multi-line input must be indented:

```python
>>> print("""\
... Usage: thingy [OPTIONS]
...      -h                        Display this usage message
...      -H hostname               Hostname to connect to
... """)
Usage: thingy [OPTIONS]
     -h                        Display this usage message
     -H hostname               Hostname to connect to
```

Strings can be concatenated (glued together) with the `+` operator, and repeated with `*`:

```python
>>> 3 * 'un' + 'ium'
'unununium'
```
String concatenation only works with two literals, not with variables or expressions:

```python
>>> prefix = 'Py'
>>> prefix 'thon'  # can't concatenate a variable and a string literal
  File "<stdin>", line 1
    prefix 'thon'
                ^
SyntaxError: invalid syntax
>>> ('un' * 3) 'ium'
  File "<stdin>", line 1
    ('un' * 3) 'ium'
                   ^
SyntaxError: invalid syntax
```

To concatenate variables or a variable and a literal, use `+`:

```python
>>> prefix + 'thon'
'Python'
```
Strings can be indexed, with the first character having index 0. There is no separate character type; a character is simply a string of size one:

```python
>>> word = 'Python'
>>> word[0]  # character in position 0
'P'
>>> word[5]  # character in position 5
'n'
```
Indices may also be negative numbers, to start counting from the right:

```python
>>> word[-1]  # last character
'n'
>>> word[-2]  # second-last character
'o'
>>> word[-6]
'P'
```
In addition to indexing, slicing is also supported. While indexing is used to obtain individual characters, slicing allows you to obtain substring:

```python
>>> word[0:2]  # characters from position 0 (included) to 2 (excluded)
'Py'
>>> word[2:5]  # characters from position 2 (included) to 5 (excluded)
'tho'
```
Note how the start is always included, and the end always excluded. This makes sure that `s[:i] + s[i:]` is always equal to `s`:

```python  
>>> word[:2] + word[2:]
'Python'
>>> word[:4] + word[4:]
'Python'
```
Slice indices have useful defaults; an omitted first index defaults to zero, an omitted second index defaults to the size of the string being sliced.

```python
>>> word[:2]   # character from the beginning to position 2 (excluded)
'Py'
>>> word[4:]   # characters from position 4 (included) to the end
'on'
>>> word[-2:]  # characters from the second-last (included) to the end
'on'
```
Attempting to use an index that is too large will result in an error:

```python
>>> word[42]  # the word only has 6 characters
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: string index out of range

```
However, out of range slice indexes are handled gracefully when used for slicing:

```python
>>> word[4:42]
'on'
>>> word[42:]
''
```
Python strings cannot be changed — they are immutable. Therefore, assigning to an indexed position in the string results in an error:

```python
>>> word[0] = 'J'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
>>> word[2:] = 'py'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
```
If you need a different string, you should create a new one:

```python
>>> 'J' + word[1:]
'Jython'
>>> word[:2] + 'py'
'Pypy'
```
The built-in function `len()` returns the length of a string:

```python
>>> s = 'supercalifragilisticexpialidocious'
>>> len(s)
34
```