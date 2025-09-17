---
title: SI100B_Fall_2025_Recitation_1
separator: <!--s-->
verticalSeparator: <!--v-->
theme: simple
highlightTheme: github
css: assets/custom.css
autoTitlePage: true
makeTitle:
    lecture: SI100B Fall 2025 Recitation 1
    title: 环境配置 & 如何使用搜索引擎解决问题
    detail: SI100B 2025 Staff | 2025-09-19
makeThanks: true
---

# 配置开始前的说明

<!--v-->
### 推荐阅读

[你缺失的那门计算机课](https://www.criwits.top/missing/) 新手向，计算机快速上手

[MIT: Missing Semester](https://missing-semester-cn.github.io/) 进阶向，需要配置好 Bash 环境

<!--v-->

## 我们将要配置什么？

在本教程中，我们将配置一套可以用于 SI100B 课程的环境： Anaconda + Jupyter Notebook + VS Code

</br>

- Anaconda：一个 Python 发行版，提供了**包管理、环境管理**等非常方便的功能
  - 这里我们并没有选取 `python.org` 的 Python 安装包，是因为 Anaconda 提供了更好的环境管理功能
  - Miniconda 也是不错的选择，体积更小
  - Anaconda = Python + conda + 已预装的大量包
- Jupyter Notebook：一个交互式笔记本，即在一个文档里运行代码，可以融合文本、公式、图像等多种元素
- VS Code：~~最好的~~代码编辑器，拥有丰富的插件生态，支持多种编程语言

<!--v-->

## ⚠️：不要安装多个 Python

<div style=" margin-top: 10px; margin-right: 10px;" markdown="1">
<img src="images/python_environment.png" width="55%" style="float: right;">

<br/>

- 不同的项目可能需要不同的 Python 版本
- 不同的 Python 版本又可能需要不同版本的库
- 有没有工具可以让我们在不同的 Python 环境之间自由切换？

</div>

<!--v-->

## 可能遇到的问题

- 检查你的用户名是否为英文，中文用户名可能导致安装软件时出现问题
  - 打开终端，输入 `whoami`, 输出中不应该包含中文字符
- 我们将在 Windows 11 操作系统下演示，如果你使用其他操作系统，可以询问使用对应操作系统的助教
- 如果你遇到任何问题，请在 Piazza 或 Office Hour 求助，助教们都乐意帮助你 🥰

<!--s-->

# Anaconda

<!--v-->

## 安装 Anaconda

- 打开浏览器，访问 [Anaconda 官网下载页面](https://www.anaconda.com/download/success)，点击 Download 按钮开始下载
- 也可以选择国内镜像下载，如 [清华大学镜像站](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/?C=M&O=D)

<img src="images/anaconda_download.png" width="50%" style="display: block; margin: 0 auto;">

<!--v-->

## 安装 Anaconda

- 下载完成后，运行安装程序
- 点击 Next/I Agree 几次后会出现如下图所示的，选择安装位置的界面，如果不确定要安装到哪个位置，直接点击 Next 即可

<img src="images/anaconda_install_location.png" width="50%" style="display: block; margin: 0 auto;">

- 接下来一路点 Next/Install 直到安装完成即可

<!--v-->

## 启动 Anaconda Powershell Prompt

- 在安装完成后，Anaconda Navigator 会自动打开，我们可以在这里找到 Anaconda Powershell Prompt
- 后面你也可以在开始菜单中找到 Anaconda Powershell Prompt 和 Anaconda Prompt

<img src="images/anaconda_navigator.png" width="40%" style="display: block; margin: 0 auto;">

<!--v-->

## 创建一个新的 Python 环境

- 在 Anaconda Navigator 中，点击左侧的 Environments `->` Create
- 输入环境的名字，比如 `si100`，然后点击 Create

<img src="images/anaconda_create_env.png" width="40%" style="display: block; margin: 0 auto;">

<!--v-->

## 创建一个新的 Python 环境

<img src="images/anaconda_name_env.png" width="40%" style="display: block; margin: 0 auto;">

<!--s-->

# VS Code

<!--v-->

## 安装 VS Code

- 打开浏览器，访问 [VS Code 官网下载页面](https://code.visualstudio.com/Download)，选择对应你的操作系统的版本下载

<img src="images/vscode_download.png" width="70%" style="display: block; margin: 0 auto;">

<!--v-->

## 安装 VS Code

- 下载完成后，运行安装程序
- 点击同意协议

<img src="images/vscode_install_1.png" width="50%" style="display: block; margin: 0 auto;">

<!--v-->

## 安装 VS Code

- 选择安装位置
- 如果不确定要安装到哪个位置，就用默认的位置

<img src="images/vscode_install_2.png" width="50%" style="display: block; margin: 0 auto;">

<!--v-->

## 安装 VS Code

- 在选择附加任务的界面，将下图红框中的选项勾选上

<img src="images/vscode_install_3.png" width="50%" style="display: block; margin: 0 auto;">

- 继续一路点击，完成安装

<!--v-->

## 安装 VS Code 插件

- 打开 VS Code，点击左侧边栏的 Extensions 图标
- “Python”：官方的Python语言支持，提供更好的语法分析、调试器、代码跳转等等
- “Jupyter”：在VS Code里渲染和编辑Jupyter Notebook！
- 如果侧边栏没有自动推荐这两个插件，可以在搜索框中搜索并安装

<img src="images/vscode_extensions.png" width="40%" style="display: block; margin: 0 auto;">

- 另外的，可以安装一些其他插件，比如SSH、颜色主题、彩虹花括号等等，可以让你的 VS Code 更加好用，这些我们留给大家自己去探索
<!--v-->

## 在 VS Code 中使用 Jupyter Notebook

- 新建一个文件夹，命名为 `SI100B`
- 将 Piazza 上的本课的 Jupyter Notebook 文件（`.ipynb` 文件）移动到 `SI100B` 文件夹中
- 在 Anaconda Navigator 中找到 VS Code 点击 Launch，令 VS Code 可以找到 Anaconda 中的 Python 环境
- 在 VS Code 中点击顶部菜单栏的 File `->` Open Folder，打开刚刚新建的 `SI100B` 文件夹
- 点击左侧边栏的 `.ipynb` 文件，即可打开文件，跟随 Notebook 的内容继续学习

<div style="position: absolute; bottom: -20vh; text-align: center;">

### 到这里，我们的环境配置初步完成！🎉
### 特别感谢SI100+同学提供的相关资料。

</div>

<!--s--> 

# Administrivia

<!--v-->

在本学期中，我们将会有三次使用在线评判机（Online Judge）的作业。具体细节会在为来每一次作业发布时说明。
我们要求大家**独立**完成每一次的作业。如果发现有抄袭行为，我们将会按照学校的相关规定进行处理。

<!--v-->

不要让ChatGPT代替你完成作业！作业的目的是回顾和练习。


<!--s--> 

# 如何使用搜索引擎解决问题

<!--v-->

## 为什么要使用搜索引擎？—— 你应该开始搜索的 101 个理由

- 你现在真的遇到问题了，而遇到问题就应该**解决问题**
- 网上很可能有这个问题的解决方案
- 只靠自己摸索不一定能解决问题
- 可能会搜索到高于这个问题的更深入的知识，扩充你的知识面
- 搜索没有任何的代价
- 这一次没有搞懂，下一次还要再费时间
- 别人通常没有义务帮你解决问题，你应该感谢他们的帮助，但是搜索引擎无所谓！
- 找出思路里面潜在的错误
- ......

<!--v-->

## 通用的搜索引擎

这些搜索引擎可以解决大部分问题

- Google
- Bing
- CN Bing 国内版/百度（仅适合用于搜索中文社区内容，如“百度贴吧”）

<!--v-->

## 如何搜索——关键词

- 一大段描述文字的搜索结果通常不尽人意的
  - 搜索引擎不是有分词功能吗？
  - 长句子分词后也有很多杂音
- 清除冗余
  - “我该怎么用工具 x 做出 y?” `->` “x y”
  - 用空格来分隔关键词，视情况选择具体的还是更抽象的关键词
- 通过搜索结果来调整关键词
  - 搜索结果里面可能不包含一部分关键词 `->` 尝试去掉这些关键词
  - 搜索结果给你新的启发 `->` 尝试加入这些关键词
  - 根据结果不断迭代
    - 内容太老旧 `->` 限制搜索时间/加年份关键词/加软件版本号
    - 名字一样，但是不是你要搜的领域的东西 `->` 加上领域关键词
    - ......

<!--v-->

## 搜索引擎的高级功能

以 Google 为例，其他搜索引擎使用方式类似

- 强制包含关键词：半角双引号
- 强制排除关键词：减号
- 模糊匹配：星号 如 “Python * tutorial” 可能匹配到 “Python beginner tutorial”，“Python Datascience tutorial”
- 限制搜索网站：site: 如 “site:stackoverflow.com Python”
- 限制搜索文件类型：filetype: 如 “filetype:pdf Python”

你还可以使用浏览器插件实现相关功能。

<!--v-->
## AI 工具

**常用站点**

- New Bing (是在线的搜索引擎)
- ChatGPT 
- 现在上科大同学可以免费使用 [genai.shanghaitech.edu.cn](https://genai.shanghaitech.edu.cn)!

**如何询问各类对话大模型**

- 搜索引擎的“关键词”式搜索不一定合适
- 用更加详细的方式描述
- 任何要求都要写清楚
- 有些时候，说“不应该怎样”反而会加强错误

**什么适合问大模型**

- 概览性问题
- 已经有大量数据的问题（防止大模型幻觉胡说八道）


<!--s--> 

# Python是如何跑起来的

<!--v-->

## 计算机的构成
<div style=" margin-top: 10px; margin-right: 10px;" markdown="1">

<img src="images/computer-motherboard.png" width="50%" style="float: right">

<br/>

一个主机通常包括：
- 中央处理器（CPU）：计算能力的核心
- 内存（RAM）：临时存放的数据，速度快，断电失效
- 硬盘（Hard Drive -- SSD，HDD etc）：大容量储存，速度慢，断电保留
- 显卡（GPU）：渲染、矩阵计算，速度更快但是不擅长逻辑
- 电源（Power Supply）：向主板（以及显卡）直流供电
- 主板（Motherboard）：卡槽和总线，连接各个部件，提供外部接口（USB、耳机口），可能带有网卡、wifi天线等等
- 风扇和水冷：（主要给CPU）散热，显卡往往有独立的散热系统

</div>

<!--v-->
## 程序在哪里？

“Everything is a file”

- 在底层，所有东西都是**二进制**表示，所以不同的文件种类只是不同的编码
- 内存同时装载**数据和程序**
- 包含机器码的文件就是**可执行文件**，即程序，装载到内存中可以直接被CPU执行
- 程序的工作是根据输入数据计算对应的输出，所以是一个**函数**
- Python语言本身是一个程序，**代码**是这个程序的输入
- 所以我们编写的是**脚本**，而终端调用的“python3”是**解释器**
- 可以被复用的程序称为**库**（Library），可能是代码（比如Python module），也可能是机器码（比如动态链接库）

<!--v-->
## VS Code 与 Python

- VS Code是代码编辑器，其中核心的部分相当于记事本，即“文本编辑器”。代码高亮让编程更轻松。
- 插件可以给每种语言提供更细致的支持，比如自动补全，代码跳转，语法分析
- Python解释器可以独立运行（在终端直接敲下python3！）
- 编辑器/IDE可以管理文件夹中的不同类型文件、版本控制（git）、可视化调试

<img src="images/ide.png" width="50%" style="float:right">

<!--v-->
## Fun Facts about Python

- 'The Zen of Python': `import this`
- 来自1989年Guido Van Rossum在圣诞节期间的业余项目
- 得名于喜剧片Monty Python’s Flying Circus，而不是蟒蛇
- 可以被编译成其他语言，包括C、Javascript、Julia，或者直接编译为机器码
- 为什么numpy很快？因为底层是C。
  
<!--s-->

# 课堂知识回顾

<!--v-->

## Imperative vs. Declarative

- 命令式编程(Imperative)：告诉计算机如何做(How)来达到结果？程序员拥有更高的自由度，但需要耗费心智管理每一步的状态.
  ```python
  total = 0
  for i in arr:
    total += i
  ```
- 声明式编程(Declarative): 声明我们想要的结果(What)？程序员只需专注业务逻辑，细节已经由别的程序员完成了。交给编译器或者解释器去思考 How。
  ```python
  total = sum(arr)
  ```

<!--v-->

## Syntax & Semantics

- 句法(syntax): 句子的形式或结构
  - 词位(lexeme): 最基本的语法单位(eg. I, dog, hugs，+, =)
  - token：描述词位的种类(eg. keywords，operators)
- 语义(semantics): 句子的含义
- 无语法和语义错误不代表程序按照预想的执行
  - 语义难以准确传递：甲方/题目 -> 程序员 -> 代码

<!--v-->

## 类型转换

- 显式转换(Explicit conversion): 需要手动指定转换类型例如: `str()`,`int()`,`float()`
- 隐式转换(Implicit conversion): Python解释器完成自动转换
  - 向上转换类型，以防止数据丢失
  ```python
    num1 = 2
    num2 = 12.2
    res = num1 + num2
    print("Data type of res: ", type(res)) # Data type of res:  <class 'float'>
    print("Value of res: ", res) # Value of res:  14.2
  ```
  - 数据类型并不总是兼容
  ```python
    num1 = "2"
    num2 = 3
    print(num1 + num2) # TypeError: unsupported operand type(s) for +: 'int' and 'str'
  ```

<!--v-->
## 字符串
- Python 内置字符串类型名为 `str`.
- 字面量可以使用单引号或双引号 `''`, `""`, 使用三引号可跨越多行 `'''`, `"""`
  ```python
  multi = """It was the best of times.
  It was the worst of times."""
  ```
- 空字符串`''` 在布尔上下文中被认为是 false. 其他常见被视为 false 的值有 `None`,`0`,`[]`,`{}`
  ```python
  #检查空字符串
  if not myString:
     ...
  ```
- 切片：`[start:stop:step]`, 如果索引过大，会被截断为字符串长度
  ```python 
  s = "hello"
  print(s[1:100]) # ello
  print(s[100:]=='') # True
  ```

<!--v-->
## 格式化字符串
- 使用格式化字符串(f-string)提高代码可读性，便于打印调试信息
  ```python
  # 控制浮点数显示
  value = 2.791514
  print(f'approximate value = {value:.2f}')  # approximate value = 2.79

  #支持表达式插入
  width = 10
  height = 5
  area_message = f"The area is {width * height}." # The area is 50.
  ```
<!--s-->
# 答疑时间

GL;HF