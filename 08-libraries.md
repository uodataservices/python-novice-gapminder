---
title: Libraries
teaching: 20
exercises: 20
---

::::::::::::::::::::::::::::::::::::::: objectives

- Explain what software libraries are and why programmers use them.
- Write programs that import and use modules from Python's standard library.
- Find and read documentation for the standard library interactively (in the interpreter) and online.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I use software that other people have written?
- How can I find out what that software does?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Most of the power of a programming language is in its libraries.

A *library* or *module* is a collection of files that contain functions for use by other programs. They can also contain constants like Pi and Tau.

The Python standard library is a suite of modules that come with **all** Python installations.

You have additional libraries available to you from **Anaconda** and from package managers like **PyPi**.

:::::::::::::::::::::::::::::::::::::::::  callout

## Libraries and modules

A library is a collection of modules, but the terms are often used
interchangeably, especially since many libraries only consist of a single
module, so don't worry if you mix them.


::::::::::::::::::::::::::::::::::::::::::::::::::

## A program must import a library module before using it.

To use a library module you must import it. You only need to import a module once per file or interactive session.

Let's use the [math](https://docs.python.org/3/library/math.html) module
to find the cosine of pi. This is a module from Python's standard library.

```python
import math 
print("Pi is", math.pi) # Prints the constant pi stored in the math library
```
```output
pi is 3.141592653589793
```

You can use imported functions using dot-notation. Prefix the function with the name of the library (math), add a `.', then call it just as you would any function.

```python
x = math.cos(math.pi) # Assigns x the value returned by cos(pi)
print(x)
```
```output
-1.0
```

## Use `help` to learn about the contents of a library module.

- This just like `help` for a function. It lists all the functions and constants available in the module.

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

- Use `from ... import ...` syntax to load only specific items from a library module.
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

print('The cube root of 27 is', m.cbrt(27))
```
```output
The cube root of 27 is 3.0
```

This is commonly used for libraries that are frequently used and/or have long names. For example, the library `pandas`, used later in this workshop, is aliased `pd`.

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

## Rewriting Absolute Value

Remember our previous absolute value exercise? The math module has a [.fabs()](https://docs.python.org/3/library/math.html#math.fabs) function that returns the absolute value of a number. 

Update the following code to simplify the process of computing the absolute value of each number in a list of numbers.
```python
from math import fabs
original = [-1.5, 0.2, 0.4, -1.3]
result = [] # Initialize an empty list
for value in original:
  result.append(____(value)) # Update this line
print(result)
```

:::::::::::::::  solution

## Solution

```python
from math import fabs
original = [-1.5, 0.2, 0.4, -1.3]
result = [] # Initialize an empty list
for value in original:
  result.append(fabs(value)) 
print(result)
```
```output
[1.5, 0.2, 0.4, 1.3]
```
  
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


