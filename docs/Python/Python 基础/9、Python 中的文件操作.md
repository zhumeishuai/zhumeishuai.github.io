## 1、Python 中的文件路径

关于文件，它有两个关键属性，分别是 "文件名" 和 "路径"。其中，文件名指的是为每个文件设定的名称，而路径则用来指明文件在计算机上的位置。

-   在 `Windows` 中，根文件夹名为 `D:\`，路径使用反斜杠 `\` 作为路径分隔符。
-   在 `Linux` 中，根文件夹是 `/`，路径使用正斜杠 `/` 作为路径分隔符。

使用 `os.path.join()` 函数创建带有文件名称的文件存储路径：

```python
import os
My_Files = ['zhums.txt', 'wuyi.txt']
for FileName in My_Files:
    print(os.path.join('D:\study', FileName))
```

运行结果为：

```python
D:\study\zhums.txt
D:\study\wuyi.txt
```

## 2、Python 中的绝对/相对路径

### 1、当前工作目录

每个运行在计算机上的程序，都有一个 "当前工作目录"（或 `cwd`）。所有没有从根文件夹开始的文件名或路径，都假定在当前工作目录下。

>   注意，虽然文件夹是目录的更新的名称，但当前工作目录（或当前目录）是标准术语，没有当前工作文件夹这种说法。

在 `Python` 中，利用 `os.getcwd()` 函数可以取得当前工作路径的字符串，还可以利用 `os.chdir()` 改变它：

```python
import os
print(os.getcwd())
os.chdir('D:\data')
print(os.getcwd())
```

运行结果如下：

```python
C:\Users\Administrator\Desktop\Demo\python
D:\data
```

>   如果使用 `os.chdir()` 修改的工作目录不存在，`Python` 解释器会报错，例如：`FileNotFoundError: [WinError 2] 系统找不到指定的文件。: 'D:\\dataaa'`

### 2、绝对路径与相对路径

明确一个文件所在的路径，有 2 种表示方式，分别是：

-   绝对路径：总是从根文件夹开始，Window 系统中以盘符（C：、D：）作为根文件夹，而 Linux 系统中以 / 作为根文件夹。
-   相对路径：指的是文件相对于当前工作目录所在的位置。例如，当前工作目录为 "C:\Windows\System32"，若文件 demo.txt 就位于这个 System32 文件夹下，则 demo.txt 的相对路径表示为 ".\demo.txt"（其中 .\ 就表示当前所在目录）。

### 3、Python 处理绝对路径和相对路径

Python `os.path` 模块提供了一些函数，可以实现绝对路径和相对路径之间的转换，以及检查给定的路径是否为绝对路径，如下：

-   调用 `os.path.abspath(path)`，返回 `path` 参数的绝对路径的字符串。
-   调用 `os.path.isabs(path)`，如果参数是一个绝对路径，就返回 `True`，如果参数是一个相对路径，就返回 `False`
-   调用 `os.path.relpath(path, start)`，返回从 `start` 路径到 `path` 的相对路径的字符串。如果没有提供 `start`，就使用当前工作目录作为开始路径
-   调用 `os.path.dirname(path)`，返回包含 `path` 参数中最后一个斜杠之前所有内容的字符串
-   调用 `os.path.basename(path)`，返回包含 `path` 参数中最后一个斜杠之后所有内容的字符串

```python
import os
print(os.path.abspath('.'))
print(os.path.isabs('D:\\data'), os.path.isabs('.'))
print(os.path.relpath('D:\\', 'D:\\Data\\WindTerm_Data'), os.path.relpath('C:\\'))
print(os.path.dirname('D:\\Data\\WindTerm_Data\\update.log'))
print(os.path.basename('D:\\Data\\WindTerm_Data\\update.log'))
```

运行结果如下：

```python
C:\Users\Administrator\Desktop\Demo\python
True False
..\.. ..\..\..\..\..
D:\Data\WindTerm_Data
update.log
```

如果同时需要一个路径的目录名和文件名，可以调用 `os.path.split()` 获得这两个字符串的元组，例如：

```python
import os
print(os.path.split('D:\\data\\WindTerm\\update.log'))
```

运行结果如下：

```python
('D:\\data\\WindTerm', 'update.log')
```

如果提供的路径不存在，许多 Python 函数就会崩溃并报错，`os.path` 模块提供了以下函数用于检测给定的路径是否存在，以及它是文件还是文件夹：

-   `os.path.exists(path)`：如果 `path` 所指的文件或文件夹存在，返回 `True`，否则返回 `False`。
-   `os.path.isfile(path)`：如果 `path` 存在且是一个文件，返回 `True`，否则返回 `False`。
-   `os.path.isdir(path)`：如果 `path` 存在且是一个文件夹，返回 `True`，否则返回 `False`。

```python
import os
print(os.path.exists('D:\\data\\test.log'), os.path.exists('D:\\data'))
print(os.path.isdir('D:\\data'), os.path.isdir('C:\\Program Files\\wegame.exe'))
print(os.path.isfile('D:\\data'), os.path.isfile('C:\\Program Files\\wegame.exe'))
```

运行结果如下：

```python
False True
True False
False True
```

## 3、Python 文件基本操作

`Python` 中，对文件常见的操作包括创建、删除、修改权限、读取、写入等，可大致分为以下 2 类：

1.  删除、修改权限：作用于文件本身，属于系统级操作。
2.  写入、读取：是文件最常用的操作，作用于文件的内容，属于应用级操作。

### 1、系统级操作

#### 1、删除文件

```python
import os
os.remove('a.txt')
```

### 2、应用级操作

对文件的应用级操作，通常需要按照固定的步骤进行操作，且实现过程相对比较复杂。文件的应用级操作可以分为以下 3 步，每一步都需要借助对应的函数实现：

1.  打开文件：使用 `open()` 函数，该函数会返回一个文件对象；
2.  对已打开文件做读/写操作：读取文件内容可使用 `read()`、`readline()` 以及 `readlines()` 函数；向文件中写入内容，可以使用 `write()` 函数。
3.  关闭文件：完成对文件的读/写操作之后，最后需要关闭文件，可以使用 `close()` 函数。

一个文件，必须在打开之后才能对其进行操作，并且在操作结束之后，还应该将其关闭，这 3 步的顺序不能打乱。

#### 1、open() 函数：打开文件

在 `Python` 中，要操作文件，首先需要创建或者打开指定的文件，并创建一个文件对象，而这些工作可以通过内置的 `open()` 函数实现。

`open()` 函数语法如下：

```python
open(file[, mode='r'][, buffering=-1][, encoding=None][, errors=None][, newline=None][, closefd=True][, opener=None])
```

参数说明：

-   `file`: 要打开的文件路径

-   `mode`: 文件打开的模式

    | 模式 | 说明                                                         | 注意                                                       |
    | ---- | ------------------------------------------------------------ | ---------------------------------------------------------- |
    | r    | 只读模式打开文件，读文件内容的指针会放在文件的开头。（默认） | 文件必须存在                                               |
    | rb   | 以二进制格式、采用只读模式打开文件，读文件内容的指针位于文件的开头。 | 文件必须存在                                               |
    | r+   | 打开文件后，既可以从头读取文件内容，也可以从开头向文件中写入新的内容，写入的新内容会覆盖文件中等长度的原有内容。 | 文件必须存在                                               |
    | rb+  | 以二进制格式、采用读写模式打开文件，读写文件的指针会放在文件的开头。 | 文件必须存在                                               |
    | w    | 以只写模式打开文件，若该文件存在，打开时会清空文件中原有的内容。 | 若文件存在覆盖文件，反之创建新文件。                       |
    | wb   | 以二进制格式、只写模式打开文件。                             | 若文件存在覆盖文件，反之创建新文件。                       |
    | w+   | 打开文件后，会对原有内容进行清空，并对该文件有读写权限。     | 若文件存在覆盖文件，反之创建新文件。                       |
    | wb+  | 以二进制格式、读写模式打开文件                               | 若文件存在覆盖文件，反之创建新文件。                       |
    | a    | 以追加模式打开一个文件，对文件只有写入权限，                 | 若文件存在，文件指针将放在文件的末尾；反之则会创建新文件。 |
    | ab   | 以追加模式打开一个文件，对文件只有写入权限，                 | 若文件存在，文件指针将放在文件的末尾；反之则会创建新文件。 |
    | a+   | 以追加模式打开一个文件，对文件只有写入权限，                 | 若文件存在，文件指针将放在文件的末尾；反之则会创建新文件。 |
    | ab+  | 以二进制模式打开文件，并采用追加模式，对文件具有读写权限，   | 若文件存在，文件指针将放在文件的末尾；反之则会创建新文件。 |
    | x    | 排它性创建，若文件存在则失败                                 |                                                            |

-   `buffering`: 对文件读写时，是否使用缓冲区

-   `encoding`: 指定打开文件时使用的编码格式

>   文件打开模式，直接决定了后续可以对文件做哪些操作。例如，使用 r 模式打开的文件，后续编写的代码只能读取文件，而无法修改文件内容。

![不同文件打开模式的功能](https://storage.zhums.cn/d/images/image-2023111160925132.png)

```python
file1 = open('a.txt')
file2 = open('a.txt', encoding='utf-8')
print(file1)
print(file2)
```

运行结果如下：

```python
<_io.TextIOWrapper name='a.txt' mode='r' encoding='cp936'>
<_io.TextIOWrapper name='a.txt' mode='r' encoding='utf-8'>
```

>   注意，手动修改 `encoding` 参数的值，仅限于文件以文本的形式打开，以二进制格式打开时，不能对 `encoding` 参数的值做任何修改，否则程序会抛出 `ValueError` 异常，如下所示：`ValueError: binary mode doesn't take an encoding argument`

##### open() 的缓冲区

通常情况下、建议使用 `open()` 函数时打开缓冲区，即不需要修改 `buffing` 参数的值。

>   如果 `buffing` 参数的值为 `0`（或者 `False`），则表示在打开指定文件时不使用缓冲区；如果 `buffing` 参数值为大于 `1` 的整数，该整数用于指定缓冲区的大小（单位是字节）；如果 `buffing` 参数的值为负数，则代表使用默认的缓冲区大小。

原因很简单，目前为止计算机内存的 `I/O` 速度仍远远高于计算机外设（例如键盘、鼠标、硬盘等）的 `I/O` 速度，如果不使用缓冲区，则程序在执行 `I/O` 操作时，内存和外设就必须进行同步读写操作，也就是说，内存必须等待外设输入（输出）一个字节之后，才能再次输出（输入）一个字节。这意味着，内存中的程序大部分时间都处于等待状态。

而如果使用缓冲区，则程序在执行输出操作时，会先将所有数据都输出到缓冲区中，然后继续执行其它操作，缓冲区中的数据会有外设自行读取处理；同样，当程序执行输入操作时，会先等外设将数据读入缓冲区中，无需同外设做同步读写操作。

##### 文件对象常用的属性

成功打开文件之后，可以调用文件对象本身拥有的属性获取当前文件的部分信息，其常见的属性为：

-   `file.name`：返回文件的名称；
-   `file.mode`：返回打开文件时，采用的打开模式；
-   `file.encoding`：返回打开文件时，使用的编码格式；
-   `file.closed`：判断文件是否己经关闭。

```python
file1 = open('a.txt', mode='w', encoding='utf-8')
print(file1.closed)
print(file1.name)
print(file1.mode)
print(file1.encoding)
```

运行结果如下：

```python
False
a.txt
w
utf-8
```

>   使用 `open()` 函数打开的文件对象，必须手动进行关闭，Python 垃圾回收机制无法自动回收打开文件所占用的资源。

#### 2、读取文件

##### 1、read() 方法：按字节（字符）读取文件

-   `read()`：逐个字节或者字符读取文件中的内容；

对于使用 `open()` 方法，并以可读模式（包括 `r`、`r+`、`rb`、`rb+`）打开的文件，可以调用 `read()` 函数逐个字节（或者逐个字符）读取文件中的内容。

>   如果文件是以文本模式（非二进制模式）打开的，则 `read()` 方法会逐个字符进行读取；反之，如果文件以二进制模式打开，则 `read()` 方法会逐个字节进行读取。

`read()` 方法的基本语法格式如下：

```python
file.read([size])
```

-   `file`：表示已打开的文件对象；
-   `size`：指定一次最多可读取的字符（字节）个数，默认一次性读取所有内容。

```python
# install.log 文件内容如下
2023-10-31 11:53:36 - [Info]: [ -----> 开始运行任务 "配置 History" <----- ]
2023-10-31 11:53:37 - [Success]: [ -----> Histroy 配置成功! <----- ]
```

```python
file1 = open('install.log', encoding='utf-8')
print(file1.read())
file1.close()

>>>
2023-10-31 11:53:36 - [Info]: [ -----> 开始运行任务 "配置 History" <----- ]
2023-10-31 11:53:37 - [Success]: [ -----> Histroy 配置成功! <----- ]
```

使用 `size` 参数，指定 `read()` 每次可读取的最大字符（或者字节）数，例如：

```python
file1 = open('install.log', encoding='utf-8')
print(file1.read(5))
file1.close()

>>>
2023-
```

>   `size` 表示一次最多可读取的字符（或字节）数，即便设置的 `size` 大于文件中存储的字符（字节）数，`read()` 函数也不会报错，它只会读取文件中所有的数据。

对于以二进制格式打开的文件，`read()` 会逐个字节读取文件中的内容。例如：

```python
file1 = open('install.log', mode='rb')
print(file1.read(10))
file1.close()

>>>
b'2023-10-31 11:53:36 - [Info]: [ -----> \xe5\xbc\x80\xe5\xa7\x8b\xe8\xbf\x90\xe8\xa1\x8c\xe4\xbb\xbb\xe5\x8a\xa1 "\xe9\x85\x8d\xe7\xbd\xae History" <----- ]\r\n2023-10-31 11:53:37 - [Success]: [ -----> Histroy \xe9\x85\x8d\xe7\xbd\xae\xe6\x88\x90\xe5\x8a\x9f! <----- ]'
```

>   可以看到，输出的数据为 `bytes` 字节串。可以调用 `decode()` 方法，将其转换成我们认识的字符串。

##### 2、readline() 方法：按行读取文件

-   `readline()`：逐行读取文件中的内容；

`readline()` 方法用于读取文件中的一行，以 `\n` 作为读取一行的标志。基本语法格式为：

```python
readline([size])
```

`file`：打开的文件对象；

`size`：指定读取每一行时，一次最多读取的字符（字节）数。

>   和 `read()` 方法一样，此方法成功读取文件数据的前提是，使用 `open()` 函数指定打开文件的模式必须为可读模式（包括 `r、rb、r+、rb+` 4 种）。

```python
file1 = open('config.log', encoding='utf-8')
print(file1.readline())
print(file1.readline(10))
file1.close()

>>>
2023-10-31 11:53:36 - [Info]: [ -----> 开始运行任务 "配置 History" <----- ]

2023-10-31

```

##### 3、readlines() 方法：按行读取文件

-   `readlines()`：读取文件中的所有行，它和调用不指定 `size` 参数的 `read()` 方法类似，只不过该函数返回是一个字符串列表，每个元素为文件中的一行内容。

>   和 `readline()` 方法一样，`readlines()` 方法在读取每一行时，会连同行尾的换行符一块读取。
>
>   和 `read()`、`readline()` 方法一样，此方法成功读取文件数据的前提是，使用 `open()` 函数指定打开文件的模式必须为可读模式（包括 `r、rb、r+、rb+` 4 种）。

```python
file1 = open('config.log', encoding='utf-8')
print(file1.readlines())
file1.close()

>>>
['2023-10-31 11:53:36 - [Info]: [ -----> 开始运行任务 "配置 History" <----- ]\n', '2023-10-31 11:53:37 - [Success]: [ -----> Histroy 配置成功! <----- ]']
```

#### 3、写入文件

##### 1、write() 方法

`write()` 方法，可以向文件中写入指定内容。语法如下：

```python
file.write(string)
```

`file`：表示已经打开的文件对象；

`string`：表示要写入文件的字符串（或字节串，仅适用写入二进制文件中）。

>   使用 `write()` 写入数据时，需保证 `open()` 函数是以 `r+、w、w+、a、a+` 的模式打开文件，否则执行 `write()` 函数会抛出 `io.UnsupportedOperation` 错误。

```python
# host.txt 内容如下
ip=10.0.0.10
netmask=255.255.255.0
```

```python
file1 = open('host.txt', mode='a+')
file1.write("\ngateway=10.0.0.1")
print(file1.read())
file1.close()

>>>

```

```python
# 运行后 host.txt 内容如下：
ip=10.0.0.10
netmask=255.255.255.0
gateway=10.0.0.1
```

>   写入文件完成后，要调用 `close()` 方法将文件关闭，否则写入的内容不会保存到文件中。例如，将上面程序中最后一行 `file1.close()` 删掉，再次运行此程序并打开 `host.txt`，发现该文件是空的。因为在写入文件内容时，系统不会立刻把数据写入磁盘，而是先缓存起来，只有调用 `close()` 方法时，系统才会将没有写入的数据全部写入磁盘文件中。
>
>   如果向文件写入数据后，不想马上关闭文件，也可以调用文件对象提供的 `flush()` 方法，将缓冲区的数据写入文件中。

通过设置 `open()` 函数的 `buffering` 参数可以关闭缓冲区，这样数据不就可以直接写入文件中了？对于以二进制格式打开的文件，可以不使用缓冲区，写入的数据会直接进入磁盘文件；但对于以文本格式打开的文件，必须使用缓冲区，否则 Python 解释器会 `ValueError` 错误。例如：

```python
file1 = open(file='a.txt', mode='w', buffering=0)
file1.write("test")

>>>
Traceback (most recent call last):
  File "c:/Users/Administrator/Desktop/Demo/python/hello.py", line 1, in <module>
    file1 = open(file='a.txt', mode='w', buffering=0)
ValueError: can't have unbuffered text I/O
```

##### 2、writelines() 方法

`writelines()` 方法，可以实现将字符串列表写入文件中。

例如：通过使用 `writelines()` 方法，可以轻松实现将 `a.txt` 文件中的数据复制到其它文件中，如下：

```python
file1 = open(file='a.txt')
file2 = open(file='b.txt', mode='w')
file2.writelines(file1.readlines())
file1.close()
file2.close()
```

执行此代码，在 `a.txt` 文件同级目录下会生成一个 `b.txt` 文件，且该文件中包含的数据和 `a.txt` 完全一样。

>   使用 `writelines()` 方法向文件中写入多行数据时，不会自动给各行添加换行符。上面例子中，之所以 `b.txt` 文件中会逐行显示数据，是因为 `readlines()` 函数在读取各行数据时，读入了行尾的换行符。

#### 4、close() 方法：关闭文件

`close()` 方法用来关闭已打开文件的，语法如下：

```python
file.close()
```

-   `file`： 表示已打开的文件对象。

使用 `open()` 函数打开的文件，在操作完成后，一定要调用 `close()` 方法将其关闭。文件在打开并操作完成之后，就应该及时关闭，否则程序的运行可能出现问题。

举个例子，分析如下代码：

```python
import os
f = open("my_file.txt",'w')
os.remove("my_file.txt")
```

代码中，我们引入了 `os` 模块，调用了该模块中的 `remove()` 方法，该方法的功能是删除指定的文件。但是，如果运行此程序，`Python` 解释器会报如下错误：

```python
Traceback (most recent call last):
  File "c:/Users/Administrator/Desktop/Demo/python/hello.py", line 3, in <module>
    os.remove("my_file.txt")
PermissionError: [WinError 32] 另一个程序正在使用此文件，进程无法访问。: 'my_file.txt'
```

显然，由于使用 `open()` 函数打开了 `my_file.txt` 文件，但没有及时关闭，导致后续 `remove()` 方法运行出现错误。

如果不调用 `close()` 方法关闭已打开的文件，确定不影响读取文件的操作，但会导致 `write()` 或者 `writeline()` 函数向文件中写数据时，写入失败。例如：

```python
f = open("my_file.txt", 'w')
f.write("http://c.biancheng.net/shell/")
```

程序执行后，虽然 `Python` 解释器不报错，但打开 `my_file.txt` 文件会发现，根本没有写入成功。这是因为，在向以文本格式（而不是二进制格式）打开的文件中写入数据时，`Python` 出于效率的考虑，会先将数据临时存储到缓冲区中，只有使用 `close()` 方法关闭文件时，才会将缓冲区中的数据真正写入文件中。

因此，在上面程序的最后添加如下代码：

```python
f.close()
```

再次运行程序，就会看到 "http://c.biancheng.net/shell/" 成功写入到了 `a.txt` 文件。

当然在某些实际场景中，我们可能需要在将数据成功写入到文件中，但并不想关闭文件。这也是可以实现的，调用 `flush()` 方法即可，例如：

```python
f = open("my_file.txt", 'w')
f.write("http://c.biancheng.net/shell/")f.flush()
```

打开 `my_file.txt` 文件，会发现已经向文件中成功写入了字符串 "http://c.biancheng.net/shell/"。

#### 5、seek() 和 tell() 方法

##### 1、文件指针

使用 `open()` 函数打开文件并读取文件中的内容时，总是会从文件的第一个字符（字节）开始。如果要指定读取的起始位置就需要移动文件指针的位置。

文件指针用于标明文件读写的起始位置。假如把文件看成一个水流，文件中每个数据（以普通模式打开，每个数据就是一个字符；以 `b` 模式打开，每个数据就是一个字节）就相当于一个水滴，而文件指针就标明了文件将要从文件的哪个位置开始读起。

通过移动文件指针的位置，再借助 `read()` 和 `write()` 方法，就可以轻松实现，读取文件中指定位置的数据（或者向文件中的指定位置写入数据）。

实现移动文件指针文件对象提供了 `tell()` 和 `seek()` 方法：

-   `tell()`：方法用于判断文件指针当前所处的位置
-   `seek()`：方法用于移动文件指针到文件的指定位置。

##### 2、tell() 方法

`tell()` 方法基本语法如下：

```python
file.tell()
```

-   `file`：表示文件对象

```python
file = open(file='a.txt')
print(file.tell())
print(file.read(5))
print(file.tell())

>>>
0
Hello
5
```

可以看到，当使用 `open()` 函数打开文件时，文件指针的起始位置为 `0`，表示位于文件的开头处，当使用 `read()` 函数从文件中读取 `5` 个字符之后，文件指针同时向后移动了 `5` 个字符的位置。这表明，当程序使用文件对象读写数据时，文件指针会自动向后移动：读写了多少个数据，文件指针就自动向后移动多少个位置。

##### 3、seek() 方法

`seek()` 方法用于将文件指针移动至指定位置，语法格式如下：

```python
file.seek(offset[, whence])
```

-   `file`：表示文件对象；
-   `whence`：指定文件指针要放置的位置，`0` 代表文件头（默认值）、`1` 代表当前位置、`2` 代表文件尾。
-   `offset`：表示相对于 `whence` 位置文件指针的偏移量，正数表示向后偏移，负数表示向前偏移。例如，当 `whence == 1 && offset == 5`（即 `seek(5,1)` ），表示文件指针从当前位置向后移动 `5` 个字符。

>   注意：当 `offset` 值非 `0` 时，`Python` 要求文件必须要以二进制格式打开，否则会抛出 `io.UnsupportedOperation` 错误。

```python
f = open('a.txt', 'rb')
print(f.tell())		# 返回文件指针的位置
print(f.read(1))    # 读取一个字节，文件指针自动后移 1 个数据
print(f.tell())
f.seek(5)			# 将文件指针从文件开头，向后移动到 5 个字符的位置
print(f.tell())
print(f.read(1))
f.seek(5, 1)		# 将文件指针从当前位置，向后移动到 5 个字符的位置
print(f.tell())
print(f.read(1))
print(f.tell())
f.seek(-1, 2)		# 将文件指针从文件结尾，向前移动到 1 个字符的位置
print(f.tell())
print(f.read(1))

>>>
0
b'H'
1
5
b' '
11
b'n'
12
11
b'n'
```

## 4、Python 中的 with as 语句

文件的输入输出、数据库的连接断开等，都是常见的资源管理操作。但资源都是有限的，在写程序时，必须保证这些资源在使用过后得到释放，不然就容易造成资源泄露，轻者使得系统处理缓慢，严重时会使系统崩溃。

例如，在文件操作时，打开的文件最后一定要关闭，否则会程序的运行造成意想不到的隐患。但是，即便使用 `close()` 做好了关闭文件的操作，如果在打开文件或文件操作过程中抛出了异常，还是无法及时关闭文件。

为了更好地避免此类问题，不同的编程语言都引入了不同的机制。在 Python 中，对应的解决方式是使用 `with as` 语句操作上下文管理器（context manager），它能够帮助我们自动分配并且释放资源。

>   简单的理解，同时包含 `__enter__()` 和 `__exit__()` 方法的对象就是上下文管理器。常见构建上下文管理器的方式有 2 种，分别是基于类实现和基于生成器实现，

例如，使用 with as 操作已经打开的文件对象（本身就是上下文管理器），无论期间是否抛出异常，都能保证 with as 语句执行完毕后自动关闭已经打开的文件。

`with as` 语句的语法格式：

```python
with expression [as target]：
    codes
```

`target` 参数用于指定一个变量，`expression` 指定的结果保存到该变量中。`with as` 语句中的代码块如果不想执行任何语句，可以直接使用 `pass` 关键字代替。

```python
# a.txt 内容如下
Hello Python
```

```python
with open('a.txt', 'a') as f:
	f.write("\n人生苦短，我学 Python")
```

运行结果为：

```python
Hello Python
人生苦短，我学 Python
```

可以看到，通过使用 `with as` 语句，即便最终没有关闭文件，修改文件内容的操作也能成功。

## 5、Python 中的 pickle 模块

`Python` 中有个序列化过程叫作 `pickle`，它能够实现任意对象与文本之间的相互转化，也可以实现任意对象与二进制之间的相互转化。也就是说，`pickle` 可以实现 `Python` 对象的存储及恢复。

值得一提的是，`pickle` 是 `python` 语言的一个标准模块，安装 `python` 的同时就已经安装了 `pickle` 库，因此它不需要再单独安装，使用 `import` 将其导入到程序中，就可以直接使用。

`pickle` 模块提供了以下 4 个方法：

-   `load()`：读取指定的序列化数据文件，并返回对象。

-   `loads()`：读取给定的二进制对象数据，并将其转换为 `Python` 对象；
-   `dump()`：将 `Python` 中的对象序列化成二进制对象，并写入文件；
-   `dumps()`：将 `Python` 中的对象序列化成二进制对象，并返回；

以上这 4 个方法可分为两类，其中 `dumps` 和 `loads` 实现基于内存的 `Python` 对象与二进制互转；`dump` 和 `load` 实现基于文件的 `Python` 对象与二进制互转。

### dumps() 方法

将 `Python` 对象转为二进制对象，其语法如下：

```python
dumps(obj, protocol=None, *, fix_imports=True, buffer_callback=None)
```

-   `obj`：要转换的 Python 对象；
-   `protocol`：指定 `pickler` 使用的协议，可选择的协议范围 `0-5`。若未指定，默认值为 `4`

```python
import pickle
tup1 = ('I Love Python', {1, 2, 3}, None)
byt1 = pickle.dumps(tup1)		# 使用 dumps() 方法将 tup1 转成 byt1
print(type(byt1), byt1)

>>>
<class 'bytes'> b'\x80\x04\x95\x1e\x00\x00\x00\x00\x00\x00\x00\x8c\rI Love Python\x94\x8f\x94(K\x01K\x02K\x03\x90N\x87\x94.'
```

### loads() 方法

将二进制对象转换成 `Python` 对象，其语法如下：

```python
loads(data, *, fix_imports=True, encoding='ASCII', errors='strict')
```

-   `data`：表示要转换的二进制对象

```python
import pickle
tup1 = ('I Love Python', {1, 2, 3}, None)
byt1 = pickle.dumps(tup1)
print(type(byt1), byt1)
tup2 = pickle.loads(byt1)
print(type(tup2), tup2)

>>>
<class 'tuple'> ('I Love Python', {1, 2, 3}, None)
```

### dump() 方法

将 `Python` 对象转换成二进制文件，其语法如下：

```python
dump (obj, file,protocol=None, *, fix mports=True)
```

其中各个参数的具体含义如下：

-   `obj`：要转换的 `Python` 对象。
-   `file`：转换到指定的二进制文件中，要求该文件必须是以 `wb` 的打开方式进行操作。
-   `protocol`：指定 `pickler` 使用的协议，可选择的协议范围 `0-5`。若未指定，默认值为 `4`

```python
import pickle
tup1 = ('I Love Python', {1, 2, 3}, None)
with open('a.txt', 'wb') as f:
    pickle.dump(tup1, f)
```

### load() 方法

将二进制对象文件转换成 `Python` 对象。其语法如下：

```python
load(file, *, fix_imports=True, encoding='ASCII', errors='strict')
```

-   `file`：参数表示要转换的二进制对象文件（必须以 `rb` 的打开方式操作文件）

```python
import pickle
with open('a.txt', 'rb') as f:
    tup2 = pickle.load(f)
    print(type(tup2), tup2)

>>>
<class 'tuple'> ('I Love Python', {1, 2, 3}, None)
```

>   看似强大的 pickle 模块，其实也有它的短板，即 pickle 不支持并发地访问持久性对象，在复杂的系统环境下，尤其是读取海量数据时，使用 pickle 会使整个系统的 `I/O`读取性能成为瓶颈。这种情况下，可以使用 ZODB。
>
>   ZODB 是一个健壮的、多用户的和面向对象的数据库系统，专门用于存储 Python 语言中的对象数据，它能够存储和管理任意复杂的 Python 对象，并支持事务操作和并发控制。并且，ZODB 也是在 Python 的序列化操作基础之上实现的，因此要想有效地使用 ZODB，必须先学好 pickle。

## 6、Python 的 fileinput 模块

### input 方法

`input()` 方法用于同时打开指定的多个文件，还可以逐个读取这些文件中的内容。

`input()` 方法的语法如下：

```python
fileinput.input（files="filename1, filename2, ...", inplace=False, backup='', bufsize=0, mode='r', openhook=None）
```

返回一个 `FileInput` 对象，可以理解为是将多个指定文件合并之后的文件对象。其中，各个参数的含义如下：

-   `files`：多个文件的路径列表；
-   `inplace`：用于指定是否将标准输出的结果写回到文件，此参数默认值为 `False`；
-   `backup`：用于指定备份文件的扩展名；
-   `bufsize`：指定缓冲区的大小，默认为 `0`；
-   `mode`：打开文件的格式，默认为 `r`（只读格式）；
-   `openhook`：控制文件的打开方式，例如编码格式等。

>   注意：和 `open()` 函数不同，`input()` 方法不能指定打开文件的编码格式，这意味着使用该函数读取的所有文件，除非以二进制方式进行读取，否则该文件编码格式都必须和当前操作系统默认的编码格式相同，不然 Python 解释器可能会提示 UnicodeDecodeError 错误。

和 `open()` 函数返回单个的文件对象不同，`fileinput` 对象无需调用类似 `read()`、`readline()`、`readlines()` 这样的方法，直接通过 `for` 循环即可按次序读取多个文件中的数据。

使用 `fileinput.input()` 方法读取两个文件内容。

```python
import fileinput
for line in fileinput.input(files=('a.txt', 'b.txt')):		# for 循环遍历 fileinput 对象
    print(line)
fileinput.close()		# 关闭文件流
```

### 其它方法

| 方法          | 说明                                          |
| ------------- | --------------------------------------------- |
| `filename()`  | 返回当前正在读取的文件名                      |
| fileno()      | 返回当前正在读取文件的文件描述符              |
| lineno()      | 返回当前读取了多少行                          |
| filelineno()  | 返回当前正在读取的内容位于当前文件中的行号    |
| isfirstline() | 判断当前读取的内容是否在当前文件中位于第 1 行 |
| nextfile()    | 关闭当前正在读取的文件，并开始读取下一个文件  |
| close()       | 关闭 `FileInput` 对象                         |

## 7、Python 中的 linecache 模块

`linecache` 模块擅长读取指定文件中的指定行。

`linecache` 模块常用来读取 `Python` 源文件中的代码，它使用的是 `UTF-8` 编码格式来读取文件内容。这意味着，使用该模块读取的文件，其编码格式也必须为 `UTF-8`，否则要么读取出来的数据是乱码，要么直接读取失败（`Python` 解释器会报 `SyntaxError` 异常）。

### getline() 方法

`getline()` 方法用于读取指定模块中指定文件的指定行（仅读取指定文件时，无需指定模块）。

```python
getline(filename, lineno, module_globals=None)
```

-   `filename`：指定文件名
-   `lineno`：指定行号
-   `module_globals`：指定要读取的具体模块名。==当指定文件以相对路径的方式传给 filename 参数时，按照 sys.path 规定的路径查找该文件==

```python
import linecache
print(linecache.getline(filename='a.txt', lineno=2))
print(linecache.getline(linecache.__file__, 8))

>>>
Ubuntu CentOS

import functools

```

### 其它方法

| 方法                      | 说明                                                         |
| ------------------------- | ------------------------------------------------------------ |
| clearcache()              | 如果程序某处，不再需要之前使用 `getline()` 函数读取的数据，则可以使用该方法清空缓存 |
| checkcache(filename=None) | 检查缓存的有效性，即如果使用 `getline()` 函数读取的数据，其实在本地已经被修改，此时就可以使用该方法检查缓存是否为新的数据。如果省略文件名，将检车所有缓存数据的有效性。 |

## 8、Python 的 pathlib 模块

### pathlib 模块介绍

`pathlib` 模块中包含的是一些类，它们的继承关系如下图所示：

![../_images/pathlib-inheritance.png](https://storage.zhums.cn/d/images/image-2023111060925132.png)

>   上图中，箭头连接的是有继承关系的两个类，以 `PurePosixPath` 和 `PurePath` 类为例，`PurePosizPath` 继承自 `PurePath`，即前者是后者的子类。

`pathlib` 模块的操作对象是各种操作系统中使用的路径（例如指定文件位置的路径，包括绝对路径和相对路径）。上图中类的功能：

-   `PurePath`：类会将路径看做是一个普通的字符串，它可以实现将多个指定的字符串拼接成适用于当前操作系统的路径格式，同时还可以判断任意两个路径是否相等。注意，使用 `PurePath` 操作的路径，它并不会关心该路径是否真实有效。
-   `PurePosixPath/PureWindowsPath`：`PurePath` 的子类，前者用于操作 `UNIX` 风格的路径，后者用于操作 `Windows` 风格的路径。
-   `Path`：操作的路径一定是真实有效的。`Path` 类提供了判断路径是否真实存在的方法。
-   `PosixPath/WindowPath`：`Path` 的子类，分别用于操作 `Unix` 风格的路径和 `Windows` 风格的路径。

### PurePath 类的用法

PurePath 类（以及 PurePosixPath 类和 PureWindowsPath 类）都提供了大量的构造方法、实例方法以及类实例属性，供我们使用。

#### PurePath 类构造方法

需要注意的是，在使用 `PurePath` 类时，考虑到操作系统的不同，如果在 `UNIX` 系统上使用 `PurePath` 创建对象，该类的构造方法实际返回的是 `PurePosixPath` 对象；反之，如果在 `Windows` 系统上使用 `PurePath` 创建对象，该类的构造方法返回的是 `PureWindowsPath` 对象。当然，完全可以直接使用 `PurePosixPath` 类或者 `PureWindowsPath` 类创建指定操作系统使用的类对象。

```python
from pathlib import *
path = PurePath('a.txt')
print(type(path))

>>>
<class 'pathlib.PureWindowsPath'>
```

`PurePath` 在创建对象时，也支持传入多个路径字符串，它们会被拼接成一个路径格式的字符串。例如：

```python
from pathlib import *
path1 = PurePath('https:', 'zhums.cn', 'op')
print(path1)

>>>
https:\zhums.cn\op
```

可以看到，由于本机为 Windows 系统，因此这里输出的是适用于 Windows 平台的路径。如果想在 Windows 系统上输出 UNIX 风格的路径字符串，就需要使用 `PurePosixPath` 类。例如：

```python
from pathlib import *
path2 = PurePosixPath('https:', 'zhums.cn', 'op')
print(path2)

>>>
https:/zhums.cn/op
```

如果在使用 `PurePath` 类构造方法时，不传入任何参数，则等同于传入点 `.`（表示当前路径）作为参数。例如：

```python
from pathlib import *
path1 = PurePath()
print(path1)

>>>
.
```

如果传入 PurePath 构造方法中的多个参数中，包含多个根路径，则只会有最后一个根路径及后面的子路径生效。例如：

```python
from pathlib import *
path = PurePath('C://','D://','my_file.txt')
print(path)

>>>
D:\my_file.txt
```

如果传给 PurePath 构造方法的参数中包含有多余的斜杠或者点（ `.` 表示当前路径），会直接被忽略（ `..` 不会被忽略）。举个例子：

```python
from pathlib import *
path = PurePath('C://../my_file.txt')
print(path)

>>>
C:\..\my_file.txt
```

`PurePath` 类还重载各种比较运算符，多余同种风格的路径字符串来说，可以判断是否相等，也可以比较大小（实际上就是比较字符串的大小）；对于不同种风格的路径字符串之间，只能判断是否相等（显然，不可能相等），但不能比较大小。

```python
from pathlib import *
# Unix风格的路径区分大小写
print(PurePosixPath('C://my_file.txt') == PurePosixPath('c://my_file.txt'))
# Windows风格的路径不区分大小写
print(PureWindowsPath('C://my_file.txt') == PureWindowsPath('c://my_file.txt'))

>>>
False
True
```

比较特殊的是，PurePath 类对象支持直接使用斜杠（/）作为多个字符串之间的连接符，例如：

```python
from pathlib import *
path = PurePosixPath('C://')
print(path / 'my_file.txt')

>>>
C:/my_file.txt
```

#### PurePath 类实例属性和实例方法

下表罗列出了常用的 PurePath 类实例方法和属性。由于从本质上讲，PurePath 的操作对象是字符串，因此表中的这些实例属性和实例方法，实质也是对字符串进行操作。

| 类实例属性和实例方法名       | 功能描述                                                     |
| ---------------------------- | ------------------------------------------------------------ |
| PurePath.parts               | 返回路径字符串中所包含的各部分。                             |
| PurePath.drive               | 返回路径字符串中的驱动器盘符。                               |
| PurePath.root                | 返回路径字符串中的根路径。                                   |
| PurePath.anchor              | 返回路径字符串中的盘符和根路径。                             |
| PurePath.parents             | 返回当前路径的全部父路径。                                   |
| PurPath.parent               | 返回当前路径的上一级路径，相当于 parents[0] 的返回值。       |
| PurePath.name                | 返回当前路径中的文件名。                                     |
| PurePath.suffixes            | 返回当前路径中的文件所有后缀名。                             |
| PurePath.suffix              | 返回当前路径中的文件后缀名。相当于 suffixes 属性返回的列表的最后一个元素。 |
| PurePath.stem                | 返回当前路径中的主文件名。                                   |
| PurePath.as_posix()          | 将当前路径转换成 UNIX 风格的路径。                           |
| PurePath.as_uri()            | 将当前路径转换成 URL。只有绝对路径才能转换，否则将会引发 ValueError。 |
| PurePath.is_absolute()       | 判断当前路径是否为绝对路径。                                 |
| PurePath.joinpath(*other)    | 将多个路径连接在一起，作用类似于前面介绍的斜杠（/）连接符。  |
| PurePath.match(pattern)      | 判断当前路径是否匹配指定通配符。                             |
| PurePath.relative_to(*other) | 获取当前路径中去除基准路径之后的结果。                       |
| PurePath.with_name(name)     | 将当前路径中的文件名替换成新文件名。如果当前路径中没有文件名，则会引发 ValueError。 |
| PurePath.with_suffix(suffix) | 将当前路径中的文件后缀名替换成新的后缀名。如果当前路径中没有后缀名，则会添加新的后缀名。 |

### path 类的功能和用法

和 PurPath 类相比，Path 类的最大不同，就是支持对路径的真实性进行判断。

Path 是 PurePath 的子类，因此 Path 类除了支持 PurePath 提供的各种构造函数、实例属性以及实例方法之外，还提供甄别路径字符串有效性的方法，甚至还可以判断该路径对应的是文件还是文件夹，如果是文件，还支持对文件进行读写等操作。

和 PurePath 一样，Path 同样有 2 个子类，分别为 PosixPath（表示 UNIX 风格的路径）和 WindowsPath（表示 Windows 风格的路径）。

官方手册 https://docs.python.org/3/library/pathlib.html

## 9、Python 的 os 模块

### os.path 模块

| 方法                                | 说明                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| os.path.abspath(path)               | 返回 path 的绝对路径。                                       |
| os.path.basename(path)              | 获取 path 路径的基本名称，即 path 末尾到最后一个斜杠的位置之间的字符串。 |
| os.path.commonprefix(list)          | 返回 list（多个路径）中，所有 path 共有的最长的路径。        |
| os.path.dirname(path)               | 返回 path 路径中的目录部分。                                 |
| os.path.exists(path)                | 判断 path 对应的文件是否存在，如果存在，返回 True；反之，返回 False。和 lexists() 的区别在于，exists()会自动判断失效的文件链接（类似 Windows 系统中文件的快捷方式），而 lexists() 却不会。 |
| os.path.lexists(path)               | 判断路径是否存在，如果存在，则返回 True；反之，返回 False。  |
| os.path.expanduser(path)            | 把 path 中包含的 "~" 和 "~user" 转换成用户目录。             |
| os.path.expandvars(path)            | 根据环境变量的值替换 path 中包含的 "$name" 和 "${name}"。    |
| os.path.getatime(path)              | 返回 path 所指文件的最近访问时间（浮点型秒数）。             |
| os.path.getmtime(path)              | 返回文件的最近修改时间（单位为秒）。                         |
| os.path.getctime(path)              | 返回文件的创建时间（单位为秒，自 1970 年 1 月 1 日起（又称 Unix 时间））。 |
| os.path.getsize(path)               | 返回文件大小，如果文件不存在就返回错误。                     |
| os.path.isabs(path)                 | 判断是否为绝对路径。                                         |
| os.path.isfile(path)                | 判断路径是否为文件。                                         |
| os.path.isdir(path)                 | 判断路径是否为目录。                                         |
| os.path.islink(path)                | 判断路径是否为链接文件（类似 Windows 系统中的快捷方式）。    |
| os.path.ismount(path)               | 判断路径是否为挂载点。                                       |
| os.path.join(path1[, path2[, ...]]) | 把目录和文件名合成一个路径。                                 |
| os.path.normcase(path)              | 转换 path 的大小写和斜杠。                                   |
| os.path.normpath(path)              | 规范 path 字符串形式。                                       |
| os.path.realpath(path)              | 返回 path 的真实路径。                                       |
| os.path.relpath(path[, start])      | 从 start 开始计算相对路径。                                  |
| os.path.samefile(path1, path2)      | 判断目录或文件是否相同。                                     |
| os.path.sameopenfile(fp1, fp2)      | 判断 fp1 和 fp2 是否指向同一文件。                           |
| os.path.samestat(stat1, stat2)      | 判断 stat1 和 stat2 是否指向同一个文件。                     |
| os.path.split(path)                 | 把路径分割成 dirname 和 basename，返回一个元组。             |
| os.path.splitdrive(path)            | 一般用在 windows 下，返回驱动器名和路径组成的元组。          |
| os.path.splitext(path)              | 分割路径，返回路径名和文件扩展名的元组。                     |
| os.path.splitunc(path)              | 把路径分割为加载点与文件。                                   |
| os.path.walk(path, visit, arg)      | 遍历path，进入每个目录都调用 visit 函数，visit 函数必须有 3 个参数(arg, dirname, names)，dirname 表示当前目录的目录名，names 代表当前目录下的所有文件名，args 则为 walk 的第三个参数。 |
| os.path.supports_unicode_filenames  | 设置是否可以将任意 Unicode 字符串用作文件名。                |

## 10、Python 的 fnmatch 模块

fnmatch 模块中，常用的函数及其功能如表所示。

| 函数名                                 | 功能                                                         |
| -------------------------------------- | ------------------------------------------------------------ |
| fnmatch.filter(names, pattern)         | 对 names 列表进行过滤，返回 names 列表中匹配 pattern 的文件名组成的子集合。 |
| fnmatch.fnmatch(filename, pattern)     | 判断 filename 文件名，是否和指定 pattern 字符串匹配          |
| fnmatch.fnmatchcase(filename, pattern) | 和 fnmatch() 函数功能大致相同，只是该函数区分大小写。        |
| fnmatch.translate(pattern)             | 将一个 UNIX shell 风格的 pattern 字符串，转换为正则表达式    |

fnmatch 模块匹配文件名的模式使用的就是 UNIX shell 风格，其支持使用如下几个通配符：

-   *：可匹配任意个任意字符。
-   ？：可匹配一个任意字符。
-   [字符序列]：可匹配中括号里字符序列中的任意字符。该字符序列也支持中画线表示法。比如 [a-c] 可代表 a、b 和 c 字符中任意一个。
-   [!字符序列]：可匹配不在中括号里字符序列中的任意字符。

## 11、Python 的 tempfile 模块

tempfile 模块专门用于创建临时文件和临时目录

tempfile 模块中常用的函数，如下表所示。

| tempfile 模块函数                                            | 功能描述                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| tempfile.TemporaryFile(mode='w+b', buffering=None, encoding=None, newline=None, suffix=None, prefix=None, dir=None) | 创建临时文件。该函数返回一个类文件对象，也就是支持文件 I/O。 |
| tempfile.NamedTemporaryFile(mode='w+b', buffering=None, encoding=None, newline=None, suffix=None, prefix=None, dir=None, delete=True) | 创建临时文件。该函数的功能与上一个函数的功能大致相同，只是它生成的临时文件在文件系统中有文件名。 |
| tempfile.SpooledTemporaryFile(max_size=0, mode='w+b', buffering=None, encoding=None, newline=None, suffix=None, prefix=None, dir=None) | 创建临时文件。与 TemporaryFile 函数相比，当程序向该临时文件输出数据时，会先输出到内存中，直到超过 max_size 才会真正输出到物理磁盘中。 |
| tempfile.TemporaryDirectory(suffix=None, prefix=None, dir=None) | 生成临时目录。                                               |
| tempfile.gettempdir()                                        | 获取系统的临时目录。                                         |
| tempfile.gettempdirb()                                       | 与 gettempdir() 相同，只是该函数返回字节串。                 |
| tempfile.gettempprefix()                                     | 返回用于生成临时文件的前缀名。                               |
| tempfile.gettempprefixb()                                    | 与 gettempprefix() 相同，只是该函数返回字节串。              |

>   提示：表中有些函数包含很多参数，但这些参数都具有自己的默认值，因此如果没有特殊要求，可以不对其传参。

tempfile 模块还提供了 tempfile.mkstemp() 和 tempfile.mkdtemp() 两个低级别的函数。上面介绍的 4 个用于创建临时文件和临时目录的函数都是高级别的函数，高级别的函数支持自动清理，而且可以与 with 语句一起使用，而这两个低级别的函数则不支持，因此一般推荐使用高级别的函数来创建临时文件和临时目录。

此外，tempfile 模块还提供了 tempfile.tempdir 属性，通过对该属性赋值可以改变系统的临时目录。

```python
import tempfile

# 创建临时文件
fp = tempfile.TemporaryFile(mode='w+')      
print(fp.name)
fp.write('人生苦短，我用 Python')
fp.seek(0)          # 将文件指针移到开头，准备读取文件
print(fp.read())    # 输出刚才写入的内容
fp.close()          # 关闭文件，该文件将会被自动删除

# 通过 with 语句创建临时文件，with 会自动关闭临时文件
with tempfile.TemporaryFile(mode='w+') as fp:
    fp.write('I Love Python!')      # 写入内容
    fp.seek(0)          # 将文件指针移到开始处，准备读取文件
    print(fp.read())    # 读取文件内容

# 通过 with 语句创建临时目录
with tempfile.TemporaryDirectory() as tmpdir:
    print('创建临时目录', tmpdir)
```

运行结果为：

```python
C:\Users\Administrator\AppData\Local\Temp\tmpfg7gb6jz
人生苦短，我用 Python
I Love Python!
创建临时目录 C:\Users\Administrator\AppData\Local\Temp\tmpzvdsy4od
```



# 