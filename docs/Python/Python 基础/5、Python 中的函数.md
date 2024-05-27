## 1、Python 函数基本使用

`Python` 函数支持接收多个（ `≥0` ）参数，`Python` 函数还支持返回多个（ `≥0` ）值。

### 1、Python 函数的定义

定义函数通过 `def` 关键字实现，具体语法如下:

```python
def Function_Name ([Args1][, Argsn]):
    Code
    ...
    [return [Return_Value]]
```

-   `Function_Name`: 函数名，符合 Python 规则的标识符
-   `Argsn`: 形参列表
-   `[return [Return_Value]]`: 指定函数的返回值

```python
def Pass_Test():		# 定义空函数
    pass
def Return_Hello():		# 返回字符串 'hello'
    return 'hello'
f_pass = Pass_Test()
info = Return_Hello()
print(f_pass)
print(info)
```

### 2、Python 函数的调用

函数调用的基本语法如下:

```python
[Var_Name] = Function_Name([Args_List])
```

-   `Var_Name`: 定义变量用于接收函数的返回值
-   `Funciton_Name`: 函数名
-   `Args_List`: 参数列表

>**注意：**创建函数有多少个形参，那么调用时就需要传入多少个值，且顺序必须和创建函数时一致。即便该函数没有参数，函数名后的小括号也不能省略。

```python
def Return_Info(info):
    return info
Msg = Return_Info("This is test args")
print(Msg)

>>>
This is test args
```

### 3、为函数提供说明文档

通过调用 `Python` 的 `help()` 内置函数或 `__doc__` 属性，可以查看某个函数的使用说明文档。事实上，无论是 `Python` 提供给我们的函数，还是自定义的函数，其说明文档都需要设计该函数的程序员自己编写。

其实，函数的说明文档，本质就是一段字符串，只不过作为说明文档，字符串的放置位置是有讲究的，函数的说明文档通常位于函数内部、所有代码的最前面。

```python
def Return_Info(info):
    '''
    返回给定的参数值。
    '''
    return info
help(Return_Info)
print(Return_Info.__doc__)

>>>
Help on function Return_Info in module __main__:

Return_Info(info)
    返回给定的参数值。


    返回给定的参数值。
```

## 2、Python 函数的参数

### 1、Python 函数值传递和引用传递

通常情况下，定义函数时都会选择有参数的函数形式，函数参数的作用是传递数据给函数，令其对接收的数据做具体的操作处理。

在使用函数时，经常会用到形式参数（简称 "形参"）和实际参数（简称 "实参"），二者都叫参数，之间的区别是：

-   形式参数：在定义函数时，函数名后面括号中的参数就是形式参数，例如:

    ```python
    # 定义函数时，这里的函数参数 obj 就是形式参数
    def demo(obj):
        print(obj)
    ```

-   实际参数：在调用函数时，函数名后面括号中的参数称为实际参数，也就是函数的调用者给函数的参数。例如:

    ```python
    a = "C语言中文网"
    # 调用已经定义好的 demo 函数，此时传入的函数参数 a 就是实际参数
    demo(a)
    ```

>   实参和形参的区别，就如同剧本选主角，剧本中的角色相当于形参，而演角色的演员就相当于实参。

**实参是如何传递给形参？**

`Python` 中，根据实参的类型不同，函数参数的传递方式可分为 `2` 种，分别为值传递和引用（地址）传递：

-   值传递：适用于实参类型为不可变类型（字符串、数字、元组）
-   引用（地址）传递：适用于实参类型为可变类型（列表，字典）

值传递和引用传递的区别在于: 函数参数进行值传递后，若形参的值发生改变，不会影响实参的值；而函数参数继续引用传递后，改变形参的值，实参的值也会一同改变。

```python
def demo(obj) :
    obj += obj
    print("形参值为：", obj)
print("--- 值传递 ---")
a = "Python"
demo(a)
print("实参值为：", a)

print("--- 引用传递 ---")
a = [1, 2, 3]
demo(a)
print("实参值为：", a)

>>>
--- 值传递 ---
形参值为： PythonPython
实参值为： Python
--- 引用传递 ---
形参值为： [1, 2, 3, 1, 2, 3]
实参值为： [1, 2, 3, 1, 2, 3]
```

>通过上面的执行结果不难看出，在执行值传递时，改变形式参数的值，实际参数并不会发生改变；而在进行引用传递时，改变形式参数的值，实际参数也会发生同样的改变。

>   对于函数传递的方法，可阅读 [Python 函数参数传递机制（超级详细）](http://c.biancheng.net/view/2258.html) 深入探究其原因。

### 2、Python 位置参数

位置参数，有时也称必备参数，指的是必须按照正确的顺序将实际参数传到函数中，换句话说，调用函数时传入实际参数的数量和位置都必须和定义函数时保持一致。

实参和形参数量必须一致

在调用函数，指定的实际参数的数量，必须和形式参数的数量一致（传多传少都不行），否则 `Python` 解释器会抛出 `TypeError` 异常，并提示缺少必要的位置参数

```python
def func (name,city):
    print('I am %s,I am from %s'%(name,city))

func('zhums','hefei')

>>>
I am zhums,I am from hefei
```

### 3、Python 关键字参数

关键字参数，可以避免牢记参数位置的麻烦，令函数的调用和参数传递更加灵活方便。

关键字参数是指使用形式参数的名字来确定输入的参数值。通过此方式指定函数实参时，不再需要与形参的位置完全一致，只要将参数名写正确即可。

>   因此`Python`函数的参数名应该具有更好的语义，这样程序可以立刻明确传入函数的每个参数的含义。

```python
def Func_Info(name, age):
    print("name:", name)
    print("age:", age)
# 位置参数
Func_Info("zhums", 22)
# 关键字参数
Func_Info("wuyi", age=19)
Func_Info(age=19, name='zhaosy')

>>>
name: zhums
age: 22
name: wuyi
age: 19
name: zhaosy
age: 19
```

函数调用时，关键字参数必须跟在位置参数后面。所有传递的关键字参数都必须匹配一个函数接受的参数（，关键字参数的顺序并不重要。这也包括必选参数。

```python
def Func_Info(name, age):
    print("name:", name)
    print("age:", age)
Func_Info(name="zhums", 21)

>>>
Traceback (most recent call last):
  File "C:\Users\Administrator\Desktop\Demo\python\test.py", line 4
    Func_Info(name="zhums", 21)
                              ^
SyntaxError: positional argument follows keyword argument
```

### 4、Python 默认参数

在调用函数时如果不指定某个参数，`Python` 解释器会抛出异常。为了解决这个问题，`Python` 允许为参数设置默认值，即在定义函数时，直接给形式参数指定一个默认值。这样的话，即便调用函数时没有给拥有默认值的形参传递参数，该参数可以直接使用定义函数时设置的默认值。

`Python` 定义带有默认值参数的函数，其语法格式如下：

```python
def Function_Name(Args1, Args2=Default_Value)：
    codes
```

>   **注意:** 使用此格式定义函数时，指定有默认值的形式参数必须在所有没默认值参数的最后，否则会产生语法错误。

```python
def Info(age=18, name):
    pass
    
>>>
Traceback (most recent call last):
  File "C:\Users\Administrator\Desktop\Demo\python\test.py", line 1
    def Info(age=18, name):
                     ^^^^
SyntaxError: non-default argument follows default argument
```

```python
def Info(name, age=18):
    print("name:", name)
    print("age:", age)
Info('zhums', 21)
Info('wuyi')

>>>
name: zhums
age: 21
name: wuyi
age: 18
```

在 `Pyhton` 中，可以使用 `Function_Name.__defaults__` 查看函数的默认值参数的当前值，其返回值是一个元组。以上面的 `Info()` 函数为例，在其基础上，执行如下代码：

```python
def Info(name, age=18):
    pass
print(Info.__defaults__)

>>>
(18,)
```

### 5、参数组

#### 1、元组参数组

通过给形参前添加 `*` 使参数变成一个元组，所有传递的参数变成元组的元素

```python
def func(*args):
    print(args)
    print(args[0], args[1])
func(1, 2)
func(1, 2, 3)

>>>
(1, 2)
1 2
(1, 2, 3)
1 2
```

#### 2、字典参数组

通过给形参前添加 `**` 使参数变成一个字典，所有传递的参数变成字典的键值对，这里传参要求键等于值的形式

```python
def func(**args):
    print(args)
    print(args['name'], args['age'])
func(name = 'zhums', age = 20)

>>>
{'name': 'zhums', 'age': 20}
zhums 20
```

## 3、Python 函数的返回值

### 1、return 函数返回值

在 Python 中，用 def 语句创建函数时，可以用 `return` 语句指定应该返回的值，该返回值可以是任意类型。需要注意的是，`return` 语句在同一函数中可以出现多次，但只要有一个得到执行，就会直接结束函数的执行。

函数中，使用 return 语句的语法格式如下：

```python
return [Return_Value]
```

-   Return_Value：返回值默认 None

通过 `return` 语句指定返回值后，在调用函数时，既可以将该函数赋值给一个变量，用变量保存函数的返回值，也可以将函数再作为某个函数的实际参数。

```python
def add(a,b):
    c = a + b
    return c
c = add(3,4)		# 函数赋值给变量
print(c)
print(add(3,4))		# 函数返回值作为其他函数的实际参数

>>>
7
7
```

函数中可以同时包含多个 `return` 语句，但需要注意的是，最终真正执行的做多只有 `1` 个，且一旦执行，函数运行会立即结束。

```python
def isGreater0(x):
    if x > 0:
        return True
    else:
        return False
print(isGreater0(5))
print(isGreater0(0))

>>>
True
False
```

## 4、Python 变量的作用域

所谓作用域，就是变量的有效范围，就是变量可以在哪个范围以内使用。有些变量可以在整段代码的任意位置使用，有些变量只能在函数内部使用，有些变量只能在 for 循环内部使用。

变量的作用域由变量的定义位置决定，在不同位置定义的变量，它的作用域是不一样的。

### 1、局部变量

在函数内部定义的变量，它的作用域也仅限于函数内部，出了函数就不能使用了，这样的变量称为局部变量（Local Variable）。

>   当函数被执行时，Python 会为其分配一块临时的存储空间，所有在函数内部定义的变量，都会存储在这块空间中。而在函数执行完毕后，这块临时存储空间随即会被释放并回收，该空间中存储的变量自然也就无法再被使用。

可以看到，如果在函数外部访问其内部定义的变量，Python 解释器会报 NameError 错误，并提示我们没有定义要访问的变量，这也证实了当函数执行完毕后，其内部定义的变量会被销毁并回收。

```python
def demo():
    add = "zhums.top"
    print("函数内部 add =", add)
demo()
print("函数外部 add =",add)

>>>
函数内部 add = zhums.top
Traceback (most recent call last):
  File "C:\Users\Administrator\Desktop\Demo\python\test.py", line 5, in <module>
    print("函数外部 add =",add)
NameError: name 'add' is not defined
```

函数的参数也属于局部变量，只能在函数内部使用。

```python
def demo(name,add):
    print("函数内部 name =",name)
    print("函数内部 add =",add)
demo("zhums","www.zhums.top")
print("函数外部 name =",name)
print("函数外部 add =",add)

>>>
函数内部 name = zhums
函数内部 add = www.zhums.top
Traceback (most recent call last):
  File "C:\Users\Administrator\Desktop\Demo\python\test.py", line 5, in <module>
    print("函数外部 name =",name)
NameError: name 'name' is not defined
```

### 2、全局变量

在所有函数的外部定义变量，这样的变量称为全局变量（Global Variable）。和局部变量不同，全局变量的默认作用域是整个程序，即全局变量既可以在各个函数的外部使用，也可以在各函数内部使用。

定义全局变量的方式有以下 2 种：

1.  在函数体外定义的变量，一定是全局变量。

    ```python
    name = 'zhums'
    def text():
        print("函数内部：", name)
    ```

2.  在函数体内定义全局变量。即使用 global 关键字对变量进行修饰后，该变量就会变为全局变量。

    ```python
    def text():
        global name
        name = 'zhums'
    text()
    ```

    >   注意：在使用 `global` 关键字修饰变量名时，不能直接给变量赋初值，否则会引发语法错误。

### 3、获取指定作用域中的变量

在一些特定场景中，可能需要获取某个作用域内（全局范围内或者局部范围内）所有的变量，Python 提供了以下 3 种方式：

1.  globals() 函数
2.  locals() 函数
3.  vars(Object) 函数

#### 1、globals() 函数

`globals()` 函数为 Python 的内置函数，它可以返回一个包含全局范围内所有变量的字典，该字典中的每个键值对，键为变量名，值为该变量的值。

```python
global_name = "人生苦短，我用 Python"
def text():
    name = "zhums"
print(globals())

>>> %Run test.py
{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <_frozen_importlib_external.SourceFileLoader object at 0x000001F83BC84730>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>, '__file__': 'C:\\Users\\Administrator\\Desktop\\Demo\\python\\test.py', 'global_name': '人生苦短，我用 Python', 'text': <function text at 0x000001F83C499A20>}ss
```

通过调用 `globals()` 函数，可以得到一个包含所有全局变量的字典。并且可以通过该字典访问指定变量，还可以修改它的值。例如：

```python
global_name = "人生苦短，我用 Python"
def text():
    name = "zhums"
print(globals()['global_name'])
globals()['global_name'] = "Python YYDS"
print(global_name)

>>>s
人生苦短，我用 Python
Python YYDS
```

#### 2、locals() 函数

`locals()` 函数也是 Python 内置函数之一，调用该函数可以得到一个包含当前作用域内所有变量的字典。

```python
global_name = "Python"
def text():
    local_name = "Shell"
    print("函数内部的 locals:")
    print(locals())
text()
print("函数外部的 locals:")
print(locals())

>>>
函数内部的 locals:
{'local_name': 'Shell'}
函数外部的 locals:
{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <_frozen_importlib_external.SourceFileLoader object at 0x0000018947E24730>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>, '__file__': 'C:\\Users\\Administrator\\Desktop\\Demo\\python\\test.py', 'global_name': 'Python', 'text': <function text at 0x0000018948649A20>}
```

>   注意：当使用 `locals()` 函数获得所有局部变量组成的字典时，可以向 `globals()` 函数那样，通过指定键访问对应的变量值，但无法对变量值做修改。

```python
def text():
    Shename = "shell教程"
    print(locals()['Shename'])
    locals()['Shename'] = "Python"
    print(Shename)
text()

>>>
shell教程
shell教程
```

#### 3、vars(Object) 函数

`vars()` 函数是 Python 内置函数，其功能是返回一个指定 `object` 对象范围内所有变量组成的字典。如果不传入 `object` 参数，`vars()` 和 `locals()` 的作用完全相同。

```python
global_name = "Python"
class Demo:
    local_name = "Shell"
print("有 object：")
print(vars(Demo))
print("无 object：")
print(vars())

>>>
有 object：
{'__module__': '__main__', 'local_name': 'Shell', '__dict__': <attribute '__dict__' of 'Demo' objects>, '__weakref__': <attribute '__weakref__' of 'Demo' objects>, '__doc__': None}
无 object：
{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <_frozen_importlib_external.SourceFileLoader object at 0x00000209C1394730>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>, '__file__': 'C:\\Users\\Administrator\\Desktop\\Demo\\python\\test.py', 'global_name': 'Python', 'Demo': <class '__main__.Demo'>}
```

## 5、Python 局部函数

在 Python 的函数中再定义函数，此类函数称为局部函数。

首先，和局部变量一样，默认情况下局部函数只能在其所在函数的作用域内使用。举个例子：

```python
def outdef ():		# 全局函数
    def indef():	# 局部函数
        print("www.zhums.top")
    indef()		# 调用局部函数
outdef()		# 调用全局函数

>>>
www.zhums.top
```

如同全局函数返回其局部变量，就可以扩大该变量的作用域一样，通过将局部函数作为所在函数的返回值，也可以扩大局部函数的使用范围。例如:

```python
def outdef ():		# 全局函数
    def indef():    # 局部函数
        print("调用局部函数")
    return indef    # 调用局部函数
new_indef = outdef()	# 调用全局函数
new_indef()				# 调用全局函数中的局部函数

>>>
调用局部函数
```

>   因此，对于局部函数的作用域，可以总结为：如果所在函数没有返回局部函数，则局部函数的可用范围仅限于所在函数内部；反之，如果所在函数将局部函数作为返回值，则局部函数的作用域就会扩大，既可以在所在函数内部使用，也可以在所在函数的作用域中使用。
>
>   以上面程序中的 outdef() 和 indef() 为例，如果 outdef() 不将 indef 作为返回值，则 indef() 只能在 outdef() 函数内部使用；反之，则 indef() 函数既可以在 outdef() 函数内部使用，也可以在 outdef() 函数的作用域，也就是全局范围内使用。

如果局部函数中定义有和所在函数中变量同名的变量，也会发生 "遮蔽" 的问题。如：

```python
def outdef ():		# 全局函数
    name = "所在函数中定义的 name 变量"
    def indef():    # 局部函数
        print(name)
        name = "局部函数中定义的 name 变量"
    indef()
outdef()		# 调用全局函数

>>>
UnboundLocalError: local variable 'name' referenced before assignment
```

此错误直译过来的意思是 "局部变量 name 还没定义就使用"。导致该错误的原因就在于，局部函数 indef() 中定义的 name 变量遮蔽了所在函数 outdef() 中定义的 name 变量。再加上，indef() 函数中 name 变量的定义位于 print() 输出语句之后，导致 print(name) 语句在执行时找不到定义的 name 变量，因此程序报错。

由于这里的 name 变量也是局部变量，因此前面章节讲解的 `globals()` 函数或者 `globals` 关键字，并不适用于解决此问题。这里可以使用 Python 提供的 `nonlocal` 关键字。

例如，修改上面程序为：

```python
def outdef ():		# 全局函数
    name = "所在函数中定义的 name 变量"
    def indef():    # 局部函数
        nonlocal name
        print(name)
        name = "局部函数中定义的 name 变量"	# 修改 name 变量的值
    indef()
outdef()	# 调用全局函数

>>>
所在函数中定义的 name 变量
```

## 6、Python 的闭包函数

[Python闭包（Closure）详解 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/453787908)

[深入浅出python闭包 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/22229197)

### 1、Python 闭包

闭包，又称闭包函数或者闭合函数，与嵌套函数类似，不同之处在于，闭包中外部函数返回的不是一个具体的值，而是一个函数。一般情况下，返回的函数会赋值给一个变量，这个变量可以在后面被继续执行调用。

例如，计算一个数的 `n` 次幂，用闭包可以写成下面的代码：

```python
# 闭包函数，其中 exponent 称为自由变量
def nth_power(exponent):
    def exponent_of(base):
        return base ** exponent
    return exponent_of 		# 返回值是 exponent_of 函数

square = nth_power(2)
print(square(2))  		# 计算 2 的平方
cube = nth_power(3)
print(cube(2)) 		# 计算 2 的立方

>>>
4
8
```

在上面程序中，外部函数 `nth_power()` 的返回值是函数 `exponent_of()`，而不是一个具体的数值。

需要注意的是，在执行完 `square = nth_power(2)` 和 `cube = nth_power(3)` 后，外部函数 `nth_power()` 的参数 `exponent` 会和内部函数 `exponent_of` 一起赋值给 `squre` 和 `cube`，这样之后调用 `square(2)` 或者 `cube(2)` 时，程序就能顺利地输出结果，而不会报错说参数 `exponent` 没有定义。

>   为什么要闭包呢？上面的程序，完全可以写成下面的形式：

```python
def  nth_power_rewrite(base, exponent):
	return base ** exponent
```

上面程序确实可以实现相同的功能，不过使用闭包，可以让程序变得更简洁易读。比如需要计算很多个数的平方，那么下面哪一种形式更好呢？

```python
# 不使用闭包
res1 = nth_power_rewrite(base1, 2)
res2 = nth_power_rewrite(base2, 2)
res3 = nth_power_rewrite(base3, 2)
# 使用闭包
square = nth_power(2)
res1 = square(base1)
res2 = square(base2)
res3 = square(base3)
```

显然第二种方式表达更为简洁，在每次调用函数时，都可以少输入一个参数。

其次，和缩减嵌套函数的优点类似，函数开头需要做一些额外工作，当需要多次调用该函数时，如果将那些额外工作的代码放在外部函数，就可以减少多次调用导致的不必要开销，提高程序的运行效率。

### 2、Python 闭包的 \__closure__ 属性

闭包比普通的函数多了一个 `__closure__` 属性，该属性记录着自由变量的地址。当闭包被调用时，系统就会根据该地址找到对应的自由变量，完成整体的函数调用。

以 `nth_power()` 为例，当其被调用时，可以通过 `__closure__` 属性获取自由变量（也就是程序中的 `exponent` 参数）存储的地址，例如：

可以看到，显示的内容是一个 `int` 整数类型，这就是 `square` 中自由变量 `exponent` 的初始值。还可以看到，`__closure__` 属性的类型是一个元组，这表明闭包可以支持多个自由变量的形式。

```python
def nth_power(exponent):
    def exponent_of(base):
        return base ** exponent
    return exponent_of
square = nth_power(2)
print(type(square.__closure__), square.__closure__)		# 查看 __closure__ 属性值

>>>
<class 'tuple'> (<cell at 0x000001E7034F3760: int object at 0x000001E702B80110>,)
```

## 7、Python lambda 表达式（匿名函数）

`lambda` 表达式，又称匿名函数，它们没有函数名称，只能通过赋值给变量或作为参数传递给其他函数来使用。常用来表示内部仅包含 1 行表达式的函数。如果一个函数的函数体仅有 1 行表达式，则该函数就可以用 `lambda` 表达式来代替。

`lambda` 表达式的语法如下：

```python
lambda_expr = lambda [parameter_list] : expression
```

-   `parameter_list`：参数列表，等同于定义函数中指定的参数列表
-   `expression`：表达式，表达式中出现的参数需要在 `parameter_list` 中定义，且表达式只能是单行的，只能有一个表达式。

上面的语法转换为普通函数的形式如下所示：

```python
def name(parameter_list):
    return expression
name(parameter_list)
```

例子：

```python
num = 100
demo1 = lambda : 'Demo1'
print(demo1())
demo2 = lambda : print('Demo2')
demo2()
demo3 = lambda x, y : x * y
print(demo3(2, 3))
demo4 = lambda : num
print(demo4())

>>>
Demo1
Demo2
6
100
```

>   `lambda` 表达式，就是简单函数（函数体仅是单行的表达式）的简写版本。相比函数，`lambda` 表达式具有以下 2 个优势：
>
>   -   对于单行函数，使用 `lambda` 表达式可以省去定义函数的过程，让代码更加简洁；
>   -   对于不需要多次复用的函数，使用 `lambda` 表达式可以在用完之后立即释放，提高程序执行的性能。

## 递归函数

如果一个函数在内部调用本身，那么这个函数就是递归函数，递归函数会形成一个深度循环！

### 计算阶乘

```python
def func(n):
    if n == 1:
        return 1
    return n * func(n-1)
while True:
    n = int(input('Please enter the Num：'))
    print(func(n))
    if n > 10:
        break
        
>>>
Please enter the Num：5
120
```

### 斐波那契数列

```python
def feibo(n):
    if n <= 1 or n == 2:
        return 1
    return (feibo(n-1) + feibo(n-2))
num = int(input("Please enter the Number:"))
list1 = [feibo(i) for i in range(1, num+1)]
print(list1)

>>>
Please enter the Number:6
[1, 1, 2, 3, 5, 8]
```

### 2 分算法

```python
def search_value(arr, target, start, end):
    if end >= start:
        mid = (start + end) // 2        # 保存中间下标
        if arr[mid] == target:
            return mid
        elif arr[mid] > target:
            return search_value(arr, target, start, mid - 1)
        else:
            return search_value(arr, target, mid + 1, end)
    else:
        return -1
list1 = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
target = int(input('Enter target: '))
index = search_value(list1, target, 0, len(list1) - 1)
if index != -1:
    print("Index:", index)
else:
    print('not found')
```

执行结果：

```python
(python3.12.0) E:\Demo\python>C:/Users/Administrator/miniconda3/envs/python3.12.0/python.exe e:/Demo/python/demo.py
Enter target: 3
Index: 2

(python3.12.0) E:\Demo\python>C:/Users/Administrator/miniconda3/envs/python3.12.0/python.exe e:/Demo/python/demo.py
Enter target: 8 
Index: 7

(python3.12.0) E:\Demo\python>C:/Users/Administrator/miniconda3/envs/python3.12.0/python.exe e:/Demo/python/demo.py
Enter target: 11
not found
```

## 8、栈溢出

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

## 9、Python 的装饰器

在不改变原有函数的基础上给函数增加功能

### 1、通用装饰器定义

```python
def wrapper(func):		# wrapper 装饰器名称，func 被装饰的函数
    def inner(*args, **kwargs):		# *args/**kwargs 给原函数同样的参数配置
        '''植入要在执行原函数前要执行的操作'''
        result = func(*args, **kwargs)	# func() 运行原函数，result 接收原函数返回值
        '''植入要在执行原函数后要执行的操作'''
        return result	# 返回原函数的返回值
    return inner	# 相当于返回原函数的返回值，用来替代原函数

@wrapper		# Python 语法糖，等同于 func = wrapper(func)
def func ():
    pass
```

### 2、实例

```python
flag = False
def blog_login():
    global flag
    while True:
        username = input('请输入用户名：')
        password = input('请输出密码：')
        if username == 'admin' and password == '123456':
            print('登录成功')
            flag = True
            break
        else:
            print('登陆失败，请检查用户名和密码')

def login(blog):
    def inner(*args, **kwargs):
        if not flag:
            blog_login()
        ret = blog(*args, **kwargs)
        return ret
    return inner

@login
def add_blog():
    print('我要写文章')

@login
def del_blog():
    print('我要删文章')

def read_blog():
    print('我要看文章')

add_blog()
del_blog()
read_blog()
```

## Python 推导式

### 列表推导式

列表推导式的包含以下内容：一个表达式，后面为一个 `for` 子句，然后，是零个或多个 `for` 或 `if` 子句。结果是由表达式依据 `for` 和 `if` 子句求值计算而得出一个新列表。语法格式如下：

```python
[ expression for variable in iterable [if condition ...]]  
```

**列表推导式执行顺序**：各语句之间是嵌套关系，左边第二个语句是最外层，依次往右进一层，左边第一条语句是最后一层

```python
list1 = [i for i in range(10)]
print(list1)
list2 = [i * 2 for i in range(10)]
print(list2)
list3 = [i for i in range(10) if i != 5]
print(list3)

>>>
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
[0, 1, 2, 3, 4, 6, 7, 8, 9]
```

```python
list1 = []
for i in range(1, 5):
    item = f"item{i}"
    list1.append(item)
print(list1)

list2 = [f"item{item}" for item in range(1, 5)]
print(list2)

>>>
['item1', 'item2', 'item3', 'item4']
['item1', 'item2', 'item3', 'item4']
```

现有一列表 `L = [[1,2,3], [4,5,6], [7.8,9]]` 要求取出元素 `1/4/7` 和 `1/5/9`

```python
L = [[1,2,3], [4,5,6], [7,8,9]]
result = [i[0] for i in L]
print(result)
result2 = [L[i][i] for i in range(len(L))]
print(result2)

>>>
[1, 4, 7]
[1, 5, 9]
```

### 字典推导式

字典推导式的包含以下内容：一个表达式，后面为一个 `for` 子句，然后，是零个或多个 `for` 或 `if` 子句。结果是由表达式依据 `for` 和 `if` 子句求值计算而得出一个新字典。语法格式如下：

```python
{ expression for variable in iterable [if condition ...]}
```

```python
age = [18, 19, 20]      # --> {0:18, 1:19, 2:20}
dict1 = {i:age[i] for i in range(len(age))}
print(dict1)

>>>
{0:18, 1:19, 2:20}
```

### 集合推导式

集合推导式的包含以下内容：一个表达式，后面为一个 `for` 子句，然后，是零个或多个 `for` 或 `if` 子句。结果是由表达式依据 `for` 和 `if` 子句求值计算而得出一个新集合。语法格式如下：

```python
{ expression for variable in iterable [if condition ...]}
```

```python
set1 = {i for i in range(1, 5)}
print(set1)

>>>
{1, 2, 3, 4}
```

### 元组生成式

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

## Python 的迭代器

迭代器统一了一些数据类型的循环遍历方式。(list, dict, set, tuple, str)

`__iter__`：获取对象的迭代器。如果对象有 `__iter__` 属性，称它为可迭代对象。

`__next__`：从迭代器中获取下一个数据。如果对象有 `__next__` 属性，称它为迭代器。

**迭代器的特点：**

1.  只能向后获取数据，不能向前；
2.  只能使用一次，一旦去玩最后一个结果，继续获取下一个会报异常 `StopIteration`；
3.  特别节省资源（省内存）。
4.  惰性机制（只有调用 `__next__` 才会获取数据）

```python
str1 = 'abc'
list1 = [1, 2, 3]
tup1 = (1, 2, 3)
set1 = {1, 2, 3}
dict1 = {'a': 1, 'b': 2, 'c':3}

str2 = str1.__iter__()
list2 = list1.__iter__()
tup2 = tup1.__iter__()
set2 = set1.__iter__()
dict2 = dict1.__iter__()

print(type(str2), str2)
print(type(list2), list2)
print(type(tup2), tup2)
print(type(set2), set2)
print(type(dict2), dict2)

>>>
<class 'str_ascii_iterator'> <str_ascii_iterator object at 0x00000256CE8BB490>
<class 'list_iterator'> <list_iterator object at 0x00000256CE8BB4C0>
<class 'tuple_iterator'> <tuple_iterator object at 0x00000256CE8BB4F0>
<class 'set_iterator'> <set_iterator object at 0x00000256CE8EBE40>
<class 'dict_keyiterator'> <dict_keyiterator object at 0x00000256CE6FE5C0>
```

```python
def iter_demo (data):
    from collections.abc import Iterable
    if isinstance(data, Iterable):  # 判断传入数据是否为可迭代对象
        it_obj = data.__iter__()    # 获取迭代器
        while True:
            try:
                print(it_obj.__next__())
            except StopIteration as err:
                print("出现异常")
                break

iter_demo('ABC')
iter_demo([1, 2, 3])

>>>
A
B
C
出现异常
1
2
3
出现异常
```

## Python 的生成器

### 生成器函数

如果函数中包含 `yield`，并且是通过 `yield` 来返回数据的话，那么这个函数就是一个生成器（generator）函数。生成器本质上是一个迭代器，每次调用生成器的 `__next()__` 方法或使用 `for` 循环进行迭代时，函数会从上次暂停的地方继续执行，直到再次遇到 `yield` 语句。

调用一个生成器函数，返回的是一个迭代器对象。

```python
def generator():
    yield 'hello'
generator()		# 此时不是在运行函数，而是在创建生成器
```

### 生成器表达式

```
(expression for variable in iterable)
```

```python
def func():
    print(111)
    yield 222
g = func()
g1 = (i for i in g)
g2 = (i for i in g1)

print(list(g))
print(list(g1))
print(list(g2))

>>>
111
[222]
[]
[]
```



# 