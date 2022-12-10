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
