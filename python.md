# Python

## Lambda

- `lambda <arguments> : <expression>`: Small anonymous function
- Can only have one expression, can take multiple arguments

```
func = lambda a : a + 10
print(func(1)) # Will output 11
``` 

- Can also be used inside another function

```
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

```
def func(a):
  return a+10
  
# prints [11, 12, 13]
print(list(map(func, [1,2,3])))

```

- Can also use with Lambda function

`print(list(map(lambda a:a+10, [1,2,3])))`

