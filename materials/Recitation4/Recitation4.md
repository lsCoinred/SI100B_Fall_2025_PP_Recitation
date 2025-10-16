---
title: SI100B_Fall_2025_Recitation_4
separator: <!--s-->
verticalSeparator: <!--v-->
theme: simple
highlightTheme: github
css: assets/custom.css
autoTitlePage: true
makeTitle:
    lecture: SI100B Fall 2025 Recitation 4
    title: L7 & L8
    detail: SI100B 2025 Staff | 2025-10-17
makeThanks: true
---
# Functions as Objects

<!--v-->
## Functions as Objects
- Python中函数可以作为参数传递
- 示例：灵活折扣系统
  - 定义主函数`apply_discount(price, discount_strategy)`
  - `discount_strategy`是一个函数，计算折扣金额

<!--s-->
# Tuple
<!--v-->
## Tuples（元组）
- 一种新的复合数据类型
- 不可变（immutable）
- 用圆括号`()`表示
- 支持索引、切片、合并、长度、最大/最小值等操作


**Tuples操作示例**
```python
tuple_empty = ()      # 空元组
tuple_short = (2,)    # 单元素元组需加逗号
hello_tuple = (2, "stu", 3)
hello_tuple[0]   # 2
hello_tuple[1:3] # ("stu", 3)
```

<!--v-->


## 可变数量的参数

Python 有一些内置函数可以接受可变数量的参数，例如 `min()`。
可以使用 `*` 符号来实现相同的功能。
```python
def mean(*args): tot = 0
    for a in args:
        tot += a
return tot / len(args)

mean(1, 2, 3, 4, 5, 6)
```
其中 `args` 绑定到所提供值的元组

<!--v-->




<!--s-->

# List
<!--v-->
## List(列表)
- 可变（mutable）序列
- 用方括号`[]`表示
- 可包含任意类型元素
- 支持索引、切片、合并、迭代等操作

例子:
```python
empty_list = []
hello_list = [2, "a", 4, [1, 2]]
hello_list[0]      # 2
hello_list[3]      # [1, 2]
[1, 2] + [3, 4]    # [1, 2, 3, 4]
```
<!--v-->
## List(列表)
- `append(element)`：在末尾添加元素（无返回值）
- `sort()`：原地排序，返回None
- `reverse()`：原地反转，返回None
- `sorted(list)`：返回新排序列表，不修改原列表
<!--v-->
## Lists与函数
可传递列表给函数，函数内可修改原列表（副作用）
示例：平方列表中所有元素
```python
def square_list(L):
    for i in range(len(L)):
        L[i] = L[i] ** 2
```
<!--v-->
## 字符串与列表互转
字符串转列表：
- `list(s)`：每个字符作为元素
- `s.split(char)`：按字符分割
列表转字符串：
- `''.join(L)`：合并列表为字符串
- `'_'.join(L)`：用指定字符连接


<!--s-->
# ALIASING, CLONING
<!--v-->
## 为什么需要 Copy？
- 赋值语句只是为一个对象**另起**了一个名字
- 对于自身可变的对象，会使目标和对象同时改变
```py[]
l1 = [1, 2, 3]
l2 = l1
l2.append(4)
print(l2)  # [1, 2, 3, 4]
print(l1)  # [1, 2, 3, 4]
```
- 场景：将List作为一个参数传递给一个函数，函数有可能对List进行改变

<!--v-->
## 对一个列表进行 Copy
- 改变生成的副本，不影响原始对象
- `Lnew= Loriginal[:]` 或者 `Lnew = copy.copy(Loriginal)`
  - 等价于创建空列表 `Lnew`, 接着将遍历 `Loriginal`，将 `Loriginal` 的每个元素依次 `append` 进 `Lnew`
```py[]
l1 = [4, 5, 6]
l2 = l1[:]
l2.append(7)
print(l2)  # [4, 5, 6, 7]
print(l1)  # [4, 5, 6]
```
<img src="images/Tutorial4_copy.png" width="70%" style="display: block; margin: 0 auto;">

<!--v-->
## Shallow Copy 一个嵌套的可变对象
<img src="images/Tutorial4_copy_nested.png" style="display: block; margin: 0 auto;">

<!--v--> 
## Deep Copy
- 使用深拷贝当列表可能包含可变元素时，以确保每个层级的每个结构都被复制。
<img src="images/Tutorial4_deep_copy.png" width="90%" style="display: block; margin: 0 auto;">

<!--v-->
## 如果只拷贝 k 层呢?
```py[]
# Example usage
original = [1, [2, [3, [4 , 4]]]]
deepk_copied = k_level_copy(original, 3)
# Modify the deep copy
deepk_copied[1][1][0] = 'Changed'
deepk_copied[1][1][1][1] = 'Changed'
print(original) # [1, [2, [3, [4, 'Changed']]]]
print(deepk_copied) # [1, [2, ['Changed', [4, 'Changed']]]]
```
- `k_level_copy(original, 1)` 等价于 `copy.copy(original)` 
- `k_level_copy(original, 4)` 等价于 `copy.deepcopy(original)` 
<!--v-->
## 如果只拷贝 k 层呢? (Optional)
```py[]
def k_level_copy(obj, k):
    if k <= 0:
        return obj
    if isinstance(obj, list):
        new_list = []
        for item in obj:
            new_list.append(k_level_copy(item, k - 1))  
        return new_list
    elif isinstance(obj, dict):
        ...
    else:
        return obj  # Return the object if it's immutable
```
<!--v-->
## 更多例子
```py
import copy
orig = ['Hi, I am ', list('Bob')]
alias = orig
shallow = orig.copy()
deep = copy.deepcopy(orig)
orig[0] = 'Hi, he is'
orig[1][0] = 'C'
print(orig, alias, shallow, deep, sep='\n')
```
What should be the output?

<!--v-->
## 更多例子
```text
['Hi, he is', ['C', 'o', 'b']]
['Hi, he is', ['C', 'o', 'b']]
['Hi, I am ', ['C', 'o', 'b']]
['Hi, I am ', ['B', 'o', 'b']]
```
<!--v-->
## Some cool list comprehension solutions
```py
def remove_all(l, val):
    return [x for x in l if x != val]
```
```py
def remove_dups(L1, L2):
    return [x for x in L1 if x not in L2]
```
<!--v-->
# Decorators
<!--v-->
_Anything in Python is an object._

```py
def nice():
    print('hello')
def apathetic():
    print('...')
```

```py
import random
logic = {0: nice, 1: apathetic, 2: nice}
logic[random.randint(0, 2)]()
```

```text
hello
```

<!--v-->

_They can be arguments._

```py
def plus(x, y):
    return x + y
def div(x, y):
    return x / y
def perform(x, y, op):
    print(op(x, y))
    
perform(2, 3, div)  
perform(2, 10, lambda x, y: x**y) 
```
```text
0.6666666666666666
1024
```

<!--v-->

_They can be returned._
```py
def wrapper(rapper):
    def greet():
        print('This is rapper ' + rapper + '.')
    return greet

wrapper('Ken')()  
```
```text
This is rapper Ken.
```

<!--v-->
If a function takes a function as argument and returns a function, it can actually produce a modified version of the argument function. Python allows us to perform such modification with the notation '@'.

```py
# The decorator 
def triplet(f):
    def _inner(x):
        f(x)
        f(x)
        f(x)
    return _inner

def annihilator(f):
    def do_nothing(*args, **kwargs):
        pass
    return do_nothing
```
<!--v-->
```py
@triplet
def say(name):
    print('hello ' + name)
    
@annihilator
def say_goodbye(word):
    print(word)
```

```py
say('world')
print('----')
say_goodbye('I will miss you', time = 2)
```

```text
hello world
hello world
hello world
----
```

<!--v-->
An example from wiki.python.org:

```py
def __main__(func):

    if __name__ == "__main__":
        import sys, os
        args = sys.argv[:]
        args[0] = os.path.abspath(args[0])
        func(*args)
        
@__main__
def main(*args):
    print(f'mian received {len(args)} arguments')
```

```text
(ml) zws@fugue SI100B-test % python main.py 1 2 3      
mian received 4 arguments
```
<!--v-->
Some useful decorators, built-in or provided by modules...
- Call the function when program terminates: `@atexit.register`
- Checks if the values in a enum declaration is unique: `@enum.unique`
- Partial function that pre-specifies some parameters: `partial()`
  e.g. `lean_print = functools.partial(print, end = '', sep = '')`

More to be used in OOP...
- Generates `__init__` etc. (_class_ decorator!): `@dataclasses.dataclass`
- Declare static (global/within a class) functions: `@staticmethod`, `@classmethod`
- Getter method: `@property`
  
<!--s-->
# Tuples
<!--v-->

- Tuple is about immutability.
- It encapsulates a _linear_ order, like a _struct_, but without field names.
    - You don't want to accidentally modify its structure!
    - e.g. A list of points in $\mathbb {R}^2$: `[(0.2, 0.3), (1.1, 1.2), ...]`
- Is _hashable_ (if its elements are hashable), therefore can be used as dictionary keys.

<!--v-->

- Singletons
  ```py
  >>> 1 == (1) != (1,)
  True
  ```
- Constructors
  `tuple()` accepts iterables
- Packing and Unpacking
  ```py
  temperature, humidity = get_weather()
  a, b, c = c, a, b
  ```
  
<!--v-->
Linear Operations...
- Linear indexing, Slicing
  ```py
  ('a', 'b', 'c', 'd')[3] == 'd'
  (0, 1, 2, 3, 4, 5)[1:3] == (1, 2)
  (0, 1, 2, 3)[::-1] == (3, 2, 1, 0)
  ```
- Concatenation, Repeating
  ```py
  (1, 2, 3, 4) + (10, 11) == (1, 2, 3, 4, 10, 11)
  (1, 2) * 3 == (1, 2, 1, 2, 1, 2)
  ```
- Sorting
  ```py
  sorted_tuple = tuple(sorted(original_tuple))
  ```