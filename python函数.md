---
title: python函数
date: 2016-08-10 14:52:44
categories: python
tags: python
---
##all(iterable)
版本：该函数在python2.5版本首次出现，适用于2.5以上版本，包括python3，兼容python3版本。
说明：如果iterable的所有元素不为0、''、False或者iterable为空，all(iterable)返回True，否则返回False；函数等价于：

```

def all(iterable):

    for element in iterable:

        if not element:

            return False

    return True

```

参数iterable：可迭代对象；

示例：


```

all(['a', 'b', 'c', 'd'])  #列表list，元素都不为空或0

True

all(['a', 'b', '', 'd'])  #列表list，存在一个为空的元素

False

 all([0, 1，2, 3])  #列表list，存在一个为0的元素

False
  
all(('a', 'b', 'c', 'd'))  #元组tuple，元素都不为空或0

True

all(('a', 'b', '', 'd'))  #元组tuple，存在一个为空的元素

False

all((0, 1，2, 3))  #元组tuple，存在一个为0的元素

False
  
all([]) # 空列表

True

all(()) # 空元组

True

```

**注意：空元组、空列表返回值为True，这里要特别注意**
##any(iterable)
如果iterable的任何元素不为0、''、False,all(iterable)返回True。如果iterable为空，返回False。函数等价于：

注意比较该函数与all()函数的区别，any是任意，而all是全部。

```

def any(iterable):

   for element in iterable:

       if  element:

           return False

   return True

```

参数iterable：可迭代对象；

示例：
```

any(['a', 'b', 'c', 'd'])  #列表list，元素都不为空或0

True

any(['a', 'b', '', 'd'])  #列表list，存在一个为空的元素

True

any([0, '', False])  #列表list,元素全为0,'',false

False

any(('a', 'b', 'c', 'd'))  #元组tuple，元素都不为空或0

True

any(('a', 'b', '', 'd'))  #元组tuple，存在一个为空的元素

any((0, '', False))  #元组tuple，元素全为0,'',false

False
 
any([]) # 空列表

False

 any(()) # 空元组

False

```

##callable(object)
中文说明：检查对象object是否可调用。如果返回True，object仍然可能调用失败；但如果返回False，调用对象ojbect绝对不会成功。
注意：类是可调用的，而类的实例实现了__call__()方法才可调用。
版本：该函数在python2.x版本中都可用。但是在python3.0版本中被移除，而在python3.2以后版本中被重新添加。

英文说明：Return True if the object argument appears callable, False if not. If this returns true, it is still possible that a call fails, but if it is false, calling object will never succeed. Note that classes are callable (calling a class returns a new instance); class instances are callable if they have a __call__() method.

代码实例：
```
callable(0)

False

callable("mystring")

False

def add(a, b):
…     return a + b
…
callable(add)

True

class A:
…      def method(self):
…         return 0
…
callable(A)

True
 a = A()

callable(a)

False

class B:
…     def __call__(self):
…         return 0
…
callable(B)

True
b = B()

callable(b)

True

```
##chr()
通过help 查看相关函数的帮助文档

help (chr)

chr(...)

    chr(i) -> character    

    Return a string of one character with ordinal i; 0 <= i < 256.

参数是0 - 256 的一个整数，返回值是当前整数对应的ascii字符。参数可以是10进制也可以是16进制的形式


十六进制：

[python] view plain copy 在CODE上查看代码片派生到我的代码片
print chr(0x30), chr(0x31), chr(0x61)  
0 1 a  

十进制:

[python] view plain copy 在CODE上查看代码片派生到我的代码片
 print chr(48), chr(49), chr(97)  
0 1 a


##bin(x)
英文说明：Convert an integer number to a binary string. The result is a valid Python expression. If x is not a Python int object, it has to define an __index__() method that returns an integer.
New in version 2.6.
中文说明：将整数x转换为二进制字符串，如果x不为Python中int类型，x必须包含方法__index__()并且返回值为integer；
参数x：整数或者包含__index__()方法切返回值为integer的类型；
版本：bin函数是python2.6中新增函数，使用时要注意版本问题。
实例讲解：

bin(521)

**这里的显示结果形式与我们平时习惯有些差别，主要是前面多了0b，这是表示二进制的意思。**
'0b1000001001'
**非整型的情况，必须包含__index__()方法切返回值为integer的类型**
```

class myType:
... 　　def __index__(self):
... 　　　　return 35
    
myvar = myType()

```
 bin(myvar)
    
'0b1000001001'

PS:改函数非常简单，但是要注意版本，和参数类型


3

len(bin(5))

bin()函数用法 bin(number)-> string. 返回整型（integer）或长整型（long）的二进制表示，返回类型为字符串。

a = bin(5) print a 得到 a = '0b101'. '0b'表示二进制表示，‘101’为正数5的二进制表示。因为返回类型为string，故len()后得到为5.

Answer：5

##同行打印
你的意思是想要输出什么格式呢？
要是输出：abcd，可以不用for,直接print(a)
要是中间需要加空格，可以讲你的print语句改成：print(i,end = ' '）