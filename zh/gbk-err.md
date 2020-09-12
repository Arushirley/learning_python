
# [PYTHON中读取TXT文本出现“ 'GBK' CODEC CAN'T DECODE BYTE 0XBF IN POSITION 2: ILLEGAL MULTIBYTE SEQUENCE”的解决办法](https://www.cnblogs.com/chuxin-sweet/p/9401824.html)

UnicodeDecodeError: 'gbk' codec can't decode byte 0xbf in position 2: illegal multibyte sequence

今天练习通过读取英文版的Walden.txt的文本信息，统计文本中的英文单词词频的时候出现了这样的错误提示。

错误的意思是：Unicode的解码（Decode）出现错误了，以gbk编码的方式去解码（该字符串变成Unicode），但是此处通过gbk的方式，却无法解码（can't decode）.''illegal multibyte sequence"的意思是非法的多字节序列，也就是说无法解码了。

出现这样的错误，可能是要处理的字符串本身不是gbk编码，却是以gbk编码去解码。比如，字符串本身是utf-8的，但用gbk去解码，必然出错。

针对以上的这个问题，查阅网上资料，可以按照如下的步骤进行尝试：

（1）在打开文本时候，可以指明打开方式：

file = open(path, encoding='gbk')

（2）如果上一步还不能解决，可能是文本中出现的一些特殊符号超出了gbk的编码范围，可以选择编码范围更广的‘gb18030’，如：

 file = open(path, encoding='gb18030'）

（3）如果（2）还不能解决，说明文中出现了连‘gb18030'也无法编码的字符，可以使用‘ignore’属性忽略非法字符，如：

file = open(path, encoding='gb18030', errors='ignore')

或者：

file=open(path).read().decode(‘gb18030’,’ignore’)

通过尝试，基本解决问题，源代码如下：

```
path =  'E://Python/Walden.txt'

file  =  open(path,encoding =  'gb18030',errors =  'ignore')

file2 =  open('E://Python/Walden2.txt','w')

file2.write(file.read())

file.close()

file2.close()

with open('E://Python/Walden2.txt','r') as text:

words =  text.read().split()

print(words)

for  word in  words:

print('{}-{} times'.format(word,words.count(word)))
```

结果如图：

![](https://images2018.cnblogs.com/blog/1433419/201808/1433419-20180801154537767-1913923446.png)

虽然已经能够区分各个单词，但还有一定的问题，如大小写重复统计，字符-的统计，还需要进一步改进。

总结：

Python文件读写的几种模式：

r, rb ,w ,wb 那么在读写文件时，有无b标识的主要区别在哪里呢？

1. 文件使用方式标识

‘r’: 默认值，表示从文件读取数据。

‘w’: 表示要向文件写入数据，并截断从前的内容

‘a’：表示要向文件写入数据，添加到当前内容尾部

‘r+’ ：表示对文件进行可读写操作（删除以前的所有数据）

‘r+a’：表示对文件可进行读写操作（添加到当前文件尾部）

‘b’：表示要读写二进制数据

2. 读文件

进行读文件操作时，直到读到文档结束符（EOF）才算读取到文件最后，Python会认为字节\x1A（26）转换成的字符为文档结束符（EOF），故使用‘r’进行读取二进制文件时，可能会出现文档读取不全的现象。

例如：二进制文件中存在如下从低位向高位排列的数据：7F 32 1A 2F 3D 2C 12 2E 76

如果使用‘r’进行读取，则读到第三个字节，即认为文件结束。

如果使用‘rb’按照二进制位进行读取的，不会将读取的字节转换成字符，从而避免了上面的错误。

解决方案： 二进制文件就用二进制方法读取‘rb’

总结：

使用‘r’的时候，如果碰到‘0x1A’，就视为文件结束，就是EOF。使用‘rb’则不存在这个问题，即：如果你用二进制写入再用文件读出的话，如果其中存在‘0x1A’，就只会读出文件的一部分，使用‘rb’会一直读取文件末尾。

3.写文件

对于字符串x='abc\ndef'，我们可用len(x)得到它的长度为7，\n我们称之为换行符，实际上就是0x0A。当我们用‘w’即文本方式写的时候，在windows平台上会自动将‘0x0A’变成两个字符‘0x0D’,'0x0A',即文件长度实际上变成8。当用‘r’文本方式读取时，又自动的转换成原来的换行符。如果换成‘wb’二进制方式来写的话，则会保持一个字符不变，读取的时候也是原样读取。所以如果用文本方式写入，用二进制方式读取的话，就要考虑这多出的一个字节了。‘0x0D’也称回车符。Linux下不会变，因为Linux只使用‘0x0A’来表示换行。

分类:  [Python基础](https://www.cnblogs.com/chuxin-sweet/category/1255185.html)