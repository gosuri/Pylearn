# Modules

A module is a collection of functions, types and type classes. Modules are
defined in a file with the extension `.py`. The name of the module is the
name of the file. For example, the module `math` is defined in the file
`math.py`.

A module can be imported into another module using the `import` statement.
For example, to import the `math` module:

```python
import math
```

The `math` module defines a function called `sqrt` that computes the square
root of a number:

```python
>>> math.sqrt(4)
2.0
```

A module can contain executable statements as well as function definitions. These statements are intended to initialize the module. They are executed only the first time the module name is encountered in an import statement. (They are also run if the file is executed as a script.)

Each module has its own private namespace, which is used as the global symbol table for all functions defined in the module. Thus, the author of a module can use global variables in the module without worrying about accidental clashes with a user’s global variables. On the other hand, if you know what you are doing you can touch a module’s global variables with the same notation used to refer to its functions, modname.itemname.

Modules can import other modules. It is customary but not required to place all import statements at the beginning of a module (or script, for that matter).

There are several ways to import a module. The simplest way is to import the module name:

```python
import math
```

This does not introduce the module’s name in the current symbol table; it only introduces the module’s functions into the current symbol table. Using the module name prefix, you can access the function:

```python
>>> math.sqrt(4)
2.0
```

Another form of import statement imports names from a module directly into the importing module’s symbol table. For example:

```python
from math import sqrt
```

This does not introduce the module’s name in the current symbol table; it only introduces the function `sqrt` into the current symbol table. Using the function name, you can access the function:

```python
>>> sqrt(4)
2.0
```

The third form of import statement imports all names that a module defines into the importing module’s symbol table. For example:

```python
from math import *
```

This does not introduce the module’s name in the current symbol table; it only introduces the functions into the current symbol table. Using the function name, you can access the function:

```python
>>> sqrt(4)
2.0
```

if the module name is followed by `as`, then it is bound directly to the given name. For example:

```python
import math as m
```

It can also be used to import a specific attribute from a module into the current namespace:

```python
from math import sqrt as s
```

## Executing modules as scripts

When you run a module with:

```bash
python fibo.py <arguments>
```

the code in the module will be executed, just as if you imported it, but with the `__name__` set to `"__main__"`. That means that by adding this code at the end of your module:

```python
if __name__ == "__main__":
    import sys
    fib(int(sys.argv[1]))
```

you can make the file usable as a script as well as an importable module, because the code that parses the command line only runs if the module is executed as the “main” file:

```bash
$ python fibo.py 50
12586269025
```
if the module is imported, the code is not run:

```python
>>> import fibo
>>>
```

## The Module Search Path

When a module named `spam` is imported, the interpreter first searches for a built-in module with that name. If not found, it then searches for a file named `spam.py` in a list of directories given by the variable `sys.path`. `sys.path` is initialized from these locations:

* The directory containing the input script (or the current directory when no file is specified).
* `PYTHONPATH` (a list of directory names, with the same syntax as the shell variable `PATH`).
* The installation-dependent default.

After initialization, `PYTHONPATH` is modified by the site module to add site-specific paths. The site module also adds `/usr/local/lib/python` and `/usr/lib/python` to `sys.path`. (The actual directory names depend on the version of Python and the installation.)

You can modify `sys.path` using standard list operations:

```python
import sys
sys.path.append('/ufs/guido/lib/python')
```

## “Compiled” Python files

Top speed up loading modules, Python caches the compiled version of each module in the `__pycache__` directory under the name `module.version.pyc`, where the version encodes the format of the compiled file; it generally contains the Python version number. For example, `__pycache__/foo.cpython-35.pyc` would be the compiled version of `foo.py` for Python 3.5.

The compiled version of a module is stale if the source changes; stale compiled files are silently ignored. If you want to force Python to recompile a module, you can use the `-B` command-line option to disable the creation of `*.pyc` files or you can delete the corresponding `*.pyc` file(s).

Python checks the modification time of the source against the time of the compiled version, and recompiles it if necessary. This is done automatically when you import a module, but you can also use the `-c` command-line option to compile a module without importing it.

Python does not check the cache in two circumstances. First, it always recompiles a module if it was loaded from a source file that is still open. Second, it never looks in the cache if the source file has the same name as a built-in module (for example, `sys.py`).

Some tips for speeding up Python programs:

* You can use the `-O` command-line option to remove all of the `assert` statements from your program. This can make a big difference in the speed of programs that contain many `assert` statements.
* You can use the `-OO` command-line option to remove all of the `assert` and `__doc__` statements. This can make a big difference in the speed of programs that contain many `assert` statements.
* A program doesn't run any faster when it is read from a `.pyc` file than when it is read from a `.py` file. The `.pyc` file is only used to speed up the loading of the module. If you want to speed up the execution of a program, you should compile it to a standalone executable using `py2exe` or `py2app`.
* The module compileall can precompile all modules in a directory tree.

## Standard Modules

Python comes with a library of standard modules, described in [The Python Standard Library](https://docs.python.org/3/library/index.html). Most of these modules are written in C and provide access to system functionality such as file I/O that would otherwise be inaccessible to Python programmers, as well as to various operating system services. Some modules are written in Python and provide access to operations that are too bulky for inclusion in the interpreter, such as regular expression support.

One of the most useful modules is `sys`, which provides access to some variables used or maintained by the interpreter and to functions that interact strongly with the interpreter. It is always available.

## The 'dir()' Function

The built-in function `dir()` is used to find out which names a module defines. It returns a sorted list of strings:

```python
>>> import fibo, sys
>>> dir(fibo)
['__name__', 'fib', 'fib2']
>>> dir(sys)
['__breakpointhook__', '__displayhook__', '__doc__', '__excepthook__',
 '__interactivehook__', '__loader__', '__name__', '__package__', '__spec__',
 '__stderr__', '__stdin__', '__stdout__', '__unraisablehook__',
 '_clear_type_cache', '_current_frames', '_debugmallocstats', '_framework',
 '_getframe', '_git', '_home', '_xoptions', 'abiflags', 'addaudithook',
 'api_version', 'argv', 'audit', 'base_exec_prefix', 'base_prefix',
 'breakpointhook', 'builtin_module_names', 'byteorder', 'call_tracing',
 'callstats', 'copyright', 'displayhook', 'dont_write_bytecode', 'exc_info',
 'excepthook', 'exec_prefix', 'executable', 'exit', 'flags', 'float_info',
 'float_repr_style', 'get_asyncgen_hooks', 'get_coroutine_origin_tracking_depth',
 'getallocatedblocks', 'getdefaultencoding', 'getdlopenflags',
 'getfilesystemencodeerrors', 'getfilesystemencoding', 'getprofile',
 'getrecursionlimit', 'getrefcount', 'getsizeof', 'getswitchinterval',
 'gettrace', 'hash_info', 'hexversion', 'implementation', 'int_info',
 'intern', 'is_finalizing', 'last_traceback', 'last_type', 'last_value',
 'maxsize', 'maxunicode', 'meta_path', 'modules', 'path', 'path_hooks',
 'path_importer_cache', 'platform', 'prefix', 'ps1', 'ps2', 'pycache_prefix',
 'set_asyncgen_hooks', 'set_coroutine_origin_tracking_depth', 'setdlopenflags',
 'setprofile', 'setrecursionlimit', 'setswitchinterval', 'settrace', 'stderr',
 'stdin', 'stdout', 'thread_info', 'unraisablehook', 'version', 'version_info',
 'warnoptions']
```

Without arguments, `dir()` lists the names you have defined currently:

```python
>>> a = [1, 2, 3, 4, 5]
>>> import fibo
>>> fib = fibo.fib
>>> dir()
['__builtins__', '__doc__', '__loader__', '__name__', '__package__', '__spec__',
 'a', 'fib', 'fibo', 'sys']
```

dir() does not list the names of built-in functions and variables. If you want a list of those, they are defined in the standard module `builtins`:

```python
>>> import builtins
>>> dir(builtins)
['ArithmeticError', 'AssertionError', 'AttributeError', 'BaseException',
 'BlockingIOError', 'BrokenPipeError', 'BufferError', 'BytesWarning',
 'ChildProcessError', 'ConnectionAbortedError', 'ConnectionError',
 'ConnectionRefusedError', 'ConnectionResetError', 'DeprecationWarning',
 'EOFError', 'Ellipsis', 'EnvironmentError', 'Exception', 'False', 'FileExistsError',
 'FileNotFoundError', 'FloatingPointError', 'FutureWarning', 'GeneratorExit',
 'IOError', 'ImportError', 'ImportWarning', 'IndentationError', 'IndexError',
 'InterruptedError', 'IsADirectoryError', 'KeyError', 'KeyboardInterrupt',
 'LookupError', 'MemoryError', 'NameError', 'None', 'NotADirectoryError',
 'NotImplemented', 'NotImplementedError', 'OSError', 'OverflowError',
 'PendingDeprecationWarning', 'PermissionError', 'ProcessLookupError',
 'RecursionError', 'ReferenceError', 'ResourceWarning', 'RuntimeError',
 'RuntimeWarning', 'StopAsyncIteration', 'StopIteration', 'SyntaxError',
 'SyntaxWarning', 'SystemError', 'SystemExit', 'TabError', 'TimeoutError',
 'True', 'TypeError', 'UnboundLocalError', 'UnicodeDecodeError',
 'UnicodeEncodeError', 'UnicodeError', 'UnicodeTranslateError',
 'UnicodeWarning', 'UserWarning', 'ValueError', 'Warning', 'ZeroDivisionError',
 '__build_class__', '__debug__', '__doc__', '__import__', '__loader__',
 '__name__', '__package__', '__spec__', 'abs', 'all', 'any', 'ascii', 'bin',
 'bool', 'breakpoint', 'bytearray', 'bytes', 'callable', 'chr', 'classmethod',
 'compile', 'complex', 'delattr', 'dict', 'dir', 'divmod', 'enumerate',
 'eval', 'exec', 'filter', 'float', 'format', 'frozenset', 'getattr',
 'globals', 'hasattr', 'hash', 'help', 'hex', 'id', 'input', 'int', 'isinstance',
 'issubclass', 'iter', 'len', 'license', 'list', 'locals', 'map', 'max',
 'memoryview', 'min', 'next', 'object', 'oct', 'open', 'ord',
'pow', 'print', 'property', 'quit', 'range', 'repr', 'reversed', 'round',
'set', 'setattr', 'slice', 'sorted', 'staticmethod', 'str', 'sum', 'super',
'tuple', 'type', 'vars', 'zip']
```

## Packages

Packages are a way of structuring Python’s module namespace by using “dotted module names”. For example, the module name `A.B` designates a submodule named `B` in a package named `A`. Just like the use of modules saves the authors of different modules from having to worry about each other’s global variable names, the use of dotted module names saves the authors of multi-module packages like NumPy or Pillow from having to worry about each other’s module names.

Suppose you want to design a collection of modules (a “package”) for the uniform handling of sound files and sound data. There are many different sound file formats (`.wav`, `.aiff`, `.au`, `.snd`), so you may need to create and maintain a growing collection of modules for the conversion between the various file formats. There may also be a great variety of operations you want to perform on sound data, such as mixing, adding echo, applying an equalizer function, creating an artificial stereo effect, and so on. 


Here's a possible structure the package (this example assumes that the modules described here have already been written):

```python
sound/
    __init__.py
    formats/
        __init__.py
        wavread.py
        wavwrite.py
        aiffread.py
        aiffwrite.py
        auread.py
        auwrite.py
        sndhdr.py
    effects/
        __init__.py
        echo.py
        surround.py
        reverse.py
        ...
```

When importing the package, Python searches through the directories on `sys.path` looking for the package subdirectory. Once found, the interpreter executes all the `__init__.py` files it finds along the way. These can perform various initialization tasks (including setting the `__all__` variable, described later), and they can also contain the `import` statements that actually load the package’s modules into the package’s namespace. For example, the file `sound/effects/__init__.py` might contain the following code:

```python
from . import echo
from . import surround
from . import reverse
```

This would cause the three named submodules to be imported when the `sound.effects` package is imported, as in `import sound.effects`. It would also mean that references such as `sound.effects.echo.echofilter(input, output, delay=0.7, atten=4)` would work, assuming the `echo` module had been defined (it probably also contains an `__init__.py` file).

### Importing *From* a Package

There are four ways to import modules from a package:

1. `import package.module`
2. `from package import module`
3. `from package.module import name`
4. `from package.module import *`

The first way, `import package.module`, imports the module named `module` from the package named `package`. The `package` must be in the list of directories that is contained in the variable `sys.path`. The statement `import package.module` is equivalent to `import module` if the search path is appropriately modified.

The second way, `from package import module`, imports the module named `module` from the package named `package`. The `package` must be in the list of directories that is contained in the variable `sys.path`. The statement `from package import module` is equivalent to `import package.module` if the search path is appropriately modified.

The third way, `from package.module import name`, imports the submodule `module` from the package `package` and then imports the attribute `name` from the module `module`. The `package` must be in the list of directories that is contained in the variable `sys.path`. The statement `from package.module import name` is equivalent to `from package.module import name` if the search path is appropriately modified.

The fourth way, `from package.module import *`, imports the submodule `module` from the package `package` and then imports all names except those beginning with an underscore (`_`) from the module `module`. The `package` must be in the list of directories that is contained in the variable `sys.path`. The statement `from package.module import *` is equivalent to `from package.module import *` if the search path is appropriately modified.

### Intra-package References

When packages are structured into subpackages (as with the `sound` package in the example), you can use absolute imports to refer to submodules of siblings packages. For example, if the module `sound.filters.vocoder` needs to use the `echo` module in the `sound.effects` package, it can use `from sound.effects import echo`.   

### Packages in Multiple Directories

The simple case of a package contained in a single directory is handled by the `import` statement; the statement `import sound.effects.echo` searches for a built-in module named `sound`, then for a file named `sound.py` in a list of directories given by the variable `sys.path`, and then for a directory named `sound` in the same list. When it finds a directory, it looks for a file named `__init__.py` in that directory, and treats that as a package. The `__init__.py` can contain the same set of import statements that any other module can contain, and Python adds some additional attributes to the module when it is imported in this way. (See section The Module Search Path for more information on how Python searches for modules.)