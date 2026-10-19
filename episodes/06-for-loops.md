---
title: For Loops
teaching: 10
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Explain what a for loop does.
- Correctly write for loops to repeat simple calculations.
- Trace changes to a loop variable as the loop runs.
- Trace changes to other variables as they are updated by a for loop.

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

The loop has three parts: an iterable, a loop variable, and a body that is repeated once for each item in the iterable. The name of a loop variable can be any valid variable name.

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

:::::::::::::::::::::::::::::::::::::::  challenge

## Classifying Errors

Is an indentation error a syntax error or a runtime error?

:::::::::::::::  solution

## Solution

An IndentationError is a syntax error. Programs with syntax errors cannot be started.
A program with a runtime error will start but an error will be thrown under certain conditions.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

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


## The `range()` function iterates over a sequence of numbers.

Use `range()` to iterate over a sequence of numbers.

* The built-in function range produces a sequence of numbers.
* Not a list: the numbers are produced on demand to make looping over large ranges more efficient.
* `range(N)` is the numbers 0..N-1

```python
for i in range(5):
    print(i)
```

```output
0
1
2
3
4
```

The `range()` function is convenient when you want to do an operation a fixed number of times.

```python
housemates = ["joe", "james", "yao"] # Iterated in order
for housemate in range(len(housemates)):
    name = housemates.pop()
    print(name, "moved out")
print(housemates)
```
```output
yao moved out
james moved out
joe moved out
[]
```

The numbers in a range can be adjusted by their *start*, *stop*, and *step* arguments. If a single integer is supplied, it is assumed to be the *stop*. The default value of step is 1, ie. it is incremented by 1.

```python
one_to_five = range(1, 6) # Start at 1, stop before 6 (exclusive)
for num in one_to_five:
    print(num)
```
```output
1
2
3
4
5
```

Set the step parameter to -1 to have the range count down rather than up. The start is still inclusive and the stop is still exclusive.

```python
five_to_one = range(5, 0, -1) # Start at 5 (inclusive), stop at 0 (exclusive), -1 to step
for num in five_to_one:
    print(num)
```
```output
5
4
3
2
1
```

## Programming pattern: accumulation

A common pattern in programs is to:

1. Initialize an accumulator variable to zero, the empty string, or the empty list.
2. Update the variable with values from a collection

Let's say we want to compute the sum of the first five integers starting at 1. You will need to initalize a varable called `total` to 0. This will be our accumulator variable.

```python
# Sum the first 10 integers.
total = 0 # Initialize a variable called sum
for num in range(1, 6):
    print("Total", total)
    print("Adding", num)
    total = total + num # same as total += num
print(total)
```
```output
Total 0
Adding 1
Total 1
Adding 2
Total 3
Adding 3
Total 6
Adding 4
Total 10
Adding 5
15
```

Let's find the total length (in characters) of the strings in the following list: `["red", "green", "blue"]`.

```python
total = 0
for word in ["red", "green", "blue"]:
    total = total + len(word)
print(total)
```
```output
12
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Making an Acronym

Using that same `["red", "green", "blue"]` list, how could we derive the acronym `"rgb"` using
an accumulator pattern?

```python
acronym = _____
for word in ["red", "green", "blue"]:
    acronym = ___________ + ________
print(acronym)
```

:::::::::::::::  solution

## Solution

Instead of accumulating a number starting at 0, accumulate a string one character at a time starting with the empty string.

```python
acronym = ""
for word in ["red", "green", "blue"]:
    acronym = acronym + word[0]
print(acronym)
```

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

## Debugging Accumulators

Let's say you want to compute the **factorial** of 6 or $6!$ by hand. This is equal to 6 * 5 * 4 * 3 * 2 * 1. We can use a for-loop and an accumulator pattern to do this.

Let's say your first draft looks like this. 

```python
accumulator = 0
for i in range(1, 7): # 1 inclusive to 7 exclusive
    print(i)
    accumulator = accumulator * i
print("6! = ", accumulator)
```

Is the answer correct? What needs to be changed about this block of code in order for it to compute $6!$ correctly? 

:::::::::::::::  solution

You're *multiplying* rather than adding. Making your accumulator start at 0 will 0 out your results, as the product of any number * 0 is 0. Therefore, to get the correct result, you want $1 * (6 * 5 * 4 * 3 * 2 * 1)$. Setting accumulator to 1 fixes this.s

## Solution

```python
accumulator = 1
for i in range(1, 7): # 1 inclusive to 7 exclusive
    accumulator = accumulator * i
print("6! = ", accumulator)
```
```output
6! =  720
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- A for loop executes commands once for each value in a collection.
- A for loop is made up of a collection, a loop variable, and a body.
- The first line of the for loop must end with a colon, and the body must be indented.
- Indentation is always meaningful in Python.
- Loop variables can be called anything (but it is strongly advised to have a meaningful name to the looping variable).
- The body of a loop can contain many statements.
- Use range() to iterate over a sequence of numbers.

::::::::::::::::::::::::::::::::::::::::::::::::::


