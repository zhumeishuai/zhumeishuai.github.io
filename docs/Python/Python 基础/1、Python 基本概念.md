## 1、标识符

标识符就是变量、函数、属性、类、模块等可以由自定义名称的代码元素。构成标识符的字符均遵循一定的命名规则。

Python 中标识符的命名规则如下：

-   区分大小写：Myname 与 myname 是两个不同的标识符。
-   不能以数字开头，可以是下画线 '_' 或字母。
-   除首字符外的其他字符必须是 '_'、字母和数字。
-   关键字不能作为标识符。
-   不能使用 Python 的内置函数作为标识符。

## 2、关键字

关键字是语言本身定义好的有特殊含义的代码元素。

```python
import keyword
print(keyword.kwlist)		# 查看关键字

>>>
['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```

## 3、变量

在 Python 中，为一个变量赋值的同时就声明了该变量，该变量的数据类型就是赋值数据所属的类型，该变量还可以接收其它类型的数据。

### 1、赋值

```python
name1 = 'zhums'					# 传统赋值
age1 = num = 18					# 链式赋值
name2, age2 = 'wuyi', 19		# 序列解包赋值
print(name1)
print(age1, num)
print(name2, age2)

>>>
zhums
18 18
wuyi 19
```

## 4、语句

Python 代码由关键字、标识符、表达式和语句等构成，语句是代码的重要组成部分。

在 Python 中，一行代码就表示一条语句，一般情况下语句结束时不加分号。

```python
name = 'zhums'
age = 21;		# 语句结束可以加分号，但不符合 Python 编程规范。
a = b = c =10	# Python 链式赋值语句可以同时给多个变量赋相同的值
```

## 5、注释

### 1、单行注释

Python 单行注释使用井号 `# ` 来注释。

```python
# coding=utf-8
# 这个注释告诉 Python 解释器该文件的编码集是 UTF-8，可以避免代码中有中文等亚洲文字无法解释文件的问题。该语句必须放在文件的第1、2行才能生效。替代写法 # -*- coding:utf-8 -*-
```

### 2、多行注释

Python 中多行注释使用 3 单引号 `''' 注释内容 '''` 或 3 双引号 `""" 注释内容 """` 来注释。

```python
'''
line1
line2
'''

"""
line1
line2
"""
```

## 1、Print() 输出

### 1、基本语法

```python
print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)
```

-   `sep` 参数用于指定分隔符，默认为空格。

```pyhon
print ("Hello", "World")
print ("Hello", "World", sep=' | ')

>>>
Hello World
Hello | World
```

-   `end` 参数用于指定结束符，默认为换行。

```python
for i in range(1,3):
    print (i)
for num in range(1,3):
    print (num, end=",")

>>>
1
2
1,2,
```

`file` 参数用于指定 `print()` 函数的输出目标，默认值为 `sys.stdout`，系统标准输出即屏幕。

```python
# 指定 file 参数，让 print() 函数输出到特定文件中。

f = open("demo.txt","w")			# open() 函数用于打开 demo.txt 文件
print('Welcome to Python',file=f)	# 将字符串写入文件
f.close()							# 调用 close() 函数关闭文件
```

`flush` 参数用于控制输出缓存，该参数一般保持为 False 即可，这样可以获得较好的性能。

### 2、占位符

```python
%s		# 字符串占位符
%d		# 数字占位符
%o		# 八进制数字占位符
%x|%X	# 十六进制数字占位符
%f		# 浮点数占位符
```

```python
str1 = "Hello"
str2 = "Python"
num1 = 10
num2 = 20
float1 = 10.115
float2 = 20.2224
print ("str1: %s" %str1)
print ("str1: %s  str2: %s" %(str1, str2))
print ("num1: %d" %num1)
print ("num1: %o  num1: %x" %(num1, num1))
print ("float1: %f" %float1)

>>>
str1: Hello
str1: Hello  str2: Python
num1: 10
num1: 12  num1: a
float1: 10.115000
```

### 3、指定最小输出宽度

当使用占位符时，可以指定最小输出宽度即至少占用多少个字符的位置：

-   `%nd`: 表示输出的整数宽度至少为 n。
-   `%ns`: 表示输出的字符串宽度至少为 n.

```python
str1 = "Hello"
num1 = 10
float1 = 10.115
print ("str1:%8s" %str1)
print ("num1:%4d" %num1)
print ("float1:%.2f" %float1)

>>>
str1:   Hello
num1:  10
float1:10.12
```

### 4、指定对齐方式

默认 `print()` 右对齐输出。当数据不够宽时，数据总是靠右输出，而在左边补充空格以达到指定的宽度。Python 允许在最小宽度之前增加一个标志来改变对齐方式，Python 支持的标志如下：

| 标志 | 说明                                           |
| ---- | ---------------------------------------------- |
| -    | 左对齐                                         |
| +    | 表示输出的数字要带符号即正数带 `+`，负数带 `-` |
| 0    | 表示宽度不足时补充 `0` 而不是空格              |

>   **说明：**
>
>   -   对于整数，指定左对齐时，在右边补 0 是没有效果的，因为这样会改变整数的值。
>   -   对于小数，以上三个标志可以同时存在。
>   -   对于字符串，只能使用 `-` 标志，因为符号对于字符串没有意义，而补 0 会改变字符串的值。

```python
n = 123456
f = 140.5
s = "Hello"
print("n(09):%09d" %n)		# %09d 表示最小宽度为9，左边补0
print("n(+9):%+9d" %n)		# %+9d 表示最小宽度为9，带上符号
print("f(-+0):%-+010f" %f)	# %-+010f 表示最小宽度为10，左对齐，带上符号
print("s(-10):%-10s." %s)	# %-10s 表示最小宽度为10，左对齐

>>>
n(09):000123456
n(+9):  +123456
f(-+0):+140.500000
s(-10):Hello    
```

### 5、指定浮点数精度

对于浮点数 `print()` 允许指定小数点后的数字位数，也即指定小数的输出精度。精度值需要放在最小宽度之后，中间用点号 `.` 隔开；也可以不写最小宽度，只写精度。

-   `%.nf`: n 表示输出精度，`.`是必须存在的。
-   `%m.nf`: m 表示最小宽度。

```python
f = 3.141592653
print("%8.3f" % f)			# 最小宽度为 8，小数点后保留 3 位
print("%08.3f" % f)			# 最小宽度为 8，小数点后保留 3 位，左边补 0
print("%+08.3f" % f)		# 最小宽度为 8，小数点后保留 3 位，左边补 0，带符号

>>>
   3.142
0003.142
+003.142
```

## 2、Input() 输入

```python
# input 函数
语法： NAME = input('提示信息')
作用： 输入
```
