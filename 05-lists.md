---
title: Lists
teaching: 20
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Explain what a Python list is.
- Explain why programs need collections of values.
- Write programs that create lists, index them, slice them, and modify them.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I store multiple values in one object.

::::::::::::::::::::::::::::::::::::::::::::::::::

##  Lists stores values of any type

A *list* stores multiple values in one object, in a specific order. Values in a list can be called "elements" or "items".

A list is represented by comma-separated items enclosed in `[]`.

```python
first_list = ["my", "first", "list"]
print(first_list)
```
```output
['my', 'first', 'list']
```

Items in a list do not have to be of the same type.

```python
lucky_numbers = ["15", 31, 12.0]
print(lucky_numbers)
```
```output
['15', 31, 12.0]
```

Use `len` to find out how many values are in a list.

```python
print(len(first_list))
```
```output
3
```

## Lists are indexed like strings

Just like strings, lists are indexed from 0 to n-1, where n is the length of the list. Use [] to select indexed values. 

```python
alphabet = "abcde"
words = ["apple", "boy", "camel", "dog"]

print(alphabet[1])
print(words[1])
```

```output
b
boy
```

Make sure you check the length of a list before indexing into it. As with strings, indexing into a value that doesn't exist (because the list is too short) causes an IndexError.

```python
words[5] # This will fail
```
```output
IndexError                                Traceback (most recent call last)
Cell In[80], line 1
----> 1 words[5]

IndexError: list index out of range
```

You can also use the same syntax `[start:stop]` you used to express slices for strings with lists.

```python
print(words[:2])
```
```output
['apple', 'boy']
```

:::::::::::::::::::::::::::::::::::::::  challenge

## List Indexing, String Indexing

How would I get a slice of a specific *character* in a specific item in `words`? Let's say I want to get a substring containing the letter `y` in `boy`.

```python
words = ["apple", "boy", "camel", "dog"]
print(words_____) # Add indexing here
```

:::::::::::::::  solution

## Solution
You can accomplish this by indexing into the second item in words `[1]` and indexing into the third character of that `[2]`. 

Nested indexing is read from left to right, starting from the outermost
collection.
```python
words[1][2]
```
```output
'y'
```
:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Values in lists can be reassigned

Use indexing on the left side of an assignment statement to replace a value inside a list.

Lists are **mutable**: they can be changed after they are instantiated. 

```python
pressures = [0.273, 0.275, 0.277, 0.275, 0.276]
pressures[0] = 0.26
print('Pressures is now:', pressures)
```
```output
pressures is now: [0.265, 0.275, 0.277, 0.275, 0.276]
```

## The append method adds items to the end of a list

Use the `.append` method to add items to the end of a list. 

```python
primes = [2, 3, 5]
print('primes is initially:', primes)
primes.append(7)
print('primes has become:', primes)
```
```output
primes is initially: [2, 3, 5]
primes has become: [2, 3, 5, 7]
```

The `.append()` method returns None and modifies the list in place. That is, it directly modifies the list
that calls the method rather than returning a copy.

This is an intentional design choice.

```python
returned_by_append = primes.append(11) # Append 11 but return None
print(returned_by_append)
print(primes)
```
```output
None
[2, 3, 5, 7, 11]
```

## Extending a list concatenates two lists together

Use the .extend() method to add a list passed in as an argument to the *end* of that list.

```python
housemates = ["dave", "rose"]
guests = ["bob", "yao", "sam"]
guests.extend(housemates) # Also modifies in place
print("The following people will be at my party", guests)
print("There are", len(guests), "guests")
```
```output
The following people will be at my party ['bob', 'yao', 'sam', 'dave', 'rose']
There are 5 guests
```

Appending a list to a list creates a nested list: a list inside of a list.
```python
ml = [1, "dog", "antelope"]
ml2 = [2, 2, 3]
ml.append(ml2)
print(ml)
```
```output
[1, 'dog', 'antelope', [2, 2, 3]]
```

## The empty list contains no values.
We don't have to create lists with items already in them. The empty list `[]` is a list with length 0. 

```python
x = []
len(x)
```
```output
0
```
You can think of it as "the zero of lists."

The empty list is useful because we can add items to it using methods like .`append()` and `.extend()`.

```python
x.append(4)
x.append(5)
print(x)
```
```output
[4, 5]
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Append or Extend?

Can you make `z` into `[1, 2, 3, 4, 5]` using `.append()`? How about with `.extend()`?
```python
z = [1, 2, 3]
```

:::::::::::::::  solution

## Solution

We can append 4, then 5.
```python
z = [1, 2, 3]
z.append(4)
z.append(5)
print(z)
```
```output
[1, 2, 3, 4, 5]
```

Or we can extend the list with `[4, 5]`.
```python
z = [1, 2, 3] # Reset z
z.extend([4,5])
print(z)
```
```output
[1, 2, 3, 4, 5]
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Inserting into list with `.insert()`
So far, we've looked at methods that modify the *end* of a list. 

The method **.insert(i, x)** inserts item `x` before the item at position `i`.

```python
alpha = ["apple", "berry", "durian"]
alpha.insert(2, "cherry") # Before the item at index 2 ("durian") 
print(alpha)
```
```output
['apple', 'berry', 'cherry', 'durian']
```

## Removing items from lists: del, .remove(), and .pop()

We use `del list_name[index]` to remove an element from a list.
- `del` is not a function or a method, but a statement in the language.

```python
primes = [2, 3, 5, 7, 9]
print('primes before removing', primes)
del primes[4]
print('primes after removing', primes)
```
```output
primes before removing: [2, 3, 5, 7, 9]
primes after removing: [2, 3, 5, 7]
```

However, it is more common to see items removed from lists using the `.remove()` and `.pop()` methods.
`.remove(x)` will remove the first instance of value(x) from a list. Like `.append()`, the `.remove()`
function returns None.

```python
housemates = ["rose", "sam"] 
housemates.remove("rose") 
housemates
```
```output
['sam']
```

It will return a ValueError if there are no instances of x in the list.
Now that "rose" has already moved out, `.remove()` will fail because 
it cannot find a "rose" in the list to remove.


```python
housemates.remove("rose") # This will fail
```
```output
----> 1 housemates.remove("rose")

ValueError: list.remove(x): x not in list
```

Let's say two new housemates move in: "josh" and "joe". 

```python
housemates.append("josh")
housemates.append("joe")
print("There are now", len(housemates), "people in the house.")
```

The landlord imposes a new rule. Only two people are allowed in the house.
The person who moved in most recently (the end of the list) must move out. 

We can use the `.pop()` method to remove (and return) the last item in a list. 

```python
evicted = housemates.pop() # Removes and returns the last item in a list
print(evicted, "was evicted.")
print(housemates, "live in the house")
```
output```
joe was evicted.
['sam', 'josh'] live in the house
```

You cannot `.pop()` values from an empty list.

```python
empty_house = []
empty_house.pop() # This will fails
```
```output
IndexError                                Traceback (most recent call last)
Cell In[23], line 2
      1 empty_house = []
----> 2 empty_house.pop()

IndexError: pop from empty list
```


## Character strings are immutable.

We cannot change the characters in a string after it has been created because Python considers the string to be a single *primitive* value.

Primitives (strings, ints, floats, booleans) are **immutable**. This means that when we want to change the value of a string or number variable, we can only replace the old value with a completely new value.

```python
element = "Helium"
element[0] = 'C'
```

```error
TypeError: 'str' object does not support item assignment
```

Lists and character strings are both *collections*. 


## Mutable and immutable objects: when a copy isn't a copy
Be careful when modifying data in-place. 
If two variables refer to the same list, and you modify the list value, it will change for both variables!

This has to do with the mechanics of assignment and mutability in Python.

```python
x = [1, 3]
y = x # y points to x
x.append(5)
print(x)
print("y", y, "is another name for x")
```
```output
[1, 3, 5]
y [1, 3, 5] is another name for x
```

If you wish to make two copies of the same list, use the `.copy()` method instead.
This method returns a new list with the same contents. This principle applies for all *mutable* variables. (We'll learn about another mutable
data type---the DataFrame---later in this workshop.)

```python
x = [1, 3]
y = x.copy() # Y points to a different, mutable list
x.append(5)
print("x", x)
print("y", y, "hasn't changed.")
```
```output
x [1, 3, 5]
y [1, 3] hasn't changed.
```

For additional reading on this topic, see this question from the [official Python FAQ](https://docs.python.org/3/faq/programming.html#why-did-changing-list-y-also-change-list-x).


## Two ways of sorting lists
There are two common ways to sort lists by their values: 
the sorted() function which returns a sorted collection as a copy and .sort() method which sorts a list in place.

```python
numbers = [1, 5, 3, 4, 2]
snumbers = sorted(numbers) # Returns a copy
print(numbers) # Unchanged
print(snumbers)
```
```output
[1, 5, 3, 4, 2]
[1, 2, 3, 4, 5]
```

Notice that the `.sort()` method returns `None` and permanently changes `numbers`.
```python
print("Numbers before .sort()", numbers)
numbers.sort() # Permanently changes numbers
print("Numbers after", numbers)
```
```output
Numbers before .sort() [1, 5, 3, 4, 2]
Numbers after [1, 2, 3, 4, 5]
```

However, sorting a list only works when all its values are of the same data type. Remember those rules about comparing items of different types
with `min()` and `max()`?

```python
valid_list = ["a", 3, [1]] # This will work
```
```python
valid_list.sort()
```
```output
TypeError                                 Traceback (most recent call last)
Cell In[27], line 1
----> 1 valid_list.sort()

TypeError: '<' not supported between instances of 'int' and 'str'
```


:::::::::::::::::::::::::::::::::::::::  challenge

## Fill in the Blanks

Fill in the blanks so that the program below produces the output shown.

```python
values = ____
values.____(1)
values.____(3)
values.____(5)
print('first time:', values)
values = values[____]
print('second time:', values)
```

```output
first time: [1, 3, 5]
second time: [3, 5]
```

:::::::::::::::  solution

## Solution

```python
values = []
values.append(1)
values.append(3)
values.append(5)
print('first time:', values)
values = values[1:]
print('second time:', values)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## How Large is a Slice?

If `start` and `stop` are both non-negative integers,
how long is the list `values[start:stop]`?

:::::::::::::::  solution

## Solution

The list `values[start:stop]` has up to `stop - start` elements.  For example,
`values[1:4]` has the 3 elements `values[1]`, `values[2]`, and `values[3]`.
Why 'up to'? As we saw in [episode 2](02-variables.md),
if `stop` is greater than the total length of the list `values`,
we will still get a list back but it will be shorter than expected.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## From Strings to Lists and Back

Given this:

```python
print('string to list:', list('tin'))
print('list to string:', ''.join(['g', 'o', 'l', 'd']))
```

```output
string to list: ['t', 'i', 'n']
list to string: gold
```

1. What does `list('some string')` do?
2. What does `'-'.join(['x', 'y', 'z'])` generate?

:::::::::::::::  solution

## Solution

1. [`list('some string')`](https://docs.python.org/3/library/stdtypes.html#list) converts a string into a list containing all of its characters.
2. [`join`](https://docs.python.org/3/library/stdtypes.html#str.join) returns a string that is the *concatenation*
  of each string element in the list and adds the separator between each element in the list. This results in
  `x-y-z`. The separator between the elements is the string that provides this method.
  
  

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Working With the End

What does the following program print?

```python
element = 'helium'
print(element[-1])
```

1. How does Python interpret a negative index?
2. If a list or string has N elements,
  what is the most negative index that can safely be used with it,
  and what location does that index represent?
3. If `values` is a list, what does `del values[-1]` do?
4. How can you display all elements but the last one without changing `values`?
  (Hint: you will need to combine slicing and negative indexing.)

:::::::::::::::  solution

## Solution

The program prints `m`.

1. Python interprets a negative index as starting from the end (as opposed to
  starting from the beginning).  The last element is `-1`.
2. The last index that can safely be used with a list of N elements is element
  `-N`, which represents the first element.
3. `del values[-1]` removes the last element from the list.
4. `values[:-1]`
  
  

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::   

:::::::::::::::::::::::::::::::::::::::  challenge

## Slice Bounds

What does the following program print?

```python
element = 'lithium'
print(element[0:20])
print(element[-1:3])
```

:::::::::::::::  solution

## Solution

```output
lithium

```

The first statement prints the whole string, since the slice goes beyond the total length of the string.
The second statement returns an empty string, because the slice goes "out of bounds" of the string.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Sort and Sorted

What do these two programs print?
In simple terms, explain the difference between `sorted(letters)` and `letters.sort()`.

```python
# Program A
letters = list('gold')
result = sorted(letters)
print('letters is', letters, 'and result is', result)
```

```python
# Program B
letters = list('gold')
result = letters.sort()
print('letters is', letters, 'and result is', result)
```

:::::::::::::::  solution

## Solution

Program A prints

```output
letters is ['g', 'o', 'l', 'd'] and result is ['d', 'g', 'l', 'o']
```

Program B prints

```output
letters is ['d', 'g', 'l', 'o'] and result is None
```

`sorted(letters)` returns a sorted copy of the list `letters` (the original
list `letters` remains unchanged), while `letters.sort()` sorts the list
`letters` in-place and does not return anything.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- A list stores many values in a single structure.
- Use an item's index to fetch it from a list.
- Lists' values can be replaced by assigning to them.
- Appending items to a list lengthens it.
- Use `del` to remove items from a list entirely.
- The empty list contains no values.
- Lists may contain values of different types.
- Character strings can be indexed like lists.
- Character strings are immutable.
- Indexing beyond the end of the collection is an error.

::::::::::::::::::::::::::::::::::::::::::::::::::


