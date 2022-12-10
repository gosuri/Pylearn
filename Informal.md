## Informal Introduction to Python

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
### Indentation

Python uses indentation for blocks, instead of curly braces. Both tabs and spaces are supported, but the standard indentation requires standard Python code to use four spaces. For example:

```python
if True:
    print("True")
else:
    print("False")
```

### Numbers

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

In addition to the `int` and `float` types, Python supports other types of numbers, such as `Decimal` and `Fraction`. Python also has built-in support for complex numbers, and uses the `j` or `J` suffix to indicate the imaginary part (e.g. `3+5j`).


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

### Lists

Lists are the most versatile of Python's compound data types. A list contains items separated by commas and enclosed within square brackets (`[]`). To some extent, lists are similar to arrays in C. One difference between them is that all the items belonging to a list can be of different data type, but usually the items all have the same type.

The values stored in a list can be accessed using the slice operator (`[]` and `[:]`) with indexes starting at 0 in the beginning of the list and working their way to end -1. The plus (`+`) sign is the list concatenation operator, and the asterisk (`*`) is the repetition operator.

The following example will help to clarify these concepts:

```python
>>> # List slicing
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits[0]  # indexing returns the item
'orange'
>>> fruits[0:3]  # slicing returns a new list
['orange', 'apple', 'pear']
>>> fruits[3:]  # slicing returns a new list
['banana', 'kiwi', 'apple', 'banana']
>>> fruits[:3]  # slicing returns a new list
['orange', 'apple', 'pear']
>>> fruits[-3:]  # slicing returns a new list
['kiwi', 'apple', 'banana']
>>> fruits[:]  # slicing returns a new list
['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits[::2]  # slicing returns a new list
['orange', 'pear', 'kiwi', 'banana']
>>> fruits[::-1]  # slicing returns a new list
['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange']
>>> fruits[::-2]  # slicing returns a new list
['banana', 'kiwi', 'pear', 'orange']
>>> fruits[3:-1]  # slicing returns a new list
['banana', 'kiwi', 'apple']
>>> fruits[3:-2]  # slicing returns a new list
['banana', 'kiwi']
>>> fruits[3:-3]  # slicing returns a new list
['banana']
```
Lists also support operations like concatenation:

```python
>>> fruits + ['grape', 'mango']
['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana', 'grape', 'mango']
```
... and repetition:

```python
>>> fruits * 2
['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana', 'orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
```
... and membership testing:

```python
>>> 'orange' in fruits
True
>>> 'grape' in fruits
False
```
... and iteration:

```python
>>> for fruit in fruits:
...     print(fruit)
...
orange
apple
pear
banana
kiwi
apple
banana
```
Lists can be nested:

```python
>>> a = ['a', 'b', 'c']
>>> n = [1, 2, 3]
>>> x = [a, n]
>>> x
[['a', 'b', 'c'], [1, 2, 3]]
>>> x[0]
['a', 'b', 'c']
>>> x[0][1]
'b'
```
Lists are a mutable type, i.e. it is possible to change their content:

```python
>>> fruits[0] = 'grape'
>>> fruits
['grape', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
```
The built-in function `len()` also applies to lists:

```python
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> len(fruits)
7
```
It is possible to append new items to the end of the list, by using the `append()` method (we will see more about methods later):

```python
>>> fruits.append('grape')
>>> fruits
['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana', 'grape']
```
Assignment to slices is also possible, and this can even change the size of the list or clear it entirely:

```python

>>> # Replace some items:
>>> fruits[0:2] = ['grape', 'apple']
>>> fruits
['grape', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana', 'grape']
>>> # Remove some:
>>> fruits[0:2] = []
>>> fruits
['pear', 'banana', 'kiwi', 'apple', 'banana', 'grape']
>>> # Clear the list by replacing all the elements with an empty list:
>>> fruits[:] = []
>>> fruits
[]
```
The `del` statement can also be used to remove items from a list:

```python
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> del fruits[0]
>>> fruits
['apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
```
It is possible to remove multiple items from a list using the `del` statement:

```python
>>> del fruits[0:2]
>>> fruits
['banana', 'kiwi', 'apple', 'banana']
```
The `del` statement can also be used to remove an entire list:

```python
>>> del fruits
>>> fruits
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'fruits' is not defined
```
The `remove()` method removes the first matching value, not a specific index:

```python
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits.remove('apple')
>>> fruits
['orange', 'pear', 'banana', 'kiwi', 'apple', 'banana']
```
The `pop()` method removes the item at the given index and returns it. If no index is specified, `pop()` removes and returns the last item in the list.

```python
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits.pop()
'banana'
>>> fruits
['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple']
>>> fruits.pop(0)
'orange'
>>> fruits
['apple', 'pear', 'banana', 'kiwi', 'apple']
```
The `insert()` method inserts an item at a given position. The first argument is the index of the element before which to insert, so `a.insert(0, x)` inserts at the front of the list, and `a.insert(len(a), x)` is equivalent to `a.append(x)`.

```python
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits.insert(0, 'grape')
>>> fruits
['grape', 'orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
```
The `clear()` method removes all items from the list. Equivalent to `del a[:]`.

```python
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits.clear()
>>> fruits
[]
```
The `index()` method returns the index of the first item whose value is equal to the argument. It raises a `ValueError` if there is no such item.

```python
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits.index('banana')
3
>>> fruits.index('banana', 4)  # Find next banana starting a position 4
6
>>> fruits.index('grape')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: 'grape' is not in list
```
The `count()` method returns the number of times the argument appears in the list.

```python
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits.count('apple')
2
>>> fruits.count('grape')
0
```
The `sort()` method sorts the items of the list in place (the arguments can be used for sort customization, see `sorted()` for their explanation).

```python
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits.sort()
>>> fruits
['apple', 'apple', 'banana', 'banana', 'kiwi', 'orange', 'pear']
```

The `reverse()` method reverses the elements of the list in place.

```python
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits.reverse()
>>> fruits
['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange']
```
The `copy()` method returns a shallow copy of the list. Equivalent to `a[:]`.

```python
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits_copy = fruits.copy()
>>> fruits_copy
['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
```
The `list()` constructor builds lists from iterables:

```python
>>> list('cat')
['c', 'a', 't']
```