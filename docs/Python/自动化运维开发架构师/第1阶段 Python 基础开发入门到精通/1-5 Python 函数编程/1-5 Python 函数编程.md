## 1.1 函数的定义

### 1.1.1 Python 函数的定义

```python
# 函数 < function >：是一个可以被重复调用的带有入口和一个出口的固定的程序块
# 函数的定义：< function > 代码块，计算机的函数，是一个固定的一个程序段，或称其为一个子程序，它在可以实现固定运算功能的同事，还带有一个入口和一个出口，所谓的出口，就是函数所带的各个参数，我们可以通过这个入口，把函数的参数值代入子程序，供计算机处理；所谓出口，就是指函数的函数值，在计算机求得之后，由此口带回给调用它的程序
简单说就是将我们要执行的代码进行结构的整合，形成可被重复调用的代码块
```

```python
# 函数的优点：
    1、减少冗余代码
    2、代码结构清晰
    3、保持代码的一致性
```

```python
# 函数的编写：
# 语法：
	def 函数名 (参数):
        '函数参数'
        代码块
        return
# 函数名命名规范：
    1、字母开头
    2、不允许有关键字
    3、不允许有特殊符号
    4、不允许莫名其妙的函数名
    5、参数：参数是定义在参数括号里，由调用时传入，作用在函数内部的变量
    6、如果有参数，写在参照括号里
    7、如果没有参数，写空括号
```

## 1.2 函数的调用

### 1.2.1 函数调用

函数在没有被调用前不会执行

```python
函数名加小括号，若参照括号中有参数的情况下，要对应传参
在定义函数的参照括号内定义的参数，称之为形参
在调用参数的时我们传递的值，称之为实参
```

```python
# DEMO：

def func (age):
    print('zsy is yyds')
    return age + 2
print(func)    # 函数所在的内存地址
func(17)
age = func(17)
print(age)

# 执行结果：

<function func at 0x000001E09D547D08>
zsy is yyds
zsy is yyds
19
```

## 1.3 函数的划分

按照参数类型分类：位置参数、关键字参数、默认参数、参数组

### 1.3.1 位置参数

```python
在传参时，实参传递的顺序按照形参按照形参定义的顺序进行传递
```

```python
# DEMO：

def func (name,city):
    print('I am %s,I am from %s'%(name,city))

func('zms','hefei')

# 执行结果：

I am zms,I am from hefei
```

### 1.3.2 关键字参数

```python
在传参时，以形参等于实参的形式忽略形参定义的顺序进行传参
Python 解释器能够用参数名匹配参数值
```

```python
# DEMO：

def func (name,city):
    print('I am %s,I am from %s'%(name,city))

func(city = 'hefei',name='zms')

# 执行结果：

I am zms,I am from hefei
```

### 1.3.3 默认值参数 < 面试题 >

```python
在定义参数时，给形参一个默认值，在我们调用函数的时候，如果不给有默认值的形参传参时，自动采用默认值
```

```python
# 注意：默认参数必须写在正常参数的后面
```

```python
# DEMO：

def func (name,city='China'):
    print('I am %s,I am from %s'%(name,city))

func('zms')

# 执行结果：

I am zms,I am from China
```

### 1.3.4 参数组 < 面试题 >

```python
处理比声明时更多的参数，会将传入的参数变成元组 < *args > 或字典 < **kwargs > 声明时不用命名
```

#### 1.3.4.1 元组参数组

```python
# 通过给形参前添加 * 使参数变成一个元组，所有传递的参数变成元组的元素
```

```python
# DEMO：

def func (*args):
    print(args)
    print('I am %s,I am from %s'%(args[0],args[1]))
func(1,2)
func(3,4,5)

# 执行结果：

(1, 2)
I am 1,I am from 2
(3, 4, 5)
I am 3,I am from 4
```

#### 1.3.4.2 字典参数组

```python
# 通过给形参前添加 ** 使参数变成一个字典，所有传递的参数变成字典的键值对，这里传参要求键等于值的形式
```

```python
# DEMO：

def func (**kwargs):
    print(kwargs)
    print('I am %s,I am from %s'%(kwargs['name'],kwargs['city']))
func(name = 'zms',city = 'hefei')

# 执行结果：

{'name': 'zms', 'city': 'hefei'}
I am zms,I am from hefei
```

```python
# 案例

def say_hello(c,d,e=3,*args,**kwargs):
    a = args 
    b = kwargs 
    print(a,b)
say_hello(1,2,3,4,5,6,a = 1)

# 执行结果：

(4, 5, 6) {'a': 1}
```

```python
# 参数的定义顺序
Python2：必选参数、默认参数、可变参数、关键字参数
Python3：可变参数可以写在默认参数前面
```

## 1.4 匿名函数

```python
	Lambda 函数，即 Lambda 表达式 < lambda expression > 是一个匿名函数 < 不存在函数名的函数 > Lambda 表达式基于数学中的入演算得名，直接对应于其中的 lambda 抽象 < Lambda abstraction > 
```

```python
优点：
1、lambda 函数比较轻便，即用即删除，很适合需要完成一项功能，但是此功能只在此一处使用，连名字都很随意的情况下
2、匿名函数，一般用来给 filter、 map 这样的函数式变成服务
3、作为回调函数，传递给某些应用，比如消息处理
4、不用考虑命名冲突问题
```

### 1.4.1 Lambda

```python
语法： lambda 参数:表达式(block)
参数： 可选，通常以逗号分隔的变量表达式形式，也就是位置参数
表达式： 不能包含循环、 return、 elif、 可以包含 if
```

```python
# DEMO：

L = lambda x:x*x
print(L)
print(L(2))
# 相当于如下函数
def l (x):
    return x*x
print(l(2))
A = lambda x:'x>10' if x> 10 else 'x<=10'
print(A(11))
# 相当于如下函数
def a (x):
    if x > 10:
        return 'x>10'
    else:
        return 'x<=10'
print(a(11))

# 执行结果：

<function <lambda> at 0x000002B097C37D08>
4
4
x>10
x>10
```

```python
# 注意：在 Python2 中 lambda 不支持 print，但在 Python3 中支持 print
```

### 1.4.2 map()

```python
'''
语法：map(函数,可迭代对象)
说明：map() 是 Python 的内置函数，它接受一个函数和一个可迭代对象，并通过函数一次作用在可迭代对象的每一个元素上，得到一个新的对象
'''
```

```python
# DEMO：

# 对一个列表中的元素进行平算
list1 = [1,2,3,4]
list2 = []
# 普通函数的写法
def func(x):
    return x*x
for i in list1:
    list2.append(func(i))
print(list2)

# map() 的写法
list1 = [1,2,3,4]
def func(x):
    return x*x
list2 = map(func,list1)
print(list(list2))
# lambda 的写法
list1 = [1,2,3,4]
list2 = map(lambda x:x*x,list1)
print(list(list2))

# 执行结果：

[1, 4, 9, 16]
[1, 4, 9, 16]
[1, 4, 9, 16]
```

```python
# 练习：
# 给定两个列表 a=[1,2,3] b=[4,5,6] 把两者中每个元素的数值相加在一起，即 c=[5,7,9]

a = [1,2,3]
b = [4,5,6]
c = map(lambda x,y:x+y,a,b)
print(list(c))

# 执行结果：

[5, 7, 9]
```

**注意：**即使 lambda 简洁好用，但不建议滥用

1. 好多人觉得方便，容易滥用
2. 用多了，程序的可读性很差
3. 每个人对抽象层级的接受和忍耐不同

## 1.5 函数作用域

```python
# 函数作用域即变量起作用的范围
```

### 1.5.1 作用域分类

```python
1、local 局部作用域，本地作用域 < L >
2、enclosing 嵌套作用域 < E >
3、global 全局作用域 < G >
4、built-in 内建作用域 < B >
```

```python
for if while 这些流程控制不会形成自己的作用域
```

```python
import sys		# 得到所有该模块的方法，内建作用域
print(dir(sys))
```

```python
# DEMO：

name = 'while'    # 全局作用域
def outer():
    name = 'hl'    # 嵌套作用域
    def inner():
        name = 'zms'    # 本地作用域
        age = 18
        print(name,age)
    inner()
outer()

# 执行结果：

zms 18
```

```python
# 局部变量，全局变量
局部变量指在程序中只在特定过程或函数中可以访问的变量
如果一个变量既可以在函数中使用，也可以在其它函数中使用，这样的变量就叫全局变量
```

```python
# 总结：
局部变量，就是定义在函数内部的变量
不同的函数，可以定义相同名字的局部变量，互不影响
局部变量的作用是为了临时保存数据，需要在函数中定义进行存储
```

### 1.5.2 声明变量

```python
global		# 声明全局变量
nonlocal	# 声明非本地变量
```

```python
# global 声明，函数内部调用全局变量

name = 'while'    
def outer():
    name = 'hl'    
    def inner():
        global name
        age = 18
        print(name,age)
    inner()
outer()

# 执行结果：

while 18
```

```python
# global 声明，函数内部操作全局变量

name = 'while'    
def outer():
    name = 'hl'    
    def inner():
        global name
        name = 'zms'
        age = 18
        print(name,age)
    inner()
outer()
print(name)

# 执行结果：

zms 18
zms
```

```python
# nonlocaL 声明，函数内部操作父函数内变量

name = 'while'    
def outer():
    name = 'hl'    
    def inner():
        nonlocal name
        name = 'zms'
        age = 18
        print(name,age)
    inner()
    print(name)
outer()

# 执行结果：

zms 18
zms
```

```python
# 变量的查找遵循 '就近原则'，由内到外的查找
```

```python
# 如果是可变类型的数据，即不用声明 global
```

```python
# DEMO:

a = [1,2,3]
b = {}
c = set()
def func():
    a.append(4)
    b.update({'name':'hl'})
    c.add('zsy')
func()
print(a,b,c)

# 执行结果：

[1, 2, 3, 4] {'name': 'hl'} {'zsy'}
```

```python
# 总结：
	在函数中不适用 global 声明全局变量时不能修改全局变量，其本质是不能修改全局变量的指向，即不能将全局变量指向新的数据
    对于不可变类型的全局变量来说，因其指定的数据不能修改，所以不使用 global 无法修改全局变量
    对于可变类型的全局变量来说，因其指向的数据可以修改，所以不使用 global 也可以修改全局变量
```

## 1.6 偏导数

```python
# 应用场景：
	函数在执行时，要带上所有必要的参数进行调用。然后有时参数可以在函数被调用之前提前获知。这种情况下，一个函数有一个或多个参数预先就能用上，以便函数能用更少的参数进行调用
```

```python
# DEMO：

import functools
def add(a,b):
    print('a:%d,b:%d'%(a,b))
    return a + b
plus3 = functools.partial(add,3)
plus5 = functools.partial(add,5)
print(plus3(2))
print(plus5(3))

# 执行结果：

a:3,b:2
5
a:5,b:3
8
```

## 1.7 实战

```python
# 利用函数式编程，爬取百度图片
```

## 1.8 作业

```python
1、A = ['a','b','c'] B = ['d','e','f'] 利用 map()，lambda 生成一个新的列表 C = ['ad', 'be', 'cf']

A = ['a','b','c']
B = ['d','e','f']
C = map(lambda x,y:x+y,A,B)
print(list(C))
```

