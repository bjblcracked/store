---
title: python keywords
date: 2016-08-15 19:47:49
tags: python
categories: python
---
**##raise:**

引发异常,raise [exception[,data]]

在Python中，要想引发异常，最简单的形式就是输入关键字raise，后跟要引发的异常的名称。

异常名称标识出具体的类：Python异常是那些类的对象。执行raise语句时，Python会创建指定的异常类的一个对象。

raise语句还可指定对异常对象进行初始化的参数。为此，请在异常类的名称后添加一个逗号以及指定的参数（或者由参数构成的一个元组）。

```

try:

    raise MyError #自己抛出一个异常

except MyError:

    print 'a error'


raise ValueError,’invalid argument’

捕捉到的内容为:

type  = VauleError

message = invalid argument

```

**##pass:**

pass语句在函数中的作用

当你在编写一个程序时，执行语句部分思路还没有完成，这时你可以用pass语句来占位，也可以当做是一个标记，是要过后来完成的代码。比如下面这样：

```

def iplaypython():

       pass

```

定义一个函数iplaypython，但函数体部分暂时还没有完成，又不能空着不写内容，因此可以用pass来替代占个位置。

pass语句在循环中的作用

pass也常用于为复合语句编写一个空的主体，比如说你想一个while语句的无限循环，每次迭代时不需要任何操作，你可以这样写：

```

while True:

    pass

```

以上只是举个例子，现实中最好不要写这样的代码，因为执行代码块为pass也就是空什么也不做，这时python会进入死循环。

pass语句用法总结:

1、空语句，什么也不做

2、在特别的时候用来保证格式或是语义的完整性


**##assert:**

1,assert语句用来声明某个条件是真的。

2、如果你非常确信某个你使用的列表中至少有一个元素，而你想要检验这一点，并且在它非真的时候引发一个错误，那么assert语句是应用在这种情形下的理想语句。

3、当assert语句失败的时候，会引发一AssertionError

```

mylist = ['item']

assert len(mylist) >= 1

mylist.pop()

'item'

assert len(mylist) >= 1

Traceback (most recent call last):

 File "<stdin>", line 1, in <module>

AssertionError


```

**##with:**

python中with可以明显改进代码友好度，比如：

```

with open('a.txt') as f:  

    print f.readlines()  

```

为了我们自己的类也可以使用with， 只要给这个类增加两个函数__enter__, __exit__即可：

```

class A:  

    def __enter__(self):
  
        print 'in enter' 
 
    def __exit__(self, e_t, e_v, t_b):  

        print 'in exit'  

  
with A() as a:  

    print 'in with' 
 
  
in enter  

in with  

in exit  

```

另外python库中还有一个模块contextlib，使你不用构造含有__enter__, __exit__的类就可以使用with：

```

from contextlib import contextmanager 
 
from __future__ import with_statement 
 
@contextmanager  

def context():  

print 'entering the zone'  

   try:  

        yield  

    except Exception, e: 
 
         print 'with an error %s'%e  

         raise e  

     else:  

        print 'with no error'  

 
with context():  


     print '----in context call------'
  
  

entering the zone  

----in context call------ 
 
with no error  

```

使用的最多的就是这个contextmanager, 另外还有一个closing 用处不大

```

from contextlib import closing  

import urllib  
  
with closing(urllib.urlopen('http://www.python.org')) as page: 
 
    for line in page:  

        print line  

```

**##global:**

如果你想要为一个定义在函数外的变量赋值，那么你就得告诉Python这个变量名不是局部的，而是 全局 的。我们使用global语句完成这一功能。没有global语句，是不可能为定义在函数外的变量赋值的。你可以使用定义在函数外的变量的值（假设在函数内没有同名的变量）。然而，我并不鼓励你这样做，并且你应该尽量避免这样做，因为这使得程序的读者会不清楚这个变量是在哪里定义的。使用global语句可以清楚地表明变量是在外面的块定义的。

```

!/usr/bin/python

Filename: func_global.py

def func():

　　global x

　　print 'x is', x

　　x = 2

　　print 'Changed local x to', x


x = 50

func()

print 'Value of x is', x

（源文件：code/func_global.py）


　　输出

$ python func_global.py

x is 50

Changed global x to 2

Value of x is 2

```

global语句被用来声明x是全局的——因此，当我们在函数内把值赋给x的时候，这个变化也反映在我们在主块中使用x的值的时候。你可以使用同一个global语句指定多个全局变量。例如global x, y, z。


**##del:**

python del方法从列表中删除某个项目索引,这个和列表的pop方法不一样，pop方法则返回一个值。

```

a = [-1, 1, 66.25, 333, 333, 1234.5]

del a[0]

a

[1, 66.25, 333, 333, 1234.5]

del a[2:4]

 a

[1, 66.25, 1234.5]

del a[:]

a

[]

也可用于删除整个变量： del a


```

