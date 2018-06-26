# Booleans and logic
* `True` and `False` must be capitalized
* Standard comparisons like `> >= < <= == !=` work as expected but `and`, `or`, and  `not` must be used instead of `&&`, `||`, and `!`

If statement general form
```python
if condtion:
    ...
elif condition:
    ...
else:
    ...
```

Python does not have switch statements but a dictionary can sometimes be used in it's place. _Note: this will only ever match one value._
```python
def f(x):
    return {
        'a': 1,
        'b': 2
    }.get(x, 9)    # 9 is default if x not found
```

# Loops

Regular loop
```python
for item in items:
    print('the current item is ' + item)
    # or for an object
    print('the current key is ' + item)
```

Loop over object keys and values
```python
for key, value in obj.items():
    print('the value of ' + key + ' is ' + value)
```

Loop a number of times
```python
for i in range(0, 10):
    print('the loops has run' + i + 'time(s)')
```

Loop over list with indexes
```python
for i, item in enumerate(items):
    print('the loops has run ' + i + ' time(s)')
    print('the current item is ' + item)
```

While Loop
```python
while condition:
    print('still going...')
```

# Lists (arrays)
* Create: `list = [1, 1, 2, 3]`
* Get first item `list[0]`
* Get last item `list[-1]`
* Slice `list[1:2]`
* Insert and item `list.insert(i, x)`
* Remove an item `list.remove(x)`
* Count occurrences of x `list.count(x)`

## Stack operations
* stack push `list.append(item)`
* stack pop `list.pop(item)`

Python lists shouldn't be used as a queue as they don't have left push or pop methods. The `deque` container is list like with `leftpop()` and `leftappend()` methods. (Obviously `list.insert(0, item)` and `list.remove(0)` can be used in place of left pop and push but it will be worse than (O)n)

# Tuples
Tuples basically are non-mutable lists. Because of this they are also faster than lists. They are create using regular brackets rather than square.

* Create a tuple `hd = (1920, 1080)`

# Dictionaries
Dictionaries are key value store similar to a JSON object, keys must be valid strings, values can be numbers, strings, dictionaries, lists, functions, and more.
```python
example_dict = {
    'name': 'John',
    'hobbies': ['reading', 'dictionaries'],
    'age': 42,
}
```
* Accessing object values `age = example_dict['age']`
* Adding values to an object `example_dict['weight'] = 80`
* Modifying a value `example_dict['age'] = 43`
* Remove a key/value pair `del example_dict['name']`

# Functions
```python
def simple_add_function(x, y):
    """This is the docstring, it breifly explains the function's purpose"""
    return x + y
```
```python
def function_with_default_parameter(username="World"):
    """Greet the user

    If the docstring requires more than one line it should be formatted like this,
    with the first line summarizing the function, a blank line, then more detail.
    """
    return 'Hello, ' + username
```

## Lambda functions
Lambda functions can be use to create anonymous functions that are particularly useful for map, reduce, and filer (below). Instead of
```python
def square(x):
    return x**2

squared_list = map(square, list_to_be_squared)
```
We can just write
```python
squared_list = map(lambda x: x**2, list_to_be_squared)
```

# Map, reduce, and filter
`map` and `filter` are built in, but `reduce` must be imported form `functools`

* `map(function, iterable)` applies the function to each element of the iterable and returns the result
* `filter(function, iterable)` filters out items in the iterable that return false when passed into the function
* `reduce(function, iterable)` needs a function that takes two param, the first is the sum, and the second the current item, it return the first param after the function is applied to each element eg: (reduce also takes an optional 3rd argument for the initial value, default 0)
```python
from functools import reduce

product = reduce(lambda sum, x: sum * x)
```

# List comprehensions
List comprehensions can replace all functionality of map and reduce functions they take the general form
```python
new_list = [ expression for item in items ]
```

They can also be used to filter lists with the optional if and condition
```python
new_list = [ expression for item in items if condition ]
```

Example square all values in a list then filter out values less than 10
```python
initial_list = [0, 1, 2, 3, 4, 5, 6]
squared_list = [ x**2 for x in initial_list ]
filtered_list = [ x for x in squared_list if x > 10 ]
```

# Classes
General form:
```python
class Dog(Animal):
    """The dog class inherits from the animal class"""

    def __init__(self, name):
        self.name = name
    
    def bark(self):
        """Bark and introduce self"""
        print("woof I'm " + self.name)

my_dog = Dog('lucky')
my_dog.bark()
```

# Pip
Pip is the python package manager. Packages are normally installed into a virtual environment (see below) to avoid conflicts between projects.
* Install a package `pip install package-name`
* Create a list of install packages `pip freeze > requirements.txt`
* Install packages from a requirements file `pip install -r requirements.txt`

# VirtualEnv and virtualenvwrapper
Virtualenv creates a folder in you current directory and installs all python packages there to avoid conflicts with other python projects on the same system. This will leave virtualenv folder scattered across the system and may not be desirable. Virtualenvwrapper stores all virtualenvs in you home directory and provides some nicer tools to work with virtualenv.

Virtualenv basic commands
* `virtualenv venv` create a `venv` folder in current directory that will contain all virtualenv files
* `virtualenv -p /usr/bin/python2.7 venv` choose python version for virtualenv (default is 3.6)
* `source venv/bin/activate` activate the virtualenv
* `deactivate` deactivate the virtualenv
* `rm -rf venv` delete the virtualenv

Virtualenvwrapper basic commands
* `mkvirtualenv <env_name>` create a new virtualenv
* `workon <env_name>` switch to `env_name`
* `workon` list available virtualenvs 
* `deactivate` deactivate the virtualenv
* `rmvirtualenv <env_name>` delete the virtualenv