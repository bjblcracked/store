---
title: 'python os,sys'
date: 2016-08-13 10:23:11
tags: python
categories: python
---
##sys
sys.argv           命令行参数List，第一个元素是程序本身路径 

sys.modules.keys() 返回所有已经导入的模块列表
 
sys.exc_info()     获取当前正在处理的异常类,exc_type、exc_value、exc_traceback当前处理的异常详细信息 

sys.exit(n)        退出程序，正常退出时exit(0) 

sys.hexversion     获取Python解释程序的版本值，16进制格式如：0x020403F0 

sys.version        获取Python解释程序的版本信息 

sys.maxint         最大的Int值 

sys.maxunicode     最大的Unicode值 

sys.modules        返回系统导入的模块字段，key是模块名，value是模块
 
sys.path           返回模块的搜索路径，初始化时使用PYTHONPATH环境变量的值 

sys.platform       返回操作系统平台名称 

sys.stdout         标准输出

sys.stdin          标准输入

sys.stderr         错误输出

sys.exc_clear()    用来清除当前线程所出现的当前的或最近的错误信息

sys.exec_prefix    返回平台独立的python文件安装的位置

sys.byteorder      本地字节规则的指示器，big-endian平台的值是'big',little-endian平台的值是'little'

sys.copyright      记录python版权相关的东西

sys.api_version    解释器的C的API版本

sys.version_info 

 sys.version_info

(2, 4, 3, 'final', 0) 'final'表示最终,也有'candidate'表示候选，表示版本级别，是否有后继的发行

sys.displayhook(value)      如果value非空，这个函数会把他输出到sys.stdout，并且将他保存进__builtin__._.指在python的交互式解释器里，'_'代表上次你输入得到的结果，hook是钩子的意思，将上次的结果钩过来

sys.getdefaultencoding()    返回当前你所用的默认的字符编码格式

sys.getfilesystemencoding() 返回将Unicode文件名转换成系统文件名的编码的名字

sys.setdefaultencoding(name)用来设置当前默认的字符编码，如果name和任何一个可用的编码都不匹配，抛出LookupError，这个函数只会被site模块的sitecustomize使用，一旦别site模块使用了，他会从sys模块移除

sys.builtin_module_names    Python解释器导入的模块列表 

sys.executable              Python解释程序路径 

sys.getwindowsversion()     获取Windows的版本 

sys.stdin.readline()        从标准输入读一行，sys.stdout.write("a") 屏幕输出a


##杂记
Python tips: 什么是*args和**kwargs？
先来看个例子：

```

def foo(*args, **kwargs):

    print 'args = ', args

    print 'kwargs = ', kwargs

    print '---------------------------------------'


if __name__ == '__main__':

    foo(1,2,3,4)

    foo(a=1,b=2,c=3)

    foo(1,2,3,4, a=1,b=2,c=3)

    foo('a', 1, None, a=1, b='2', c=3)

输出结果如下：

args =  (1, 2, 3, 4) 

kwargs =  {} 

--------------------------------------- 

args =  ()
 
kwargs =  {'a': 1, 'c': 3, 'b': 2}
 
---------------------------------------
 
args =  (1, 2, 3, 4) 

kwargs =  {'a': 1, 'c': 3, 'b': 2} 

-------------------------------------

args =  ('a', 1, None) 

kwargs =  {'a': 1, 'c': 3, 'b': '2'} 

---------------------------------------

```

可以看到，这两个是python中的可变参数。*args表示任何多个无名参数，它是一个tuple；**kwargs表示关键字参数，它是一个dict。并且同时使用*args和**kwargs时，必须*args参数列要在**kwargs前，像foo(a=1, b='2', c=3, a', 1, None, )这样调用的话，会提示语法错误“SyntaxError: non-keyword arg after keyword arg”。

 

呵呵，知道*args和**kwargs是什么了吧。还有一个很漂亮的用法，就是创建字典：

```

    def kw_dict(**kwargs):

        return kwargs

    print kw_dict(a=1,b=2,c=3) == {'a':1, 'b':2, 'c':3}

```

其实python中就带有dict类，使用dict(a=1,b=2,c=3)即可创建一个字典了。


* 是来告诉 Python 将函数得到的所有参数作为一个字符串列表放在args中。就像你使用过的 argv 一样。除了一些特别需要这种形式通常是比较少使用的。


##os模块

一、os模块概述

Python os模块包含普遍的操作系统功能。如果你希望你的程序能够与平台无关的话，这个模块是尤为重要的。(一语中的)

二、常用方法

1、os.name

输出字符串指示正在使用的平台。如果是window 则用'nt'表示，对于Linux/Unix用户，它是'posix'。

2、os.getcwd()

函数得到当前工作目录，即当前Python脚本工作的目录路径。

3、os.listdir()

返回指定目录下的所有文件和目录名。

 os.listdir(os.getcwd())

['Django', 'DLLs', 'Doc', 'include', 'Lib', 'libs', 'LICENSE.txt', 'MySQL-python-wininst.log', 'NEWS.txt', 'PIL-wininst.log', 'python.exe', 'pythonw.exe', 

'README.txt', 'RemoveMySQL-python.exe', 'RemovePIL.exe', 

'Removesetuptools.exe', 'Scripts', 'setuptools-wininst.log', 'tcl', 'Tools',

 'w9xpopen.exe']


4、os.remove()

删除一个文件。

5、os.system()

运行shell命令。

os.system('dir')

0

os.system('cmd') #启动dos

6、os.sep 可以取代操作系统特定的路径分割符。

7、os.linesep字符串给出当前平台使用的行终止符

os.linesep

'\r\n'            #Windows使用'\r\n'，Linux使用'\n'而Mac使用'\r'。

os.sep

'\\'              #Windows
 
8、os.path.split()

函数返回一个路径的目录名和文件名

os.path.split('C:\\Python25\\abc.txt')

('C:\\Python25', 'abc.txt')

9、os.path.isfile()和os.path.isdir()函数分别检验给出的路径是一个文件还是目录。

os.path.isdir(os.getcwd())

True

os.path.isfile('a.txt')

False

10、os.path.exists()函数用来检验给出的路径是否真地存在

os.path.exists('C:\\Python25\\abc.txt')

False

os.path.exists('C:\\Python25')

True


11、os.path.abspath(name):获得绝对路径

12、os.path.normpath(path):规范path字符串形式

13、os.path.getsize(name):获得文件大小，如果name是目录返回0L

14、os.path.splitext():分离文件名与扩展名

os.path.splitext('a.txt')

('a', '.txt')

15、os.path.join(path,name):连接目录与文件名或目录

os.path.join('c:\\Python','a.txt')

'c:\\Python\\a.txt'

os.path.join('c:\\Python','f1')

'c:\\Python\\f1'

16、os.path.basename(path):返回文件名

os.path.basename('a.txt')

'a.txt'

os.path.basename('c:\\Python\\a.txt')

'a.txt'
 
17、os.path.dirname(path):返回文件路径

os.path.dirname('c:\\Python\\a.txt')

'c:\\Python'


你应该很快注意到了我们 import 了又一个很好用的命令 exists。这个命令将文件名字符串作为参数，如果文件存在的话，它将返回 True，否则将返回 False。在本书的下半部分，我们将使用这个函数做很多的事情，不过现在你应该学会怎样通过 import 调用它。