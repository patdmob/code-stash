# Python Code Stash



```python
register_1 = []
register_2 = []

def register_function(register_type="first"):
    """
    A function register decorator that accepts an
    argument to specify which register to use. The
    register is a list of function calls.

    >>> @register_function("second")
    >>> def some_func(a,b):
    >>>     return a + b
    >>> register_2
    [<function __main__.some_func(a,b)>]
    """
    def inner_decorator(f):
        if register_type == "first":
            register_1.append(f)
        elif register_type == "second":
            register_2.append(f)
        else:
            raise TypeError(f"register_type must be either 'first' or 'second', not '{register_type}'")
        return f
    return inner_decorator

```

```python
def list_closure():
    """
    A closure containing a list 

    >>> list_reg = list_closure()
    >>> list_reg("test")
    ['test']
    >>> list_reg("test2")
    ['test', 'test2']
    >>> list_reg()
    ['test', 'test2']
    """
    data =  []
    def closure(*args):
        # nonlocal data # only needed for immutable data types
        if args:
            data.append(args[0])
        return data
    return closure

```


```python
def counter_closure():
    """
    A closure used to count each time called  

    >>> counter = counter_closure()
    >>> counter()
    1
    >>> counter()
    2
    """
    counter = 0
    def closure():
        nonlocal counter # only needed for immutable data types
        counter += 1
        return counter
    return closure

```
