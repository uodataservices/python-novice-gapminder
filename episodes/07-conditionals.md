---
title: Conditionals
teaching: 10
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Write conditional statements including if, elif, and else branches.
- Trace the execution of conditionals.
- Apply conditionals inside loops.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can my programs do different things based on data values?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Booleans can be True or False

We've discussed the following *primitive* data types so far: strings, ints, and floats. Let's add bools or Booleans to that list.

Booleans can be `True` or `False`. They are returned by conditional statements formed with operators like `==`, `<`, or `>`.

```python
print(3 > 5) # Should return False
```
```output
False
```

The `==` sign and `=` have very different meanings in Python. The `==` sign tests whether or not two values are equal.

```python
y = 4 # Assignment
print (y == 4) # Is y (4) equal to 4?
```
```output
True
```

## Use if statements to control whether or not a block of code is executed
Today, we will discuss [**control flow**](https://docs.python.org/3/tutorial/controlflow.html), one of the most powerful aspects of programming languages.

* An **if statement** controls whether or not a block of code is executed.
* The first line of an if statement starts with `if` and ends with a colon.
* The body of an if statement is indented, just like a for loop.

```python
temp_f = 95
if temp_f > 90: # The indented block runs if (temp_f > 90) is True
    print("Specimen is too hot")
```
```output
Specimen is too hot
```

If the condition tested in the if statement evalutates to `True`, then the block of code underneath the if statement executes. If it evaluates to `False`, the code block is skipped.

## Conditionals can be used with loops
Conditionals can be used used inside loops to do different things with different items in a collection.

```python
grades = [70, 85, 90, 42, 95, 63]
for grade in grades:
    if grade >= 70:
        print("This is a passing grade", grade)
```
```output
This is a passing grade 70
This is a passing grade 85
This is a passing grade 90
This is a passing grade 95
```

Let's combine this with the accumulator pattern to answer a more sophisticated question. Rather than print the passing grades, let's print the *number* of students who passed.

```python
passed = 0 # Initialize to zero
for grade in grades:
    if grade >= 70:
        passed = passed + 1
print(passed, "students passed the class.")
```
```output
4 students passed the class.
```

## Use `else` to execute a block of code when an `if` condition is *not* true.

**Else** executes a block of code when an if condition is **not** `True`. It is always paired with an **if** statement.

* `else` is indented like the **if** it is paired with.
* Not every `if` needs an `else` but every `else` needs an `if`.

```python
temp = 32
if temp > 90:
    print("It's too hot")
else:
    print("It's freezing.")
```
```output
It's freezing.
```

:::::::::::::::::::::::::::::::::::::::  challenge

## If, else, and indentation

When using conditional statements, `if variable` is shorthand for `if variable == True`.

In the example below, how many print statements will print if `no_gas` is `True`? How many if `no_gas` is `False`?
```python
no_gas = _____
if no_gas:
    print("Getting gas")
    no_gas = False
else:
    print("Buying snacks")
print("Resumed driving")
```

:::::::::::::::  solution

## Solution

If `no_gas` is True, the "Getting gas" and "Resumed driving" statements will print.

```output
Getting gas
Resumed driving
```

If `no_gas` is False, the "Buying snacks" and "Resumed driving" statements will print.
```output
Buying snacks
Resumed driving
```

Though the value of `no_gas` was changed within the code block under the `if` statement, the `else` statement was skipped over. Which block of code executes in an if/else pair is decided at the the time the `if` is tested. 

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Use `elif` to specify additional tests

We can also chain several tests together using elif, which is short for “else if”. The following Python code uses `elif` to print the sign of a number.

```python
num = -3
if num > 0:
    print(num, 'is positive')
elif num == 0:
    print(num, 'is zero')
else:
    print(num, 'is negative')
```
```output
-3 is negative
```

## Conditions are tested once, in order

* Exactly one condition of an `if`/`else` pair or an `if`/`elif`/`else` trio will execute.
* Consecutive `if` statements are tested independently and in order.

```python
grade = 85
if grade >= 90:
    print('grade is A')
elif grade >= 80:
    print('grade is B')
elif grade >= 70:
    print('grade is C')
```
```output
grade is B
```

Python does *not* go back and re-evaluate a statement if the values change.

```python
velocity = 10.0
if velocity > 20.0:
    print('moving too fast')
else:
    print('adjusting velocity')
    velocity = 50.0
```
```output
adjusting velocity
```

## Use `and` and `or` to combine tests

We can also combine tests using `and` and `or`. `and` is only true if both parts are true:

```python
if (1 > 0) and (-1 >= 0):
    print('both parts are true')
else:
    print('at least one part is false')
```
```output
at least one part is false
```

`or` is true if at least one part is true:

```python
if (1 < 0) or (1 >= 0):
    print('at least one test is true')
```
```output
at least one test is true
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Tracing Execution

What does this program print?

```python
pressure = 71.9
if pressure > 50.0:
    pressure = 25.0
elif pressure <= 50.0:
    pressure = 0.0
print(pressure)
```

:::::::::::::::  solution

## Solution

```output
25.0
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Trimming Values

Fill in the blanks so that this program creates a new list
containing zeroes where the original list's values were negative
and ones where the original list's values were positive.

```python
original = [-1.5, 0.2, 0.4, 0.0, -1.3, 0.4]
result = ____
for value in original:
    if ____:
        result.append(0)
    else:
        ____
print(result)
```

```output
[0, 1, 1, 1, 0, 1]
```

:::::::::::::::  solution

## Solution

```python
original = [-1.5, 0.2, 0.4, 0.0, -1.3, 0.4]
result = []
for value in original:
    if value < 0.0:
        result.append(0)
    else:
        result.append(1)
print(result)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Computing absolute value using conditionals

Let's say you want to compute the absolute value $|x|$ of each float x in a list. Append each value to a new list called `result` in the same order as the `original` input. Do not change the values in `original`.

I have provided a skeleton to get you started.

```python
original = [-1.5, 0.2, 0.4, -1.3]
result = ___
for value in original:
    if value < ___: # if negative
        result.append(value * __)
    else: # if positive
        result.append(____)
print(result)
```

:::::::::::::::  solution

## Solution

```python
original = [-1.5, 0.2, 0.4, -1.3]
result = [] # Initialize an empty list
for value in original:
    if value < 0: # if negative
        result.append(value * -1)
    else: # if positive
        result.append(value) # abs val of a positive number is itself 
print(result)
```
```output
[1.5, 0.2, 0.4, 1.3]
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Use `if` statements to control whether or not a block of code is executed.
- Conditionals are often used inside loops.
- Use `else` to execute a block of code when an `if` condition is *not* true.
- Use `elif` to specify additional tests.
- Conditions are tested once, in order.
- X `and` Y is only true if both X and Y are true.
- X `or` Y is true if either X or Y, or both, are true.

::::::::::::::::::::::::::::::::::::::::::::::::::


