
# 10. 标准库简介[¶](https://docs.python.org/zh-cn/3/tutorial/stdlib.html#brief-tour-of-the-standard-library "永久链接至标题")

## 10.1. 操作系统接口[](https://docs.python.org/zh-cn/3/tutorial/stdlib.html#operating-system-interface "永久链接至标题")

[`os`](https://docs.python.org/zh-cn/3/library/os.html#module-os "os: Miscellaneous operating system interfaces.")  模块提供了许多与操作系统交互的函数:

>>>

>>> import os
>>> os.getcwd()      # Return the current working directory
'C:\\Python38'
>>> os.chdir('/server/accesslogs')   # Change current working directory
>>> os.system('mkdir today')   # Run the command mkdir in the system shell
0

一定要使用  `import  os`  而不是  `from  os  import  *`  。这将避免内建的  [`open()`](https://docs.python.org/zh-cn/3/library/functions.html#open "open")  函数被  [`os.open()`](https://docs.python.org/zh-cn/3/library/os.html#os.open "os.open")  隐式替换掉，它们的使用方式大不相同。

内置的  [`dir()`](https://docs.python.org/zh-cn/3/library/functions.html#dir "dir")  和  [`help()`](https://docs.python.org/zh-cn/3/library/functions.html#help "help")  函数可用作交互式辅助工具，用于处理大型模块，如  [`os`](https://docs.python.org/zh-cn/3/library/os.html#module-os "os: Miscellaneous operating system interfaces."):

>>>

>>> import os
>>> dir(os)
<returns a list of all module functions>
>>> help(os)
<returns an extensive manual page created from the module's docstrings>

对于日常文件和目录管理任务，  [`shutil`](https://docs.python.org/zh-cn/3/library/shutil.html#module-shutil "shutil: High-level file operations, including copying.")  模块提供了更易于使用的更高级别的接口:

>>>

>>> import shutil
>>> shutil.copyfile('data.db', 'archive.db')
'archive.db'
>>> shutil.move('/build/executables', 'installdir')
'installdir'

## 10.2. 文件通配符[](https://docs.python.org/zh-cn/3/tutorial/stdlib.html#file-wildcards "永久链接至标题")

[`glob`](https://docs.python.org/zh-cn/3/library/glob.html#module-glob "glob: Unix shell style pathname pattern expansion.")  模块提供了一个在目录中使用通配符搜索创建文件列表的函数:

>>>

>>> import glob
>>> glob.glob('*.py')
['primes.py', 'random.py', 'quote.py']

## 10.3. 命令行参数[](https://docs.python.org/zh-cn/3/tutorial/stdlib.html#command-line-arguments "永久链接至标题")

通用实用程序脚本通常需要处理命令行参数。这些参数作为列表存储在  [`sys`](https://docs.python.org/zh-cn/3/library/sys.html#module-sys "sys: Access system-specific parameters and functions.")  模块的  _argv_  属性中。例如，以下输出来自在命令行运行  `python  demo.py  one  two  three`

>>>

>>> import sys
>>> print(sys.argv)
['demo.py', 'one', 'two', 'three']

[`argparse`](https://docs.python.org/zh-cn/3/library/argparse.html#module-argparse "argparse: Command-line option and argument parsing library.")  模块提供了一种更复杂的机制来处理命令行参数。 以下脚本可提取一个或多个文件名，并可选择要显示的行数:

import argparse

parser = argparse.ArgumentParser(prog = 'top',
    description = 'Show top lines from each file')
parser.add_argument('filenames', nargs='+')
parser.add_argument('-l', '--lines', type=int, default=10)
args = parser.parse_args()
print(args)

当在通过  `python  top.py  --lines=5  alpha.txt  beta.txt`  在命令行运行时，该脚本会将  `args.lines`  设为  `5`  并将  `args.filenames`  设为  `['alpha.txt',  'beta.txt']`。

## 10.4. 错误输出重定向和程序终止[](https://docs.python.org/zh-cn/3/tutorial/stdlib.html#error-output-redirection-and-program-termination "永久链接至标题")

[`sys`](https://docs.python.org/zh-cn/3/library/sys.html#module-sys "sys: Access system-specific parameters and functions.")  模块还具有  _stdin_  ，  _stdout_  和  _stderr_  的属性。后者对于发出警告和错误消息非常有用，即使在  _stdout_  被重定向后也可以看到它们:

>>>

>>> sys.stderr.write('Warning, log file not found starting a new one\n')
Warning, log file not found starting a new one

终止脚本的最直接方法是使用  `sys.exit()`  。

## 10.5. 字符串模式匹配[](https://docs.python.org/zh-cn/3/tutorial/stdlib.html#string-pattern-matching "永久链接至标题")

[`re`](https://docs.python.org/zh-cn/3/library/re.html#module-re "re: Regular expression operations.")  模块为高级字符串处理提供正则表达式工具。对于复杂的匹配和操作，正则表达式提供简洁，优化的解决方案:

>>>

>>> import re
>>> re.findall(r'\bf[a-z]*', 'which foot or hand fell fastest')
['foot', 'fell', 'fastest']
>>> re.sub(r'(\b[a-z]+) \1', r'\1', 'cat in the the hat')
'cat in the hat'

当只需要简单的功能时，首选字符串方法因为它们更容易阅读和调试:

>>>

>>> 'tea for too'.replace('too', 'two')
'tea for two'

## 10.6. 数学[](https://docs.python.org/zh-cn/3/tutorial/stdlib.html#mathematics "永久链接至标题")

[`math`](https://docs.python.org/zh-cn/3/library/math.html#module-math "math: Mathematical functions (sin() etc.).")  模块提供对浮点数学的底层C库函数的访问:

>>>

>>> import math
>>> math.cos(math.pi / 4)
0.70710678118654757
>>> math.log(1024, 2)
10.0

[`random`](https://docs.python.org/zh-cn/3/library/random.html#module-random "random: Generate pseudo-random numbers with various common distributions.")  模块提供了进行随机选择的工具:

>>>

>>> import random
>>> random.choice(['apple', 'pear', 'banana'])
'apple'
>>> random.sample(range(100), 10)   # sampling without replacement
[30, 83, 16, 4, 8, 81, 41, 50, 18, 33]
>>> random.random()    # random float
0.17970987693706186
>>> random.randrange(6)    # random integer chosen from range(6)
4

[`statistics`](https://docs.python.org/zh-cn/3/library/statistics.html#module-statistics "statistics: Mathematical statistics functions")  模块计算数值数据的基本统计属性（均值，中位数，方差等）:

>>>

>>> import statistics
>>> data = [2.75, 1.75, 1.25, 0.25, 0.5, 1.25, 3.5]
>>> statistics.mean(data)
1.6071428571428572
>>> statistics.median(data)
1.25
>>> statistics.variance(data)
1.3720238095238095

SciPy项目 <[https://scipy.org](https://scipy.org/)> 有许多其他模块用于数值计算。

## 10.7. 互联网访问[](https://docs.python.org/zh-cn/3/tutorial/stdlib.html#internet-access "永久链接至标题")

有许多模块可用于访问互联网和处理互联网协议。其中两个最简单的  [`urllib.request`](https://docs.python.org/zh-cn/3/library/urllib.request.html#module-urllib.request "urllib.request: Extensible library for opening URLs.")  用于从URL检索数据，以及  [`smtplib`](https://docs.python.org/zh-cn/3/library/smtplib.html#module-smtplib "smtplib: SMTP protocol client (requires sockets).")  用于发送邮件:

>>>

>>> from urllib.request import urlopen
>>> with urlopen('http://tycho.usno.navy.mil/cgi-bin/timer.pl') as response:
...     for line in response:
...         line = line.decode('utf-8')  # Decoding the binary data to text.
...         if 'EST' in line or 'EDT' in line:  # look for Eastern Time
...             print(line)

<BR>Nov. 25, 09:43:32 PM EST

>>> import smtplib
>>> server = smtplib.SMTP('localhost')
>>> server.sendmail('soothsayer@example.org', 'jcaesar@example.org',
... """To: jcaesar@example.org
... From: soothsayer@example.org
...
... Beware the Ides of March.
... """)
>>> server.quit()

（请注意，第二个示例需要在localhost上运行的邮件服务器。）

## 10.8. 日期和时间[](https://docs.python.org/zh-cn/3/tutorial/stdlib.html#dates-and-times "永久链接至标题")

[`datetime`](https://docs.python.org/zh-cn/3/library/datetime.html#module-datetime "datetime: Basic date and time types.")  模块提供了以简单和复杂的方式操作日期和时间的类。虽然支持日期和时间算法，但实现的重点是有效的成员提取以进行输出格式化和操作。该模块还支持可感知时区的对象。

>>>

>>> # dates are easily constructed and formatted
>>> from datetime import date
>>> now = date.today()
>>> now
datetime.date(2003, 12, 2)
>>> now.strftime("%m-%d-%y. %d %b %Y is a %A on the %d day of %B.")
'12-02-03. 02 Dec 2003 is a Tuesday on the 02 day of December.'

>>> # dates support calendar arithmetic
>>> birthday = date(1964, 7, 31)
>>> age = now - birthday
>>> age.days
14368

## 10.9. 数据压缩[](https://docs.python.org/zh-cn/3/tutorial/stdlib.html#data-compression "永久链接至标题")

常见的数据存档和压缩格式由模块直接支持，包括：[`zlib`](https://docs.python.org/zh-cn/3/library/zlib.html#module-zlib "zlib: Low-level interface to compression and decompression routines compatible with gzip."),  [`gzip`](https://docs.python.org/zh-cn/3/library/gzip.html#module-gzip "gzip: Interfaces for gzip compression and decompression using file objects."),  [`bz2`](https://docs.python.org/zh-cn/3/library/bz2.html#module-bz2 "bz2: Interfaces for bzip2 compression and decompression."),  [`lzma`](https://docs.python.org/zh-cn/3/library/lzma.html#module-lzma "lzma: A Python wrapper for the liblzma compression library."),  [`zipfile`](https://docs.python.org/zh-cn/3/library/zipfile.html#module-zipfile "zipfile: Read and write ZIP-format archive files.")  和  [`tarfile`](https://docs.python.org/zh-cn/3/library/tarfile.html#module-tarfile "tarfile: Read and write tar-format archive files.")。:

>>>

>>> import zlib
>>> s = b'witch which has which witches wrist watch'
>>> len(s)
41
>>> t = zlib.compress(s)
>>> len(t)
37
>>> zlib.decompress(t)
b'witch which has which witches wrist watch'
>>> zlib.crc32(s)
226805979

## 10.10. 性能测量[](https://docs.python.org/zh-cn/3/tutorial/stdlib.html#performance-measurement "永久链接至标题")

一些Python用户对了解同一问题的不同方法的相对性能产生了浓厚的兴趣。 Python提供了一种可以立即回答这些问题的测量工具。

例如，元组封包和拆包功能相比传统的交换参数可能更具吸引力。[`timeit`](https://docs.python.org/zh-cn/3/library/timeit.html#module-timeit "timeit: Measure the execution time of small code snippets.")  模块可以快速演示在运行效率方面一定的优势:

>>>

>>> from timeit import Timer
>>> Timer('t=a; a=b; b=t', 'a=1; b=2').timeit()
0.57535828626024577
>>> Timer('a,b = b,a', 'a=1; b=2').timeit()
0.54962537085770791

与  [`timeit`](https://docs.python.org/zh-cn/3/library/timeit.html#module-timeit "timeit: Measure the execution time of small code snippets.")  的精细粒度级别相反，  [`profile`](https://docs.python.org/zh-cn/3/library/profile.html#module-profile "profile: Python source profiler.")  和  [`pstats`](https://docs.python.org/zh-cn/3/library/profile.html#module-pstats "pstats: Statistics object for use with the profiler.")  模块提供了用于在较大的代码块中识别时间关键部分的工具。

## 10.11. 质量控制[](https://docs.python.org/zh-cn/3/tutorial/stdlib.html#quality-control "永久链接至标题")

开发高质量软件的一种方法是在开发过程中为每个函数编写测试，并在开发过程中经常运行这些测试。

[`doctest`](https://docs.python.org/zh-cn/3/library/doctest.html#module-doctest "doctest: Test pieces of code within docstrings.")  模块提供了一个工具，用于扫描模块并验证程序文档字符串中嵌入的测试。测试构造就像将典型调用及其结果剪切并粘贴到文档字符串一样简单。这通过向用户提供示例来改进文档，并且它允许doctest模块确保代码保持对文档的真实:

def average(values):
    """Computes the arithmetic mean of a list of numbers.

 >>> print(average([20, 30, 70]))
 40.0
 """
    return sum(values) / len(values)

import doctest
doctest.testmod()   # automatically validate the embedded tests

[`unittest`](https://docs.python.org/zh-cn/3/library/unittest.html#module-unittest "unittest: Unit testing framework for Python.")  模块不像  [`doctest`](https://docs.python.org/zh-cn/3/library/doctest.html#module-doctest "doctest: Test pieces of code within docstrings.")  模块那样易于使用，但它允许在一个单独的文件中维护更全面的测试集:

import unittest

class TestStatisticalFunctions(unittest.TestCase):

    def test_average(self):
        self.assertEqual(average([20, 30, 70]), 40.0)
        self.assertEqual(round(average([1, 5, 7]), 1), 4.3)
        with self.assertRaises(ZeroDivisionError):
            average([])
        with self.assertRaises(TypeError):
            average(20, 30, 70)

unittest.main()  # Calling from the command line invokes all tests

## 10.12. 自带电池[](https://docs.python.org/zh-cn/3/tutorial/stdlib.html#batteries-included "永久链接至标题")

Python有“自带电池”的理念。通过其包的复杂和强大功能可以最好地看到这一点。例如:

-   [`xmlrpc.client`](https://docs.python.org/zh-cn/3/library/xmlrpc.client.html#module-xmlrpc.client "xmlrpc.client: XML-RPC client access.")  和  [`xmlrpc.server`](https://docs.python.org/zh-cn/3/library/xmlrpc.server.html#module-xmlrpc.server "xmlrpc.server: Basic XML-RPC server implementations.")  模块使得实现远程过程调用变成了小菜一碟。 尽管存在于模块名称中，但用户不需要直接了解或处理 XML。
    
-   [`email`](https://docs.python.org/zh-cn/3/library/email.html#module-email "email: Package supporting the parsing, manipulating, and generating email messages.")  包是一个用于管理电子邮件的库，包括MIME和其他符合  [**RFC 2822**](https://tools.ietf.org/html/rfc2822.html)  规范的邮件文档。与  [`smtplib`](https://docs.python.org/zh-cn/3/library/smtplib.html#module-smtplib "smtplib: SMTP protocol client (requires sockets).")  和  [`poplib`](https://docs.python.org/zh-cn/3/library/poplib.html#module-poplib "poplib: POP3 protocol client (requires sockets).")  不同（它们实际上做的是发送和接收消息），电子邮件包提供完整的工具集，用于构建或解码复杂的消息结构（包括附件）以及实现互联网编码和标头协议。
    
-   [`json`](https://docs.python.org/zh-cn/3/library/json.html#module-json "json: Encode and decode the JSON format.")  包为解析这种流行的数据交换格式提供了强大的支持。  [`csv`](https://docs.python.org/zh-cn/3/library/csv.html#module-csv "csv: Write and read tabular data to and from delimited files.")  模块支持以逗号分隔值格式直接读取和写入文件，这种格式通常为数据库和电子表格所支持。 XML 处理由  [`xml.etree.ElementTree`](https://docs.python.org/zh-cn/3/library/xml.etree.elementtree.html#module-xml.etree.ElementTree "xml.etree.ElementTree: Implementation of the ElementTree API.")  ，  [`xml.dom`](https://docs.python.org/zh-cn/3/library/xml.dom.html#module-xml.dom "xml.dom: Document Object Model API for Python.")  和  [`xml.sax`](https://docs.python.org/zh-cn/3/library/xml.sax.html#module-xml.sax "xml.sax: Package containing SAX2 base classes and convenience functions.")  包支持。这些模块和软件包共同大大简化了 Python 应用程序和其他工具之间的数据交换。
    
-   [`sqlite3`](https://docs.python.org/zh-cn/3/library/sqlite3.html#module-sqlite3 "sqlite3: A DB-API 2.0 implementation using SQLite 3.x.")  模块是 SQLite 数据库库的包装器，提供了一个可以使用稍微非标准的 SQL 语法更新和访问的持久数据库。
    
-   国际化由许多模块支持，包括  [`gettext`](https://docs.python.org/zh-cn/3/library/gettext.html#module-gettext "gettext: Multilingual internationalization services.")  ，  [`locale`](https://docs.python.org/zh-cn/3/library/locale.html#module-locale "locale: Internationalization services.")  ，以及  [`codecs`](https://docs.python.org/zh-cn/3/library/codecs.html#module-codecs "codecs: Encode and decode data and streams.")  包。


# 11. 标准库简介 —— 第二部分[](https://docs.python.org/zh-cn/3/tutorial/stdlib2.html#brief-tour-of-the-standard-library-part-ii "永久链接至标题")

第二部分涵盖了专业编程所需要的更高级的模块。这些模块很少用在小脚本中。

## 11.1. 格式化输出[](https://docs.python.org/zh-cn/3/tutorial/stdlib2.html#output-formatting "永久链接至标题")

[`reprlib`](https://docs.python.org/zh-cn/3/library/reprlib.html#module-reprlib "reprlib: Alternate repr() implementation with size limits.")  模块提供了一个定制化版本的  [`repr()`](https://docs.python.org/zh-cn/3/library/functions.html#repr "repr")  函数，用于缩略显示大型或深层嵌套的容器对象:

>>>

>>> import reprlib
>>> reprlib.repr(set('supercalifragilisticexpialidocious'))
"{'a', 'c', 'd', 'e', 'f', 'g', ...}"

[`pprint`](https://docs.python.org/zh-cn/3/library/pprint.html#module-pprint "pprint: Data pretty printer.")  模块提供了更加复杂的打印控制，其输出的内置对象和用户自定义对象能够被解释器直接读取。当输出结果过长而需要折行时，“美化输出机制”会添加换行符和缩进，以更清楚地展示数据结构:

>>>

>>> import pprint
>>> t = [[[['black', 'cyan'], 'white', ['green', 'red']], [['magenta',
...     'yellow'], 'blue']]]
...
>>> pprint.pprint(t, width=30)
[[[['black', 'cyan'],
 'white',
 ['green', 'red']],
 [['magenta', 'yellow'],
 'blue']]]

[`textwrap`](https://docs.python.org/zh-cn/3/library/textwrap.html#module-textwrap "textwrap: Text wrapping and filling")  模块能够格式化文本段落，以适应给定的屏幕宽度:

>>>

>>> import textwrap
>>> doc = """The wrap() method is just like fill() except that it returns
... a list of strings instead of one big string with newlines to separate
... the wrapped lines."""
...
>>> print(textwrap.fill(doc, width=40))
The wrap() method is just like fill()
except that it returns a list of strings
instead of one big string with newlines
to separate the wrapped lines.

[`locale`](https://docs.python.org/zh-cn/3/library/locale.html#module-locale "locale: Internationalization services.")  模块处理与特定地域文化相关的数据格式。locale 模块的 format 函数包含一个 grouping 属性，可直接将数字格式化为带有组分隔符的样式:

>>>

>>> import locale
>>> locale.setlocale(locale.LC_ALL, 'English_United States.1252')
'English_United States.1252'
>>> conv = locale.localeconv()          # get a mapping of conventions
>>> x = 1234567.8
>>> locale.format("%d", x, grouping=True)
'1,234,567'
>>> locale.format_string("%s%.*f", (conv['currency_symbol'],
...                      conv['frac_digits'], x), grouping=True)
'$1,234,567.80'

## 11.2. 模板[](https://docs.python.org/zh-cn/3/tutorial/stdlib2.html#templating "永久链接至标题")

[`string`](https://docs.python.org/zh-cn/3/library/string.html#module-string "string: Common string operations.")  模块包含一个通用的  [`Template`](https://docs.python.org/zh-cn/3/library/string.html#string.Template "string.Template")  类，具有适用于最终用户的简化语法。它允许用户在不更改应用逻辑的情况下定制自己的应用。

上述格式化操作是通过占位符实现的，占位符由  `$`  加上合法的 Python 标识符（只能包含字母、数字和下划线）构成。一旦使用花括号将占位符括起来，就可以在后面直接跟上更多的字母和数字而无需空格分割。`$$`  将被转义成单个字符  `$`:

>>>

>>> from string import Template
>>> t = Template('${village}folk send $$10 to $cause.')
>>> t.substitute(village='Nottingham', cause='the ditch fund')
'Nottinghamfolk send $10 to the ditch fund.'

如果在字典或关键字参数中未提供某个占位符的值，那么  [`substitute()`](https://docs.python.org/zh-cn/3/library/string.html#string.Template.substitute "string.Template.substitute") 方法将抛出  [`KeyError`](https://docs.python.org/zh-cn/3/library/exceptions.html#KeyError "KeyError")。对于邮件合并类型的应用，用户提供的数据有可能是不完整的，此时使用  [`safe_substitute()`](https://docs.python.org/zh-cn/3/library/string.html#string.Template.safe_substitute "string.Template.safe_substitute")  方法更加合适 —— 如果数据缺失，它会直接将占位符原样保留。

>>>

>>> t = Template('Return the $item to $owner.')
>>> d = dict(item='unladen swallow')
>>> t.substitute(d)
Traceback (most recent call last):
  ...
KeyError: 'owner'
>>> t.safe_substitute(d)
'Return the unladen swallow to $owner.'

Template 的子类可以自定义定界符。例如，以下是某个照片浏览器的批量重命名功能，采用了百分号作为日期、照片序号和照片格式的占位符:

>>>

>>> import time, os.path
>>> photofiles = ['img_1074.jpg', 'img_1076.jpg', 'img_1077.jpg']
>>> class BatchRename(Template):
...     delimiter = '%'
>>> fmt = input('Enter rename style (%d-date %n-seqnum %f-format):  ')
Enter rename style (%d-date %n-seqnum %f-format):  Ashley_%n%f

>>> t = BatchRename(fmt)
>>> date = time.strftime('%d%b%y')
>>> for i, filename in enumerate(photofiles):
...     base, ext = os.path.splitext(filename)
...     newname = t.substitute(d=date, n=i, f=ext)
...     print('{0} --> {1}'.format(filename, newname))

img_1074.jpg --> Ashley_0.jpg
img_1076.jpg --> Ashley_1.jpg
img_1077.jpg --> Ashley_2.jpg

模板的另一个应用是将程序逻辑与多样的格式化输出细节分离开来。这使得对 XML 文件、纯文本报表和 HTML 网络报表使用自定义模板成为可能。

## 11.3. 使用二进制数据记录格式[](https://docs.python.org/zh-cn/3/tutorial/stdlib2.html#working-with-binary-data-record-layouts "永久链接至标题")

[`struct`](https://docs.python.org/zh-cn/3/library/struct.html#module-struct "struct: Interpret bytes as packed binary data.")  模块提供了  [`pack()`](https://docs.python.org/zh-cn/3/library/struct.html#struct.pack "struct.pack")  和  [`unpack()`](https://docs.python.org/zh-cn/3/library/struct.html#struct.unpack "struct.unpack")  函数，用于处理不定长度的二进制记录格式。下面的例子展示了在不使用  [`zipfile`](https://docs.python.org/zh-cn/3/library/zipfile.html#module-zipfile "zipfile: Read and write ZIP-format archive files.")  模块的情况下，如何循环遍历一个 ZIP 文件的所有头信息。Pack 代码  `"H"`  和  `"I"`  分别代表两字节和四字节无符号整数。`"<"`  代表它们是标准尺寸的小尾型字节序:

import struct

with open('myfile.zip', 'rb') as f:
    data = f.read()

start = 0
for i in range(3):                      # show the first 3 file headers
    start += 14
    fields = struct.unpack('<IIIHH', data[start:start+16])
    crc32, comp_size, uncomp_size, filenamesize, extra_size = fields

    start += 16
    filename = data[start:start+filenamesize]
    start += filenamesize
    extra = data[start:start+extra_size]
    print(filename, hex(crc32), comp_size, uncomp_size)

    start += extra_size + comp_size     # skip to the next header

## 11.4. 多线程[](https://docs.python.org/zh-cn/3/tutorial/stdlib2.html#multi-threading "永久链接至标题")

线程是一种对于非顺序依赖的多个任务进行解耦的技术。多线程可以提高应用的响应效率，当接收用户输入的同时，保持其他任务在后台运行。一个有关的应用场景是，将 I/O 和计算运行在两个并行的线程中。

以下代码展示了高阶的  [`threading`](https://docs.python.org/zh-cn/3/library/threading.html#module-threading "threading: Thread-based parallelism.")  模块如何在后台运行任务，且不影响主程序的继续运行:

import threading, zipfile

class AsyncZip(threading.Thread):
    def __init__(self, infile, outfile):
        threading.Thread.__init__(self)
        self.infile = infile
        self.outfile = outfile

    def run(self):
        f = zipfile.ZipFile(self.outfile, 'w', zipfile.ZIP_DEFLATED)
        f.write(self.infile)
        f.close()
        print('Finished background zip of:', self.infile)

background = AsyncZip('mydata.txt', 'myarchive.zip')
background.start()
print('The main program continues to run in foreground.')

background.join()    # Wait for the background task to finish
print('Main program waited until background was done.')

多线程应用面临的主要挑战是，相互协调的多个线程之间需要共享数据或其他资源。为此，threading 模块提供了多个同步操作原语，包括线程锁、事件、条件变量和信号量。

尽管这些工具非常强大，但微小的设计错误却可以导致一些难以复现的问题。因此，实现多任务协作的首选方法是将对资源的所有请求集中到一个线程中，然后使用  [`queue`](https://docs.python.org/zh-cn/3/library/queue.html#module-queue "queue: A synchronized queue class.")  模块向该线程供应来自其他线程的请求。应用程序使用  [`Queue`](https://docs.python.org/zh-cn/3/library/queue.html#queue.Queue "queue.Queue") 对象进行线程间通信和协调，更易于设计，更易读，更可靠。

## 11.5. 日志记录[](https://docs.python.org/zh-cn/3/tutorial/stdlib2.html#logging "永久链接至标题")

[`logging`](https://docs.python.org/zh-cn/3/library/logging.html#module-logging "logging: Flexible event logging system for applications.")  模块提供功能齐全且灵活的日志记录系统。在最简单的情况下，日志消息被发送到文件或  `sys.stderr`

import logging
logging.debug('Debugging information')
logging.info('Informational message')
logging.warning('Warning:config file %s not found', 'server.conf')
logging.error('Error occurred')
logging.critical('Critical error -- shutting down')

这会产生以下输出:

WARNING:root:Warning:config file server.conf not found
ERROR:root:Error occurred
CRITICAL:root:Critical error -- shutting down

默认情况下，informational 和 debugging 消息被压制，输出会发送到标准错误流。其他输出选项包括将消息转发到电子邮件，数据报，套接字或 HTTP 服务器。新的过滤器可以根据消息优先级选择不同的路由方式：`DEBUG`，`INFO`，`WARNING`，`ERROR`，和  `CRITICAL`。

日志系统可以直接从 Python 配置，也可以从用户配置文件加载，以便自定义日志记录而无需更改应用程序。

## 11.6. 弱引用[](https://docs.python.org/zh-cn/3/tutorial/stdlib2.html#weak-references "永久链接至标题")

Python 会自动进行内存管理（对大多数对象进行引用计数并使用  [garbage collection](https://docs.python.org/zh-cn/3/glossary.html#term-garbage-collection)  来清除循环引用）。 当某个对象的最后一个引用被移除后不久就会释放其所占用的内存。

此方式对大多数应用来说都适用，但偶尔也必须在对象持续被其他对象所使用时跟踪它们。 不幸的是，跟踪它们将创建一个会令其永久化的引用。  [`weakref`](https://docs.python.org/zh-cn/3/library/weakref.html#module-weakref "weakref: Support for weak references and weak dictionaries.")  模块提供的工具可以不必创建引用就能跟踪对象。 当对象不再需要时，它将自动从一个弱引用表中被移除，并为弱引用对象触发一个回调。 典型应用包括对创建开销较大的对象进行缓存:

>>>

>>> import weakref, gc
>>> class A:
...     def __init__(self, value):
...         self.value = value
...     def __repr__(self):
...         return str(self.value)
...
>>> a = A(10)                   # create a reference
>>> d = weakref.WeakValueDictionary()
>>> d['primary'] = a            # does not create a reference
>>> d['primary']                # fetch the object if it is still alive
10
>>> del a                       # remove the one reference
>>> gc.collect()                # run garbage collection right away
0
>>> d['primary']                # entry was automatically removed
Traceback (most recent call last): File "<stdin>", line 1, in <module>
    d['primary']                # entry was automatically removed File "C:/python38/lib/weakref.py", line 46, in __getitem__
    o = self.data[key]()
KeyError: 'primary'

## 11.7. 用于操作列表的工具[](https://docs.python.org/zh-cn/3/tutorial/stdlib2.html#tools-for-working-with-lists "永久链接至标题")

许多对于数据结构的需求可以通过内置列表类型来满足。 但是，有时也会需要具有不同效费比的替代实现。

[`array`](https://docs.python.org/zh-cn/3/library/array.html#module-array "array: Space efficient arrays of uniformly typed numeric values.")  模块提供了一种  [`array()`](https://docs.python.org/zh-cn/3/library/array.html#array.array "array.array")  对象，它类似于列表，但只能存储类型一致的数据且存储密集更高。 下面的例子演示了一个以两个字节为存储单元的无符号二进制数值的数组 (类型码为  `"H"`)，而对于普通列表来说，每个条目存储为标准 Python 的 int 对象通常要占用16 个字节:

>>>

>>> from array import array
>>> a = array('H', [4000, 10, 700, 22222])
>>> sum(a)
26932
>>> a[1:3]
array('H', [10, 700])

[`collections`](https://docs.python.org/zh-cn/3/library/collections.html#module-collections "collections: Container datatypes")  模块提供了一种  [`deque()`](https://docs.python.org/zh-cn/3/library/collections.html#collections.deque "collections.deque")  对象，它类似于列表，但从左端添加和弹出的速度较快，而在中间查找的速度较慢。 此种对象适用于实现队列和广度优先树搜索:

>>>

>>> from collections import deque
>>> d = deque(["task1", "task2", "task3"])
>>> d.append("task4")
>>> print("Handling", d.popleft())
Handling task1

unsearched = deque([starting_node])
def breadth_first_search(unsearched):
    node = unsearched.popleft()
    for m in gen_moves(node):
        if is_goal(m):
            return m
        unsearched.append(m)

在替代的列表实现以外，标准库也提供了其他工具，例如  [`bisect`](https://docs.python.org/zh-cn/3/library/bisect.html#module-bisect "bisect: Array bisection algorithms for binary searching.")  模块具有用于操作排序列表的函数:

>>>

>>> import bisect
>>> scores = [(100, 'perl'), (200, 'tcl'), (400, 'lua'), (500, 'python')]
>>> bisect.insort(scores, (300, 'ruby'))
>>> scores
[(100, 'perl'), (200, 'tcl'), (300, 'ruby'), (400, 'lua'), (500, 'python')]

[`heapq`](https://docs.python.org/zh-cn/3/library/heapq.html#module-heapq "heapq: Heap queue algorithm (a.k.a. priority queue).")  模块提供了基于常规列表来实现堆的函数。 最小值的条目总是保持在位置零。 这对于需要重复访问最小元素而不希望运行完整列表排序的应用来说非常有用:

>>>

>>> from heapq import heapify, heappop, heappush
>>> data = [1, 3, 5, 7, 9, 2, 4, 6, 8, 0]
>>> heapify(data)                      # rearrange the list into heap order
>>> heappush(data, -5)                 # add a new entry
>>> [heappop(data) for i in range(3)]  # fetch the three smallest entries
[-5, 0, 1]

## 11.8. 十进制浮点运算[](https://docs.python.org/zh-cn/3/tutorial/stdlib2.html#decimal-floating-point-arithmetic "永久链接至标题")

[`decimal`](https://docs.python.org/zh-cn/3/library/decimal.html#module-decimal "decimal: Implementation of the General Decimal Arithmetic  Specification.")  模块提供了一种  [`Decimal`](https://docs.python.org/zh-cn/3/library/decimal.html#decimal.Decimal "decimal.Decimal")  数据类型用于十进制浮点运算。 相比内置的  [`float`](https://docs.python.org/zh-cn/3/library/functions.html#float "float")  二进制浮点实现，该类特别适用于

-   财务应用和其他需要精确十进制表示的用途，
    
-   控制精度，
    
-   控制四舍五入以满足法律或监管要求，
    
-   跟踪有效小数位，或
    
-   用户期望结果与手工完成的计算相匹配的应用程序。
    

例如，使用十进制浮点和二进制浮点数计算70美分手机和5％税的总费用，会产生的不同结果。如果结果四舍五入到最接近的分数差异会更大:

>>>

>>> from decimal import *
>>> round(Decimal('0.70') * Decimal('1.05'), 2)
Decimal('0.74')
>>> round(.70 * 1.05, 2)
0.73

[`Decimal`](https://docs.python.org/zh-cn/3/library/decimal.html#decimal.Decimal "decimal.Decimal")  表示的结果会保留尾部的零，并根据具有两个有效位的被乘数自动推出四个有效位。 Decimal 可以模拟手工运算来避免当二进制浮点数无法精确表示十进制数时会导致的问题。

精确表示特性使得  [`Decimal`](https://docs.python.org/zh-cn/3/library/decimal.html#decimal.Decimal "decimal.Decimal")  类能够执行对于二进制浮点数来说不适用的模运算和相等性检测:

>>>

>>> Decimal('1.00') % Decimal('.10')
Decimal('0.00')
>>> 1.00 % 0.10
0.09999999999999995

>>> sum([Decimal('0.1')]*10) == Decimal('1.0')
True
>>> sum([0.1]*10) == 1.0
False

[`decimal`](https://docs.python.org/zh-cn/3/library/decimal.html#module-decimal "decimal: Implementation of the General Decimal Arithmetic  Specification.")  模块提供了运算所需要的足够精度:

>>>

>>> getcontext().prec = 36
>>> Decimal(1) / Decimal(7)
Decimal('0.142857142857142857142857142857142857')