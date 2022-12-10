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

## The Python Environment