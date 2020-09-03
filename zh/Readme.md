# Chinese

语言的名字（python 一词直译为 “蟒蛇”）得名自 BBC 节目 “Monty Python的飞行马戏团” ，而与爬行动物没有关系。在文档中用 Monty Python 来开玩笑不只是被允许的，还是被推荐的！


## Docs:
[Chinese](https://docs.python.org/zh-cn/3/)

### 常识:
[基础](base.md)

### 作为计算器使用[](https://docs.python.org/zh-cn/3/tutorial/introduction.html#using-python-as-a-calculator "永久链接至标题")

让我们尝试一些简单的 Python 命令。启动解释器，等待界面中的提示符，`>>>`  （这应该花不了多少时间）。

#### 数字[](https://docs.python.org/zh-cn/3/tutorial/introduction.html#numbers "永久链接至标题")

解释器就像一个简单的计算器一样：你可以在里面输入一个表达式然后它会写出答案。 表达式的语法很直接：运算符  `+`、`-`、`*`、`/`  的用法和其他大部分语言一样（比如 Pascal 或者 C 语言）；括号 (`()`) 用来分组。比如:

>>>

>>> 2 + 2
4
>>> 50 - 5*6
20
>>> (50 - 5*6) / 4
5.0
>>> 8 / 5  # division always returns a floating point number
1.6

整数（比如  `2`、`4`、`20`  ）的类型是  [`int`](https://docs.python.org/zh-cn/3/library/functions.html#int "int")，有小数部分的（比如  `5.0`、`1.6`  ）的类型是  [`float`](https://docs.python.org/zh-cn/3/library/functions.html#float "float")。 在这个手册的后半部分我们会看到更多的数字类型。

除法运算 (`/`) 永远返回浮点数类型。如果要做  [floor division](https://docs.python.org/zh-cn/3/glossary.html#term-floor-division)  得到一个整数结果（忽略小数部分）你可以使用  `//`  运算符；如果要计算余数，可以使用  `%`

>>>

>>> 17 / 3  # classic division returns a float
5.666666666666667
>>>
>>> 17 // 3  # floor division discards the fractional part
5
>>> 17 % 3  # the % operator returns the remainder of the division
2
>>> 5 * 3 + 2  # result * divisor + remainder
17

在Python中，可以使用  `**`  运算符来计算乘方  [1](https://docs.python.org/zh-cn/3/tutorial/introduction.html#id3)

>>>

>>> 5 ** 2  # 5 squared
25
>>> 2 ** 7  # 2 to the power of 7
128

等号 (`=`) 用于给一个变量赋值。然后在下一个交互提示符之前不会有结果显示出来:

>>>

>>> width = 20
>>> height = 5 * 9
>>> width * height
900

如果一个变量未定义（未赋值），试图使用它时会向你提示错误:

>>>

>>> n  # try to access an undefined variable
Traceback (most recent call last): File "<stdin>", line 1, in <module>
NameError: name 'n' is not defined

Python中提供浮点数的完整支持；包含多种混合类型运算数的运算会把整数转换为浮点数:

>>>

>>> 4 * 3.75 - 1
14.0

在交互模式下，上一次打印出来的表达式被赋值给变量  `_`。这意味着当你把Python用作桌面计算器时，继续计算会相对简单，比如:

>>>

>>> tax = 12.5 / 100
>>> price = 100.50
>>> price * tax
12.5625
>>> price + _
113.0625
>>> round(_, 2)
113.06

这个变量应该被使用者当作是只读类型。不要向它显式地赋值——你会创建一个和它名字相同独立的本地变量，它会使用魔法行为屏蔽内部变量。

除了  [`int`](https://docs.python.org/zh-cn/3/library/functions.html#int "int")  和  [`float`](https://docs.python.org/zh-cn/3/library/functions.html#float "float")，Python也支持其他类型的数字，例如  [`Decimal`](https://docs.python.org/zh-cn/3/library/decimal.html#decimal.Decimal "decimal.Decimal")  或者  [`Fraction`](https://docs.python.org/zh-cn/3/library/fractions.html#fractions.Fraction "fractions.Fraction")。Python 也内置对  [复数](https://docs.python.org/zh-cn/3/library/stdtypes.html#typesnumeric)  的支持，使用后缀  `j`  或者  `J`  就可以表示虚数部分（例如  `3+5j`  ）。

#### 字符串[](https://docs.python.org/zh-cn/3/tutorial/introduction.html#strings "永久链接至标题")

除了数字，Python 也可以操作字符串。字符串有多种形式，可以使用单引号（`'...'`），双引号（`"..."`）都可以获得同样的结果  [2](https://docs.python.org/zh-cn/3/tutorial/introduction.html#id4)。反斜杠  `\`  可以用来转义:

>>>

>>> 'spam eggs'  # single quotes
'spam eggs'
>>> 'doesn\'t'  # use \' to escape the single quote...
"doesn't"
>>> "doesn't"  # ...or use double quotes instead
"doesn't"
>>> '"Yes," they said.'
'"Yes," they said.'
>>> "\"Yes,\" they said."
'"Yes," they said.'
>>> '"Isn\'t," they said.'
'"Isn\'t," they said.'

在交互式解释器中，输出的字符串外面会加上引号，特殊字符会使用反斜杠来转义。 虽然有时这看起来会与输入不一样（外面所加的引号可能会改变），但两个字符串是相同的。 如果字符串中有单引号而没有双引号，该字符串外将加双引号来表示，否则就加单引号。  [`print()`](https://docs.python.org/zh-cn/3/library/functions.html#print "print")  函数会生成可读性更强的输出，即略去两边的引号，并且打印出经过转义的特殊字符:

>>>

>>> '"Isn\'t," they said.'
'"Isn\'t," they said.'
>>> print('"Isn\'t," they said.')
"Isn't," they said.
>>> s = 'First line.\nSecond line.'  # \n means newline
>>> s  # without print(), \n is included in the output
'First line.\nSecond line.'
>>> print(s)  # with print(), \n produces a new line
First line.
Second line.

如果你不希望前置了  `\`  的字符转义成特殊字符，可以使用  _原始字符串_  方式，在引号前添加  `r`  即可:

>>>

>>> print('C:\some\name')  # here \n means newline!
C:\some
ame
>>> print(r'C:\some\name')  # note the r before the quote
C:\some\name

字符串字面值可以跨行连续输入。一种方式是用三重引号：`"""..."""`  或  `'''...'''`。字符串中的回车换行会自动包含到字符串中，如果不想包含，在行尾添加一个  `\`  即可。如下例:

print("""\
Usage: thingy [OPTIONS]
 -h                        Display this usage message
 -H hostname               Hostname to connect to
""")

将产生如下输出（注意最开始的换行没有包括进来）:

Usage: thingy [OPTIONS]
     -h                        Display this usage message
     -H hostname               Hostname to connect to

字符串可以用  `+`  进行连接（粘到一起），也可以用  `*`  进行重复:

>>>

>>> # 3 times 'un', followed by 'ium'
>>> 3 * 'un' + 'ium'
'unununium'

相邻的两个或多个  _字符串字面值_  （引号引起来的字符）将会自动连接到一起.

>>>

>>> 'Py' 'thon'
'Python'

把很长的字符串拆开分别输入的时候尤其有用:

>>>

>>> text = ('Put several strings within parentheses '
...         'to have them joined together.')
>>> text
'Put several strings within parentheses to have them joined together.'

只能对两个字面值这样操作，变量或表达式不行:

>>>

>>> prefix = 'Py'
>>> prefix 'thon'  # can't concatenate a variable and a string literal
  File "<stdin>", line 1
    prefix 'thon'
                ^
SyntaxError: invalid syntax
>>> ('un' * 3) 'ium'
  File "<stdin>", line 1
    ('un' * 3) 'ium'
                   ^
SyntaxError: invalid syntax

如果你想连接变量，或者连接变量和字面值，可以用  `+`  号:

>>>

>>> prefix + 'thon'
'Python'

字符串是可以被  _索引_  （下标访问）的，第一个字符索引是 0。单个字符并没有特殊的类型，只是一个长度为一的字符串:

>>>

>>> word = 'Python'
>>> word[0]  # character in position 0
'P'
>>> word[5]  # character in position 5
'n'

索引也可以用负数，这种会从右边开始数:

>>>

>>> word[-1]  # last character
'n'
>>> word[-2]  # second-last character
'o'
>>> word[-6]
'P'

注意 -0 和 0 是一样的，所以负数索引从 -1 开始。

除了索引，字符串还支持  _切片_。索引可以得到单个字符，而  _切片_  可以获取子字符串:

>>>

>>> word[0:2]  # characters from position 0 (included) to 2 (excluded)
'Py'
>>> word[2:5]  # characters from position 2 (included) to 5 (excluded)
'tho'

注意切片的开始总是被包括在结果中，而结束不被包括。这使得  `s[:i]  +  s[i:]`  总是等于  `s`

>>>

>>> word[:2] + word[2:]
'Python'
>>> word[:4] + word[4:]
'Python'

切片的索引有默认值；省略开始索引时默认为0，省略结束索引时默认为到字符串的结束:

>>>

>>> word[:2]   # character from the beginning to position 2 (excluded)
'Py'
>>> word[4:]   # characters from position 4 (included) to the end
'on'
>>> word[-2:]  # characters from the second-last (included) to the end
'on'

您也可以这么理解切片：将索引视作指向字符  _之间_  ，第一个字符的左侧标为0，最后一个字符的右侧标为  _n_  ，其中  _n_  是字符串长度。例如:

 +---+---+---+---+---+---+
 | P | y | t | h | o | n |
 +---+---+---+---+---+---+
 0   1   2   3   4   5   6
-6  -5  -4  -3  -2  -1

第一行数标注了字符串 0...6 的索引的位置，第二行标注了对应的负的索引。那么从  _i_  到  _j_  的切片就包括了标有  _i_  和  _j_  的位置之间的所有字符。

对于使用非负索引的切片，如果索引不越界，那么得到的切片长度就是起止索引之差。例如，  `word[1:3]`  的长度为2。

试图使用过大的索引会产生一个错误:

>>>

>>> word[42]  # the word only has 6 characters
Traceback (most recent call last): File "<stdin>", line 1, in <module>
IndexError: string index out of range

但是，切片中的越界索引会被自动处理:

>>>

>>> word[4:42]
'on'
>>> word[42:]
''

Python 中的字符串不能被修改，它们是  [immutable](https://docs.python.org/zh-cn/3/glossary.html#term-immutable)  的。因此，向字符串的某个索引位置赋值会产生一个错误:

>>>

>>> word[0] = 'J'
Traceback (most recent call last): File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
>>> word[2:] = 'py'
Traceback (most recent call last): File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment

如果需要一个不同的字符串，应当新建一个:

>>>

>>> 'J' + word[1:]
'Jython'
>>> word[:2] + 'py'
'Pypy'

内建函数  [`len()`](https://docs.python.org/zh-cn/3/library/functions.html#len "len")  返回一个字符串的长度:

>>>

>>> s = 'supercalifragilisticexpialidocious'
>>> len(s)
34

参见

[文本序列类型 --- str](https://docs.python.org/zh-cn/3/library/stdtypes.html#textseq)

字符串是一种  _序列类型_  ，因此也支持序列类型的各种操作。

[字符串的方法](https://docs.python.org/zh-cn/3/library/stdtypes.html#string-methods)

字符串支持许多变换和查找的方法。

[格式化字符串字面值](https://docs.python.org/zh-cn/3/reference/lexical_analysis.html#f-strings)

内嵌表达式的字符串字面值。

[格式字符串语法](https://docs.python.org/zh-cn/3/library/string.html#formatstrings)

使用  [`str.format()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.format "str.format")  进行字符串格式化。

[printf 风格的字符串格式化](https://docs.python.org/zh-cn/3/library/stdtypes.html#old-string-formatting)

这里详述了使用  `%`  运算符进行字符串格式化。

#### 列表[](https://docs.python.org/zh-cn/3/tutorial/introduction.html#lists "永久链接至标题")

Python 中可以通过组合一些值得到多种  _复合_  数据类型。其中最常用的  _列表_  ，可以通过方括号括起、逗号分隔的一组值（元素）得到。一个  _列表_  可以包含不同类型的元素，但通常使用时各个元素类型相同:

>>>

>>> squares = [1, 4, 9, 16, 25]
>>> squares
[1, 4, 9, 16, 25]

和字符串（以及各种内置的  [sequence](https://docs.python.org/zh-cn/3/glossary.html#term-sequence)  类型）一样，列表也支持索引和切片:

>>>

>>> squares[0]  # indexing returns the item
1
>>> squares[-1]
25
>>> squares[-3:]  # slicing returns a new list
[9, 16, 25]

所有的切片操作都返回一个包含所请求元素的新列表。 这意味着以下切片操作会返回列表的一个  [浅拷贝](https://docs.python.org/zh-cn/3/library/copy.html#shallow-vs-deep-copy):

>>>

>>> squares[:]
[1, 4, 9, 16, 25]

列表同样支持拼接操作:

>>>

>>> squares + [36, 49, 64, 81, 100]
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

与  [immutable](https://docs.python.org/zh-cn/3/glossary.html#term-immutable)  的字符串不同, 列表是一个  [mutable](https://docs.python.org/zh-cn/3/glossary.html#term-mutable)  类型，就是说，它自己的内容可以改变:

>>>

>>> cubes = [1, 8, 27, 65, 125]  # something's wrong here
>>> 4 ** 3  # the cube of 4 is 64, not 65!
64
>>> cubes[3] = 64  # replace the wrong value
>>> cubes
[1, 8, 27, 64, 125]

你也可以在列表末尾通过  `append()`  _方法_  来添加新元素（我们将在后面介绍有关方法的详情）:

>>>

>>> cubes.append(216)  # add the cube of 6
>>> cubes.append(7 ** 3)  # and the cube of 7
>>> cubes
[1, 8, 27, 64, 125, 216, 343]

给切片赋值也是可以的，这样甚至可以改变列表大小，或者把列表整个清空:

>>>

>>> letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
>>> letters
['a', 'b', 'c', 'd', 'e', 'f', 'g']
>>> # replace some values
>>> letters[2:5] = ['C', 'D', 'E']
>>> letters
['a', 'b', 'C', 'D', 'E', 'f', 'g']
>>> # now remove them
>>> letters[2:5] = []
>>> letters
['a', 'b', 'f', 'g']
>>> # clear the list by replacing all the elements with an empty list
>>> letters[:] = []
>>> letters
[]

内置函数  [`len()`](https://docs.python.org/zh-cn/3/library/functions.html#len "len")  也可以作用到列表上:

>>>

>>> letters = ['a', 'b', 'c', 'd']
>>> len(letters)
4

也可以嵌套列表 (创建包含其他列表的列表), 比如说:

>>>

>>> a = ['a', 'b', 'c']
>>> n = [1, 2, 3]
>>> x = [a, n]
>>> x
[['a', 'b', 'c'], [1, 2, 3]]
>>> x[0]
['a', 'b', 'c']
>>> x[0][1]
'b'


### 第一步[](https://docs.python.org/zh-cn/3/tutorial/introduction.html#first-steps-towards-programming "永久链接至标题")

当然，我们可以将 Python 用于更复杂的任务，而不是仅仅两个和两个一起添加。 例如，我们可以编写  [斐波那契数列](https://en.wikipedia.org/wiki/Fibonacci_number)  的初始子序列，如下所示:

>>>

>>> # Fibonacci series:
... # the sum of two elements defines the next
... a, b = 0, 1
>>> while a < 10:
...     print(a)
...     a, b = b, a+b
...
0
1
1
2
3
5
8

这个例子引入了几个新的特性。

-   第一行含有一个  _多重赋值_: 变量  `a`  和  `b`  同时得到了新值 0 和 1. 最后一行又用了一次多重赋值, 这展示出了右手边的表达式，在任何赋值发生之前就被求值了。右手边的表达式是从左到右被求值的。
    
-   [`while`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#while)  循环只要它的条件（这里指：  `a  <  10`）保持为真就会一直执行。Python 和 C 一样，任何非零整数都为真；零为假。这个条件也可以是字符串或是列表的值，事实上任何序列都可以；长度非零就为真，空序列就为假。在这个例子里，判断条件是一个简单的比较。标准的比较操作符的写法和 C 语言里是一样：  `<`  （小于）、  `>`  （大于）、  `==`  （等于）、  `<=`  （小于或等于)、  `>=`  （大于或等于）以及  `!=`  （不等于）。
    
-   _循环体_  是  _缩进的_  ：缩进是 Python 组织语句的方式。在交互式命令行里，你得给每个缩进的行敲下 Tab 键或者（多个）空格键。实际上用文本编辑器的话，你要准备更复杂的输入方式；所有像样的文本编辑器都有自动缩进的设置。交互式命令行里，当一个组合的语句输入时, 需要在最后敲一个空白行表示完成（因为语法分析器猜不出来你什么时候打的是最后一行）。注意，在同一块语句中的每一行，都要缩进相同的长度。
    
-   [`print()`](https://docs.python.org/zh-cn/3/library/functions.html#print "print")  函数将所有传进来的参数值打印出来. 它和直接输入你要显示的表达式(比如我们之前在计算器的例子里做的)不一样， print() 能处理多个参数，包括浮点数，字符串。 字符串会打印不带引号的内容, 并且在参数项之间会插入一个空格, 这样你就可以很好的把东西格式化, 像这样:
    
    >>>
    
    >>> i = 256*256
    >>> print('The value of i is', i)
    The value of i is 65536
    
    关键字参数  _end_  可以用来取消输出后面的换行, 或使用另外一个字符串来结尾:
    
    >>>
    
    >>> a, b = 0, 1
    >>> while a < 1000:
    ...     print(a, end=',')
    ...     a, b = b, a+b
    ...
    0,1,1,2,3,5,8,13,21,34,55,89,144,233,377,610,987,


### 其他流程控制工具[¶](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#more-control-flow-tools "永久链接至标题")

除了刚刚介绍过的  [`while`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#while)  语句，Python 中也会使用其他语言中常见的流程控制语句，只是稍有变化。

#### `if`  语句[](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#if-statements "永久链接至标题")

可能最为人所熟知的编程语句就是  [`if`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#if)  语句了。例如

>>>

>>> x = int(input("Please enter an integer: "))
Please enter an integer: 42
>>> if x < 0:
...     x = 0
...     print('Negative changed to zero')
... elif x == 0:
...     print('Zero')
... elif x == 1:
...     print('Single')
... else:
...     print('More')
...
More

可以有零个或多个  [`elif`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#elif)  部分，以及一个可选的  [`else`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#else)  部分。 关键字 '`elif`' 是 'else if' 的缩写，适合用于避免过多的缩进。 一个  `if`  ...  `elif`  ...  `elif`  ... 序列可以看作是其他语言中的  `switch`  或  `case`  语句的替代。

#### `for`  语句[](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#for-statements "永久链接至标题")

Python 中的  [`for`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#for)  语句与你在 C 或 Pascal 中所用到的有所不同。 Python 中的  `for`  语句并不总是对算术递增的数值进行迭代（如同 Pascal），或是给予用户定义迭代步骤和暂停条件的能力（如同 C），而是对任意序列进行迭代（例如列表或字符串），条目的迭代顺序与它们在序列中出现的顺序一致。 例如（此处英文为双关语）:

>>>

>>> # Measure some strings:
... words = ['cat', 'window', 'defenestrate']
>>> for w in words:
...     print(w, len(w))
...
cat 3
window 6
defenestrate 12

在遍历同一个集合时修改该集合的代码可能很难获得正确的结果。通常，更直接的做法是循环遍历该集合的副本或创建新集合：

# Strategy:  Iterate over a copy
for user, status in users.copy().items():
    if status == 'inactive':
        del users[user]

# Strategy:  Create a new collection
active_users = {}
for user, status in users.items():
    if status == 'active':
        active_users[user] = status

####  [`range()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#range "range")  函数[](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#the-range-function "永久链接至标题")

如果你确实需要遍历一个数字序列，内置函数  [`range()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#range "range")  会派上用场。它生成算术级数:

>>>

>>> for i in range(5):
...     print(i)
...
0
1
2
3
4

给定的终止数值并不在要生成的序列里；`range(10)`  会生成10个值，并且是以合法的索引生成一个长度为10的序列。range也可以以另一个数字开头，或者以指定的幅度增加（甚至是负数；有时这也被叫做 '步进'）

range(5, 10)
   5, 6, 7, 8, 9

range(0, 10, 3)
   0, 3, 6, 9

range(-10, -100, -30)
  -10, -40, -70

要以序列的索引来迭代，您可以将  [`range()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#range "range")  和  [`len()`](https://docs.python.org/zh-cn/3/library/functions.html#len "len")  组合如下:

>>>

>>> a = ['Mary', 'had', 'a', 'little', 'lamb']
>>> for i in range(len(a)):
...     print(i, a[i])
...
0 Mary
1 had
2 a
3 little
4 lamb

然而，在大多数这类情况下，使用  [`enumerate()`](https://docs.python.org/zh-cn/3/library/functions.html#enumerate "enumerate")  函数比较方便，请参见  [循环的技巧](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#tut-loopidioms)  。

如果你只打印 range，会出现奇怪的结果:

>>>

>>> print(range(10))
range(0, 10)

[`range()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#range "range")  所返回的对象在许多方面表现得像一个列表，但实际上却并不是。此对象会在你迭代它时基于所希望的序列返回连续的项，但它没有真正生成列表，这样就能节省空间。

我们称这样对象为  [iterable](https://docs.python.org/zh-cn/3/glossary.html#term-iterable)，也就是说，适合作为这样的目标对象：函数和结构期望从中获取连续的项直到所提供的项全部耗尽。 我们已经看到  [`for`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#for)  语句就是这样一种结构，而接受可迭代对象的函数的一个例子是  [`sum()`](https://docs.python.org/zh-cn/3/library/functions.html#sum "sum"):

>>>

>>> sum(range(4))  # 0 + 1 + 2 + 3
6

稍后我们将看到更多返回可迭代对象以及将可迭代对象作为参数的函数。 最后，也许你会很好奇如何从一个指定范围内获取一个列表。 以下是解决方案：

>>>

>>> list(range(4))
[0, 1, 2, 3]

在  [数据结构](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#tut-structures)  章节中，我们将讨论  [`list()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#list "list")  的更多细节。

## 4.4. `break`  和  `continue`  语句，以及循环中的  `else`  子句[](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#break-and-continue-statements-and-else-clauses-on-loops "永久链接至标题")

[`break`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#break)  语句，和 C 中的类似，用于跳出最近的  [`for`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#for)  或  [`while`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#while)  循环.

循环语句可能带有  `else`  子句；它会在循环耗尽了可迭代对象 (使用  [`for`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#for)) 或循环条件变为假值 (使用  [`while`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#while)) 时被执行，但不会在循环被  [`break`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#break)  语句终止时被执行。 以下搜索素数的循环就是这样的一个例子:

>>>

>>> for n in range(2, 10):
...     for x in range(2, n):
...         if n % x == 0:
...             print(n, 'equals', x, '*', n//x)
...             break
...     else:
...         # loop fell through without finding a factor
...         print(n, 'is a prime number')
...
2 is a prime number
3 is a prime number
4 equals 2 * 2
5 is a prime number
6 equals 2 * 3
7 is a prime number
8 equals 2 * 4
9 equals 3 * 3

（是的，这是正确的代码。仔细看：  `else`  子句属于  [`for`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#for)  循环，  **不属于**  [`if`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#if)  语句。）

当和循环一起使用时，`else`  子句与  [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try)  语句中的  `else`  子句的共同点多于  [`if`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#if)  语句中的同类子句:  [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try)  语句中的  `else`  子句会在未发生异常时执行，而循环中的  `else`  子句则会在未发生  `break`  时执行。 有关  `try`  语句和异常的更多信息，请参阅  [处理异常](https://docs.python.org/zh-cn/3/tutorial/errors.html#tut-handling)。

[`continue`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#continue)  语句也是借鉴自 C 语言，表示继续循环中的下一次迭代:

>>>

>>> for num in range(2, 10):
...     if num % 2 == 0:
...         print("Found an even number", num)
...         continue
...     print("Found a number", num)
Found an even number 2
Found a number 3
Found an even number 4
Found a number 5
Found an even number 6
Found a number 7
Found an even number 8
Found a number 9

####  `pass`  语句[](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#pass-statements "永久链接至标题")

[`pass`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#pass)  语句什么也不做。当语法上需要一个语句，但程序需要什么动作也不做时，可以使用它。例如:

>>>

>>> while True:
...     pass  # Busy-wait for keyboard interrupt (Ctrl+C)
...

这通常用于创建最小的类:

>>>

>>> class MyEmptyClass:
...     pass
...

[`pass`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#pass)  的另一个可以使用的场合是在你编写新的代码时作为一个函数或条件子句体的占位符，允许你保持在更抽象的层次上进行思考。  `pass`  会被静默地忽略:

>>>

>>> def initlog(*args):
...     pass   # Remember to implement this!
...

####  定义函数[](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#defining-functions "永久链接至标题")

我们可以创建一个输出任意范围内 Fibonacci 数列的函数:

>>>

>>> def fib(n):    # write Fibonacci series up to n
...     """Print a Fibonacci series up to n."""
...     a, b = 0, 1
...     while a < n:
...         print(a, end=' ')
...         a, b = b, a+b
...     print()
...
>>> # Now call the function we just defined:
... fib(2000)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597

关键字  [`def`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#def)  引入一个函数  _定义_。它必须后跟函数名称和带括号的形式参数列表。构成函数体的语句从下一行开始，并且必须缩进。

函数体的第一个语句可以（可选的）是字符串文字；这个字符串文字是函数的文档字符串或  _docstring_  。（有关文档字符串的更多信息，请参阅  [文档字符串](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#tut-docstrings)  部分）有些工具使用文档字符串自动生成在线或印刷文档，或者让用户以交互式的形式浏览代码；在你编写的代码中包含文档字符串是一种很好的做法，所以要养成习惯。

函数的  _执行_  会引入一个用于函数局部变量的新符号表。 更确切地说，函数中所有的变量赋值都将存储在局部符号表中；而变量引用会首先在局部符号表中查找，然后是外层函数的局部符号表，再然后是全局符号表，最后是内置名称的符号表。 因此，全局变量和外层函数的变量不能在函数内部直接赋值（除非是在  [`global`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#global)  语句中定义的全局变量，或者是在  [`nonlocal`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#nonlocal)  语句中定义的外层函数的变量），尽管它们可以被引用。

在函数被调用时，实际参数（实参）会被引入被调用函数的本地符号表中；因此，实参是通过  _按值调用_  传递的（其中  _值_  始终是对象  _引用_  而不是对象的值）。[1](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#id2)  当一个函数调用另外一个函数时，将会为该调用创建一个新的本地符号表。

函数定义会将函数名称与函数对象在当前符号表中进行关联。 解释器会将该名称所指向的对象识别为用户自定义函数。 其他名称也可指向同一个函数对象并可被用来访问访函数:

>>>

>>> fib
<function fib at 10042ed0>
>>> f = fib
>>> f(100)
0 1 1 2 3 5 8 13 21 34 55 89

如果你学过其他语言，你可能会认为  `fib`  不是函数而是一个过程，因为它并不返回值。事实上，即使没有  [`return`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#return)  语句的函数也会返回一个值，尽管它是一个相当无聊的值。这个值称为  `None`  （它是内置名称）。一般来说解释器不会打印出单独的返回值  `None`  ，如果你真想看到它，你可以使用  [`print()`](https://docs.python.org/zh-cn/3/library/functions.html#print "print")

>>>

>>> fib(0)
>>> print(fib(0))
None

写一个返回斐波那契数列的列表（而不是把它打印出来）的函数，非常简单:

>>>

>>> def fib2(n):  # return Fibonacci series up to n
...     """Return a list containing the Fibonacci series up to n."""
...     result = []
...     a, b = 0, 1
...     while a < n:
...         result.append(a)    # see below
...         a, b = b, a+b
...     return result
...
>>> f100 = fib2(100)    # call it
>>> f100                # write the result
[0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]

此示例中，像往常一样，演示了一些新的 Python 功能:

-   [`return`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#return)  语句会从函数内部返回一个值。 不带表达式参数的  `return`  会返回  `None`。 函数执行完毕退出也会返回  `None`。
    
-   `result.append(a)`  语句调用了列表对象  `result`  的  _方法_  。方法是“属于”一个对象的函数，它被命名为  `obj.methodname`  ，其中  `obj`  是某个对象（也可能是一个表达式），  `methodname`  是由对象类型中定义的方法的名称。不同的类型可以定义不同的方法。不同类型的方法可以有相同的名称而不会引起歧义。（可以使用  _类_  定义自己的对象类型和方法，请参阅  [类](https://docs.python.org/zh-cn/3/tutorial/classes.html#tut-classes)  ）示例中的方法  `append()`  是为列表对象定义的；它会在列表的最后添加一个新的元素。在这个示例中它相当于  `result  =  result  +  [a]`  ，但更高效。
    

####  函数定义的更多形式[](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#more-on-defining-functions "永久链接至标题")

给函数定义有可变数目的参数也是可行的。这里有三种形式，可以组合使用。

####  参数默认值[](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#default-argument-values "永久链接至标题")

最有用的形式是对一个或多个参数指定一个默认值。这样创建的函数，可以用比定义时允许的更少的参数调用，比如:

def ask_ok(prompt, retries=4, reminder='Please try again!'):
    while True:
        ok = input(prompt)
        if ok in ('y', 'ye', 'yes'):
            return True
        if ok in ('n', 'no', 'nop', 'nope'):
            return False
        retries = retries - 1
        if retries < 0:
            raise ValueError('invalid user response')
        print(reminder)

这个函数可以通过几种方式调用:

-   只给出必需的参数：`ask_ok('Do  you  really  want  to  quit?')`
    
-   给出一个可选的参数：`ask_ok('OK  to  overwrite  the  file?',  2)`
    
-   或者给出所有的参数：`ask_ok('OK  to  overwrite  the  file?',  2,  'Come  on,  only  yes  or  no!')`
    

这个示例还介绍了  [`in`](https://docs.python.org/zh-cn/3/reference/expressions.html#in)  关键字。它可以测试一个序列是否包含某个值。

默认值是在  _定义过程_  中在函数定义处计算的，所以

i = 5

def f(arg=i):
    print(arg)

i = 6
f()

会打印  `5`。

**重要警告：**  默认值只会执行一次。这条规则在默认值为可变对象（列表、字典以及大多数类实例）时很重要。比如，下面的函数会存储在后续调用中传递给它的参数:

def f(a, L=[]):
    L.append(a)
    return L

print(f(1))
print(f(2))
print(f(3))

这将打印出

[1]
[1, 2]
[1, 2, 3]

如果你不想要在后续调用之间共享默认值，你可以这样写这个函数:

def f(a, L=None):
    if L is None:
        L = []
    L.append(a)
    return L

#### 关键字参数[](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#keyword-arguments "永久链接至标题")

也可以使用形如  `kwarg=value`  的  [关键字参数](https://docs.python.org/zh-cn/3/glossary.html#term-keyword-argument)  来调用函数。例如下面的函数:

def parrot(voltage, state='a stiff', action='voom', type='Norwegian Blue'):
    print("-- This parrot wouldn't", action, end=' ')
    print("if you put", voltage, "volts through it.")
    print("-- Lovely plumage, the", type)
    print("-- It's", state, "!")

接受一个必需的参数（`voltage`）和三个可选的参数（`state`,  `action`，和  `type`）。这个函数可以通过下面的任何一种方式调用:

parrot(1000)                                          # 1 positional argument
parrot(voltage=1000)                                  # 1 keyword argument
parrot(voltage=1000000, action='VOOOOOM')             # 2 keyword arguments
parrot(action='VOOOOOM', voltage=1000000)             # 2 keyword arguments
parrot('a million', 'bereft of life', 'jump')         # 3 positional arguments
parrot('a thousand', state='pushing up the daisies')  # 1 positional, 1 keyword

但下面的函数调用都是无效的:

parrot()                     # required argument missing
parrot(voltage=5.0, 'dead')  # non-keyword argument after a keyword argument
parrot(110, voltage=220)     # duplicate value for the same argument
parrot(actor='John Cleese')  # unknown keyword argument

在函数调用中，关键字参数必须跟随在位置参数的后面。传递的所有关键字参数必须与函数接受的其中一个参数匹配（比如  `actor`  不是函数  `parrot`  的有效参数），它们的顺序并不重要。这也包括非可选参数，（比如  `parrot(voltage=1000)`  也是有效的）。不能对同一个参数多次赋值。下面是一个因为此限制而失败的例子:

>>>

>>> def function(a):
...     pass
...
>>> function(0, a=0)
Traceback (most recent call last): File "<stdin>", line 1, in <module>
TypeError: function() got multiple values for keyword argument 'a'

当存在一个形式为  `**name`  的最后一个形参时，它会接收一个字典 (参见  [映射类型 --- dict](https://docs.python.org/zh-cn/3/library/stdtypes.html#typesmapping))，其中包含除了与已有形参相对应的关键字参数以外的所有关键字参数。 这可以与一个形式为  `*name`，接收一个包含除了已有形参列表以外的位置参数的  [元组](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#tut-tuples)  的形参 (将在下一小节介绍) 组合使用 (`*name`  必须出现在  `**name`  之前。) 例如，如果我们这样定义一个函数:

def cheeseshop(kind, *arguments, **keywords):
    print("-- Do you have any", kind, "?")
    print("-- I'm sorry, we're all out of", kind)
    for arg in arguments:
        print(arg)
    print("-" * 40)
    for kw in keywords:
        print(kw, ":", keywords[kw])

它可以像这样调用:

cheeseshop("Limburger", "It's very runny, sir.",
           "It's really very, VERY runny, sir.",
           shopkeeper="Michael Palin",
           client="John Cleese",
           sketch="Cheese Shop Sketch")

当然它会打印:

-- Do you have any Limburger ?
-- I'm sorry, we're all out of Limburger
It's very runny, sir.
It's really very, VERY runny, sir.
----------------------------------------
shopkeeper : Michael Palin
client : John Cleese
sketch : Cheese Shop Sketch

注意打印时关键字参数的顺序保证与调用函数时提供它们的顺序是相匹配的。

####  特殊参数[](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#special-parameters "永久链接至标题")

默认情况下，函数的参数传递形式可以是位置参数或是显式的关键字参数。 为了确保可读性和运行效率，限制允许的参数传递形式是有意义的，这样开发者只需查看函数定义即可确定参数项是仅按位置、按位置也按关键字，还是仅按关键字传递。

函数的定义看起来可以像是这样：

def f(pos1, pos2, /, pos_or_kwd, *, kwd1, kwd2):
      -----------    ----------     ----------
        |             |                  |
        |        Positional or keyword   |
        |                                - Keyword only
         -- Positional only

在这里  `/`  和  `*`  是可选的。 如果使用这些符号则表明可以通过何种形参将参数值传递给函数：仅限位置、位置或关键字，以及仅限关键字。 关键字形参也被称为命名形参。

##### 位置或关键字参数[](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#positional-or-keyword-arguments "永久链接至标题")

如果函数定义中未使用  `/`  和  `*`，则参数可以按位置或按关键字传递给函数。

##### 仅限位置参数[](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#positional-only-parameters "永久链接至标题")

在这里还可以发现更多细节，特定形参可以被标记为  _仅限位置_。 如果是  _仅限位置_  的形参，则其位置是重要的，并且该形参不能作为关键字传入。 仅限位置形参要放在  `/`  (正斜杠) 之前。 这个  `/`  被用来从逻辑上分隔仅限位置形参和其它形参。 如果函数定义中没有  `/`，则表示没有仅限位置形参。

在  `/`  之后的形参可以为  _位置或关键字_  或  _仅限关键字_。

##### 仅限关键字参数[](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#keyword-only-arguments "永久链接至标题")

要将形参标记为  _仅限关键字_，即指明该形参必须以关键字参数的形式传入，应在参数列表的第一个  _仅限关键字_  形参之前放置一个  `*`。

##### 函数示例[](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#function-examples "永久链接至标题")

请考虑以下示例函数定义并特别注意  `/`  和  `*`  标记:

>>>

>>> def standard_arg(arg):
...     print(arg)
...
>>> def pos_only_arg(arg, /):
...     print(arg)
...
>>> def kwd_only_arg(*, arg):
...     print(arg)
...
>>> def combined_example(pos_only, /, standard, *, kwd_only):
...     print(pos_only, standard, kwd_only)

第一个函数定义  `standard_arg`  是最常见的形式，对调用方式没有任何限制，参数可以按位置也可以按关键字传入:

>>>

>>> standard_arg(2)
2

>>> standard_arg(arg=2)
2

第二个函数  `pos_only_arg`  在函数定义中带有  `/`，限制仅使用位置形参。:

>>>

>>> pos_only_arg(1)
1

>>> pos_only_arg(arg=1)
Traceback (most recent call last): File "<stdin>", line 1, in <module>
TypeError: pos_only_arg() got an unexpected keyword argument 'arg'

第三个函数  `kwd_only_args`  在函数定义中通过  `*`  指明仅允许关键字参数:

>>>

>>> kwd_only_arg(3)
Traceback (most recent call last): File "<stdin>", line 1, in <module>
TypeError: kwd_only_arg() takes 0 positional arguments but 1 was given

>>> kwd_only_arg(arg=3)
3

而最后一个则在同一函数定义中使用了全部三种调用方式:

>>>

>>> combined_example(1, 2, 3)
Traceback (most recent call last): File "<stdin>", line 1, in <module>
TypeError: combined_example() takes 2 positional arguments but 3 were given

>>> combined_example(1, 2, kwd_only=3)
1 2 3

>>> combined_example(1, standard=2, kwd_only=3)
1 2 3

>>> combined_example(pos_only=1, standard=2, kwd_only=3)
Traceback (most recent call last): File "<stdin>", line 1, in <module>
TypeError: combined_example() got an unexpected keyword argument 'pos_only'

最后，请考虑这个函数定义，它的位置参数  `name`  和  `**kwds`  之间由于存在关键字名称  `name`  而可能产生潜在冲突:

def foo(name, **kwds):
    return 'name' in kwds

任何调用都不可能让它返回  `True`，因为关键字  `'name'`  将总是绑定到第一个形参。 例如:

>>>

>>> foo(1, **{'name': 2})
Traceback (most recent call last): File "<stdin>", line 1, in <module>
TypeError: foo() got multiple values for argument 'name'
>>>

但使用  `/`  (仅限位置参数) 就可能做到，因为它允许  `name`  作为位置参数，也允许  `'name'`  作为关键字参数的关键字名称:

def foo(name, /, **kwds):
    return 'name' in kwds
>>> foo(1, **{'name': 2})
True

换句话说，仅限位置形参的名称可以在  `**kwds`  中使用而不产生歧义。

##### 概括[](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#recap "永久链接至标题")

用例将确定要在函数定义中使用的参数:

def f(pos1, pos2, /, pos_or_kwd, *, kwd1, kwd2):

作为指导：

-   如果你希望形参名称对用户来说不可用，则使用仅限位置形参。 这适用于形参名称没有实际意义，以及当你希望强制规定调用时的参数顺序，或是需要同时收受一些位置形参和任意关键字形参等情况。
    
-   当形参名称有实际意义，以及显式指定形参名称可使函数定义更易理解，或者当你想要防止用户过于依赖传入参数的位置时，则使用仅限关键字形参。
    
-   对于 API 来说，使用仅限位置形参可以防止形参名称在未来被修改时造成破坏性的 API 变动。
    

#### 任意的参数列表[](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#arbitrary-argument-lists "永久链接至标题")

最后，最不常用的选项是可以使用任意数量的参数调用函数。这些参数会被包含在一个元组里（参见  [元组和序列](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#tut-tuples)  ）。在可变数量的参数之前，可能会出现零个或多个普通参数。:

def write_multiple_items(file, separator, *args):
    file.write(separator.join(args))

一般来说，这些  `可变参数`  将在形式参数列表的末尾，因为它们收集传递给函数的所有剩余输入参数。出现在  `*args`  参数之后的任何形式参数都是 ‘仅限关键字参数’，也就是说它们只能作为关键字参数而不能是位置参数。:

>>>

>>> def concat(*args, sep="/"):
...     return sep.join(args)
...
>>> concat("earth", "mars", "venus")
'earth/mars/venus'
>>> concat("earth", "mars", "venus", sep=".")
'earth.mars.venus'

#### 解包参数列表[](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#unpacking-argument-lists "永久链接至标题")

当参数已经在列表或元组中但要为需要单独位置参数的函数调用解包时，会发生相反的情况。例如，内置的  [`range()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#range "range")  函数需要单独的  _start_  和  _stop_  参数。如果它们不能单独使用，可以使用  `*`  操作符 来编写函数调用以便从列表或元组中解包参数:

>>>

>>> list(range(3, 6))            # normal call with separate arguments
[3, 4, 5]
>>> args = [3, 6]
>>> list(range(*args))            # call with arguments unpacked from a list
[3, 4, 5]

同样的方式，字典可使用  `**`  操作符 来提供关键字参数:

>>>

>>> def parrot(voltage, state='a stiff', action='voom'):
...     print("-- This parrot wouldn't", action, end=' ')
...     print("if you put", voltage, "volts through it.", end=' ')
...     print("E's", state, "!")
...
>>> d = {"voltage": "four million", "state": "bleedin' demised", "action": "VOOM"}
>>> parrot(**d)
-- This parrot wouldn't VOOM if you put four million volts through it. E's bleedin' demised !

#### Lambda 表达式[](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#lambda-expressions "永久链接至标题")

可以用  [`lambda`](https://docs.python.org/zh-cn/3/reference/expressions.html#lambda)  关键字来创建一个小的匿名函数。这个函数返回两个参数的和：  `lambda  a,  b:  a+b`  。Lambda函数可以在需要函数对象的任何地方使用。它们在语法上限于单个表达式。从语义上来说，它们只是正常函数定义的语法糖。与嵌套函数定义一样，lambda函数可以引用所包含域的变量:

>>>

>>> def make_incrementor(n):
...     return lambda x: x + n
...
>>> f = make_incrementor(42)
>>> f(0)
42
>>> f(1)
43

上面的例子使用一个lambda表达式来返回一个函数。另一个用法是传递一个小函数作为参数:

>>>

>>> pairs = [(1, 'one'), (2, 'two'), (3, 'three'), (4, 'four')]
>>> pairs.sort(key=lambda pair: pair[1])
>>> pairs
[(4, 'four'), (1, 'one'), (3, 'three'), (2, 'two')]

#### 文档字符串[](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#documentation-strings "永久链接至标题")

以下是有关文档字符串的内容和格式的一些约定。

第一行应该是对象目的的简要概述。为简洁起见，它不应显式声明对象的名称或类型，因为这些可通过其他方式获得（除非名称恰好是描述函数操作的动词）。这一行应以大写字母开头，以句点结尾。

如果文档字符串中有更多行，则第二行应为空白，从而在视觉上将摘要与其余描述分开。后面几行应该是一个或多个段落，描述对象的调用约定，它的副作用等。

Python 解析器不会从 Python 中删除多行字符串文字的缩进，因此处理文档的工具必须在需要时删除缩进。 这是使用以下约定完成的。 文档字符串第一行  _之后_  的第一个非空行确定整个文档字符串的缩进量。（我们不能使用第一行，因为它通常与字符串的开头引号相邻，因此它的缩进在字符串文字中不明显。）然后从字符串的所有行的开头剥离与该缩进 "等效" 的空格。 缩进更少的行不应该出现，但是如果它们出现，则应该剥离它们的所有前导空格。 应在转化制表符为空格后测试空格的等效性（通常转化为8个空格）。

下面是一个多行文档字符串的例子:

>>>

>>> def my_function():
...     """Do nothing, but document it.
...
...     No, really, it doesn't do anything.
...     """
...     pass
...
>>> print(my_function.__doc__)
Do nothing, but document it.

 No, really, it doesn't do anything.

#### 函数标注[](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#function-annotations "永久链接至标题")

[函数标注](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#function)  是关于用户自定义函数中使用的类型的完全可选元数据信息（有关详情请参阅  [**PEP 3107**](https://www.python.org/dev/peps/pep-3107)  和  [**PEP 484**](https://www.python.org/dev/peps/pep-0484)  ）。

[函数标注](https://docs.python.org/zh-cn/3/glossary.html#term-function-annotation)  以字典的形式存放在函数的  `__annotations__`  属性中，并且不会影响函数的任何其他部分。 形参标注的定义方式是在形参名称后加上冒号，后面跟一个表达式，该表达式会被求值为标注的值。 返回值标注的定义方式是加上一个组合符号  `->`，后面跟一个表达式，该标注位于形参列表和表示  [`def`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#def)  语句结束的冒号之间。 下面的示例有一个位置参数，一个关键字参数以及返回值带有相应标注:

>>>

>>> def f(ham: str, eggs: str = 'eggs') -> str:
...     print("Annotations:", f.__annotations__)
...     print("Arguments:", ham, eggs)
...     return ham + ' and ' + eggs
...
>>> f('spam')
Annotations: {'ham': <class 'str'>, 'return': <class 'str'>, 'eggs': <class 'str'>}
Arguments: spam eggs
'spam and eggs'

##### 小插曲：编码风格[](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#intermezzo-coding-style "永久链接至标题")

现在你将要写更长，更复杂的 Python 代码，是时候讨论一下  _代码风格_  了。 大多数语言都能以不同的风格被编写（或更准确地说，被格式化）；有些比其他的更具有可读性。 能让其他人轻松阅读你的代码总是一个好主意，采用一种好的编码风格对此有很大帮助。

对于Python，[**PEP 8**](https://www.python.org/dev/peps/pep-0008)  已经成为大多数项目所遵循的风格指南；它促进了一种非常易读且令人赏心悦目的编码风格。每个Python开发人员都应该在某个时候阅读它；以下是为你提取的最重要的几个要点：

-   使用4个空格缩进，不要使用制表符。
    
    4个空格是一个在小缩进（允许更大的嵌套深度）和大缩进（更容易阅读）的一种很好的折中方案。制表符会引入混乱，最好不要使用它。
    
-   换行，使一行不超过79个字符。
    
    这有助于使用小型显示器的用户，并且可以在较大的显示器上并排放置多个代码文件。
    
-   使用空行分隔函数和类，以及函数内的较大的代码块。
    
-   如果可能，把注释放到单独的一行。
    
-   使用文档字符串。
    
-   在运算符前后和逗号后使用空格，但不能直接在括号内使用：  `a  =  f(1,  2)  +  g(3,  4)`。
    
-   以一致的规则为你的类和函数命名；按照惯例应使用  `UpperCamelCase`  来命名类，而以  `lowercase_with_underscores`  来命名函数和方法。 始终应使用  `self`  来命名第一个方法参数 (有关类和方法的更多信息请参阅  [初探类](https://docs.python.org/zh-cn/3/tutorial/classes.html#tut-firstclasses))。
    
-   如果你的代码旨在用于国际环境，请不要使用花哨的编码。Python 默认的 UTF-8 或者纯 ASCII 在任何情况下都能有最好的表现。
    
-   同样，哪怕只有很小的可能，遇到说不同语言的人阅读或维护代码，也不要在标识符中使用非ASCII字符。
    

备注

[1](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#id1)

实际上，_通过对象引用调用_  会是一个更好的表述，因为如果传递的是可变对象，则调用者将看到被调用者对其做出的任何更改（插入到列表中的元素）。