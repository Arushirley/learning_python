
# Python新手简单练习题

![](https://csdnimg.cn/release/phoenix/template/new_img/original.png)

置顶  [萨克买单](https://me.csdn.net/qq_40302589)  2019-07-17 18:14:12  ![](https://csdnimg.cn/release/phoenix/template/new_img/articleReadEyes.png)  5525 ![](https://csdnimg.cn/release/phoenix/template/new_img/tobarCollect.png)  收藏  52

分类专栏：  [Pyhon](https://blog.csdn.net/qq_40302589/category_9133057.html)

版权

## Python新手简单练习题

（1）设计“过7游戏”的程序，打印1-100之间除了含7和7的倍数以外的数字。

```python
for i in range(101):
    if i%7!=0:
        print(i,end=" ")

```

```python
运行结果：
1 2 3 4 5 6 8 9 10 11 12 13 15 16 17 18 19 20 22 23 24 25 26 27 29 30 31 32 33 34 36 37 38 39 40 41 43 44 45 46 47 48 50 51 52 53 54 55 57 58 59 60 61 62 64 65 66 67 68 69 71 72 73 74 75 76 78 79 80 81 82 83 85 86 87 88 89 90 92 93 94 95 96 97 99 100 

```

（2）编写程序用户登录程序且仅有三次机会（if和for）

```python
name = "admin"
password = "123456"
i = 3
while i > 0:
    iname = input("请输入用户名：")
    ipassword = input("请输入用户密码")
    if iname == name and ipassword == password:
        print("登录成功")
        break
    else:
        print("登录失败，请重新输入！")
        i -= 1
else:
    print("您已经失败三次，无法登录了！")

```

```python
运行结果：请输入用户名：admin
请输入用户密码123456
登录成功

```

( 3 ) 编写程序实现，一串字符串是否为有效变量名

```python
str1 = input("请输入一串字符:")
if '_' in str1:
    str2=str1.replace('_','a')
    if str2.isalnum():
        if str2[0].isdigit():
            print("该字符为非法变量名")
        else:
            print("该字符为合法变量名")
    else:
        print("该字符为非法变量名")
elif '_' not in str1:
    if str1.isalnum():
        if str1[0].isdigit():
            print("该字符为非法变量名")
        else:
            print("该字符为合法变量名")
    else:
        print("该字符为非法变量名")

```

```python
运行结果：
请输入一串字符:_.'';'
该字符为非法变量名

```

( 4 )最多猜10次的游戏，猜测范围1-100，根据input内容提示猜大或者猜小，如果猜中，结束循环。

```python
import random
realnum = random.randint(1, 100)
i = 0
while i <= 10:
    guessnum = int(input("请输入一个1-100之间的数"))
    i += 1
    if guessnum == realnum:
        print("恭喜你，猜对了！你总共用了", i,"次")
        break
    elif guessnum<realnum:
        print("你猜小了！")
        i=i+1
    else:
        print("你猜大了！")
else:
    print("你已经猜错10次，没有机会了！")

```

```python
运行结果：
请输入一个1-100之间的数50
你猜小了！
请输入一个1-100之间的数75
你猜大了！
请输入一个1-100之间的数63
你猜大了！
请输入一个1-100之间的数58
你猜小了！
请输入一个1-100之间的数61
你猜小了！
请输入一个1-100之间的数62
恭喜你，猜对了！你总共用了 9 次

```

( 5 )使用while循环实现2-3+4-5+6…+100的和。

```python
num=2
count=0
while num <=100:
    if num%2==0:
        count=count+num
    else:
        count=count-num
    num+=1
print(count)

```

```python
运行结果：
51

```

( 6 )使用循环实现九九乘法表

```python
for i in range(1, 10):
    for x in range(1, i + 1):
        print('%d X %d = %d' % (i, x, i * x), end='  ')
    print('\n')

```

```python
运行结果：
1 X 1 = 1  

2 X 1 = 2  2 X 2 = 4  

3 X 1 = 3  3 X 2 = 6  3 X 3 = 9  

4 X 1 = 4  4 X 2 = 8  4 X 3 = 12  4 X 4 = 16  

5 X 1 = 5  5 X 2 = 10  5 X 3 = 15  5 X 4 = 20  5 X 5 = 25  

6 X 1 = 6  6 X 2 = 12  6 X 3 = 18  6 X 4 = 24  6 X 5 = 30  6 X 6 = 36  

7 X 1 = 7  7 X 2 = 14  7 X 3 = 21  7 X 4 = 28  7 X 5 = 35  7 X 6 = 42  7 X 7 = 49  

8 X 1 = 8  8 X 2 = 16  8 X 3 = 24  8 X 4 = 32  8 X 5 = 40  8 X 6 = 48  8 X 7 = 56  8 X 8 = 64  

9 X 1 = 9  9 X 2 = 18  9 X 3 = 27  9 X 4 = 36  9 X 5 = 45  9 X 6 = 54  9 X 7 = 63  9 X 8 = 72  9 X 9 = 81  

```

( 7 )已知列表 li=[22478,24066,23398,38498],利用字符串拼接遍历，输出结果“城市学院”

```python
li=[22478,24066,23398,38498]
str1=''
for i in li:
    str1=str1+chr(i)
print(str1)

```

```python
运行结果：
城市学院

```

## 博主qq:1031748759.欢迎批评指正！！！