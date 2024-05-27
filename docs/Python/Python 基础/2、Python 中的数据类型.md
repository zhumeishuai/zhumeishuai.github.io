在 Python 中所有的数据类型都是类，每个数据值都是类的 "实例"。

```python
# 在 Python 中使用 type() 函数来判断对象的数据类型
type(Object)
```

## 1、数字

Python 中的数字类型有 4 种：

-   整数
-   浮点数
-   复数
-   布尔，布尔类型事实上是整数的一种。

### 1、整数

Python 中的整数为 `int`  类，整数类型的范围可以很大，表示很大的整数，只受计算机硬件的限制。

```python
int1=28				# 十进制表示方式
int2=0b11100		# 二进制表示方式，以数字 0 和字母 b/B 作为前缀
int3=0o34			# 八进制表示方式，以数字 0 和字母 o/O 作为前缀
int4=0x1c			# 十六进制表示方式，以数字 0 和字母 x/X 作为前缀
print (int1, type(int1))
print (int2, type(int2))
print (int3, type(int3))
print (int4, type(int4))

>>> 
28 <class 'int'>
28 <class 'int'>
28 <class 'int'>
28 <class 'int'>
```

### 2、浮点数

Python 的浮点数为 `float` 类，Python 只支持双精度浮点数，而且是与本机相关的。

```python
float1=2.2			# 十进制表示方式
float2=2.222e2		# 科学计数法表示方式，以字母 e/E 表示 10 的指数。
print (float1, type(float1))
print (float2, type(float2))

>>>
2.2 <class 'float'>
222.2 <class 'float'>
```

>   写成科学计数法的形式就是小数，即使最终的值像是一个整数。如：2e2 等价与 200，但 2e2 是一个小数。

### 3、复数

Python 中的复数为 `complex` 类。

复数由实部和虚部构成，在 Python 中，复数的虚部以 `j/J ` 为后缀，具体格式为：`a+bj`

```python
print ((2+2j)+(2))
print ((2+2j)+(2j))
print ((2+2j)+(2+2j))
print ((2+2j)+(2-2j))
print ((2+2j)*(2))
print ((2+2j)*(2j))
print ((2+2j)*(2+2j))

num1=2+2j
print (num1, type(num1))
>>>
(4+2j)
(2+4j)
(4+4j)
(4+0j)
(4+4j)
(-4+4j)
8j
(2+2j) <class 'complex'>
```

### 4、布尔

Python 中的布尔为 `bool` 类，`bool` 是 `int` 的子类，它只有两个值：`True` 和 `False`。

```python
bool1=True
bool2=False
print (bool1, type(bool1))
print (bool2, type(bool2))

>>>
True <class 'bool'>
False <class 'bool'>
```

### 5、数字类型间类型转换

Python 的数字类型中，除复数外，其它三中数字类型都可以相互转换，分为隐式转换和显式转换。

#### 1、隐式转换

数字之间可以进行数学计算，在数学计算时若数字的类型不同，则会发生隐式转换。

| 数字 a 的类型 | 数字 b 的类型 | 转换后的类型 |
| ------------- | ------------- | ------------ |
| bool          | int           | int          |
| bool、int     | float         | float        |

```python
num1=1+True
num2=1.0+True
num3=1+1.0
print (num1, type(num1))
print (num2, type(num2))
print (num3, type(num3))

>>>
2 <class 'int'>
2.0 <class 'float'>
2.0 <class 'float'>
```

#### 2、显式转换

在上面隐式转换的例子中，表达式 `1+1.0` 中的 `1` 被隐式转换为浮点数 `1.0`，但在有些时候希望把浮点数 `1.0` 转换为整数 `1`。这时候可以使用数字类型转换函数进行显式转换。

除复数外，其它三种数字类型都有自己的转换函数，分别是：`int()`、`float()`、`bool()` 函数。

```python
num1=int(1.0)			# 浮点数 1.0 被转换成整数 1
num2=int(True)			# 布尔值 True 被转换成整数 1
num3=float(1)			# 整数 1 被转换成浮点数 1.1
num4=float(True)		# 布尔值 True 被转换成浮点数 1.0
num5=bool(0)			# 整数 0 被转换为 False
num6=bool(2)			# 非 0 整数被转换成 True
num7=bool('')			# 空字符串被转换成 False
num8=bool(' ')			# 非空字符串被转换成 True
print (num1, type(num1))
print (num2, type(num2))
print (num3, type(num3))
print (num4, type(num4))
print (num5, type(num5))
print (num6, type(num6))
print (num7, type(num7))
print (num8, type(num8))

>>>
1 <class 'int'>
1 <class 'int'>
1.0 <class 'float'>
1.0 <class 'float'>
False <class 'bool'>
True <class 'bool'>
False <class 'bool'>
True <class 'bool'>
```

## 2、序列

序列是一种可迭代、元素有序的数据，指的是一块可存放多个值的连续内存空间，这些值按一定顺序排列，可通过每个值所在位置的编号（称为索引）访问它们。

在 Python 中，序列包括字符串、列表、元组、集合和字典，这些序列支持以下几种通用的操作，但比较特殊的是，集合和字典不支持索引、切片、相加和相乘操作。

### 1、序列索引



序列中，每个元素都有属于自己的编号（索引）。从起始元素开始，索引值从 0 开始递增如下图：

![image-20231122101849100](https://storage.zhums.cn/d/images/202311221018152.png)

Python 还支持索引值是负数，此类索引是从右向左计数，换句话说，从最后一个元素开始计数，从索引值 -1 开始，如下图：

<img src="https://storage.zhums.cn/d/images/202311221020627.png" style="zoom:80%;" />

>   注意: 在使用负值作为列序中各元素的索引值时，是从 -1 开始，而不是从 0 开始。

```python
str1="Hello World"
print ("str1[0]:",str1[0])
print ("str1[-1]:",str1[-1])

>>>
str1[0]: H
str1[-1]: d
```

### 2、序列切片

切片操作是访问序列中元素的另一种方法，它可以访问一定范围内的元素，通过切片操作，可以生成一个新的序列。

序列实现切片操作的语法格式如下：

>`sname[start:end:step]`
>
>-   `sname`：表示序列的名称；
>-   `start`：表示切片的开始索引位置（包括该位置），默认为 0；
>-   `end`：表示切片的结束索引位置（不包括该位置），默认为序列的长度；
>-   `step`：表示在切片过程中的步长，默认为 1；
>    -   若 `step > 0`, 则表示从左向右切片。此时，`start` 必须小于 `end` 才有结果，否则为空。 
>    -   若 `step < 0`, 则表示从右到左切片。此时，`start` 必须大于 `end` 才有结果，否则为空。

>   len() 函数用于返回序列的长度即元素的个数。

```python
str1="Hello World"
print (len(str1))

>>>
11
```

```python
str1="Hello World"
print (str1[:2])
print (str1[2:4])
print (str1[:6:2])
```

### 3、序列相加、相乘

#### 1、序列相加

Python 中，可以使用加 `(+)` 运算符将两个相同数据类型的序列连接起来。

```python
str=('Hello')
print (str + ' Python')

>>>
Hello Python
```

#### 2、序列相乘

Python 中，可以使用乘 `(*)` 运算符将支持一个序列 `*` 数字 `n` 运算符可以将一个序列重复多次。

```python
str=('Hello')
print (str * 3)

>>>
HelloHelloHello
```

>   比较特殊的是，列表类型在进行乘法运算时，还可以实现初始化指定长度列表的功能。例如如下的代码，将创建一个长度为 `5` 的列表，列表中的每个元素都是 `None`，表示什么都没有。

```python
list = [None] * 5
print (list)

>>>
[None, None, None, None, None]
```

### 4、判断元素是否在序列中

测试元素是否在序列中的运算符有两个：`in` 和 `not in`，`in` 用于测试是否包含某一个元素，`not in` 用于测试是否不包含某一个元素。

```python
str = "Hello World"
print ('W' in str)
print ('W' not in str)

>>>
True
False
```

### 5、和序列相关的内置函数

| 函数        | 说明                                            |
| ----------- | ----------------------------------------------- |
| len()       | 返回序列的长度，即序列中元素的个数              |
| max()       | 返回序列中最大的元素                            |
| min()       | 返回序列中最小的元素                            |
| list()      | 将序列转换为列表                                |
| str()       | 将序列转换为字符串                              |
| sum()       | 返回序列元素之和                                |
| sorted()    | 对序列中的元素排序                              |
| reverse()   | 对序列中的元素反向排序                          |
| enumerate() | 将序列组合为一个索引序列，一般用于 `for` 循环中 |

```python
list=[2,1,3]
print (len(list), max(list), min(list))
print (sum(list), sorted(list))

>>>
3 3 1
6 [1, 2, 3]
```



### 6、字符串

字符串是一个有序的，不可修改的，以引号包围的序列。在 Python 中双引号或单引号中的数据，就是字符串。在 Python 中双引号和单引号没有任何区别。

#### 字符串中的特殊字符

```python
\			# 转义符
\在行尾时	 # 续行符
\a			# 响铃
\b			# 退格
\000		# 空
\n			# 换行
\v			# 纵向制表符
\t			# 横向制表符
\r			# 回车
\f			# 换页
```

#### 字符串拼接

##### 字符串拼接

在 Python 中拼接（连接）字符串直接将两个字符串紧挨着写在一起即可，这种方法使能够拼接字符串常量，具体格式为：

```python
strname = "str1" "str2"
```

-   `strname`: 表示拼接以后的字符串变量名
-   `str1/str2`: 表示要拼接的字符串内容

```python
str1="Baidu" "https://www.baidu.com"
print(str1)

>>>
Baiduhttps://www.baidu.com
```

如果需要使用变量，就需要借助 `+` 运算符来拼接，具体格式为:

```python
strname = str1 + str2
```

```python
str1="Baidu"
str2="http://www.baidu.com"
str3=str1 + str2
print(str3)

>>>
Baiduhttps://www.baidu.com
```

##### 字符串和数字的拼接

Python 不允许直接拼接数字和字符串，必须先将数字转换成字符串。可以借助 `str()` 和 `repr()` 函数将数字转换为字符串。

```python
str(Object)
repr(Object)
```

```python
name="zhums"
age=21
day=1000
info=name + "已经" + str(age) + "岁了," + "已经活了" + repr(day) + "天了"
print(info)

>>>
zhums已经21岁了,已经活了1000天了
```

>`str()` 和 `repr()` 的区别:
>
>-   `str()` 用于将数据转换成适合人类阅读的字符串形式。
>-   `repr()` 用于将数据转换成适合解释器阅读的字符串形式（Python 表达式的形式），适合在开发和调试阶段使用；如果没有等价的语法，则会发生 SyntaxError 异常。

```python
s = "https://www.baidu.com"
s_str = str(s)
s_repr = repr(s)
print( type(s_str), s_str)
print( type(s_repr), s_repr )

>>>
<class 'str'> https://www.baidu.com
<class 'str'> 'https://www.baidu.com'
```

上面的例子中，`s` 本身就是一个字符串，但是我们依然使用 `str()` 和 `repr()` 对它进行了转换。从运行结果可以看出，`str()` 保留了字符串最原始的样子，而 `repr()` 使用引号将字符串包围起来，这就是 Python 字符串的表达式形式。

另外，在 Python 交互式编程环境中输入一个表达式（变量、加减乘除、逻辑运算等）时，Python 会自动使用 `repr()` 函数处理该表达式。

#### len() 函数: 获取字符串长度或字节数

```python
str="Hello World"
print(len(str))		# 获取字符串的长度

>>>
11
```

在 Python 中，不同的字符所占的字节数不同，数字、英文字母、小数点、下划线以及空格，各占一个字节，而一个汉字可能占 `2~4` 个字节，具体占多少个，取决于采用的编码方式。例如，汉字在 `GBK/GB2312` 编码中占用 `2` 个字节，而在 `UTF-8` 编码中一般占用 `3` 个字节。

>   `encode()` 方法用于对字符串进行编码，默认使用 `UTF-8`。

```python
str="人生苦短，我用 Python"	# 6 个汉字和 1 个中文标点占 21 个字节，6 个英文和 1 个英文标点占用 7 个字节
print(len(str.encode()))

>>>
28
```

```python
str="人生苦短，我用 Python"	# 6 个汉字和 1 个中文标点占 14 个字节，6 个英文和 1 个英文标点占用 7 个字节
print(len(str.encode('GBK')))

>>>
21
```

#### split() 方法: 分割字符串

`split()` 方法用于将一个字符串按照指定的分隔符切分成多个字符串，这些字符串会保存到列表中，作为方法的返回值反馈出来，基本语法如下:

```python
str.split(sep,maxsplit)
```

-   str: 表示要进行分割的字符串
-   sep: 指定分隔符，可以包含多个字符。默认为 `None`，表示所有空字符，包括空格、换行符 "\n" 制表符 "\t" 等
-   maxsplit: 可选参数，用于指定分割的次数，最后列表中子串的个数最多为 `maxsplit+1`。如果不指定或者指定为 `-1`，表示没有限制

>   如果不指定 `sep` 参数，需要以 `maxsplit=x` 的方式指定 `maxsplit` 参数

```python
str1="www.baidu.com"
str2="www baidu com"
print(str1.split('.'))
print(str1.split('baidu'))
print(str1.split('.', 1))
print(str2.split(maxsplit=1))

>>>
['www', 'baidu', 'com']
['www.', '.com']
['www', 'baidu.com']
['www', 'baidu com']
```

#### join() 方法: 合并字符串

`join()` 方法是 `split()` 方法的逆方法，用来将列表（或元组）中包含的多个字符串连接成一个字符串。

使用 `join()` 方法合并字符串时，它会将列表（或元组）中多个字符串采用固定的分隔符连接在一起。例如: 字符串 "www.baidu.com" 可以看做是通过分隔符 "." 将 `['www', 'baidu', 'com']` 列表合并为一个字符串的结果。

`join()` 方法的语法格式如下：

```python
newstr = symbol.join(iterable)
```

-   `newstr`: 合并后生成的新字符串
-   `symbol`: 指定合并时的分隔符
-   `iterable`: 合并操作的源字符串数据，允许以列表、元组等形式提供

```python
list1=['www', 'baidu', 'com']
tup1=('', 'usr', 'bin', 'python')
print('.'.join(list1))
print('/'.join(tup1))

>>>
www.baidu.com
/usr/bin/python
```

#### count() 方法: 统计字符串出现的次数

`count()` 方法用于统计一个字符串在另一个字符串中出现的次数，若检索的字符串不存在，则返回 0，否则返回出现的次数。

`count()` 方法的语法格式如下：

```python
str.count(sub[,strart[,end]])
```

-   `str`: 原字符串
-   `sub`: 要检索的字符串
-   `start`: 检索的起始位置，默认从头开始检索
-   `end`: 检索的结束位置，默认检索到末尾

```python
str1="Hello World"
print(str1.count('o'))
print(str1.count('o', 5))
print(str1.count('o', 0, -3))
print(str1.count('A'))

>>>
2
1
2
0
```

#### find() 方法: 检测字符串中是否包含某子串

`find()` 方法用于检索字符串中是否包含目标字符串，如果包含，则返回第一次出现该字符串的索引；反之，则返回 `-1`。

`find()` 方法的语法格式如下:

```python
str.find(sub[,start[,end]])
```

-   `str`: 原字符串；
-   `sub`: 要检索的目标字符串；
-   `start`: 开始检索的起始位置。默认从头开始
-   `end`: 结束检索的结束位置。默认检索到结尾

```python
str1="Hello World"
print(str1.find('o'))
print(str1.find('o',5))
print(str1.find('o',1,-5))
print(str1.find('A'))

>>>
4
7
4
-1
```

`Python` 中还提供了 `rfind()` 方法，与 `find()` 方法不同的在于 `rfind()` 从字符串右边开始检索。

```python
str1="Hello World"
print(str1.rfind('o'))

>>>
7
```

#### ljust()/rjust()/center() 方法: 文本对齐

##### ljust() 方法

`ljust()` 方法的功能是向指定字符串的右侧填充指定字符，从而达到左对齐文本的目的。

`ljust()` 方法的基本格式如下：

```python
str.ljust(width[, fillchar])
```

其中各个参数的含义如下：

-   `str`: 要进行填充的字符串；
-   `width`: 包括 str 本身长度在内，字符串要占的总长度；
-   `fillchar`: 可选参数，指定填充字符串时所用的字符，默认使用空格。

```python
str1="http://www.baidu.com"
str2="www.baidu.com"
print(str1.ljust(21, '#'))
print(str2.ljust(21, '#'))

>>>
http://www.baidu.com#
www.baidu.com########
```

##### rjust() 方法

`rjust()` 和 `ljust()` 方法类似，唯一的不同在于，``rjust()`` 方法是向字符串的左侧填充指定字符，从而达到右对齐文本的目的。

`rjust()` 方法的基本格式如下：

```python
str.rjust(width[, fillchar])
```

其中各个参数的含义和 `ljust()` 完全相同。

```python
str1="http://www.baidu.com"
str2="www.baidu.com"
print(str1.rjust(21, '#'))
print(str2.rjust(21, '#'))

>>>
#http://www.baidu.com
########www.baidu.com
```

##### center() 方法

`center()` 字符串方法与 `ljust()` 和 `rjust()` 的用法类似，但它让文本居中，而不是左对齐或右对齐。

`center()` 方法的基本格式如下：

```python
str.center(width[, fillchar])
```

其中各个参数的含义和 `ljust()` 方法相同。

```python
str1="http://www.baidu.com"
str2="www.baidu.com"
print(str1.center(24, '#'))
print(str2.center(24, '#'))

>>>
##http://www.baidu.com##
#####www.baidu.com######
```

#### startswith()/endswith() 方法: 检测字符串是否以指定字符串开头或结尾

##### startswith() 方法

`startswith()` 方法用于检索字符串是否以指定字符串开头，如果是返回 `True`；反之返回 `False`。语法格式如下：

```python
str.startswith(sub[,start[,end]])
```

-   `str`: 原字符串；
-   `sub`: 要检索的子串；
-   `start`: 指定检索开始的起始位置索引，默认从头开始检索；
-   `end`: 指定检索的结束位置索引，默认检索到结束。

```python
str1="http://www.baidu.com"
print(str1.startswith('http'))
print(str1.startswith('w'))
print(str1.startswith('w', 7))

>>>
True
False
True
```

##### endswith() 方法

`endswith()` 方法用于检索字符串是否以指定字符串结尾，如果是则返回 `True`；反之则返回 `False`。语法格式如下：

```python
str.endswith(sub[,start[,end]])
```

此格式中各参数的含义如下：

-   `str`：原字符串；
-   `sub`：要检索的字符串；
-   `start`：指定检索开始时的起始位置索引，默认从头开始检索。
-   `end`：指定检索的结束位置索引，默认一直检索到结束。

```python
str1="http://www.baidu.com"
print(str1.endswith('m'))
print(str1.endswith('com'))
print(str1.endswith('com', 7))

>>>
True
True
True
```

#### 大写小转换的方法

>   注意: 以下 3 个方法都仅限于将转换后的新字符串返回，而不会修改原字符串。

##### title() 方法

`title()` 方法用于将字符串中每个单词的首字母转为大写，其他字母全部转为小写，转换完成后，此方法会返回转换得到的字符串。如果字符串中没有需要被转换的字符，此方法会将字符串原封不动地返回。

`title()` 方法的语法格式如下：

```python
str.title()
```

-   `str` 表示要进行转换的字符串。

```python
str1="http://www.baidu.com"
print(str1.title())

>>>
Http://Www.Baidu.Com
```

##### lower() 方法

`lower()` 方法用于将字符串中的所有大写字母转换为小写字母，转换完成后，该方法会返回新得到的字符串。如果字符串中原本就都是小写字母，则该方法会返回原字符串。

`lower()` 方法的语法格式如下：

```python
str.lower()
```

-   `str`: 要进行转换的字符串。

```python
str1="WWW.BAIDU.COM"
print(str1.lower())

>>>
www.baidu.com
```

##### upper() 方法

`upper()` 方法用于将字符串中的所有小写字母转换为大写字母，转换完成后，该方法会返回新得到的字符串。反之，则返回原字符串。

`upper()` 方法的语法格式如下：

```python
str.upper()
```

-   `str`: 要进行转换的字符串。

```python
str1="www.baidu.com"
print(str1.upper())

>>>
WWW.BAIDU.COM
```

#### 删除字符串中空格的方法

用户输入数据时，很有可能会无意中输入多余的空格，或者在一些场景中，字符串前后不允许出现空格和特殊字符，此时就需要去除字符串中的空格和特殊字符。这里的特殊字符，指的是制表符（\t）、回车符（\r）、换行符（\n）等。

`Python` 中，字符串变量提供了 3 种方法来删除字符串中多余的空格和特殊字符，它们分别是：

-   `strip()`：删除字符串左右两侧的空格或特殊字符。
-   `lstrip()`：删除字符串左边的空格或特殊字符。
-   `rstrip()`：删除字符串右边的空格或特殊字符。

>   注意，Python 的 str 是不可变的（不可变的意思是指，字符串一旦形成，它所包含的字符序列就不能发生任何改变），因此这三个方法只是返回字符串前面或后面空白被删除之后的副本，并不会改变字符串本身。

##### strip() 方法

`strip()` 方法用于删除字符串左右两个的空格和特殊字符，该方法的语法格式为：

```python
str.strip([chars])
```

-   `str`: 原字符串
-   `chars`: 用来指定要删除的字符，可以同时指定多个，默认删除空格、制表符、回车符、换行符等特殊字符。

```python
str1="www.baidu.com  \n"
print(str1.strip())
print(str1)

>>>
www.baidu.com
www.baidu.com

```

##### lstrip() 方法

`lstrip()` 方法用于去掉字符串左侧的空格和特殊字符。该方法的语法格式如下：

```python
str.lstrip([chars])
```

`str` 和 `chars` 参数的含义，分别同 `strip()` 语法格式中的 `str` 和 `chars` 完全相同。

```python
str1="\n www.baidu.com"
print(str1.lstrip())
print(str1)

>>>
www.baidu.com

 www.baidu.com
```

##### rstrip() 方法

`rstrip()` 方法用于去掉字符串右侧的空格和特殊字符。该方法的语法格式如下：

```python
str.rstrip([chars])
```

`str` 和 `chars` 参数的含义，分别同 `rtrip()` 语法格式中的 `str` 和 `chars` 完全相同。

```python
str1="www.baidu.com \n"
print(str1.rstrip())
print(str1)

>>>
www.baidu.com
www.baidu.com 

```

#### format() 方法: 格式化输出

`format()` 方法语法格式如下:

```python
str.format(args)
```

-   `str`: 指定字符串的显示样式
-   `args`: 指定要进行格式转换的项，如果有多项，之间有逗号进行分割。

在创建显示样式模板时，需要使用 `{}` 和 `:` 来指定占位符，其完整的语法格式为：

```
{ [index][ : [ [fill] align] [sign] [#] [width] [.precision] [type] ] }
```

>   注意，格式中用 [] 括起来的参数都是可选参数，即可以使用，也可以不使用。各个参数的含义如下：

-   `index`: 指定后边设置的格式要作用到 `args` 中第几个数据，数据的索引值从 `0` 开始。如果省略此选项，则会根据 `args` 中数据的先后顺序自动分配

-   `fill`: 指定空白处填充的字符。注意，当填充字符为逗号(,)且作用于整数或浮点数时，该整数（或浮点数）会以逗号分隔的形式输出，例如（`1000000` 会输出 `1,000,000`）

    ```python
    print("货币形式：{:,d}".format(1000000))
    
    >>>
    货币形式：1,000,000
    ```

-   `align`: 指定数据的对齐方式，具体的对齐方式如下:

    | align | 说明                                                         |
    | ----- | ------------------------------------------------------------ |
    | <     | 数据左对齐                                                   |
    | >     | 数据右对齐                                                   |
    | =     | 数据右对齐，同时将符号放置在填充内容的最左侧，该选项只对数字类型有效 |
    | ^     | 数据居中，此选项需和 `width` 参数一起使用                    |

-   `sign`: 指定有无符号数，此参数的值及说明如下表:

    | sign | 说明                                                         |
    | ---- | ------------------------------------------------------------ |
    | +    | 正数前加正号，负数前加负号                                   |
    | -    | 正数前不加正号，负数前加负号                                 |
    | 空格 | 正数前加空格，负数前加负号                                   |
    | #    | 对于二进制数、八进制数和十六进制数，使用此参数，各进制数前会分别显示 `0b、0o、0x` 前缀；反之则不显示前缀 |

    ```python
    print("100的十六进制：{:#x}".format(100))
    
    >>>
    100的十六进制：0x64
    ```

-   `width`: 指定输出数据时所占的宽度。

-   `.precision`: 指定保留的小数位数。

    ```python
    #输出百分比形式
    print("0.111的百分比表示：{:.0%}".format(0.111))
    
    >>>
    0.111的百分比表示：11%
    ```

-   `type`: 指定输出数据的具体类型

    | type | 说明                                                  |
    | ---- | ----------------------------------------------------- |
    | s    | 对字符串类型格式化                                    |
    | d    | 十进制整数                                            |
    | c    | 将十进制整数自动转换为对应的 `Unicode` 字符           |
    | e/E  | 转化成科学记数法后，再格式化输出                      |
    | g/G  | 自动在 `e/E` 和 `f/F` 中切换                          |
    | b    | 将十进制数自动转换成二进制表示，再格式化输出          |
    | o    | 将十进制数自动转换成八进制表示，再格式化输出          |
    | x/X  | 将十进制数自动转换成十六进制表示，再格式化输出        |
    | f/F  | 转换为浮点数（默认小数点后保留 `6` 位），再格式化输出 |
    | %    | 显示百分比（默认显示小数点后 `6` 位）                 |

    ```python
    #科学计数法表示
    print("科学计数法：{:E}".format(1200.12))
    
    >>>
    科学计数法：1.200120E+03
    ```

```python
str="Name:{:>8s}\nName:{:>8}"
print(str.format("Python","Java"))

>>>
Name:  Python
Name:    Java
```

#### encode()/decode() 方法: 编码转换

在 `Python` 中，有 `2` 种常用的字符串类型，分别为 `str` 和 `bytes` 类型，其中 `str` 用来表示 `Unicode` 字符，`bytes` 用来表示二进制数据。`str` 类型和 `bytes` 类型之间就需要使用 `encode()` 和 `decode()` 方法进行转换。

##### encode() 方法：编码

`encode()` 方法用于将 `str` 类型转换成 `bytes` 类型，这个过程也称为 "编码"，语法格式如下:

```python
str.encode([encoding="UTF-8"][,errors="strict"])
```

-   `str`: 要进行转换的字符串

-   `encoding`: 指定编码采用的字符编码，默认 `utf-8`，当方法中只使用这一个参数时，可以省略 `encoding=`

-   `errors`: 指定错误处理方式，默认值为 `strict` 

    `strict`: 遇到非法字符就抛出异常

    `ignore`: 忽略非法字符

    `replace`: 用 `'?'` 替换非法字符

    `xmlcharrefreplace`: 使用 `xml` 的字符引用

>   注意: 使用 `encode()` 方法对原字符串进行编码，不会直接修改原字符串。

```python
str1 = '我爱 Python'
print (str1.encode())
print (str1.encode('GBK'))

>>>
b'\xe6\x88\x91\xe7\x88\xb1 Python'
b'\xce\xd2\xb0\xae Python'
```

##### decode() 方法：解码

`decode()` 方法用于将 `bytes` 类型的二进制数据转换为 `str` 类型，这个过程也称为 "解码"，语法格式如下:

```python
str.decode([encoding="UTF-8"][,errors="strict"])
```

-   `str`: 要进行转换的字符串

-   `encoding`: 指定解码采用的字符编码，默认 `utf-8`，当方法中只使用这一个参数时，可以省略 `encoding=`，对 `bytes` 类型数据解码要选择和编码时一样的格式。

-   `errors`: 指定错误处理方式，默认值为 `strict` 

    `strict`: 遇到非法字符就抛出异常

    `ignore`: 忽略非法字符

    `replace`: 用 `'?'` 替换非法字符

    `xmlcharrefreplace`: 使用 `xml` 的字符引用

```python
str1 = '我爱 Python'
bytes1 = str1.encode(encoding='GBK')
print(bytes1.decode('GBK'))
print(bytes1.decode(encoding='UTF-8', errors='replace'))		# 不指定 errors 默认会抛出异常

>>>
我爱 Python
�Ұ� Python
```

##### 编码转换

```python

```

#### f-string 格式化字符串

[Python字符串格式化问题：%、format()与f-strings - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/90439125#:~:text=f-Strings：一种改进版格式化方式 1 最简单的句法 f-strings 的句法类似于 str.format () ，但要更简洁，你可以感受一下它的可读性：,运行效率 f-string 中的 f 前缀也可以是 “fast” 的意思。 )

```python
>>> name = 'zhums'
>>> f'name:{name}'
'name:zhums'
>>> f'{10 * 10}'   
'100'
```

### 7、列表

列表是一个有序的，可修改的，元素以逗号分隔，以中括号包围的序列。

#### 1、定义列表

>   1、使用 [ ] 创建列表

```python
list=[]			# 定义一个空列表
Name=['zhums', 'wuyi']
Info=['zhums', 21, ['zhums', 21]]	# 列表中的元素可以为任何 Python 支持的数据类型
print (list, Name, Info)

>>>
[] ['zhums', 'wuyi'] ['zhums', 21, ['zhums', 21]]
```

>   2、使用 `list()` 函数创建列表

除了使用 `[ ]` 创建列表外，Python 还提供了一个内置的函数 `list()`，使用它可以将其它数据类型转换为列表类型。

```python
tuple1 = ('Python', 'Java', 'C++', 'JavaScript')
dict1 = {'a':100, 'b':42, 'c':9}
range1 = range(1, 6)
list1 = list("hello")		# 将字符串转换成列表
list2 = list(tuple1)		# 将元组转换成列表
list3 = list(dict1)			# 将字典转换成列表
list4 = list(range1)		# 将区间转换成列表
print(list1)
print(list2)
print(list3)
print(list4)

>>>
['h', 'e', 'l', 'l', 'o']
['Python', 'Java', 'C++', 'JavaScript']
['a', 'b', 'c']
[1, 2, 3, 4, 5]
```

#### 2、删除列表

使用 `del` 关键字来删除列表，但实际开发中并不经常删除列表，因为 `Python` 自带的垃圾回收机制会自动销毁无用的列表，即使开发者不手动删除，``Python` 也会自动将其回收。

```python
# del 关键字语法格式：
del List_Name
```

```python
lang = ["Python", "MATLAB"]
del lang
print (lang)

>>>
print (lang)
NameError: name 'lang' is not defined
```

#### 3、添加元素

##### 1、+ 运算符连接列表

`+` 运算符可以将多个序列连接起来；列表是序列的一种，所以也可以使用 `+` 进行连接，相当于在第一个列表的末尾添加了另一个列表。

```python
list1=[1,2,3]
list2=[4,5,6]
print (list1 + list2)

>>>
[1, 2, 3, 4, 5, 6]
```

##### 2、append() 方法追加单个元素

`append()` 方法用于在列表的末尾追加指定元素。

```python
# append() 方法语法如下：
List_Name.append(Object)
```

-   List_Name: 表示要添加元素的列表
-   Object: 表示要追加的数据，可以是单个元素，也可以是列表、元组等。

```python
list1 = ['Python', 'Java']
t = ('JavaScript', 'C#')
list1.append('Shell')    		# 追加单个元素
print(list1)
list1.append(t)    				# 追加元组，整个元组被当成一个元素
print(list1)
list1.append(['Ruby', 'SQL'])	# 追加列表，整个列表也被当成一个元素
print(list1)

>>>
['Python', 'Java', 'Shell']
['Python', 'Java', 'Shell', ('JavaScript', 'C#')]
['Python', 'Java', 'Shell', ('JavaScript', 'C#'), ['Ruby', 'SQL']]
```

>   可以看到，当给 `append()` 方法传递列表或者元组时，此方法会将它们视为一个整体，作为一个元素添加到列表中，从而形成包含列表和元组的新列表。

##### 3、extend() 方法追加多个元素

>   `extend()` 和 `append()` 的不同之处在于：`extend()` 不会把列表或者元祖视为一个整体，而是把它们包含的元素逐个添加到列表中。

```python
# extend() 方法语法如下：
List_Name.extend(Object)
```

-   List_Name: 表示要添加元素的列表
-   Object: 表示要追加的数据，可以是单个元素，也可以是列表、元组等，但不能是单个数字。

```python
l = ['Python', 'Java']
l.extend('Go')				# 追加元素
t = ('JavaScript', 'C#')
print(l)
l.extend(t)					# 追加元组，元组被拆分成多个元素
print(l)
l.extend(['Ruby', 'SQL'])	# 追加列表，列表也被拆分成多个元素
print(l)

>>>
['Python', 'Java', 'G', 'o']
['Python', 'Java', 'G', 'o', 'JavaScript', 'C#']
['Python', 'Java', 'G', 'o', 'JavaScript', 'C#', 'Ruby', 'SQL']
```

##### 4、insert() 方法插入单个元素

`append()` 和 `extend()` 方法只能在列表末尾插入元素，如果希望在列表中间某个位置插入元素，那么可以使用 `insert()` 方法。

```python
List_Name.insert(Index,Object)
```

-   List_Name: 表示要添加元素的列表
-   Index: 表示指定位置的索引值
-   Object: 表示要插入的数据，可以是单个元素，也可以是列表、元组等，但不能是单个数字。

```python
l = ['Python']
t = ('C#', 'Go')
l.insert(0, 'C')		# 插入元素
print(l)
l.insert(1, t)			# 插入元组，整个元祖被当成一个元素
print(l) 
l.insert(2, ['Ruby'])	# 插入列表，整个列表被当成一个元素
print(l)
l.insert(0, "Hello")	# 插入字符串，整个字符串被当成一个元素
print(l)

>>>
['C', 'Python']
['C', ('C#', 'Go'), 'Python']
['C', ('C#', 'Go'), ['Ruby'], 'Python']
['Hello', 'C', ('C#', 'Go'), ['Ruby'], 'Python']
```

#### 4、删除元素

在 `Python` 列表中删除元素主要分为以下 3 种场景：

-   根据目标元素所在位置的索引进行删除，可以使用 `del` 关键字或者 `pop()` 方法；
-   根据元素本身的值进行删除，可使用列表（`list` 类型）提供的 `remove()` 方法；
-   将列表中所有元素全部删除，可使用列表（`list` 类型）提供的 `clear()` 方法。

##### 1、del 根据索引值删除元素

`del` 是 `Python` 中的关键字，专门用来执行删除操作，它可以删除整个列表，还可以删除列表中的某些元素或者删除某一段连续的元素。

1、`del` 删除单个元素语法如下：

```python
del List_Name[Index]
```

-   List_Name: 表示要删除元素的列表
-   Index: 表示指定位置的索引值

```python
lang = ["Python", "C++", "Java",  "MATLAB"]
del lang[2]			# 使用正数索引
print(lang)
del lang[-2]		# 使用负数索引
print(lang)

>>>
['Python', 'C++', 'MATLAB']
['Python', 'MATLAB']
```

2、`del` 删除连续元素语法如下：`del` 会删除从索引 `Start` 到 `End` 之间的元素，不包括 `End` 位置的元素。

```python
del List_Name[Start:End]
```

-   List_Name: 表示要删除元素的列表
-   Start: 表示开始位置的索引
-   End: 表示结束位置的索引

```python
lang = ["Python", "C++", "Java", "PHP", "MATLAB"]
del lang[1:3]
print(lang)
lang.extend(["SQL", "C#", "Go"])
print(lang)
del lang[-5:-2]
print(lang)

>>>
['Python', 'PHP', 'MATLAB']
['Python', 'PHP', 'MATLAB', 'SQL', 'C#', 'Go']
['Python', 'C#', 'Go']
```

##### 2、pop() 根据索引值删除元素

`Python` 中 `pop()` 方法用来删除列表中指定索引处的元素，具体语法如下:

```python
List_Name.pop(Index)
```

-   List_Name: 表示要删除元素的列表
-   Index: 表示要删除元素的索引值，默认为 `-1`

```python
lang = ["Python", "C++", "PHP", "MATLAB"]
lang.pop(1)
print(lang)
lang.pop()
print(lang)

>>>
['Python', 'PHP', 'MATLAB']
['Python', 'PHP']
```

##### 3、remove() 根据元素值删除元素

在 `Python` 中 `remove()` 方法会根据元素本身的值来进行删除操作。

>   注意: `remove()` 方法只会删除第一个和指定值相同的元素，而且必须保证该元素是存在的，否则会返回 `ValueError` 错误。

`remove()` 方法语法如下:

```python
List_Name.remove(Value)
```

-   List_Name: 表示要删除元素的列表
-   Value: 表示要删除的元素的值

```python
name = ['zhums', 'wuyi', 'zhaosy']
name.remove('zhaosy')
print(name)

>>>
['zhums', 'wuyi']
```

##### 4、clear() 删除所有元素

在 `Python` 中 `clear()` 方法用来删除列表的所有元素，即清空列表。

```python
name = ['zhums', 'wuyi', 'zhaosy']
name.clear()
print(name)

>>>
[]
```

#### 5、修改元素

##### 1、修改单个元素

修改单个元素直接使用 `=` 赋值运算符即可。

```python
lang = ['Python', 'Shell', 'C++']
lang[1]='Java'
print(lang)
lang[-3]='Shell'
print(lang)

>>>
['Python', 'Java', 'C++']
['Shell', 'Java', 'C++']
```

##### 2、修改多个元素

`Python` 支持通过切片语法给一组元素赋值。在进行这种操作时，如果不指定步长（`step` 参数），`Python` 就不要求新赋值的元素个数与原来的元素个数相同；这意味，该操作既可以为列表添加元素，也可以为列表删除元素。

```python
nums = [1, 2, 3, 4, 5]
nums[1:4] = [22, 33, 44]# 修改第 2-5 个元素的值（不包括第 5 个元素）
print(nums)

>>>
[1, 22, 33, 44, 5]
```

如果对空切片（`slice`）赋值，就相当于插入一组新的元素：

```python
nums = [1, 2, 3, 4, 5]
nums[3:3] = [22, 222]		# 在索引 3 处插入元素
print(nums)

>>>
[1, 2, 3, 22, 222, 4, 5]
```

>   使用切片语法赋值时，`Python` 不支持单个值，例如下面的写法就是错误的：

```python
nums[4:4] = 77
```

如果使用字符串赋值，`Python` 会自动把字符串转换成序列，其中的每个字符都是一个元素，如下:

```python
s = list("Hello")
s[2:4] = "XYZ"
print(s)

>>>
['H', 'e', 'X', 'Y', 'Z', 'o']
```

使用切片语法时也可以指定步长（`step` 参数），这个时候就要求所赋值的新元素的个数与原有元素的个数相同，例如：

```python
nums = [1, 2, 3, 4, 5, 6, 7]		# 步长为 2，为第 1、3、5 个元素赋值
nums[1:6:2] = [11, 22, 33]
print(nums)

>>>
[1, 11, 3, 22, 5, 33, 7]
```

#### 6、列表的查找

##### 1、index() 方法

`index()` 方法用来查找某个元素在列表中出现的位置（也就是索引），如果该元素不存在，则会导致 `ValueError` 错误，所以在查找之前最好使用 `count()` 方法判断一下。

```python
# index() 语法如下：
List_Name.index(Object, Start, End)
```

-   List_Name: 列表名称
-   Object: 要查找的元素
-   Start: 表示起始位置，默认从列表开头
-   End: 表示结束位置，默认到列表结尾

```python
nums = [40, 2, 100, 7, -20.5]
print( nums.index(2) )			# 检索列表中的所有元素
print( nums.index(100, 1, 3) )	# 检索索引 1-3 之间的元素
print( nums.index(7, 2) )		# 检索索引 2 之后的元素

>>>
1
2
3
```

##### 2、count() 方法

`count()` 方法用来统计某个元素在列表中出现的次数。

```python
# count() 语法如下：
List_Name.count(Object)
```

-   List_Name: 列表名称
-   Object: 要统计的元素

```python
nums = [40, 36, 100, -20.5, 36]
#统计元素出现的次数
print("36 出现了 %d 次" %nums.count(36))
#判断一个元素是否存在
if nums.count(100):
    print("列表中存在 100 这个元素")
else:
    print("列表中不存在 100 这个元素")

>>>
36 出现了 2 次
列表中存在 100 这个元素
```

#### 7、列表的排序

##### 1、reverse() 方法

```python
reverse
'''
说明：对列表中的元素进行反向排序
语法：reverse()
'''
```

##### 2、sort() 方法

```python
sort
'''
说明：按照 ASCII 码表进行排序
语法：sort()
'''
```

```python
list1 = ['data2', 'data1', 'data3']
list1.reverse()
print(list1)
list1.sort()
print(list1)	

>>>
['data3', 'data1', 'data2']
['data1', 'data2', 'data3']
```

### 8、元组

元组（`tuple`）是 `Python` 中另一个重要的序列结构，和列表类似，元组也是由一系列按特定顺序排序的元素组成。

>   元组和列表（`list`）的不同之处在于：
>
>   -   列表的元素是可以更改的，包括修改元素值，删除和插入元素，所以列表是可变序列；
>   -   而元组一旦被创建，它的元素就不可更改了，所以元组是不可变序列。
>
>   元组也可以看做是不可变的列表，通常情况下，元组用于保存无需修改的内容。

元组的所有元素都放在一对小括号 `( )` 中，相邻元素之间用逗号`,`分隔，如下所示：

```python
(element1, element2, ... , elementn)
```

其中 `element1~elementn` 表示元组中的各个元素，个数没有限制，只要是 Python 支持的数据类型就可以。

#### 1、定义元组

##### 1、使用 () 创建元组

```python
Tuple_Name=(element1, element2, ..., elementn)
```

>   **注意:** 当创建的元组中只有一个字符串类型的元素时，该元素后面必须要加一个逗号`','`否则 `Python` 解释器会将它视为字符串。如下所示：

```python
a = ("Hello World")# 不加逗号
b = ("Hello World",)# 加逗号
print(type(a), a)
print(type(b), b)

>>>
<class 'str'> Hello World
<class 'tuple'> ('Hello World',)
```

>   也可以省略小括号

```python
tup1=1, 'zhums', [1, 2]
print(tup1, type(tup1))

>>>
(1, 'zhums', [1, 2]) <class 'tuple'>
```

##### 2、使用 tuple() 函数创建元组

```python
tuple(Data)
# Data 表示可以转换为元组的数据，包括字符串、元组、range 对象等。
```

```python
tup1=tuple("Hello")				# 将字符串转换为元组
tup2=tuple(['Python', 'Shell', 'Java'])		# 将列表转换为元组
tup3=tuple({'name':'zhums', 'age':21})		# 将字典转换为元组
tup4=tuple(range(1,5))			# 将区间转换为元组
tup5=tuple()					# 定义空元组
print(tup1, type(tup1))
print(tup2, type(tup2))
print(tup3, type(tup3))
print(tup4, type(tup4))
print(tup5, type(tup5))

>>>
('H', 'e', 'l', 'l', 'o') <class 'tuple'>
('Python', 'Shell', 'Java') <class 'tuple'>
('name', 'age') <class 'tuple'>
(1, 2, 3, 4) <class 'tuple'>
() <class 'tuple'>
```

#### 2、删除元组

通过 `del` 关键字删除元组。

>Python 自带垃圾回收功能，会自动销毁不用的元组，所以一般不需要通过 `del` 来手动删除。

```python
tup1=(1, 2, 3)
del(tup1)
```



#### 3、修改元组

元组是不可变序列，元组中的元素不能被修改，所以只能创建一个新的元组去替代旧的元组。

```python
tup1=(1, 2, 3)
print(tup1)
tup1=(3, 2, 1)
print(tup1)

>>>
(1, 2, 3)
(3, 2, 1)
```

#### 4、元组拆包

创建元组，并将多个数据放到元组中，这个过程被称为元组打包。与元组打包相反的操作是拆包，就是将元组中的元素取出，分别赋值给不同的变量。

```python
s_id, s_name=(101, 'zhums')
print(s_id, s_name)

>>>
101 zhums
# 将元组（101, 'zhums'）拆包到变量 s_id 和 s_name
```

## 3、Bytes

`bytes` 是 `Python 3.x` 新增的类型，在 `Python 2.x` 中是不存在的。

字节串（`bytes`）和字符串（`string`）的对比：

-   字符串由若干个字符组成，以字符为单位进行操作；字节串由若干个字节组成，以字节为单位进行操作。
-   字节串和字符串除了操作的数据单元不同之外，它们支持的所有方法都基本相同。
-   字节串和字符串都是不可变序列，不能随意增加和删除数据。

`bytes` 只负责以字节序列的形式（二进制形式）来存储数据，至于这些数据到底表示什么内容（字符串、数字、图片、音频等），完全由程序的解析方式决定。如果采用合适的字符编码方式（字符集），字节串可以恢复成字符串；反之亦然，字符串也可以转换成字节串。

说白了，`bytes` 只是简单地记录内存中的原始数据，至于如何使用这些数据，`bytes` 并不在意，你想怎么使用就怎么使用，`bytes` 并不约束你的行为。

`bytes` 类型的数据非常适合在互联网上传输，可以用于网络通信编程；`bytes` 也可以用来存储图片、音频、视频等二进制格式的文件。

字符串和 `bytes` 存在着千丝万缕的联系，可以通过字符串来创建 `bytes` 对象，或者说将字符串转换成 `bytes` 对象。以下三种方法可以达到这个目的：

-   如果字符串的内容都是 `ASCII` 字符，那么直接在字符串前面添加 `b` 前缀就可以转换成 `bytes`。
-   `bytes` 是一个类，调用它的构造方法，也就是 `bytes()`，可以将字符串按照指定的字符集转换成 `bytes`；如果不指定字符集，那么默认采用 `UTF-8`。
-   字符串本身有一个 `encode()` 方法，该方法专门用来将字符串按照指定的字符集转换成对应的字节串；如果不指定字符集，那么默认采用 `UTF-8`。

```python
b1 = bytes()		# 通过构造函数创建空 bytes
b2 = b''			# 通过空字符串创建空 bytes
b3 = b'Python'		# 通过 b 前缀将字符串转换成 bytes
b4 = bytes('我用 Python', encoding='UTF-8')	# 为 bytes() 方法指定字符集
b5 = "Python 我用".encode('UTF-8')			# 通过 encode() 方法将字符串转换成 bytes
print('b1: ', type(b1), b1)
print('b2: ', type(b2), b2)
print('b3: ', type(b3), b3)
print('b4: ', type(b4), b4)
print('b5: ', type(b4), b5)

>>>
b1:  <class 'bytes'> b''
b2:  <class 'bytes'> b''
b3:  <class 'bytes'> b'Python'
b4:  <class 'bytes'> b'\xe6\x88\x91\xe7\x94\xa8 Python'
b5:  <class 'bytes'> b'Python \xe6\x88\x91\xe7\x94\xa8'
```

>   从运行结果可以发现，对于非 `ASCII` 字符，`print` 输出的是它的字符编码值（十六进制形式），而不是字符本身。非 `ASCII` 字符一般占用两个字节以上的内存，而 `bytes` 是按照单个字节来处理数据的，所以不能一次处理多个字节。

## 4、字典

`Python` 字典（`dict`）是一种无序的、可变的序列，它的元素以 "键值对（`key-value`）的形式存储。相对地，列表（`list`）和元组（`tuple`）都是有序的序列，它们的元素在底层是连续存储的。

字典的键不能包含重复的元素，值可以。

### 1、定义字典

#### 1、使用 {} 创建字典

由于字典中每个元素都包含两部分，分别是键（`key`）和值（`value`），因此在创建字典时，键和值之间使用冒号 `:` 分隔，相邻元素之间使用逗号 `,` 分隔，所有元素放在大括号 `{ }` 中。

```python
Dict_Name = {'key':'value1', 'key2':'value2', ..., 'keyn':valuen}
```

```python
dict1 = {'数学': 95, '英语': 92, '语文': 84}		# 使用字符串作为 key
dict2 = {(20, 30): 'great', 30: [1,2,3]}		# 使用元组、数字作为 key
dict3 = {}		# 创建空字典
print(dict1)
print(dict2)
print(dict3)

>>>
{'数学': 95, '英语': 92, '语文': 84}
{(20, 30): 'great', 30: [1, 2, 3]}
{}
```

#### 2、通过 formkeys() 方法创建字典

`Python` 中，还可以使用 `dict` 字典类型提供的 `fromkeys()` 方法创建带有默认值的字典，具体格式为：

```python
Dict_Name = dict.fromkeys(List，Default_Value)
```

-   List: 表示字典中所有键的列表
-   Default_Value: 表示默认值，默认为空值 `None`

```python
dict1 = dict.fromkeys(['语文', '数学', '英语'], 60)
dict2 = dict.fromkeys(['语文', '数学', '英语'])
print(dict1)
print(dict2)

>>>
{'语文': 60, '数学': 60, '英语': 60}
{'语文': None, '数学': None, '英语': None}
```

#### 3、使用 dict() 函数创建字典

```python
Var_Name = dict(key1=value1, key2=value2...)


# Demo
Info = dict(name='zhums', age=21)
print(Info)

>>>
{'name': 'zhums', 'age': 21}
```

```python
Var_Name = [('key1', value1), ('key2', value2), ('key3', value3)]
Var_Name = [['key1', value1], ['key2', value2], ['key3', value3]]
Var_Name = (('key1', value1), ('key2', value2), ('key3', value3))
Var_Name = (['key1', value1], ['key2', value2], ['key3', value3])
Dict_Name = dict(Var_Name)


# Demo
demo1 = [('two',2), ('one',1), ('three',3)]
demo2 = [['two',2], ['one',1], ['three',3]]
demo3 = (('two',2), ('one',1), ('three',3))
demo4 = (['two',2], ['one',1], ['three',3])
dict1=dict(demo1)
dict2=dict(demo2)
dict3=dict(demo3)
dict4=dict(demo4)
print(dict1)
print(dict2)
print(dict3)
print(dict4)

>>>
{'two': 2, 'one': 1, 'three': 3}
{'two': 2, 'one': 1, 'three': 3}
{'two': 2, 'one': 1, 'three': 3}
{'two': 2, 'one': 1, 'three': 3}
```

```python
keys = ['key1', 'key2', 'key3']		# 也可以是字符串或元组
values = [value1, value2, value3]	# 也可以是字符串或元组
dict1 = dict( zip(keys, values) )


# Demo
keys = ['one', 'two', 'three']
values = [1, 2, 3]
dict1 = dict( zip(keys, values) )
print(dict1)

>>>
{'one': 1, 'two': 2, 'three': 3}
```

```python
Var_Name = dict()

# Demo
dict1 = dict()		# 创建空字典
print(dict1)

>>>
{}
```

### 2、访问字典

序列类型的数据是通过下标来访问元素的，而字典不同，它通过键来访问对应的值。因为字典中的元素是无序的，每个元素的位置都不固定，所以字典也不能像列表和元组那样，采用切片的方式一次性访问多个元素。

**Python 访问字典元素的具体格式为：**

```python
Dict_Name[Key]
```

-   Dict_Name: 表示字典变量的名字
-   Key: 表示键名。注意，键必须是存在的，否则会抛出异常

```python
tup = (['two',26], ['one',88])
dic = dict(tup)
print(dic['one'])  #键存在

>>>
88
```

除了上面这种方式外，Python 更推荐使用 `dict` 类型提供的 `get()` 方法来获取指定键对应的值。当指定的键不存在时，`get()` 方法不会抛出异常。

```python
# get() 方法的语法:
DictName.get(Key[,Default])
```

-   DictName: 表示字典变量的名字；
-   Key: 表示指定的键；
-   Default: 用于指定要查询的键不存在时，此方法返回的默认值，默认 `None`。

```python
a = dict(two=0.65, one=88, three=100, four=-59)
print( a.get('one') )
print( a.get('name') )
print( a.get('name','Key is not exists !') )

>>>
88
None
Key is not exists !
```

### 3、删除字典

和删除列表、元组一样，手动删除字典也可以使用 `del` 关键字，例如：

```python
dict1 = {'name':'zhums', 'age':21}
del dict1
```

>   Python 自带垃圾回收功能，会自动销毁不用的字典，所以一般不需要通过 `del` 来手动删除。

### 4、字典元素基本操作

#### 1、添加元素

为字典添加新的元素，直接给不存在的 `key` 赋值即可，格式如下:

```python
DictName[Key]=Value
```

-   DictName: 字典名称
-   Key: 要添加的键
-   Value: 要添加的键的值，是 Python 支持的数据类型即可

```python
dict1={'name': 'zhums', 'age': 21}
dict1['sex']='man'
print(dict1)

>>>
{'name': 'zhums', 'age': 21, 'sex': 'man'}
```

#### 2、修改元素

字典数据中只能够修改其键的值。

```python
dict1={'name': 'zhums', 'age': 21}
dict1['name']='wuyi'
print(dict1)

>>>
{'name': 'wuyi', 'age': 21}
```

#### 3、删除元素

删除字典中的元素使用 `del` 关键字。

```python
dict1={'name': 'zhums', 'age': 21}
del dict1['age']
print(dict1)

>>>
{'name': 'wuyi'}
```

#### 4、判断元素

判断字典中是否存在指定键值对，首先应判断字典中是否有对应的键。判断字典是否包含指定键值对的键，可以使用 `in` 或 `not in` 运算符。

>   注意: 对于 `dict` 而言，`in` 或 `not in` 运算符都是基于 `key` 来判断的。

```python
dict1={'name': 'zhums', 'age': 21}
print( 'name' in dict1)
print( 'sex' in dict1)

>>>
True
False
```

### 5、字典常用方法

#### keys()、values()、items()

| 方法     | 作用               |
| -------- | ------------------ |
| keys()   |                    |
| values() | 返回字典中所有值   |
| items()  | 返回字典中所有键值 |

```python
dict1={'name': 'zhums', 'age': 21}
print(dict1.keys())
print(dict1.values())
print(dict1.items())

>>>
dict_keys(['name', 'age'])
dict_values(['zhums', 21])
dict_items([('name', 'zhums'), ('age', 21)])
```

#### copy()

`copy()` 方法返回一个字典的拷贝，也即返回一个具有相同键值对的新字典。

```python
a = {'one': 1, 'two': 2, 'three': [1,2,3]}
b = a.copy()
print(b)

>>>
{'one': 1, 'two': 2, 'three': [1, 2, 3]}
```

>   注意: `copy()` 方法所遵循的拷贝原理，既有深拷贝，也有浅拷贝。拿拷贝字典 `a` 为例，`copy()` 方法只会对最表层的键值对进行深拷贝，也就是说，它会再申请一块内存用来存放 `{'one': 1, 'two': 2, 'three': []}`；而对于某些列表类型的值来说，此方法对其做的是浅拷贝，也就是说，`b` 中的 `[1,2,3]` 的值不是自己独有，而是和 `a` 共有。

```python
a = {'one': 1, 'two': 2, 'three': [1,2,3]}
b = a.copy()
a['four']=100	# 向 a 中添加新键值对，由于 b 已经提前将 a 所有键值对都深拷贝过来，因此 a 添加新键值对，不会影响 b。
print(a)
print(b)
a['three'].remove(1)	# 由于 b 和 a 共享 [1,2,3]（浅拷贝），因此移除 a 中列表中的元素，也会影响 b。
print(a)
print(b)

>>>
{'one': 1, 'two': 2, 'three': [1, 2, 3], 'four': 100}
{'one': 1, 'two': 2, 'three': [1, 2, 3]}
{'one': 1, 'two': 2, 'three': [2, 3], 'four': 100}
{'one': 1, 'two': 2, 'three': [2, 3]}
```

#### update()

`update()` 方法可以使用一个字典所包含的键值对来更新己有的字典。

在执行 `update()` 方法时，如果被更新的字典中己包含对应的键值对，那么原 `value` 会被覆盖；如果被更新的字典中不包含对应的键值对，则该键值对被添加进去。

```python
a = {'one': 1, 'two': 2, 'three': 3}
a.update({'one':4.5, 'four': 9.3})
print(a)

>>>
{'one': 4.5, 'two': 2, 'three': 3, 'four': 9.3}
```

>   由于被更新的字典中已包含 `key` 为 `one` 的键值对，因此更新时该键值对的 `value` 将被覆盖；而被更新的字典中不包含 `key` 为 `four` 的键值对，所以更新时会为原字典增加一个新的键值对。

#### pop() 和 popitem()

`pop()` 方法用于删除指定的键值对。语法如下:

```python
DictName.pop(Key)
```

-   DictName: 字典名称
-   Key: 要删除的键

`popitem()` 方法用于随机删除一个键值对。语法如下:

```python
DictName.popitem()
```

```python
a = {'数学': 95, '语文': 89, '英语': 90, '化学': 83, '物理': 89}
print(a)
a.pop('化学')
print(a)
a.popitem()
print(a)

>>>
{'数学': 95, '语文': 89, '英语': 90, '化学': 83, '物理': 89}
{'数学': 95, '语文': 89, '英语': 90, '物理': 89}
{'数学': 95, '语文': 89, '英语': 90}
```

>   其实，说 `popitem()` 随机删除字典中的一个键值对是不准确的，虽然字典是一种无须的列表，但键值对在底层也是有存储顺序的，`popitem()` 总是弹出底层中的最后一个 `key-value`，这和列表的 `pop()` 方法类似，都实现了数据结构中 "出栈" 的操作。

#### setdefault()

`setdefault()` 方法用来返回某个 `key` 对应的 `value`，其语法格式如下：

```
DictName.setdefault(Key, Default_Value)
```

-   DictName: 字典名称
-   Key: 键
-   Default_Value: 默认值，默认 `None`

当指定的 `key` 不存在时，`setdefault()` 会先为这个不存在的 `key` 设置一个默认的 `Default_Value`，然后再返回 `Default_Value`。也就是说，`setdefault()` 方法总能返回指定 `key` 对应的 `value`：

-   如果该 `key` 存在，那么直接返回该 `key` 对应的 `value`；
-   如果该 `key` 不存在，那么先为该 `key` 设置默认的 `Default_Value`，然后再返回该 `key` 对应的 `Default_Value`。

```python
a = {'数学': 95, '语文': 89, '英语': 90}
print(a)
a.setdefault('物理', 94)	# key 不存在，指定默认值
print(a)
a.setdefault('化学')		# key 不存在，不指定默认值
print(a)
a.setdefault('数学', 100)	# key 存在，指定默认值
print(a)

>>>
{'数学': 95, '语文': 89, '英语': 90}
{'数学': 95, '语文': 89, '英语': 90, '物理': 94}
{'数学': 95, '语文': 89, '英语': 90, '物理': 94, '化学': None}
{'数学': 95, '语文': 89, '英语': 90, '物理': 94, '化学': None}
```

## 5、集合

`Python` 中的集合，和数学中的集合概念一样，用来保存不重复的元素，即集合中的元素都是唯一的，互不相同。

从形式上看，和字典类似，`Python` 集合会将所有元素放在一对大括号 `{}` 中，相邻元素之间用 `","` 分隔，如下所示：

```python
{element1,element2,...,elementn}
```

其中，`elementn` 表示集合中的元素，个数没有限制。

从内容上看，同一集合中，只能存储不可变的数据类型，包括整形、浮点型、字符串、元组，无法存储列表、字典、集合这些可变的数据类型，否则 `Python` 解释器会抛出 `TypeError` 错误。如下：

```python

```

### 1、创建集合

#### 1、使用 {} 创建

```python
Set_Name={element1, element2, ..., elementn}
```

```python
set1={1, 1.1, 'one', ('zhums',)}
print(type(set1), set1)

>>>
<class 'set'> {1, 'one', 1.1, ('zhums',)}
```

#### 2、使用 set() 函数创建

`set()` 函数为 `Python` 的内置函数，其功能是将字符串、列表、元组、`range` 对象等可迭代对象转换成集合，语法格式如下：

```python
SetName = set(Iteration)
```

-   Iteration: 表示字符串、列表、元组、`range` 对象等数据。

```python
set1 = set("hello")
set2 = set([1,2,3,4,5])
set3 = set((1,2,3,4,5))
set4 = set(range(1, 6))
print("set1:", set1)
print("set2:", set2)
print("set3:", set3)
print("set4:", set4)

>>>
set1: {'e', 'o', 'h', 'l'}
set2: {1, 2, 3, 4, 5}
set3: {1, 2, 3, 4, 5}
set4: {1, 2, 3, 4, 5}
```

>注意: 如果要创建空集合，只能使用 `set()` 函数实现。因为直接使用一对 `{}`，`Python` 解释器会将其视为一个空字典。

### 2、访问集合

由于集合中的元素是无序的，因此无法向列表那样使用下标访问元素。`Python` 中，访问集合元素最常用的方法是使用循环结构，将集合中的数据逐一读取出来。

```python
set1={1, 1.1, 'one', ('zhums',)}
for i in set1:
    print(i, end=' ')

>>>
one ('zhums',) 1.1 1 
```

### 3、删除集合

使用 `del()` 关键字删除集合。

```python
set1={1, 1.1, 'one', ('zhums',)}
del(set1)
```

### 4、集合元素基本操作

#### 1、添加元素

使用 `add()` 方法在集合中添加元素，添加的元素只能为 "数字、字符串、元组、布尔类型"，不能添加 "列表、字典、集合"这类可变数据。语法格式如下:

```python
SetName.add(element)
```

```python
set1={1, 'one'}
print(set1)
set1.add(2)
print(set1)

>>>
{1, 'one'}
{1, 2, 'one'}
```

#### 2、删除元素

1、使用 `remove()` 方法删除集合中的指定元素。语法格式如下:

```python
SetName.remove(element)
```

>   注意: 若要删除的元素不在集合中，则会抛出 `KeyError` 错误。

```python
set1={1, 'one'}
print(set1)
set1.remove(1)
print(set1)

>>>
{'one', 1}
{'one'}
```

2、使用 `discard()` 方法删除集合中的指定元素，该方法与 `remove()` 的区别在于当删除元素失败时，不会抛出错误。

```python
set1={1, 'one'}
print(set1)
set1.discard(2)
print(set1)

>>>
{1, 'one'}
{1, 'one'}
```

#### 3、交集、并集、差集运算

```python
set1={1,2,3}
set2={3,4,5}
```

| 运算符操作 | 运算符 | 说明                                    | 例子                          |
| ---------- | ------ | --------------------------------------- | ----------------------------- |
| 交集       | &      | 取两集合公共的元素                      | set1 & set2 <br />{3}         |
| 并集       | \|     | 取两集合全部的元素                      | set1 \| set2<br />{1,2,3,4,5} |
| 差集       | -      | 取一个集合中另一个集合没有的元素        | set1 - set2<br />{1,2}        |
| 对称差集   | ^      | 取集合 `A` 和 `B` 中不属于 `A&B` 的元素 | set1 ^ set2<br />{1,2,4,5}    |

### 5、集合常用方法

| 方法                          | 语法                                   | 说明                                                         |
| ----------------------------- | -------------------------------------- | ------------------------------------------------------------ |
| add()                         | set1.add()                             | 向 set1 集合中添加元素                                       |
| clear()                       | set1.clear()                           | 清空 set1 集合中的元素                                       |
| copy()                        | set2=set1.copy()                       | 拷贝 set1 集合中的元素给 set2                                |
| difference()                  | set3 = set1.difference(set2)           | 将 set1 集合中有而 set2 没有的元素给 set3                    |
| difference_update()           | set1.difference_update(set2)           | 从 set1 中删除与 set2 相同的元素                             |
| discard()                     | set1.discard(elem)                     | 删除 set1 中的 elem 元素                                     |
| intersection()                | set3 = set1.intersection(set2)         | 取 set1 和 set2 的交集给 set3                                |
| intersection_update()         | set1.intersection_update(set2)         | 取 set1 和 set2 的交集，并更新给 set1                        |
| isdisjoint()                  | set1.isdisjoint(set2)                  | 判断 set1 和 set2 是否没有交集，有交集返回 False；没有交集返回 True |
| issubset()                    | set1.issubset(set2)                    | 判断 set1 是否是 set2 的子集                                 |
| issuperset()                  | set1.issuperset(set2)                  | 判断 set2 是否是 set1 的子集                                 |
| pop()                         | a = set1.pop()                         | 取 set1 中一个元素，并赋值给 a                               |
| remove()                      | set1.remove(elem)                      | 移除 set1 中的 elem 元素                                     |
| symmetric_difference()        | set3 = set1.symmetric_difference(set2) | 取 set1 和 set2 中互不相同的元素，给 set3                    |
| symmetric_difference_update() | set1.symmetric_difference_update(set2) | 取 set1 和 set2 中互不相同的元素，并更新给 set1              |
| union()                       | set3 = set1.union(set2)                | 取 set1 和 set2 的并集，赋给 set3                            |
| update()                      | set1.update(elem)                      | 添加列表或集合中的元素到 set1                                |

```python
2+2i + 2   4+2i
2+2i + 2i  2+4i
2+2i + 2.2i  2+4.2i
2+2i * 2   4+4i
2+2i * 2i  4i-4
2+2i * 3i  6i-6
2+2i / 2   1+1i
2+2i / 2i  
```

```python
8+8i
8i+8

2 * 2+2j

4-4j
```

```python
4+4j
-4+4j
```

# 