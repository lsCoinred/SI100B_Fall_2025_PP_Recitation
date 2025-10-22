---
title: SI100B_Fall_2025_Recitation_5
separator: <!--s-->
verticalSeparator: <!--v-->
theme: simple
highlightTheme: github
css: assets/custom.css
autoTitlePage: true # 一级标题 `#` 开头的将自动居中并占满一页
makeTitle: # 制作封面页
    lecture: SI100B Fall 2025 Recitation 4
    title: L9 & L10 回顾
    detail: SI100B 2025 Staff | 2025-10-24
makeThanks: true # 制作结尾页
---

# Exceptions
<!--v-->
## Exceptions

When the programme crash inevitably, it throws an Exception.
```python
def cause_memory_error():
    """Create huge lists until memory is exhausted"""
    huge_list = []
    while True:
        huge_list.append(' ' * 10**6)  # Add 1MB of data each time

# Running this function will eventually cause MemoryError
# cause_memory_error()  # Uncomment to crash
```
```python
def divide_unsafe(a, b):
    return a / b  # Crashes if b=0

# Test
print(divide_sunafe(10, 0))
```
<!--v-->
## Exceptions
Proper Exception Handling helps you:
- Quick Error Location Identification
- Preventing Program Crashes from Trivial Errors

<!--v-->

## Specific Exception Catching

```python
def process_user_data(user_data):
    try:
        # Each operation has potential specific exceptions
        username = user_data['username']
        age = int(user_data['age'])
        email = user_data['email']
        
        # Process the data
        user_profile = {
            'username': username.upper(),
            'age': age + 1,  # For demonstration
            'email': email.lower()
        }
        
        return user_profile
        
    except KeyError as e:
        print(f"Missing required field: {e}")
        return None
    except ValueError as e:
        print(f"Invalid data format in age field: {e}")
        return None
    except AttributeError as e:
        print(f"Data type error: {e}")
        return None

# Test with various error scenarios
test_data1 = {'age': 'twenty'}  # ValueError
test_data2 = {'username': 'john'}  # KeyError for 'age'
test_data3 = {'username': 123, 'age': '25', 'email': 'test@test.com'}  # AttributeError

print(process_user_data(test_data1))
# Output: Invalid data format in age field: invalid literal for int() with base 10: 'twenty'
```
<!--v-->
## Detailed Error Context
```python
def read_config_file(config_path):
    try:
        with open(config_path, 'r') as file:
            import json
            config = json.load(file)
            
            # Validate required configuration keys
            required_keys = ['database_url', 'api_key', 'timeout']
            for key in required_keys:
                if key not in config:
                    raise KeyError(f"Missing required config key: {key}")
            
            return config
            
    except FileNotFoundError:
        print(f"❌ Config file not found: {config_path}")
        return None
    except json.JSONDecodeError as e:
        print(f"❌ Invalid JSON in config file: {e}")
        return None
    except KeyError as e:
        print(f"❌ Configuration error: {e}")
        return None
    except Exception as e:
        print(f"❌ Unexpected error reading config: {e}")
        return None

# Test
config = read_config_file("nonexistent_config.json")
if config is None:
    print("Using default configuration instead...")
```
<!--v-->
## Preventing Program Crashes from Trivial Errors
```python
# Inevitable approach
def divide_unsafe(a, b):
    return a / b  # Crashes if b=0

# Avoidable approach
def divide_safe(a, b):
    try:
        return a / b
    except ZeroDivisionError:
        print("Error: Cannot divide by zero")
        return None
    except TypeError:
        print("Error: Inputs must be numbers")
        return None

# Test
print(divide_safe(10, 2))  # 5.0
print(divide_safe(10, 0))  # None, program continues
```
<!--v-->
## Preventing Program Crashes from Trivial Errors
```python
def process_files_with_cleanup(file_paths):
    """
    Process multiple files with automatic cleanup on errors
    """
    processed_files = []
    
    for file_path in file_paths:
        try:
            # Attempt to open and process each file
            with open(file_path, 'r') as file:
                content = file.read()
                
                # Simulate processing that might fail
                if 'invalid' in content:
                    raise ValueError(f"Invalid content detected in {file_path}")
                
                processed_files.append({
                    'file': file_path,
                    'content_length': len(content),
                    'status': 'processed'
                })
                
        except FileNotFoundError:
            print(f"📁 File not found: {file_path} - skipping")
            processed_files.append({
                'file': file_path,
                'status': 'not_found'
            })
            
        except PermissionError:
            print(f"🔒 Permission denied: {file_path} - skipping")
            processed_files.append({
                'file': file_path,
                'status': 'permission_denied'
            })
            
        except ValueError as e:
            print(f"❌ Processing error: {e}")
            processed_files.append({
                'file': file_path,
                'status': 'processing_error'
            })
            
        except Exception as e:
            print(f"⚠️ Unexpected error with {file_path}: {e}")
            processed_files.append({
                'file': file_path,
                'status': 'unexpected_error'
            })
    
    return processed_files

# Test with various file scenarios
files = [
    "existing_file.txt",
    "nonexistent_file.txt", 
    "/root/protected_file.txt",  # Permission error (on Unix systems)
    "file_with_invalid_content.txt"
]

results = process_files_with_cleanup(files)
print("Processing completed. Summary:")
for result in results:
    print(f"- {result['file']}: {result['status']}")
```
<!--v-->
## More about Exceptions?
- exception_hierarchy
- Define exception by yourself
- Exception Chaining
<!--s-->
# Assertions
<!--v-->
A special exception for defensive programming.
## assertion
```python
def divide(a, b):
    assert b != 0, "Denominator cannot be zero"
    return a / b

# This works
result = divide(10, 2)  # Returns 5.0

# This will raise AssertionError
# result = divide(10, 0)  # AssertionError: Denominator cannot be zero
```
- Input Validation
- Preconditions and Postconditions
- Debugging during development
- Testing invariants in your code
<!--s-->
# Dictionary
<!--v-->
## Dict
Dictionaries are unordered, mutable collections of key-value pairs that provide extremely fast data retrieval. They are one of Python's most powerful and commonly used data structures.

### Key Characteristics
- Unordered: Items have no defined order (though insertion order is preserved in Python 3.7+)

- Mutable: Can be modified after creation

- Key-Value Pairs: Store data as {key: value} pairs

- Keys must be hashable: Typically strings, numbers, or tuples

- Fast lookups: O(1) average time complexity for operations

```python
# Creating dictionaries
empty_dict = {}
person = {'name': 'Alice', 'age': 30, 'city': 'New York'}
grades = dict(math=95, science=88, history=92)

print(person)  # {'name': 'Alice', 'age': 30, 'city': 'New York'}
```
<!--v-->
## Fast Retrival
```python
import time
data = list(range(100000))
lst = data.copy()
dct = dict.fromkeys(data)


target = 9999999

start = time.time()
target in lst
list_time = time.time() - start

start = time.time()  
target in dct
dict_time = time.time() - start

print(f"list: {list_time:.6f}s")
print(f"dict: {dict_time:.6f}s")
```
<!--v-->
## Why Dictionary Lookup is O(1)
# Why Python Dictionary Lookup is O(1)

## The Magic: Hash Tables

Dictionaries use **hash tables** underneath, which enables constant-time operations.

## How It Works

### 1. **Hashing**
```python
# Every key is converted to a hash value
key = "name"
hash_value = hash(key)  # Returns a fixed-size integer
```

### 2. **Direct Index Calculation**
```python
# Hash value determines the storage location
index = hash(key) % array_size  # Direct array access
```

### 3. **Instant Access**
- No searching through all elements
- Go directly to calculated index
- Retrieve value in one step
<!--v-->
## Visual Example

```
Dictionary: {'name': 'Alice', 'age': 30, 'city': 'NYC'}

Hash Table:
Index 0: None
Index 1: ('name', 'Alice')    # hash('name') % size = 1
Index 2: None         
Index 3: ('city', 'NYC')      # hash('city') % size = 3
Index 4: None
```

### Key Points

- **Hash function** converts any key to a numerical index
- **Direct array access** - no iteration needed
- **Same process** regardless of dictionary size
- **Collisions handled efficiently** with minimal overhead
<!--v-->
## Why It's Always O(1)

- **10 items**: 1 step to find value
- **10,000 items**: 1 step to find value  
- **1,000,000 items**: 1 step to find value

The lookup time **doesn't increase** with dictionary size - that's the definition of O(1) constant time complexity.

### Real-World Analogy

Think of a **library with numbered shelves**:
- You know exactly which shelf has your book
- Don't need to check every shelf
- Same time to find a book in small or large library

That's how dictionaries achieve O(1) magic!
<!--v-->
## Creating Dictionaries
```python
# Empty dictionary
empty_dict = {}
empty_dict = dict()

# With initial values
person = {'name': 'Alice', 'age': 30, 'city': 'New York'}
grades = dict(math=95, science=88)  # Keys as keyword arguments

# From sequences
keys = ['a', 'b', 'c']
values = [1, 2, 3]
mapped = dict(zip(keys, values))  # {'a': 1, 'b': 2, 'c': 3}

# Dictionary comprehension
squares = {x: x*x for x in range(5)}  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```
<!--v-->
## Accessing Values
```python
person = {'name': 'Alice', 'age': 30}

# Square bracket notation
print(person['name'])  # 'Alice'

# get() method (safe access)
print(person.get('age'))      # 30
print(person.get('email'))    # None
print(person.get('email', 'Not found'))  # 'Not found'

# Check key existence
print('name' in person)     # True
print('email' not in person) # True
```
<!--v-->
## Modifying Dictionaries
```python
person = {'name': 'Alice'}

# Add/update items
person['age'] = 30           # Add new key
person['name'] = 'Bob'       # Update existing key

# update() method
person.update({'city': 'NYC', 'age': 31})  # Multiple updates

# setdefault() - get value or set if not exists
count = person.setdefault('visits', 0)  # Returns 0, sets 'visits': 0
```
<!--v-->
## Removing Items
```python
person = {'name': 'Alice', 'age': 30, 'city': 'NYC'}

# pop() - remove and return value
age = person.pop('age')           # age = 30, removes 'age'
email = person.pop('email', None) # Returns None if key doesn't exist

# popitem() - remove and return last item (LIFO)
key, value = person.popitem()     # Removes ('city', 'NYC')

# del statement
del person['name']               # Removes 'name' key

# clear() - remove all items
person.clear()                   # person becomes {}
```
<!--v-->
## Iterating Over Dictionaries
``` python
person = {'name': 'Alice', 'age': 30, 'city': 'NYC'}

# Iterate keys
for key in person:
    print(key)

for key in person.keys():
    print(key)

# Iterate values
for value in person.values():
    print(value)

# Iterate key-value pairs
for key, value in person.items():
    print(f"{key}: {value}")
```
<!--v-->
## Dictionary Views
```python
person = {'name': 'Alice', 'age': 30}

# View objects (dynamic)
keys_view = person.keys()       # dict_keys(['name', 'age'])
values_view = person.values()   # dict_values(['Alice', 30])
items_view = person.items()     # dict_items([('name', 'Alice'), ('age', 30)])

# Views update when dict changes
person['city'] = 'NYC'
print(list(keys_view))  # ['name', 'age', 'city'] - automatically updated
```
<!--v-->
## Dictionary Comprehension
```python
# Basic comprehension
numbers = [1, 2, 3, 4]
squares = {x: x**2 for x in numbers}  # {1: 1, 2: 4, 3: 9, 4: 16}

# With condition
even_squares = {x: x**2 for x in numbers if x % 2 == 0}  # {2: 4, 4: 16}

# Transform existing dictionary
person = {'name': 'alice', 'age': '30'}
uppercase = {k: v.upper() if isinstance(v, str) else v for k, v in person.items()}
# {'name': 'ALICE', 'age': '30'}

# Swap keys and values
original = {'a': 1, 'b': 2, 'c': 3}
swapped = {v: k for k, v in original.items()}  # {1: 'a', 2: 'b', 3: 'c'}
```
<!--v-->
## Merging Dictionaries
```python
# Python 3.5+ - unpacking
dict1 = {'a': 1, 'b': 2}
dict2 = {'b': 3, 'c': 4}
merged = {**dict1, **dict2}  # {'a': 1, 'b': 3, 'c': 4}

# update() method
dict1.update(dict2)  # dict1 becomes {'a': 1, 'b': 3, 'c': 4}

# Python 3.9+ - union operators
merged = dict1 | dict2        # New dict: {'a': 1, 'b': 3, 'c': 4}
dict1 |= dict2               # In-place update of dict1
```
<!--v-->
## Useful Dictionary Methods
```python
person = {'name': 'Alice', 'age': 30}

# copy() - shallow copy
person_copy = person.copy()

# fromkeys() - create dict from sequence
defaults = dict.fromkeys(['name', 'age', 'city'], 'unknown')
# {'name': 'unknown', 'age': 'unknown', 'city': 'unknown'}

# len() - number of items
print(len(person))  # 2

# Check emptiness
if person:          # True if not empty
    print("Dict has items")
```
<!--s-->
# Recursion
<!--v-->
## Recursion is a way of thinking
- The factorial of a number `n` (n!) is the product of all positive integers up to `n`.
`5! = 5 * 4 * 3 * 2 * 1 = 120`

- The factorial of n is just n times the factorial of (n-1).
```python
factorial(n) = n × factorial(n-1)
```

We can break down a huge difficult problem to many small and easy ones. (The base case will be very easy.)
- "If I can solve for n-1, I can solve for n"
```python
def factorial_iterative(n):
    result = 1
    # Loop from 1 to n, multiplying each time
    for i in range(1, n + 1):
        result *= i
    return result

print(factorial_iterative(5))  # Output: 120
```
<!--v-->
## Recursion: fibonacci
0,1,1,2,3,5,8,13...
fibonacci(n) = fibonacci(n-1) + fibonacci(n-2)
```python
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)
```
<!--v-->
## Recursion: permutations
The permutation of n elements = the first element of each permetation + the full permutation of the remaining n-1 elements.

n个元素的排列 = 每个元素开头 + 剩下n-1个元素的全排列
```python
def permutations(nums):
    if len(nums) == 0:
        return [[]]
    
    result = []
    for i in range(len(nums)):
        rest = nums[:i] + nums[i+1:]
        for p in permutations(rest):
            result.append([nums[i]] + p)
    return result
```
<!--v-->
## Iteration v.s. Recursion

*   **Iteration:** Uses looping constructs (`for`, `while`) to repeat a block of code. It's a *step-by-step* execution of instructions.
*   **Recursion:** A function that calls *itself* to solve a smaller instance of the same problem. It's a "divide and conquer" approach.

<!--v-->

## Visual Example: Calculating Factorial

The factorial of a number `n` (n!) is the product of all positive integers up to `n`.
`5! = 5 * 4 * 3 * 2 * 1 = 120`
<!--v-->
## 1. Iterative Approach

```python
def factorial_iterative(n):
    result = 1
    # Loop from 1 to n, multiplying each time
    for i in range(1, n + 1):
        result *= i
    return result

print(factorial_iterative(5))  # Output: 120
```
**How it works:**
*   `result` starts at 1.
*   The loop runs from 1 to 5, multiplying `result` by each number.
*   The state is managed by the loop variable `i` and the `result` variable.
<!--v-->
## 2. Recursive Approach

```python
def factorial_recursive(n):
    # Base Case: stops the recursion
    if n == 0 or n == 1:
        return 1
    # Recursive Case: function calls itself with a smaller problem
    else:
        return n * factorial_recursive(n - 1)

print(factorial_recursive(5))  # Output: 120
```
**How it works:**
*   **Base Case (`n == 0 or n == 1`)**: This is crucial. It stops the function from calling itself indefinitely.
*   **Recursive Case (`n * factorial_recursive(n-1)`)**: The function breaks the problem down. "The factorial of 5 is 5 times the factorial of 4."
<!--v-->
**Visualizing the Recursive Calls:**
```
factorial_recursive(5)
= 5 * factorial_recursive(4)
= 5 * (4 * factorial_recursive(3))
= 5 * (4 * (3 * factorial_recursive(2)))
= 5 * (4 * (3 * (2 * factorial_recursive(1))))
= 5 * (4 * (3 * (2 * 1)))  <-- Base case is reached here!
= 5 * (4 * (3 * 2))
= 5 * (4 * 6)
= 5 * 24
= 120
```
Each call waits on the stack for the result of the next call until the base case is reached, then the values "bubble back up."
<!--v-->

## Head-to-Head Comparison

| Feature | Iteration | Recursion |
| :--- | :--- | :--- |
| **Definition** | Repeats a block of code using loops. | A function calls itself. |
| **State** | Maintains state with a **counter variable** (e.g., `i`). | Maintains state through **parameters** passed in each call. |
| **Termination** | Terminates when the **loop condition** becomes false. | Terminates when a **base case** is reached. |
| **Performance** | Generally **faster** and more **memory-efficient**. No overhead of function calls. | Can be **slower** and use **more memory** due to function call overhead and stack usage. |
| **Stack Usage** | Uses a fixed amount of memory. | Uses the **call stack**; deep recursion can cause a **stack overflow**. |
| **Code Readability** | Can be less readable for problems inherently recursive. | Often more **elegant and intuitive** for problems like tree traversal, Fibonacci, etc. |
| **Infinite Loop** | Infinite loop consumes CPU but no stack overflow. | Infinite recursion causes a **stack overflow** error. |
<!--v-->

## When to Use Which?

### Use **Iteration** when:
*   **Performance is critical:** You need the fastest execution and minimal memory footprint.
*   **The problem is naturally iterative:** For example, processing each element in a simple list.
*   **Deep recursion is a risk:** If the problem size is large, iteration avoids stack overflows.
*   **Memory is limited:** Embedded systems often favor iteration.

### Use **Recursion** when:
*   **The code is much cleaner and easier to understand:** This is the most important reason. For problems with a recursive structure, a recursive solution can be significantly more readable and less error-prone.
*   **The problem is inherently recursive:**
    *   Tree and Graph traversals (e.g., calculating directory sizes).
    *   Problems like Towers of Hanoi, Fibonacci series (though memoization is needed for efficiency).
    *   Divide and Conquer algorithms (Merge Sort, Quick Sort).
    *   Backtracking algorithms.
<!--v-->
## Tips: Tail Recursion

There's a special case called **Tail Recursion**, where the recursive call is the *very last thing* the function does. A good compiler can optimize tail recursion to use constant stack space, effectively turning it into an iteration. This eliminates the main performance drawback of recursion.

**Non-Tail Recursive (like our factorial example):**
`return n * factorial(n-1)` // The multiplication happens *after* the recursive call returns.

**Tail Recursive Factorial (using an accumulator):**
```python
def factorial_tail_recursive(n, accumulator=1):
    if n == 0:
        return accumulator
    else:
        return factorial_tail_recursive(n - 1, n * accumulator)
```
// The recursive call is the last operation. A smart language/compiler can optimize this.

**Note:** Python does not perform tail call optimization, but languages like Scala, Haskell, and functional languages often do.
<!--v-->