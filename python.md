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

