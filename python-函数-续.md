---
title: python 函数(续)
date: 2016-08-13 10:22:32
tags: python
categories: python
---

##**return语句**

return语句用来从一个函数 返回 即跳出函数。我们也可选从函数 返回一个值 。
没有返回值的return语句等价于return None。None是Python中表示没有任何东西的特殊类型。例如，如果一个变量的值为None，可以表示它没有值。

除非你提供你自己的return语句，每个函数都在结尾暗含有return None语句。
##文本基本处理
我们谈到“文本处理”时，我们通常是指处理的内容。Python 将文本文件的内容读入可以操作的字符串变量非常容易。文件对象提供了三个“读”方法： .read()、.readline() 和 .readlines()。每种方法可以接受一个变量以限制每次读取的数据量，但它们通常不使用变量。 .read() 每次读取整个文件，它通常用于将文件内容放到一个字符串变量中。然而 .read() 生成文件内容最直接的字符串表示，但对于连续的面向行的处理，它却是不必要的，并且如果文件大于可用内存，则不可能实现这种处理。
.readline() 和 .readlines() 非常相似。它们都在类似于以下的结构中使用：

Python .readlines() 示例

        fh = open( 'c:\\autoexec.bat')        
        for line in fh.readlines():                     
        print   line.readline() 
        readlines()

之间的差异是后者一次读取整个文件，象 .read()一样。.readlines()自动将文件内容分析成一个行的列表，该列表可以由 Python 的 for... in ... 结构进行处理。另一方面，.readline()每次只读取一行，通常比 .readlines()慢得多。仅当没有足够内存可以一次读取整个文件时，才应该使用.readline()。   

writeline()是输出后换行，下次写会在下一行写。write()是输出后光标在行末不会换行，下次写会接着这行写


##.seek()
需要注意的是它的语法如下这一点很重要：

fp.seek(offset, from_what)
哪里fp是你正在使用的文件指针; offset意味着你将多少位置移动; from_what定义的参考你的观点：

0：意味着你的参考点是开始该文件的
1：意味着你的参考点是当前文件位置
2：意味着你的参考点是最终的文件
如果省略，from_what默认为0。

永远不要忘记，管理文件的时候，总会有这个文件你在哪里目前正在对内部的位置。当只需打开，那个位置是文件的开始，但是当你使用它，你可能会提前。当你需要将是对你有用沿着打开的文件，就像你旅行到一个路径。
seek那个函数不返回值，你print淡然显示为None了

file.seek(0)是重新定位在文件的第0位及开始位置 
file = open("test.txt","rw")  #注意这行的变动
file.seek(3)  #定位到第3个
for i in file:
    print i
现在到了最后一位了
for i in file:
    print i
不会显示任何结果

file.seek(0) #定位到第0个

for i in file:
    print i 

**补充哦**
重新定位到0的好处是不用再次打开文件。


