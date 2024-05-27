## 1、什么是模块

`Python` 标准库中包含了大量的模块（称为标准模块），还有大量的第三方模块，开发者自己也可以开发自定义模块。通过这些强大的模块可以极大地提高开发者的开发效率。

用一句话总结：模块就是 `Python` 程序。换句话说，任何 `Python` 程序都可以作为模块。

模块可以比作一盒积木，通过它可以拼出多种主题的玩具，这与前面介绍的函数不同，一个函数仅相当于一块积木，而一个模块（`.py` 文件）中可以包含多个函数，也就是很多积木。模块和函数的关系如下图所示：

<img src="https://storage.zhums.cn/d/images/image-20231025165030789.png" alt="image-20231025165030789" style="zoom:80%;" />

有个名为 `modules.py` 的文件，代码如下：

```python
def print_hello ():
    print("Hello")
```

在同级目录下创建一个名为 `say.py` 的文件代码如下：

```python
import modules
modules.print_hello()
```

执行结果如下：

```python
Hello
```

`say.py` 文件中使用了原本在 `modules.py` 文件中才有的 `print_hello` 函数，相对于 `day.py` 来说，`print_hello` 就是一个自定义的模块，只需要将 `print_hello` 模块导入到 `say.py` 文件中，就可以直接在 `say.py` 文件中使用模块中的资源。

与此同时，当调用模块中的 `print_hello()` 函数时，使用的语法格式为 "模块名.函数名"，这是因为，相对于 `say.py` 文件，`modules.py` 文件中的代码自成一个命名空间，因此在调用其他模块中的函数时，需要明确指明函数的出处，否则 Python 解释器将会报错。

## 2、Python 导入模块

### 1、import 语法

1.  `import 模块名1 [as 别名1], 模块名2 [as 别名2]，…`：这种语法格式的 `import` 语句，会导入指定模块中的所有成员（包括变量、函数、类等）。使用模块中的成员时，需用该模块名（或别名）作为前缀。
2.  `from 模块名 import 成员名1 [as 别名1]，成员名2 [as 别名2]，…`： 这种语法格式的 `import` 语句，只会导入模块中指定的成员。使用该成员时，无需附加任何前缀，直接使用成员名（或别名）即可。

>   第二种`import`语句也可以使用`form 模块名 import ＊`的格式导模块中的所有成员，但此方式不推荐使用。

### 2、语法一使用

**1、基本使用**

```python
import sys
print(sys.argv[0])
```

运行结果为：

```python
c:/Users/Administrator/Desktop/Demo/python/demo.py
```

>   `sys`模块下的`argv`变量用于获取运行`Python`程序的命令行参数，其中`argv[0]`用于获取当前`Python`程序的存储路径

**2、使用别名**

```python
import sys as alias_sys
print(alias_sys.argv[0])
```

运行结果为：

```python
c:/Users/Administrator/Desktop/Demo/python/demo.py
```

**3、一次导入多个模块**

```python
import sys, os
print(sys.argv[0])
print(os.sep)
```

运行结果为：

```python
c:/Users/Administrator/Desktop/Demo/python/demo.py
\
```

>   `os`模块的`sep`变量代表平台上的路径分隔符

**4、一次导入多个模块并使用别名**

```python
import sys as alias_sys, os as alias_os
print(alias_sys.argv[0])
print(alias_os.sep)
```

运行结果为：

```python
c:/Users/Administrator/Desktop/Demo/python/demo.py
\
```

### 3、语法二使用

**1、基本使用**

```python
from sys import argv
print(argv[0])
```

运行结果为：

```python
c:/Users/Administrator/Desktop/Demo/python/demo.py
```

**2、使用别名**

```python
from sys import argv as alias_argv
print(alias_argv[0])
```

运行结果为：

```python
c:/Users/Administrator/Desktop/Demo/python/demo.py
```

**3、一次导入多个模块成员**

```python
from sys import argv, winver
print(argv[0])
print(winver)
```

运行结果为：

```python
c:/Users/Administrator/Desktop/Demo/python/demo.py
3.8
```

>   `sys`的`winver`成员记录了该`Python`的版本号

**4、一次导入多个模块成员并使用别名**

```python
from sys import argv as alias_argv, winver as alias_winver
print(alias_argv[0])
print(alias_winver)
```

运行结果为：

```python
c:/Users/Administrator/Desktop/Demo/python/demo.py
3.8
```

**5、一次导入模块中所有成员（不推荐）**

```python
from sys import *
print(argv[0])
print(winver)
```

运行结果为：

```python
c:/Users/Administrator/Desktop/Demo/python/demo.py
3.8
```

>一般不推荐使用`from 模块 import *`这种语法导入指定模块内的所有成员，因为它存在潜在的风险。比如同时导入`module1`和`module2`内的所有成员，若两个模块内都有一个`foo()`函数，那么程序在调用`foo()`时是有风险的。

## 3、Python 自定义模块

`Python` 模块就是 `Python` 程序，换句话说，只要是 `Python` 程序，都可以作为模块导入。例如，下面定义了一个简单的模块（编写在 `demo.py` 文件中）：

```python
name = 'zhums'
age = 21
def say():
    print("人生苦短，我学 Python")
class Language:
    def __init__(self, name, desc):
        self.name = name
        self.desc = desc
    def say(self):
        print(self.name, ':', self.desc)
```

通常情况下，为了检验模板中代码的正确性，一般会为其设计一段测试代码，例如：

```python
print('我是 %s ，我今年 %d 了' %(name, age))
say()
pylang = Language('python', '人生苦短，我学 Python')
pylang.say()
```

执行结果如下：

```python
我是 zhums ，我今年 21 了
人生苦短，我学 Python
python : 人生苦短，我学 Python
```

在此基础上，新建一个 `test.py` 文件，并在该文件中使用 `demo.py` 模板文件，即使用 `import` 语句导入 `demo.py`

```python
import demo
```

此时，如果直接运行 `test.py` 文件，其运行结果如下：

```python
我是 zhums ，我今年 21 了
人生苦短，我学 Python
python : 人生苦短，我学 Python
```

可以看到，当执行 `test.py` 文件时，它同样会执行 `demo.py` 中用来测试的程序，这显然不是我们想要的效果。正常的效果应该是，只有直接运行模板文件时，测试代码才会被执行；反之，如果是其它程序以引入的方式执行模板文件，则测试代码不应该被执行。

要实现这个效果，可以借助 ` Python` 内置的 `__name__` 变量。当直接运行一个模块时，`__name__` 变量的值为 `__main__`；而将模块被导入其他程序中并运行该程序时，处于模块中的 `__name__` 变量的值就变成了模块名。因此，如果希望测试函数只有在直接运行模块文件时才执行，则可在调用测试函数时增加判断，即只有当 `__name__ =='__main__'` 时才调用测试函数。

因此，可以修改 `demo.py` 模板文件中的测试代码为：

```python
if __name__ == __main__:
    print('我是 %s ，我今年 %d 了' %(name, age))
    say()
    pylang = Language('python', '人生苦短，我学 Python')
    pylang.say()
```

再次运行 `demo.py` 模板文件时，其执行结果不变；而运行 `test.py` 文件时，其执行结果为空，显然测试代码并未执行。

**自定义模块编写说明文档**

为自定义的模块添加说明文档，和函数或类的添加方法相同，即只需在模块开头的位置定义一个字符串即可。例如，为 `demo.py` 模板文件添加一个说明文档：

```python
'''
demo 模块中包含以下内容：
name 字符串变量：初始值为 "zhums"
age  整数变量：初始值为 21
say() 函数
Language 类：包含 name 和 desc 属性和 say() 方法。
'''
```

在此基础上，通过模板的 `__doc__` 属性，来访问模板的说明文档。例如，在 `test.py` 文件中添加如下代码：

```python
import demo
print(demo.__doc__)
```

运行结果为：

```python
demo 模块中包含以下内容：
name 字符串变量：初始值为 "zhums"
age  整数变量：初始值为 21
say() 函数
Language 类：包含 name 和 desc 属性和 say() 方法。
```

## 4、Python 添加模块的方式

### 1、Python 查找模块文件的过程

通常情况下，当使用 `import` 语句导入模块后，`Python` 会按照以下顺序查找指定的模块文件：

1.  在当前目录，即当前执行的程序文件所在目录下查找；
2.  到 PYTHONPATH（环境变量）下的每个目录中查找；
3.  到 Python 默认的安装目录下查找。

以上所有涉及到的目录，都保存在标准模块 `sys` 的 `sys.path` 变量中，通过此变量我们可以看到指定程序文件支持查找的所有目录。换句话说，如果要导入的模块没有存储在 `sys.path` 显示的目录中，那么导入该模块并运行程序时，`Python` 解释器就会抛出 `ModuleNotFoundError`（未找到模块）异常。

因此解决 "`Python `找不到指定模块" 的方法有 3 种，分别是：

1.  向 `sys.path` 中临时添加模块文件存储位置的完整路径；
2.  将模块放在 `sys.path` 变量中已包含的模块加载路径中；
3.  设置 `path` 系统环境变量。

### 2、方式一：临时添加模块完整路径

```python
import sys
sys.path.append('C:\\Users\\Administrator\\Desktop\\Demo\\python\\aaa')
print(sys.path)
import demo
demo.say()
```

执行结果如下：

```python
['c:\\Users\\Administrator\\Desktop\\Demo\\python', 'C:\\Users\\Administrator\\miniconda3\\envs\\python3.8.2\\python38.zip', 'C:\\Users\\Administrator\\miniconda3\\envs\\python3.8.2\\DLLs', 'C:\\Users\\Administrator\\miniconda3\\envs\\python3.8.2\\lib', 'C:\\Users\\Administrator\\miniconda3\\envs\\python3.8.2', 'C:\\Users\\Administrator\\miniconda3\\envs\\python3.8.2\\lib\\site-packages', 'C:\\Users\\Administrator\\Desktop\\Demo\\python\\aaa']
人生苦短，我学 Python
```

>注意的是，通过该方法添加的目录，只能在执行当前文件的窗口中有效，窗口关闭后即失效。

### 3、方式二：将模块放在指定位置

`sys.path` 变量列出的所有路径都是 `Python` 默认的模块加载路径，但通常默认将 `Python` 的扩展模块添加在 `lib\site-packages` 路径下，它专门用于存放 `Python` 的扩展模块和包。

因此可以直接将编写好的 `demo.py` 文件添加到 `lib\site-packages` 路径下，就相当于为 `Python` 扩展了一个 `demo` 模块，这样任何 `Python` 程序都可使用该模块。

### 4、方式三：设置环境变量

`PYTHONPATH` 环境变量（简称 `path` 变量）的值是很多路径组成的集合，`Python` 解释器会按照 `path` 包含的路径进行一次搜索，直到找到指定要加载的模块。当然，如果最终依旧没有找到，则 `Python` 就报 `ModuleNotFoundError` 异常。

#### 1、Windows

1、此电脑右击选择属性 -> 高级系统设置 -> 环境变量 -> 新建用户变量

2、设置变量名为：`PYTHONPATH`，表明将要建立名为 `PYTHONPATH` 的环境变量；设置变量值为：`.;D:\python_modules`。这里包含两条路径（以分号 ；作为分隔符）

-   第一条路径为一个点（`.`），表示当前路径，当运行 `Python` 程序时，`Python` 将可以从当前路径加载模块；
-   第二条路径为 `D:\python_modules`，当运行 `Python` 程序时，`Python` 将可以从 `D:\python_modules` 中加载模块。

#### 2、Linux

```python
echo "PYTHONPATH=.:/root/python_modules" >> /root/.bash_profile
echo "export PYTHONPATH" >> /root/.bash_profile
source /root/.bash_profile
```

## 5、Python \__all__ 变量

以 `form 模块名 import *` 的方式导入模块时，导入的是该模块中名称不以下划线（单下划线 "-" 或双下划线 "--"）开头的变量、函数和类。因此，如果不想模块文件中的某个成员被引入到其它文件中使用，可以在其名称前添加下划线。

以 `demo.py` 模块文件和 `test.py` 文件为例，各自包含的内容如下所示：

```python
# demo.py
name = 'zhums'
age = 21
def say():
    print("人生苦短，我学 Python")

# test.py
from demo import *
print('我是 %s ，我今年 %d 了' %(name, age))
say()
```

`test.py` 执行结果如下：

```python
我是 zhums ，我今年 21 了
人生苦短，我学 Python
```

在此基础上，如果 `demo.py` 模块中的 `age` 变量不想被引入，则只需将其名称改为 `_age` 或 `__age`即可。修改之后，再次执行 `test.py`，其输出结果为：

```python
Traceback (most recent call last):
  File "c:/Users/Administrator/Desktop/Demo/python/hello.py", line 2, in <module>
    print('我是 %s ，我今年 %d 了' %(name, age))
NameError: name 'age' is not defined
```

**Python 模块中的 \__all__ 变量**

还可以借助模块提供的 `__all__` 变量，该变量的值是一个列表，存储的是当前模块中一些成员（变量、函数或者类）的名称。通过在模块文件中设置 `__all__` 变量，当其它文件以 `from 模块名 import *` 的形式导入该模块时，该文件中只能使用 `__all__` 列表中指定的成员。

>   也就是说，以 `from 模块名 import *` 形式导入的模块，当该模块定义了 `__all__` 变量时，只能导入该变量指定的成员，未指定的成员是无法导入的。

修改 `demo.py` 模块文件中的代码如下：

```python
name = 'zhums'
age = 21
def say():
    print("人生苦短，我学 Python")
__all__ = ["name", "say"]
```

运行 `test.py` 文件结果为：

```python
Traceback (most recent call last):
  File "c:/Users/Administrator/Desktop/Demo/python/hello.py", line 2, in <module>
    print('我是 %s ，我今年 %d 了' %(name, age))
NameError: name 'age' is not defined
```

>   **注意：**`__all__` 变量仅限于在其它文件中以 `from 模块名 import *` 的方式引入。使用以下 2 种方式引入模块，`__all__` 变量的设置是无效的。
>
>   -   `import 模块名`
>   -   `from 模块名 import 成员名`

## 6、Python 中的包

实际开发中，一个项目往往需要使用成百上千的模块，如果将这些模块都堆放在一起，势必不好管理。而且，使用模块可以有效避免变量名或函数名重名引发的冲突，但是如果模块名重复怎么办呢？因此，`Python` 提出了包（`Package`）的概念。

简单理解，包就是文件夹，只不过在该文件夹下必须存在一个名为 `__init__.py` 的文件。

>   注意，这是 Python 2.x 的规定，而在 Python 3.x 中，`__init__.py` 对包来说，并不是必须的。

每个包的目录下都必须建立一个 `__init__.py` 的模块，可以是一个空模块，可以写一些初始化代码，其作用就是告诉 `Python` 要将该目录当成包来处理。

注意，`__init__.py` 不同于其它模块文件，此模块的模块名不是 `__init__`，而是它所在的包名。例如，在 `settings` 包中的 `__init__.py` 文件，其模块名就是 `settings`。

包是一个包含多个模块的文件夹，它的本质依然是模块，因此包中也可以包含包。

>   Python 库：相比模块和包，库是一个更大的概念，例如在 Python 标准库中的每个库都有好多个包，而每个包中都有若干个模块。

## 7、Python 创建、导入包

### 1、创建包

包其实就是一个包含 `__init__.py` 文件的文件夹。因此手动创建一个包，只需进行以下 2 步操作：

1.  新建一个文件夹，文件夹的名称就是新建包的包名；
2.  在该文件夹中，创建一个 `__init__.py` 文件，该文件中可以不编写任何代码也可以编写一些初始化代码，则当有其它程序文件导入包时，会自动执行该文件中的代码。

示例：创建一个名为 `my_pkg` 的包

1、创建名为 `my_pkg` 的文件夹

2、在文件夹中创建一个名为 `__init__.py` 的文件，内容如下：

```python
'''
    创建第一个 Python 包
'''
print('I Love Python')
```

3、包中添加两个模块：分别是 `module1.py`、`module2.py`，代码分别如下:

```python
# module1.py 模块文件
def display(arc):
    print(arc)

# module2.py 模块文件
class PyLanguage:
    def display(self):
        print("Python")
```

### 2、导入包

包本质上还是模块，因此导入模块的语法同样也适用于导入包。无论导入我们自定义的包，还是导入从他处下载的第三方包，导入方法可归结为以下 3 种：

1.  `import 包名[.模块名 [as 别名]]`
2.  `from 包名 import 模块名 [as 别名]`
3.  `from 包名.模块名 import 成员名 [as 别名]`

>   导入包的同时，会在包目录下生成一个含有 `__init__.cpython-36.pyc` 文件的 `__pycache__` 文件夹。

#### 1、`import 包名[.模块名 [as 别名]]` 导入包

**1、标准用法**

```python
import my_pkg.module1
my_pkg.module1.display('Hello')
```

运行结果如下：

```python
I Love Python
Hello
```

**2、使用 `as` 别名**

```python
import my_pkg.module1 as mod1
mod1.display('Hello')
```

运行结果如下：

```python
I Love Python
Hello
```

#### 2、`from 包名 import 模块名 [as 别名]` 导入包

**1、标准用法**

```python
from my_pkg import module1
module1.display('Hello')
```

运行结果如下：

```python
I Love Python
Hello
```

>   此格式导入包中模块后，使用其成员不需要带包名前缀，但需要带模块名前缀。

**2、使用 `as` 别名**

```python
from my_pkg import module1 as mod1
mod1.display('Hello')
```

运行结果如下：

```python
I Love Python
Hello
```

>同样，既然包也是模块，那么这种语法格式自然也支持 `from 包名 import *` 这种写法，它和 import 包名 的作用一样，都只是将该包的 `__init__.py` 文件导入并执行。

#### 3、`from 包名.模块名 import 成员名 [as 别名]` 导入包

```python
from my_pkg.module1 import display
display('Hello')
```

运行结果如下：

```python
I Love Python
Hello
```

**2、使用 `as` 别名**

```python
from my_pkg.module1 import display as show
show('Hello')
```

运行结果如下：

```python
I Love Python
Hello
```

**3、加载所有成员**

```python
from my_pkg.module1 import *
display('Hello')
print(name)
```

运行结果如下：

```python
I Love Python
Hello
zhums
```

## 8、Python 查看模块

导入模块或者包之后，怎么知道该模块中具体包含哪些成员（变量、函数或者类）呢？查看已导入模块（包）中包含的成员，本节给大家介绍 2 种方法。

### 1、查看模块成员：dir() 函数

通过 `dir()` 函数，可以查看某指定模块包含的全部成员（包括变量、函数和类）。注意这里所指的全部成员，不仅包含可供我们调用的模块成员，还包含所有名称以双下划线 "_-_" 开头和结尾的成员，而这些 "特殊" 命名的成员，是为了在本模块中使用的，并不希望被其它文件调用。

```python
import string
print(dir(string))
```

执行结果如下：

```python
['Formatter', 'Template', '_ChainMap', '_TemplateMetaclass', '__all__', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', '_re', '_string', 'ascii_letters', 'ascii_lowercase', 'ascii_uppercase', 'capwords', 'digits', 'hexdigits', 'octdigits', 'printable', 'punctuation', 'whitespace']
```

可以看到通过 `dir()` 函数获取到的模块成员，不仅包含供外部文件使用的成员，还包含很多 "特殊"（名称以 2 个下划线开头和结束）的成员，列出这些成员，并没有实际意义。

通过列表推导式，在 `dir()` 函数输出结果的基础上，筛选出对我们有用的成员并显示出来。

```python
import string
print([e for e in dir(string) if not e.startswith('_')])
```

运行结果如下：

```python
['Formatter', 'Template', 'ascii_letters', 'ascii_lowercase', 'ascii_uppercase', 'capwords', 'digits', 'hexdigits', 'octdigits', 'printable', 'punctuation', 'whitespace']
```

### 2、查看模块成员：\__all__ 变量

除了使用 `dir()` 函数之外，还可以使用 `__all__` 变量，借助该变量也可以查看模块（包）内包含的所有成员。

```python
import string
print(string.__all__)
```

程序执行结果为：

```python
['ascii_letters', 'ascii_lowercase', 'ascii_uppercase', 'capwords', 'digits', 'hexdigits', 'octdigits', 'printable', 'punctuation', 'whitespace', 'Formatter', 'Template']s
```

显然，和 `dir()` 函数相比，`__all__` 变量在查看指定模块成员时，它不会显示模块中的特殊成员，同时还会根据成员的名称进行排序显示。

不过并非所有的模块都支持使用 `__all__` 变量，因此对于获取有些模块的成员，就只能使用 `dir()` 函数。

## 9、Python \__doc__ 属性

在使用 `dir()` 函数和 `__all__` 变量的基础上，虽然能知晓指定模块（或包）中所有可用的成员（变量、函数和类），但对于不熟悉模块的用户，还是不清楚各个成员的功能。

针对这种情况，可以使用 `help()` 函数来获取指定成员（甚至是该模块）的帮助信息。

```python
# module1.py 模块文件
def display(arc):
    '''直接输出指定参数'''
    print(arc)
```

```python
import my_pkg.module1
print([e for e in dir(my_pkg.module1) if not e.startswith('_')])
help(my_pkg.module1)
help(my_pkg.module1.display)
```

```python
['display']
Help on module my_pkg.module1 in my_pkg:

NAME
    my_pkg.module1 - # module1.py 模块文件

FUNCTIONS
    display(arc)
        直接输出指定参数

FILE
    c:\users\administrator\desktop\demo\python\my_pkg\module1.py
    
Help on function display in module my_pkg.module1:

display(arc)
    直接输出指定参数
```

值得一提的是，之所以我们可以使用 `help()` 函数查看具体成员的信息，是因为该成员本身就包含表示自身身份的说明文档（本质是字符串，位于该成员内部开头的位置）。无论是函数还是类，都可以使用 `__doc__` 属性获取它们的说明文档，模块也不例外。

以 `my_pkg `包 `module1` 模块中的 `display()` 函数为例，用 `__doc__` 变量获取其说明文档：

```python
import my_pkg.module1
print(my_pkg.module1.display.__doc__)
```

执行结果如下：

```python
直接输出指定参数
```

>   其实，`help()` 函数底层也是借助 `__doc__` 属性实现的。

那么，如果使用 `help()` 函数或者 `__doc__` 属性，仍然无法满足我们的需求，还可以使用以下 2 种方法：

1.  调用 `__file__` 属性，查看该模块或者包文件的具体存储位置，直接查看其源代码
2.  对于非自定义的模块或者包，可以查阅 `Python` 库的参考文档 https://docs.python.org/3/library/index.html

## 10、Python \__file__ 属性

通过 `__file__` 属性可以查找该模块（或包）文件所在的具体存储位置。

```python
import my_pkg
import string
print(my_pkg.__file__)	
print(string.__file__)
```

运行结果如下：

```python
c:\Users\Administrator\Desktop\Demo\python\my_pkg\__init__.py
C:\Users\Administrator\miniconda3\envs\python3.8.2\lib\string.py
```

>   引入 `my_pkg` 包时，实际上执行的是 `__init__.py` 文件，因此查看 `my_pkg` 包的存储路径，输出的 `__init__.py` 文件的路径

由此，

>   通过调用 `__file__` 属性输出的绝对路径，轻易地找到该模块（或包）的源文件；但并不是所有模块都提供 `__file__` 属性，因为并不是所有模块的实现都采用 `Python` 语言，有些模块采用的是其它编程语言（如 C 语言）。

# 