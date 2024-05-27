## 1.1 递归函数

### 1.1.1 递归函数的定义

```python
# 如果一个函数在内部调用本身，那么这个函数就是递归函数，递归函数会形成一个深度循环！
```

### 1.1.2 递归函数的使用

```python
# 计算阶乘
# 方法一：
n = int(input('Please enter the Num：'))
result = 1
i = 1
while i <= n:
    result *= i
    i += 1
print(result)

# 方法二：
def func(n):
    if n == 1:
        return 1
    return n * func(n-1)
while True:
    n = int(input('Please enter the Num：'))
    print(func(n))
    if n > 10:
        break
```

### 1.1.3 斐波那契数列 < 面试 >

```python
题目：斐波那契数列，该数列中有 n 个数字，112358
分析：该数列中，从第三个数开始：数值=前一个数字+前二个数字
```

```python
# 方法一：
def feibo(n):
    a,b = 0,1
    c = []
    while n > 0:
        c.append(b)
        a,b = b,a+b
        n -= 1
    print(c)
feibo(5)
```

```python
# 方法二：
def feibo(n):
    if n <= 1 or n == 2:
        return 1;
    return (feibo(n-1) + feibo(n-2))
n = int(input("Please enter the Number:"))
list1 = [feibo(i) for i in range(1,n+1)]
print(list1)
```

```python
总结：
1、明显看到递归函数的优点：定义简单，逻辑清晰
2、实际上递归都可以使用循环来代替
```

### 1.1.4 栈溢出

```python
栈溢出：在计算机中，函数调用时通过栈 < stack > 这种数据结构实现的，每当进入一个函数调用，栈就会加一层栈帧，每当函数返回，栈就会减一层栈帧。由于栈的大小不是无限的，所以递归调用的次数过多，会导致栈溢出
```

```python
# 解决栈溢出的方法：尾递归
# 在函数返回的时候，调用自身本身，并且 return 语句不能包含任何表达式。这样，编译器戒者解释器就可以把尾递归做优化，使递归本身无论调用多少次，都只占用一个栈帧，不会出现栈溢出的情况。
def func(n):
    return test(n,1)    
def test(num,product):
    if num == 1:
        return product
    return test(num - 1,num * product) 
print(func(4))
# 很遗憾的是：对于大部分语言来说都没有对尾递归进行优化，Python 同样也是。
```

## 1.2 闭包

### 1.2.1 闭包定义

```python
1、闭包函数必须有内嵌函数
2、内嵌函数可以引用该嵌套函数上一级命名空间 < namespace > 中的变量
3、闭包函数必须返回内嵌函数
```

Python 装饰器就是使用了闭包

```python
# DEMO:

def outer():
    def inner():
        print('This is Inner')
    return inner
outer()()

# 执行结果：

This is Inner
```

```python
# 闭包的好处：
1、使代码变得简洁
2、提高代码的拓展性
```

### 1.2.2 闭包分析

```python
def outer(num):		# num=20
    def inner(num_in):	# num_in=200
        print('inner,num_in is %d'%num_in)	# num_in=200
        return num + num_in	# 220
    return inner
a = outer(20)	# a=inner
print(a(200))	# a(200)=inner(200)

# 执行结果：

inner,num_in is 200
220
```

## 1.3 装饰器

### 1.3.1 装饰器定义

```python
装饰器是程序开发中经常用到的功能，用于在原有的函数上增添新的代码需求
```

```python
# 应用场景：
1、当我们写好一个函数时，项目也已经上线了，突然客户想要增添一个需求，让这个函数处理的更加细致，这个时候就可以用到装饰器了
2、淘宝登录验证
3、log 日志
```

```python
# 执行顺序：
先返回内嵌函数 >> 有参数直接传参给内嵌函数 >> 执行内嵌函数
```

```python
# 定义两个函数，分别打印它们的名字
def func1():
    print('this is xuegod1')
def func2():
    print('this is xuegod2')
func1()
func2()

# 执行结果：

this is xuegod1
this is xuegod2
```

```python
# 现在要对两个函数做修改，增加打印他们的国家

def outer(func):
    def inner():
        func()
        print('come from china')
    return inner
@outer	
# 等同与 func1 = outer(func1)，第一个func1为了接收返回的inner，第二个func1是func1()函数作为一个实参传递给形参func

def func1():
    print('this is xuegod1')
@outer
def func2():
    print('this is xuegod2')
func1()
func2()

# 执行结果：

this is xuegod1
come from china
this is xuegod2
come from china
```

```python
# 在闭包函数中传递参数，然后让 func1 获取到我们传递的值

def outer(func):
    def inner(name):
        func(name)
        print('inner中的%s'%name)
    return inner
@outer # func1 = outer(func1)
def func1(name): # name='for'
    print('this is xuegod1')
    print('I am %s'%name)
func1('for')

# 执行结果：

this is xuegod1
I am for
inner中的for
```

```python
# 更通用的装饰器

def outer(func): # func=func1
    def inner(*args,**kwargs): # args=5,kwargs=5
        c = func(*args,**kwargs) # func1(5,5),c=25
        print(c)
    return inner
@outer # outer(func1)
def func1(a,b=2):  # a=5,b=5
    return a * b
func1(5,5)  # inner(5,5)

# 执行结果：

25
```

## 1.4 实战

```python
# 模拟淘宝加入购物车时我们进行客户登录验证
import time
list1 = ['hl','zsy','zms']
def outer(func): # func=login
    def inner(name): # name='zms'
        func(name) # login('zms')
        print('开始判断有没有登录')
        time.sleep(2)
        if name in list1: # True
            print('已经登录')
            time.sleep(1)
        else:
            print('你没有登录')
            time.sleep(1)
    return inner
@outer  # outer(login),inner
def login(name): # name='zms'
    print('%s 要浏览'%name) # name='zms'
@outer
def goods_cart(name):
    print('%s 要加入购物车'%name)
login('zms') # inner('zms')
goods_cart('for')

# 执行结果：

zms 要浏览
开始判断有没有登录
已经登录
for 要加入购物车
开始判断有没有登录
你没有登录
```





