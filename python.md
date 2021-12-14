# Python Code Stash


You can use registers if you have an undeterminable list
of functions to run. This cuts down on updating code in multiple
places.

```python
register_1 = []
register_2 = []

def register_function_decorator(register_type="first"):
    """
    A function register decorator that accepts an
    argument to specify which register to use. The
    register is a list of function calls.

    >>> @register_function("second")
    >>> def some_func(a,b):
    ...`     return a + b
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
Example of using dictionaries as case statements or to replace if/else logic. You can think of extended if elif elif elif else statements as a conditional mapping. Dictionaries can do this mapping faster? and is more easily understood More complex expressions/logic can be evaluated outside of the dictionary and condensed into a label. 

```python



def get_group_label(str_for_hash: str) -> str:
    """
    Takes a string and returns a treatment/control
    group label for experimentation.
    """
    from hashlib import md5
    hash_mod_100 = int(md5(str_for_hash.encode("utf-8")).hexdigest(), 16) % 100

    group_definitions = dict(
        control=range(10),
        treatment_a=range(10, 100),
    )

    group = [k for k, v in group_definitions.items() if hash_mod_100 in v]

    return group[0] if len(group) != 0 else None


```





```python


class StopWatch:
    """
    A timer instance which calculates the running mean and
    variance of tdelta. 

    https://www.johndcook.com/blog/standard_deviation/

    Instantiating the object starts the timer. split() adds
    a lap and calculates the running mean and standard 
    deviation for that split. stop() ends the count and
    displays the total time, mean, and standard deviation.
    """
    
    def __init__(self):
        self.start = datetime.now()
        self.iteration_time = datetime.now()
        self.mu = 0.0
        self.var = 0.0
        self.n = 1
        self.end = None

    def split(self):
        self.end = datetime.now()
        tdelta = self.end - self.iteration_time
        print(f"Time Delta (seconds): {tdelta.total_seconds(): <6.3f}") 
 
        mu_new = self.mu + (tdelta.total_seconds() - self.mu)/self.n if self.mu != 0.0 else tdelta.total_seconds()
        self.var = self.var + ((tdelta.total_seconds() - self.mu)*(tdelta.total_seconds() - mu_new))
        self.mu = mu_new
        print(f"Mean (seconds): {mu_new: <8.3f}\nStandard Deviation (seconds): {math.sqrt(self.var/(self.n - 1)) if self.n != 1 else 0.0: <8.3f}")

        self.iteration_time = datetime.now()
        self.n += 1

    def stop(self):
        self.end = datetime.now()
        print(f"\nTotal Time (seconds): {(self.end - self.start).total_seconds(): <8.3f}\nMean (seconds): {self.mu: <8.3f}\nStandard Deviation (seconds): {math.sqrt(self.var/(self.n - 1))  if self.n != 1 else 0.0: <8.3f}")
```
