## random --- 生成伪随机数

[random --- 生成伪随机数 — Python 3.12.0 文档](https://docs.python.org/zh-cn/3/library/random.html)

### 整数用函数

#### random.randrange()

```python
random.randrange([start, ]stop[, step])
```

-   `start`：开始，默认为 `0`
-   `stop`：结束，但不包括 `stop`
-   `step`：步长，默认为 `1`

返回从 `range(start, stop, step)` 随机选择的一个元素。

>   关键字参数不应被使用因为它们可能以预料之外的方式被解读。 例如`randrange(start=100)`会被解读为`randrange(0, 100, 1)`。

>   在`3.12`版更改: 不再支持非整数类型的自动转换。`randrange(10.0)`和`randrange(Fraction(10, 1))`之类的调用现在将会引发`TypeError`。

```python
>>> import random
>>> random.randrange(2, 6, 2) 
2
>>> random.randrange(2, 6, 2)
2
>>> random.randrange(2, 6, 2)
4
```

#### random.randint(a, b)

返回随机整数 `N` 满足 `a <= N <= b`。相当于 `randrange(a, b+1)`。

```python
>>> import random
>>> random.randint(1, 3)
2
>>> random.randint(1, 3)
1
>>> random.randint(1, 3)
3
```

### 序列用函数

#### random.choice(seq)

从非空序列 `seq` 返回一个随机元素。 如果 `seq` 为空，则引发 `IndexError`。

```python
>>> import random
>>> str1 = 'zhums'      
>>> random.choice(str1)
'h'
>>> random.choice(str1)
'm'
```

## datetime --- 基本日期和时间类型

[datetime --- 基本日期和时间类型 — Python 3.12.1 文档](https://docs.python.org/zh-cn/3/library/datetime.html)

```python
>>> print(datetime.datetime.now())
2023-12-18 13:29:18.015196
>>> print(datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S"))
2023-12-18 13:29:56
```



## time --- 时间的访问和转换

[time --- 时间的访问和转换 — Python 3.12.1 文档](https://docs.python.org/zh-cn/3/library/time.html)

### time.time()

返回以浮点数表示的从 `epoch` 开始的秒数形式的时间。`epoch` 是起始的时间点，即 `time.gmtime(0)` 的返回值。 这在所有平台上都是 `1970-01-01, 00:00:00 (UTC)`。

```python
import time

startTime = time.time()

for i in range(1, 100000):
    print(i)

endTime = time.time()
print("代码执行时间：", endTime - startTime)
```



## os --- 多种操作系统接口

### os.uname()

```python
os.uname()
```

返回当前操作系统的识别信息。返回值是一个有 5 个属性的对象：

-   sysname - 操作系统名

-   nodename - 机器在网络上的名称（需要先设定）

-   release - 操作系统发行信息

-   version - 操作系统版本信息

-   machine - 硬件标识符


为了向后兼容，该对象也是可迭代的按照 sysname，nodename，release，version，和 machine 顺序组成的元组。

```python
>>> import os
>>> os.uname()
posix.uname_result(sysname='Linux', nodename='prod', release='3.10.0-1160.99.1.el7.x86_64', version='#1 SMP Wed Sep 13 14:19:20 UTC 2023', machine='x86_64')
```

### os.rename()

```python
os.rename(src, dst, *, src_dir_fd=None, dst_dir_fd=None)
```

将文件或目录 src 重命名为 dst。如果 dst 已存在，则下列情况下将会操作失败，并抛出 OSError 的子类：

```python
>>> import os
>>> os.listdir()
['algowarehouse_version_build_all_V3R1C08_202312221700.tar.gz', '.bash_history', '.conda', '.vim', '.ssh', '.lesshst', '.bashrc', '.vimrc', '.profile', 'b.log', '.viminfo', '.cache', '.wget-hsts', '.config']
>>> src = '/root/b.log'
>>> dst = '/root/c.log'
>>> os.rename(src, dst)
>>> os.listdir()
['algowarehouse_version_build_all_V3R1C08_202312221700.tar.gz', '.bash_history', '.conda', '.vim', '.ssh', '.lesshst', '.bashrc', '.vimrc', '.profile', 'c.log', '.viminfo', '.cache', '.wget-hsts', '.config']
```

### os.remove()

```python
os.remove(path, *, dir_fd=None)
```

删除文件 path。 如果 path 是目录，则会引发 OSError。 请使用 rmdir() 来移除目录。 如果文件不存在，则会引发 FileNotFoundError。

```python
os.remove('/root/a.txt')
```

### os.stat()

```python
os.stat(path, *, dir_fd=None, follow_symlinks=True)
```

获取文件或文件描述符的状态。在所给路径上执行等效于 `stat()` 系统调用的操作。`path` 可以是字符串类型，或（直接传入或通过 PathLike 接口间接传入的） bytes 类型，或打开的文件描述符。返回一个 [stat_result](https://docs.python.org/zh-cn/3/library/os.html#os.stat_result) 对象。

本函数默认会跟踪符号链接，要获取符号链接本身的 `stat`，请添加 `follow_symlinks=False` 参数，或使用 `lstat()`。

```python
>>> import os
>>> os.stat('chrony.conf')
os.stat_result(st_mode=33188, st_ino=1181891, st_dev=64769, st_nlink=1, st_uid=0, st_gid=0, st_size=1861, st_atime=1699640546, st_mtime=1697686921, st_ctime=1697686921)
>>> os.stat('chrony.conf', follow_symlinks=False)
os.stat_result(st_mode=41471, st_ino=1180748, st_dev=64769, st_nlink=1, st_uid=0, st_gid=0, st_size=16, st_atime=1703837789, st_mtime=1703837787, st_ctime=1703837787)
```

### os.chmod()

```python
os.chmod(path, mode, *, dir_fd=None, follow_symlinks=True)
```

将 path 的 mode 更改为其他由数字（八进制数，前缀为 `0o`）表示的 mode。

```python
os.chmod('a.txt', 0o777)		# rwxrwxrwx
os.chmod('a.txt', 0o754)		# rwxr-xr--
os.chmod('a.txt', 0o644)		# rw-r--r--
```

### **os.getcwd()**

```python
os.getcwd()
```

返回表示当前工作目录的字符串。

```python
>>> os.getcwd()
'/usr/lib64/python3.6'
```

### **os.chdir()**

```python
os.chdir(path)
```

将当前工作目录更改为 path。

```python
>>> os.getcwd()
'/usr/lib64/python3.6'
>>> os.chdir('/root')
>>> os.getcwd()
'/root'
```

### **os.mkdir()**

```python
os.mkdir(path, mode=0o777, *, dir_fd=None)
```

创建一个名为 `path` 的目录，应用以数字表示的权限模式 `mode`

如果目录已存在，[`FileExistsError`](https://docs.python.org/zh-cn/3/library/exceptions.html#FileExistsError)会被提出。如果路径中的父目录不存在，则会引发[`FileNotFoundError`](https://docs.python.org/zh-cn/3/library/exceptions.html#FileNotFoundError) 。

某些系统会忽略 *mode*。如果没有忽略它，那么将首先从它中减去当前的 umask 值。如果除最后 9 位（即 *mode* 八进制的最后 3 位）之外，还设置了其他位，则其他位的含义取决于各个平台。在某些平台上，它们会被忽略，应显式调用 [`chmod()`](https://docs.python.org/zh-cn/3/library/os.html#os.chmod) 进行设置。

```python
os.mkdir('ccc', 0o777)

[root@prod zhums]# umask 
0022
[root@prod zhums]# ll -d ccc
drwxr-xr-x 2 root root 4.0K Dec 29 17:40 ccc
```

### os.makedirs()

```python
os.makedirs(name, mode=0o777, exist_ok=False)
```

递归创建目录。如果 `exist_ok` 为 `False` (默认值)，则如果目标目录已存在将会引发 [`FileExistsError`](https://docs.python.org/zh-cn/3/library/exceptions.html#FileExistsError)。

```python
os.makedirs('a/b/c')
```

### **os.listdir()**

```python
os.listdir(path='.')
```

返回一个包含由 path 目录中条目名称组成的列表。该列表按任意顺序排列，并且不包括特殊条目 '.' 和 '..'。

```python
>>> os.chdir('/')
>>> os.listdir()
['.autorelabel', 'data', 'mnt', 'home', 'bin', 'root', 'tmp', 'usr', 'media', 'lib64', 'lib', 'dev', 'var', 'etc', 'run', 'opt', 'proc', 'sbin', 'boot', 'srv', 'lost+found', 'sys']
>>> os.listdir('/home')
[]
```





### os.path.join()

```python
os.path.join(path, *paths)
```

合并一个或多个路径部分。 返回值将是 `path` 和所有 `*paths` 成员的拼接，其中每个非空部分后面都紧跟一个目录分隔符，最后一个除外。

```python
>>> import os
>>> a = '/root'
>>> b = ''
>>> c = 'a.sh'
>>> os.path.join(a, b)
'/root/'
>>> b = 'scripts'
>>> os.path.join(a, b)
'/root/scripts'
>>> os.path.join(a, b, c)
'/root/scripts/a.sh'
```



## json --- JSON 编码和解码器

**json.dumps(obj, *, skipkeys=False, ensure_ascii=True, check_circular=True, allow_nan=True, cls=None, indent=None, separators=None, default=None, sort_keys=False, \*\*kw)**

将 obj 序列化为 JSON 格式的 str。

```python
>>> data = {"name": "小明", "height": "170", "age": "18"}
>>> new_data = json.dumps(data)
>>> type(data)
<class 'dict'>
>>> type(new_data)
<class 'str'>	
>>> print(json.dumps({'name': 'zhums', 'age': 21, 'hobby': ['LOL', 'CSGO']}, indent=4))
{
    "name": "zhums",
    "age": 21,
    "hobby": [
        "LOL",
        "CSGO"
    ]
}
```

**json.loads(s, *, cls=None, object_hook=None, parse_float=None, parse_int=None, parse_constant=None, object_pairs_hook=None, \*\*kw)**

将 `s`(一个包含 JSON 的 str, bytes 或 bytearray 实例) 反序列化为 Python 对象。 

如果反序列化的数据不是有效 JSON ，引发 `JSONDecodeError` 错误。

```python
>>> import json
>>> data = '''
... {
...     "name": "小明",
...     "height": "170",
...     "age": "18"
... }
... '''
>>> new_data = json.loads(data)
>>> type(data)
<class 'str'>
>>> type(new_data)
<class 'dict'>
```

## csv --- CSV 文件读写

**csv.reader(csvfile, dialect='excel', \*\*fmtparams)**

返回一个 `reader` 对象。

```python
import csv
with open("file.csv", "r") as f:
    spamreader = csv.reader(f)
    for line in spamreader:
        print(line)

>>>
['0', '31']
```

**csv.writer(csvfile, dialect='excel', \*\*fmtparams)**

返回一个 [writer](#writer 对象) 对象。

```python
import csv
with open('demo.csv', 'w', newline='') as csvfile:
    spamwriter = csv.writer(csvfile)
```

**class csv.Dialect**

`Dialect` 类是一个容器类，其属性包含有如何处理双引号、空白符、分隔符等的信息。 所有可用的 `Dialect` 名称由 `list_dialects()` 返回。

```python
import csv
with open('students.csv', 'w', newline='') as csvfile:
    writer = csv.writer(csvfile, dialect='excel')
```

**csvwriter.writerow(row)**

将 `row` 形参写入到 `writer` 的文件对象，根据当前 `Dialect` 进行格式化。 返回对下层文件对象的 `write` 方法的调用的返回值。

```python
import csv
with open("file.csv", "a", newline="") as f:
    csv_writer = csv.writer(f)
    data = [0, 31]
    csv_writer.writerow(data)
with open("file.csv", "r") as f:
    for line in csv.reader(f):
        print(line)
        
>>>
['0', '31']
```

**csvwriter.writerows(rows)**

将 `rows*`（即能迭代出多个上述 `*row` 对象的迭代器）中的所有元素写入 `writer` 的文件对象，并根据当前设置的变种进行格式化。

```python
import csv
with open("file.csv", "a", newline="") as f:
    csv_writer = csv.writer(f)
    data = [[0, 31], [1, 30], [2, 32]]
    csv_writer.writerows(data)
with open("file.csv", "r") as f:
    for line in csv.reader(f):
        print(line)
        
>>>
['0', '31']
['1', '30']
['2', '32']
```

## re --- 正则表达式操作

[re --- 正则表达式操作 — Python 3.12.1 文档](https://docs.python.org/zh-cn/3/library/re.html#module-re)

### 正则表达式语法

#### 字符匹配

| 字符 | 功能                                                         |
| ---- | ------------------------------------------------------------ |
| .    | 默认匹配除换行符外的任意单个字符                             |
| []   | 匹配 [] 中列举的字符；[abc]/\[^abc]/[a-z]/[0-9]/[0-9a-zA-Z]  |
| \d   | 对于 Unicode (str) 样式：<br/>  匹配任何 Unicode 十进制数（Unicode 字符目录 [Nd] 里的字符）。包括 [0-9] 和很多其他的数字字符。如果设置了 ASCII 标志，只匹配 [0-9] 。<br/>对于8位(bytes)样式：<br/>  匹配任何十进制数，就是 [0-9]。 |
| \D   | 匹配任何非十进制数字的字符。就是 \d 取反。 如果设置了 ASCII 标志，就相当于 \[^0-9] 。 |
| \s   | 对于 Unicode (str) 样式：<br/>  匹配任何 Unicode 空白字符（包括 [ \t\n\r\f\v] ，还有很多其他字符，比如不同语言排版规则约定的不换行空格）。如果 ASCII 被设置，就只匹配 [ \t\n\r\f\v] 。<br/>对于8位(bytes)样式：<br/>  匹配 ASCII 中的空白字符，就是 [ \t\n\r\f\v] 。 |
| \S   | 匹配任何非空白字符。就是 \s 取反。如果设置了 ASCII 标志，就相当于 \[^ \t\n\r\f\v] 。 |
| \w   | 对于 Unicode (str) 样式：<br/>  匹配 Unicode 单词类字符；包括字母数字字符 (如 str.isalnum() 所定义的) 以及下划线 (\_)。 如果使用了 ASCII 旗标，则将只匹配 [a-zA-Z0-9_]。<br/>对于8位(bytes)样式：<br/>  匹配 ASCII 字符中的数字和字母和下划线，就是 [a-zA-Z0-9_] 。如果设置了 LOCALE 标记，就匹配当前语言区域的数字和字母和下划线。 |
| \W   | 匹配非单词字符的字符。这与 \w 正相反。如果使用了 ASCII 旗标，这就等价于 \[^a-zA-Z0-9_]。如果使用了 LOCALE 旗标，则会匹配当前区域中既非字母数字也非下划线的字符。 |
|      |                                                              |

#### 匹配次数

| 字符   | 功能                                                         |
| ------ | ------------------------------------------------------------ |
| *      | 匹配前一个字符 0 次或任意次                                  |
| +      | 匹配前一个字符 1 次或任意次                                  |
| ?      | 匹配前一个字符 0 次或 1 次                                   |
| {m}    | 匹配前一个字符 m 次                                          |
| {m, n} | 匹配前一个字符 m 到 n 次。忽略 m 则下限为 0 次，忽略 n 上限为无限次。逗号不能省略。 |

#### 位置锚定

| 字符 | 功能                                                         |
| ---- | ------------------------------------------------------------ |
| ^    | 匹配字符串的开头，并且在 MULTILINE 模式下也匹配换行后的首个符号。 |
| $    | 匹配字符串的结尾或者在字符串结尾换行符的前一个字符，在 MULTILINE 模式下也会匹配换行符之前的文本。 |

#### 分组

| 字符           | 功能                                                         |
| -------------- | ------------------------------------------------------------ |
| \|             | 匹配左右任意表达式。                                         |
| (...)          | 匹配括号内的任意正则表达式，并标识出组合的开始和结尾。匹配完成后，组合的内容可以在使用 \number 进行引用。 |
| \number        | 引用分组 number 匹配到的字符串。                             |
| (?P\<name>...) | 分组定义别名，匹配到的字符串组通过定义的 name 引用。         |
| (?P=name)      | 引用别名为 name 分组匹配到的字符串                           |
|                |                                                              |

-   \number 示例

```python
import re

ret1 = re.match(r"<(.*)>.*</\1>", "<h1>MySite</h1>")
ret2 = re.match(r"<(.*)><(.*)>.*</\2></\1>", "<html><h1>www.itcast.cn</h1></html>")

print(ret1.group())
print(ret2.group())

>>>
<h1>MySite</h1>
<html><h1>www.itcast.cn</h1></html>
```

-   (?P\<name>) 和 (?P=name) 示例

```python
import re

ret1 = re.match(r"<(?P<name1>.*)><(?P<name2>.*)>.*</(?P=name2)></(?P=name1)>","<html><h1>MySite</h1></html>")
print(ret1.group('name1'))
print(ret1.group())

>>>
html
<html><h1>MySite</h1></html>
```

### 模块内容

#### 标志

##### re.A | re.ASCII

使 \w, \W, \b, \B, \d, \D, \s 和 \S 只匹配 ASCII，而不是 Unicode。只对 Unicode 样式有效，会被 byte 样式忽略。

##### re.I | re.IGNORECASE

忽略大小写匹配。

##### re.M | re.MULTILINE

多行模式

设置以后，样式字符 '^' 匹配字符串的开始，和每一行的开始（换行符后面紧跟的符号）；样式字符 '\$' 匹配字符串尾，和每一行的结尾（换行符前面那个符号）。默认情况下，'^' 匹配字符串头，'$' 匹配字符串尾。

##### re.S | re.DOTALL

让 '.' 特殊字符匹配任何字符，包括换行符；如果没有这个标记，'.' 匹配除换行符外的其它任意字符。



#### 函数

##### re.findall()

`re.findall(pattern, string, flags=0)`

返回 pattern 在 string 中的所有非重叠匹配，以字符串列表或字符串元组列表的形式。对 string 的扫描从左至右，匹配结果按照找到的顺序返回。 空匹配也包括在结果中。

返回结果取决于模式中捕获组的数量。如果没有组，返回与整个模式匹配的字符串列表。如果有且仅有一个组，返回与该组匹配的字符串列表。如果有多个组，返回与这些组匹配的字符串元组列表。非捕获组不影响结果。

```python
>>> re.findall(r'\bf[a-z]*', 'which foot or hand fell fastest')
['foot', 'fell', 'fastest']
>>> re.findall(r'(\w+)=(\d+)', 'set width=20 and height=10')
[('width', '20'), ('height', '10')]
```

##### re.finditer()

`re.finditer(pattern, string, flags=0)`

针对正则表达式 pattern 在 string 里的所有非重叠匹配返回一个产生 Match 对象的 iterator。 string 将被从左至右地扫描，并且匹配也将按被找到的顺序返回。 空匹配也会被包括在结果中。

```python
import re

result = re.finditer(r'\d+', '123abc456def')
for i in result:
    print(i.group())
```

```python
# 运行结果
123
456
```

##### re.sub()

`re.sub(pattern, repl, string, count=0, flags=0)`

返回通过使用 repl 替换在 string 中通过 pattern 匹配的数据。

-   count: 指定要替换的最大次数；必须是非负整数。默认为 0 表示所有的匹配都会被替换。

```python
import re

result = re.sub(r'\d+', 'AAA', '123abc456def', count=1)
print(result)
```

```python
# 运行结果

AAAabc456def
```

##### re.subn()

`re.subn(pattern, repl, string, count=0, flags=0)`

与 [sub()](#re.sub())相同，但是返回一个元组 `(string, count)`

```python
import re

result = re.subn(r'\d+', 'AAA', '123abc456def')
print(result)
```

```python
# 运行结果
('AAAabcAAAdef', 2)
```

##### re.split()

`re.split(pattern, string, maxsplit=0, flags=0)`

将 pattern 作为分隔符分割 string。若 pattern 中匹配到括号，那么所有的组里的文字也会包含在列表里。如果 maxsplit 非零， 最多进行 maxsplit 次分隔， 剩下的字符全部返回到列表的最后一个元素。

```python
import re

result = re.split(r'\d', 'abc1def2ghi', maxsplit=1)
print(result)
```

```python
# 运行结果
['abc', 'def2ghi']
```

如果分隔符里有捕获组合，并且匹配到字符串的开始，那么结果将会在开头和结尾加上一个空字符串。这样的话，分隔组将会出现在结果列表中同样的位置。

```python
import re

result = re.split(r'(\W+)', '...Hello World...')
print(result)
```

```python
# 运行结果
['', '...', 'Hello', ' ', 'World', '...', '']
```

##### re.purge()

清除正则表达式的缓存。

## logging --- Python 的日志记录工具
