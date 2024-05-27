## 1、判断语句

### 1、if 语句

#### 1、单分支

```python
if expr1:
    代码块 1
```

#### 2、双分支

```python
if expr1:
    代码块 1
else:
    代码块 3
```

#### 3、多分支

```python
if expr1:
    代码块 1
elif expr2:
    代码块 2
else:
    代码块 3
```

#### 4、示例

##### 1、计算 BMI

```python
height = float(input("请输入身高(米):"))
weight = float(input("请输入体重(千克):"))
bmi = weight / (height * height)
if bmi < 18.5:
    print("BMI 指数为:" + str(bmi), "体重过轻")
elif  bmi >= 18.5 and bmi < 24.9:
    print("BMI 指数为:" + str(bmi), "体重正常")
elif  bmi >= 24.9 and bmi < 29.9:
    print("BMI 指数为:" + str(bmi), "体重偏重")
else:
    print("BMI 指数为:" + str(bmi), "体重超重")
    
>>>
请输入身高(米):1.68
请输入体重(千克):46
BMI 指数为:16.298185941043087 体重过轻
```

### 2、assert 断言

`Python assert` 语句，又称断言语句，可以看做是功能缩小版的 `if` 语句，它用于判断某个表达式的值，如果值为真，则程序可以继续往下执行；反之，`Python` 解释器会报 `AssertionError` 错误。

`assert` 语句的语法结构为：

```python
assert 表达式
```

`assert` 语句的执行流程用 `if` 判断语句表示，如下所示：

```python
if 表达式==True:
    程序继续执行
else:
    程序报 'AssertionError' 错误
```

>   `assert` 会令程序崩溃，为什么还要使用它呢？因为，与其让程序在晚些时候崩溃，不如在错误条件出现时，就直接让程序崩溃，这有利于对程序排错，提高程序的健壮性。
>
>   因此，`assert` 语句通常用于检查用户的输入是否符合规定，还经常用作程序初期测试和调试过程中的辅助工具。

```python
mathmark = int(input("请输入数学分数: "))
assert 0 <= mathmark <= 100	# 断言数学分数是否在正常范围内，当 mathmark 在 0-100 之间时程序才会继续执行
print("数学分数为：", mathmark)

>>>
请输入数学分数: 100
数学分数为： 100
>>>
请输入数学分数: 654
Traceback (most recent call last):
  File "C:\Users\Administrator\Desktop\Demo\python\test.py", line 2, in <module>
    assert 0 <= mathmark <= 100
AssertionError
```

## 2、循环语句

### 1、while 循环

#### 1、while 循环执行流程

`while` 语句执行的具体流程为：

首先判断条件表达式的值，其值为真（`True`）时，则执行代码块中的语句，当执行完毕后，再回过头来重新判断条件表达式的值是否为真，若仍为真，则继续重新执行代码块...如此循环，直到条件表达式的值为假（`False`），才终止循环。

#### 2、while 循环语法

```python
while expr:
	代码块
[else:			# else 是在循环正常结束后才执行的语句，当遇到 break、return 和异常发生时都会中断循环
	代码块]
```

#### 3、while 循环示例

**1、打印 `1-10` 的所有数字。**

```python
num = 1
while num <= 10:
    print(num, end=' ')
    num+=1
    
>>>
1 2 3 4 5 6 7 8 9 10 
```

**2、遍历字符串**

```python
my_site = "http://www.zhums.top"
num = 0
while num < len(my_site):
    print(my_site[num], end=" ")
    num+=1

>>>
h t t p : / / w w w . z h u m s . t o p 
```

**3、else 子句示例**

```python
i = 0
while i * i < 10:
    i += 1
    print (str(i) + ' * ' + str(i) + ' =', i * i)
else:
    print ("While Over!")

>>>
1 * 1 = 1
2 * 2 = 4
3 * 3 = 9
4 * 4 = 16
While Over!
```

**4、嵌套循环**

```python
n = int(input('Please Input Number：'))
i = 1
while i <= n:
    j = 1
    while j <= i:
        print('*',end=' ')
        j += 1
    print()
    i += 1
    
>>>
Please Input Number：5
* 
* * 
* * * 
* * * * 
* * * * *
```

### 2、for 循环

`Python` 中的 `for` 语句，即 `for-in 语句`，常用语遍历可迭代对象中的元素。可迭代对象包括：字符串、列表、元组、集合和字典等。 

#### 1、for 循环语法

```python
for Var in Object:
	代码块
[else:			# else 是在循环正常结束后才执行的语句，当遇到 break、return 和异常发生时都会中断循环
	代码块]
```

#### 2、range() 函数

`Python` 中的 `range()` 函数用于生成可迭代对象。

##### 1、range() 函数语法

```python
range(start,stop[,step])
```

-   `start`：开始，默认为 `0`
-   `stop`：结束，但不包括 `stop`
-   `step`：步长，默认为 `1`

##### 2、示例

**1、打印 `1-10` 之内的偶数**

```python
num = list(range(2,11,2))
print(num)

>>>
[2, 4, 6, 8, 10]
```

**2、打印 `1-10` 分别的平方值**

```python
list1 = []
for i in range(1,11):
    list1.append(i ** 2)
print(list1)

>>>
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

```python
# Demo

for i in range(1,5):
    print (i)
else:
    print ("for run done!")

for num in range(1,5):
    print (num)
    if num == 3:
        break
else:
    print ("for run error done!")

>>>
1
2
3
4
for run done!
1
2
3
```

#### 3、序列解包赋值

在 `Python` 的 `for` 循环中，可以使用序列解包（Sequence Unpacking）来同时迭代和赋值。这意味着可以将一个序列（如列表、元组等）中的元素拆解并分别赋值给多个变量。

>   在下面的 Demo 中，`info` 是一个包含多个元组的列表。在 `for  `循环中，使用序列解包赋值将每个元组的第一个元素赋值给 `name` 变量，第二个元素赋值给 `home` 变量。

```python
info = [("朱美帅", "宿州"), ("吴仪", "芜湖")]
for name, home in info:
    print(f"My name is {name}, My home is {home}")

>>>
My name is 朱美帅, My home is 宿州
My name is 吴仪, My home is 芜湖
```

#### 4、for 循环示例

**1、遍历字符串。**

```python
my_site = "www.zhums.top"
for url in my_site:
    print(url, end=' ')

>>>
w w w . z h u m s . t o p 
```

**2、打印 `1-100` 的累加**

```python
result = 0
for i in range(101):
    result += i
print(result)

>>>
5050
```

**3、嵌套循环打印九九乘法表。**

```python
for i in range(1, 10):
    for j in range(1, i+1):
        print('%dx%d=%d\t' %(j, i, j*i), end='')
    print()
    
>>>
1x1=1	
1x2=2	2x2=4	
1x3=3	2x3=6	3x3=9	
1x4=4	2x4=8	3x4=12	4x4=16	
1x5=5	2x5=10	3x5=15	4x5=20	5x5=25	
1x6=6	2x6=12	3x6=18	4x6=24	5x6=30	6x6=36	
1x7=7	2x7=14	3x7=21	4x7=28	5x7=35	6x7=42	7x7=49	
1x8=8	2x8=16	3x8=24	4x8=32	5x8=40	6x8=48	7x8=56	8x8=64	
1x9=9	2x9=18	3x9=27	4x9=36	5x9=45	6x9=54	7x9=63	8x9=72	9x9=81
```

## 3、跳转语句

### 1、break

`break` 语句用于强行退出循环体，不再执行循环体中剩余的语句。 

```python
for i in range(1,4):
    if i == 2:
        break 
    print (i)
    
>>>
1
```

### 2、continue

`continue` 语句用于终止执行本次循环，直接从下一次循环继续执行。

```python
for i in range(1,4):
    if i == 2:
        continue
    print (i)

>>>
1
3
```

### 3、pass 关键字

`Python` 中的 `pass` 关键字，用来让解释器跳过此处，什么都不做；放在任何缩进的语句块部分。

```python
if expr1:
    pass
elif expr2:
    pass
else:
    pass
```

## 计算水仙花数

通过 `while` 循环计算出水仙花数。水仙花数是一个三位数，三位数各位的立方之和等于三位数本身。

```python
a = 100; b = c = d =0
while a < 1000:
    b = a // 100
    c = (a % 100) // 10
    d = a % 10
    if (b ** 3 + c ** 3 + d ** 3) == a:
        print (a)
    a += 1

>>>
153
370
371
407
```

# 