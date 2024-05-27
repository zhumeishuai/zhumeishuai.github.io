## 1、什么是异常及常见的异常类型

在编写程序时，难免会遇到错误，有的是编写人员疏忽造成的语法错误，有的是程序内部隐含逻辑问题造成的数据错误，还有的是程序运行时与系统的规则冲突造成的系统错误，等等。

编写程序时遇到的错误可大致分为 2 类，分别为语法错误和运行时错误。

### 语法错误

语法错误，也就是解析代码时出现的错误。当代码不符合 Python 语法规则时，Python 解释器在解析时就会报出 SyntaxError 语法错误，与此同时还会明确指出最早探测到错误的语句。例如：

```python
print "Hello,World!"
```

Python 3 已不再支持上面这种写法，所以在运行时，解释器会报如下错误：

```python
SyntaxError: Missing parentheses in call to 'print'. Did you mean print(...)?
```

语法错误多是开发者疏忽导致的，属于真正意义上的错误，是解释器无法容忍的，因此，只有将程序中的所有语法错误全部纠正，程序才能执行。

### 运行时错误

运行时错误，即程序在语法上都是正确的，但在运行时发生了错误。例如：

```python
a = 1/0
```

上面这句代码的意思是用 1 除以 0，并赋值给 a 。因为 0 作除数是没有意义的，所以运行后会产生如下错误：

```python
raceback (most recent call last):
  File "e:\Demo\python\demo.py", line 1, in <module>
    a = 1/0
        ~^~
ZeroDivisionError: division by zero
```

以上运行输出结果中，前两段指明了错误的位置，最后一句表示出错的类型。在 Python 中，把这种运行时产生错误的情况叫做**异常（Exceptions）**。更多异常类型见：[内置异常 — Python 3.12.0 文档](https://docs.python.org/zh-cn/3/library/exceptions.html#concrete-exceptions)

## 2、try except 语句

### 1、基本语法

[Python](https://c.biancheng.net/python/) 中，用`try except`语句块捕获并处理异常，其基本语法结构如下所示：

```python
try:
	# 可能产生异常的代码块
except [ Error1 [as alias] ]:
	# 处理异常的代码块 1
except [ (Error3, Error4, ... ) [as alias] ]:
	# 处理异常的代码块 2
except [Exception]:
	# 处理其它异常
```

-   `(Error*)`：其中，`Error*` 表示具体的异常类型
-   `as alias`：给异常类型起别名
-   `Exception`：匹配程序可能发生的所有异常情况

从`try except`的基本语法格式可以看出，try 块有且仅有一个，但 except 代码块可以有多个，且每个 except 块都可以同时处理多种异常。

>   当程序发生不同的意外情况时，会对应特定的异常类型，Python 解释器会根据该异常类型选择对应的 except 块来处理该异常。

### 2、执行流程

1.  首先，执行 `try` 子句（在 `try` 和 `except` 关键字之间的语句）。
2.  如果执行过程中没有异常发生，则忽略 `except` 子句，`try` 子句执行后结束。
3.  如果执行过程中出现异常，那么 `try` 子句中的余下部分会被忽略。若异常类型与 `except` 声明的类型相符，那么会执行对应的 `except` 子句。
4.  如果找不到匹配的 `except`，那么这个异常将传递给上层的 `try` 中，若上层也无法匹配则程序运行终止。

```python
try:
    print('外层 try')
    try:
        a = int(input('请输入除数：'))
        b = int(input('请输入被除数：'))
        c = a / b
        print('结果为：', c)
    except ValueError:
        print('值错误')
except ArithmeticError:
    print('外层 except')
    print('被除数不能为 0')

>>>
外层 try
请输入除数：10
请输入被除数：0
外层 except
被除数不能为 0
```

### 3、获取特定异常的有关信息

每种异常类型都提供了如下几个属性和方法，通过调用它们，就可以获取当前处理异常类型的相关信息：

-   `args`：返回异常的错误编号和描述字符串；
-   `str(e)`：返回异常信息，但不包括异常信息的类型；
-   `repr(e)`：返回较全的异常信息，包括异常信息的类型。

```python
try:
    import os
    os.aaa
except Exception as err:
    print(err.args)
    print(str(err))
    print(repr(err))
   
>>>
("module 'os' has no attribute 'aaa'",)
module 'os' has no attribute 'aaa'
AttributeError("module 'os' has no attribute 'aaa'")
```

>   除此之外，如果想要更加详细的异常信息，可以使用 `traceback` 模块。

## 3、try except else 语句

在原 `try except `结构的基础上，Python 异常处理机制还提供了一个 `else` 块，也就是原有 `try except` 语句的基础上再添加一个 `else` 块，即`try except else`结构。

使用 `else` 包裹的代码，只有当 `try` 块没有捕获到任何异常时，才会得到执行；反之，如果 `try` 块捕获到异常，即便调用对应的 `except` 处理完异常，`else` 块中的代码也不会得到执行。

```python
try:
    result = 20 / int(input('请输入除数:'))
    print(result)
except ValueError:
    print('必须输入整数')
except ArithmeticError:
    print('算术错误，除数不能为 0')
else:
    print('没有出现异常')
print("继续执行")

>>>
请输入除数:10
2.0
没有出现异常
继续执行
```

如上所示，当我们输入正确的数据时，try 块中的程序正常执行，Python 解释器执行完 try 块中的程序之后，会继续执行 else 块中的程序，继而执行后续的程序。

## 4、try finally 语句

Python 异常处理机制还提供了一个 `finally` 语句，无论 `try` 块是否发生异常，最终都要执行 `finally` 其中的代码。基于 `finally` 语句的这种特性，在某些情况下，当 `try` 块中的程序打开了一些物理资源（文件、数据库连接等）时，由于这些资源必须手动回收，而回收工作通常就放在 `finally` 块中。

>   注意：和`else`语句不同，`finally`只要求和`try`搭配使用，而至于该结构中是否包含`except`以及`else`，对于`finally`不是必须的（`else`必须和`try` `except`搭配使用）。

>   Python 垃圾回收机制，只能帮我们回收变量、类对象占用的内存，而无法自动完成类似关闭文件、数据库连接等这些的工作。

举个例子：

```python
try:
    a = int(input("请输入 a 的值:"))
    print(20/a)
except:
    print("发生异常！")
else:
    print("执行 else 块中的代码")   
finally :
    print("执行 finally 块中的代码")
    
>>>
请输入 a 的值:4
5.0
执行 else 块中的代码
执行 finally 块中的代码

>>>
请输入 a 的值:a
发生异常！
执行 finally 块中的代码
```

即便当 `try` 块发生异常，且没有合适和 `except` 处理异常时，`finally` 块中的代码也会得到执行。例如：

```python
try:
    #发生异常
    print(20/0)
finally :
    print("执行 finally 块中的代码")
    
>>>
执行 finally 块中的代码
Traceback (most recent call last):
  File "e:\Demo\python\demo.py", line 3, in <module>
    print(20/0)
          ~~^~
ZeroDivisionError: division by zero
```

## 5、raise 语句

Python 允许在程序中手动设置异常，使用 `raise` 语句抛出一个指定的异常。

`raise` 语句的语法格式如下：

```python
raise [exceptionName[(reason)]]
```

-   `exceptionName`：指定抛出的异常名称，必须是一个异常的实例或者是异常的类（也就是 [`Exception`](https://docs.python.org/zh-cn/3/library/exceptions.html#exception-hierarchy) 的子类）必。
-   `reason`：异常信息的相关描述。

如果没有提供 `exceptionName` 参数，则 `raise` 会重新引发当前正在处理的异常，也被称为活动的异常。如果当前没有活动的异常，则会引发 `RuntimeError` 来提示发生了错误。如果仅省略了 `reason` 参数，则在抛出异常时，将不附带任何的异常描述信息。

也就是说，raise 语句有如下三种常用的用法：

1.  `raise`：该语句引发当前上下文中捕获的异常（比如在 `except` 块中），或默认引发 `RuntimeError` 异常。
2.  `raise exceptionName`：抛出指定类型的异常。
3.  `raise exceptionName(reason)`：爬出指定类型的异常的同时，附带异常的描述信息。

```python
>>> raise
Traceback (most recent call last):
 File "<pyshell#1>", line 1, in <module>
  raise
RuntimeError: No active exception to reraise

>>> raise ZeroDivisionError
Traceback (most recent call last):
 File "<pyshell#0>", line 1, in <module>
  raise ZeroDivisionError
ZeroDivisionError

>>> raise ZeroDivisionError("除数不能为零")
Traceback (most recent call last):
 File "<pyshell#2>", line 1, in <module>
  raise ZeroDivisionError("除数不能为零")
ZeroDivisionError: 除数不能为零
```

当然，手动让程序引发异常，很多时候并不是为了让其崩溃。事实上，raise 语句引发的异常通常用 try except（else finally）异常处理结构来捕获并进行处理。例如：

```python
try:
    a = input("输入一个数：")
    #判断用户输入的是否为数字
    if(not a.isdigit()):
        raise ValueError("a 必须是数字")
except ValueError as e:
    print("引发异常：",repr(e))
    
>>>
输入一个数：a
引发异常： ValueError('a 必须是数字',)
```

可以看到，当用户输入的不是数字时，程序会进入 if 判断语句，并执行 raise 引发 ValueError 异常。但由于其位于 try 块中，因为 raise 抛出的异常会被 try 捕获，并由 except 块进行处理。

因此，虽然程序中使用了 raise 语句引发异常，但程序的执行是正常的，手动抛出的异常并不会导致程序崩溃。

**在使用 raise 语句时可以不带参数，例如：**

```python
try:
    a = input("输入一个数：")
    if(not a.isdigit()):
        raise ValueError("a 必须是数字")
except ValueError as e:
    print("引发异常：",repr(e))
    raise
>>>
输入一个数：a
引发异常： ValueError('a 必须是数字')
Traceback (most recent call last):
  File "e:\Demo\python\demo.py", line 4, in <module>
    raise ValueError("a 必须是数字")
ValueError: a 必须是数字
```

这里重点关注位于 except 块中的 raise，由于在其之前已经手动引发了 ValueError 异常，因此这里当再使用 raise 语句时，它会再次引发一次。

当在没有引发过异常的程序使用无参的 raise 语句时，它默认引发的是 RuntimeError 异常。例如：

```python
try:
    a = input("输入一个数：")
    if(not a.isdigit()):
        raise
except RuntimeError as e:
    print("引发异常：",repr(e))
    
>>>
输入一个数：a
引发异常： RuntimeError('No active exception to reraise',)
```

## 6、Python 的 sys.exc_info() 方法：获取异常信息

在实际调试程序的过程中，有时只获得异常的类型是远远不够的，还需要借助更详细的异常信息才能解决问题。

捕获异常时，有 2 种方式可获得更多的异常信息，分别是：

1.  使用 sys 模块中的 exc_info 方法；
2.  使用 traceback 模块中的相关函数。

模块 sys 中，有两个方法可以返回异常的全部信息，分别是 exc_info() 和 last_traceback()，这两个函数有相同的功能和用法，本节仅以 exc_info() 方法为例。

exc_info() 方法会将当前的异常信息以元组的形式返回，该元组中包含 3 个元素，分别为 type、value 和 traceback，它们的含义分别是：

-   type：异常类型的名称，它是 BaseException 的子类
-   value：捕获到的异常实例。
-   traceback：是一个 traceback 对象。

举个例子：

```python
import sys
try:
    x = int(input("请输入一个被除数："))
    print("30除以",x,"等于",30/x)
except:
    print(sys.exc_info())
    print("其他异常...")
    
>>>
请输入一个被除数：0
(<class 'ZeroDivisionError'>, ZeroDivisionError('division by zero',), <traceback object at 0x000001FCF638DD48>)
其他异常...
```

输出结果中，第 2 行是抛出异常的全部信息，这是一个元组，有 3 个元素，第一个元素是一个 ZeroDivisionError 类；第 2 个元素是异常类型 ZeroDivisionError 类的一个实例；第 3 个元素为一个 traceback 对象。其中，通过前 2 个元素可以看出抛出的异常类型以及描述信息，对于第 3 个元素，是一个 traceback 对象，无法直接看出有关异常的信息，还需要对其做进一步处理。

要查看 traceback 对象包含的内容，需要先引进 traceback 模块，然后调用 traceback 模块中的 print_tb 方法，并将 sys.exc_info() 输出的 traceback 对象作为参数参入。例如：

```python
import sys
#引入traceback模块
import traceback
try:
    x = int(input("请输入一个被除数："))
    print("30除以",x,"等于",30/x)
except:
    #print(sys.exc_info())
    traceback.print_tb(sys.exc_info()[2])
    print("其他异常...")

>>>
请输入一个被除数：0
  File "C:\Users\mengma\Desktop\demo.py", line 7, in <module>
    print("30除以",x,"等于",30/x)
其他异常...
```

可以看到，输出信息中包含了更多的异常信息，包括文件名、抛出异常的代码所在的行数、抛出异常的具体代码。

## 7、Python 的 traceback 模块

除了使用 sys.exc_info() 方法获取更多的异常信息之外，还可以使用 traceback 模块，该模块可以用来查看异常的传播轨迹，追踪异常触发的源头。

下面示例显示了如何显示异常传播轨迹：

```python
class SelfException(Exception):
    pass
def main():
    firstMethod()
def firstMethod():
    secondMethod()
def secondMethod():
    thirdMethod()
def thirdMethod():
    raise SelfException("自定义异常信息")
main()

>>>
Traceback (most recent call last):
  File "e:\Demo\python\demo.py", line 11, in <module>
    main()
  File "e:\Demo\python\demo.py", line 4, in main
    firstMethod()
  File "e:\Demo\python\demo.py", line 6, in firstMethod
    secondMethod()
  File "e:\Demo\python\demo.py", line 8, in secondMethod
    thirdMethod()
  File "e:\Demo\python\demo.py", line 10, in thirdMethod
    raise SelfException("自定义异常信息")
SelfException: 自定义异常信息
```

从输出结果可以看出，异常从 thirdMethod() 函数开始触发，传到 secondMethod() 函数，再传到 firstMethod() 函数，最后传到 main() 函数，在 main() 函数止，这个过程就是整个异常的传播轨迹。

在实际应用程序的开发中，大多数复杂操作都会被分解成一系列函数或方法调用。这是因为，为了具有更好的可重用性，会将每个可重用的代码单元定义成函数或方法，将复杂任务逐渐分解为更易管理的小型子任务。由于一个大的业务功能需要由多个函数或方法来共同实现，在最终编程模型中，很多对象将通过一系列函数或方法调用来实现通信，执行任务。

所以，当应用程序运行时，经常会发生一系列函数或方法调用，从而形成“函数调用战”。异常的传播则相反，只要异常没有被完全捕获（包括异常没有被捕获，或者异常被处理后重新引发了新异常），异常就从发生异常的函数或方法逐渐向外传播，首先传给该函数或方法的调用者，该函数或方法的调用者再传给其调用者，直至最后传到 [Python](https://c.biancheng.net/python/) 解释器，此时 Python 解释器会中止该程序，并打印异常的传播轨迹信息。

很多初学者一看到输出结果所示的异常提示信息，就会惊慌失措，他们以为程序出现了很多严重的错误，其实只有一个错误，系统提示那么多行信息，只不过是显示异常依次触发的轨迹。

其实，上面程序的运算结果显示的异常传播轨迹信息非常清晰，它记录了应用程序中执行停止的各个点。最后一行信息详细显示了异常的类型和异常的详细消息。从这一行向上，逐个记录了异常发生源头、异常依次传播所经过的轨迹，并标明异常发生在哪个文件、哪一行、哪个函数处。

使用 traceback 模块查看异常传播轨迹，首先需要将 traceback 模块引入，该模块提供了如下两个常用方法：

-   traceback.print_exc()：将异常传播轨迹信息输出到控制台或指定文件中。
-   format_exc()：将异常传播轨迹信息转换成字符串。

可能有读者好奇，从上面方法看不出它们到底处理哪个异常的传播轨迹信息。实际上我们常用的 print_exc() 是 print_exc([limit[, file]]) 省略了 limit、file 两个参数的形式。而 print_exc([limit[, file]]) 的完整形式是 `print_exception(etype, value, tb[,limit[, file]])`，在完整形式中，前面三个参数用于分别指定异常的如下信息：

-   etype：指定异常类型；
-   value：指定异常值；
-   tb：指定异常的traceback 信息；

当程序处于 except 块中时，该 except 块所捕获的异常信息可通过 sys 对象来获取，其中 sys.exc_type、sys.exc_value、sys.exc_traceback 就代表当前 except 块内的异常类型、异常值和异常传播轨迹。

简单来说， print_exc([limit[, file]]) 相当于如下形式：

print_exception(sys.exc_etype, sys.exc_value, sys.exc_tb[, limit[, file]])

也就是说，使用 print_exc([limit[, file]]) 会自动处理当前 except 块所捕获的异常。该方法还涉及两个参数：

1.  limit：用于限制显示异常传播的层数，比如函数 A 调用函数 B，函数 B 发生了异常，如果指定 limit=1，则只显示函数 A 里面发生的异常。如果不设置 limit 参数，则默认全部显示。
2.  file：指定将异常传播轨迹信息输出到指定文件中。如果不指定该参数，则默认输出到控制台。

借助于 traceback 模块的帮助，我们可以使用 except 块捕获异常，并在其中打印异常传播信息，包括把它输出到文件中。例如如下程序：

```python
import traceback
class SelfException(Exception): pass
def main():
    firstMethod()
def firstMethod():
    secondMethod()
def secondMethod():
    thirdMethod()
def thirdMethod():
    raise SelfException("自定义异常信息")
try:
    main()
except:
    # 捕捉异常，并将异常传播信息输出控制台
    traceback.print_exc()
    # 捕捉异常，并将异常传播信息输出指定文件中
    traceback.print_exc(file=open('log.txt', 'a'))
```

上面程序第一行先导入了 traceback 模块，接下来程序使用 except 捕获程序的异常，并使用 traceback 的 print_exc() 方法输出异常传播信息，分别将它输出到控制台和指定文件中。

运行上面程序，同样可以看到在控制台输出异常传播信息，而且在程序目录下生成了一个 log.txt 文件，该文件中同样记录了异常传播信息。

# 