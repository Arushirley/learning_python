
## [Python3中的关键字](https://www.cnblogs.com/PastimeRr/p/8305022.html)

共计33个：请看注释->

（关于关键字的解释我会随着对Python的深入了解而不断的完善。）

 1 false  
　 #布尔类型的值，表示假，与true对应  
 2 class
　 #定义类的关键字  
　　  
 3 finally  
　 #异常处理使用的关键字，用它可以指定始终执行的代码，指定代码在finally里面  
　　　　例如：  
　　　　　　class MyException(Exception):pass  
　　　　　　try:  
　　　　　　　　#some code here  
　　　　　　　　raise MyException  
　　　　　　except MyException:  
　　　　　　　　print "MyException encoutered"  
　　　　　　finally:  
　　　　　　　　print "Arrive finally"

 4 is  
　 #Python中的对象包含三个要素：id,type,value  
　　其中：  
　　　　id:用来唯一标示一个对象  
　　　　type：标识对象的类型  
　　　　value：是对象的值  
　　is：就是用来判断a对象是否就是b对象，是通过id来判断的  
　　==：判断的是a对象的值是否和b对象的值相等，是通过value来判断的  
　　　　例如：  
　　　　　　>>> a = 1  
　　　　　　>>> b = 1.0  
　　　　　　>>> a is b  
　　　　　　False  
　　　　　　>>> a == b  
　　　　　　True  
　　　　　　>>> id(a)  
　　　　　　12777000  
　　　　　　>>> id(b)  
　　　　　　14986000

 5 return  
　 #python 函数返回值 return，函数中一定要有return返回值才是完整的函数。如果你没有python定义函数返回值，那么会得到一个结果是None对象，而None表示没有任何值。  
　　　　例如：  
　　　　　　def fnc1(x,y):  
 print x+y  
　　　　　　当函数没有显示return，默认返回none值，以下测试：  
　　　　　　　　>>> result = fnc1(2, 3)  
　　　　　　　　>>> result is None  
　　　　　　　　True  
 6 none  
#None是一个特殊的常量，None和False不同，None不是0。None不是空字符串。None和任何其他数据类型比较永远返回False。None有自己的数据类型NoneType。我们可以将None复制给任何变量，但是不能创建其他NoneType对象。 　　　　例如：  
　　　　　　>>> type(None)    
　　　　　　<class 'NoneType'>    
　　　　　　>>> None == 0    
　　　　　　False    
　　　　　　>>> None == ''    
　　　　　　False    
　　　　　　>>> None == None    
　　　　　　True    
　　　　　　>>> None == False 　　　　　　False  
  
 7 continue  
　　#continue语句被用来告诉Python跳过当前循环块中的剩余语句，然后继续进行下一轮循环。  

 8 for  
　　#for循环可以遍历任何序列的项目，如一个列表或者一个字符串  
　　　　例如：  
　　　　　　for letter in 'Python': # 第一个实例 print '当前字母 :', letter fruits = ['banana', 'apple', 'mango'] for fruit in fruits: # 第二个实例 print '当前水果 :', fruit print "Good bye!"  
 9 lambda  
　　#匿名函数是个很时髦的概念，提升了代码的简洁程度。  
　　　　例如：  
　　　　　　g = lambda x:x+1  
　　　　运行结果：  
　　　　　　g(1)  
　　　　　　>>>2  
　　　　　　g(2)  
　　　　　　>>>3  
　　　　　　g(7)  
　　　　　　>>>8  
　　　　再例如：  
　　　　　　>>> foo = [2, 18, 9, 22, 17, 24, 8, 12, 27]  
　　　　　　>>>  
　　　　　　>>> print filter(lambda x: x % 3 == 0, foo)  
　　　　　　[18, 9, 24, 12, 27]  
　　　　　　>>>  
　　　　　　>>> print map(lambda x: x * 2 + 10, foo)  
　　　　　　[14, 46, 28, 54, 44, 58, 26, 34, 64]  
　　　　　　>>>  
　　　　　　>>> print reduce(lambda x, y: x + y, foo)  
　　　　网络上有人总结：  
　　　　　　lambda 是为了减少单行函数的定义而存在的。  

10 try  
　　#程序员可以使用try…except语句来处理异常。把通常的语句块放在try块中，而把错误处理的语句放在except块中。  

11 true  
　　#布尔类型的值，表示真，与false相反。 12 def  
　　#定义函数用的  
　　　　例如：  
　　　　　　def hello()  
　　　　　　　　print('hello,hongten')  
　　　　　　调用：  
　　　　　　hello()  
　　　　　　结果：  
　　　　　　>>>hello,hongten  
13 from  
　　#在python用import或者from…import来导入相应的模块。  
14 nonlocal  
　　#nonlocal关键字用来在函数或其他作用域中使用外层（非全局）变量。  
　　　　例如：  
　　　　　　def make_counter():  
　　　　　　　　count = 0  
　　　　　　　　def counter():  
　　　　　　　　　　nonlocal count  
　　　　　　　　　　count += 1  
　　　　　　　　　　return count  
　　　　　　　　return counter  
  
　　　　　　def make_counter_test():  
　　　　　　　　mc = make_counter()  
　　　　　　　　print(mc())  
　　　　　　　　print(mc())  
　　　　　　　　print(mc()) 15 while  
　　#while语句重复执行一块语句。while是循环语句的一种，while语句有一个可选的else从句。  
16 and  
　　#逻辑判断语句，and左右两边都为真，则判断结果为真，否则都是假  
17 del  
　　#del用于list列表操作，删除一个或者连续几个元素。  
　　　　例如：  
　　　　　　a = [-1,3,'aa',85] # 定义一个list  
　　　　　　del a[0] # 删除第0个元素  
　　　　　　del a[2:4] # 删除从第2个到第3个元素。  
18 global  
　　#定义全局标量。  
19 not  
　　#逻辑判断，取反的意思  
20 with  
　　#with是python2.5以后有的，它实质是一个控制流语句，with可以用来简化try…finally语句，它的主要用法是实现一个类_enter_()和_exit_()方法。  
　　　　例如：  
　　　　　　class controlled_execution:  
　　　　　　　　def _enter_(self):  
　　　　　　　　　　set things up  
　　　　　　　　　　return thing  
　　　　　　　　def _exit_(self,type,value,traceback):  
　　　　　　　　　　tear thing down  
　　　　　　with controlled_execution() as thing:  
　　　　　　　　some code 21 as  
　　#结合with使用。 22 elif  
　　#和if配合使用的  
23 if  
　　#if语句用来检验一个条件，如果条件为真，我们运行一块语句(称为if…块)，否则我们处理另外一块语句（称为else…块）。else从句是可选的。  
24 or  
　　#逻辑判断，or两边有一个为真，判断结果就是真。  
25 yield  
　　#yield用起来像return,yield在告诉程序，要求函数返回一个生成器  
　　　　例如：  
　　　　　　def createGenerator():  
　　　　　　mylist = range(3)  
　　　　　　for i in mylist:  
　　　　　　yield i*i  
26 assret  
　　#断言，用来在运行中检查程序的正确性，和其他语言一样的作用。  
　　　　例如：  
　　　　　　assert len(mylist) >= 1 27 else  
　　#与if配合使用  
28 import  
　　#在Python用import或者from…import来导入相应的模块。  
　　　　例如：  
　　　　　　from sys import *  
　　　　　　print（‘path’,path）  
29 pass  
　　#pass的意思是什么都不要做，作用是为了弥补语法和空定义上的冲突，它的好处体现在代码的编写过程之中，比如你可以先写好软件的整个框架，然后再填好框架内具体函数和class的内容，如果没有pass编译器会报一堆的错误，让整个开发很不流畅。  
　　　　例如：  
　　　　　　def f(arg): pass # a function that does nothing (yet)  
　　　　　　class C: pass    # a class with no methods(yet)  
30 break  
　　#break语句是用来终止循环语句的，即使哪怕循环条件没有称为false或者序列还没有被完全递归，也会停止循环语句。提示，如果break的是for或while循环，任何对应的循环else块将不执行。  
31 except  
　　#使用try和except语句来铺货异常。  
32 in  
　　#for…in是另外一个循环语句，它在一序列的对象上递归即逐一使用队列中的每个项目。  
33 raise  
　　#railse抛出异常。  
　　　　例如：  
　　　　　　class MyException(Exception):pass  
　　　　　　try:  
　　　　　　　　#some code here  
　　　　　　　　raise MyException  
　　　　　　except MyException:  
　　　　　　　　print('MyException encoutered')  
　　　　　　finally:  
　　　　　　　　print('Arrive finally')  

