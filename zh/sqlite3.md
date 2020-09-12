
# Python操作SQLite3

2019-01-18 15:30:52  [程序猿洋洋](https://me.csdn.net/hhy1107786871)  阅读数 938更多

分类专栏：  [Python](https://blog.csdn.net/hhy1107786871/article/category/8550731)

[](http://creativecommons.org/licenses/by-sa/4.0/)版权声明：本文为博主原创文章，遵循 [CC 4.0 BY-SA](http://creativecommons.org/licenses/by-sa/4.0/) 版权协议，转载请附上原文出处链接和本声明。

本文链接：[https://blog.csdn.net/hhy1107786871/article/details/86540125](https://blog.csdn.net/hhy1107786871/article/details/86540125)

## 连接创建数据库

```python
1.  # connect_sqlite3.py
    
2.  import sqlite3
    

4.  DB_Name = 'test.db'
    
5.  # 连接数据库，如果不存在则会在当前目录创建
    
6.  conn = sqlite3.connect(DB_Name)
    
7.  print('连接数据库%s成功' % (DB_Name))

```

程序执行结果：

```
连接数据库test.db成功
```

# 创建数据库表

```python
# create_table_sqlite3.py
import sqlite3
 
DB_Name = 'test.db'
Table_Name = 'STUDENT'
# 连接数据库，如果不存在则会在当前目录创建
conn = sqlite3.connect(DB_Name)
try:
    # 创建游标
    cursor = conn.cursor()
    # 创建STUDENT表的SQL语句，默认编码为UTF-8
    SQL = '''
      CREATE TABLE %s (
        SNO CHAR(10),
        SNAME VARCHAR(20) NOT NULL,
        PRIMARY KEY(SNO)
    )
        ''' % (Table_Name)
    # 创建数据库表
    cursor.execute(SQL)
 
    # 提交到数据库
    conn.commit()
    print('创建数据库表%s成功' % (Table_Name))
except Exception as e:
    print(e)
    # 回滚
    conn.rollback()
    print('创建数据库表%s失败' % Table_Name)
finally:
    # 关闭数据库
    conn.close()

```
程序执行结果：

```
创建数据库表STUDENT成功
```

# 增删改查

## 插入数据

```python
# insertData_sqlite3.py
import sqlite3
 
DB_Name = 'test.db'
# 连接数据库，如果不存在则会在当前目录创建
conn = sqlite3.connect(DB_Name)
try:
    # 创建游标
    cursor = conn.cursor()
    # 向STUDENT表插入数据的SQL语句
    SQL = '''
          INSERT INTO STUDENT VALUES('2016081111','张三'),('2016081112','李四'),('2016081113','王五');
          '''
    # 插入数据
    cursor.execute(SQL)
 
    # 提交到数据库
    conn.commit()
    print('插入数据到表STUDENT成功')
except Exception as e:
    print(e)
    # 回滚
    conn.rollback()
    print('插入数据到表STUDENT失败')
finally:
    # 关闭数据库
    conn.close()
```

程序执行结果为：

```
插入数据到表STUDENT成功
```

## 查询数据

```python
# selectData_sqlite3.py
import sqlite3
 
DB_Name = 'test.db'
# 连接数据库，如果不存在则会在当前目录创建
conn = sqlite3.connect(DB_Name)
try:
    # 创建游标
    cursor = conn.cursor()
    # 查询数据的SQL语句
    SQL = '''
          SELECT * FROM STUDENT;
          '''
    # 查询数据
    cursor.execute(SQL)
 
    # 获取一条数据
    one = cursor.fetchone()
    print(one)
 
    # 获取所有数据
    for row in cursor.fetchall():
        print(row)
 
except Exception as e:
    print(e)
    print('查询数据失败')
finally:
    # 关闭数据库
    conn.close()
```

程序执行结果为：

```

```

## 修改数据

```
 updateData_sqlite3.py
import sqlite3
 
DB_Name = 'test.db'
# 连接数据库，如果不存在则会在当前目录创建
conn = sqlite3.connect(DB_Name)
try:
    # 创建游标
    cursor = conn.cursor()
    # 查询数据的SQL语句
    SELECT_SQL = '''
          SELECT * FROM STUDENT;
          '''
    # 修改数据的SQL语句
    UPDATE_SQL = '''
             UPDATE STUDENT SET SNAME='%s' WHERE SNO='%s'
             ''' % ('李华', '2016081111')
 
    # 修改前
    print('修改前')
    cursor.execute(SELECT_SQL)
    for row in cursor.fetchall():
        print(row)
    # 修改数据
    cursor.execute(UPDATE_SQL)
    # 提交到数据库
    conn.commit()
 
    # 修改后
    print('修改后')
    cursor.execute(SELECT_SQL)
    for row in cursor.fetchall():
        print(row)
except Exception as e:
    print(e)
    print('修改数据失败')
finally:
    # 关闭数据库
    conn.close()
```

程序执行结果：

```

```

## 删除数据

```python
# deleteData_sqlite3.py
import sqlite3
 
DB_Name = 'test.db'
# 连接数据库，如果不存在则会在当前目录创建
conn = sqlite3.connect(DB_Name)
try:
    # 创建游标
    cursor = conn.cursor()
    # 查询数据的SQL语句
    SELECT_SQL = '''
          SELECT * FROM STUDENT;
          '''
    # 删除数据的SQL语句
    DELETE_SQL = '''
             DELETE FROM STUDENT WHERE SNO='%s'
             ''' % ('2016081111')
 
    # 删除前
    print('删除前')
    cursor.execute(SELECT_SQL)
    for row in cursor.fetchall():
        print(row)
    # 删除数据
    cursor.execute(DELETE_SQL)
    # 提交到数据库
    conn.commit()
 
    # 删除后
    print('删除后')
    cursor.execute(SELECT_SQL)
    for row in cursor.fetchall():
        print(row)
except Exception as e:
    print(e)
    print('删除数据失败')
finally:
    # 关闭数据库
    conn.close()
```

程序执行结果：


1.  删除前
    
2.  ('2016081111', '李华')
    
3.  ('2016081112', '李四')
    
4.  ('2016081113', '王五')
    
5.  删除后
    
6.  ('2016081112', '李四')
    
7.  ('2016081113', '王五')


---


# [用Python进行SQLite数据库操作](https://www.cnblogs.com/yuxc/archive/2011/08/18/2143606.html)

**简单的介绍**

SQLite数据库是一款非常小巧的嵌入式开源数据库软件，也就是说没有独立的维护进程，所有的维护都来自于程序本身。它是遵守ACID的关联式[数据库管理系统](http://baike.baidu.com/view/68446.htm)，它的设计目标是嵌入式的，而且目前已经在很多嵌入式产品中使用了它，它占用资源非常的低，在嵌入式设备中，可能只需要几百K的内存就够了。它能够支持Windows/Linux/Unix等等主流的[操作系统](http://baike.baidu.com/view/880.htm)，同时能够跟很多程序语言相结合，比如 Tcl、C#、PHP、Java等，还有ODBC接口，同样比起Mysql、PostgreSQL这两款开源世界著名的数据库管理系统来讲，它的处理速度比他们都快。SQLite第一个[Alpha版本](http://baike.baidu.com/view/707803.htm)诞生于2000年5月. 至今已经有10个年头，SQLite也迎来了一个版本 SQLite 3已经发布。

**安装与使用**

**1.导入****Python SQLITE数据库模块**

Python2.5之后，内置了SQLite3，成为了内置模块，这给我们省了安装的功夫，只需导入即可~

import sqlite3

  

**2. 创建/打开数据库**  

在调用connect函数的时候，指定库名称，如果指定的数据库存在就直接打开这个数据库，如果不存在就新创建一个再打开。  

cx = sqlite3.connect("E:/test.db")

也可以创建数据库在内存中。

con = sqlite3.connect(":memory:")

**3.数据库连接对象**

打开数据库时返回的对象cx就是一个数据库连接对象，它可以有以下操作：

1.  commit()--事务提交 
2.  rollback()--事务回滚   
3.  close()--关闭一个数据库连接   
4.  cursor()--创建一个游标   
    

关于commit()，如果isolation_level隔离级别默认，那么每次对数据库的操作，都需要使用该命令，你也可以设置isolation_level=None，这样就变为自动提交模式。

**4.使用游标查询数据库**  

我们需要使用游标对象SQL语句查询数据库，获得查询对象。 通过以下方法来定义一个游标。  

cu=cx.cursor()

游标对象有以下的操作：

1.  execute()--执行sql语句 
2.  executemany--执行多条sql语句   
3.  close()--关闭游标   
4.  fetchone()--从结果中取一条记录，并将游标指向下一条记录   
5.  fetchmany()--从结果中取多条记录   
6.  fetchall()--从结果中取出所有记录   
7.  scroll()--游标滚动    
    

**1. 建表**

cu.execute("create table catalog (id integer primary key,pid integer,name varchar(10) UNIQUE,nickname text NULL)")

上面语句创建了一个叫catalog的表，它有一个主键id，一个pid，和一个name，name是不可以重复的，以及一个nickname默认为NULL。

**2. 插入数据**  

请注意避免以下写法：  

# Never do this -- insecure 会导致注入攻击  
  
pid=200  
c.execute("... where pid = '%s'"  % pid)

正确的做法如下，如果t只是单个数值，也要采用t=(n,)的形式，因为元组是不可变的。  

for t in[(0,10,'abc','Yu'),(1,20,'cba','Xu')]:  
cx.execute("insert into catalog values (?,?,?,?)", t)

简单的插入两行数据,不过需要提醒的是,只有提交了之后,才能生效.我们使用数据库连接对象cx来进行提交commit和回滚rollback操作.  

cx.commit()

**3.查询**

cu.execute("select * from catalog")  

要提取查询到的数据,使用游标的fetch函数,如:  

In [10]: cu.fetchall()  
Out[10]: [(0, 10, u'abc', u'Yu'), (1, 20, u'cba', u'Xu')]

如果我们使用cu.fetchone(),则首先返回列表中的第一项,再次使用,则返回第二项,依次下去.

**4.修改**

In [12]: cu.execute("update catalog set name='Boy' where id = 0")  
In [13]: cx.commit()

注意,修改数据以后提交

**5.删除**  

cu.execute("delete from catalog where id = 1")  
cx.commit()  

**6.使用中文**

请先确定你的IDE或者系统默认编码是utf-8,并且在中文前加上u  

x=u'鱼'  
cu.execute("update catalog set name=? where id = 0",x)  
cu.execute("select * from catalog")  
cu.fetchall()  
[(0, 10, u'\u9c7c', u'Yu'), (1, 20, u'cba', u'Xu')]

如果要显示出中文字体，那需要依次打印出每个字符串  

```python

In [26]: for item in cu.fetchall():  
....: for element in item:  
....: print element,  
....: print....:  
0 10 鱼 Yu1  20 cba Xu

```

**7.Row类型**

Row提供了基于索引和基于名字大小写敏感的方式来访问列而几乎没有内存开销。 原文如下：

> [sqlite3.Row](http://docs.python.org/library/sqlite3.html#sqlite3.Row "sqlite3.Row") provides both index-based and case-insensitive name-based access to columns with almost no memory overhead. It will probably be better than your own custom dictionary-based approach or even a db_row based solution.

Row对象的详细介绍  

_class_ sqlite3.Row

A [Row](http://docs.python.org/library/sqlite3.html#sqlite3.Row "sqlite3.Row") instance serves as a highly optimized [row_factory](http://docs.python.org/library/sqlite3.html#sqlite3.Connection.row_factory "sqlite3.Connection.row_factory") for [Connection](http://docs.python.org/library/sqlite3.html#sqlite3.Connection "sqlite3.Connection") objects. It tries to mimic a tuple in most of its features.

It supports mapping access by column name and index, iteration, representation, equality testing and [len()](http://docs.python.org/library/functions.html#len "len").

If two [Row](http://docs.python.org/library/sqlite3.html#sqlite3.Row "sqlite3.Row") objects have exactly the same columns and their members are equal, they compare equal.

Changed in version 2.6: Added iteration and equality (hashability).

keys()

This method returns a tuple of column names. Immediately after a query, it is the first member of each tuple in [Cursor.description](http://docs.python.org/library/sqlite3.html#sqlite3.Cursor.description "sqlite3.Cursor.description").

New in version 2.6.

下面举例说明

```python

In [30]: cx.row_factory = sqlite3.Row  
  
In [31]: c = cx.cursor()  
  
In [32]: c.execute('select * from catalog')  
Out[32]: <sqlite3.Cursor object at 0x05666680>  
  
In [33]: r = c.fetchone()  
  
In [34]: type(r)  
Out[34]: <type 'sqlite3.Row'>  
  
In [35]: r  
Out[35]: <sqlite3.Row object at 0x05348980>  
  
In [36]: print r  
(0, 10, u'\u9c7c', u'Yu')  
  
In [37]: len(r)  
Out[37]: 4  
  
In [39]: r[2] #使用索引查询  
Out[39]: u'\u9c7c'  
  
In [41]: r.keys()  
Out[41]: ['id', 'pid', 'name', 'nickname']  
  
In [42]: for e in r:  
....: print e,  
....:  
0 10 鱼 Yu

```

使用列的关键词查询

In [43]: r['id']  
Out[43]: 0  
  
In [44]: r['name']  
Out[44]: u'\u9c7c'