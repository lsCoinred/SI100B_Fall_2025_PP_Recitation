---
title: SI100B_Fall_2025_Recitation_2
separator: <!--s-->
verticalSeparator: <!--v-->
theme: simple
highlightTheme: github
css: ../../assets/custom.css
autoTitlePage: true
makeTitle:
    lecture: SI100B Fall 2025 Recitation 2
    title: L2, L3 课堂复习 & HW/OJ 简介
    detail: SI100B 2025 Staff | 2025-09-26
makeThanks: true
---

# Homework & Online Judge

<!--v-->

- Homework1 已发布
- 截止日期 10月3日10:AM
- OJ网址: [http://10.15.21.133/d/SI100B_2025_Autumn/](http://10.15.21.133/d/SI100B_2025_Autumn/ ) 网址IP为学校内网，如若想在校外访问，在 egate 平台上使用上科大 VPN 来访问学校内网。
- 账号：我们为每一位同学用学校邮箱([name2025@shanghaitech.edu.cn](mailto:name2025@shanghaitech.edu.cn))提前注册了账号，用户名为name2025，可以使用忘记密码功能用自己的邮箱重置密码。

<!--v-->

## 作业提交

<img src="images/homework_submit_1.png" width="75%" style="float: middle;">

<!--v-->

## 作业提交

<img src="images/homework_submit_2.png" width="75%" style="float: middle;">

<!--v-->
## 作业提交

<img src="images/homework_submit_3.png" width="100%" style="float: middle;">


<!--v-->
## 学术诚信
- 对作业中所有提交过的程序查重（不仅仅是每道题目的最后一次提交）
- 禁止使用AI工具直接生成作业代码
- 保护好自己的代码

<!--v-->
## 作业中的Hint解释

### Q2

> 待作业出来后更新

```python
print(int('F', 16)) 
print('{:X}'.format(31))
```

<!--s-->
# IO

<!--v-->
## 输入
```python
student_id = input("input your student number: ")
```
- 注意！如果 input 函数存在参数，会将其写入到标准输出，写作业代码时不建议添加参数。
- 这里的 input 函数会返回一个输入的**字符串**，即使输入的是数字，也会被当作字符串处理。
  
<!--v-->
## 输出
- print("Hello World!")
- print("x = ", x)
- print(f"x = {x}")
- print(f"x = {x:.2f}")
- print("x={}".format(x))

更多细节可以参考 [Python 文档](https://docs.python.org/zh-cn/3/reference/lexical_analysis.html#string-and-bytes-literals) 但是不要太过于关注细枝末节。

<!--s-->
# 分支

<!--v-->
## 区分 = 和 ==
- variable = value 赋值语句
- some_expression == other_expression 判断相等

<!--v-->
## 判断
返回一个布尔变量，即 True 或 False
- == 等于
- != 不等于
- \> 大于
- < 小于
- \>= 大于等于
- <= 小于等于

<!--v-->
## if-elif-else

 猜数字游戏
 ```python
number = 7 
guess = int(input("Enter an integer: ")) 
if guess == number:
    print("Congratulations, you guessed it.") 
elif guess < number:
    print("No, it is a little higher than that.") 
else:
    print("No, it is a little lower than that.")
 ```

<!--v-->
## Match-Case Statement (Optional)
- python **3.10** 引入的新特性，类似（但更强大）于 C/C++ 中的 Switch-Case 语句
- 将一个变量与不同的**字面值** (Literal) 匹配
  - 从上到下将变量与 case 语句中的每个模式进行比较，直到确认匹配
  - 如果没有其他匹配项，则执行 _ 默认情况
```python
light_color = input("Enter the traffic color") 
match light_color:
  case "red":
    print("Stop")
  case "yellow":
    print("Caution: Prepare to stop") 
  case "green":
    print("Go") 
  case _:
    print("Invalid color")
```

<!--v-->
## Match-Case Statement (Optional)
- 匹配的同时，用于绑定变量
```python
# point is an (x, y) tuple 
match point:
  case (0, 0):
    print("Origin") 
  case (0, y):
    print(f"Y={y}")
  case (x, 0):
    print(f"X={x}") 
  case (x, y):
    print(f"X={x}, Y={y}") 
  case _:
    raise ValueError("Not a point")
```
- 更多用法查阅 [PEP363](https://peps.python.org/pep-0636/)

<!--s-->
# 循环
<!--v-->
## while 循环
在 while 循环中，当条件为 True 时，循环体会一直执行，直到条件为 False。
```python
while condition:
  statement
```
避免无限循环，确保循环条件最终为 False。

<!--v-->
## for 循环
for 循环通常用于遍历一个序列（列表、元祖、字符串等）或其他可迭代对象。
```python
for i in range(5):
  print(i)
```
```python
for i in "hello":
  print(i)
```
<!--v-->
## break 和 continue
- break 语句用于跳出当前循环
- continue 语句用于跳过当前循环中的剩余语句，然后继续下一次循环

<!--v-->
## 猜数字游戏
```python
number = 7 
while True:
  guess = int(input("Enter an integer: ")) 
  if guess == number:
    print("Congratulations, you guessed it.")
    break # break the loop 
  elif guess < number:
    print("No, it is a little higher than that.") 
  else:
    print("No, it is a little lower than that.")

```

<!--s-->
# Coding Style
<!--v-->
## 为什么要有良好的代码风格？
**“There are only two hard things in Computer Science: cache invalidation and naming things” ---Phil Karlton**
- 方便自己检查 bug
- 方便合作者阅读代码
- 阅读/写出赏心悦目的代码能让人心情愉悦

<!--v-->
## 遵循 PEP 8 规范
Python 创建了一个官方的编码风格规范：[PEP 8](https://peps.python.org/pep-0008/)，以保持不同开发者编写的代码风格的一致性。

1. 使用3个空格进行锁进。
2. 每行不超过79个字符。
3. 变量命名约定：
   - 对于普通变量，使用蛇形命名法，例如：max_value.
   - 对于常量，使用全大写字母，并使用下划线连接，例如：MAX_VALUE。
   - 对于仅供内部使用的变量，在其前面添加下划线前缀，例如：_local_var。
   - 对于与Python 关键字冲突的变量名，在变量末尾添加下划线，例如：class_。

<!--v-->
## 描述性的变量名
- 代码大量使用描述性较弱的变量名，读者将很难理解代码的含义。例如
 <div style=" margin-top: 10px; margin-right: 20px; margin-left: 20px" markdown="1">

| weakly descriptive | strong descriptive | 
|:---:|:---:|
| data | file_chunks | 
| temp | pending_id | 
| result | active_menber | 
</div> 

- 一些特殊情况：
  - 数组索引 `i,j,k`
  - 一些整数 `n`
  - 一个临时字符串 `s`
  - 一个异常 `e`
  - 文件对象 `fp`

<!--v-->
## 两种最常见的命名规范
- 驼峰命名法（Camel Case）：第一个单词首字母小写，其余单词首字母答谢，此法常用于方法名:
  - firstName
  - findLocation
- 下划线命名法（Snake Case）：所有单词用下划线连接。
  - first_name
  - find_location

<!--v-->
## 善用空格
- 肉眼可利用空格快速区分代码的不同部分
- 在二元运算符（如`+`、`-`、`==`、`>` 和`=`）前后使用空格，明确区分运算符和操作数。例如：`1 + 1`，`ans += 1`
- 在 “,” 后使用空格。例如：`func(a, b, c)`

<!--v-->
## 缩进
- 可以选择使用 4 个空格（PEP8 规范）、2个空格（Google style）或 1个 tab 作为缩进方式。
- 必须在所有代码中保持相同的缩进方式
<img src="images/indentation_method.png" width="75%" style="float: middle;">


<!--v-->
## 减少无意义注释（Comment）
- 没有编译器或者解释器的相助，编写和维护注释需要更多的时间成本
- 试图通过更好的命名替代注释
```python
# HTTP response code indicates can't find the requested resource 
if stauts_code == 404:
  ...
```
```python
HTTP_NOT_FOUND = 404 
if stauts_code == HTTP_NOT_FOUND:
  ...
```

<!--s-->

# 答疑时间
