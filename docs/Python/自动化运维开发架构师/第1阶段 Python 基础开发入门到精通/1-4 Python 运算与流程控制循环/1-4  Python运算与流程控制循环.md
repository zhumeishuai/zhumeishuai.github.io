## 1.1 Python 运算

### 1.1.1 布尔值

```python
True：非 0 的数字，非空的字符串、列表、元组、字典
False：0、''、()、[]、{}、None
布尔值可以利用逻辑运算符来运算
```

```python
# 空值:空值为 None；None 不能理解为 0；0 是有意义的，None 是一个特殊的空值； 
非 且 或 （执行先后顺序）。
```

```python
# DEMO：

# and 运算，所有条件都符合才为 True
print(True and True)
print(True and False)
print(False and False)
# or 运算，只有其中一个为 True，都为 True
print(True or False)
print(True or True)
print(False or False)
# not 运算
print(not True)
print(not False)

# 执行结果：

True
False
False
True
True
False
False
True
```

### 1.1.2 自增运算

```python
i += 1		# i = i + 1
i -= 1		# i = i - 1
i *= 1		# i = i * 1
i /= 1		# i = i / 1
```

```python
# DEMO：

i = 10
i += 1
print(i)
i -= 1
print(i)
i *= 2
print(i)
i /= 2
print(i)

# 执行结果：

11
10
20
10.0
```

### 1.1.3 比较 < 关系 > 运算符

| 运算符 | 描述                                                       |
| ------ | ---------------------------------------------------------- |
| ==     | 检查两个操作数的值是否相等，若相等则为真                   |
| !=     | 检查两个操作数的值是否不等，若不等则为真                   |
| <>     | 检查两个操作数的值是否相等，若不相等则为真，Python3 中废弃 |
| >      | 检查左操作数的值是否大于右操作数，若大于则为真             |
| <      | 检查左操作数的值是否小于右操作数，若小于则为真             |
| >=     | 检查左操作数的值是否大于或等于右操作数，若是则为真         |
| <=     | 检查左操作数的值是否小于或等于右操作数，若是则为真         |

### 1.1.4 逻辑运算符

| 运算符 | 逻辑表达式 | 描述                                                         |
| ------ | ---------- | ------------------------------------------------------------ |
| and    | x and y    | 布尔"与" 如果 x 为 False，返回 False，否则它返回 y 的计算值  |
| or     | x or y     | 布尔"或" 如果 x 是 True，返回 True，否则它返回 y 的计算值    |
| not    | not x      | 布尔"非" 如果 x 为 True，返回 False ，如果 x 为 False，返回 True |

```python
# DEMO：

print(True or False and False)
print(not False and False)
print(not False and False or True)

# 执行结果：

True
False
True
```

```python
# 执行顺序
not > and > or
```

```python
# 判断是否是闰年

'''
闰年是公历中的名词：
普通年:能被 4 整除但不能被 100 整除的年份为普通闰年。（如 2004 年就是闰年，1999 年不是闰年）； 
世纪年:能被 400 整除的为世纪闰年。（如 2000 年是世纪闰年，1900 年不是世纪闰年）；
'''

year = int(input('Please Input Years：'))
if year % 4 == 0 and year % 100 != 0 or year %400 == 0:
    print('{}是闰年'.format(year))
else:
    print('{}不是闰年'.format(year))
    
# 执行结果：
>>> %Run test.py
Please Input Years：2004
2004是闰年
>>> %Run test.py
Please Input Years：1999
1999不是闰年
>>> %Run test.py
Please Input Years：2000
2000是闰年
>>> %Run test.py
Please Input Years：1900
1900不是闰年
```

## 1.2 Python 流程控制

### 1.2.1 if 判断

```python
# if 语法
if 条件1:
    语句块
elif 条件2:
    语句块
else:
    语句块
```

```python
# DEMO：

age = int(input('Please Input Age：')) 
if age >= 18:
    print('成年')
elif age >=10:
    print('未成年')
else:
    print('小孩子')
    
# 执行结果：

>>> %Run test.py
Please Input Age：18
成年
>>> %Run test.py
Please Input Age：12
未成年
>>> %Run test.py
Please Input Age：5
小孩子
```

**要减少无意义的判断**

```python
# 循环判断
# DEMO：

num = 18
if num < 15:
    if num > 8:
        print('15 > num > 8') 
else:
    print('111')
    if num < 30:
        print('15 < num < 30')

# 执行结果：

111
15 < num < 30
```

### 1.2.2 for 循环

#### 1.2.2.1 for 循环语法

```python
for 变量 in 可迭代对象:
	语句块
```

#### 1.2.2.2 基本 for 循环

```python
range() 函数
'''
说明：返回一个可迭代对象
语法：range(start,stop[,step])
start：开始，默认从 0 开始
stop：结束，但不包括 stop
step：步长，默认为 1
'''
```

```python
# DEMO： 

for i in range(10):
    print(i,end='')
    
# 执行结果：

0123456789
```

#### 1.2.2.3 特殊的 for 循环

```python
# 序列解包赋值
# DEMO：

num = [(1,2),(3,4)]
for i,j in num:
    print('这是 i %s'%i,end=',')
    print('这是 j %s'%j)
    
# 执行结果：

这是 i 1,这是 j 2
这是 i 3,这是 j 4
```

#### 1.2.2.4 嵌套循环

```python
# 语法：
for 条件1:
    语句块
	for 条件2:
        语句块
# 外层循环一次，内层循环一遍
```

```python
# 打印九九乘法表
# DEMO：

for i in range(1,10):
    for j in range(1,i+1):
        print('%dx%d=%d\t'%(j,i,j*i),end='')
    print()
    
# 执行结果：

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

### 1.2.3 while 循环

```python
# while 与 for 不同，for 是一个广度遍历，而 while 是一个深度遍历，while 只要条件满足就会一直执行，直到不满足
```

```python
# Python 中默认的死循环条件为 True
```

#### 1.2.3.1 while 循环语法

```python
while 条件:
    代码块
```

#### 1.2.3.2 基本 while 循环

```python
# DEMO：

i = 1
while i < 5:
    print('I am is for ')
    i += 1
    
# 执行结果：

I am is for 
I am is for 
I am is for 
I am is for 
```

#### 1.2.3.3 while 嵌套

```python
# DEMO：

n = int(input('Please Input Number：'))
i = 1
while i <= n:
    j = 1
    while j <= i:
        print('*',end=' ')
        j += 1
    print()
    i += 1
    
# 执行结果：

Please Input Number：5
* 
* * 
* * * 
* * * * 
* * * * *
```

### 1.2.4 流程控制词

```python
pass		# 放在任何缩进的语句块部分，只是占位
continue	# 提前结束本轮循环，并直接开始下一轮循环
break		# 直接退出循环
注意：不要滥用 break 和 continue 语句。break 和 continue 会造成代码执行逻辑分叉过多容易出错。大多数循环并不需要用到 break 和 continue 语句
```

#### 1.2.4.1 pass 

```python
# DEMO：

name = 'xuegod'
for i in name:
    if i == 'e':
        pass
    print(i,end=' ')

# 执行结果：

x u e g o d 
```

#### 1.2.4.2 break

```python
# DEMO:

name = 'xuegod'
for i in name:
    if i == 'e':
        break
    print(i,end=' ')

# 执行结果：

x u
```

```python
# DEMO：

i = 0
while i < 10:
    i += 1
    if i == 5:
        break
    print(i,end='')
    
# 执行结果：

1234
```

#### 1.2.4.3 continue

```python
# DEMO:

name = 'xuegod'
for i in name:
    if i == 'e':
        continue
    print(i,end=' ')

# 执行结果：

x u g o d
```

```python
# DEMO：

i = 0
while i < 10:
    i += 1
    if i == 5:
        continue
    print(i,end='')

# 执行结果：

1234678910
```

## 1.3 Python 推导式

### 1.3.1 列表推导式

```python
# 列表推导能非常简洁的够早一个新列表
语法：[变量 for 变量 in 可迭代对象]
```

```python
# 生成一个列表，列表中元素为 0-9

# 1、使用 for 循环
list1 = []
for i in range(10):
    list1.append(i)
print(list1)

# 2、使用列表推导式
list1 = [i for i in range(10)]
print(list1)
```

```python
# 使用列表推导式生成 0-9 之间的偶数

list1 = [i for i in range(10) if i %2 ==0]
print(list1)

# 执行结果：
[0, 2, 4, 6, 8]
```

```python
# 现有一列表 L=[[1,2,3],[4,5,6],[7.8,9]] 要求取出元素 1/4/7 和 1/5/9 

L = [[1,2,3],[4,5,6],[7,8,9]]
result = [i[0] for i in L]
print(result)
result2 = [L[i][i] for i in range(len(L))]
print(result2)

# 执行结果：

[1, 4, 7]
[1, 5, 9]
```

```python
# DEMO：

a = [(i,j) for i in range(1,5) for j in range(6,10)] 
print(a)

# 相当于如下 for 循环
# for i in range(1,5):
#     for j in range(6,10):
#         pass

b = [(x,y,z) for x in range(2)for y in range(2)for z in range(2)] 
print(b)

# 执行结果：

[(1, 6), (1, 7), (1, 8), (1, 9), (2, 6), (2, 7), (2, 8), (2, 9), (3, 6), (3, 7), (3, 8), (3, 9), (4, 6), (4, 7), (4, 8), (4, 9)]
[(0, 0, 0), (0, 0, 1), (0, 1, 0), (0, 1, 1), (1, 0, 0), (1, 0, 1), (1, 1, 0), (1, 1, 1)]
```

### 1.3.2 字典推导式

```python
# 字典和集合推导式是该思想的延续，语法差不多，只不过产生的是集合和字典而已
语法： dic1 ={k:v fro k,v in {'name':'hl','age':18}.items()}
```

```python
# DEMO：

dict1 = {k:v for k,v in {'name':'hl','age':18}.items()}
print(dict1)

# 执行结果：

{'name': 'hl', 'age': 18}
```

### 1.3.3 集合推导式

```python
# 集合推导式与列表推导式十分相似，唯一的区别在于用 {} 代替 []
语法： {变量 for 变量 in 可迭代对象}
```

```python
# DEMO：

L = [1,2,3,1,2,3,4]
set1 = {i for i in L}
print(set1)

# 执行结果：

{1, 2, 3, 4}
```

### 1.3.4 元组生成式

```python
# DEMO：

a = (i for i in range(5))
for i in a:
    print(i)
    
# 执行结果：

0
1
2
3
4
```

## 1.4 Python 深浅拷贝及作用

### 1.4.1 深浅拷贝定义

```python
# 深拷贝
	拷贝所有对象，包括顶级对象以及嵌套对相关，所以原始对象的改变不会造成深拷贝里任何子元素的改变
# 浅拷贝
	只拷贝顶级对象，没有拷贝嵌套对象，所以原始数据改变，嵌套对象会变
```

```python
# 应用场景：
	比如在 CMDB 系统中，我们定义了一个报警模板 call 给所有的服务器使用，此时有一批特殊应用的服务器需要不同的报警参数，我们既不想单独新建模板来一个一个添加报警参数，又不想修改默认模板而影响其他机器的报警阈值。此时我们就需要用深拷贝来完成
    我们在维护服务器信息的时候，经常要更新服务器信息，这时我们重新一个一个添加时比较麻烦的，我们可以把原始数据类型拷贝一份，在它的基础上做修改
```

```python
# DEMO：

import copy
a = [1,2,3,4,[5,6,7,9,10]]
b = a
print('a 的ID是：%d'%id(a))
print('b 的ID是：%d'%id(b))
c = copy.copy(a)
print('c 的ID是：%d'%id(c))
d = copy.deepcopy(a)
print('c 的ID是：%d'%id(d))
a.append(8)
a[4].append(9)
print(a)
print(b)

# 执行结果：

a 的ID是：1843826884104
b 的ID是：1843826884104
c 的ID是：1843826879944
c 的ID是：1843826882504
[1, 2, 3, 4, [5, 6, 7, 9, 10, 9], 8]
[1, 2, 3, 4, [5, 6, 7, 9, 10, 9], 8]
```

## 1.5 作业

```python
1、给你一个字符串例如：’abcsadfadsfgfegegegea’，经过计算返回一个字典，字典中包含每个元素当中的个数，结合if 判断，for 循环，完成本次代码！
    例如：‘abb’        {‘a’:1,’b’:2}
2、输入任意行文字，存亍列表L中,当丌输入任何容直接回车后结束输入
    1. 打印L列表中的内容
    2. 计算您共输入了几行内容
    3. 计算您共输入了多少个字符 
```

