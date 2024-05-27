## 1、Python 面向对象

### 1、什么是面向对象

面向对象编程（Object-oriented Programming，简称 OOP），是一种封装代码的方法。前面已经接触了封装，比如说，将乱七八糟的数据扔进列表中，这就是一种简单的封装，是数据层面的封装；把常用的代码块打包成一个函数，这也是一种封装，是语句层面的封装。

代码封装，其实就是隐藏实现功能的具体代码，仅留给用户使用的接口，就好像使用计算机，用户只需要使用键盘、鼠标就可以实现一些功能，而根本不需要知道其内部是如何工作的。

面向对象编程，也是一种封装的思想，不过显然比以上两种封装更先进，它可以更好地模拟真实世界里的事物（将其视为对象），并把描述特征的数据和代码块（函数）封装到一起。

例如：若在某游戏中设计一个乌龟的角色，应该如何来实现呢？使用面向对象的思想会更简单，可以分为如下两个方面进行描述：

1.  从表面特征来描述，例如，绿色的、有 4 条腿、重 10 kg、有外壳等等。
2.  从所具有的的行为来描述，例如，它会爬、会吃东西、会睡觉、会将头和四肢缩到壳里，等等。

如果将乌龟用代码来表示，则其表面特征可以用变量来表示，其行为特征可以通过建立各种函数来表示。参考代码如下所示：

```python
class tortoise:
    bodyColor = "绿色"
    footNum = 4
    weight = 10
    hasShell = True
    # 会爬
    def crawl(self):
        print("乌龟会爬")
    # 会吃东西
    def eat(self):
        print("乌龟吃东西")
    # 会睡觉
    def sleep(self):
        print("乌龟在睡觉")
    # 会缩到壳里
    def protect(self):
        print("乌龟缩进了壳里")
```

因此，从某种程度上，相比较只用变量或只用函数，使用面向对象的思想可以更好地模拟现实生活中的事物。

不仅如此，在 Python 中，所有的变量其实也都是对象，包括整形（int）、浮点型（float）、字符串（str）、列表(list)、元组(tuple)、字典（dict）和集合（set）。以字典（dict）为例，它包含多个函数供我们使用，例如使用 keys() 获取字典中所有的键，使用 values() 获取字典中所有的值，使用 item() 获取字典中所有的键值对，等等。

### 2、面向对象相关术语

面向对象中，常用术语包括：

-   类：可以理解是一个模板，通过它可以创建出无数个具体实例（对象）。比如，前面编写的 `tortoise` 表示的只是乌龟这个物种，通过它可以创建出无数个实例来代表各种不同特征的乌龟（这一过程又称为类的实例化）。
-   对象：类不能直接使用，通过类创建出的实例（又称对象）才能使用。类似汽车图纸和汽车的关系，图纸本身（类）并不能使用，通过图纸创建出的汽车（对象）才能使用。
-   属性：类中的变量称为属性。例如，`tortoise` 这个类中，`bodyColor、footNum、weight、hasShell` 都是这个类拥有的属性。
-   方法：类中的函数称为方法。和函数所有不同的是，方法至少要包含一个 `self` 参数。方法无法单独使用，只能和类的对象一起使用。

## 2、Python 类的定义

在[面向对象相关术语](#2、面向对象相关术语)中提到，类仅仅充当图纸的作用，本身并不能直接使用，只有根据图纸造出的实际物品（对象）才能直接使用。因此，Python 程序中类的使用顺序是：

1.  创建（定义）类，也就是制作图纸的过程；
2.  创建类的实例对象（根据图纸造出实际的物品），通过实例对象实现特定的功能。

在 Python 中使用 `class` 关键字定义类，语法格式如下：

```python
class ClassName:
    [Var]...
    [Func]...
```

>   注意: 无论是类属性还是类方法，对于类来说都不是必需的，可以有也可以没有。另外，Python 类中属性和方法所在的位置是任意的，即它们之间并没有固定的前后顺序。

>   类属性指的就是包含在类中的变量；而类方法指的是包含类中的函数。换句话说，类属性和类方法其实分别是包含类中的变量和函数的别称。需要注意的一点是，同属一个类的所有类属性和类方法，要保持统一的缩进格式，通常统一缩进 4 个空格。

定义一个类：

```python
class TheFirstDemo:
    '''
        This is ClassDemo
    '''
    # 定义类属性
    Name = 'zhums'
    # 定义类方法
    def say(self, content):
        print(content)
```

>   和函数一样，我们也可以为类定义说明文档，其要放到类头之后，类体之前的位置，如上面程序中第二行的字符串，就是 TheFirstDemo 这个类的说明文档。

上面创建了一个名为 `TheFirstDemo` 的类，其包含了一个名为 `Name` 的类属性。注意，根据定义属性位置的不同，在各个类方法之外定义的变量称为类属性或类变量（如 `Name` 属性），而在类方法中定义的属性称为实例属性（或实例变量），它们的区别和用法查看 [Python 类属性和实例属性](#6、Python 类属性和实例属性)。

事实上，完全可以创建一个没有任何类属性和类方法的类，换句话说，Python 允许创建空类，例如：

```python
class Empty:
	pass
```

## 3、Python 的类构造方法 \__init__()

在创建类时，可以手动添加一个 `__init__()` 方法，该方法是一个特殊的类实例方法，称为构造方法（或构造函数）。

构造方法用于创建对象时使用，每当创建一个类的实例对象时，[Python](http://c.biancheng.net/python/) 解释器都会自动调用它。[Python](http://c.biancheng.net/python/) 类中，手动添加构造方法的语法格式如下：

```python
def __init__(self,...):
    codes...
```

>   此方法的方法名中，开头和结尾各有 2 个下划线，且中间不能有空格。Python 中很多这种以双下划线开头、双下划线结尾的方法，都具有特殊的意义。

`__init__()` 方法可以包含多个参数，但必须包含一个名为 `self` 的参数且作为第一个参数。也就是说，类的构造方法最少也要有一个 `self` 参数。例如，仍以 TheFirstDemo 类为例，添加构造方法的代码如下所示：

```python
class TheFirstDemo:
    ''' This is ClassDemo '''
    def __init__(self):
        print("调用构造方法")
    Name = 'zhums'
    def say(self, content):
        print(content)
```

>   注意，即便不手动为类添加构造方法，Python 也会自动为类添加一个仅包含 `self` 参数的构造方法。
>
>   仅包含 `self` 参数的 `__init__()` 构造方法，又称为类的默认构造方法。

**创建类对象**

如下可以看到在创建 `Object1` 这个对象时，隐式调用了手动创建的 `__init__()` 构造方法。

```python
class TheFirstDemo:
    ''' This is ClassDemo '''
    def __init__(self):
        print("调用构造方法")
    Name = 'zhums'
    def say(self, content):
        print(content)
Object1 = TheFirstDemo()

>>>
调用构造方法
```

在 `__init__()` 构造方法中，除了 `self` 参数外，还可以自定义一些参数，参数之间使用逗号 "," 进行分割。例如，下面的代码在创建 `__init__()` 方法时，额外指定了 2 个参数：

>注意: 由于创建对象时会调用类的构造方法，如果构造函数有多个参数时，需要手动传递参数

```python
class ClassDemo:
    ''' This is ClassDemo '''
    def __init__(self, name, age):
        print("%s 今年 %d 岁" %(name, age))
Info = ClassDemo('zhums', 21)

>>>
zhums 今年 21 岁
```

>   可以看到，虽然构造方法中有 self、name、add 3 个参数，但实际需要传参的仅有 name 和 add，也就是说，self 不需要手动传递参数。关于 self 参数，这里只需要知道，在创建类对象时，无需给 self 传参。

## 4、Python 类对象的创建和使用

如果想使用类，则必须创建该类的对象。创建类对象的过程，又称为类的实例化。

### 1、Python 类的实例化

对已定义好类进行实例化，语法如下：

```python
VarName = ClassName(Args)
```

>   定义类时，若没有手动添加 `__init__()` 构造方法，或添加的 `__init__()` 中仅有一个 `self` 参数，则创建类对象时的参数可以省略不写。

如下代码创建了名为 Info 的类，并对其进行了实例化：

```python
class Info:
    # 定义 2 个类变量
    Name = 'zhums'
    Age = 21
    def __init__(self, Name, Age):
        # 定义两个实例变量
        self.Name = Name
        self.Age = Age
        print("%s 今年 %d 岁" %(Name, Age))
# 将 Info 对象赋给 Student1 变量
Studnet1 = Info('zhums', 21)
```

在上面的程序中，由于构造方法除 self 参数外，还包含 2 个参数，且这 2 个参数没有设置默认参数，因此在实例化类对象时，需要传入相应的 name 值和 add 值（self 参数是特殊参数，不需要手动传值，Python 会自动传给它值）。

>   类变量和实例变量，简单地理解，定义在各个类方法之外（包含在类中）的变量为类变量（或者类属性），定义在类方法中的变量为实例变量（或者实例属性），二者的具体区别和用法可查看[Python 类属性和实例属性](#6、Python 类属性和实例属性)

### 2、Python 类对象的使用

定义的类只有进行实例化，也就是使用该类创建对象之后，才能得到利用。总的来说，实例化后的类对象可以执行以下操作：

-   访问或修改类对象具有的实例变量，甚至可以添加新的实例变量或者删除已有的实例变量；
-   调用类对象的方法，包括调用现有的方法，以及给类对象动态添加方法。

#### 1、类对象访问变量或方法

使用已创建好的类对象访问类中实例变量的语法格式如下：

```python
ObjectName.VarName
```

使用类对象调用类中方法的语法格式如下：

```python
ObjectName.FunctionName(Args)
```

注意，对象名和变量名以及方法名之间用点 "." 连接。

```python
class Info:
    def __init__(self, Name, Age):
        self.Name = Name
        self.Age = Age
    def say(self, content):
        print(content)
Studnet1 = Info('zhums', 21)
# 输出实例变量 Name 和 Age 的值
print(Studnet1.Name, Studnet1.Age)
# 修改变量的值
Studnet1.Name = 'wuyi'
Studnet1.Age = 19
# 再次输出实例变量 Name 和 Age 的值
print(Studnet1.Name, Studnet1.Age)
# 调用 Studnet1 的 say 方法
Studnet1.say('人生苦短, 我用 Python')

>>>
zhums 21
wuyi 19
人生苦短, 我用 Python
```

#### 2、给类对象动态添加/删除变量

Python 支持为已创建好的对象动态增加实例变量，例如：

```python
Studnet1.Sex = 'man'
print(Studnet1.Sex)
```

Python 支持为已创建好的对象动态删除实例变量，例如：

```python
del Studnet1.Age
print(Studnet1.Age)
```

#### 3、给类对象动态添加方法

>   在理解下面内容之前，需明白`self`参数的含义和作用。[Python 的 self 参数](#5、Python 的 self 参数)

需要注意的是，为类对象动态增加的方法，`Python` 不会自动将调用者自动绑定到第一个参数（即使将第一个参数命名为 `self` 也没用）如下所示：

```python
class CLanguage:
    def say(self, content):
        print(content)
clanguage = CLanguage()

def info(self):
    print("---info函数---", self)

# 使用 info 对 clanguage 的 foo 方法赋值（动态绑定方法）
clanguage.foo = info
# Python 不会自动将调用者绑定到第一个参数，因此程序需要手动将调用者绑定为第一个参数
clanguage.foo(clanguage)

# 使用 lambda 表达式为 clanguage 对象的 bar 方法赋值（动态绑定方法）
clanguage.bar = lambda self: print('--lambda表达式--', self)
clanguage.bar(clanguage)
```

上面的第 10 行和第 15 行代码分别使用函数、`lambda` 表达式为 `clanguage` 对象动态增加了方法，但对于动态增加的方法，`Python` 不会自动将方法调用者绑定到它们的第一个参数，因此程序必须手动为第一个参数传入参数值，如上 12/16 行所示。

有没有不用手动给 `self` 传值的方法呢？通过借助 `types` 模块下的 `MethodType` 可以实现，仍以上面的 `info()` 函数为例：

```python
def info(self,content):    
    print("C语言中文网地址为：%s" % content)
# 导入 MethodType
from types import MethodType
clanguage.info = MethodType(info, clanguage)
# 第一个参数已经绑定了，无需传入
clanguage.info("http://c.biancheng.net")
```

可以看到，由于使用 MethodType 包装 info() 函数时，已经将该函数的 self 参数绑定为 clanguage，因此后续再使用 info() 函数时，就不用再给 self 参数绑定值了。

```python
def info(self,content):    
    print("C语言中文网地址为：%s" %content)

# 导入 MethodType
from types import MethodType
clanguage.info = MethodType(info, clanguage)
# 第一个参数已经绑定了，无需传入
clanguage.info("http://c.biancheng.net")
```

可以看到，由于使用 `MethodType` 包装 `info()` 函数时，已经将该函数的 `self` 参数绑定为 `clanguage`，因此后续再使用 `info()` 函数时，就不用再给 `self` 参数绑定值了。

## 5、Python 的 self 参数

在定义类的过程中，无论是显式创建类的构造方法，还是向类中添加实例方法，都要求将 `self` 参数作为方法的第一个参数。

事实上，`Python` 只是规定了无论是构造方法还是实例方法，最少都要包含一个参数，并没有规定改参数的具体名称。之所以将其命名为 `self` 只是程序员之间约定俗成的一种习惯。

那么，`self` 参数的具体作用是什么呢？打个比方，如果把类比作造房子的图纸，那么类实例化后的对象是真正可以住的房子。根据一张图纸（类），我们可以设计出成千上万的房子（类对象），每个房子长相都是类似的（都有相同的类变量和类方法），但它们都有各自的主人，那么如何对它们进行区分呢？当然是通过 `self` 参数，它就相当于每个房子的门钥匙，可以保证每个房子的主人仅能进入自己的房子（每个类对象只能调用自己的类变量和类方法）。

也就是说，同一个类可以产生多个对象，当某个对象调用类方法时，该对象会把自身的引用作为第一个参数自动传给该方法，换句话说，`Python` 会自动绑定类方法的第一个参数指向调用该方法的对象。如此，`Python` 解释器就能知道到底要操作哪个对象的方法了。

因此，程序在调用实例方法和构造方法时，不需要手动为第一个参数传值。如下所示：

```python
class Person:
    def study(self):
        print(self, "正在学 Python")
zhangsan = Person()
zhangsan.study()
lisi = Person()
lisi.study()
```

上面代码中，`study()` 中的 `self` 代表该方法的调用者，即谁调用该方法，那么 `self` 就代表谁。因此，该程序的运行结果为：

```python
<__main__.Person object at 0x000001B6608F7550> 正在学 Python
<__main__.Person object at 0x000001B6608F7520> 正在学 Python
```

另外，对于构造函数中的 `self` 参数，其代表的是当前正在初始化的类对象。如下所示：

```python
class Person:
    def __init__(self,name):
        self.name=name
zhangsan = Person("zhangsan")
print(zhangsan.name)
lisi = Person("lisi")
print(lisi.name)
```

运行结果为：

```python
zhangsan
lisi
```

可以看到，`zhangsan` 在进行初始化时，调用的构造函数中 `self` 代表的是 `zhangsan`；而 `lisi` 在进行初始化时，调用的构造函数中 `self` 代表的是 `lisi`。

除了类对象可以直接调用类方法，还有一种函数调用的方式，如下所示：

```python
class Person:
    def who(self):
        print(self)
zhangsan = Person()
print(zhangsan.who)
who = (zhangsan.who)
who()		# 通过 who 变量调用 zhangsan 对象中的 who() 方法
```

运行结果为：

```python
<__main__.Person object at 0x000001E63F247520>
<__main__.Person object at 0x000001E63F247520>
```

显然，无论采用哪种方法，`self` 所表示的都是实际调用该方法的对象。

>   总之，无论是类中的构造函数还是普通的类方法，实际调用它们的谁，则第一个参数 `self` 就代表谁。

## 6、Python 类属性和实例属性

在类中，根据变量定义的位置不同，及定义的方式不同，类属性又可细分为以下 3 种类型：

1.  类中，函数外：此范围定义的变量，称为类属性或类变量；
2.  类中，函数内：以 `self.变量名` 的方式定义的变量，称为实例属性或实例变量；
3.  类中，函数内：以 `变量名=变量值` 的方式定义的变量，称为局部变量。

### 类属性（类变量）

类属性指的是在类中，但在类方法外定义的变量。如下：

```python
class Demo:
    # 定义 2 个类变量
    Name = 'Linux 运维平台'
    Site = 'https://op.zhums.top'
    # 定义 1 个 say 方法
    def say(self, content):
        print(content)
```

上面程序中，`Name` 和 `Site` 属于类变量。

类变量的特点是，所有类的实例化对象都同时共享类变量，也就是说，类变量在所有实例化对象中是作为公用资源存在的。类方法的调用方式有 2 种，既可以使用类名直接调用，也可以使用类的实例化对象调用。

在上面的 `Demo` 类外部添加如下代码：

```python
# 使用类名直接调用
print(Demo.Name)
print(Demo.Site)
# 修改类变量的值
Demo.Name = '运维平台'
Demo.Site = 'op.zhums.top'
print(Demo.Name)
print(Demo.Site)
```

运行结果如下：

```python
Linux 运维平台
https://op.zhums.top
运维平台
op.zhums.top
```

可以看到通过类名不仅可以调用类变量，也可以修改它的值。

也可以通过类对象调用所属类中的类变量==不推荐使用==，在 `Demo` 类的外部添加如下代码：

```python
CDemo = Demo()
print(CDemo.Name)
print(CDemo.Site)
```

运行结果如下：

```python
Linux 运维平台
https://op.zhums.top
```

>   注意：因为类变量为所有实例化对象共有，修改类变量的值，会影响所有的实例化对象。如下代码：

```python
class Demo:
    Name = 'Linux 运维平台'
print('修改前，各类对象中类变量的值：')
Demo1 = Demo()
print(Demo1.Name)
Demo2 = Demo()
print(Demo2.Name)
print('修改后，各类对象中类变量的值：')
Demo.Name = '运维平台'
print(Demo1.Name)
print(Demo2.Name)

>>>
修改前，各类对象中类变量的值：
Linux 运维平台
Linux 运维平台
修改后，各类对象中类变量的值：
运维平台
运维平台
```

通过类名修改类变量，会作用到所有的实例化对象。

>   注意: 通过类对象无法修改类变量。通过类对象给类变量赋值，本质上不再是修改类变量的值，而是再给对象定义新的实例变量。

### 实例属性（实例变量）

实例变量指的是在任意类方法内部，以 `self.变量名` 的方式定义的变量，其特点是只作用于调用方法的对象。另外实例变量只能通过对象名访问，无法通过类名访问。

```python
class WebSite:
    def __init__(self):
        self.Name = 'Linux 运维平台'
        self.Site = 'https://op.zhums.top'
    def say(self):
        self.Catalog = 1
```

此 `WebSite` 类中，`Name Site` 及 `Catalog` 都是实例变量。其中，由于 `__init__()` 函数在创建类对象时会自动调用，而 `say()` 方法需要类对象手动调用。因此，`WebSite` 类的类对象都会包含 `Name Site` 实例变量，而只有调用了 `say()` 方法的类对象，才包含 `Catalog` 实例变量。

在上面的基础上添加如下代码：

```python
Site1 = WebSite()
print(Site1.Name)
print(Site1.Site)
# print(Site1.Catalog)   由于 Site1 对象没有调用 say() 方法，所以没有 Catalog 变量，这行会报错
Site2 = WebSite()
print(Site2.Name)
print(Site2.Site)
Site2.say()  # 调用了 say() 方法，才会拥有 Catalog 实例变量
print(Site2.Catalog)

>>>
Linux 运维平台
https://op.zhums.top
Linux 运维平台
https://op.zhums.top
1
```

通过类对象可以访问类变量，但无法修改类变量的值。这是因为，通过类对象修改类变量的值，不是在给 "类变量赋值"，而是 "定义新的实例变量"。

>   类中，实例变量和类变量可以同名，但这种情况下使用类对象将无法调用类变量，它会首选实例变量，这也是不推荐 "类变量使用对象名调用" 的原因。

另外，和类变量不同，通过某个对象修改实例变量的值，不会影响类的其它实例化对象，更不会影响同名的类变量。例如：

```python
class WebSite :
    name = "Linux 运维平台"  #类变量
    add = "https://"  # 类变量
    def __init__(self):
        self.name = "运维平台"   #实例变量
        self.add = "https://op.zhums.top"   #实例变量
Site1 = WebSite()
Site1.name = "Linux 运维"		# 修改 Site1 对象的实例变量
Site1.add = "op.zhums.top"
print(Site1.name)
print(Site1.add)
Site2 = WebSite()
print(Site2.name)
print(Site2.add)
print(WebSite.name)		# 输出类变量的值
print(WebSite.add)

>>>
Linux 运维
op.zhums.top
运维平台
https://op.zhums.top
Linux 运维平台
https://
```

### 局部变量

类方法中还可以定义局部变量，局部变量直接以 "变量名=变量值" 的方式定义，如下：

```python
class Demo:
    def count(self, money):
        sale = 0.8 * money
        print("优惠后的价格为:", sale)
Demo1 = Demo()
Demo1.count(100)

>>>
优惠后的价格为: 80.0
```

>通常情况下，定义局部变量是为了所在类方法功能的实现。需要注意的一点是，局部变量只能用于所在函数中，函数执行完成后，局部变量也会被销毁。

## 7、Python 类的类方法、静态方法和实例方法

和类属性一样，类方法也可以进行更细致的划分，具体可分为类方法、实例方法和静态方法。

和类属性的分类不同，区分这 3 种类方法非常简单：

-   即采用 `@classmethod` 修饰的方法为类方法；
-   采用 `@staticmethod` 修饰的方法为静态方法；
-   不用任何修改的方法为实例方法。

>   其中 `@classmethod` 和 `@staticmethod` 都是函数装饰器

### Python 类的实例方法

通常在类中定义的方法默认都是 "实例方法"（类的构造方法理论上也属于实例方法）。

```python
class CLanguage:
    #类构造方法，也属于实例方法
    def __init__(self):
        self.name = "C语言中文网"
        self.add = "http://c.biancheng.net"
    # 下面定义了一个say实例方法
    def say(self):
        print(self, "正在调用 say() 实例方法")
```

实例方法最大的特点就是，它最少也要包含一个 `self  `参数，用于绑定调用此方法的实例对象（`Python  `会自动完成绑定）。实例方法通常会用类对象直接调用，例如：

```python
zhangsan = CLanguage()
zhangsan.say()
```

运行结果为：

```python
<__main__.CLanguage object at 0x0000024626CA8AF0> 正在调用 say() 实例方法
```

>有关使用类名直接调用实例方法的更多介绍，可阅读《[Python 类调用实例方法](# 8、Python 类调用实例方法)》一节。

### Python 类的类方法

`Python` 类方法和实例方法相似，它最少也要包含一个参数，只不过类方法中通常将其命名为 `cls`，`Python` 会自动将类本身绑定给 `cls` 参数（注意，绑定的不是类对象）。也就是说，我们在调用类方法时，无需显式为 `cls` 参数传参。

>   和 `self` 一样，`cls` 参数的命名也不是规定的（可以随意命名），只是 `Python` 程序员约定俗称的习惯而已。

和实例方法最大的不同在于，类方法需要使用 `＠classmethod` 修饰符进行修饰，例如：

```python
class CLanguage:
    @classmethod
    def info(cls):
        print(cls, "正在调用类方法")
```

>   注意，如果没有 `＠classmethod`，则 `Python` 解释器会将 `info()` 方法认定为实例方法，而不是类方法。

类方法推荐使用类名直接调用，当然也可以使用实例对象来调用（不推荐）。例如，在上面 `CLanguage` 类的基础上，在该类外部添加如下代码：

```python
# 使用类名直接调用类方法
CLanguage.info()		

# 使用类对象调用类方法
clang = CLanguage()		
clang.info()
```

运行结果为：

```python
<class '__main__.CLanguage'> 正在调用类方法
<class '__main__.CLanguage'> 正在调用类方法
```

### Python 类的静态方法

静态方法，其实就是函数，和函数唯一的区别是，静态方法定义在类这个空间（类命名空间）中，而函数则定义在程序所在的空间（全局命名空间）中。

静态方法没有类似 `self`、`cls` 这样的特殊参数，因此 `Python` 解释器不会对它包含的参数做任何类或对象的绑定。也正因为如此，类的静态方法中无法调用任何类属性和类方法。

静态方法需要使用 `＠staticmethod`，例如：

```python
class CLanguage:
    @staticmethod
    def info(name, add):
        print(name, add)
```

静态方法的调用，既可以使用类名，也可以使用类对象，例如：

```python
# 使用类名直接调用类方法
CLanguage.info("百度", "https://www.baidu.com")

# 使用类对象调用类方法
clang = CLanguage()
clang.info("阿里云", "https://www.aliyun.com")
```

运行结果为：

```python
百度 https://www.baidu.com
阿里云 https://www.aliyun.com
```

>   在实际编程中，几乎不会用到类方法和静态方法，因为我们完全可以使用函数代替它们实现想要的功能，但在一些特殊的场景中（例如工厂模式中），使用类方法和静态方法也是很不错的选择。

## 8、Python 类调用实例方法

类方法大体分为 3 类，分别是类方法、实例方法和静态方法，其中实例方法用的是最多的。实例方法的调用方式其实有 2 种，既可以采用类对象调用，也可以直接通过类名调用。

通常情况下，我们习惯使用类对象调用类中的实例方法。但如果想用类调用实例方法，不能像如下这样：

```python
class CLanguage:
    def info(self):
        print("我正在学习 Python")
CLanguage.info()
```

运行上面代码，程序会报出如下错误：

```python
Traceback (most recent call last):
  File "c:/Users/Administrator/Desktop/Demo/python/demo.py", line 4, in <module>
    CLanguage.info()
TypeError: info() missing 1 required positional argument: 'self'
```

最后一行报错信息提示我们，调用 `info()` 方法时缺少给 `self` 参数传参。这意味着，和使用类对象调用实例方法不同，通过类名直接调用实例方法时，`Python` 并不会自动给 `self` 参数传值。因为 `self` 参数需要的是方法的实际调用者（是类对象），而这里只提供了类名，当然无法自动传值。

因此，如果想通过类名直接调用实例方法，就必须手动为 `self` 参数传值。例如修改上面的代码为：

```python
class CLanguage:
    def info(self):
        print("我正在学习 Python")
clang = CLanguage()
CLanguage.info(clang)
```

再次运行程序，结果为：

```python
我正在学 Python
```

可以看到，通过手动将 `clang` 这个类对象传给了 `self` 参数，使得程序得以正确执行。这里调用实例方法的形式等价于 `clang.info()`

值得一提的是，上面的报错信息只是让我们手动为 `self` 参数传值，但并没有规定必须传一个该类的对象，其实完全可以任意传入一个参数，例如：

```python
class CLanguage:
    def info(self):
        print(self, "我正在学习 Python")
CLanguage.info('zhums')
```

运行结果为：

```python
zhums 我正在学习 Python
```

可以看到，"zhums" 这个字符串传给了 `info()` 方法的 `self` 参数。显然，无论是 `info()` 方法中使用 `self` 参数调用其它类方法，还是使用 `self` 参数定义新的实例变量，胡乱的给 `self` 参数传参都将会导致程序运行崩溃。

总的来说，`Python` 中允许使用类名直接调用实例方法，但必须手动为该方法的第一个 `self` 参数传递参数，这种调用方法的方式被称为 "非绑定方法"。

>   用类的实例对象访问类成员的方式称为绑定方法，而用类名调用类成员的方式称为非绑定方法。

## 9、Python 类的继承

### 1、类的继承

Python 同样支持类的继承，如果一种语言不支持继承，类就没有什么意义。派生类的定义如下所示:

```python
class DerivedClassName(BaseClassName):
    <statement-1>
    ...
    <statement-N>
```

子类（派生类 `DerivedClassName`）会继承父类（基类 `BaseClassName`）的属性和方法。`BaseClassName`（实例中的基类名）必须与派生类定义在一个作用域内。除了类，还可以用表达式，基类定义在另一个模块中时这一点非常有用:

```python
class DerivedClassName(modname.BaseClassName):
```

```python
class people:		# 定义基类
    name = ''
    age = 0
    __weight = 0	# 私有属性，类外部无法直接访问
    def __init__(self, n, a, w):
        self.name = n
        self.age = a
        self.__weight = w
    def speak(self):
        print('%s 说：我 %d 岁' %(self.name, self.age))

class student(people):	# 定义派生类，指定基类
    grade = ''
    def __init__(self, n, a, w, g):
        people.__init__(self, n, a, w)	# 调用基类的构造函数
        self.grade = g
    def speak(self):		# 覆盖基类的同名方法
        print('%s 说：我 %d 岁了，我在读 %d 年级' %(self.name, self.age, self.grade))
        
s = student('ken',10,60,3)
s.speak()

>>>
ken 说：我 10 岁了，我在读 3 年级
```

### 2、多继承

Python同样有限的支持多继承形式。多继承的类定义形如下例:

```python
class DerivedClassName(Base1, Base2, Base3):
    <statement-1>
    ...
    <statement-N>
```

需要注意括号中父类的顺序，若是父类中有相同的方法名，而在子类使用时未指定，`Python` 会从左至右搜索 即方法在子类中未找到时，从左到右查找父类中是否包含方法。

```python
class people:
    name = ''
    age = 0
    __weight = 0
    def __init__(self, n, a, w):
        self.name = n
        self.age = a
        self.__weight = w
    def speak(self):
        print('%s 说：我 %d 岁' %(self.name, self.age))

class student(people):
    grade = ''
    def __init__(self, n, a, w, g):
        people.__init__(self, n, a, w)
        self.grade = g
    def speak(self):
        print('%s 说：我 %d 岁了，我在读 %d 年级' %(self.name, self.age, self.grade))

class speaker():
    topic = ''
    name = ''
    def __init__(self, n, t):
        self.topic = t
        self.name = n
    def speak(self):
        print('我叫 %s，我是一个程序员，我分享的主题是 %s' %(self.name, self.topic))

class sample(student, speaker):
    a = ''
    def __init__(self, n, a, w, g, t):
        student.__init__(self, n, a, w, g)
        speaker.__init__(self, n, t)
        
test = sample('zhums', 18, 170, 4, 'Python')
test.speak()

>>>
zhums 说：我 10 岁了，我在读 4 年级
```

### 3、方法重写

如果父类方法的功能不能满足需求，可以在子类重写父类的方法，实例如下：

```

```













