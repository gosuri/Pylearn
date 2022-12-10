# Data Structures

## Lists as Stacks

Lists can be used as stacks, where the last element added is the first element retrieved (“last-in, first-out”).

To add an item to the top of the stack, use `append()`. To retrieve an item from the top of the stack, use the `pop()` method without an explicit index.

```python
stack = [3, 4, 5]
stack.append(6)
stack.append(7)
stack
# [3, 4, 5, 6, 7]
stack.pop()
# 7
stack
# [3, 4, 5, 6]
stack.pop()
# 6
stack.pop()
# 5
stack
# [3, 4]
```

## Lists as Queues

Lists can also be used as queues, where the first element added is the first element retrieved (“first-in, first-out”); however, lists are not efficient for this purpose.

To implement a queue, use `collections.deque` which was designed to have fast appends and pops from both ends. For example:

```python
from collections import deque
queue = deque(["Eric", "John", "Michael"])
queue.append("Terry")           # Terry arrives
queue.append("Graham")          # Graham arrives
queue.popleft()                 # The first to arrive now leaves
# 'Eric'
queue.popleft()                 # The second to arrive now leaves
# 'John'
queue                           # Remaining queue in order of arrival
# deque(['Michael', 'Terry', 'Graham'])
```

## List Comprehensions

List comprehensions provide a concise way to create lists. Common applications are to make new lists where each element is the result of some operations applied to each member of another sequence or iterable, or to create a subsequence of those elements that satisfy a certain condition.

For example, assume we want to create a list of squares, like:

```python
squares = []
for x in range(10):
    squares.append(x**2)

squares
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

The above example creates or overwrites a variable named `x` that still exists after the loop completes. We can calculate the list of squares without any side effects using:

```python
squares = list(map(lambda x: x**2, range(10)))
squares
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

or equivalently:

```python
squares = [x**2 for x in range(10)]
squares
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

A list comprehension consists of brackets containing an expression followed by a `for` clause, then zero or more `for` or `if` clauses. The result will be a new list resulting from evaluating the expression in the context of the `for` and `if` clauses which follow it. For example, this listcomp combines the elements of two lists if they are not equal:

```python
[(x, y) for x in [1,2,3] for y in [3,1,4] if x != y]
# [(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]
```

and it’s equivalent to:

```python
combs = []
for x in [1,2,3]:
    for y in [3,1,4]:
        if x != y:
            combs.append((x, y))
combs
# [(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]
```

List comprehensions can contain complex expressions and nested functions:

```python
from math import pi
[str(round(pi, i)) for i in range(1, 6)]
# ['3.1', '3.14', '3.142', '3.1416', '3.14159']
```

### Nested List Comprehensions

The initial expression in a list comprehension can be any arbitrary expression, including another list comprehension.

For example, this example combines the elements of two lists if they are not equal:

```python
matrix = [
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12],
]
[[row[i] for row in matrix] for i in range(4)]
# [[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```
The following example transposes rows and columns:

```python
transposed = []
for i in range(4):
    transposed.append([row[i] for row in matrix])
transposed
# [[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```

which, in turn, is the same as:

```python
transposed = []
for i in range(4):
    # the following 3 lines implement the nested listcomp
    transposed_row = []
    for row in matrix:
        transposed_row.append(row[i])
    transposed.append(transposed_row)
transposed
# [[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```

In the real world, you should prefer built-in functions to complex flow statements. The `zip()` function would do a great job for this use case.

```python
list(zip(*matrix))
# [(1, 5, 9), (2, 6, 10), (3, 7, 11), (4, 8, 12)]
```

## The `del` statement

You can remove an item from a list given its index instead of its value by using the `del` statement.

Del can also be used to remove slices from a list or clear the entire list (which we did earlier by assignment of an empty list to the slice).

```python
a = [-1, 1, 66.25, 333, 333, 1234.5]
del a[0]
a
# [1, 66.25, 333, 333, 1234.5]
del a[2:4]
a
# [1, 66.25, 1234.5]
del a[:]
a
# []
del a
a
# NameError: name 'a' is not defined
```

## Tuples and Sequences

A tuple consists of a number of values separated by commas. It is similar to a list except that the tuples cannot be changed unlike lists. 

Tuples are usually enclosed in parentheses. For example:

```python
t = 12345, 54321, 'hello!'
t[0]
# 12345
t
# (12345, 54321, 'hello!')
# Tuples may be nested:
u = t, (1, 2, 3, 4, 5)
u
# ((12345, 54321, 'hello!'), (1, 2, 3, 4, 5))
# Tuples are immutable:
t[0] = 88888
# TypeError: 'tuple' object does not support item assignment
# But they can contain mutable objects:
v = ([1, 2, 3], [3, 2, 1])
v
# ([1, 2, 3], [3, 2, 1])
```

Tuples are immutable, and usually contain a heterogeneous sequence of elements that are accessed via unpacking (see later in this section) or indexing (or even by attribute in the case of namedtuples). 

Lists are mutable, and their elements are usually homogeneous and are accessed by iterating over the list.

Creating tuples with one item is a bit tricky, there are two ways to do it. The first way is to use a comma after the item inside the parentheses. For example:

```python
t = (50,) # comma is necessary
t
# (50,)
```

The second way is to use the tuple function, but it is not as common. For example:

```python
t = tuple('lupins')
t
# ('l', 'u', 'p', 'i', 'n', 's')
```

The statement `t = 12345, 54321, 'hello!'` is an example of tuple packing: the values `12345`, `54321` and `'hello!'` are packed together in a tuple. The reverse operation is also possible:

```python
x, y, z = t
x
# 12345
y
# 54321
z
# 'hello!'
```

This is called sequence unpacking. It works with any object that happens to be a sequence on the right-hand side, and it works for any number of variables on the left-hand side. Sequence unpacking requires that there are as many variables on the left-hand side of the equals sign as there are elements in the sequence.

## Sets

A set is an unordered collection with no duplicate elements. Basic uses include membership testing and eliminating duplicate entries.

Set objects also support mathematical operations like union, intersection, difference, and symmetric difference.

Curly braces or the `set()` function can be used to create sets.

Note: to create an empty set you have to use `set()`, not `{}`; the latter creates an empty dictionary, a data structure that we discuss in the next section.

Here is a brief demonstration:

```python
>>> basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
>>> print(basket)                      # show that duplicates have been removed
{'orange', 'banana', 'pear', 'apple'}
'orange' in basket                 # fast membership testing
True
'crabgrass' in basket
False
>>> # Demonstrate set operations on unique letters from two words
>>> a = set('abracadabra')
>>> b = set('alacazam')
>>> a                                  # unique letters in a
{'a', 'r', 'b', 'c', 'd'}   
>>> a - b                              # letters in a but not in b
{'r', 'd', 'b'}
>>> a | b                              # letters in a or b or both
{'a', 'c', 'r', 'd', 'b', 'm', 'z', 'l'}
>>> a & b                              # letters in both a and b
{'a', 'c'}
>>> a ^ b                              # letters in a or b but not both
{'r', 'd', 'b', 'm', 'z', 'l'}
```
Similar to list comprehensions, set comprehensions are also supported:

```python
>>> a = {x for x in 'abracadabra' if x not in 'abc'}
>>> a
{'r', 'd'}
```

## Dictionaries

Dictionaries are indexed by keys, which can be any immutable type; strings and numbers can always be keys. Tuples can be used as keys if they contain only strings, numbers, or tuples; if a tuple contains any mutable object either directly or indirectly, it cannot be used as a key.

You can’t use lists as keys, since lists can be modified in place using index assignments, slice assignments, or methods like `append()` and `extend()`.`

The main operations on a dictionary are storing a value with some key and extracting the value given the key. It is also possible to delete a key:value pair with `del`.

Performing `list(d)` on a dictionary returns a list of all the keys used in the dictionary, in insertion order (if you want it sorted, just use `sorted(d)` instead). To check whether a single key is in the dictionary, use the `in` keyword.

It is also possible to check whether a single key is in the dictionary using the `in` keyword. Demonstrating the dictionary:

```python
>>> tel = {'jack': 4098, 'sape': 4139}
>>> tel['guido'] = 4127
>>> tel
{'jack': 4098, 'sape': 4139, 'guido': 4127}
>>> tel['jack']
4098
>>> del tel['sape']
>>> tel['irv'] = 4127
>>> tel
{'jack': 4098, 'guido': 4127, 'irv': 4127}
>>> list(tel)
['jack', 'guido', 'irv']
>>> sorted(tel)
['guido', 'irv', 'jack']
>>> 'guido' in tel
True
>>> 'jack' not in tel
False
```

The dict() constructor builds dictionaries directly from sequences of key-value pairs:

```python
>>> dict([('sape', 4139), ('guido', 4127), ('jack', 4098)])
{'sape': 4139, 'guido': 4127, 'jack': 4098}
```
In addition, dict comprehensions can be used to create dictionaries from arbitrary key and value expressions:

```python
>>> {x: x**2 for x in (2, 4, 6)}
{2: 4, 4: 16, 6: 36}
>>> dict(sape=4139, guido=4127, jack=4098)
{'sape': 4139, 'guido': 4127, 'jack': 4098}
```

When the keys are simple strings, it is sometimes easier to specify pairs using keyword arguments:

```python
>>> dict([('sape', 4139), ('guido', 4127), ('jack', 4098)])
{'sape': 4139, 'guido': 4127, 'jack': 4098}
```

## Looping Techniques

When looping through a dictionary, the key and corresponding value can be retrieved at the same time using the items() method.

```python
>>> knights = {'gallahad': 'the pure, 'robin': 'the brave'}
>>> for k, v in knights.items():
...     print(k, v)
...
gallahad the pure
robin the brave
```

When looping through a sequence, the position index and corresponding value can be retrieved at the same time using the enumerate() function.

```python
>>> for i, v in enumerate(['tic', 'tac', 'toe']):
...     print(i, v)
...
0 tic
1 tac
2 toe
```

To loop over two or more sequences at the same time, the entries can be paired with the zip() function.

```python
>>> questions = ['name', 'quest', 'favorite color']
>>> answers = ['lancelot', 'the holy grail', 'blue']
>>> for q, a in zip(questions, answers):
...     print('What is your {0}?  It is {1}.'.format(q, a))
...
What is your name?  It is lancelot.
What is your quest?  It is the holy grail.
What is your favorite color?  It is blue.
```

To loop over a sequence in reverse, first specify the sequence in a forward direction and then call the reversed() function.

```python
>>> for i in reversed(range(1, 10, 2)):
...     print(i)
...
9
7
5
3
1
```

To loop over a sequence in sorted order, use the sorted() function which returns a new sorted list while leaving the source unaltered.

```python
>>> basket = ['apple', 'orange', 'apple', 'pear', 'orange', 'banana']
>>> for f in sorted(set(basket)):
...     print(f)
...
apple
banana
orange
pear
```

Using set() on a sequence removes duplicates. The `sorted()` function is often used in conjunction with `set()` to remove duplicates from a sequence and sort the result.

```python
>>> basket = ['apple', 'orange', 'apple', 'pear', 'orange', 'banana']
>>> for f in sorted(set(basket)):
...     print(f)
...
apple
banana
orange
pear
```

It is sometimes tempting to change a list while you are looping over it; however, it is often simpler and safer to create a new list instead.

```python
>>> import math
>>> raw_data = [56.2, float('NaN'), 51.7, 55.3, 52.5, float('NaN'), 47.8]
>>> filtered_data = []
>>> for value in raw_data:
...     if not math.isnan(value):
...         filtered_data.append(value)
...
>>> filtered_data
[56.2, 51.7, 55.3, 52.5, 47.8]
```

## More on Conditions

The conditions used in `while` and `if` statements can contain any operator, not just comparisons.

THe comparison operators `in` and `not in` check whether a value occurs (does not occur) in a sequence. The operators is and is not compare whether two objects are really the same object; this only matters for mutable objects like lists. All comparison operators have the same priority, which is lower than that of all numerical operators.

Comparisons can be chained. For example, `a < b == c` is equivalent to `a < b and b == c`, except that `b` is evaluated only once (but in both cases `a` is evaluated twice).

Comparisons may be combined using the Boolean operators `and` and `or`, and the outcome of a comparison (or of any other Boolean expression) may be negated with `not`. These have lower priorities than comparison operators; between them, `not` has the highest priority and `or` the lowest, so that `A and not B or C` is equivalent to `(A and (not B)) or C`. As always, parentheses can be used to express the desired composition.

The Boolean operators `and` and `or` are so-called short-circuit operators: their arguments are evaluated from left to right, and evaluation stops as soon as the outcome is determined. For example, if `A` and `C` are true but `B` is false, `A and B and C` does not evaluate the expression `C`. When used as a general value and not as a Boolean, the return value of a short-circuit operator is the last evaluated argument.

It is possible to assign the result of a comparison or other Boolean expression to a variable. For example,

```python
>>> x = 2
>>> 1 < x < 3
True
>>> 1 < x and x < 3
True
```

## Comparing Sequences and Other Types

Sequence objects may be compared to other objects with the same sequence type. The comparison uses lexicographical ordering: first the first two items are compared, and if they differ this determines the outcome of the comparison; if they are equal, the next two items are compared, and so on, until either sequence is exhausted. If two items to be compared are themselves sequences of the same type, the lexicographical comparison is carried out recursively. If all items of two sequences compare equal, the sequences are considered equal. If one sequence is an initial sub-sequence of the other, the shorter sequence is the smaller (lesser) one. Lexicographical ordering for strings uses the Unicode code point number to order individual characters. Some examples of comparisons between sequences of the same type:

```python
>>> (1, 2, 3)              < (1, 2, 4)
True
>>> [1, 2, 3]              < [1, 2, 4]
True
>>> 'ABC' < 'C' < 'Pascal' < 'Python'
True
>>> (1, 2, 3, 4)           < (1, 2, 4)
True
>>> (1, 2)                 < (1, 2, -1)
True
>>> (1, 2, 3)             == (1.0, 2.0, 3.0)
True
>>> (1, 2, ('aa', 'ab'))   < (1, 2, ('abc', 'a'), 4)
True
```

Note that comparisons of mixed type sequences attempt to convert the objects to a common type for the comparison. If this is not possible, a `TypeError` exception is raised. For example:

```python
>>> (1, 2, 3)        <  (1, 2, 4.0)
True
>>> (1, 2, ('aa', 'ab')) < (1, 2, ('abc', 'a'), 4)
True
```

## The `is` Operator

The `is` operator compares the identity of two objects; the `is not` operator negates the `is` operator.

```python
>>> x = y = [1, 2, 3]
>>> z = [1, 2, 3]

>>> x == y
True
>>> x == z
True
>>> x is y
True
>>> x is z
False
>>> x is not z
True
```

