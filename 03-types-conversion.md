---
title: Data Types and Type Conversion
teaching: 15
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Explain key differences between integers and floating point numbers.
- Explain key differences between numbers and character strings.
- Use built-in functions to convert between integers, floating point numbers, and strings.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- What kinds of data do programs store?
- How can I convert one type to another?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Every value has a type.

Every value in a program has a specific type.

We're going to start with three basic data types in Python:

- [Integers](https://en.wikipedia.org/wiki/Integer) represent positive or negative whole numbers like `3` or `-512`.
- [Floats](https://en.wikipedia.org/wiki/Floating-point_arithmetic) represents real numbers like `3.14159` or `-2.5`.
- [Strings](https://en.wikipedia.org/wiki/String_(computer_science)) represent text.
  * Strings can be wrapped in single quotes or double quotes so `"Ducks"` and `'Ducks'` are equally valid.

## Use the built-in function `type` to find the type of a value.

Use the built-in function `type` to find out what type a value or variables has. Remember, 
the *value* has the type and the *variable* is just a label.

```python
print(type(52))
```

```output
<class 'int'>
```

```python
fitness = 'average'
print(type(fitness))
```

```output
<class 'str'>
```

## Data types control what operations can be performed on a given value.

A value's type determines what the program can do to it.

```python
print(5 - 3)
```

```output
2
```

```python
print('hello' - 'h')
```

```error
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-2-67f5626a1e07> in <module>()
----> 1 print('hello' - 'h')

TypeError: unsupported operand type(s) for -: 'str' and 'str'
```

## You can use the "+" and "\*" operators on strings.

- "Adding" character strings concatenates them.

```python
full_name = 'Ahmed' + ' ' + 'Walsh'
print(full_name)
```

```output
Ahmed Walsh
```

Multiplying a character string by an integer *N* creates a new string that consists of that character string repeated  *N* times because multiplication is repeated addition.

```python
separator = '=' * 10
print(separator)
```

```output
==========
```

## Strings have a length (but numbers don't).

The built-in function `len` counts the number of characters in a string.

```python
print(len("Cat"))
```

```output
3
```

But numbers don't have a length.

```python
print(len(52))
```

```error
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-3-f769e8e8097d> in <module>()
----> 1 print(len(52))

TypeError: object of type 'int' has no len()
```

## You Must Convert Numbers to Strings and Vice-Versa to Use Them Together

You cannot add numbers and strings.

```python
print(1 + '2')
```

```error
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-4-fe4f54a023c6> in <module>()
----> 1 print(1 + '2')

TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

This is not allowed because it's ambiguous: should `1 + '2'` be `3` or `'12'`?

Some types can be converted to other types by using the type name as a function.

```python
print(1 + int('2'))
print(str(1) + '2')
```

```output
3
12
```

## Can mix integers and floats freely in operations.

Integers and floating-point numbers can be mixed in arithmetic.

```python
print('half is', 1 / 2.0)
print('three squared is', 3.0 ** 2)
```

```output
half is 0.5
three squared is 9.0
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Automatic Type Conversion

What type of value is 3.25 + 4?

:::::::::::::::  solution

## Solution

It is a float: integers are automatically converted to floats as necessary.

```python
result = 3.25 + 4
print(result, 'is', type(result))
```

```output
7.25 is <class 'float'>
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Use an index to get a character from a string.

- The characters (individual letters, numbers, and so on) in a string are
  ordered. For example, the string `'AB'` is not the same as `'BA'`. Because of
  this ordering, we can treat the string as a list of characters.
- Each position in the string (first, second, etc.) is given a number. This
  number is called an **index**.
- Indices are numbered starting from 0.
- Use the position's index in square brackets to get the character at that
  position.

![A line of Python code, print(atom\_name[0]), demonstrates that using the zero index will output just the initial letter, in this case 'h' for helium.](fig/2_indexing.svg)

```python
atom_name = 'helium'
print(atom_name[0])
```

```output
h
```

## Use a slice to get a substring.

- A part of a string is called a **substring**. A substring can be as short as a
  single character.
- A slice is a part of a string (or, more generally, a part of any list-like thing).
- We take a slice with the notation `[start:stop]`, where `start` is the integer
  index of the first element we want and `stop` is the integer index of
  the element *just after* the last element we want.
- Taking a slice does not change the contents of the original string. Slicing returns a copy of part of the original string.

```python
atom_name = 'sodium'
print(atom_name[0:3])
```

```output
sod
```

## Use the built-in function `len` to find the length of a string.

```python
print(len('helium'))
```

```output
6
```

Nested functions are evaluated from the inside out, like in mathematics.


:::::::::::::::::::::::::::::::::::::::  challenge

## Challenge

If you assign `a = 123`,
what happens if you try to get the second digit of `a` via `a[1]`?

:::::::::::::::  solution

## Solution

Python will raise an error if you try to perform an index operation on a
number.

If you want the Nth digit of a number you can convert it into a string using the `str` function.

```python
a = 123
print(a[1])
```

```error
TypeError: 'int' object is not subscriptable
```

```python
a = str(123)
print(a[1])
```

```output
2
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Slicing practice

What does the following program print?

```python
atom_name = 'carbon'
print('atom_name[1:3] is:', atom_name[1:3])
```

:::::::::::::::  solution

## Solution

```output
atom_name[1:3] is: ar
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Variables only change when something is assigned to them.

```python
v1 = 1
v2 = 5 * v1
v1 = 2
print('first is', v1, 'and second is', v2)
```

```output
first is 2 and second is 5
```

- The computer reads the value of `v1` when doing the multiplication,
  creates a new value, and assigns it to `v2`.
- Afterwards, the value of `v1` is set to the new value and *not dependent on `variable_one`* so its value
  does not automatically change when `v2` changes.

:::::::::::::::::::::::::::::::::::::::  challenge

## Fractions

What type of value is 3.4?
How can you find out?

:::::::::::::::  solution

## Solution

It is a floating-point number (often abbreviated "float").
It is possible to find out by using the built-in function `type()`.

```python
print(type(3.4))
```

```output
<class 'float'>
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Choose a Type

What type of value (integer, floating point number, or character string)
would you use to represent each of the following?  Try to come up with more than one good answer for each problem.  For example, in  # 1, when would counting days with a floating point variable make more sense than using an integer?

1. Number of days since the start of the year.
2. Serial number of a piece of lab equipment.
3. Current population of a city.
4. Average height of a group of students.

:::::::::::::::  solution

## Solution

The answers to the questions are:

1. Integer, since the number of days would lie between 1 and 365.
2. A string because a serial number typically contains letters and numbers.
3. I would use an integer to represent population in units of individuals.
4. Floating point number, since an average is likely to have a fractional part.
  

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Division Types

In Python 3, the `//` operator performs integer (whole-number) floor division, the `/` operator performs floating-point
division, and the `%` (or *modulo*) operator calculates and returns the remainder from integer division:

```python
print('5 // 3:', 5 // 3)
print('5 / 3:', 5 / 3)
print('5 % 3:', 5 % 3)
```

```output
5 // 3: 1
5 / 3: 1.6666666666666667
5 % 3: 2
```

Decide between the division types above for the following questions, then compute the answers in Python.

1. The number of *whole* weeks per year given 365 days per year and 7 days per week.
2. The average number of people per park in Eugene, OR given 179000 people and 135 parks.
3. The number of leftover hats given 12 hats distributed evenly among 10 volunteers.

```python
weeks_per_year = 
people_per_park = 
leftover_hats = 
print(weeks_per_year, people_per_park, leftover_hats)
```

:::::::::::::::  solution

## Solution

1. This requires *floor* division, because you don't care about partial weeks.
2. This requires *float* division, because you want to preserve the decimal in an average.
3. This requires the remainder, because you want the number of hats remaining after one hat is given out per person.

```python
weeks_per_year = 365 // 7
people_per_park = 179000 / 135
leftover_hats = 12 % 10

print(weeks_per_year, people_per_park, leftover_hats)
```

```output
52 1325.9259259259259 2
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Strings to Numbers

Where reasonable, `float()` will convert a string to a floating point number,
and `int()` will convert a floating point number to an integer:

```python
print("string to float:", float("3.4"))
print("float to int:", int(3.4))
```

```output
string to float: 3.4
float to int: 3
```

If the conversion doesn't make sense, however, an error message will occur.

```python
print("string to float:", float("Hello world!"))
```

```error
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-5-df3b790bf0a2> in <module>
----> 1 print("string to float:", float("Hello world!"))

ValueError: could not convert string to float: 'Hello world!'
```

Given this information, what do you expect the following program to do?

What does it actually do?

Why do you think it does that?

```python
print("fractional string to int:", int("3.4"))
```

:::::::::::::::  solution

## Solution

What do you expect this program to do? It would not be so unreasonable to expect the Python 3 `int` command to
convert the string "3.4" to 3.4 and an additional type conversion to 3. After all, Python 3 performs a lot of other
magic - isn't that part of its charm?

```python
int("3.4")
```

```output
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-2-ec6729dfccdc> in <module>
----> 1 int("3.4")
ValueError: invalid literal for int() with base 10: '3.4'
```

However, Python 3 throws an error. Why? To be consistent, possibly. If you ask Python to perform two consecutive
typecasts, you must convert it explicitly in code.

```python
int(float("3.4"))
```

```output
3
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Arithmetic with Different Types

Which of the following will return the floating point number `2.0`?
Note: there may be more than one right answer.

```python
first = 1.0
second = "1"
third = "1.1"
```

1. `first + float(second)`
2. `float(second) + float(third)`
3. `first + int(third)`
4. `first + int(float(third))`
5. `int(first) + int(float(third))`
6. `2.0 * second`

:::::::::::::::  solution

## Solution

Answer: 1 and 4


:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Slicing concepts

Given the following string:

```python
species_name = "Acacia buxifolia"
```

What would these expressions return?

1. `species_name[2:8]`
2. `species_name[11:]` (without a value after the colon)
3. `species_name[:4]` (without a value before the colon)
4. `species_name[:]` (just a colon)
5. `species_name[11:-3]`
6. `species_name[-5:-3]`
7. What happens when you choose a `stop` value which is out of range? (i.e., try `species_name[0:20]` or `species_name[:103]`)

:::::::::::::::  solution

## Solutions

1. `species_name[2:8]` returns the substring `'acia b'`
2. `species_name[11:]` returns the substring `'folia'`, from position 11 until the end
3. `species_name[:4]` returns the substring `'Acac'`, from the start up to but not including position 4
4. `species_name[:]` returns the entire string `'Acacia buxifolia'`
5. `species_name[11:-3]` returns the substring `'fo'`, from the 11th position to the third last position
6. `species_name[-5:-3]` also returns the substring `'fo'`, from the fifth last position to the third last
7. If a part of the slice is out of range, the operation does not fail. `species_name[0:20]` gives the same result as `species_name[0:]`, and `species_name[:103]` gives the same result as `species_name[:]`
  
  
:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Every value has a type.
- Use the built-in function `type` to find the type of a value.
- Types control what operations can be done on values.
- Strings can be added and mulitiplied.
- Strings have a length (but numbers don't).
- Use an index to get a single character from a string.
- Use a slice to get a substring.
- Use the built-in function `len` to find the length of a string.
- Must convert numbers to strings or vice versa when operating on them.
- Can mix integers and floats freely in operations.
- Variables only change value when something is assigned to them.

::::::::::::::::::::::::::::::::::::::::::::::::::


