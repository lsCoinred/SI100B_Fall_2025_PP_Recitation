---
title: SI100B_Fall_2025_Recitation_6
separator: <!--s-->
verticalSeparator: <!--v-->
theme: simple
highlightTheme: github
css: assets/custom.css
autoTitlePage: true
makeTitle:
  lecture: SI100B Fall 2025 Recitation 6
  title: HW3；L10 & L11 回顾
  detail: SI100B 2025 Staff | 2025-10-30
makeThanks: true
---

# Homework 3 Preview
<!--v-->
## Homework 3
- 已在 OJ 上发布
- Deadline 2025-11-6 21:15
- The problems should be solved <strong>individually</strong>.
<!--v-->
## Some Tricks
- English written question $\longrightarrow$ online translation.
- Lack of test cases $\longrightarrow$ generate more or get exception from friends or TAs.
- Questions are tooooo long $\longrightarrow$ spend more time on generating ideas than coding.

<!--v-->
## Question 1: **Nested List Flattener**
Implement a function that can flatten nested lists of arbitrary depth into a one-dimensional list.

实现一个函数，该函数可以将任意深度的嵌套列表展平为一维列表。

Implementing recursive algorithms.
实现递归算法
```python
def flatten_nested_list(nested) -> list:
    """
    Flatten a nested list of arbitrary depth into a one-dimensional list.

    Args:
        nested_list (list): A nested list structure that can contain integers, strings, 
                            floats, booleans, or other nested lists

    Returns:
        list: A flattened one-dimensional list whose elements are in the same order 
              as they appear from left to right in the printed original list.
    """
```

<!--v-->
## Question 2: **Sublist Operation**
1. 反转 reverse_sublist
```python
def reverse_sublist(lst, l, r, inplace):
    """
    Reverse the elements in the sublist [l:r] of a list.
    Args:
        lst (list): The input list to be processed.
        l (int): The starting index of the sublist (inclusive).
        r (int): The ending index of the sublist (exclusive).
        inplace (bool): 
            If True, modifies the list in place and returns the same list.  
            If False, returns a new list with the specified sublist reversed.
    Returns:
        list: The list with the specified sublist reversed.
    Raises:
        AssertionError: If l or r is out of range, or if l >= r.
    """
```

<!--v-->
## Question 2: **Sublist Operation**
2. 旋转 rotate_sublist
```python
def rotate_sublist(lst, l, r, k, inplace):
    """
    Rotate the elements in the sublist [l:r] of a list to the left by k positions.
    Args:
        lst (list): The input list to be processed.
        l (int): The starting index of the sublist (inclusive).
        r (int): The ending index of the sublist (exclusive).
        k (int): The number of positions to rotate left. Can be any integer.
        inplace (bool): 
            If True, modifies the list in place and returns the same list.  
            If False, returns a new list with the specified sublist rotated.
    Returns:
        list: The list with the specified sublist rotated left by k positions.
    Raises:
        AssertionError: If l or r is out of range, or if l >= r.
    """
```

<!--v-->
## Question 2: **Sublist Operation**
3. 交换 swap_sublist
```python
def swap_sublist(lst, l1, r1, l2, r2, inplace):
    """
    Swap two sublists [l1:r1] and [l2:r2] of a list.
    Args:
        lst (list): The input list to be processed.
        l1 (int): The starting index of the first sublist (inclusive).
        r1 (int): The ending index of the first sublist (exclusive).
        l2 (int): The starting index of the second sublist (inclusive).
        r2 (int): The ending index of the second sublist (exclusive).
        inplace (bool): 
            If True, modifies the list in place and returns the same list.  
            If False, returns a new list with the specified sublists swapped.
    Returns:
        list: The list with the specified sublists swapped.
    Raises:
        AssertionError: 
            If the sublist indices are out of range, if l1 >= r1 or l2 >= r2,  
            if the two sublists are not of the same length
            or the two sublists overlap.
    """
```
<!--v-->
## Question 3: **Document Keyword**
1. Compute TF (Term Frequency) for each word in a document:
   
$$\text{TF}_{t,d} = \log_{10} \left( \text{count}(t, d) + 1 \right)$$

2. Compute IDF (Inverse Document Frequency) across all documents:
   
$$\text{IDF}_{t} = \log_{10} \left( \dfrac{N}{\text{DF}_{t}}  \right)$$

3. Combine TF and IDF to obtain the TF-IDF score for each word in each document:
   
$$\text{TF-IDF}_{t,d} = \text{TF}_{t,d} \times \text{IDF}_{t} $$

<!--s-->

# Dictionary

<!--v-->
## Basic Concept
A dictionary (dict) in Python is a data structure that stores key–value pairs.

It’s like a real dictionary — you look up a “word” (key) to find its “definition” (value).
```python
# Example
student = {
    "name": "Alice",
    "age": 20,
    "major": "Computer Science"
}
```
Characteristics:
- Keys must be unique and immutable (e.g., string, number, or tuple)
- Values can be of any data type
- Dictionaries are unordered (though in Python 3.7+, they preserve insertion order)
  
<!--v-->
## Common Operations
1. Creating Dictionaries
```python
# Method 1: Using braces
person = {"name": "Bob", "age": 25}

# Method 2: Using dict()
person = dict(name="Bob", age=25)
```

<!--v-->
## Common Operations
2. Accessing and Modifying Elements
```python
print(person["name"])       # Access
person["age"] = 26          # Modify
person["city"] = "Beijing"  # Add new key-value pair
```
✅ Safer way:
```python
print(person.get("gender", "Not specified"))
```

3. Deleting Elements
```python
del person["age"]     # Delete a key
person.pop("city")    # Remove and return a value
person.clear()        # Remove all items
```

<!--v-->
## Common Operations
4. Iterating Over a Dictionary
```python
for key in person:
    print(key, person[key])
# Or use items() to get both keys and values
for key, value in person.items():
    print(f"{key}: {value}")
```

<!--v-->
## Common Operations
5. Merging and Copying
```python
a = {"x": 1, "y": 2}
b = {"y": 3, "z": 4}

a.update(b)   # Merge b into a
print(a)      # {'x': 1, 'y': 3, 'z': 4}
```
```python
c = a.copy()  # Shallow copy

import copy
d = copy.deepcopy(a) # Deep copy
```

<!--v-->
## Useful Tricks
1. Dictionary Comprehension
```python
squares = {x: x**2 for x in range(5)}
print(squares)
# {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

2. Reverse Keys and Values
```python
person = {"Alice": 25, "Bob": 30}
inverted = {v: k for k, v in person.items()}
print(inverted)
# {25: 'Alice', 30: 'Bob'}
```

<!--s-->

# Recursion

<!--v-->
## Definition
Recursion is when a function calls itself to solve a problem by breaking it into smaller subproblems of the same structure.

**Two essential components**:
1. Base case – the simplest form of the problem that can be solved directly (stops recursion).
2. Recursive case – reduces the problem size and calls itself.

<!--v-->
## General Recursion Template
```python
def solve(problem, params...):
    # 1. Base case
    if is_base_case(problem):
        return base_answer

    # 2. Reduce the problem
    subproblems = split(problem)

    # 3. Recursively solve subproblems
    subanswers = [solve(sub, ...) for sub in subproblems]

    # 4. Combine results
    return combine(subanswers)
```

<!--v-->
## Classic Examples
1. Factorial
```python
def fact(n):
    if n <= 1:
        return 1
    return n * fact(n-1)
```
2. Fibonacci
```python
def fib(n):
    if n <= 1:
        return n
    return fib(n-1) + fib(n-2)
```

<!--v-->
## Classic Examples
3. Binary Search
```python
def binary_search(a, target, l=0, r=None):
    if r is None: r = len(a) - 1
    if l > r: return -1
    m = (l + r) // 2
    if a[m] == target: return m
    if a[m] < target:  return binary_search(a, target, m+1, r)
    else:              return binary_search(a, target, l, m-1)
```

<!--v-->
## Common Mistakes
Missing base case $\longrightarrow$ Function never stops

Not reducing problem size $\longrightarrow$ Infinite recursion

<!--s-->

# Class

<!--v-->
## Class
A class is a blueprint or template for creating objects.

It defines what attributes (data) and methods (functions) its objects will have.

```python
class Dog:
    def __init__(self, name, age):
        self.name = name    # Attribute
        self.age = age

    def bark(self):         # Method
        print(f"{self.name} says woof!")
```

<!--v-->
### Object
An object is an instance of a class.

You create an object by “calling” the class.

```python
my_dog = Dog("Buddy", 3)
my_dog.bark()
```

<!--v-->
## The `__init__()` Constructor

`__init__()` is a special method that runs automatically when you create an object.

It initializes the object’s attributes.

## Methods and `self`
`self` represents the instance of the class itself.

All instance methods must include `self` as the first parameter.

<!--v-->
## Inheritance and Method Overriding

A subclass can inherit attributes and methods from its parent class, and it can override them if needed.

```python
class Animal:
    def speak(self):
        print("Some sound")

class Cat(Animal):
    def speak(self):
        print("Meow")

kitty = Cat()
kitty.speak()  # Output: Meow
```

<!--v-->
## Dunder Methods
Dunder methods (short for “double underscore”) are special methods in Python that begin and end with two underscores, like `__init__`, `__str__`, or `__add__`.

They let you customize how objects behave with built-in Python operations:
- Printing (`__str__`)

- Adding (`__add__`)

- Comparing (`__lt__`, `__eq__`)

- Length checking (`__len__`)

- Iteration (`__iter__`, `__next__`)
  
- ...

<!--v-->
## Dunder Methods
```python
class Dog:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return f"Dog named {self.name}"

buddy = Dog("Buddy")
print(buddy)  # Output: Dog named Buddy
```
Here `__str__` defines how the object is represented when printed.
