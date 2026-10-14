---
title: For Loops
teaching: 10
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Explain what a for loop does.
- Correctly write for loops to repeat simple calculations.
- Trace changes to a loop variableas the loop runs.
- Trace chages to other variables as they are updated by a for loop.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I make a program repeat things?

::::::::::::::::::::::::::::::::::::::::::::::::::

## The power of programming comes from repetition
So far, we've been looking manipulating one value at a time. To write programs that are useful
for manipulating real data, we need to make Python perform repetitive tasks *for us*.

An example task that we might want to repeat is accessing numbers in a list. We could do this printing each number on a line of its own.

```python
odds = [1, 3, 5, 7]
print(odds[0])
print(odds[1])
print(odds[2])
print(odds[3])
```
```output
1
3
5
7
```

This is a bad approach for three reasons:

1. It's not scalable. We'd have to write hundreds of `print()` statements for a longer list.
2. It's difficult to maintain.
3. It's fragile. What happens if a list is shorter than we expected? (An error.)

We can solve this problem using a for loop that steps through each item in a collection.

```python
odds = [1, 3, 5, 7]
for num in odds:
    print(num)
```
```output
1
3
5
7
```

## A *for loop* executes commands once for each value in a collection.

A for loop tells Python to execute some statements once for each value in a list, a character string, or some other *collection*. 

The loop has three parts: an iterable, a loop variable, and a body that is repeated once for each item in the iterable. The name of a loop variable can be any valid variable name you choose, but it should indicate what you're looping over for readability. 

```python
for number in [2, 3, 5]: # the colon is important
    print(number) # so is the indentation
```

Let's anatomize this loop:

* The iterable, `[2, 3, 5]`, is what the loop is being run on. It is followed by a `:`.
* The body, `print(number)`, specifies what to do for each value in the collection.
* The loop variable, `number`, is what changes for each iteration of the loop.

This `for` loop is equivalent to:
```python
print(2)
print(3)
print(5)
```

And the `for` loop's output is:
```output
2
3
5
```

## The first line of the `for` loop must end with a colon, and the body must be indented.
The colon at the end of the first line signals the start of a *block* of statements.
Any consistent indentation is grammatical, but almost everyone uses four spaces or the tab key.

```python
for number in [2, 3, 5]:
print(number)
```
```error
IndentationError: expected an indented block
```

Python is picky about indentation and will not parse unexpected indents.
```python
firstName = "Jon"
  lastName = "Smith"
```
```error
  File "<ipython-input-7-f65f2962bf9c>", line 2
    lastName = "Smith"
    ^
IndentationError: unexpected indent
```

## Loop variables can be called anything.

As with all variables, loop variables are:
* Created on demand.
* Can have any valid variable name.

```python
for kitten in [2, 3, 5]:
    print(kitten)
```
```output
2
3
5
```

### You are not required to use loop variables in the body
You are not required to use the loop variable in the body of your loop. You can do **anything** `len(iterable)` times.

```python
for number in [1, 2, 3]:
    print("Hello")
```
```output
Hello
Hello
Hello
```

## The body of a loop can contain many statements.
The body of a loop can contain multiple statements, as long as they're all indented appropriately. 
All indented lines (an indented block) before the first unintended line are treated as part of the same loop and are evaluated in order.

```python
primes = [2, 3, 5] # First three primes
for p in primes:
    squared = p ** 2
    cubed = p ** 3
    print(p, squared, cubed)
```
```output
2 4 8
3 9 27
5 25 125
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Debugging Loops

Your friend wants to compute the square roots of 1, 4, 9, and 16 using a loop. 
They do not get the answer they expect with the following code.

What is the problem and how can it be fixed?
```python
squares = [1, 4, 9, 16]
for s in squares:
    print("The square root is", squares ** 0.5)
```

:::::::::::::::  solution

## Solution

This code has a common mistake: the iterable (squares) is used in place of the loop variable. While raising a number to the `0.5` power is equivalent to applying the square root of a number, you can't get the square root of a list!


```python
squares = [1, 4, 9, 16]
for square in squares:
    print(square ** 0.5)
```
```output
1.0
2.0
3.0
4.0
```
:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::


## Use `range` to iterate over a sequence of numbers.

- The built-in function [`range`](https://docs.python.org/3/library/stdtypes.html#range) produces a sequence of numbers.
  - *Not* a list: the numbers are produced on demand
    to make looping over large ranges more efficient.
- `range(N)` is the numbers 0..N-1
  - Exactly the legal indices of a list or character string of length N

```python
print('a range is not a list: range(0, 3)')
for number in range(0, 3):
    print(number)
```

```output
a range is not a list: range(0, 3)
0
1
2
```

## The Accumulator pattern turns many values into one.

- A common pattern in programs is to:
  1. Initialize an *accumulator* variable to zero, the empty string, or the empty list.
  2. Update the variable with values from a collection.

```python
# Sum the first 10 integers.
total = 0
for number in range(10):
   total = total + (number + 1)
print(total)
```

```output
55
```

- Read `total = total + (number + 1)` as:
  - Add 1 to the current value of the loop variable `number`.
  - Add that to the current value of the accumulator variable `total`.
  - Assign that to `total`, replacing the current value.
- We have to add `number + 1` because `range` produces 0..9, not 1..10.

:::::::::::::::::::::::::::::::::::::::  challenge

## Classifying Errors

Is an indentation error a syntax error or a runtime error?

:::::::::::::::  solution

## Solution

An IndentationError is a syntax error. Programs with syntax errors cannot be started.
A program with a runtime error will start but an error will be thrown under certain conditions.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Tracing Execution

Create a table showing the numbers of the lines that are executed when this program runs,
and the values of the variables after each line is executed.

```python
total = 0
for char in "tin":
    total = total + 1
```

:::::::::::::::  solution

## Solution

| Line no | Variables            | 
| ------- | -------------------- |
| 1       | total = 0            | 
| 2       | total = 0 char = 't' | 
| 3       | total = 1 char = 't' | 
| 2       | total = 1 char = 'i' | 
| 3       | total = 2 char = 'i' | 
| 2       | total = 2 char = 'n' | 
| 3       | total = 3 char = 'n' | 

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Reversing a String

Fill in the blanks in the program below so that it prints "nit"
(the reverse of the original character string "tin").

```python
original = "tin"
result = ____
for char in original:
    result = ____
print(result)
```

:::::::::::::::  solution

## Solution

```python
original = "tin"
result = ""
for char in original:
    result = char + result
print(result)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Practice Accumulating

Fill in the blanks in each of the programs below
to produce the indicated result.

```python
# Total length of the strings in the list: ["red", "green", "blue"] => 12
total = 0
for word in ["red", "green", "blue"]:
    ____ = ____ + len(word)
print(total)
```

:::::::::::::::  solution

## Solution

```python
total = 0
for word in ["red", "green", "blue"]:
    total = total + len(word)
print(total)
```

:::::::::::::::::::::::::

```python
# List of word lengths: ["red", "green", "blue"] => [3, 5, 4]
lengths = ____
for word in ["red", "green", "blue"]:
    lengths.____(____)
print(lengths)
```

:::::::::::::::  solution

## Solution

```python
lengths = []
for word in ["red", "green", "blue"]:
    lengths.append(len(word))
print(lengths)
```

:::::::::::::::::::::::::

```python
# Concatenate all words: ["red", "green", "blue"] => "redgreenblue"
words = ["red", "green", "blue"]
result = ____
for ____ in ____:
    ____
print(result)
```

:::::::::::::::  solution

## Solution

```python
words = ["red", "green", "blue"]
result = ""
for word in words:
    result = result + word
print(result)
```

:::::::::::::::::::::::::

**Create an acronym:** Starting from the list `["red", "green", "blue"]`, create the acronym `"RGB"` using
a for loop.

**Hint:** You may need to use a string method to properly format the acronym.

:::::::::::::::  solution

## Solution

```python
acronym = ""
for word in ["red", "green", "blue"]:
    acronym = acronym + word[0].upper()
print(acronym)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Cumulative Sum

Reorder and properly indent the lines of code below
so that they print a list with the cumulative sum of data.
The result should be `[1, 3, 5, 10]`.

```python
cumulative.append(total)
for number in data:
cumulative = []
total = total + number
total = 0
print(cumulative)
data = [1,2,2,5]
```

:::::::::::::::  solution

## Solution

```python
total = 0
data = [1,2,2,5]
cumulative = []
for number in data:
    total = total + number
    cumulative.append(total)
print(cumulative)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Identifying Variable Name Errors

1. Read the code below and try to identify what the errors are
  *without* running it.
2. Run the code and read the error message.
  What type of `NameError` do you think this is?
  Is it a string with no quotes, a misspelled variable, or a
  variable that should have been defined but was not?
3. Fix the error.
4. Repeat steps 2 and 3, until you have fixed all the errors.

```python
for number in range(10):
    # use a if the number is a multiple of 3, otherwise use b
    if (Number % 3) == 0:
        message = message + a
    else:
        message = message + "b"
print(message)
```

:::::::::::::::  solution

## Solution

- Python variable names are case sensitive: `number` and `Number` refer to different variables.
- The variable `message` needs to be initialized as an empty string.
- We want to add the string `"a"` to `message`, not the undefined variable `a`.

```python
message = ""
for number in range(10):
    # use a if the number is a multiple of 3, otherwise use b
    if (number % 3) == 0:
        message = message + "a"
    else:
        message = message + "b"
print(message)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Identifying Item Errors

1. Read the code below and try to identify what the errors are
  *without* running it.
2. Run the code, and read the error message. What type of error is it?
3. Fix the error.

```python
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
print('My favorite season is ', seasons[4])
```

:::::::::::::::  solution

## Solution

This list has 4 elements and the index to access the last element in the list is `3`.

```python
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
print('My favorite season is ', seasons[3])
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- A *for loop* executes commands once for each value in a collection.
- A `for` loop is made up of a collection, a loop variable, and a body.
- The first line of the `for` loop must end with a colon, and the body must be indented.
- Indentation is always meaningful in Python.
- Loop variables can be called anything (but it is strongly advised to have a meaningful name to the looping variable).
- The body of a loop can contain many statements.
- Use `range` to iterate over a sequence of numbers.
- The Accumulator pattern turns many values into one.

::::::::::::::::::::::::::::::::::::::::::::::::::


