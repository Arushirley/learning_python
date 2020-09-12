#### 使用SQLAlchemy

It is python 2 : To need for fingding documents at python3.

----------

数据库表是一个二维表，包含多行多列。把一个表的内容用Python的数据结构表示出来的话，可以用一个list表示多行，list的每一个元素是tuple，表示一行记录，比如，包含`id`和`name`的`user`表：

```
[
    ('1', 'Michael'),
    ('2', 'Bob'),
    ('3', 'Adam')
]

```

Python的DB-API返回的数据结构就是像上面这样表示的。

但是用tuple表示一行很难看出表的结构。如果把一个tuple用class实例来表示，就可以更容易地看出表的结构来：

```
class User(object):
    def __init__(self, id, name):
        self.id = id
        self.name = name

[
    User('1', 'Michael'),
    User('2', 'Bob'),
    User('3', 'Adam')
]

```

这就是传说中的ORM技术：Object-Relational Mapping，把关系数据库的表结构映射到对象上。是不是很简单？

但是由谁来做这个转换呢？所以ORM框架应运而生。

在Python中，最有名的ORM框架是SQLAlchemy。我们来看看SQLAlchemy的用法。

首先通过easy_install或者pip安装SQLAlchemy：

```
$ easy_install sqlalchemy

```

然后，利用上次我们在MySQL的test数据库中创建的`user`表，用SQLAlchemy来试试：

第一步，导入SQLAlchemy，并初始化DBSession：

```
# 导入:
from sqlalchemy import Column, String, create_engine
from sqlalchemy.orm import sessionmaker
from sqlalchemy.ext.declarative import declarative_base

# 创建对象的基类:
Base = declarative_base()

# 定义User对象:
class User(Base):
    # 表的名字:
    __tablename__ = 'user'

    # 表的结构:
    id = Column(String(20), primary_key=True)
    name = Column(String(20))

# 初始化数据库连接:
engine = create_engine('mysql+mysqlconnector://root:password@localhost:3306/test')
# 创建DBSession类型:
DBSession = sessionmaker(bind=engine)

```

以上代码完成SQLAlchemy的初始化和具体每个表的class定义。如果有多个表，就继续定义其他class，例如School：

```
class School(Base):
    __tablename__ = 'school'
    id = ...
    name = ...

```

`create_engine()`用来初始化数据库连接。SQLAlchemy用一个字符串表示连接信息：

```
'数据库类型+数据库驱动名称://用户名:口令@机器地址:端口号/数据库名'

```

你只需要根据需要替换掉用户名、口令等信息即可。

下面，我们看看如何向数据库表中添加一行记录。

由于有了ORM，我们向数据库表中添加一行记录，可以视为添加一个`User`对象：

```
# 创建session对象:
session = DBSession()
# 创建新User对象:
new_user = User(id='5', name='Bob')
# 添加到session:
session.add(new_user)
# 提交即保存到数据库:
session.commit()
# 关闭session:
session.close()

```

可见，关键是获取session，然后把对象添加到session，最后提交并关闭。Session对象可视为当前数据库连接。

如何从数据库表中查询数据呢？有了ORM，查询出来的可以不再是tuple，而是`User`对象。SQLAlchemy提供的查询接口如下：

```
# 创建Session:
session = DBSession()
# 创建Query查询，filter是where条件，最后调用one()返回唯一行，如果调用all()则返回所有行:
user = session.query(User).filter(User.id=='5').one()
# 打印类型和对象的name属性:
print 'type:', type(user)
print 'name:', user.name
# 关闭Session:
session.close()

```

运行结果如下：

```
type: <class '__main__.User'>
name: Bob

```

可见，ORM就是把数据库表的行与相应的对象建立关联，互相转换。

由于关系数据库的多个表还可以用外键实现一对多、多对多等关联，相应地，ORM框架也可以提供两个对象之间的一对多、多对多等功能。

例如，如果一个User拥有多个Book，就可以定义一对多关系如下：

```
class User(Base):
    __tablename__ = 'user'

    id = Column(String(20), primary_key=True)
    name = Column(String(20))
    # 一对多:
    books = relationship('Book')

class Book(Base):
    __tablename__ = 'book'

    id = Column(String(20), primary_key=True)
    name = Column(String(20))
    # “多”的一方的book表是通过外键关联到user表的:
    user_id = Column(String(20), ForeignKey('user.id'))

```

当我们查询一个User对象时，该对象的books属性将返回一个包含若干个Book对象的list。

### 小结

ORM框架的作用就是把数据库表的一行记录与一个对象互相做自动转换。

正确使用ORM的前提是了解关系数据库的原理。

link:
https://www.liaoxuefeng.com/wiki/897692888725344/955081460091040

---


# SQLAlchemy入门和进阶

[![猪了个去](https://pic2.zhimg.com/fbe6adf96_xs.jpg)](https://www.zhihu.com/people/zhulegequ)

[猪了个去](https://www.zhihu.com/people/zhulegequ)

搜索算法程序猿

176 人赞同了该文章

目录：  

1.  SQLAlchemy 简介  
    
2.  横向对比  
    
3.  核心概念与入门  
    

1.  模型定义  
    
2.  增  
    
3.  查  
    
4.  复杂查询  
    
5.  删  
    
6.  改  
    
7.  基础性能

5.  扩展与进阶  
    

1.  事件  
    
2.  反射  
    
3.  Python3.x asyncio扩展  
    
4.  分片Session  
    
5.  自定义的列类型  
    
6.  混合(hybrid)属性  
    
7.  序列化Query  
    
8.  Baked Query  
    
9.  多态与关系

  
（知乎没有自动目录和侧边栏悬浮呢。。惆怅）  

在新团队里做的技术分享，过了一段时间，整理下来并且有了新的想法。似乎入门级的教程在知乎更受欢迎？

# SQLAlchemy 简介

SQLAlchemy 是一个功能强大的Python ORM 工具包，口碑不错，社区活跃也较为开放  
提供 全功能的SQL和ORM操作 本次附赠的文件（这里放不上来，也懒得放gayhub了，总之很简单的，单元测试多一些，一下午搞定）：  
connect.py :底层的数据库连接  
orm.py :模型定义的样例  
example_test.py :单元测试，实质上可以对应业务的具体使用  
python3_test.py :展示Python3 asyncio下的SQLAlchemy

分别建立python2/3的虚拟环境，然后安装对应的requirements.txt即可

无论什么语言，无论什么库，做一个ORM实现，至少应当实现完全**语义化**的数据库操作，使得操作数据库表就像在操作对象。  
完整的ORM应当可以完全避免SQL拼接

## 为什么需要ORM

当时分享完毕之后，也确实很多同事表示还是喜欢裸SQL，我后来也又在工作中看到了很多遗留代码的问题。我也正好趁浴室迷思 想了一下，为什么我需要ORM呢？

第一条来自一个定理：

**一切由人直接来保证安全性的系统，就一定会出错**

拼接SQL、把SQL做成模板、开始使用ORM、封装出DAO层，几乎是每个项目的共识吧？  
过往的项目中，由我第一手写的，都会第一时间加入ORM，毕竟也只是两三个小文件，一百行以内的事情（后续由于封装的增多，可能会到达数百行）

这段时间在写旧系统的小规模重构（**定理2：一个好程序猿应当友好地帮前人擦好屁股，而不是靠重新制造一个新屁股实现**），拼接字符串并没有带来任何优点，反而引入了非常简单的注入漏洞，简单的设想这样一个列表API的场景：

1.  根据请求参数控制对应的：过滤条件、排序方法、翻页
2.  根据需要预取关联的表，JOIN并把对一对多的关系化为一个list

第一条，刚一上手，就发现满地的string format，翻页用了：

```text
order_sql = "ORDER BY {} {}".format(order_by,direction)
```

毫无疑问的order_by=id%3Bselect+1%3B-- 就直接注入了

要解决这些在SQL拼接的问题，除了表单验证，毫无疑问需要做一个SQL字符转义，另外在能用SQL参数的地方，需要用参数（然后也得注意拼接时候参数的个数，是的，这里我们的接口有另一个BUG，参数数量没数对）

第二个功能点，想象一下在需要的地方额外加一句LEFT JOIN，然后对结果再做额外的解析

还有一些附属功能：单元测试如何建表？代码里遍地的硬编码表名如何解决？

  
自己不是不能实现，但自己来实现这些，就走上了发明ORM的老路，用一个成熟的、文档丰富的ORM，岂不美哉？  

# 横向对比

简单的挑了三个

（知乎的表格似乎智障，不插入表格了）

SQLAlchemy、Peewee、Django ORM

Django ORM一直就不是一个全功能的ORM，会发现你想写的SQL几乎无法通过ORM写出来，当然raw属于tan90，使用裸SQL不在我们的考虑范围。Django 1.12后提供了一些subquery等各类丰富SQL操作，但这么新，估计还极少项目在这么新的版本

Peewee如果有兴趣可以后续继续使用来感受一下，Peewee也是一个功能全面的ORM，star很多但开发没有SQLAlchemy活跃

  

# 核心概念与入门

[官方文档](https://link.zhihu.com/?target=https%3A//www.sqlalchemy.org/)  
我总是在想为什么团队里很多人会觉得SQLAlchemy入门门槛高，我曾经也被困扰过，但回头一看会发现的概念实质比较简单。  
官方文档的脉络不太清晰，要扫过一遍并且学以致用才能感受得到。example很友好的！

  
回过头来看它的从教程到API的文档，会发现它的文档非常详细，学会它，除了学会了Python操作SQL的一个库，同样也可以学到从代码组织、各类Pythonic技巧到思想的很多东西

  
总的感受是：上手还算容易，精通要花很多功夫，但确实还挺有趣的

先放一个表，待会我们会继续讲

（再次损失一个表）

![](https://pic1.zhimg.com/80/v2-984901c2903ec83589d641fb930ed738_hd.png)

概念很少，并且很清晰，理解这些概念之后的后续使用时，基本可以感受到：你能直觉想到的操作，还确实都有（比如subquery、复杂查询的构造）

## 模型定义

我们来看看他如何完成模型定义：

```python
# coding=utf-8
from __future__ import unicode_literals, absolute_import
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy import Column, Integer, String, DateTime
ModelBase = declarative_base() #<-元类

class User(ModelBase):
    __tablename__ = "auth_user"

    id = Column(Integer, primary_key=True)
    date_joined = Column(DateTime)
    username = Column(String(length=30))
    password = Column(String(length=128))



```

从这里可以看到，模型定义甚至与数据库是无关的，所以允许不同的数据库后端，不同类型拥有不同的表现形式和建表语句  

这里我们可以看到它实现了 ORM与数据库连接的解耦，一些数据库后端不支持的数据类型，例如Numeric类型，在sqlite中不支持，不过SQLAlchemy也能做一些兼容使用普通浮点

**Model** 等同于数据库的一张表  
**Column** 显然就是这张表的一列

PS: SQLAlchemy 1.2之后才支持comment注释，以在ddl产生建表SQL时写上comment属性，1.2还在beta版里，所以还不能用。。。我倒很好奇为毛这个feature这么不重要

## 增

```text
with get_session() as session:
    session.add(User(username="asd", password="asd"))
    session.add(User(username="qwe", password="qwe"))
    session.commit()



```

**session**(会话)的概念，可以看成一个管理数据库持久连接的对象,在此下面是完全透明的连接池和事务等东西

> get_session底下configure可以控制auto_commit参数，= False时写操作默认都不放在事务里,SQLAlchemy默认为True

session.add函数将会把Model加入当前的持久空间(可以从session.dirty看到)，直到commit时更新

## 查

```text
with get_session() as session:
    # <class 'sqlalchemy.orm.query.Query'>
    session.query(User)


```

最简单的这个查询返回了一个Query对象  
需要注意的是，这里只构造Query，事实上并没有发送至数据库进行查询，只会在Query.get()、Query.all()、Query.one()以及Query.__iter__等具有“执行”语义的函数，才会真的去获取

**Query** ：本质上是数据表的若干行

1.  在查询情况的下，等同于SQL 中的 SELECT Syntax
2.  在update函数的操作时，可以根据参数选择等同于直接UPDATE users SET xxx WHERE name=xxx或者先用SELECT 选出ID，再循环用UPDATE xxx WHERE id=xxx
3.  delete同上

以SQLAlchemy为代表的ORM基本都支持链式操作。  
形如：

```text
with get_session() as session:
    # <class 'sqlalchemy.orm.query.Query'>
    query = (session
             .query(User)
             .filter(User.username == "asd")
             .filter_by(username="asd")
             #上面两个都是添加where
             .join(Addreess)#使用ForeignKey
             .join(Addreess,Addreess.user_id==User.id)#使用显式声明
             .limit(10)
             .offset(0)
             )


```

所有Query支持的详情见[Query API文档](https://link.zhihu.com/?target=http%3A//docs.sqlalchemy.org/en/rel_1_1/orm/query.html%23sqlalchemy.orm.query.Query.__init__)

上面也涉及到一个特别有意思的filter函数：User.username == "asd" ,实际上是SQLAlchemy重载了Column上的各种运算符 __eq__、__ge__，返回了一个BinaryExpression对象，看起来就更加符合直觉上的语义

## 复杂查询

基于Query的subquery

```text
with get_session() as session:
    # <class 'sqlalchemy.orm.query.Query'>
    query = (session
            .query(User.id)
            .filter(User.username == "asd")
            .filter_by(username="asd")
            .limit(10)
            )
    subquery = query.subquery()
    query2 = session.query(User).filter(
        User.id.in_(subquery)
    )
    print query2#<-打印展开成的SQL，此处没有SQL查询


```

理解了Query、Column的概念，也很容易自行构造出这样的SQL

所有在Column级别上的使用 详见[Column API文档](https://link.zhihu.com/?target=http%3A//docs.sqlalchemy.org/en/rel_1_1/core/metadata.html%23sqlalchemy.schema.Column.__eq__)

## 删

上面我们提到了直接对Query进行的删除：

```text
with get_session() as session:
    query = (session
             .query(User)
             .filter(User.username == "asd")
             .filter_by(username="asd")
             .join(Addreess)
             .join(Addreess,Addreess.user_id=User.id)
             .limit(10)
             .delete()#<-这里
             )


```

另外，因为Model也可以被放进session里，然后删除的，和插入是个反向操作：

```text
with get_session() as session:
    instance = session.query(User).get(1)
    session.delete(instance)
    #下一句执行：DELETE FROM auth_user WHERE auth_user.id = ?
    session.commit()


```

## 改

改首先是上述Query中所说的update方法：

```text
with get_session() as session:
            # get by id
    query = (session
             .query(User)
             .filter_by(id=1)
             .update({"username": 
                     User.username + "a"},
                     synchronize_session=False)
                     )


```

然后是在Model级别的方法：

```text
with get_session() as session:
            # get by id
    user = (session
            .query(User)
            .get(1)
            )
    user.password = "zxcv"
    # UPDATE auth_user SET password=?
    # WHERE auth_user.id = ?
    session.commit()


```

在对Model的属性进行修改的时候，session会得到修改对应的内容,下次commit即会提交SQL  
这里留个思考题：如果对1、同一对象的同一属性进行修改，2、同一对象的不同属性进行修改 ，最终会有几个SQL被发出？ 如果你来实现这样的功能，你会从哪里下手？

## 基础性能

[SQLAlchemy性能](https://link.zhihu.com/?target=http%3A//docs.sqlalchemy.org/en/rel_1_1/faq/performance.html%23faq-performance)

比较了十万条记录插入的性能  

![](https://pic1.zhimg.com/80/v2-3fd46c431fe919246a1c66484dfdec18_hd.png)

另外不要觉得比sqlite 裸SQL慢三倍很慢，注意这个量级，实际项目中会发现慢查询、不规范操作（例如for循环里放查询）的危害比引入ORM的这点开销打多了  

## 总结

到这再贴上面那个概念表，应该就能比较好的理解了

![](https://pic3.zhimg.com/80/v2-d1f3913d109b3a70f9caddaa9e686ff6_hd.png)

在用裸SQL可以解决的场景下，上述的SQLAlchemy入门部分就足以掌控场景，完成所有的增删查改API需求（甚至自动生成代码的需求），自动生成真是偷懒无止境。。不过发明新的DSL嘛，能不做就不做。。

  

# 扩展与进阶

从过往的经验来看，SQLAlchemy以优雅的直觉实现了诸多接口，并保留了良好的可扩展性，这里抛砖引玉一些有趣的特性

## 事件

应用层的触发器(trigger),支持：

1.  ConnectionEvents 包括Connection和Engine(连接后进行一些自检操作)
2.  DDLEvents 模型增删查改事件
3.  DialectEvents 不同种类的数据库的事件
4.  PoolEvents 连接池事件，连接的检出和回收等

上面的性能测试里就使用了两种事件

```text
from sqlalchemy import event
from sqlalchemy.engine import Engine
import time
import logging

logging.basicConfig()
logger = logging.getLogger("myapp.sqltime")
logger.setLevel(logging.DEBUG)

@event.listens_for(Engine, "before_cursor_execute")
def before_cursor_execute(conn, cursor, statement,
                        parameters, context, executemany):
    conn.info.setdefault('query_start_time', []).append(time.time())
    logger.debug("Start Query: %s", statement)

@event.listens_for(Engine, "after_cursor_execute")
def after_cursor_execute(conn, cursor, statement,
                        parameters, context, executemany):
    total = time.time() - conn.info['query_start_time'].pop(-1)
    logger.debug("Query Complete!")
    logger.debug("Total Time: %f", total)


```

## 反射

现有项目或者别人的代码里如果已经用其他的方式写好了表定义，不想再定义Model了，想用SQLAlchemy直接使用对应的数据库表  
查文档关键字：[Automap](https://link.zhihu.com/?target=http%3A//docs.sqlalchemy.org/en/rel_1_1/orm/extensions/automap.html%23)

```text
from sqlalchemy.ext.automap import automap_base
from sqlalchemy.orm import Session
from sqlalchemy import create_engine

Base = automap_base()

# engine, suppose it has two tables 'user' and 'address' set up
engine = create_engine("sqlite:///mydatabase.db")

# reflect the tables
Base.prepare(engine, reflect=True)
tables = Base.classes#<-load tables

User = Base.classes.user
Address = Base.classes.address
# rudimentary relationships are produced
session.add(Address(email_address="foo@bar.com", user=User(name="foo")))
session.commit()

# collection-based relationships are by default named
# "<classname>_collection"
print (u1.address_collection)


```

扩展阅读：[DeferredReflection](https://link.zhihu.com/?target=http%3A//docs.sqlalchemy.org/en/rel_1_1/orm/extensions/declarative/api.html%23sqlalchemy.ext.declarative.DeferredReflection)

我之前在一些OLAP应用 用来做数据分析时用到过。。

## Python3.x asyncio扩展

16年12月 Python3.6进入稳定期，同时也标志着Python3.4和3.5中的asyncio模块进入稳定期

SQLAlchemy对asyncio的支持在于，它实质上可以在engine层进行扩展,同时扩展Engine、Connection、Transaction、Context 代码量约400行

> Strategies for creating new instances of Engine types. These are semi-private implementation classes which provide the underlying behavior for the "strategy" keyword argument available on :func:~sqlalchemy.engine.create_engine. Current available options are plain, threadlocal, and mock. New strategies can be added via new EngineStrategy classes. """

形如：

```text
from sqlalchemy.engine.strategies import DefaultEngineStrategy
from .engine import AsyncioEngine
ASYNCIO_STRATEGY = '_asyncio'

class AsyncioEngineStrategy(DefaultEngineStrategy):
    name = ASYNCIO_STRATEGY
    engine_cls = AsyncioEngine
AsyncioEngineStrategy()  


async def main():
    engine = create_engine(
        # In-memory sqlite database cannot be accessed from different
        # threads, use file.
        'sqlite:///test.db', strategy=ASYNCIO_STRATEGY
    )

    metadata = MetaData()
    users = Table(
        'users', metadata,
        Column('id', Integer, primary_key=True),
        Column('name', Text),
    )

    # Create the table
    await engine.execute(CreateTable(users))

    conn = await engine.connect()  


```

另外提一嘴的是：asyncio不是银弹，会导致应用层压力直接传给DB，会掩盖应用的SQL写的烂的问题

## 分片Session

读写分离是当数据库压力到达一定阶段时，由应用层进行的拆分数据库压力的措施  
实现一种主从分离的Session:

1.  最简单的方案是直接扩展Session类get_bind方法

> get_bind(mapper=None, clause=None)  
> Return a “bind” to which this Session is bound. Note that the “mapper” argument is usually present when Session.get_bind() is called via an ORM operation such as a Session.query(), each individual INSERT/UPDATE/DELETE operation within a Session.flush(), call, etc.

1.  也可以使用sqlalchemy.ext.horizontal_shard模块中已经实现好的ShardedSession

> Parameters:

-   shard_chooser – A callable which, passed a Mapper, a mapped instance, and possibly a SQL clause, returns a shard ID. This id may be based off of the attributes present within the object, or on some round-robin scheme.
-   id_chooser – A callable, passed a query and a tuple of identity values, which should return a list of shard ids where the ID might reside.
-   query_chooser – For a given Query, returns the list of shard_ids where the query should be issued.
-   shards – A dictionary of string shard names to Engine objects.

允许根据model或者SQL条件、ID选择具体的数据库连接。一个未经验证的脑洞：因为shards是Engine的dict，那么是否允许在异构数据库之间使用Shard？这样会带来什么样的优缺点？

## 自定义的列类型

很久很久以前做的功能了，想象一个这样的场景：

-   Postgresql支持IP/CIDR的存储，本质上是使用4*8bit=32bit的int存储
-   Mysql此时并没有这样简单的IP存储 如何对其进行扩展？

自定义实现的列类型实质上需要：

1.  指定在某种数据库方言下的存储类型，例如Mysql下使用int
2.  实现两个方法：从数据库中取出来一个python对象和把Python对象放入数据库
3.  按需需要实现：支持一些操作符(例如==,in_)

```text
from sqlalchemy import types
class MyIPType(types.TypeDecorator):
    impl = types.Integer


    def process_bind_param(self, value, dialect):
        #from python to database
        if dialect=="mysql":
            pass
        return #....

    def process_result_value(self, value, dialect):
        #from database to python object
        return #...


```

我们也可以在awesome-sqlalchemy中找到一些有趣的类型扩展

## 混合(hybrid)属性

我们常见使用Python的property修饰器来构造一个复杂属性，SQLAlchemy中，这个混合属性的作用也类似，不仅可以用于获得对应的值，也可以用于Query时的链式操作

定义一个Model后，可以在各类增删查改中用到这个混合属性。混合属性 混合在：既是一个Python属性，也是一个可以放入数据库查询的属性

```python
class Interval(Base):
    __tablename__ = 'interval'

    id = Column(Integer, primary_key=True)
    start = Column(Integer, nullable=False)
    end = Column(Integer, nullable=False)

    def __init__(self, start, end):
        self.start = start
        self.end = end

    @hybrid_property
    def length(self):
        return self.end - self.start
    #下面这个写着玩的。。
    @length.setter
    def length(self, value):
        self._value = value

>>> i1 = Interval(5, 10)
>>> i1.length
5

>>> print Session().query(Interval).filter_by(length=5)
SELECT interval.id AS interval_id, interval.start AS interval_start,
interval."end" AS interval_end
FROM interval
WHERE interval."end" - interval.start = :param_1


```

上述还有一个写着玩儿的setter，hybrid_property支持：

1.  comparator 扩展Interval.length在各种比较符(><=)的行为
2.  deleter/setter 顾名思义
3.  expression 可以扩展最后展开的SQL表达式，例如展开成SUM(xxx):

```text
from sqlalchemy.orm import func
    #下面这个写着玩的。。
    @length.expression
    def length(self, expr):
        return func.sum(self.end, expr)


```

## 序列化Query

提供一个接口，以序列化和反序列化Query，用于跨系统、微服务的场景

```text
from sqlalchemy.ext.serializer import loads, dumps
metadata = MetaData(bind=some_engine)
Session = scoped_session(sessionmaker())

# ... define mappers

query = Session.query(User).
    filter(User.somedata=='foo').order_by(User.sortkey)

# pickle the query
serialized = dumps(query)

# unpickle.  Pass in metadata + scoped_session 
# 上面提到过的 query和Session实际上是密不可分的
query2 = loads(serialized, metadata, Session)

print query2.all()


```

这个做起来其实就非常带感了，微服务之间的必要条件就是各种dump，结合一下celery，实现一个去中心的HTTP服务也是不在话下

## Baked Query

缓存从Query生成的SQL，以减少生成时间，实际上是个应用层面的存储过程、View

```python
from sqlalchemy.ext import baked
bakery = baked.bakery()#<-创建了一个LRU

from sqlalchemy import bindparam

def search_for_user(session, username, email=None):

    baked_query = bakery(lambda session: session.query(User))
    baked_query += lambda q: q.filter(User.name == bindparam('username'))

    baked_query += lambda q: q.order_by(User.id)

    if email:
        baked_query += lambda q: q.filter(User.email == bindparam('email'))

    result = baked_query(session).params(username=username, email=email).all()

    return result
```

上面说到了SQLAlchemy展开成SQL的性能问题，真的特别担忧的话，再来一个缓存绑定参数如何？

## 多态和关系

使用多个模型，但实际上只是操作一张数据库表 此处基本略，之前写过一篇文章了：[这儿](https://zhuanlan.zhihu.com/p/26056479)

```text
class Employee(Base):  
    __tablename__ = 'employee'
    id = Column(Integer, primary_key=True)
    name = Column(String(50))
    type = Column(String(50))

    __mapper_args__ = {
        'polymorphic_identity':'employee',
        'polymorphic_on':type
    }


```

这里定义了雇员Employee 模型，指定type字段为多态所在字段，并且对于这个模型，当type字段为'employee'时，即为一个雇员

一对一、一对多、多对多的关系和自动收集成collection，这里不会细说，relationship函数的各种参数留待大家游玩。

关系间的收集有多种lazy方式，可以选择在父类读取时直接JOIN或者Subquery，也可以在需要的时候使用Query.option设置。说起来的篇幅会更长，我投个懒，大家去读文档吧~hfgl

发布于 2017-06-14