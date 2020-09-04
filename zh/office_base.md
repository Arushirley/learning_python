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


# 5. 数据结构[](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#data-structures "永久链接至标题")

本章节将详细介绍一些您已经了解的内容，并添加了一些新内容。

## 5.1. 列表的更多特性[](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#more-on-lists "永久链接至标题")

列表数据类型还有很多的方法。这里是列表对象方法的清单：

`list.``append`(_x_)

在列表的末尾添加一个元素。相当于  `a[len(a):]  =  [x]`  。

`list.``extend`(_iterable_)

使用可迭代对象中的所有元素来扩展列表。相当于  `a[len(a):]  =  iterable`  。

`list.``insert`(_i_,  _x_)

在给定的位置插入一个元素。第一个参数是要插入的元素的索引，所以  `a.insert(0,  x)`  插入列表头部，  `a.insert(len(a),  x)`  等同于  `a.append(x)`  。

`list.``remove`(_x_)

移除列表中第一个值为  _x_  的元素。如果没有这样的元素，则抛出  [`ValueError`](https://docs.python.org/zh-cn/3/library/exceptions.html#ValueError "ValueError")  异常。

`list.``pop`([_i_])

删除列表中给定位置的元素并返回它。如果没有给定位置，`a.pop()`  将会删除并返回列表中的最后一个元素。（ 方法签名中  _i_  两边的方括号表示这个参数是可选的，而不是要你输入方括号。你会在 Python 参考库中经常看到这种表示方法)。

`list.``clear`()

移除列表中的所有元素。等价于``del a[:]``

`list.``index`(_x_[,  _start_[,  _end_]])

返回列表中第一个值为  _x_  的元素的从零开始的索引。如果没有这样的元素将会抛出  [`ValueError`](https://docs.python.org/zh-cn/3/library/exceptions.html#ValueError "ValueError")  异常。

可选参数  _start_  和  _end_  是切片符号，用于将搜索限制为列表的特定子序列。返回的索引是相对于整个序列的开始计算的，而不是  _start_  参数。

`list.``count`(_x_)

返回元素  _x_  在列表中出现的次数。

`list.``sort`(_key=None_,  _reverse=False_)

对列表中的元素进行排序（参数可用于自定义排序，解释请参见  [`sorted()`](https://docs.python.org/zh-cn/3/library/functions.html#sorted "sorted")）。

`list.``reverse`()

翻转列表中的元素。

`list.``copy`()

返回列表的一个浅拷贝，等价于  `a[:]`。

多数列表方法示例：

>>>

>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits.count('apple')
2
>>> fruits.count('tangerine')
0
>>> fruits.index('banana')
3
>>> fruits.index('banana', 4)  # Find next banana starting a position 4
6
>>> fruits.reverse()
>>> fruits
['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange']
>>> fruits.append('grape')
>>> fruits
['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange', 'grape']
>>> fruits.sort()
>>> fruits
['apple', 'apple', 'banana', 'banana', 'grape', 'kiwi', 'orange', 'pear']
>>> fruits.pop()
'pear'

你可能已经注意到，像  `insert`  ，`remove`  或者  `sort`  方法，只修改列表，没有打印出返回值——它们返回默认值  `None`  。[1](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#id2)  这是Python中所有可变数据结构的设计原则。

你可能会注意到的另一件事是并非所有数据或可以排序或比较。 例如，`[None,  'hello',  10]`  就不可排序，因为整数不能与字符串比较，而  _None_  不能与其他类型比较。 并且还存在一些没有定义顺序关系的类型。 例如，`3+4j  <  5+7j`  就不是一个合法的比较。

### 5.1.1. 列表作为栈使用[](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#using-lists-as-stacks "永久链接至标题")

列表方法使得列表作为堆栈非常容易，最后一个插入，最先取出（“后进先出”）。要添加一个元素到堆栈的顶端，使用  `append()`  。要从堆栈顶部取出一个元素，使用  `pop()`  ，不用指定索引。例如

>>>

>>> stack = [3, 4, 5]
>>> stack.append(6)
>>> stack.append(7)
>>> stack
[3, 4, 5, 6, 7]
>>> stack.pop()
7
>>> stack
[3, 4, 5, 6]
>>> stack.pop()
6
>>> stack.pop()
5
>>> stack
[3, 4]

### 5.1.2. 列表作为队列使用[](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#using-lists-as-queues "永久链接至标题")

列表也可以用作队列，其中先添加的元素被最先取出 (“先进先出”)；然而列表用作这个目的相当低效。因为在列表的末尾添加和弹出元素非常快，但是在列表的开头插入或弹出元素却很慢 (因为所有的其他元素都必须移动一位)。

若要实现一个队列，可使用  [`collections.deque`](https://docs.python.org/zh-cn/3/library/collections.html#collections.deque "collections.deque")，它被设计成可以快速地从两端添加或弹出元素。例如

>>>

>>> from collections import deque
>>> queue = deque(["Eric", "John", "Michael"])
>>> queue.append("Terry")           # Terry arrives
>>> queue.append("Graham")          # Graham arrives
>>> queue.popleft()                 # The first to arrive now leaves
'Eric'
>>> queue.popleft()                 # The second to arrive now leaves
'John'
>>> queue                           # Remaining queue in order of arrival
deque(['Michael', 'Terry', 'Graham'])

### 5.1.3. 列表推导式[](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#list-comprehensions "永久链接至标题")

列表推导式提供了一个更简单的创建列表的方法。常见的用法是把某种操作应用于序列或可迭代对象的每个元素上，然后使用其结果来创建列表，或者通过满足某些特定条件元素来创建子序列。

例如，假设我们想创建一个平方列表，像这样

>>>

>>> squares = []
>>> for x in range(10):
...     squares.append(x**2)
...
>>> squares
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

注意这里创建（或被重写）的名为  `x`  的变量在for循环后仍然存在。我们可以计算平方列表的值而不会产生任何副作用

squares = list(map(lambda x: x**2, range(10)))

或者，等价于

squares = [x**2 for x in range(10)]

上面这种写法更加简洁易读。

列表推导式的结构是由一对方括号所包含的以下内容：一个表达式，后面跟一个  `for`  子句，然后是零个或多个  `for`  或  `if`  子句。 其结果将是一个新列表，由对表达式依据后面的  `for`  和  `if`  子句的内容进行求值计算而得出。 举例来说，以下列表推导式会将两个列表中不相等的元素组合起来:

>>>

>>> [(x, y) for x in [1,2,3] for y in [3,1,4] if x != y]
[(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]

而它等价于

>>>

>>> combs = []
>>> for x in [1,2,3]:
...     for y in [3,1,4]:
...         if x != y:
...             combs.append((x, y))
...
>>> combs
[(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]

注意在上面两个代码片段中，  [`for`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#for)  和  [`if`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#if)  的顺序是相同的。

如果表达式是一个元组（例如上面的  `(x,  y)`），那么就必须加上括号

>>>

>>> vec = [-4, -2, 0, 2, 4]
>>> # create a new list with the values doubled
>>> [x*2 for x in vec]
[-8, -4, 0, 4, 8]
>>> # filter the list to exclude negative numbers
>>> [x for x in vec if x >= 0]
[0, 2, 4]
>>> # apply a function to all the elements
>>> [abs(x) for x in vec]
[4, 2, 0, 2, 4]
>>> # call a method on each element
>>> freshfruit = ['  banana', '  loganberry ', 'passion fruit  ']
>>> [weapon.strip() for weapon in freshfruit]
['banana', 'loganberry', 'passion fruit']
>>> # create a list of 2-tuples like (number, square)
>>> [(x, x**2) for x in range(6)]
[(0, 0), (1, 1), (2, 4), (3, 9), (4, 16), (5, 25)]
>>> # the tuple must be parenthesized, otherwise an error is raised
>>> [x, x**2 for x in range(6)]
 File "<stdin>", line 1, in <module>
 [x, x**2 for x in range(6)]
 ^
SyntaxError: invalid syntax
>>> # flatten a list using a listcomp with two 'for'
>>> vec = [[1,2,3], [4,5,6], [7,8,9]]
>>> [num for elem in vec for num in elem]
[1, 2, 3, 4, 5, 6, 7, 8, 9]

列表推导式可以使用复杂的表达式和嵌套函数

>>>

>>> from math import pi
>>> [str(round(pi, i)) for i in range(1, 6)]
['3.1', '3.14', '3.142', '3.1416', '3.14159']

### 5.1.4. 嵌套的列表推导式[](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#nested-list-comprehensions "永久链接至标题")

列表推导式中的初始表达式可以是任何表达式，包括另一个列表推导式。

考虑下面这个 3x4的矩阵，它由3个长度为4的列表组成

>>>

>>> matrix = [
...     [1, 2, 3, 4],
...     [5, 6, 7, 8],
...     [9, 10, 11, 12],
... ]

下面的列表推导式将交换其行和列

>>>

>>> [[row[i] for row in matrix] for i in range(4)]
[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]

如上节所示，嵌套的列表推导式是基于跟随其后的  [`for`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#for)  进行求值的，所以这个例子等价于:

>>>

>>> transposed = []
>>> for i in range(4):
...     transposed.append([row[i] for row in matrix])
...
>>> transposed
[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]

反过来说，也等价于

>>>

>>> transposed = []
>>> for i in range(4):
...     # the following 3 lines implement the nested listcomp
...     transposed_row = []
...     for row in matrix:
...         transposed_row.append(row[i])
...     transposed.append(transposed_row)
...
>>> transposed
[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]

实际应用中，你应该会更喜欢使用内置函数去组成复杂的流程语句。  [`zip()`](https://docs.python.org/zh-cn/3/library/functions.html#zip "zip")  函数将会很好地处理这种情况

>>>

>>> list(zip(*matrix))
[(1, 5, 9), (2, 6, 10), (3, 7, 11), (4, 8, 12)]

关于本行中星号的详细说明，参见  [解包参数列表](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#tut-unpacking-arguments)。

## 5.2. `del`  语句[](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#the-del-statement "永久链接至标题")

有一种方式可以从列表按照给定的索引而不是值来移除一个元素: 那就是  [`del`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#del)  语句。 它不同于会返回一个值的  `pop()`  方法。  `del`  语句也可以用来从列表中移除切片或者清空整个列表（我们之前用过的方式是将一个空列表赋值给指定的切片）。 例如:

>>>

>>> a = [-1, 1, 66.25, 333, 333, 1234.5]
>>> del a[0]
>>> a
[1, 66.25, 333, 333, 1234.5]
>>> del a[2:4]
>>> a
[1, 66.25, 1234.5]
>>> del a[:]
>>> a
[]

[`del`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#del)  也可以删除整个变量

>>>

>>> del a

此后再引用  `a`  时会报错（直到另一个值被赋给它）。我们会在后面了解到  [`del`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#del)  的其他用法。

## 5.3. 元组和序列[](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#tuples-and-sequences "永久链接至标题")

我们看到列表和字符串有很多共同特性，例如索引和切片操作。他们是  _序列_  数据类型（参见  [序列类型 --- list, tuple, range](https://docs.python.org/zh-cn/3/library/stdtypes.html#typesseq)）中的两种。随着 Python 语言的发展，其他的序列类型也会被加入其中。这里介绍另一种标准序列类型:  _元组_。

一个元组由几个被逗号隔开的值组成，例如

>>>

>>> t = 12345, 54321, 'hello!'
>>> t[0]
12345
>>> t
(12345, 54321, 'hello!')
>>> # Tuples may be nested:
... u = t, (1, 2, 3, 4, 5)
>>> u
((12345, 54321, 'hello!'), (1, 2, 3, 4, 5))
>>> # Tuples are immutable:
... t[0] = 88888
Traceback (most recent call last): File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
>>> # but they can contain mutable objects:
... v = ([1, 2, 3], [3, 2, 1])
>>> v
([1, 2, 3], [3, 2, 1])

如你所见，元组在输出时总是被圆括号包围的，以便正确表示嵌套元组。输入时圆括号可有可无，不过经常会是必须的（如果这个元组是一个更大的表达式的一部分）。给元组中的一个单独的元素赋值是不允许的，当然你可以创建包含可变对象的元组，例如列表。

虽然元组可能看起来与列表很像，但它们通常是在不同的场景被使用，并且有着不同的用途。元组是  [immutable](https://docs.python.org/zh-cn/3/glossary.html#term-immutable)  ，其序列通常包含不同种类的元素，并且通过解包（这一节下面会解释）或者索引来访问（如果是  [`namedtuples`](https://docs.python.org/zh-cn/3/library/collections.html#collections.namedtuple "collections.namedtuple")  的话甚至还可以通过属性访问）。列表是  [mutable](https://docs.python.org/zh-cn/3/glossary.html#term-mutable)  ，并且列表中的元素一般是同种类型的，并且通过迭代访问。

一个特殊的问题是构造包含0个或1个元素的元组：为了适应这种情况，语法有一些额外的改变。空元组可以直接被一对空圆括号创建，含有一个元素的元组可以通过在这个元素后添加一个逗号来构建（圆括号里只有一个值的话不够明确）。丑陋，但是有效。例如

>>>

>>> empty = ()
>>> singleton = 'hello',    # <-- note trailing comma
>>> len(empty)
0
>>> len(singleton)
1
>>> singleton
('hello',)

语句  `t  =  12345,  54321,  'hello!'`  是  _元组打包_  的一个例子：值  `12345`,  `54321`  和  `'hello!'`  被打包进元组。其逆操作也是允许的

>>>

>>> x, y, z = t

这被称为  _序列解包_  也是很恰当的，因为解包操作的等号右侧可以是任何序列。序列解包要求等号左侧的变量数与右侧序列里所含的元素数相同。注意多重赋值其实也只是元组打包和序列解包的组合。

## 5.4. 集合[](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#sets "永久链接至标题")

Python也包含有  _集合_  类型。集合是由不重复元素组成的无序的集。它的基本用法包括成员检测和消除重复元素。集合对象也支持像 联合，交集，差集，对称差分等数学运算。

花括号或  [`set()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#set "set")  函数可以用来创建集合。注意：要创建一个空集合你只能用  `set()`  而不能用  `{}`，因为后者是创建一个空字典，这种数据结构我们会在下一节进行讨论。

以下是一些简单的示例

>>>

>>> basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
>>> print(basket)                      # show that duplicates have been removed
{'orange', 'banana', 'pear', 'apple'}
>>> 'orange' in basket                 # fast membership testing
True
>>> 'crabgrass' in basket
False

>>> # Demonstrate set operations on unique letters from two words
...
>>> a = set('abracadabra')
>>> b = set('alacazam')
>>> a                                  # unique letters in a
{'a', 'r', 'b', 'c', 'd'}
>>> a - b                              # letters in a but not in b
{'r', 'd', 'b'}
>>> a | b                              # letters in a or b or both
{'a', 'c', 'r', 'd', 'b', 'm', 'z', 'l'}
>>> a & b                              # letters in both a and b
{'a', 'c'}
>>> a ^ b                              # letters in a or b but not both
{'r', 'd', 'b', 'm', 'z', 'l'}

类似于  [列表推导式](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#tut-listcomps)，集合也支持推导式形式

>>>

>>> a = {x for x in 'abracadabra' if x not in 'abc'}
>>> a
{'r', 'd'}

## 5.5. 字典[](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#dictionaries "永久链接至标题")

另一个非常有用的 Python 內置数据类型是  _字典_  (参见  [映射类型 --- dict](https://docs.python.org/zh-cn/3/library/stdtypes.html#typesmapping))。字典在其他语言里可能会被叫做  _联合内存_  或  _联合数组_。与以连续整数为索引的序列不同，字典是以  _关键字_  为索引的，关键字可以是任意不可变类型，通常是字符串或数字。如果一个元组只包含字符串、数字或元组，那么这个元组也可以用作关键字。但如果元组直接或间接地包含了可变对象，那么它就不能用作关键字。列表不能用作关键字，因为列表可以通过索引、切片或  `append()`  和  `extend()`  之类的方法来改变。

理解字典的最好方式，就是将它看做是一个  _键: 值_  对的集合，键必须是唯一的（在一个字典中）。一对花括号可以创建一个空字典：`{}`  。另一种初始化字典的方式是在一对花括号里放置一些以逗号分隔的键值对，而这也是字典输出的方式。

字典主要的操作是使用关键字存储和解析值。也可以用  `del`  来删除一个键值对。如果你使用了一个已经存在的关键字来存储值，那么之前与这个关键字关联的值就会被遗忘。用一个不存在的键来取值则会报错。

对一个字典执行  `list(d)`  将返回包含该字典中所有键的列表，按插入次序排列 (如需其他排序，则要使用  `sorted(d)`)。要检查字典中是否存在一个特定键，可使用  [`in`](https://docs.python.org/zh-cn/3/reference/expressions.html#in)  关键字。

以下是使用字典的一些简单示例

>>>

>>> tel = {'jack': 4098, 'sape': 4139}
>>> tel['guido'] = 4127
>>> tel
{'jack': 4098, 'sape': 4139, 'guido': 4127}
>>> tel['jack']
4098
>>> del tel['sape']
>>> tel['irv'] = 4127
>>> tel
{'jack': 4098, 'guido': 4127, 'irv': 4127}
>>> list(tel)
['jack', 'guido', 'irv']
>>> sorted(tel)
['guido', 'irv', 'jack']
>>> 'guido' in tel
True
>>> 'jack' not in tel
False

[`dict()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#dict "dict")  构造函数可以直接从键值对序列里创建字典。

>>>

>>> dict([('sape', 4139), ('guido', 4127), ('jack', 4098)])
{'sape': 4139, 'guido': 4127, 'jack': 4098}

此外，字典推导式可以从任意的键值表达式中创建字典

>>>

>>> {x: x**2 for x in (2, 4, 6)}
{2: 4, 4: 16, 6: 36}

当关键字是简单字符串时，有时直接通过关键字参数来指定键值对更方便

>>>

>>> dict(sape=4139, guido=4127, jack=4098)
{'sape': 4139, 'guido': 4127, 'jack': 4098}

## 5.6. 循环的技巧[](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#looping-techniques "永久链接至标题")

当在字典中循环时，用  `items()`  方法可将关键字和对应的值同时取出

>>>

>>> knights = {'gallahad': 'the pure', 'robin': 'the brave'}
>>> for k, v in knights.items():
...     print(k, v)
...
gallahad the pure
robin the brave

当在序列中循环时，用  [`enumerate()`](https://docs.python.org/zh-cn/3/library/functions.html#enumerate "enumerate")  函数可以将索引位置和其对应的值同时取出

>>>

>>> for i, v in enumerate(['tic', 'tac', 'toe']):
...     print(i, v)
...
0 tic
1 tac
2 toe

当同时在两个或更多序列中循环时，可以用  [`zip()`](https://docs.python.org/zh-cn/3/library/functions.html#zip "zip")  函数将其内元素一一匹配。

>>>

>>> questions = ['name', 'quest', 'favorite color']
>>> answers = ['lancelot', 'the holy grail', 'blue']
>>> for q, a in zip(questions, answers):
...     print('What is your {0}?  It is {1}.'.format(q, a))
...
What is your name?  It is lancelot.
What is your quest?  It is the holy grail.
What is your favorite color?  It is blue.

如果要逆向循环一个序列，可以先正向定位序列，然后调用  [`reversed()`](https://docs.python.org/zh-cn/3/library/functions.html#reversed "reversed")  函数

>>>

>>> for i in reversed(range(1, 10, 2)):
...     print(i)
...
9
7
5
3
1

如果要按某个指定顺序循环一个序列，可以用  [`sorted()`](https://docs.python.org/zh-cn/3/library/functions.html#sorted "sorted")  函数，它可以在不改动原序列的基础上返回一个新的排好序的序列

>>>

>>> basket = ['apple', 'orange', 'apple', 'pear', 'orange', 'banana']
>>> for f in sorted(set(basket)):
...     print(f)
...
apple
banana
orange
pear

有时可能会想在循环时修改列表内容，一般来说改为创建一个新列表是比较简单且安全的

>>>

>>> import math
>>> raw_data = [56.2, float('NaN'), 51.7, 55.3, 52.5, float('NaN'), 47.8]
>>> filtered_data = []
>>> for value in raw_data:
...     if not math.isnan(value):
...         filtered_data.append(value)
...
>>> filtered_data
[56.2, 51.7, 55.3, 52.5, 47.8]

## 5.7. 深入条件控制[](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#more-on-conditions "永久链接至标题")

`while`  和  `if`  条件句中可以使用任意操作，而不仅仅是比较操作。

比较操作符  `in`  和  `not  in`  校验一个值是否在（或不在）一个序列里。操作符  `is`  和  `is  not`  比较两个对象是不是同一个对象，这只对像列表这样的可变对象比较重要。所有的比较操作符都有相同的优先级，且这个优先级比数值运算符低。

比较操作可以传递。例如  `a  <  b  ==  c`  会校验是否  `a`  小于  `b`  并且  `b`  等于  `c`。

比较操作可以通过布尔运算符  `and`  和  `or`  来组合，并且比较操作（或其他任何布尔运算）的结果都可以用  `not`  来取反。这些操作符的优先级低于比较操作符；在它们之中，`not`  优先级最高，  `or`  优先级最低，因此  `A  and  not  B  or  C`  等价于  `(A  and  (not  B))  or  C`。和之前一样，你也可以在这种式子里使用圆括号。

布尔运算符  `and`  和  `or`  也被称为  _短路_  运算符：它们的参数从左至右解析，一旦可以确定结果解析就会停止。例如，如果  `A`  和  `C`  为真而  `B`  为假，那么  `A  and  B  and  C`  不会解析  `C`。当用作普通值而非布尔值时，短路操作符的返回值通常是最后一个变量。

也可以把比较操作或者逻辑表达式的结果赋值给一个变量，例如

>>>

>>> string1, string2, string3 = '', 'Trondheim', 'Hammer Dance'
>>> non_null = string1 or string2 or string3
>>> non_null
'Trondheim'

请注意 Python 与 C 不同，在表达式内部赋值必须显式地使用  [海象运算符](https://docs.python.org/zh-cn/3/faq/design.html#why-can-t-i-use-an-assignment-in-an-expression)  `:=`  来完成。 这避免了 C 程序中常见的一种问题：想要在表达式中写  `==`  时却写成了  `=`。

## 5.8. 比较序列和其他类型[](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#comparing-sequences-and-other-types "永久链接至标题")

序列对象通常可以与相同序列类型的其他对象比较。 这种比较使用  _字典式_  顺序：首先比较开头的两个对应元素，如果两者不相等则比较结果就由此确定；如果两者相等则比较之后的两个元素，以此类推，直到有一个序列被耗尽。 如果要比较的两个元素本身又是相同类型的序列，则会递归地执行字典式顺序比较。 如果两个序列中所有的对应元素都相等，则两个序列也将被视为相等。 如果一个序列是另一个的初始子序列，则较短的序列就被视为较小（较少）。 对于字符串来说，字典式顺序是使用 Unicode 码位序号对单个字符排序。 下面是一些相同类型序列之间比较的例子:

(1, 2, 3)              < (1, 2, 4)
[1, 2, 3]              < [1, 2, 4]
'ABC' < 'C' < 'Pascal' < 'Python'
(1, 2, 3, 4)           < (1, 2, 4)
(1, 2)                 < (1, 2, -1)
(1, 2, 3)             == (1.0, 2.0, 3.0)
(1, 2, ('aa', 'ab'))   < (1, 2, ('abc', 'a'), 4)

注意对不同类型对象来说，只要待比较对象提供了合适的比较方法，就可以使用  `<`  和  `>`  来比较。例如，混合数值类型是通过他们的数值进行比较的，所以 0 等于 0.0，等等。否则，解释器将抛出一个  [`TypeError`](https://docs.python.org/zh-cn/3/library/exceptions.html#TypeError "TypeError")  异常，而不是随便给出一个结果。

备注

[1](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#id1)

别的语言可能会返回一个可变对象，他们允许方法连续执行，例如  `d->insert("a")->remove("b")->sort();`。


# 6. 模块[¶](https://docs.python.org/zh-cn/3/tutorial/modules.html#modules "永久链接至标题")

如果你从Python解释器退出并再次进入，之前的定义（函数和变量）都会丢失。因此，如果你想编写一个稍长些的程序，最好使用文本编辑器为解释器准备输入并将该文件作为输入运行。这被称作编写  _脚本_  。随着程序变得越来越长，你或许会想把它拆分成几个文件，以方便维护。你亦或想在不同的程序中使用一个便捷的函数， 而不必把这个函数复制到每一个程序中去。

为支持这些，Python有一种方法可以把定义放在一个文件里，并在脚本或解释器的交互式实例中使用它们。这样的文件被称作  _模块_  ；模块中的定义可以  _导入_  到其它模块或者  _主_  模块（你在顶级和计算器模式下执行的脚本中可以访问的变量集合）。

模块是一个包含Python定义和语句的文件。文件名就是模块名后跟文件后缀  `.py`  。在一个模块内部，模块名（作为一个字符串）可以通过全局变量  `__name__`  的值获得。例如，使用你最喜爱的文本编辑器在当前目录下创建一个名为  `fibo.py`  的文件， 文件中含有以下内容:

# Fibonacci numbers module

def fib(n):    # write Fibonacci series up to n
    a, b = 0, 1
    while a < n:
        print(a, end=' ')
        a, b = b, a+b
    print()

def fib2(n):   # return Fibonacci series up to n
    result = []
    a, b = 0, 1
    while a < n:
        result.append(a)
        a, b = b, a+b
    return result

现在进入Python解释器，并用以下命令导入该模块:

>>>

>>> import fibo

在当前的符号表中，这并不会直接进入到定义在  `fibo`  函数内的名称；它只是进入到模块名  `fibo`  中。你可以用模块名访问这些函数:

>>>

>>> fibo.fib(1000)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987
>>> fibo.fib2(100)
[0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
>>> fibo.__name__
'fibo'

如果你想经常使用某个函数，你可以把它赋值给一个局部变量:

>>>

>>> fib = fibo.fib
>>> fib(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377

## 6.1. 更多有关模块的信息[](https://docs.python.org/zh-cn/3/tutorial/modules.html#more-on-modules "永久链接至标题")

模块可以包含可执行的语句以及函数定义。这些语句用于初始化模块。它们仅在模块  _第一次_  在 import 语句中被导入时才执行。  [1](https://docs.python.org/zh-cn/3/tutorial/modules.html#id2)  (当文件被当作脚本运行时，它们也会执行。)

每个模块都有它自己的私有符号表，该表用作模块中定义的所有函数的全局符号表。因此，模块的作者可以在模块内使用全局变量，而不必担心与用户的全局变量发生意外冲突。另一方面，如果你知道自己在做什么，则可以用跟访问模块内的函数的同样标记方法，去访问一个模块的全局变量，`modname.itemname`。

模块可以导入其它模块。习惯上但不要求把所有  [`import`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#import)  语句放在模块（或脚本）的开头。被导入的模块名存放在调入模块的全局符号表中。

[`import`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#import)  语句有一个变体，它可以把名字从一个被调模块内直接导入到现模块的符号表里。例如:

>>>

>>> from fibo import fib, fib2
>>> fib(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377

这并不会把被调模块名引入到局部变量表里（因此在这个例子里，`fibo`  是未被定义的）。

还有一个变体甚至可以导入模块内定义的所有名称:

>>>

>>> from fibo import *
>>> fib(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377

这会调入所有非以下划线（`_`）开头的名称。 在多数情况下，Python程序员都不会使用这个功能，因为它在解释器中引入了一组未知的名称，而它们很可能会覆盖一些你已经定义过的东西。

注意通常情况下从一个模块或者包内调入  `*`  的做法是不太被接受的， 因为这通常会导致代码的可读性很差。不过，在交互式编译器中为了节省打字可以这么用。

如果模块名称之后带有  `as`，则跟在  `as`  之后的名称将直接绑定到所导入的模块。

>>>

>>> import fibo as fib
>>> fib.fib(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377

这会和  `import  fibo`  方式一样有效地调入模块， 唯一的区别是它以  `fib`  的名称存在的。

这种方式也可以在用到  [`from`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#from)  的时候使用，并会有类似的效果:

>>>

>>> from fibo import fib as fibonacci
>>> fibonacci(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377

注解

出于效率的考虑，每个模块在每个解释器会话中只被导入一次。因此，如果你更改了你的模块，则必须重新启动解释器， 或者，如果它只是一个要交互式地测试的模块，请使用  [`importlib.reload()`](https://docs.python.org/zh-cn/3/library/importlib.html#importlib.reload "importlib.reload")，例如  `import  importlib;  importlib.reload(modulename)`。

### 6.1.1. 以脚本的方式执行模块[](https://docs.python.org/zh-cn/3/tutorial/modules.html#executing-modules-as-scripts "永久链接至标题")

当你用下面方式运行一个Python模块:

python fibo.py <arguments>

模块里的代码会被执行，就好像你导入了模块一样，但是  `__name__`  被赋值为  `"__main__"`。 这意味着通过在你的模块末尾添加这些代码:

if __name__ == "__main__":
    import sys
    fib(int(sys.argv[1]))

你既可以把这个文件当作脚本又可当作一个可调入的模块来使用， 因为那段解析命令行的代码只有在当模块是以“main”文件的方式执行的时候才会运行:

$ python fibo.py 50
0 1 1 2 3 5 8 13 21 34

如果模块是被导入的，那些代码是不运行的:

>>>

>>> import fibo
>>>

这经常用于为模块提供一个方便的用户接口，或用于测试（以脚本的方式运行模块从而执行一些测试套件）。

### 6.1.2. 模块搜索路径[](https://docs.python.org/zh-cn/3/tutorial/modules.html#the-module-search-path "永久链接至标题")

当一个名为  `spam`  的模块被导入的时候，解释器首先寻找具有该名称的内置模块。如果没有找到，然后解释器从  [`sys.path`](https://docs.python.org/zh-cn/3/library/sys.html#sys.path "sys.path")  变量给出的目录列表里寻找名为  `spam.py`  的文件。[`sys.path`](https://docs.python.org/zh-cn/3/library/sys.html#sys.path "sys.path")  初始有这些目录地址:

-   包含输入脚本的目录（或者未指定文件时的当前目录）。
    
-   [`PYTHONPATH`](https://docs.python.org/zh-cn/3/using/cmdline.html#envvar-PYTHONPATH)  （一个包含目录名称的列表，它和shell变量  `PATH`  有一样的语法）。
    
-   取决于安装的默认设置
    

注解

在支持符号链接的文件系统上，包含输入脚本的目录是在追加符号链接后才计算出来的。换句话说，包含符号链接的目录并  **没有**  被添加到模块的搜索路径上。

在初始化后，Python程序可以更改  [`sys.path`](https://docs.python.org/zh-cn/3/library/sys.html#sys.path "sys.path")。包含正在运行脚本的文件目录被放在搜索路径的开头处， 在标准库路径之前。这意味着将加载此目录里的脚本，而不是标准库中的同名模块。 除非有意更换，否则这是错误。更多信息请参阅  [标准模块](https://docs.python.org/zh-cn/3/tutorial/modules.html#tut-standardmodules)。

### 6.1.3. “编译过的”Python文件[](https://docs.python.org/zh-cn/3/tutorial/modules.html#compiled-python-files "永久链接至标题")

为了加速模块载入，Python在  `__pycache__`  目录里缓存了每个模块的编译后版本，名称为  `module._version_.pyc`  ，其中名称中的版本字段对编译文件的格式进行编码； 它一般使用Python版本号。例如，在CPython版本3.3中，spam.py的编译版本将被缓存为  `__pycache__/spam.cpython-33.pyc`。此命名约定允许来自不同发行版和不同版本的Python的已编译模块共存。

Python根据编译版本检查源的修改日期，以查看它是否已过期并需要重新编译。这是一个完全自动化的过程。此外，编译的模块与平台无关，因此可以在具有不同体系结构的系统之间共享相同的库。

Python在两种情况下不会检查缓存。首先，对于从命令行直接载入的模块，它从来都是重新编译并且不存储编译结果；其次，如果没有源模块，它不会检查缓存。为了支持无源文件（仅编译）发行版本， 编译模块必须是在源目录下，并且绝对不能有源模块。

给专业人士的一些小建议:

-   你可以在Python命令中使用  [`-O`](https://docs.python.org/zh-cn/3/using/cmdline.html#cmdoption-o)  或者  [`-OO`](https://docs.python.org/zh-cn/3/using/cmdline.html#cmdoption-oo)  开关， 以减小编译后模块的大小。  `-O`  开关去除断言语句，`-OO`  开关同时去除断言语句和 __doc__ 字符串。由于有些程序可能依赖于这些，你应当只在清楚自己在做什么时才使用这个选项。“优化过的”模块有一个  `opt-`  标签并且通常小些。将来的发行版本或许会更改优化的效果。
    
-   一个从  `.pyc`  文件读出的程序并不会比它从  `.py`  读出时运行的更快，`.pyc`  文件唯一快的地方在于载入速度。
    
-   [`compileall`](https://docs.python.org/zh-cn/3/library/compileall.html#module-compileall "compileall: Tools for byte-compiling all Python source files in a directory tree.")  模块可以为一个目录下的所有模块创建.pyc文件。
    
-   关于这个过程，[**PEP 3147**](https://www.python.org/dev/peps/pep-3147)  中有更多细节，包括一个决策流程图。
    

## 6.2. 标准模块[](https://docs.python.org/zh-cn/3/tutorial/modules.html#standard-modules "永久链接至标题")

Python附带了一个标准模块库，在单独的文档Python库参考（以下称为“库参考”）中进行了描述。一些模块内置于解释器中；它们提供对不属于语言核心但仍然内置的操作的访问，以提高效率或提供对系统调用等操作系统原语的访问。这些模块的集合是一个配置选项，它也取决于底层平台。例如，[`winreg`](https://docs.python.org/zh-cn/3/library/winreg.html#module-winreg "winreg: Routines and objects for manipulating the Windows registry. (Windows)")  模块只在Windows操作系统上提供。一个特别值得注意的模块  [`sys`](https://docs.python.org/zh-cn/3/library/sys.html#module-sys "sys: Access system-specific parameters and functions.")，它被内嵌到每一个Python解释器中。变量  `sys.ps1`  和  `sys.ps2`  定义用作主要和辅助提示的字符串:

>>>

>>> import sys
>>> sys.ps1
'>>> '
>>> sys.ps2
'... '
>>> sys.ps1 = 'C> '
C> print('Yuck!')
Yuck!
C>

这两个变量只有在编译器是交互模式下才被定义。

`sys.path`  变量是一个字符串列表，用于确定解释器的模块搜索路径。该变量被初始化为从环境变量  [`PYTHONPATH`](https://docs.python.org/zh-cn/3/using/cmdline.html#envvar-PYTHONPATH)  获取的默认路径，或者如果  [`PYTHONPATH`](https://docs.python.org/zh-cn/3/using/cmdline.html#envvar-PYTHONPATH)  未设置，则从内置默认路径初始化。你可以使用标准列表操作对其进行修改:

>>>

>>> import sys
>>> sys.path.append('/ufs/guido/lib/python')

## 6.3. [`dir()`](https://docs.python.org/zh-cn/3/library/functions.html#dir "dir")  函数[](https://docs.python.org/zh-cn/3/tutorial/modules.html#the-dir-function "永久链接至标题")

内置函数  [`dir()`](https://docs.python.org/zh-cn/3/library/functions.html#dir "dir")  用于查找模块定义的名称。 它返回一个排序过的字符串列表:

>>>

>>> import fibo, sys
>>> dir(fibo)
['__name__', 'fib', 'fib2']
>>> dir(sys)  
['__displayhook__', '__doc__', '__excepthook__', '__loader__', '__name__',
 '__package__', '__stderr__', '__stdin__', '__stdout__',
 '_clear_type_cache', '_current_frames', '_debugmallocstats', '_getframe',
 '_home', '_mercurial', '_xoptions', 'abiflags', 'api_version', 'argv',
 'base_exec_prefix', 'base_prefix', 'builtin_module_names', 'byteorder',
 'call_tracing', 'callstats', 'copyright', 'displayhook',
 'dont_write_bytecode', 'exc_info', 'excepthook', 'exec_prefix',
 'executable', 'exit', 'flags', 'float_info', 'float_repr_style',
 'getcheckinterval', 'getdefaultencoding', 'getdlopenflags',
 'getfilesystemencoding', 'getobjects', 'getprofile', 'getrecursionlimit',
 'getrefcount', 'getsizeof', 'getswitchinterval', 'gettotalrefcount',
 'gettrace', 'hash_info', 'hexversion', 'implementation', 'int_info',
 'intern', 'maxsize', 'maxunicode', 'meta_path', 'modules', 'path',
 'path_hooks', 'path_importer_cache', 'platform', 'prefix', 'ps1',
 'setcheckinterval', 'setdlopenflags', 'setprofile', 'setrecursionlimit',
 'setswitchinterval', 'settrace', 'stderr', 'stdin', 'stdout',
 'thread_info', 'version', 'version_info', 'warnoptions']

如果没有参数，[`dir()`](https://docs.python.org/zh-cn/3/library/functions.html#dir "dir")  会列出你当前定义的名称:

>>>

>>> a = [1, 2, 3, 4, 5]
>>> import fibo
>>> fib = fibo.fib
>>> dir()
['__builtins__', '__name__', 'a', 'fib', 'fibo', 'sys']

注意：它列出所有类型的名称：变量，模块，函数，等等。

[`dir()`](https://docs.python.org/zh-cn/3/library/functions.html#dir "dir")  不会列出内置函数和变量的名称。如果你想要这些，它们的定义是在标准模块  [`builtins`](https://docs.python.org/zh-cn/3/library/builtins.html#module-builtins "builtins: The module that provides the built-in namespace.")  中:

>>>

>>> import builtins
>>> dir(builtins)  
['ArithmeticError', 'AssertionError', 'AttributeError', 'BaseException',
 'BlockingIOError', 'BrokenPipeError', 'BufferError', 'BytesWarning',
 'ChildProcessError', 'ConnectionAbortedError', 'ConnectionError',
 'ConnectionRefusedError', 'ConnectionResetError', 'DeprecationWarning',
 'EOFError', 'Ellipsis', 'EnvironmentError', 'Exception', 'False',
 'FileExistsError', 'FileNotFoundError', 'FloatingPointError',
 'FutureWarning', 'GeneratorExit', 'IOError', 'ImportError',
 'ImportWarning', 'IndentationError', 'IndexError', 'InterruptedError',
 'IsADirectoryError', 'KeyError', 'KeyboardInterrupt', 'LookupError',
 'MemoryError', 'NameError', 'None', 'NotADirectoryError', 'NotImplemented',
 'NotImplementedError', 'OSError', 'OverflowError',
 'PendingDeprecationWarning', 'PermissionError', 'ProcessLookupError',
 'ReferenceError', 'ResourceWarning', 'RuntimeError', 'RuntimeWarning',
 'StopIteration', 'SyntaxError', 'SyntaxWarning', 'SystemError',
 'SystemExit', 'TabError', 'TimeoutError', 'True', 'TypeError',
 'UnboundLocalError', 'UnicodeDecodeError', 'UnicodeEncodeError',
 'UnicodeError', 'UnicodeTranslateError', 'UnicodeWarning', 'UserWarning',
 'ValueError', 'Warning', 'ZeroDivisionError', '_', '__build_class__',
 '__debug__', '__doc__', '__import__', '__name__', '__package__', 'abs',
 'all', 'any', 'ascii', 'bin', 'bool', 'bytearray', 'bytes', 'callable',
 'chr', 'classmethod', 'compile', 'complex', 'copyright', 'credits',
 'delattr', 'dict', 'dir', 'divmod', 'enumerate', 'eval', 'exec', 'exit',
 'filter', 'float', 'format', 'frozenset', 'getattr', 'globals', 'hasattr',
 'hash', 'help', 'hex', 'id', 'input', 'int', 'isinstance', 'issubclass',
 'iter', 'len', 'license', 'list', 'locals', 'map', 'max', 'memoryview',
 'min', 'next', 'object', 'oct', 'open', 'ord', 'pow', 'print', 'property',
 'quit', 'range', 'repr', 'reversed', 'round', 'set', 'setattr', 'slice',
 'sorted', 'staticmethod', 'str', 'sum', 'super', 'tuple', 'type', 'vars',
 'zip']

## 6.4. 包[](https://docs.python.org/zh-cn/3/tutorial/modules.html#packages "永久链接至标题")

包是一种通过用“带点号的模块名”来构造 Python 模块命名空间的方法。 例如，模块名  `A.B`  表示  `A`  包中名为  `B`  的子模块。正如模块的使用使得不同模块的作者不必担心彼此的全局变量名称一样，使用加点的模块名可以使得 NumPy 或 Pillow 等多模块软件包的作者不必担心彼此的模块名称一样。

假设你想为声音文件和声音数据的统一处理，设计一个模块集合（一个“包”）。由于存在很多不同的声音文件格式（通常由它们的扩展名来识别，例如：`.wav`，  `.aiff`，  `.au`），因此为了不同文件格式间的转换，你可能需要创建和维护一个不断增长的模块集合。 你可能还想对声音数据还做很多不同的处理（例如，混声，添加回声，使用均衡器功能，创造人工立体声效果）， 因此为了实现这些处理，你将另外写一个无穷尽的模块流。这是你的包的可能结构（以分层文件系统的形式表示）：

sound/                          Top-level package
      __init__.py               Initialize the sound package
      formats/                  Subpackage for file format conversions
              __init__.py
              wavread.py
              wavwrite.py
              aiffread.py
              aiffwrite.py
              auread.py
              auwrite.py
              ...
      effects/                  Subpackage for sound effects
              __init__.py
              echo.py
              surround.py
              reverse.py
              ...
      filters/                  Subpackage for filters
              __init__.py
              equalizer.py
              vocoder.py
              karaoke.py
              ...

当导入这个包时，Python搜索  `sys.path`  里的目录，查找包的子目录。

必须要有  `__init__.py`  文件才能让 Python 将包含该文件的目录当作包。 这样可以防止具有通常名称例如  `string`  的目录在无意中隐藏稍后在模块搜索路径上出现的有效模块。 在最简单的情况下，`__init__.py`  可以只是一个空文件，但它也可以执行包的初始化代码或设置  `__all__`  变量，具体将在后文介绍。

包的用户可以从包中导入单个模块，例如:

import sound.effects.echo

这会加载子模块  `sound.effects.echo`  。但引用它时必须使用它的全名。

sound.effects.echo.echofilter(input, output, delay=0.7, atten=4)

导入子模块的另一种方法是

from sound.effects import echo

这也会加载子模块  `echo`  ，并使其在没有包前缀的情况下可用，因此可以按如下方式使用:

echo.echofilter(input, output, delay=0.7, atten=4)

另一种形式是直接导入所需的函数或变量:

from sound.effects.echo import echofilter

同样，这也会加载子模块  `echo`，但这会使其函数  `echofilter()`  直接可用:

echofilter(input, output, delay=0.7, atten=4)

请注意，当使用  `from  package  import  item`  时，item可以是包的子模块（或子包），也可以是包中定义的其他名称，如函数，类或变量。  `import`  语句首先测试是否在包中定义了item；如果没有，它假定它是一个模块并尝试加载它。如果找不到它，则引发  [`ImportError`](https://docs.python.org/zh-cn/3/library/exceptions.html#ImportError "ImportError")  异常。

相反，当使用  `import  item.subitem.subsubitem`  这样的语法时，除了最后一项之外的每一项都必须是一个包；最后一项可以是模块或包，但不能是前一项中定义的类或函数或变量。

### 6.4.1. 从包中导入 *[](https://docs.python.org/zh-cn/3/tutorial/modules.html#importing-from-a-package "永久链接至标题")

当用户写  `from  sound.effects  import  *`  会发生什么？理想情况下，人们希望这会以某种方式传递给文件系统，找到包中存在哪些子模块，并将它们全部导入。这可能需要很长时间，导入子模块可能会产生不必要的副作用，这种副作用只有在显式导入子模块时才会发生。

唯一的解决方案是让包作者提供一个包的显式索引。[`import`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#import)  语句使用下面的规范：如果一个包的  `__init__.py`  代码定义了一个名为  `__all__`  的列表，它会被视为在遇到  `from  package  import  *`  时应该导入的模块名列表。在发布该包的新版本时，包作者可以决定是否让此列表保持更新。包作者如果认为从他们的包中导入 * 的操作没有必要被使用，也可以决定不支持此列表。例如，文件  `sound/effects/__init__.py`  可以包含以下代码:

__all__ = ["echo", "surround", "reverse"]

这意味着  `from  sound.effects  import  *`  将导入  `sound`  包的三个命名子模块。

如果没有定义  `__all__`，`from  sound.effects  import  *`  语句  _不会_  从包  `sound.effects`  中导入所有子模块到当前命名空间；它只确保导入了包  `sound.effects`  （可能运行任何在  `__init__.py`  中的初始化代码），然后导入包中定义的任何名称。 这包括  `__init__.py`  定义的任何名称（以及显式加载的子模块）。它还包括由之前的  [`import`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#import)  语句显式加载的包的任何子模块。思考下面的代码:

import sound.effects.echo
import sound.effects.surround
from sound.effects import *

在这个例子中，  `echo`  和  `surround`  模块是在执行  `from...import`  语句时导入到当前命名空间中的，因为它们定义在  `sound.effects`  包中。（这在定义了  `__all__`  时也有效。）

虽然某些模块被设计为在使用  `import  *`  时只导出遵循某些模式的名称，但在生产代码中它仍然被认为是不好的做法。

请记住，使用  `from  package  import  specific_submodule`  没有任何问题！ 实际上，除非导入的模块需要使用来自不同包的同名子模块，否则这是推荐的表示法。

### 6.4.2. 子包参考[](https://docs.python.org/zh-cn/3/tutorial/modules.html#intra-package-references "永久链接至标题")

当包被构造成子包时（与示例中的  `sound`  包一样），你可以使用绝对导入来引用兄弟包的子模块。例如，如果模块  `sound.filters.vocoder`  需要在  `sound.effects`  包中使用  `echo`  模块，它可以使用  `from  sound.effects  import  echo`  。

你还可以使用import语句的  `from  module  import  name`  形式编写相对导入。这些导入使用前导点来指示相对导入中涉及的当前包和父包。例如，从  `surround`  模块，你可以使用:

from . import echo
from .. import formats
from ..filters import equalizer

请注意，相对导入是基于当前模块的名称进行导入的。由于主模块的名称总是  `"__main__"`  ，因此用作Python应用程序主模块的模块必须始终使用绝对导入。

### 6.4.3. 多个目录中的包[](https://docs.python.org/zh-cn/3/tutorial/modules.html#packages-in-multiple-directories "永久链接至标题")

包支持另一个特殊属性，  [`__path__`](https://docs.python.org/zh-cn/3/reference/import.html#__path__ "__path__")  。它被初始化为一个列表，其中包含在执行该文件中的代码之前保存包的文件  `__init__.py`  的目录的名称。这个变量可以修改；这样做会影响将来对包中包含的模块和子包的搜索。

虽然通常不需要此功能，但它可用于扩展程序包中的模块集。

备注

[1](https://docs.python.org/zh-cn/3/tutorial/modules.html#id1)

实际上，函数定义也是“被执行”的“语句”；模块级函数定义的执行在模块的全局符号表中输入该函数名。


# 7. 输入输出[¶](https://docs.python.org/zh-cn/3/tutorial/inputoutput.html#input-and-output "永久链接至标题")

有几种方法可以显示程序的输出；数据可以以人类可读的形式打印出来，或者写入文件以供将来使用。本章将讨论一些可能性。

## 7.1. 更漂亮的输出格式[](https://docs.python.org/zh-cn/3/tutorial/inputoutput.html#fancier-output-formatting "永久链接至标题")

到目前为止，我们遇到了两种写入值的方法：_表达式语句_  和  [`print()`](https://docs.python.org/zh-cn/3/library/functions.html#print "print")  函数。（第三种是使用文件对象的  `write()`  方法；标准输出文件可以作为  `sys.stdout`  引用。更多相关信息可参考标准库指南。）

通常，你需要更多地控制输出的格式，而不仅仅是打印空格分隔的值。有几种格式化输出的方法。

-   要使用  [格式化字符串字面值](https://docs.python.org/zh-cn/3/tutorial/inputoutput.html#tut-f-strings)  ，请在字符串的开始引号或三引号之前加上一个  `f`  或  `F`  。在此字符串中，你可以在  `{`  和  `}`  字符之间写可以引用的变量或字面值的 Python 表达式。
    
    >>>
    
    >>> year = 2016
    >>> event = 'Referendum'
    >>> f'Results of the {year}  {event}'
    'Results of the 2016 Referendum'
    
-   字符串的  [`str.format()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.format "str.format")  方法需要更多的手动操作。你仍将使用  `{`  和  `}`  来标记变量将被替换的位置，并且可以提供详细的格式化指令，但你还需要提供要格式化的信息。
    
    >>>
    
    >>> yes_votes = 42_572_654
    >>> no_votes = 43_132_495
    >>> percentage = yes_votes / (yes_votes + no_votes)
    >>> '{:-9} YES votes {:2.2%}'.format(yes_votes, percentage)
    ' 42572654 YES votes  49.67%'
    
-   最后，你可以使用字符串切片和连接操作自己完成所有的字符串处理，以创建你可以想象的任何布局。字符串类型有一些方法可以执行将字符串填充到给定列宽的有用操作。
    

当你不需要花哨的输出而只是想快速显示某些变量以进行调试时，可以使用  [`repr()`](https://docs.python.org/zh-cn/3/library/functions.html#repr "repr")  or  [`str()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str "str") 函数将任何值转化为字符串。

[`str()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str "str")  函数是用于返回人类可读的值的表示，而  [`repr()`](https://docs.python.org/zh-cn/3/library/functions.html#repr "repr")  是用于生成解释器可读的表示（如果没有等效的语法，则会强制执行  [`SyntaxError`](https://docs.python.org/zh-cn/3/library/exceptions.html#SyntaxError "SyntaxError")）对于没有人类可读性的表示的对象，  [`str()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str "str")  将返回和  [`repr()`](https://docs.python.org/zh-cn/3/library/functions.html#repr "repr")  一样的值。很多值使用任一函数都具有相同的表示，比如数字或类似列表和字典的结构。特殊的是字符串有两个不同的表示。

几个例子:

>>>

>>> s = 'Hello, world.'
>>> str(s)
'Hello, world.'
>>> repr(s)
"'Hello, world.'"
>>> str(1/7)
'0.14285714285714285'
>>> x = 10 * 3.25
>>> y = 200 * 200
>>> s = 'The value of x is ' + repr(x) + ', and y is ' + repr(y) + '...'
>>> print(s)
The value of x is 32.5, and y is 40000...
>>> # The repr() of a string adds string quotes and backslashes:
... hello = 'hello, world\n'
>>> hellos = repr(hello)
>>> print(hellos)
'hello, world\n'
>>> # The argument to repr() may be any Python object:
... repr((x, y, ('spam', 'eggs')))
"(32.5, 40000, ('spam', 'eggs'))"

[`string`](https://docs.python.org/zh-cn/3/library/string.html#module-string "string: Common string operations.")  模块包含一个  [`Template`](https://docs.python.org/zh-cn/3/library/string.html#string.Template "string.Template")  类，它提供了另一种将值替换为字符串的方法，使用类似  `$x`  的占位符并用字典中的值替换它们，但对格式的控制要少的多。

### 7.1.1. 格式化字符串文字[](https://docs.python.org/zh-cn/3/tutorial/inputoutput.html#formatted-string-literals "永久链接至标题")

[格式化字符串字面值](https://docs.python.org/zh-cn/3/reference/lexical_analysis.html#f-strings)  （常简称为 f-字符串）能让你在字符串前加上  `f`  和  `F`  并将表达式写成  `{expression}`  来在字符串中包含 Python 表达式的值。

可选的格式说明符可以跟在表达式后面。这样可以更好地控制值的格式化方式。以下示例将pi舍入到小数点后三位:

>>>

>>> import math
>>> print(f'The value of pi is approximately {math.pi:.3f}.')
The value of pi is approximately 3.142.

在  `':'`  后传递一个整数可以让该字段成为最小字符宽度。这在使列对齐时很有用。:

>>>

>>> table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 7678}
>>> for name, phone in table.items():
...     print(f'{name:10} ==> {phone:10d}')
...
Sjoerd     ==>       4127
Jack       ==>       4098
Dcab       ==>       7678

其他的修饰符可用于在格式化之前转化值。  `'!a'`  应用  [`ascii()`](https://docs.python.org/zh-cn/3/library/functions.html#ascii "ascii")  ，`'!s'`  应用  [`str()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str "str")，还有  `'!r'`  应用  [`repr()`](https://docs.python.org/zh-cn/3/library/functions.html#repr "repr"):

>>>

>>> animals = 'eels'
>>> print(f'My hovercraft is full of {animals}.')
My hovercraft is full of eels.
>>> print(f'My hovercraft is full of {animals!r}.')
My hovercraft is full of 'eels'.

有关这些格式规范的参考，请参阅参考指南  [格式规格迷你语言](https://docs.python.org/zh-cn/3/library/string.html#formatspec)。

### 7.1.2. 字符串的 format() 方法[](https://docs.python.org/zh-cn/3/tutorial/inputoutput.html#the-string-format-method "永久链接至标题")

[`str.format()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.format "str.format")  方法的基本用法如下所示:

>>>

>>> print('We are the {} who say "{}!"'.format('knights', 'Ni'))
We are the knights who say "Ni!"

花括号和其中的字符（称为格式字段）将替换为传递给  [`str.format()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.format "str.format")  方法的对象。花括号中的数字可用来表示传递给  [`str.format()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.format "str.format")  方法的对象的位置。

>>>

>>> print('{0} and {1}'.format('spam', 'eggs'))
spam and eggs
>>> print('{1} and {0}'.format('spam', 'eggs'))
eggs and spam

如果在  [`str.format()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.format "str.format")  方法中使用关键字参数，则使用参数的名称引用它们的值。:

>>>

>>> print('This {food} is {adjective}.'.format(
...       food='spam', adjective='absolutely horrible'))
This spam is absolutely horrible.

位置和关键字参数可以任意组合:

>>>

>>> print('The story of {0}, {1}, and {other}.'.format('Bill', 'Manfred',
 other='Georg'))
The story of Bill, Manfred, and Georg.

如果你有一个非常长的格式字符串，你不想把它拆开，那么你最好是按名称而不是按位置引用变量来进行格式化。 这可以通过简单地传递字典并使用方括号  `'[]'`  访问键来完成。

>>>

>>> table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
>>> print('Jack: {0[Jack]:d}; Sjoerd: {0[Sjoerd]:d}; '
...       'Dcab: {0[Dcab]:d}'.format(table))
Jack: 4098; Sjoerd: 4127; Dcab: 8637678

这也可以通过使用 '**' 符号将 table 作为关键字参数传递。

>>>

>>> table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
>>> print('Jack: {Jack:d}; Sjoerd: {Sjoerd:d}; Dcab: {Dcab:d}'.format(**table))
Jack: 4098; Sjoerd: 4127; Dcab: 8637678

这在与内置函数  [`vars()`](https://docs.python.org/zh-cn/3/library/functions.html#vars "vars")  结合使用时非常有用，它会返回包含所有局部变量的字典。

例如，下面几行代码生成一组整齐的列，其中包含给定的整数和它的平方以及立方:

>>>

>>> for x in range(1, 11):
...     print('{0:2d}  {1:3d}  {2:4d}'.format(x, x*x, x*x*x))
...
 1   1    1
 2   4    8
 3   9   27
 4  16   64
 5  25  125
 6  36  216
 7  49  343
 8  64  512
 9  81  729
10 100 1000

关于使用  [`str.format()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.format "str.format")  进行字符串格式化的完整概述，请参阅  [格式字符串语法](https://docs.python.org/zh-cn/3/library/string.html#formatstrings)  。

### 7.1.3. 手动格式化字符串[](https://docs.python.org/zh-cn/3/tutorial/inputoutput.html#manual-string-formatting "永久链接至标题")

这是同一个平方和立方的表，手动格式化的:

>>>

>>> for x in range(1, 11):
...     print(repr(x).rjust(2), repr(x*x).rjust(3), end=' ')
...     # Note use of 'end' on previous line
...     print(repr(x*x*x).rjust(4))
...
 1   1    1
 2   4    8
 3   9   27
 4  16   64
 5  25  125
 6  36  216
 7  49  343
 8  64  512
 9  81  729
10 100 1000

（注意每列之间的一个空格是通过使用  [`print()`](https://docs.python.org/zh-cn/3/library/functions.html#print "print")  的方式添加的：它总是在其参数间添加空格。）

字符串对象的  [`str.rjust()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.rjust "str.rjust")  方法通过在左侧填充空格来对给定宽度的字段中的字符串进行右对齐。类似的方法还有  [`str.ljust()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.ljust "str.ljust")  和  [`str.center()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.center "str.center")  。这些方法不会写入任何东西，它们只是返回一个新的字符串，如果输入的字符串太长，它们不会截断字符串，而是原样返回；这虽然会弄乱你的列布局，但这通常比另一种方法好，后者会在显示值时可能不准确（如果你真的想截断，你可以添加一个切片操作，例如  `x.ljust(n)[:n]`  。）

还有另外一个方法，[`str.zfill()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.zfill "str.zfill")  ，它会在数字字符串的左边填充零。它能识别正负号:

>>>

>>> '12'.zfill(5)
'00012'
>>> '-3.14'.zfill(7)
'-003.14'
>>> '3.14159265359'.zfill(5)
'3.14159265359'

### 7.1.4. 旧的字符串格式化方法[](https://docs.python.org/zh-cn/3/tutorial/inputoutput.html#old-string-formatting "永久链接至标题")

% 运算符（求余）也可用于字符串格式化。 给定  `'string'  %  values`，则  `string`  中的  `%`  实例会以零个或多个  `values`  元素替换。 此操作通常被称为字符串插值。 例如:

>>>

>>> import math
>>> print('The value of pi is approximately %5.3f.' % math.pi)
The value of pi is approximately 3.142.

可在  [printf 风格的字符串格式化](https://docs.python.org/zh-cn/3/library/stdtypes.html#old-string-formatting)  部分找到更多信息。

## 7.2. 读写文件[](https://docs.python.org/zh-cn/3/tutorial/inputoutput.html#reading-and-writing-files "永久链接至标题")

[`open()`](https://docs.python.org/zh-cn/3/library/functions.html#open "open")  返回一个  [file object](https://docs.python.org/zh-cn/3/glossary.html#term-file-object)，最常用的有两个参数：  `open(filename,  mode)`。

>>>

>>> f = open('workfile', 'w')

第一个参数是包含文件名的字符串。第二个参数是另一个字符串，其中包含一些描述文件使用方式的字符。_mode_  可以是  `'r'`  ，表示文件只能读取，`'w'`  表示只能写入（已存在的同名文件会被删除），还有  `'a'`  表示打开文件以追加内容；任何写入的数据会自动添加到文件的末尾。`'r+'`  表示打开文件进行读写。_mode_  参数是可选的；省略时默认为  `'r'`。

通常文件是以  _text mode_  打开的，这意味着从文件中读取或写入字符串时，都会以指定的编码方式进行编码。如果未指定编码格式，默认值与平台相关 (参见  [`open()`](https://docs.python.org/zh-cn/3/library/functions.html#open "open"))。在mode 中追加的  `'b'`  则以  _binary mode_  打开文件：现在数据是以字节对象的形式进行读写的。这个模式应该用于所有不包含文本的文件。

在文本模式下读取时，默认会把平台特定的行结束符 (Unix 上的  `\n`, Windows 上的  `\r\n`) 转换为  `\n`。在文本模式下写入时，默认会把出现的  `\n`  转换回平台特定的结束符。这样在幕后修改文件数据对文本文件来说没有问题，但是会破坏二进制数据例如  `JPEG`  或  `EXE`  文件中的数据。请一定要注意在读写此类文件时应使用二进制模式。

在处理文件对象时，最好使用  [`with`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#with)  关键字。 优点是当子句体结束后文件会正确关闭，即使在某个时刻引发了异常。 而且使用  `with`  相比等效的  [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try)-[`finally`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#finally)  代码块要简短得多:

>>>

>>> with open('workfile') as f:
...     read_data = f.read()

>>> # We can check that the file has been automatically closed.
>>> f.closed
True

如果你没有使用  [`with`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#with)  关键字，那么你应该调用  `f.close()`  来关闭文件并立即释放它使用的所有系统资源。如果你没有显式地关闭文件，Python的垃圾回收器最终将销毁该对象并为你关闭打开的文件，但这个文件可能会保持打开状态一段时间。另外一个风险是不同的Python实现会在不同的时间进行清理。

通过  [`with`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#with)  语句或者调用  `f.close()`  关闭文件对象后，尝试使用该文件对象将自动失败。:

>>>

>>> f.close()
>>> f.read()
Traceback (most recent call last): File "<stdin>", line 1, in <module>
ValueError: I/O operation on closed file.

### 7.2.1. 文件对象的方法[](https://docs.python.org/zh-cn/3/tutorial/inputoutput.html#methods-of-file-objects "永久链接至标题")

本节中剩下的例子将假定你已创建名为  `f`  的文件对象。

要读取文件内容，请调用  `f.read(size)`，它会读取一些数据并将其作为字符串（在文本模式下）或字节串对象（在二进制模式下）返回。  _size_  是一个可选的数值参数。 当  _size_  被省略或者为负数时，将读取并返回整个文件的内容；如果文件的大小是你的机器内存的两倍就会出现问题。 当取其他值时，将读取并返回至多  _size_  个字符（在文本模式下）或  _size_  个字节（在二进制模式下）。 如果已到达文件末尾，`f.read()`  将返回一个空字符串 (`''`)。

>>>

>>> f.read()
'This is the entire file.\n'
>>> f.read()
''

`f.readline()`  从文件中读取一行；换行符（`\n`）留在字符串的末尾，如果文件不以换行符结尾，则在文件的最后一行省略。这使得返回值明确无误；如果  `f.readline()`  返回一个空的字符串，则表示已经到达了文件末尾，而空行使用  `'\n'`  表示，该字符串只包含一个换行符。:

>>>

>>> f.readline()
'This is the first line of the file.\n'
>>> f.readline()
'Second line of the file\n'
>>> f.readline()
''

要从文件中读取行，你可以循环遍历文件对象。这是内存高效，快速的，并简化代码:

>>>

>>> for line in f:
...     print(line, end='')
...
This is the first line of the file.
Second line of the file

如果你想以列表的形式读取文件中的所有行，你也可以使用  `list(f)`  或  `f.readlines()`。

`f.write(string)`  会把  _string_  的内容写入到文件中，并返回写入的字符数。:

>>>

>>> f.write('This is a test\n')
15

在写入其他类型的对象之前，需要先把它们转化为字符串（在文本模式下）或者字节对象（在二进制模式下）:

>>>

>>> value = ('the answer', 42)
>>> s = str(value)  # convert the tuple to string
>>> f.write(s)
18

`f.tell()`  返回一个整数，给出文件对象在文件中的当前位置，表示为二进制模式下时从文件开始的字节数，以及文本模式下的意义不明的数字。

要改变文件对象的位置，请使用  `f.seek(offset,  whence)`。 通过向一个参考点添加  _offset_  来计算位置；参考点由  _whence_  参数指定。  _whence_  的 0 值表示从文件开头起算，1 表示使用当前文件位置，2 表示使用文件末尾作为参考点。  _whence_  如果省略则默认值为 0，即使用文件开头作为参考点。

>>>

>>> f = open('workfile', 'rb+')
>>> f.write(b'0123456789abcdef')
16
>>> f.seek(5)      # Go to the 6th byte in the file
5
>>> f.read(1)
b'5'
>>> f.seek(-3, 2)  # Go to the 3rd byte before the end
13
>>> f.read(1)
b'd'

在文本文件（那些在模式字符串中没有  `b`  的打开的文件）中，只允许相对于文件开头搜索（使用  `seek(0,  2)`  搜索到文件末尾是个例外）并且唯一有效的  _offset_  值是那些能从  `f.tell()`  中返回的或者是零。其他  _offset_  值都会产生未定义的行为。

文件对象有一些额外的方法，例如  `isatty()`  和  `truncate()`  ，它们使用频率较低；有关文件对象的完整指南请参阅库参考。

### 7.2.2. 使用  [`json`](https://docs.python.org/zh-cn/3/library/json.html#module-json "json: Encode and decode the JSON format.")  保存结构化数据[](https://docs.python.org/zh-cn/3/tutorial/inputoutput.html#saving-structured-data-with-json "永久链接至标题")

字符串可以很轻松地写入文件并从文件中读取出来。数字可能会费点劲，因为  `read()`  方法只能返回字符串，这些字符串必须传递给类似  [`int()`](https://docs.python.org/zh-cn/3/library/functions.html#int "int")  的函数，它会接受类似  `'123'`  这样的字符串并返回其数字值 123。当你想保存诸如嵌套列表和字典这样更复杂的数据类型时，手动解析和序列化会变得复杂。

Python 允许你使用称为  [JSON (JavaScript Object Notation)](http://json.org/)  的流行数据交换格式，而不是让用户不断的编写和调试代码以将复杂的数据类型保存到文件中。名为  [`json`](https://docs.python.org/zh-cn/3/library/json.html#module-json "json: Encode and decode the JSON format.")  的标准模块可以采用 Python 数据层次结构，并将它们转化为字符串表示形式；这个过程称为  _serializing_  。从字符串表示中重建数据称为  _deserializing_  。在序列化和反序列化之间，表示对象的字符串可能已存储在文件或数据中，或通过网络连接发送到某个远程机器。

注解

JSON格式通常被现代应用程序用于允许数据交换。许多程序员已经熟悉它，这使其成为互操作性的良好选择。

如果你有一个对象  `x`  ，你可以用一行简单的代码来查看它的 JSON 字符串表示:

>>>

>>> import json
>>> json.dumps([1, 'simple', 'list'])
'[1, "simple", "list"]'

[`dumps()`](https://docs.python.org/zh-cn/3/library/json.html#json.dumps "json.dumps")  函数的另一个变体叫做  [`dump()`](https://docs.python.org/zh-cn/3/library/json.html#json.dump "json.dump")  ，它只是将对象序列化为  [text file](https://docs.python.org/zh-cn/3/glossary.html#term-text-file)  。因此，如果  `f`  是一个  [text file](https://docs.python.org/zh-cn/3/glossary.html#term-text-file)  对象，我们可以这样做:

json.dump(x, f)

要再次解码对象，如果  `f`  是一个打开的以供阅读的  [text file](https://docs.python.org/zh-cn/3/glossary.html#term-text-file)  对象:

x = json.load(f)

这种简单的序列化技术可以处理列表和字典，但是在JSON中序列化任意类的实例需要额外的努力。  [`json`](https://docs.python.org/zh-cn/3/library/json.html#module-json "json: Encode and decode the JSON format.")  模块的参考包含对此的解释。

参见

[`pickle`](https://docs.python.org/zh-cn/3/library/pickle.html#module-pickle "pickle: Convert Python objects to streams of bytes and back.")  - 封存模块

与  [JSON](https://docs.python.org/zh-cn/3/tutorial/inputoutput.html#tut-json)  不同，_pickle_  是一种允许对任意复杂 Python 对象进行序列化的协议。因此，它为 Python 所特有，不能用于与其他语言编写的应用程序通信。默认情况下它也是不安全的：如果数据是由熟练的攻击者精心设计的，则反序列化来自不受信任来源的 pickle 数据可以执行任意代码。

# 8. 错误和异常[¶](https://docs.python.org/zh-cn/3/tutorial/errors.html#errors-and-exceptions "永久链接至标题")

到目前为止，我们还没有提到错误消息，但是如果你已经尝试过那些例子，你可能已经看过了一些错误消息。 目前（至少）有两种可区分的错误：_语法错误_  和  _异常_。

## 8.1. 语法错误[](https://docs.python.org/zh-cn/3/tutorial/errors.html#syntax-errors "永久链接至标题")

语法错误又称解析错误，可能是你在学习Python 时最容易遇到的错误:

>>>

>>> while True print('Hello world')
  File "<stdin>", line 1
    while True print('Hello world')
                   ^
SyntaxError: invalid syntax

解析器会输出出现语法错误的那一行，并显示一个“箭头”，指向这行里面检测到第一个错误。 错误是由箭头指示的位置  _上面_  的 token 引起的（或者至少是在这里被检测出的）：在示例中，在  [`print()`](https://docs.python.org/zh-cn/3/library/functions.html#print "print")  这个函数中检测到了错误，因为在它前面少了个冒号 (`':'`) 。文件名和行号也会被输出，以便输入来自脚本文件时你能知道去哪检查。

## 8.2. 异常[](https://docs.python.org/zh-cn/3/tutorial/errors.html#exceptions "永久链接至标题")

即使语句或表达式在语法上是正确的，但在尝试执行时，它仍可能会引发错误。 在执行时检测到的错误被称为  _异常_，异常不一定会导致严重后果：你将很快学会如何在 Python 程序中处理它们。 但是，大多数异常并不会被程序处理，此时会显示如下所示的错误信息:

>>>

>>> 10 * (1/0)
Traceback (most recent call last): File "<stdin>", line 1, in <module>
ZeroDivisionError: division by zero
>>> 4 + spam*3
Traceback (most recent call last): File "<stdin>", line 1, in <module>
NameError: name 'spam' is not defined
>>> '2' + 2
Traceback (most recent call last): File "<stdin>", line 1, in <module>
TypeError: Can't convert 'int' object to str implicitly

错误信息的最后一行告诉我们程序遇到了什么类型的错误。异常有不同的类型，而其类型名称将会作为错误信息的一部分中打印出来：上述示例中的异常类型依次是：[`ZeroDivisionError`](https://docs.python.org/zh-cn/3/library/exceptions.html#ZeroDivisionError "ZeroDivisionError")，  [`NameError`](https://docs.python.org/zh-cn/3/library/exceptions.html#NameError "NameError")  和  [`TypeError`](https://docs.python.org/zh-cn/3/library/exceptions.html#TypeError "TypeError")。作为异常类型打印的字符串是发生的内置异常的名称。对于所有内置异常都是如此，但对于用户定义的异常则不一定如此（虽然这是一个有用的规范）。标准的异常类型是内置的标识符（而不是保留关键字）。

这一行的剩下的部分根据异常类型及其原因提供详细信息。

错误信息的前一部分以堆栈回溯的形式显示发生异常时的上下文。通常它包含列出源代码行的堆栈回溯；但是它不会显示从标准输入中读取的行。

[内置异常](https://docs.python.org/zh-cn/3/library/exceptions.html#bltin-exceptions)  列出了内置异常和它们的含义。

## 8.3. 处理异常[](https://docs.python.org/zh-cn/3/tutorial/errors.html#handling-exceptions "永久链接至标题")

可以编写处理所选异常的程序。请看下面的例子，它会要求用户一直输入，直到输入的是一个有效的整数，但允许用户中断程序（使用  Control-C  或操作系统支持的其他操作）；请注意用户引起的中断可以通过引发  [`KeyboardInterrupt`](https://docs.python.org/zh-cn/3/library/exceptions.html#KeyboardInterrupt "KeyboardInterrupt")  异常来指示。:

>>>

>>> while True:
...     try:
...         x = int(input("Please enter a number: "))
...         break
...     except ValueError:
...         print("Oops!  That was no valid number.  Try again...")
...

[`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try)  语句的工作原理如下。

-   首先，执行  _try 子句_  （[`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try)  和  [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except)  关键字之间的（多行）语句）。
    
-   如果没有异常发生，则跳过  _except 子句_  并完成  [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try)  语句的执行。
    
-   如果在执行try 子句时发生了异常，则跳过该子句中剩下的部分。然后，如果异常的类型和  [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except)  关键字后面的异常匹配，则执行 except 子句 ，然后继续执行  [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try)  语句之后的代码。
    
-   如果发生的异常和 except 子句中指定的异常不匹配，则将其传递到外部的  [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try)  语句中；如果没有找到处理程序，则它是一个  _未处理异常_，执行将停止并显示如上所示的消息。
    

一个  [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try)  语句可能有多个 except 子句，以指定不同异常的处理程序。 最多会执行一个处理程序。 处理程序只处理相应的 try 子句中发生的异常，而不处理同一  `try`  语句内其他处理程序中的异常。 一个 except 子句可以将多个异常命名为带括号的元组，例如:

... except (RuntimeError, TypeError, NameError):
...     pass

如果发生的异常和  [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except)  子句中的类是同一个类或者是它的基类，则异常和 except 子句中的类是兼容的（但反过来则不成立 --- 列出派生类的 except 子句与基类不兼容）。 例如，下面的代码将依次打印 B, C, D

class B(Exception):
    pass

class C(B):
    pass

class D(C):
    pass

for cls in [B, C, D]:
    try:
        raise cls()
    except D:
        print("D")
    except C:
        print("C")
    except B:
        print("B")

请注意如果 except 子句被颠倒（把  `except  B`  放到第一个），它将打印 B，B，B --- 即第一个匹配的 except 子句被触发。

最后的 except 子句可以省略异常名，以用作通配符。但请谨慎使用，因为以这种方式很容易掩盖真正的编程错误！它还可用于打印错误消息，然后重新引发异常（同样允许调用者处理异常）:

import sys

try:
    f = open('myfile.txt')
    s = f.readline()
    i = int(s.strip())
except OSError as err:
    print("OS error: {0}".format(err))
except ValueError:
    print("Could not convert data to an integer.")
except:
    print("Unexpected error:", sys.exc_info()[0])
    raise

[`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try)  ...  [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except)  语句有一个可选的  _else 子句_，在使用时必须放在所有的 except 子句后面。对于在try 子句不引发异常时必须执行的代码来说很有用。例如:

for arg in sys.argv[1:]:
    try:
        f = open(arg, 'r')
    except OSError:
        print('cannot open', arg)
    else:
        print(arg, 'has', len(f.readlines()), 'lines')
        f.close()

使用  `else`  子句比向  [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try)  子句添加额外的代码要好，因为它避免了意外捕获由  `try`  ...  `except`  语句保护的代码未引发的异常。

发生异常时，它可能具有关联值，也称为异常  _参数_  。参数的存在和类型取决于异常类型。

except 子句可以在异常名称后面指定一个变量。这个变量和一个异常实例绑定，它的参数存储在  `instance.args`  中。为了方便起见，异常实例定义了  [`__str__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__str__ "object.__str__")  ，因此可以直接打印参数而无需引用  `.args`  。也可以在抛出之前首先实例化异常，并根据需要向其添加任何属性。:

>>>

>>> try:
...     raise Exception('spam', 'eggs')
... except Exception as inst:
...     print(type(inst))    # the exception instance
...     print(inst.args)     # arguments stored in .args
...     print(inst)          # __str__ allows args to be printed directly,
...                          # but may be overridden in exception subclasses
...     x, y = inst.args     # unpack args
...     print('x =', x)
...     print('y =', y)
...
<class 'Exception'>
('spam', 'eggs')
('spam', 'eggs')
x = spam
y = eggs

如果异常有参数，则它们将作为未处理异常的消息的最后一部分（'详细信息'）打印。

异常处理程序不仅处理 try 子句中遇到的异常，还处理 try 子句中调用（即使是间接地）的函数内部发生的异常。例如:

>>>

>>> def this_fails():
...     x = 1/0
...
>>> try:
...     this_fails()
... except ZeroDivisionError as err:
...     print('Handling run-time error:', err)
...
Handling run-time error: division by zero

## 8.4. 抛出异常[](https://docs.python.org/zh-cn/3/tutorial/errors.html#raising-exceptions "永久链接至标题")

[`raise`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#raise)  语句允许程序员强制发生指定的异常。例如:

>>>

>>> raise NameError('HiThere')
Traceback (most recent call last): File "<stdin>", line 1, in <module>
NameError: HiThere

[`raise`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#raise)  唯一的参数就是要抛出的异常。这个参数必须是一个异常实例或者是一个异常类（派生自  [`Exception`](https://docs.python.org/zh-cn/3/library/exceptions.html#Exception "Exception")  的类）。如果传递的是一个异常类，它将通过调用没有参数的构造函数来隐式实例化:

raise ValueError  # shorthand for 'raise ValueError()'

如果你需要确定是否引发了异常但不打算处理它，则可以使用更简单的  [`raise`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#raise)  语句形式重新引发异常

>>>

>>> try:
...     raise NameError('HiThere')
... except NameError:
...     print('An exception flew by!')
...     raise
...
An exception flew by!
Traceback (most recent call last): File "<stdin>", line 2, in <module>
NameError: HiThere

## 8.5. 用户自定义异常[](https://docs.python.org/zh-cn/3/tutorial/errors.html#user-defined-exceptions "永久链接至标题")

程序可以通过创建新的异常类来命名它们自己的异常（有关Python 类的更多信息，请参阅  [类](https://docs.python.org/zh-cn/3/tutorial/classes.html#tut-classes)）。异常通常应该直接或间接地从  [`Exception`](https://docs.python.org/zh-cn/3/library/exceptions.html#Exception "Exception")  类派生。

可以定义异常类，它可以执行任何其他类可以执行的任何操作，但通常保持简单，通常只提供许多属性，这些属性允许处理程序为异常提取有关错误的信息。在创建可能引发多个不同错误的模块时，通常的做法是为该模块定义的异常创建基类，并为不同错误条件创建特定异常类的子类:

class Error(Exception):
    """Base class for exceptions in this module."""
    pass

class InputError(Error):
    """Exception raised for errors in the input.

 Attributes:
 expression -- input expression in which the error occurred
 message -- explanation of the error
 """

    def __init__(self, expression, message):
        self.expression = expression
        self.message = message

class TransitionError(Error):
    """Raised when an operation attempts a state transition that's not
 allowed.

 Attributes:
 previous -- state at beginning of transition
 next -- attempted new state
 message -- explanation of why the specific transition is not allowed
 """

    def __init__(self, previous, next, message):
        self.previous = previous
        self.next = next
        self.message = message

大多数异常都定义为名称以“Error”结尾，类似于标准异常的命名。

许多标准模块定义了它们自己的异常，以报告它们定义的函数中可能出现的错误。有关类的更多信息，请参见类  [类](https://docs.python.org/zh-cn/3/tutorial/classes.html#tut-classes)。

## 8.6. 定义清理操作[](https://docs.python.org/zh-cn/3/tutorial/errors.html#defining-clean-up-actions "永久链接至标题")

[`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try)  语句有另一个可选子句，用于定义必须在所有情况下执行的清理操作。例如:

>>>

>>> try:
...     raise KeyboardInterrupt
... finally:
...     print('Goodbye, world!')
...
Goodbye, world!
KeyboardInterrupt
Traceback (most recent call last): File "<stdin>", line 2, in <module>

如果存在  [`finally`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#finally)  子句，则  `finally`  子句将作为  [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try)  语句结束前的最后一项任务被执行。  `finally`  子句不论  `try`  语句是否产生了异常都会被执行。 以下几点讨论了当异常发生时一些更复杂的情况：

-   如果在执行  `try`  子句期间发生了异常，该异常可由一个  [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except)  子句进行处理。 如果异常没有被某个  `except`  子句所处理，则该异常会在  `finally`  子句执行之后被重新引发。
    
-   异常也可能在  `except`  或  `else`  子句执行期间发生。 同样地，该异常会在  `finally`  子句执行之后被重新引发。
    
-   如果在执行  `try`  语句时遇到一个  [`break`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#break),  [`continue`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#continue)  或  [`return`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#return)  语句，则  `finally`  子句将在执行  `break`,  `continue`  或  `return`  语句之前被执行。
    
-   如果  `finally`  子句中包含一个  `return`  语句，则返回值将来自  `finally`  子句的某个  `return`  语句的返回值，而非来自  `try`  子句的  `return`  语句的返回值。
    

例如

>>>

>>> def bool_return():
...     try:
...         return True
...     finally:
...         return False
...
>>> bool_return()
False

一个更为复杂的例子:

>>>

>>> def divide(x, y):
...     try:
...         result = x / y
...     except ZeroDivisionError:
...         print("division by zero!")
...     else:
...         print("result is", result)
...     finally:
...         print("executing finally clause")
...
>>> divide(2, 1)
result is 2.0
executing finally clause
>>> divide(2, 0)
division by zero!
executing finally clause
>>> divide("2", "1")
executing finally clause
Traceback (most recent call last): File "<stdin>", line 1, in <module> File "<stdin>", line 3, in divide
TypeError: unsupported operand type(s) for /: 'str' and 'str'

正如你所看到的，[`finally`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#finally)  子句在任何情况下都会被执行。 两个字符串相除所引发的  [`TypeError`](https://docs.python.org/zh-cn/3/library/exceptions.html#TypeError "TypeError")  不会由  [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except)  子句处理，因此会在  `finally`  子句执行后被重新引发。

在实际应用程序中，[`finally`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#finally)  子句对于释放外部资源（例如文件或者网络连接）非常有用，无论是否成功使用资源。

## 8.7. 预定义的清理操作[](https://docs.python.org/zh-cn/3/tutorial/errors.html#predefined-clean-up-actions "永久链接至标题")

某些对象定义了在不再需要该对象时要执行的标准清理操作，无论使用该对象的操作是成功还是失败。请查看下面的示例，它尝试打开一个文件并把其内容打印到屏幕上。:

for line in open("myfile.txt"):
    print(line, end="")

这个代码的问题在于，它在这部分代码执行完后，会使文件在一段不确定的时间内处于打开状态。这在简单脚本中不是问题，但对于较大的应用程序来说可能是个问题。  [`with`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#with)  语句允许像文件这样的对象能够以一种确保它们得到及时和正确的清理的方式使用。:

with open("myfile.txt") as f:
    for line in f:
        print(line, end="")

执行完语句后，即使在处理行时遇到问题，文件  _f_  也始终会被关闭。和文件一样，提供预定义清理操作的对象将在其文档中指出这一点。


# 9. 类[](https://docs.python.org/zh-cn/3/tutorial/classes.html#classes "永久链接至标题")

类提供了一种组合数据和功能的方法。 创建一个新类意味着创建一个新的对象  _类型_，从而允许创建一个该类型的新  _实例_  。 每个类的实例可以拥有保存自己状态的属性。 一个类的实例也可以有改变自己状态的（定义在类中的）方法。

和其他编程语言相比，Python 用非常少的新语法和语义将类加入到语言中。它是 C++ 和 Modula-3 中类机制的结合。Python 的类提供了面向对象编程的所有标准特性：类继承机制允许多个基类，派生类可以覆盖它基类的任何方法，一个方法可以调用基类中相同名称的的方法。对象可以包含任意数量和类型的数据。和模块一样，类也拥有 Python 天然的动态特性：它们在运行时创建，可以在创建后修改。

在 C++ 术语中，通常类成员（包括数据成员）是  _public_  (例外见下文  [私有变量](https://docs.python.org/zh-cn/3/tutorial/classes.html#tut-private))，所有成员函数都是  _virtual_。 与在 Modula-3 中一样，没有用于从其方法引用对象成员的简写：方法函数使用表示对象的显式第一个参数声明，该参数由调用隐式提供。 与 Smalltalk 一样，类本身也是对象。 这为导入和重命名提供了语义。 与 C++ 和 Modula-3 不同，内置类型可以用作用户扩展的基类。 此外，与 C++ 一样，大多数具有特殊语法（算术运算符，下标等）的内置运算符都可以为类实例而重新定义。

（由于缺乏关于类的公认术语，我会偶尔使用 Smalltalk 和 C++ 的用辞。 我还会使用 Modula-3 的术语，因为其面向对象的语义比 C++ 更接近 Python，但我预计少有读者听说过它。）

## 9.1. 名称和对象[](https://docs.python.org/zh-cn/3/tutorial/classes.html#a-word-about-names-and-objects "永久链接至标题")

对象具有个性，多个名称（在多个作用域内）可以绑定到同一个对象。这在其他语言中称为别名。乍一看Python时通常不会理解这一点，在处理不可变的基本类型（数字，字符串，元组）时可以安全地忽略它。但是，别名对涉及可变对象，如列表，字典和大多数其他类型，的Python代码的语义可能会产生惊人的影响。这通常用于程序的好处，因为别名在某些方面表现得像指针。例如，传递一个对象很便宜，因为实现只传递一个指针；如果函数修改了作为参数传递的对象，调用者将看到更改 --- 这就不需要像 Pascal 中那样使用两个不同的参数传递机制。

## 9.2. Python 作用域和命名空间[](https://docs.python.org/zh-cn/3/tutorial/classes.html#python-scopes-and-namespaces "永久链接至标题")

在介绍类之前，我首先要告诉你一些Python的作用域规则。类定义对命名空间有一些巧妙的技巧，你需要知道作用域和命名空间如何工作才能完全理解正在发生的事情。顺便说一下，关于这个主题的知识对任何高级Python程序员都很有用。

让我们从一些定义开始。

_namespace_  （命名空间）是一个从名字到对象的映射。 大部分命名空间当前都由 Python 字典实现，但一般情况下基本不会去关注它们（除了要面对性能问题时），而且也有可能在将来更改。 下面是几个命名空间的例子：存放内置函数的集合（包含  [`abs()`](https://docs.python.org/zh-cn/3/library/functions.html#abs "abs")  这样的函数，和内建的异常等）；模块中的全局名称；函数调用中的局部名称。 从某种意义上说，对象的属性集合也是一种命名空间的形式。 关于命名空间的重要一点是，不同命名空间中的名称之间绝对没有关系；例如，两个不同的模块都可以定义一个  `maximize`  函数而不会产生混淆 --- 模块的用户必须在其前面加上模块名称。

顺便说明一下，我把任何跟在一个点号之后的名称都称为  _属性_  --- 例如，在表达式  `z.real`  中，`real`  是对象  `z`  的一个属性。按严格的说法，对模块中名称的引用属于属性引用：在表达式  `modname.funcname`  中，`modname`  是一个模块对象而  `funcname`  是它的一个属性。在此情况下在模块的属性和模块中定义的全局名称之间正好存在一个直观的映射：它们共享相同的命名空间！  [1](https://docs.python.org/zh-cn/3/tutorial/classes.html#id2)

属性可以是只读或者可写的。如果为后者，那么对属性的赋值是可行的。模块属性是可以写，你可以写出  `modname.the_answer  =  42`  。可写的属性同样可以用  [`del`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#del)  语句删除。例如，  `del  modname.the_answer`  将会从名为  `modname`  的对象中移除  `the_answer`  属性。

在不同时刻创建的命名空间拥有不同的生存期。包含内置名称的命名空间是在 Python 解释器启动时创建的，永远不会被删除。模块的全局命名空间在模块定义被读入时创建；通常，模块命名空间也会持续到解释器退出。被解释器的顶层调用执行的语句，从一个脚本文件读取或交互式地读取，被认为是  [`__main__`](https://docs.python.org/zh-cn/3/library/__main__.html#module-__main__ "__main__: The environment where the top-level script is run.")  模块调用的一部分，因此它们拥有自己的全局命名空间。（内置名称实际上也存在于一个模块中；这个模块称作  [`builtins`](https://docs.python.org/zh-cn/3/library/builtins.html#module-builtins "builtins: The module that provides the built-in namespace.")  。）

一个函数的本地命名空间在这个函数被调用时创建，并在函数返回或抛出一个不在函数内部处理的错误时被删除。（事实上，比起描述到底发生了什么，忘掉它更好。）当然，每次递归调用都会有它自己的本地命名空间。

一个  _作用域_  是一个命名空间可直接访问的 Python 程序的文本区域。 这里的 “可直接访问” 意味着对名称的非限定引用会尝试在命名空间中查找名称。

虽然作用域是静态地确定的，但它们会被动态地使用。 在执行期间的任何时刻，会有 3 或 4 个个命名空间可被直接访问的嵌套作用域:

-   最先搜索的最内部作用域包含局部名称
    
-   从最近的封闭作用域开始搜索的任何封闭函数的作用域包含非局部名称，也包括非全局名称
    
-   倒数第二个作用域包含当前模块的全局名称
    
-   最外面的作用域（最后搜索）是包含内置名称的命名空间
    

如果一个名称被声明为全局变量，则所有引用和赋值将直接指向包含该模块的全局名称的中间作用域。 要重新绑定在最内层作用域以外找到的变量，可以使用  [`nonlocal`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#nonlocal)  语句声明为非本地变量。 如果没有被声明为非本地变量，这些变量将是只读的（尝试写入这样的变量只会在最内层作用域中创建一个  _新的_  局部变量，而同名的外部变量保持不变）。

通常，当前局部作用域将（按字面文本）引用当前函数的局部名称。 在函数以外，局部作用域将引用与全局作用域相一致的命名空间：模块的命名空间。 类定义将在局部命名空间内再放置另一个命名空间。

重要的是应该意识到作用域是按字面文本来确定的：在一个模块内定义的函数的全局作用域就是该模块的命名空间，无论该函数从什么地方或以什么别名被调用。 另一方面，实际的名称搜索是在运行时动态完成的 --- 但是，Python 正在朝着“编译时静态名称解析”的方向发展，因此不要过于依赖动态名称解析！ （事实上，局部变量已经是被静态确定了。）

Python 的一个特殊规定是这样的 -- 如果不存在生效的  [`global`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#global)  或  [`nonlocal`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#nonlocal)  语句 -- 则对名称的赋值总是会进入最内层作用域。 赋值不会复制数据 --- 它们只是将名称绑定到对象。 删除也是如此：语句  `del  x`  会从局部作用域所引用的命名空间中移除对  `x`  的绑定。 事实上，所有引入新名称的操作都是使用局部作用域：特别地，[`import`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#import)  语句和函数定义会在局部作用域中绑定模块或函数名称。

[`global`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#global)  语句可被用来表明特定变量生存于全局作用域并且应当在其中被重新绑定；[`nonlocal`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#nonlocal)  语句表明特定变量生存于外层作用域中并且应当在其中被重新绑定。

### 9.2.1. 作用域和命名空间示例[](https://docs.python.org/zh-cn/3/tutorial/classes.html#scopes-and-namespaces-example "永久链接至标题")

这个例子演示了如何引用不同作用域和名称空间，以及  [`global`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#global)  和  [`nonlocal`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#nonlocal)  会如何影响变量绑定:

def scope_test():
    def do_local():
        spam = "local spam"

    def do_nonlocal():
        nonlocal spam
        spam = "nonlocal spam"

    def do_global():
        global spam
        spam = "global spam"

    spam = "test spam"
    do_local()
    print("After local assignment:", spam)
    do_nonlocal()
    print("After nonlocal assignment:", spam)
    do_global()
    print("After global assignment:", spam)

scope_test()
print("In global scope:", spam)

示例代码的输出是：

After local assignment: test spam
After nonlocal assignment: nonlocal spam
After global assignment: nonlocal spam
In global scope: global spam

请注意  _局部_  赋值（这是默认状态）不会改变  _scope_test_  对  _spam_  的绑定。  [`nonlocal`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#nonlocal)  赋值会改变  _scope_test_  对  _spam_  的绑定，而  [`global`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#global)  赋值会改变模块层级的绑定。

您还可以在  [`global`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#global)  赋值之前看到之前没有  _spam_  的绑定。

## 9.3. 初探类[](https://docs.python.org/zh-cn/3/tutorial/classes.html#a-first-look-at-classes "永久链接至标题")

类引入了一些新语法，三种新对象类型和一些新语义。

### 9.3.1. 类定义语法[](https://docs.python.org/zh-cn/3/tutorial/classes.html#class-definition-syntax "永久链接至标题")

最简单的类定义看起来像这样:

class ClassName:
    <statement-1>
    .
    .
    .
    <statement-N>

类定义与函数定义 ([`def`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#def)  语句) 一样必须被执行才会起作用。 （你可以尝试将类定义放在  [`if`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#if)  语句的一个分支或是函数的内部。）

在实践中，类定义内的语句通常都是函数定义，但也允许有其他语句，有时还很有用 --- 我们会稍后再回来说明这个问题。 在类内部的函数定义通常具有一种特别形式的参数列表，这是方法调用的约定规范所指明的 --- 这个问题也将在稍后再说明。

当进入类定义时，将创建一个新的命名空间，并将其用作局部作用域 --- 因此，所有对局部变量的赋值都是在这个新命名空间之内。 特别的，函数定义会绑定到这里的新函数名称。

当（从结尾处）正常离开类定义时，将创建一个  _类对象_。 这基本上是一个包围在类定义所创建命名空间内容周围的包装器；我们将在下一节了解有关类对象的更多信息。 原始的（在进入类定义之前起作用的）局部作用域将重新生效，类对象将在这里被绑定到类定义头所给出的类名称 (在这个示例中为  `ClassName`)。

### 9.3.2. 类对象[](https://docs.python.org/zh-cn/3/tutorial/classes.html#class-objects "永久链接至标题")

类对象支持两种操作：属性引用和实例化。

_属性引用_  使用 Python 中所有属性引用所使用的标准语法:  `obj.name`。 有效的属性名称是类对象被创建时存在于类命名空间中的所有名称。 因此，如果类定义是这样的:

class MyClass:
    """A simple example class"""
    i = 12345

    def f(self):
        return 'hello world'

那么  `MyClass.i`  和  `MyClass.f`  就是有效的属性引用，将分别返回一个整数和一个函数对象。 类属性也可以被赋值，因此可以通过赋值来更改  `MyClass.i`  的值。  `__doc__`  也是一个有效的属性，将返回所属类的文档字符串:  `"A  simple  example  class"`。

类的  _实例化_  使用函数表示法。 可以把类对象视为是返回该类的一个新实例的不带参数的函数。 举例来说（假设使用上述的类）:

x = MyClass()

创建类的新  _实例_  并将此对象分配给局部变量  `x`。

实例化操作（“调用”类对象）会创建一个空对象。 许多类喜欢创建带有特定初始状态的自定义实例。 为此类定义可能包含一个名为  [`__init__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__init__ "object.__init__")  的特殊方法，就像这样:

def __init__(self):
    self.data = []

当一个类定义了  [`__init__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__init__ "object.__init__")  方法时，类的实例化操作会自动为新创建的类实例发起调用  [`__init__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__init__ "object.__init__")。 因此在这个示例中，可以通过以下语句获得一个经初始化的新实例:

x = MyClass()

当然，[`__init__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__init__ "object.__init__")  方法还可以有额外参数以实现更高灵活性。 在这种情况下，提供给类实例化运算符的参数将被传递给  [`__init__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__init__ "object.__init__")。 例如，:

>>>

>>> class Complex:
...     def __init__(self, realpart, imagpart):
...         self.r = realpart
...         self.i = imagpart
...
>>> x = Complex(3.0, -4.5)
>>> x.r, x.i
(3.0, -4.5)

### 9.3.3. 实例对象[](https://docs.python.org/zh-cn/3/tutorial/classes.html#instance-objects "永久链接至标题")

现在我们能用实例对象做什么？ 实例对象理解的唯一操作是属性引用。 有两种有效的属性名称：数据属性和方法。

_数据属性_  对应于 Smalltalk 中的“实例变量”，以及 C++ 中的“数据成员”。 数据属性不需要声明；像局部变量一样，它们将在第一次被赋值时产生。 例如，如果  `x`  是上面创建的  `MyClass`  的实例，则以下代码段将打印数值  `16`，且不保留任何追踪信息:

x.counter = 1
while x.counter < 10:
    x.counter = x.counter * 2
print(x.counter)
del x.counter

另一类实例属性引用称为  _方法_。 方法是“从属于”对象的函数。 （在 Python 中，方法这个术语并不是类实例所特有的：其他对象也可以有方法。 例如，列表对象具有 append, insert, remove, sort 等方法。 然而，在以下讨论中，我们使用方法一词将专指类实例对象的方法，除非另外显式地说明。）

实例对象的有效方法名称依赖于其所属的类。 根据定义，一个类中所有是函数对象的属性都是定义了其实例的相应方法。 因此在我们的示例中，`x.f`  是有效的方法引用，因为  `MyClass.f`  是一个函数，而  `x.i`  不是方法，因为  `MyClass.i`  不是一个函数。 但是  `x.f`  与  `MyClass.f`  并不是一回事 --- 它是一个  _方法对象_，不是函数对象。

### 9.3.4. 方法对象[](https://docs.python.org/zh-cn/3/tutorial/classes.html#method-objects "永久链接至标题")

通常，方法在绑定后立即被调用:

x.f()

在  `MyClass`  示例中，这将返回字符串  `'hello  world'`。 但是，立即调用一个方法并不是必须的:  `x.f`  是一个方法对象，它可以被保存起来以后再调用。 例如:

xf = x.f
while True:
    print(xf())

将继续打印  `hello  world`，直到结束。

当一个方法被调用时到底发生了什么？ 你可能已经注意到上面调用  `x.f()`  时并没有带参数，虽然  `f()`  的函数定义指定了一个参数。 这个参数发生了什么事？ 当不带参数地调用一个需要参数的函数时 Python 肯定会引发异常 --- 即使参数实际未被使用...

实际上，你可能已经猜到了答案：方法的特殊之处就在于实例对象会作为函数的第一个参数被传入。 在我们的示例中，调用  `x.f()`  其实就相当于  `MyClass.f(x)`。 总之，调用一个具有  _n_  个参数的方法就相当于调用再多一个参数的对应函数，这个参数值为方法所属实例对象，位置在其他参数之前。

如果你仍然无法理解方法的运作原理，那么查看实现细节可能会澄清问题。 当一个实例的非数据属性被引用时，将搜索实例所属的类。 如果被引用的属性名称表示一个有效的类属性中的函数对象，会通过打包（指向）查找到的实例对象和函数对象到一个抽象对象的方式来创建方法对象：这个抽象对象就是方法对象。 当附带参数列表调用方法对象时，将基于实例对象和参数列表构建一个新的参数列表，并使用这个新参数列表调用相应的函数对象。

### 9.3.5. 类和实例变量[](https://docs.python.org/zh-cn/3/tutorial/classes.html#class-and-instance-variables "永久链接至标题")

一般来说，实例变量用于每个实例的唯一数据，而类变量用于类的所有实例共享的属性和方法:

class Dog:

    kind = 'canine'         # class variable shared by all instances

    def __init__(self, name):
        self.name = name    # instance variable unique to each instance

>>> d = Dog('Fido')
>>> e = Dog('Buddy')
>>> d.kind                  # shared by all dogs
'canine'
>>> e.kind                  # shared by all dogs
'canine'
>>> d.name                  # unique to d
'Fido'
>>> e.name                  # unique to e
'Buddy'

正如  [名称和对象](https://docs.python.org/zh-cn/3/tutorial/classes.html#tut-object)  中已讨论过的，共享数据可能在涉及  [mutable](https://docs.python.org/zh-cn/3/glossary.html#term-mutable)  对象例如列表和字典的时候导致令人惊讶的结果。 例如以下代码中的  _tricks_  列表不应该被用作类变量，因为所有的  _Dog_  实例将只共享一个单独的列表:

class Dog:

    tricks = []             # mistaken use of a class variable

    def __init__(self, name):
        self.name = name

    def add_trick(self, trick):
        self.tricks.append(trick)

>>> d = Dog('Fido')
>>> e = Dog('Buddy')
>>> d.add_trick('roll over')
>>> e.add_trick('play dead')
>>> d.tricks                # unexpectedly shared by all dogs
['roll over', 'play dead']

正确的类设计应该使用实例变量:

class Dog:

    def __init__(self, name):
        self.name = name
        self.tricks = []    # creates a new empty list for each dog

    def add_trick(self, trick):
        self.tricks.append(trick)

>>> d = Dog('Fido')
>>> e = Dog('Buddy')
>>> d.add_trick('roll over')
>>> e.add_trick('play dead')
>>> d.tricks
['roll over']
>>> e.tricks
['play dead']

## 9.4. 补充说明[](https://docs.python.org/zh-cn/3/tutorial/classes.html#random-remarks "永久链接至标题")

如果同样的属性名称同时出现在实例和类中，则属性查找会优先选择实例:

>>>

>>> class Warehouse:
 purpose = 'storage'
 region = 'west'

>>> w1 = Warehouse()
>>> print(w1.purpose, w1.region)
storage west
>>> w2 = Warehouse()
>>> w2.region = 'east'
>>> print(w2.purpose, w2.region)
storage east

数据属性可以被方法以及一个对象的普通用户（“客户端”）所引用。 换句话说，类不能用于实现纯抽象数据类型。 实际上，在 Python 中没有任何东西能强制隐藏数据 --- 它是完全基于约定的。 （而在另一方面，用 C 语言编写的 Python 实现则可以完全隐藏实现细节，并在必要时控制对象的访问；此特性可以通过用 C 编写 Python 扩展来使用。）

客户端应当谨慎地使用数据属性 --- 客户端可能通过直接操作数据属性的方式破坏由方法所维护的固定变量。 请注意客户端可以向一个实例对象添加他们自己的数据属性而不会影响方法的可用性，只要保证避免名称冲突 --- 再次提醒，在此使用命名约定可以省去许多令人头痛的麻烦。

在方法内部引用数据属性（或其他方法！）并没有简便方式。 我发现这实际上提升了方法的可读性：当浏览一个方法代码时，不会存在混淆局部变量和实例变量的机会。

方法的第一个参数常常被命名为  `self`。 这也不过就是一个约定:  `self`  这一名称在 Python 中绝对没有特殊含义。 但是要注意，不遵循此约定会使得你的代码对其他 Python 程序员来说缺乏可读性，而且也可以想像一个  _类浏览器_  程序的编写可能会依赖于这样的约定。

任何一个作为类属性的函数都为该类的实例定义了一个相应方法。 函数定义的文本并非必须包含于类定义之内：将一个函数对象赋值给一个局部变量也是可以的。 例如:

# Function defined outside the class
def f1(self, x, y):
    return min(x, x+y)

class C:
    f = f1

    def g(self):
        return 'hello world'

    h = g

现在  `f`,  `g`  和  `h`  都是  `C`  类的引用函数对象的属性，因而它们就都是  `C`  的实例的方法 --- 其中  `h`  完全等同于  `g`。 但请注意，本示例的做法通常只会令程序的阅读者感到迷惑。

方法可以通过使用  `self`  参数的方法属性调用其他方法:

class Bag:
    def __init__(self):
        self.data = []

    def add(self, x):
        self.data.append(x)

    def addtwice(self, x):
        self.add(x)
        self.add(x)

方法可以通过与普通函数相同的方式引用全局名称。 与方法相关联的全局作用域就是包含其定义的模块。 （类永远不会被作为全局作用域。） 虽然我们很少会有充分的理由在方法中使用全局作用域，但全局作用域存在许多合法的使用场景：举个例子，导入到全局作用域的函数和模块可以被方法所使用，在其中定义的函数和类也一样。 通常，包含该方法的类本身是在全局作用域中定义的，而在下一节中我们将会发现为何方法需要引用其所属类的很好的理由。

每个值都是一个对象，因此具有  _类_  （也称为  _类型_），并存储为  `object.__class__`  。

## 9.5. 继承[](https://docs.python.org/zh-cn/3/tutorial/classes.html#inheritance "永久链接至标题")

当然，如果不支持继承，语言特性就不值得称为“类”。派生类定义的语法如下所示:

class DerivedClassName(BaseClassName):
    <statement-1>
    .
    .
    .
    <statement-N>

名称  `BaseClassName`  必须定义于包含派生类定义的作用域中。 也允许用其他任意表达式代替基类名称所在的位置。 这有时也可能会用得上，例如，当基类定义在另一个模块中的时候:

class DerivedClassName(modname.BaseClassName):

派生类定义的执行过程与基类相同。 当构造类对象时，基类会被记住。 此信息将被用来解析属性引用：如果请求的属性在类中找不到，搜索将转往基类中进行查找。 如果基类本身也派生自其他某个类，则此规则将被递归地应用。

派生类的实例化没有任何特殊之处:  `DerivedClassName()`  会创建该类的一个新实例。 方法引用将按以下方式解析：搜索相应的类属性，如有必要将按基类继承链逐步向下查找，如果产生了一个函数对象则方法引用就生效。

派生类可能会重载其基类的方法。 因为方法在调用同一对象的其他方法时没有特殊权限，调用同一基类中定义的另一方法的基类方法最终可能会调用覆盖它的派生类的方法。 （对 C++ 程序员的提示：Python 中所有的方法实际上都是  `virtual`  方法。）

在派生类中的重载方法实际上可能想要扩展而非简单地替换同名的基类方法。 有一种方式可以简单地直接调用基类方法：即调用  `BaseClassName.methodname(self,  arguments)`。 有时这对客户端来说也是有用的。 （请注意仅当此基类可在全局作用域中以  `BaseClassName`  的名称被访问时方可使用此方式。）

Python有两个内置函数可被用于继承机制：

-   使用  [`isinstance()`](https://docs.python.org/zh-cn/3/library/functions.html#isinstance "isinstance")  来检查一个实例的类型:  `isinstance(obj,  int)`  仅会在  `obj.__class__`  为  [`int`](https://docs.python.org/zh-cn/3/library/functions.html#int "int")  或某个派生自  [`int`](https://docs.python.org/zh-cn/3/library/functions.html#int "int")  的类时为  `True`。
    
-   使用  [`issubclass()`](https://docs.python.org/zh-cn/3/library/functions.html#issubclass "issubclass")  来检查类的继承关系:  `issubclass(bool,  int)`  为  `True`，因为  [`bool`](https://docs.python.org/zh-cn/3/library/functions.html#bool "bool")  是  [`int`](https://docs.python.org/zh-cn/3/library/functions.html#int "int")  的子类。 但是，`issubclass(float,  int)`  为  `False`，因为  [`float`](https://docs.python.org/zh-cn/3/library/functions.html#float "float")  不是  [`int`](https://docs.python.org/zh-cn/3/library/functions.html#int "int")  的子类。
    

### 9.5.1. 多重继承[](https://docs.python.org/zh-cn/3/tutorial/classes.html#multiple-inheritance "永久链接至标题")

Python也支持一种多重继承。 带有多个基类的类定义语句如下所示:

class DerivedClassName(Base1, Base2, Base3):
    <statement-1>
    .
    .
    .
    <statement-N>

对于多数应用来说，在最简单的情况下，你可以认为搜索从父类所继承属性的操作是深度优先、从左至右的，当层次结构中存在重叠时不会在同一个类中搜索两次。 因此，如果某一属性在  `DerivedClassName`  中未找到，则会到  `Base1`  中搜索它，然后（递归地）到  `Base1`  的基类中搜索，如果在那里未找到，再到  `Base2`  中搜索，依此类推。

真实情况比这个更复杂一些；方法解析顺序会动态改变以支持对  [`super()`](https://docs.python.org/zh-cn/3/library/functions.html#super "super")  的协同调用。 这种方式在某些其他多重继承型语言中被称为后续方法调用，它比单继承型语言中的 super 调用更强大。

动态改变顺序是有必要的，因为所有多重继承的情况都会显示出一个或更多的菱形关联（即至少有一个父类可通过多条路径被最底层类所访问）。 例如，所有类都是继承自  [`object`](https://docs.python.org/zh-cn/3/library/functions.html#object "object")，因此任何多重继承的情况都提供了一条以上的路径可以通向  [`object`](https://docs.python.org/zh-cn/3/library/functions.html#object "object")。 为了确保基类不会被访问一次以上，动态算法会用一种特殊方式将搜索顺序线性化， 保留每个类所指定的从左至右的顺序，只调用每个父类一次，并且保持单调（即一个类可以被子类化而不影响其父类的优先顺序）。 总而言之，这些特性使得设计具有多重继承的可靠且可扩展的类成为可能。 要了解更多细节，请参阅  [https://www.python.org/download/releases/2.3/mro/](https://www.python.org/download/releases/2.3/mro/)。

## 9.6. 私有变量[](https://docs.python.org/zh-cn/3/tutorial/classes.html#private-variables "永久链接至标题")

那种仅限从一个对象内部访问的“私有”实例变量在 Python 中并不存在。 但是，大多数 Python 代码都遵循这样一个约定：带有一个下划线的名称 (例如  `_spam`) 应该被当作是 API 的非公有部分 (无论它是函数、方法或是数据成员)。 这应当被视为一个实现细节，可能不经通知即加以改变。

由于存在对于类私有成员的有效使用场景（例如避免名称与子类所定义的名称相冲突），因此存在对此种机制的有限支持，称为  _名称改写_。 任何形式为  `__spam`  的标识符（至少带有两个前缀下划线，至多一个后缀下划线）的文本将被替换为  `_classname__spam`，其中  `classname`  为去除了前缀下划线的当前类名称。 这种改写不考虑标识符的句法位置，只要它出现在类定义内部就会进行。

名称改写有助于让子类重载方法而不破坏类内方法调用。例如:

class Mapping:
    def __init__(self, iterable):
        self.items_list = []
        self.__update(iterable)

    def update(self, iterable):
        for item in iterable:
            self.items_list.append(item)

    __update = update   # private copy of original update() method

class MappingSubclass(Mapping):

    def update(self, keys, values):
        # provides new signature for update()
        # but does not break __init__()
        for item in zip(keys, values):
            self.items_list.append(item)

上面的示例即使在  `MappingSubclass`  引入了一个  `__update`  标识符的情况下也不会出错，因为它会在  `Mapping`  类中被替换为  `_Mapping__update`  而在  `MappingSubclass`  类中被替换为  `_MappingSubclass__update`。

请注意，改写规则的设计主要是为了避免意外冲突；访问或修改被视为私有的变量仍然是可能的。这在特殊情况下甚至会很有用，例如在调试器中。

请注意传递给  `exec()`  或  `eval()`  的代码不会将发起调用类的类名视作当前类；这类似于  `global`  语句的效果，因此这种效果仅限于同时经过字节码编译的代码。 同样的限制也适用于  `getattr()`,  `setattr()`  和  `delattr()`，以及对于  `__dict__`  的直接引用。

## 9.7. 杂项说明[](https://docs.python.org/zh-cn/3/tutorial/classes.html#odds-and-ends "永久链接至标题")

有时会需要使用类似于 Pascal 的“record”或 C 的“struct”这样的数据类型，将一些命名数据项捆绑在一起。 这种情况适合定义一个空类:

class Employee:
    pass

john = Employee()  # Create an empty employee record

# Fill the fields of the record
john.name = 'John Doe'
john.dept = 'computer lab'
john.salary = 1000

一段需要特定抽象数据类型的 Python 代码往往可以被传入一个模拟了该数据类型的方法的类作为替代。 例如，如果你有一个基于文件对象来格式化某些数据的函数，你可以定义一个带有  `read()`  和  `readline()`  方法从字符串缓存获取数据的类，并将其作为参数传入。

实例方法对象也具有属性:  `m.__self__`  就是带有  `m()`  方法的实例对象，而  `m.__func__`  则是该方法所对应的函数对象。

## 9.8. 迭代器[](https://docs.python.org/zh-cn/3/tutorial/classes.html#iterators "永久链接至标题")

到目前为止，您可能已经注意到大多数容器对象都可以使用  [`for`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#for)  语句:

for element in [1, 2, 3]:
    print(element)
for element in (1, 2, 3):
    print(element)
for key in {'one':1, 'two':2}:
    print(key)
for char in "123":
    print(char)
for line in open("myfile.txt"):
    print(line, end='')

这种访问风格清晰、简洁又方便。 迭代器的使用非常普遍并使得 Python 成为一个统一的整体。 在幕后，[`for`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#for)  语句会在容器对象上调用  [`iter()`](https://docs.python.org/zh-cn/3/library/functions.html#iter "iter")。 该函数返回一个定义了  [`__next__()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#iterator.__next__ "iterator.__next__")  方法的迭代器对象，此方法将逐一访问容器中的元素。 当元素用尽时，[`__next__()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#iterator.__next__ "iterator.__next__")  将引发  [`StopIteration`](https://docs.python.org/zh-cn/3/library/exceptions.html#StopIteration "StopIteration")  异常来通知终止  `for`  循环。 你可以使用  [`next()`](https://docs.python.org/zh-cn/3/library/functions.html#next "next")  内置函数来调用  [`__next__()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#iterator.__next__ "iterator.__next__")  方法；这个例子显示了它的运作方式:

>>>

>>> s = 'abc'
>>> it = iter(s)
>>> it
<iterator object at 0x00A1DB50>
>>> next(it)
'a'
>>> next(it)
'b'
>>> next(it)
'c'
>>> next(it)
Traceback (most recent call last): File "<stdin>", line 1, in <module>
    next(it)
StopIteration

看过迭代器协议的幕后机制，给你的类添加迭代器行为就很容易了。 定义一个  [`__iter__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__iter__ "object.__iter__")  方法来返回一个带有  [`__next__()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#iterator.__next__ "iterator.__next__")  方法的对象。 如果类已定义了  `__next__()`，则  [`__iter__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__iter__ "object.__iter__")  可以简单地返回  `self`:

class Reverse:
    """Iterator for looping over a sequence backwards."""
    def __init__(self, data):
        self.data = data
        self.index = len(data)

    def __iter__(self):
        return self

    def __next__(self):
        if self.index == 0:
            raise StopIteration
        self.index = self.index - 1
        return self.data[self.index]

>>>

>>> rev = Reverse('spam')
>>> iter(rev)
<__main__.Reverse object at 0x00A1DB50>
>>> for char in rev:
...     print(char)
...
m
a
p
s

## 9.9. 生成器[](https://docs.python.org/zh-cn/3/tutorial/classes.html#generators "永久链接至标题")

[生成器](https://docs.python.org/zh-cn/3/glossary.html#term-generator)  是一个用于创建迭代器的简单而强大的工具。 它们的写法类似于标准的函数，但当它们要返回数据时会使用  [`yield`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#yield)  语句。 每次在生成器上调用  [`next()`](https://docs.python.org/zh-cn/3/library/functions.html#next "next")  时，它会从上次离开的位置恢复执行（它会记住上次执行语句时的所有数据值）。 一个显示如何非常容易地创建生成器的示例如下:

def reverse(data):
    for index in range(len(data)-1, -1, -1):
        yield data[index]

>>>

>>> for char in reverse('golf'):
...     print(char)
...
f
l
o
g

可以用生成器来完成的操作同样可以用前一节所描述的基于类的迭代器来完成。 但生成器的写法更为紧凑，因为它会自动创建  [`__iter__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__iter__ "object.__iter__")  和  [`__next__()`](https://docs.python.org/zh-cn/3/reference/expressions.html#generator.__next__ "generator.__next__")  方法。

另一个关键特性在于局部变量和执行状态会在每次调用之间自动保存。 这使得该函数相比使用  `self.index`  和  `self.data`  这种实例变量的方式更易编写且更为清晰。

除了会自动创建方法和保存程序状态，当生成器终结时，它们还会自动引发  [`StopIteration`](https://docs.python.org/zh-cn/3/library/exceptions.html#StopIteration "StopIteration")。 这些特性结合在一起，使得创建迭代器能与编写常规函数一样容易。

## 9.10. 生成器表达式[](https://docs.python.org/zh-cn/3/tutorial/classes.html#generator-expressions "永久链接至标题")

某些简单的生成器可以写成简洁的表达式代码，所用语法类似列表推导式，将外层为圆括号而非方括号。 这种表达式被设计用于生成器将立即被外层函数所使用的情况。 生成器表达式相比完整的生成器更紧凑但较不灵活，相比等效的列表推导式则更为节省内存。

示例:

>>>

>>> sum(i*i for i in range(10))                 # sum of squares
285

>>> xvec = [10, 20, 30]
>>> yvec = [7, 5, 3]
>>> sum(x*y for x,y in zip(xvec, yvec))         # dot product
260

>>> unique_words = set(word for line in page  for word in line.split())

>>> valedictorian = max((student.gpa, student.name) for student in graduates)

>>> data = 'golf'
>>> list(data[i] for i in range(len(data)-1, -1, -1))
['f', 'l', 'o', 'g']

备注

[1](https://docs.python.org/zh-cn/3/tutorial/classes.html#id1)

存在一个例外。 模块对象有一个秘密的只读属性  [`__dict__`](https://docs.python.org/zh-cn/3/library/stdtypes.html#object.__dict__ "object.__dict__")，它返回用于实现模块命名空间的字典；[`__dict__`](https://docs.python.org/zh-cn/3/library/stdtypes.html#object.__dict__ "object.__dict__")  是属性但不是全局名称。 显然，使用这个将违反命名空间实现的抽象，应当仅被用于事后调试器之类的场合。