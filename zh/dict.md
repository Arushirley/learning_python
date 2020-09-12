
# [Python——字典dict()详解](https://www.cnblogs.com/mingmingming/p/11050495.html)

# 一、字典

_字典是Python提供的一种数据类型，用于存放有映射关系的数据，字典相当于两组数据，其中一组是key，是关键数据（程序对字典的操作都是基于key），另一组数据是value，可以通过key来进行访问。如图：  
![](https://img2018.cnblogs.com/blog/1719609/201906/1719609-20190619113938322-608333110.png)_

## 1、创建字典

通过Python内置函数help()查看帮助：

`>>>` `help``(``dict``)`

`Help`  `on` `class`  `dict`  `in`  `module builtins:`

`class`  `dict``(``object``)`

`|` `dict``()` `-``> new empty dictionary`

`|` `dict``(mapping)` `-``> new dictionary initialized` `from`  `a mapping` `object``'s`

`| (key, value) pairs`

`|` `dict``(iterable)` `-``> new dictionary initialized as` `if`  `via:`

`| d` `=`  `{}`

`|` `for`  `k, v` `in`  `iterable:`

`| d[k]` `=`  `v`

`|` `dict``(``*``*``kwargs)` `-``> new dictionary initialized with the name``=``value pairs`

`|` `in`  `the keyword argument` `list``. For example:` `dict``(one``=``1``, two``=``2``)`

`|`

`| Methods defined here:`

`|`

`| __contains__(``self``, key,` `/``)`

`|` `True`  `if`  `the dictionary has the specified key,` `else`  `False``.`

`|`

`| __delitem__(``self``, key,` `/``)`

`| Delete` `self``[key].`

`|`

`| __eq__(``self``, value,` `/``)`

`| Return` `self``=``=``value.`

`|`

`| __ge__(``self``, value,` `/``)`

`| Return` `self``>``=``value.`

`|`

`| __getattribute__(``self``, name,` `/``)`

`| Return` `getattr``(``self``, name).`

`|`

`| __getitem__(...)`

`| x.__getitem__(y) <``=``=``> x[y]`

`|`

`| __gt__(``self``, value,` `/``)`

`| Return` `self``>value.`

`|`

`| __init__(``self``,` `/``,` `*``args,` `*``*``kwargs)`

`| Initialize` `self``. See` `help``(``type``(``self``))` `for`  `accurate signature.`

`|`

`| __iter__(``self``,` `/``)`

`| Implement` `iter``(``self``).`

`|`

`| __le__(``self``, value,` `/``)`

`| Return` `self``<``=``value.`

`|`

`| __len__(``self``,` `/``)`

`| Return` `len``(``self``).`

`|`

`| __lt__(``self``, value,` `/``)`

`| Return` `self``<value.`

`|`

`| __ne__(``self``, value,` `/``)`

`| Return` `self``!``=``value.`

`|`

`| __repr__(``self``,` `/``)`

`| Return` `repr``(``self``).`

`|`

`| __setitem__(``self``, key, value,` `/``)`

`|` `Set`  `self``[key] to value.`

`|`

`| __sizeof__(...)`

`| D.__sizeof__()` `-``> size of D` `in`  `memory,` `in`  `bytes`

`|`

`| clear(...)`

`| D.clear()` `-``>` `None``. Remove` `all`  `items` `from`  `D.`

`|`

`| copy(...)`

`| D.copy()` `-``> a shallow copy of D`

`|`

`| get(``self``, key, default``=``None``,` `/``)`

`| Return the value` `for`  `key` `if`  `key` `is`  `in`  `the dictionary,` `else`  `default.`

`|`

`| items(...)`

`| D.items()` `-``> a` `set``-``like` `object`  `providing a view on D's items`

`|`

`| keys(...)`

`| D.keys()` `-``> a` `set``-``like` `object`  `providing a view on D's keys`

`|`

`| pop(...)`

`| D.pop(k[,d])` `-``> v, remove specified key` `and`  `return`  `the corresponding value.`

`| If key` `is`  `not`  `found, d` `is`  `returned` `if`  `given, otherwise KeyError` `is`  `raised`

`|`

`| popitem(...)`

`| D.popitem()` `-``> (k, v), remove` `and`  `return`  `some (key, value) pair as a`

`|` `2``-``tuple``; but` `raise`  `KeyError` `if`  `D` `is`  `empty.`

`|`

`| setdefault(``self``, key, default``=``None``,` `/``)`

`| Insert key with a value of default` `if`  `key` `is`  `not`  `in`  `the dictionary.`

`|`

`| Return the value` `for`  `key` `if`  `key` `is`  `in`  `the dictionary,` `else`  `default.`

`|`

`| update(...)`

`| D.update([E, ]``*``*``F)` `-``>` `None``. Update D` `from`  `dict``/``iterable E` `and`  `F.`

`| If E` `is`  `present` `and`  `has a .keys() method, then does:` `for`  `k` `in`  `E: D[k]` `=`  `E[k]`

`| If E` `is`  `present` `and`  `lacks a .keys() method, then does:` `for`  `k, v` `in`  `E: D[k]` `=`  `v`

`| In either case, this` `is`  `followed by:` `for`  `k` `in`  `F: D[k]` `=`  `F[k]`

`|`

`| values(...)`

`| D.values()` `-``> an` `object`  `providing a view on D's values`

`|`

`|` `-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-`

`| Class methods defined here:`

`|`

`| fromkeys(iterable, value``=``None``,` `/``)` `from`  `builtins.``type`

`| Create a new dictionary with keys` `from`  `iterable` `and`  `values` `set`  `to value.`

`|`

`|` `-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-`

`| Static methods defined here:`

`|`

`| __new__(``*``args,` `*``*``kwargs)` `from`  `builtins.``type`

`| Create` `and`  `return`  `a new` `object``. See` `help``(``type``)` `for`  `accurate signature.`

`|`

`|` `-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-``-`

`| Data` `and`  `other attributes defined here:`

`|`

`| __hash__` `=`  `None`

通过帮助文档，可以看到，程序可以使用花括号或者dict()函数创建字典，  
花括号创建字典，例：


`# 使用花括号创建字典`

`a` `=`  `{``'小红'``:``'学霸'``,``'小黑'``:``'学渣'``,``'老王'``:``'班主任'``}`

`print`  `(a)`

`# 打印 {'小红': '学霸', '小黑': '学渣', '老王': '班主任'}`

`# 使用花括号创建空字典`

`b` `=`  `{}`

`print`  `(b)`

`# 打印 {}`

`# 字典嵌套`

`c` `=`  `{``'学生'``:{``'小红'``:``'学霸'``,``'小黑'``:``'学渣'``},``'老师'``:{``'老王'``:``'班主任'``}}`

`print`  `(c)`

`# 打印 {'学生': {'小红': '学霸', '小黑': '学渣'}, '老师': {'老王': '班主任'}}`

`print`  `(c[``'学生'``])`

`# 打印 {'小红': '学霸', '小黑': '学渣'}`

`# 元组作为字典的key`

`d` `=`  `{(``'级长'``,``'班主任'``):``'老王'``,(``'学生'``,``'委员'``):``'小红'``}`

`print`  `(d)`

`# 打印 {('级长', '班主任'): '老王', ('学生', '委员'): '小红'}`

`print`  `(d[(``'学生'``,` `'委员'``)])`

`# 打印 '小红'`

使用dict函数创建字典，例：

```
`# 创建空字典`

`e` `=`  `dict``()`

`print`  `(e)`

`# 打印 {}`

`# 使用dict指定关键字参数创建字典，key不允许使用表达式`

`f` `=`  `dict``(k1` `=`  `1``,k2` `=`  `'v2'``)`

`print`  `(f)`

`# 打印 {'k1': 1, 'k2': 'v2'}`

`# 使用dict指定关键字参数创建字典，key使用表达式`

`y` `=`  `dict``(``1``=``1``,``2``=``2``)`

`# 报错：SyntaxError: keyword can't be an expression`

`# 创建两个键值对字典`

`h1` `=`  `[(``'k1'``,``1``),(``'k2'``,``2``)]`

`h` `=`  `dict``(h1)`

`print`  `(h1)`

`# 打印 {'k1': 1, 'k2': 2}`

`# 创建三个键值对字典`

`i1` `=`  `[[``'j1'``,``1``],[``'j2'``,``2``],[``'j3'``,``3``]]`

`i` `=`  `dict``(i1)`

`print`  `(i)`

`# 打印 {'j1': 1, 'j2': 2, 'j3': 3}`
```

## 2、字典用法

- 通过key访问value
```

`a` `=`  `{``'小红'``:``'学霸'``,``'小黑'``:``'学渣'``,``'老王'``:``'班主任'``}`

`# 通过key访问value`

`print`  `(a[``'小红'``])`

`# 打印 学霸`

`c` `=`  `{``'学生'``:{``'小红'``:``'学霸'``,``'小黑'``:``'学渣'``},``'老师'``:{``'老王'``:``'班主任'``}}`

`# 访问字典嵌套字典的value`

`c1` `=`  `c[``'学生'``]`

`print`  `(c1)`

`# 打印 {'小红': '学霸', '小黑': '学渣'}`

`print`  `(c1[``'小红'``])`

`# 打印 学霸`
```
- 通过key添加键值对

```

`# 创建字典`

`n` `=`  `dict``(k1` `=`  `1``,k2` `=`  `2``,k3` `=`  `3``)`

`# 通过key添加key-value对(需要为不存在的key赋值，如果已存在，会被覆盖)`

`n[``'k4'``]` `=`  `4`

`print`  `(n)`

`# 打印 {'k1': 1, 'k2': 2, 'k3': 3, 'k4': 4}`
```
- 通过key修改键值对

```
`m` `=`  `{``'k1'``:` `1``,` `'k2'``:` `2``,` `'k3'``:` `3``}`

`# 如果key已存在，则新的value会覆盖原来的value`

`m[``'k1'``]` `=`  `'覆盖'`

`print`  `(m)`

`# 打印 {'k1': '覆盖', 'k2': 2, 'k3': 3}`
```

- 通过in或not in运算符判断字典是否包含指定的key

```
`p` `=`  `{``'k1'``:` `1``,` `'k2'``:` `2``,` `'k3'``:` `3``,` `'k4'``:` `4``}`

`# 判断p是否包含名为'k1'的key`

`print`  `(``'k1'`  `in`  `p)`

`# 打印 True`

`print`  `(``'k1'`  `not`  `in`  `p)`

`# 打印 False`

`#判断p是否包含名为'k5'的key`

`print`  `(``'k5'`  `in`  `p)`

`# 打印 False`

`print`  `(``'k5'`  `not`  `in`  `p)`

`# 打印 True`
```

## 3、字典的常用方法

我们可以在Python交互模式中，输入dir(dict)查看dict类包含哪些方法，  
例：


`>>>` `dir``(``dict``)`

`[``'__class__'``,` `'__contains__'``,` `'__delattr__'``,` `'__delitem__'``,` `'__dir__'``,` `'__doc__'``,` `'__eq__'``,` `'__format__'``,` `'__ge__'``,` `'__getattribute__'``,` `'__getitem__'``,` `'__gt__'``,` `'__hash__'``,` `'__init__'``,` `'__init_subclass__'``,` `'__iter__'``,` `'__le__'``,` `'__len__'``,` `'__lt__'``,` `'__ne__'``,` `'__new__'``,` `'__reduce__'``,` `'__reduce_ex__'``,` `'__repr__'``,` `'__setattr__'``,` `'__setitem__'``,` `'__sizeof__'``,` `'__str__'``,` `'__subclasshook__'``,` `'clear'``,` `'copy'``,` `'fromkeys'``,` `'get'``,` `'items'``,` `'keys'``,` `'pop'``,` `'popitem'``,` `'setdefault'``,` `'update'``,` `'values'``]`

### 1）、clear()　　

用于清除一个字典的键值对，当一个字典执行clean()之后，这个字典将会变为空字典。


`>>>` `help``(``dict``.clear)`

`Help`  `on method_descriptor:`

`clear(...)`

`D.clear()` `-``>` `None``. Remove` `all`  `items` `from`  `D.<em` `id``=``"__mceDel"`  `style``=``"background-color: #ffffff; font-family: 'PingFang SC', 'Helvetica Neue', Helvetica, Arial, sans-serif; font-size: 14px;"``>　<``/``em>`

例：

```

`c` `=`  `dict``(k1` `=`  `1``,k2` `=`  `2``)`

`c.clear()`

`print``(c)`

`# 打印 {}`
```

### 2）、copy()　　

可复制一个字典的键值对。


`>>>` `help``(``dict``.copy)`

`Help`  `on method_descriptor:`

`copy(...)`

`D.copy()` `-``> a shallow copy of D`

例：

```
`c` `=`  `dict``(k1` `=`  `1``,k2` `=`  `2``)`

`d` `=`  `c.copy()`

`print``(d)`

`# 打印 {'k1': 1, 'k2': 2}`
```

### 3）、fromkeys()　

使用给定的多个key创建字典，这些key对应的value默认为None，该方法一般会使用dict类直接调用（字典对象调用没有什么意义）。



`>>>` `help``(``dict``.fromkeys)`

`Help`  `on built``-``in`  `function fromkeys:`

`fromkeys(iterable, value``=``None``,` `/``) method of builtins.``type`  `instance`

`Create a new dictionary with keys` `from`  `iterable` `and`  `values` `set`  `to value.`

例：

```

`a` `=`  `([``'k1'``,``'k2'``,``'k3'``])`

`b` `=`  `dict``.fromkeys(a)`

`print``(b)`

`# 打印 {'k1': None, 'k2': None, 'k3': None}`

`# 传入'test'作为默认的value`

`d` `=`  `([``'k1'``,``'k2'``,``'k3'``])`

`e` `=`  `dict``.fromkeys(d,``'test'``)`

`print``(e)`

`# 打印 {'k1': 'test', 'k2': 'test', 'k3': 'test'}`
```

### 4）、get()

如果key在字典中，则返回key对应的value值，否则返回default默认参数None。



`>>>` `help``(``dict``.get)`

`Help`  `on method_descriptor:`

`get(``self``, key, default``=``None``,` `/``)`

`Return the value` `for`  `key` `if`  `key` `is`  `in`  `the dictionary,` `else`  `default.`

例：

```
`a` `=`  `dict``(k1` `=`  `1``, k2` `=``2``)`

`print``(a.get(``'k1'``))`

`# 打印 1`

`print``(a.get(``'k10'``))`

`# 打印 None`

`# 传入“Not_found”作为默认的default`

`print``(a.get(``'k10'``,``'Not_found'``))`

`# 打印 Not_found`
```

### 5）、items()

用于获取字典中的所有键值对,返回dict_items对象。



`>>>` `help``(``dict``.items)`

`Help`  `on method_descriptor:`

`items(...)`

`D.items()` `-``> a` `set``-``like` `object`  `providing a view on D's items`

例：

```
`a` `=`  `dict``(k1` `=``1``,k2` `=`  `2``)`

`print``(a.items())`

`# 打印 dict_items([('k1', 1), ('k2', 2)])`

`# 将dict_items转换成list`

`print``(``list``(a.items()))`

`# 打印 [('k1', 1), ('k2', 2)]`
```

### 6）、keys()

用于返回字典中的所有key，返回dict_keys对象。

`>>>` `help``(``dict``.keys)`

`Help`  `on method_descriptor:`

`keys(...)`

`D.keys()` `-``> a` `set``-``like` `object`  `providing a view on D's keys`

例：
```

`a` `=`  `dict``(k1` `=``1``,k2` `=`  `2``)`

`print``(a.keys())`

`# 打印 dict_keys(['k1', 'k2'])`

`# 将dict_keys转换成list`

`print``(``list``(a.keys()))`

`# 打印 ['k1', 'k2']`
```

### 7）、values()

用于返回字典中的所有value，返回dict_values对象。



`>>>` `help``(``dict``.values)`

`Help`  `on method_descriptor:`

`values(...)`

`D.values()` `-``> an` `object`  `providing a view on D's values`

例：
```

`a` `=`  `dict``(k1` `=``1``,k2` `=`  `2``)`

`print``(a.values())`

`# 打印 dict_values([1, 2])`

`# 将dict_values转换为list`

`print``(``list``(a.values()))`

`# 打印 [1, 2]`
```

### 8）、popitem()

用于随机删除字典中的一个键值对，实际上字典的popitem()方法总是弹出底层存储的最后一个键值对。

`>>>` `help``(``dict``.popitem)`

`Help`  `on method_descriptor:`

`popitem(...)`

`D.popitem()` `-``> (k, v), remove` `and`  `return`  `some (key, value) pair as a`

`2``-``tuple``; but` `raise`  `KeyError` `if`  `D` `is`  `empty.`

例：

```

`a` `=`  `dict``(k1` `=``1``,k2` `=`  `2``,k3` `=`  `3``,k4` `=`  `4``,k5` `=`  `5``)`

`print``(a.popitem())`

`# 打印 ('k5', 5)`

`print``(a)`

`# 打印 {'k1': 1, 'k2': 2, 'k3': 3, 'k4': 4}`
```

### 9）、setdefault()

用于根据key获取对应的value，如果key在字典中不存在时，会先给这个key设置一个默认的value，再返回这个key对应的value。



`>>>` `help``(``dict``.setdefault)`

`Help`  `on method_descriptor:`

`setdefault(``self``, key, default``=``None``,` `/``)`

`Insert key with a value of default` `if`  `key` `is`  `not`  `in`  `the dictionary.`

`Return the value` `for`  `key` `if`  `key` `is`  `in`  `the dictionary,` `else`  `default.`

例：

``` python

`a` `=`  `dict``(k1` `=``1``,k2` `=`  `2``)`

`print``(a.setdefault(``'k1'``))`

`# 打印 1`

`print``(a.setdefault(``'k10'``))`

`# 打印 None`

`# 传入‘test’作为默认的default`

`print``(a.setdefault(``'k11'``,``'test'``))`

`#打印 test`

`print``(a)`

`# 打印 {'k1': 1, 'k2': 2, 'k10': None, 'k11': 'test'}`
```

### 10）、update()

在一个字典中，可根据key对已存在的键值对进行覆盖，如果key不存在，则该键值对会被添加进字典。



`>>>` `help``(``dict``.update)`

`Help`  `on method_descriptor:`

`update(...)`

`D.update([E, ]``*``*``F)` `-``>` `None``. Update D` `from`  `dict``/``iterable E` `and`  `F.`

`If E` `is`  `present` `and`  `has a .keys() method, then does:` `for`  `k` `in`  `E: D[k]` `=`  `E[k]`

`If E` `is`  `present` `and`  `lacks a .keys() method, then does:` `for`  `k, v` `in`  `E: D[k]` `=`  `v`

`In either case, this` `is`  `followed by:` `for`  `k` `in`  `F: D[k]` `=`  `F[k]`

例：

```

`a` `=`  `dict``(k1` `=``1``,k2` `=`  `2``)`

`# 根据key对已存在的key-value，覆盖value`

`a.update(k1` `=`  `3``)`

`print``(a)`

`# 打印 {'k1': 3, 'k2': 2}`

`# key不存在，该键值对会被添加进字典`

`a.update(k3` `=`  `10``)`

`print``(a)`

`# 打印 {'k1': 3, 'k2': 2, 'k3': 10}`
```

### 11）、pop()

用于根据key获取对应的value，并且删除该键值对。


`>>>` `help``(``dict``.pop)`

`Help`  `on method_descriptor:`

`pop(...)`

`D.pop(k[,d])` `-``> v, remove specified key` `and`  `return`  `the corresponding value.`

`If key` `is`  `not`  `found, d` `is`  `returned` `if`  `given, otherwise KeyError` `is`  `raised`

例：

```

`a` `=`  `dict``(k1` `=``1``,k2` `=`  `2``,k3` `=`  `3``,k4` `=`  `4``,k5` `=`  `5``)`

`print``(a.pop(``'k1'``))`

`# 打印 1`

`print``(a)`

`# 打印 {'k2': 2, 'k3': 3, 'k4': 4, 'k5': 5}`
```

### 4、注意事项

列表不允许对不存在的索引赋值，但字典允许对不存在的键赋值。  
例：


`p` `=`  `[``1``,``2``,``3``,``4``,``5``]`

`# 对不存在的索引赋值`

`p[``5``]` `=`  `666`

`# 报错 IndexError: list assignment index out of range`

`q` `=`  `dict``(a``=``1``,b``=``2``)`

`# 对不存在的key赋值`

`q[``'c'``]` `=`  `3`

`print`  `(q)`

`# 打印 {'a': 1, 'b': 2, 'c': 3}`