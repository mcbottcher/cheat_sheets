# Python

## Lambda

- `lambda <arguments> : <expression>`: Small anonymous function
- Can only have one expression, can take multiple arguments

```python
func = lambda a : a + 10
print(func(1)) # Will output 11
``` 

- Can also be used inside another function

```python
def myfunc(n):
  return lambda a : a * n

# function to double input
mydoubler = myfunc(2)
# function to triple input
mytripler = myfunc(3)

print(mydoubler(11))
print(mytripler(11))
```

## Map

- `map(func, iter)`: Applies func to each element of iterable
- Returns a map object, need to covert to another type to view, e.g. list()
- map object is an iterator -> it doesn't store the new data, just how to data is mapped, so when extracting a value it will map the value on the fly

```python
def func(a):
  return a+10
  
# prints [11, 12, 13]
print(list(map(func, [1,2,3])))

```

- Can also use with Lambda function

```python
print(list(map(lambda a:a+10, [1,2,3])))
```

## Filter

- `filter(func, iter)`: Added each element of iterable to new iterable if func returns true

```python
def func(a):
  return a != 0
  
# prints [1, 2]
print(list(filter(func, [0, 1, 2])))
```

- Also used with lambda

```python
print(list(filter(lambda a:a!=0, [0, 1, 2])))
```

## Set

- Set is a collection which is unordered, unchangable (can remove and add items still), and unindexed
- `my_set = {"banana", "apple", "cherry"}`
- Sets cannot have duplicate entries -> they will be ignored if there is a duplicate
- Can also use the `set()` object: `my_set = set(("banana", "apple", 2, True))`

## String formatting

- `print(f"Hello {my_string}")`

## Checking for a type

- Use `isinstance(object, class_type)`
- Don't use `==`

## Equality vs Identity

- `is` checks that two variables point to the same object in memory
  - Use `is` when checking for `None True False` -> `if my_var is None:`
- `==` or `!=` check that the value of two objects are the same

## Range Length Looping

- Better to NOT use something like `for i in range(len(a))`
- Instead use `for v in a:` or similar
- If you need the index, you can use enumerate to get the element and the index at the same time:

```python
a = [1, 2, 3]
for index, element in enumerate(a):
  ...
```

## Zip

- Returns a zip object, which is an iterator of tuples
- Each tuple contains the elements from the same index in the given input iterators
- If given input iterators have different lengths, zip iterator will be of length of the shortest input iterator
- Cannot be accessed with indexes so need to covert to a list or similar, or use in a loop

```python
a = ("John", "Charles", "Mike")
b = ("Jenny", "Christy", "Monica")

x = zip(a, b)

for av, bv in x:
  ...
```

## Timing code

- Use `time.perf_counter()` to time code

```python
start = time.perf_counter()
...
end = time.perf_counter()
print(end - start)
```

## Logging

- Use logging instead of print statements for debug
- Can use different levels of log, and your own formatting

```python
def my_func():
  logging.debug("debug info")
  logging.info("general info")
  logging.error("not good")

def main():
  level = logging.DEBUG
  fmt = '[%(levelname)s] %(asctime)s - %(message)s'
  logging.basicConfig(level=level, format=fmt)
```

## Exceptions

```python
try:
  ...
except FileNotFoundError:
  ...
except Exception as e:
  print(e)
```

- Used to handle errors in pieces of code you think an error could occur in
- Can use multiple except statements to catch different errors -> put more generic ones like `Exception` towards the bottom
- use the `else` to run code if the try block finishes without raising and exception
- use `finally` to run if code is successful or if exception is thrown

```python
try:
  ...
except FileNotFoundError:
  ...
else:
  print('Try succeeded')
finally:
  print('This always runs')
```

- Raise your own exceptions: `raise Exception`

```python
class MyCustomError(Exception):
  pass

try:
  if 1 == 2:
    raise MyCustomError
except MyCustomError:
  print('My custom exception was triggered')
```

## List comprehension

- Create a new list where each element which passes a filter is altered by a function

```python
nums = [1, 2, 3, 4]
# For all elements in nums which are even, double them and put them in my_list
my_list = [x*2 for x in nums if x%2 == 0]

# my_list = [4, 8]
```

## Iterator

- e.g. `map()`
- A type that allows iteration but doesn't store any raw data
- Iterator stores where in sequence you are:

```python
x = [1, 2, 3, 4, 5]
y = map(lambda i: i*2, x)

# can also use y.__next__()
next(y)

# This loop will start at second iteration of y .i.e. 2*2 = 4
for i in y:
  print(y)
```

- use `iter()` to make an iterator e.g.: `x = iter(range(1, 11))`
- Exception `StopIterator` will stop an interator -> how a for loop stops for example

## Generator

```python
def generator(n):
  for i in range(n):
    # pauses function and returns i to the calling function
    yield i

for i in gen(5):
  print(i)
```
- Yield pauses function, saves context of function, uses the value, then comes back to continue the function
- Could also implement like this, remembering yield pauses then continues

```python
def gen():
  yield 1
  yield 2
  yield 3

for i in gen():
  # prints 1, 2, 3
  print(i)
```

- Can also use generator comprehensions

```python
gen = (i for i in range(10) if i%2)

for i in gen:
  # prints 1, 3, 5, 7, 9
  print(gen)
```