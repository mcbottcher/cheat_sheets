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


