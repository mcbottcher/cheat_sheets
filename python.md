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



