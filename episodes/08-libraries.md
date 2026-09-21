---
title: Libraries
teaching: 10
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Explain what software libraries are and why programmers create and use them.
- Write programs that import and use modules from Python's standard library.
- Find and read documentation for the standard library interactively (in the interpreter) and online.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I use software that other people have written?
- How can I find out what that software does?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Most of the power of a programming language is in its libraries.

- A *library* is a collection of files (called *modules*) that contains
  functions for use by other programs.
  - May also contain data values (e.g., numerical constants) and other things.
  - Library's contents are supposed to be related, but there's no way to enforce that.
- The Python [standard library][stdlib] is an extensive suite of modules that comes
  with Python itself.
- Many additional libraries are available from [PyPI][pypi] (the Python Package Index).
- We will see later how to write new libraries.

:::::::::::::::::::::::::::::::::::::::::  callout

## Libraries and modules

A library is a collection of modules, but the terms are often used
interchangeably, especially since many libraries only consist of a single
module, so don't worry if you mix them.


::::::::::::::::::::::::::::::::::::::::::::::::::

## A program must import a library module before using it.

- Use `import` to load a library module into a program's memory.
- Then refer to things from the module as `module_name.thing_name`.
  - Python uses `.` to mean "part of" or "in".

Let's use the [math](https://docs.python.org/3/library/math.html) module
to find the cosine of pi.

```python
import math

print('pi is', math.pi)
print('cos(pi) is', math.cos(math.pi))
```

```output
pi is 3.141592653589793
cos(pi) is -1.0
```

- Have to refer to each item with the module's name.
  - `math.cos(pi)` won't work: the reference to `pi`
    doesn't somehow "inherit" the function's reference to `math`.

## Use `help` to learn about the contents of a library module.

- This just like `help` for a function.

```python
help(math)
```

```output
Help on module math:

NAME
    math

MODULE REFERENCE
    http://docs.python.org/3/library/math

    The following documentation is automatically generated from the Python
    source files.  It may be incomplete, incorrect or include features that
    are considered implementation detail and may vary between Python
    implementations.  When in doubt, consult the module reference at the
    location listed above.

DESCRIPTION
    This module is always available.  It provides access to the
    mathematical functions defined by the C standard.

FUNCTIONS
    acos(x, /)
        Return the arc cosine (measured in radians) of x.
⋮ ⋮ ⋮
```

## Import specific items from a library module to shorten programs.

- Use `from ... import ...` to load only specific items from a library module.
- In this format, you don't have to use the library name as a prefix.


```python
from math import pi, pow

radius = 5
area = pi * pow(5, 2)
print("The area of a circle with radius 5 is", area)
```

```output
The area of a circle with radius 5 is 78.53981633974483
```

## Create an alias for a library module when importing it to shorten programs.

- Use `import ... as ...` to give a library a short *alias* while importing it.
- You can refer to functions or constants in the library using that shortened name.

```python
import math as m

print('cos(pi) is', m.cos(m.pi))
```

```output
cos(pi) is -1.0
```

- Commonly used for libraries that are frequently used and/or have long names.
  - For example, the library `pandas`, used later in this workshop, is aliased `pd`.

:::::::::::::::::::::::::::::::::::::::  challenge

## Exploring the Math Module

1. What function from the `math` module can you use to calculate a square root
  *without* using `sqrt`?
2. Since the library contains this function, why does `sqrt` exist?

**HINT**: A square root can be written as x<sup>1/2</sup> or x<sup>0.5</sup> in exponent notation.

:::::::::::::::  solution

## Solution

Using `help(math)` we see that we've got `pow(x,y)` in addition to `sqrt(x)`,
  so we could use `pow(x, 0.5)` to find a square root too! The `sqrt(x)` function is more readable than `pow(x, 0.5)`. Readability is a cornerstone of good programming, so it makes sense to provide a special function for this common case.
  
  
:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Getting Help with Modules

When a colleague of yours types `help(statistics)`, Python reports an error:

```error
NameError: name 'statistics' is not defined
```

What has your colleague forgotten to do?

:::::::::::::::  solution

## Solution

Your colleague has forgotten to import the statistics module. This can be fixed as follows.

```python
import statistics
help(statistics)
```

```output
Help on module statistics:

NAME
    statistics - Basic statistics module.
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Applying New Modules

Let's say you want find to the *average* of the following five measurements in inches: 60, 65, 58, 70, 63. The [statistics](https://docs.python.org/3/library/statistics.html) module
should be able to help you.

1. Create a list named `heights` with the the measurements `[60, 65, 58, 70, 63]`.
2. Find a function inside the statistics module that computes the average of a list. 
Use `help()` to find it.
3. Apply that function to `heights`.

```python
import statistics
heights = ____

print("The average is", _____.______(heights), "inches.")
```

:::::::::::::::  solution

## Solution

The function you're looking for is [mean](https://docs.python.org/3/library/statistics.html#statistics.mean), which computes the average of a list of numbers.

```python
import statistics
heights = [60, 65, 58, 70, 63]
print("The average is", statistics.mean(heights), "inches.")
```

```output
The average is 63.2 inches.
```


:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Importing With Aliases

1. Fill in the blanks so that the program below prints the square root of pi.
2. Rewrite the program so that it uses `import` *without* `as`.
3. Which form do you find easier to read?

```python
import ____ as m
root_pi = ____.sqrt(___.pi)
print(____)
```

:::::::::::::::  solution

## Solution

```python
import math as m
root_pi = m.sqrt(m.pi)
print(root_pi)
```

This can be rewritten as:

```python
import math
root_pi = math.sqrt(math.pi)
print(root_pi)
```

Since you just wrote the code, you might actually
find the first version easier to read. But when trying to read a huge piece
of code written by someone else, non-abbreviated names are often easier, except
where there are clear conventions. 



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Reading Error Messages

1. Read the code below and try to identify what the errors are without running it.
2. Run the code, and read the error message. What type of error is it?

```python
from math import log
log(0)
```

:::::::::::::::  solution

## Solution

```output
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-1-d72e1d780bab> in <module>
      1 from math import log
----> 2 log(0)

ValueError: math domain error
```

1. The logarithm of `x` is only defined for `x > 0`, so 0 is outside the
  domain of the function.
2. You get an error of type `ValueError`, indicating that the function
  received an inappropriate argument value. The additional message
  "math domain error" makes it clearer what the problem is.
  
  

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

[stdlib]: https://docs.python.org/3/library/
[pypi]: https://pypi.python.org/pypi/
[randommod]: https://docs.python.org/3/library/random.html
[pep8-imports]: https://pep8.org/#imports


:::::::::::::::::::::::::::::::::::::::: keypoints

- Most of the power of a programming language is in its libraries.
- A program must import a library module in order to use it.
- Use `help` to learn about the contents of a library module.
- The `math` and `statistics` modules contain helpful functions and constants
for mathematical operations.
- Import specific items from a library or create an alias to shorten programs.

::::::::::::::::::::::::::::::::::::::::::::::::::


