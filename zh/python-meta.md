
# Python 中的元编程

简化任务

![author photo](https://www.ibm.com/developerworks/i/p-skansal60.jpg)

[Satwik Kansal](https://www.linkedin.com/in/satwikkansal)  
2018 年 5 月 23 日发布

[Weibo](https://service.weibo.com/share/share.php?url=http%3A%2F%2Fwww.ibm.com%2Fdeveloperworks%2Fcn%2Fanalytics%2Flibrary%2Fba-metaprogramming-python%2Findex.html%&title=Python%20%E4%B8%AD%E7%9A%84%E5%85%83%E7%BC%96%E7%A8%8B&language=zh_cn)[Google+](https://plus.google.com/share?url=http%3A%2F%2Fwww.ibm.com%2Fdeveloperworks%2Fcn%2Fanalytics%2Flibrary%2Fba-metaprogramming-python%2Findex.html&t=Python%20%E4%B8%AD%E7%9A%84%E5%85%83%E7%BC%96%E7%A8%8B)[用电子邮件发送本页面](mailto:?subject=Python%20%E4%B8%AD%E7%9A%84%E5%85%83%E7%BC%96%E7%A8%8B&body=http%3A%2F%2Fwww.ibm.com%2Fdeveloperworks%2Fcn%2Fanalytics%2Flibrary%2Fba-metaprogramming-python%2Findex.html)

[![Comments](https://dw1.s81c.com/developerworks/i/v18/article/dw-article-cmt-icon.png)](https://www.ibm.com/developerworks/cn/analytics/library/ba-metaprogramming-python/index.html#icomments)

[](https://www.ibm.com/developerworks/cn/analytics/library/ba-metaprogramming-python/index.html#icomments)

1

就像元数据是有关数据的数据一样，元编程就是编写用于操纵程序的某些程序。人们普遍认为，元程序就是生成其他程序的某些程序，但范式更加广泛。所有旨在自我读取、分析、转换或修改的程序都是元编程的范例。例如：

-   领域特定语言 (DSL)
-   解析器
-   解释器
-   编译器
-   定理证明器
-   术语重写器

本教程探究 Python 中的元编程。本文通过考察 Python 的特性，更新您的 Python 知识，让您能够更深入地理解本教程中的概念。同时，还说明了 Python 中的类型为何会比只返回对象的类更重要。之后，讨论了在 Python 中进行元编程的方法，以及元编程如何简化某些任务。

## 稍作反思

如果您使用 Python 进行编程已经有段时间，可能知道一切都是对象，而类创建了这些对象。但是，如果一切都是对象（类也是对象），那么谁来创建这些类呢？这就是我要解答的问题。

我们来验证一下上述说法是否正确：

1

2

3

4

5

`>>> class SomeClass:`

`... pass`

`>>> some_object = SomeClass()`

`>>> type(some_obj)`

`<``__main__.SomeClass` `instance at 0x7f8de4432f80>`

因此，在对象上调用的  `type`  函数返回该对象的类。

1

2

3

4

5

6

7

`>>> import inspect`

`>>>inspect.isclass(SomeClass)`

`True`

`>>>inspect.isclass(some_object)`

`False`

`>>>inspect.isclass(type(some_object))`

`True`

如果将类传递给  `inspect.isclass`，它就会返回  `True`，否则即返回  `False`。因为  `some_object`  不是类（它是  `SomeClass`  类的实例），所以 inspect.isclass 返回  `False`。又因为  `type(some_object)`  返回  `some_object`  的类，所以  `inspect.isclass(type(some_object))`  返回  `True`：

1

2

3

4

`>>> type(SomeClass)`

`<``type` `'classobj'>>>>`

`inspect.isclass(type(SomeClass))`

`True`

在 Python 3 中，所有类在默认情况下从  `Classobj`  类继承。现在，一切都说得通了。但  `classobj`  又该如何解释？我们来开开眼：

1

2

3

4

5

6

7

8

`>>> type(type(SomeClass))`

`<``type` `'type'>`

`>>>inspect.isclass(type(type(SomeClass)))`

`True`

`>>>type(type(type(SomeClass)))`

`<``type` `'type'>`

`>>>isclass(type(type(type(SomeClass))))`

`True`

发现了吗？事实证明，一开始的说法（一切都是对象）并不完全正确。下面是更准确的说法：

除 type 之外，Python 中的一切都是对象，它们要么是类的实例，要么是元类的实例。

验证这一点：

1

2

3

4

5

`>>> some_obj = SomeClass()`

`>>> isinstance(some_obj,SomeClass)`

`True`

`>>> isinstance(SomeClass, type)`

`True`

现在，我们知道了实例是实例化的类，而类是元类的实例。

## `type`  并不是我们所想的那样

`type`  本身是类，也是自己的类型。它是一个元类。元类用于实例化并定义类的行为，就像类用于实例化并定义实例的行为一样。

`type`  是 Python 使用的内置元类。为改变 Python 中类的行为（比如，`SomeClass`  的行为），我们可以通过继承  `type`  元类，定义一个自定义元类。元类是在 Python 中进行元编程的一种方法。

## 定义了某个类后会发生什么情况？

我们首先回顾下已知的内容。Python 程序的基本构建块是：

-   语句
-   函数
-   类

语句用于在程序中执行实际的工作。语句可以在全局范围（模块级别）或局部范围（限于函数内）执行。函数类似代码的基本单元，由用于完成特定任务的一个或多个语句以某种顺序构成。可以在模块级别定义函数，也可以将函数定义为类的方法。类为函数提供面向对象的编程方法。它们定义对象如何进行实例化以及对象的特征（属性和方法）。

类的名称空间被分层为不同的字典。例如：

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

`>>> class SomeClass:`

`... class_var = 1`

`... def __init__(self):`

`... self.some_var = 'Some value'`

`>>> SomeClass.__dict__`

`{'__doc__': None,`

`'__init__': <``function` `__main__.__init__>,`

`'__module__': '__main__',`

`'class_var': 1}`

`>>> s = SomeClass()`

`>>> s.__dict__`

`{'some_var': 'Some value'}`

以下是每次遇到关键字类时发生的情况：

-   类的主体（语句和函数）被隔离。
-   创建类的名称空间字典（但尚未填充）。
-   先执行类的主体，然后使用所有属性、定义的方法以及与类有关的其他一些有用信息来填充名称空间字典。
-   在基类或要创建的类的元类挂钩（稍后解释）中确定元类。
-   然后，通过类的名称、基类和属性调用元类，对其进行实例化。

因为  `type`  是 Python 中的默认元类，所以可以在 Python 中使用  `type`  来创建类。

## `type`  的另一面

通过一个参数调用  `type`  时，会生成现有类的  `type`  信息。通过三个参数调用  `type`  时，会创建一个新的类对象。调用  `type`  时，参数是类名、基类列表以及指定类的名称空间的字典（所有字段和方法）。

所以：  
`>>> class SomeClass: pass`

等同于：  
`>>> SomeClass = type('SomeClass', (), {})`

以及：

1

2

3

4

5

6

7

`class ParentClass:`

`pass`

`class SomeClass(ParentClass):`

`some_var = 5`

`def some_function(self):`

`print("Hello!")`

实际等同于：

1

2

3

4

5

6

7

8

`def some_function(self):`

`print("Hello")`

`ParentClass = type('ParentClass', (), {})`

`SomeClass = type('SomeClass',`

`[ParentClass],`

`{'some_function': some_function,`

`'some_var':5})`

因此，通过使用自定义元类而不是  `type`，我们可以将某种行为注入到不太可能的类中。但是在实现元类来改变行为之前，我们来看一下在 Python 中进行元编程更为常见的方法。

## 装饰器：在 Python 中进行元编程的常见例子

装饰器是用于改变函数或类的行为的一种方法。装饰器的用法类似如下：

1

2

3

`@some_decorator`

`def some_func(*args, **kwargs):`

`pass`

`some_func`  包装的  `@some_decorator`  只是语法糖的代表 。我们知道在 Python 中，函数和类（`metaclass`  类型除外）都是对象，也就是说它们可以：

-   分配给某个变量
-   复制
-   作为参数传递给其他函数

前面的语法实际等同于：  
`some_func = some_decorator(some_func)`

您可能想知道  `some_decorator`  是如何定义的：

1

2

3

4

5

6

7

8

9

`def some_decorator(f):`

`"""`

`The decorator receives function as a parameter.`

`"""`

`def wrapper(*args, **kwargs):`

`# doing something before calling the function`

`f(*args, **kwargs)`

`# doing something after the function is called`

`return wrapper`

我们假设自己有一个从 URL 访存已提取数据的函数。我们从中访存数据的服务器具备调节机制，如果它检测到在相同时间间隔内从某个 IP 地址传入大量请求，就会进行调节。所以，为了让提取器像人类一样，我们愿意等待随机长度的时间，然后再提交请求以欺骗服务器。 能否使装饰器也做到这样？我们来看一下：

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

`from functools import wraps`

`import random`

`import time`

`def wait_random(min_wait=1, max_wait=30):`

`def inner_function(func):`

`@wraps(func)`

`def wrapper(*args, **kwargs):`

`time.sleep(random.randint(min_wait, max_wait))`

`return func(*args, **kwargs)`

`return wrapper`

`return inner_function`

`@wait_random(10, 15)`

`def function_to_scrape():`

`# some scraping stuff`

您对  `Inner_function`  和  `@wraps`  装饰器可能有点陌生。如果您仔细查看就会发现，`inner_function`  与我们前面定义的  `some_decorator`  类似。  `Wait_random`  中的另一层包装也支持将参数传递到装饰器（`min_wait`  和  `max_wait`）。`@Wraps`  是个不错的装饰器，可以复制  `func`  的元数据（比如名称、文档字符串以及函数属性）。如果不使用这些，我们就无法从  `help(func)`  等函数调用获得有用的结果，因为在这种情况下，它会返回  `wrapper`  而不是  `func`  的文档字符串和信息。

但是，如果我们拥有  `scraper`  类以及多个此类函数会怎样：

1

2

3

4

5

6

7

8

9

10

`class Scraper:`

`def func_to_scrape_1(self):`

`# some scraping stuff`

`pass`

`def func_to_scrape_2(self):`

`# some scraping stuff`

`pass`

`def func_to_scrape_3(self):`

`# some scraping stuff`

`pass`

一种选择就是使用  `@wait_random`  单独包装所有函数。但我们可以做得更好：我们可以创建一个类装饰器。方法就是遍历类名称空间，确定函数，然后通过装饰器包装这些函数。

1

2

3

4

5

6

7

8

`def classwrapper(cls):`

`for name, val in vars(cls).items():`

``# `callable` return `True` if the argument is callable``

``# i.e. implements the `__call` ``

`if callable(val):`

`# instead of val, wrap it with our decorator.`

`setattr(cls, name, wait_random()(val))`

`return cls`

现在，您可以使用  `@classwrapper`  包装整个类。但是，如果存在多个 scraper 类或者  `scraper`  的多个子类会怎样？您可以对这些类单独使用  `@classwrapper`，或者在这种情况下，也可以创建元类。

## 元类

编写自定义元类分为两个步骤：

1.  编写元类类型的子类。
2.  使用元类挂钩将新元类插入到类创建流程中。

我们使 type 类实现子类化，并修改魔术方法，比如  [`__init__`](https://docs.python.org/2/reference/datamodel.html#object.__init__)、[`__new__`](https://docs.python.org/2/reference/datamodel.html#object.__new__)、[`__prepare__`](https://docs.python.org/3/reference/datamodel.html#preparing-the-class-namespace)  以及  [`__call__`](https://docs.python.org/2/reference/datamodel.html#object.__call__)，以便在创建类时修改类的行为。这些方法包含基类、类名、属性及其值等方面的信息。在 Python 2 中，元类挂钩是称为  `__metaclass__`  的类中的静态字段。在 Python 3 中，您可以将元类指定为类的基类列表中的一个  `metaclass`  参数。

1

2

3

4

5

6

7

8

9

10

11

12

`>>> class CustomMetaClass(type):`

`... def __init__(cls, name, bases, attrs):`

`... for name, value in attrs.items():`

`# do some stuff`

`... print('{} :{}'.format(name, value))`

`>>> class SomeClass:`

`... # the Python 2.x way`

`... __metaclass__ = CustomMetaClass`

`... class_attribute = "Some string"`

`__module__ :__main__`

`__metaclass__ :<``class` `'__main__.CustomMetaClass'>`

`class_attribute :Some string`

由于  `CustomMetaClass`  的  `__init__`  方法中的 print 语句，这些属性将会自动打印。我们假设您在 Python 项目中有个令人讨厌的合作者，此人更喜欢使用  `camelCase`  来命名类属性和方法。您知道这样不好，该合作者应该使用  `snake_case`（毕竟，这是 Python！）。我们能否编写元类，将所有这些 camelCase 属性更改为 snake_case？

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

`def camel_to_snake(name):`

`"""`

`A function that converts camelCase to snake_case.`

`Referred from: https://stackoverflow.com/questions/1175208/elegant-python-function-to-convert-camelcase-to-snake-case`

`"""`

`import re`

`s1 = re.sub('(.)([A-Z][a-z]+)', r'\1_\2', name)`

`return re.sub('([a-z0-9])([A-Z])', r'\1_\2', s1).lower()`

`class SnakeCaseMetaclass(type):`

`def __new__(snakecase_metaclass, future_class_name,`

`future_class_parents, future_class_attr):`

`snakecase_attrs = {}`

`for name, val in future_class_attr.items():`

`snakecase_attrs[camel_to_snake(name)] = val`

`return type(future_class_name, future_class_parents,`

`snakecase_attrs)`

您可能想知道我们在这里为什么使用  `__new__`  而不是  `__init__`。`__new__`  实际上是创建实例的第一步。它负责返回类的新实例。而在另一方面，`__init__`  则不会返回任何内容。它只负责在创建实例后对其进行初始化。请牢记一条简单的经验法则：当需要控制新实例的创建时使用  `new`，而在需要控制新实例的初始化时则使用  `init`。

在元类中实现  `__init__`  并不常见，因为它不是那么强大 — 在实际调用  `__init__`  之前，已经构造了类。您可以将其视为具有一个类装饰器，但不同点在于：在构建子类时会运行  `__init__`，而不会为子类调用类装饰器。

因为我们的任务包括创建新实例（防止这些 camelCase 属性潜入类中），所以覆盖自定义  `SnakeCaseMetaClass`  中的  `__new__`  方法。我们来确认下它是否运行：

1

2

3

4

5

6

`>>> class SomeClass(metaclass=SnakeCaseMetaclass):`

`... camelCaseVar = 5`

`>>> SomeClass.camelCaseVar`

`AttributeError: type object 'SomeClass' has no attribute 'camelCaseVar'`

`>>> SomeClass.camel_case_var`

`5`

它已运行！现在，您已了解了如何在 Python 中编写和使用元类。我们再来探究一下这有何用途。

## 在 Python 中使用元类

您可以使用元类对属性、方法及其值执行不同的准则。前面例子（使用 snake_case）的类似示例包括：

-   值的域限制
-   隐式转换自定义类的值（您可能希望向用户隐藏编写类的所有这些复杂方面）
-   执行不同的命名约定和样式准则（比如，“每种方法都应有一个文档字符串”）
-   向类添加新的属性

在类定义本身中定义所有这种逻辑时使用元类，主要原因就是为了避免在整个代码库中出现重复代码。

## 元类的实际使用

因为在子类中会继承元类，所以元类解决了代码冗余（不要重复自己 — DRY）这一实际问题。 通常情况下，在生成类对象的同时，通过执行额外操作或添加额外代码，元类也可以帮助提取有关类创建的复杂逻辑。元类的一些实际用例包括：

-   抽象基类
-   类的注册
-   在库和框架中创建 API

我们来具体看一下每个示例。

## 抽象基类

抽象基类是只能被继承而不会被实例化的类。Python 具有以下内容：

1

2

3

4

5

6

7

8

9

10

11

`from abc import ABCMeta, abstractmethod`

`class Vehicle(metaclass=ABCMeta):`

`@abstractmethod`

`def refill_tank(self, litres):`

`pass`

`@abstractmethod`

`def move_ahead(self):`

`pass`

我们来创建一个从  `Vehicle`  类继承的  `Truck`  类：

1

2

3

4

5

6

7

8

9

10

11

`class Truck(Vehicle):`

`def __init__(self, company, color, wheels):`

`self.company = company`

`self.color = color`

`self.wheels = wheels`

`def refill_tank(self, litres):`

`pass`

`def move_ahead(self):`

`pass`

请注意，我们没有实现抽象方法。我们来看下如果尝试实例化  `Truck`  类的对象会发生什么情况：

1

2

3

`>>> mini_truck = Truck("Tesla Roadster", "Black", 4)`

`TypeError: Can't instantiate abstract class Truck with abstract methods move_ahead, refill_tank`

可以通过在  `Truck`  类中定义两种抽象方法来修复这个问题：

1

2

3

4

5

6

7

8

9

10

11

12

13

14

`class Truck(Vehicle):`

`def __init__(self, company, color, wheels):`

`self.company = company`

`self.color = color`

`self.wheels = wheels`

`def refill_tank(self, litres):`

`pass`

`def move_ahead(self):`

`pass`

`>>> mini_truck = Truck("Tesla Roadster", "Black", 4)`

`>>> mini_truck`

`<``__main__.Truck` `at 0x7f881ca1d828>`

## 类的注册

为理解这一点，我们以某个服务器上的多个文件处理程序为例。想法就是能够根据文件格式快速找到正确的处理程序类。我们将创建处理程序字典，让  `CustomMetaclass`  注册在代码中遇到的不同处理程序：

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

22

23

24

`handlers = {}`

`class CustomMetaclass(type):`

`def __new__(meta, name, bases, attrs):`

`cls = type.__new__(meta, name, bases, attrs)`

`for ext in attrs["formats"]:`

`handlers[ext] = cls`

`return cls`

`class Handler(metaclass=CustomMetaclass):`

`formats = []`

`# common stuff for all kinds of file format handlers`

`class ImageHandler(Handler):`

`formats = ["jpeg", "png"]`

`class AudioHandler(Handler):`

`formats = ["mp3", "wav"]`

`>>> handlers`

`{'mp3': __main__.AudioHandler,`

`'jpeg': __main__.ImageHandler,`

`'png': __main__.ImageHandler,`

`'wav': __main__.AudioHandler}`

现在，根据文件格式，我们很容易就知道要使用哪个处理程序类。一般来说，无论何时需要维护存储类特征的某种数据结构，都可以使用元类。

## 创建 API

由于元类能够防止子类中的逻辑冗余，能够隐藏用户无需知道的自定义类创建逻辑，因此元类在框架和库中得到广泛应用。这为减少样板和拥有更出色的 API 创造了一些值得注意的机会。例如，思考一下 Django ORM 的这个使用片段：

1

2

3

4

`>>> from from django.db import models`

`>>> class Vehicle(models.Model):`

`... color = models.CharField(max_length=10)`

`... wheels = models.IntegerField()`

我们在此创建了一个  `Vehicle`  类，它从 Django 包中的 models.Model 类继承而来。在该类的内部，我们定义了几个字段（color 和 wheels）来表示车辆的特征。现在，我们尝试实例化刚刚所创建类的对象。

1

2

3

4

5

`>>> four_wheeler = Vehicle(color="Blue", wheels="Four")`

`# Raises an error`

`>>> four_wheeler = Vehicle(color="Blue", wheels=4)`

`>>> four_wheeler.wheels`

`4`

作为创建车辆模型的用户，我们只需从 models.Model 类继承，然后编写一些高级语句。其余工作（比如创建数据库挂钩，提出无效值错误，返回  `int`  类型而不是 models.IntegerField）则由 model.Models 类以及它使用的元类在后台完成。

## 总结

在本教程中，您了解了 Python 中的实例、类以及元类之间的关系。您学习了元编程知识，这是一种操纵代码的方法。我们讨论了函数装饰器和类装饰器，二者是将自定义行为注入到类和方法中的一种方式。然后，我们通过使 Python 的默认 type 元类子类化，实现了自定义元类。最后，我们介绍了元类的一些实际用例。是否使用元类这个问题在网上饱受争议，但是现在，对于某种问题是否利用元编程才能更好地解决，您应该可以更轻松地展开分析并得出答案。

#### 相关主题

-   [Python 初学者指南](https://www.ibm.com/developerworks/opensource/library/os-beginners-guide-python/index.html)
-   [技术讲座：Python：一种持续奉献、不断发展和永续学习的语言](https://developer.ibm.com/code/techtalks/python-language-keeps-giving-growing-learming/)

#### 评论

添加或订阅评论，请先登录或注册。

有新评论时提醒我

-   最新的
-   历史
-   热门

-   ![](https://www.ibm.com/developerworks/maverick/image/user/user-icon.png)2018 年 06 月 05 日
    
    [msdog](https://www.ibm.com/developerworks/community/profiles/user/msdog)
    
    感谢作者，学到很多。 发现个小问题 handlers = {} class CustomMetaclass(type): def __new__(meta, name, bases, attrs): cls = type.__new__(meta, name, bases, attrs) for ext in attrs["files"]: handlers[ext] = cls return cls class Handler(metaclass=CustomMetaclass): formats = [] # common stuff for all kinds of file format handlers class ImageHandler(Handler): formats = ["jpeg", "png"] class AudioHandler(Handler): formats = ["mp3", "wav"] the for ext in attrs["files"]: should be attrs['formats']
