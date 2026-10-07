---
title: Variables and Assignment
teaching: 20
exercises: 20
---

::::::::::::::::::::::::::::::::::::::: objectives

- Write programs that assign values to variables.
- Correctly trace value changes in programs.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- What basic data types can I work with in Python?
- How can I create a new variable in Python?
- How do I use the `print()` function?
- Can I change the value associated with a variable after I create it?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Variables

To do anything useful with data, we need to assign its value to a *variable*.
We [assign](../learners/reference.md#assign) a value to a
[variable](../learners/reference.md#variable), using the equals sign `=`.

For example, we can track the height of a patient by
assigning the value `65` to a variable `height_cm`:

```python
height_cm = 65
```

In the future, Python will substitute the value we assigned to
`height_cm` when evaluating statements. 

```python
height_cm
```
```output
65
```

In Python, variable names:

- can include letters, digits, and underscores
- cannot start with a digit
- are [case sensitive](../learners/reference.md#case-sensitive).

This means that, for example:

- `height0` is a valid variable name, whereas `0height` is not
- `height` and `height` are different variables

A variable is created when a value is assigned to it.

Here, Python assigns 42 to the variable `age`
  and a *string* (always in quotes) to the variable `first_name`.
  
```python
age = 42
first_name = 'Ahmed'
```

## Use `print` to display values.

- Python has a built-in function called `print` that prints things as text.
- Call the function (i.e., tell Python to run it) by using its name.
- Provide values to the function (i.e., the things to print) in parentheses.

We can print a single value like this.

```python
print(height_cm)
```
```output
65
```

We can display multiple values in one line of output by passing in comma-separated **arguments** to `print()`.

```python
print(first_name, 'is', age, 'years old')
```

```output
Ahmed is 42 years old
```

By default, `print` function puts a single space between items to separate them and wrapss them in a single line.

## Variables must be created before they are used.

- If a variable doesn't exist yet, or if the name has been mis-spelled,
  Python reports an error. (Unlike some languages, which "guess" a default value.)

```python
print(last_name)
```

```error
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-1-c1fbb4e96102> in <module>()
----> 1 print(last_name)

NameError: name 'last_name' is not defined
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Variables Persist Between Cells

Be aware that it is the *order* of execution of cells that is important in a Jupyter notebook, not the order
in which they appear. Python remembers *all* the code that was run previously in a given session, including any variables you have
defined, irrespective of the order in the notebook. 

If you define variables lower down the notebook and then
(re)run cells further up, those defined further down will still be present. As an example, create two cells with the
following content, in this order:

```python
print(myval)
```

```python
myval = 1
```

* If you execute this in order, the first cell will give an error.
* However, if you run the first cell *after* the second
cell it will print out `1`. 
* To prevent confusion, it can be helpful to use the `Kernel` -> `Restart & Run All` option which
restarts the kernel and runs everything from top to bottom.
* A good Jupyter Notebook will execute as intended when cells are run from top to bottom.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Variables can be used in calculations.

We can use variables in calculations just as if they were values.

```python
age = age + 3
print('Age in three years:', age)
```

```output
Age in three years: 45
```

## Python is case-sensitive.

- Python thinks that upper- and lower-case letters are different,
  so `Name` and `name` are different variables.
- There are conventions for using upper-case letters at the start of variable names so we will use lower-case letters for now.

## Use meaningful variable names.

- Python doesn't care what you call variables as long as they obey the rules
  (alphanumeric characters and the underscore).

```python
flab = 42
ewr_422 = 'Ahmed'
print(ewr_422, 'is', flab, 'years old')
```

- Use meaningful variable names to help other people understand what the program does.
- The most important "other person" is your future self.

:::::::::::::::::::::::::::::::::::::::  challenge

## Predicting Values

What is the final value of `position` in the program below?
(Try to predict the value without running the program,
then check your prediction.)

```python
initial = 'left'
position = initial
initial = 'right'
```

:::::::::::::::  solution

## Solution

```python
print(position)
```

```output
left
```

The `initial` variable is assigned the value `'left'`.
In the second line, the `position` variable also receives
the string value `'left'`. In the third line, the `initial` variable is given the
value `'right'`, but the `position` variable retains its string value
of `'left'`.


:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Check Your Understanding

What values do the variables `mass` and `age` have after each of the following statements?
Test your answer by executing the lines.

```python
mass = 47.5
age = 122
mass = mass * 2.0
age = age - 20
```

:::::::::::::::  solution

## Solution

1. `mass` holds a value of 47.5, `age` does not exist
2. `mass` still holds a value of 47.5, `age` holds a value of 122
3. `mass` now has a value of 95.0, `age`'s value is still 122
4. `mass` still has a value of 95.0, `age` now holds 102

To prove this, print `mass` and `age`.

```python
print("mass is", mass, "age is", age)
```
```output
mass is 95.0 age is 102
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Use variables to store values.
- Use `print` to display values.
- Variables persist between cells.
- Variables must be created before they are used.
- Variables can be used in calculations.
- Python is case-sensitive.
- Use meaningful variable names.

::::::::::::::::::::::::::::::::::::::::::::::::::


