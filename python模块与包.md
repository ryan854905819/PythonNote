# 模块
-----
一个模块就是一个包含了python定义和声明的文件，文件名就是模块名字加上.py的后缀。

模块分类：

- python标准库
- 第三方模块
- 应用程序自定义模块


模块使用：

模块导入方法

1 import 语句

    import module1[, module2[,... moduleN]
    
2 from…import 语句 

    from modname import name1[, name2[, ... nameN]]  
对比import spam，会将源文件的名称空间'spam'带到当前名称空间中，使用时必须是spam.名字的方式

而from 语句相当于import，也会创建新的名称空间，但是将spam中的名字直接导入到当前的名称空间中，在当前名称空间中，直接使用名字就可以了.    
    
    
    
写一个简单模块例子：
    
    示例文件：spam.py，文件名spam.py,模块名spam


     #spam.py
    print('from the spam.py')
      
    money=1000
      
    def read1():
        print('spam->read1->money',money)
      
    def read2():
        print('spam->read2 calling read')
        read1()
     
    def change():
        global money
        money=0
        
        
模块可以包含可执行的语句和函数的定义，这些语句的目的是初始化模块，它们只在模块名第一次遇到导入import语句时才执行（import语句是可以在程序中的任意位置使用的,且针对同一个模块很import多次,为了防止你重复导入，python的优化手段是：第一次导入后就将模块名加载到内存了，后续的import语句仅是对已经加载大内存中的模块对象增加了一次引用，不会重新执行模块内的语句）    


当我们使用import语句的时候，Python解释器是怎样找到对应的文件的呢？答案就是解释器有自己的搜索路径，存在sys.path里。


查看导入内存的模块： sys.modules 查询结果如下面这种字典格式

{zipimport':< module 'zipimport' (built-in) >,.....}


 每个模块都是一个独立的名称空间，定义在这个模块中的函数，把这个模块的名称空间当做全局名称空间，这样我们在编写自己的模块时，就不用担心我们定义在自己模块中全局变量会在被导入时，与使用者的全局变量冲突

测试一:money与spam.money不冲突

     2 #test.py
     3 import spam 
     4 money=10
     5 print(spam.money)
     6 
     7 '''
     8 执行结果：
     9 from the spam.py
    10 1000
    11 '''


测试二：read1与spam.read1不冲突

     2 #test.py
     3 import spam
     4 def read1():
     5     print('========')
     6 spam.read1()
     7 
     8 '''
     9 执行结果:
    10 from the spam.py
    11 spam->read1->money 1000
    12 '''

测试三：执行spam.change()操作的全局变量money仍然是spam中的

     2 #test.py
     3 import spam
     4 money=1
     5 spam.change()
     6 print(money)
     7 
     8 '''
     9 执行结果：
    10 from the spam.py
    11 0
    12 '''

总结：首次导入模块spam时会做三件事：

1.为源文件(spam模块)创建新的名称空间，在spam中定义的函数和方法若是使用到了global时访问的就是这个名称空间。

2.在新创建的命名空间中执行模块中包含的代码

3.创建名字spam来引用该命名空间

    这个名字和变量名没什么区别，都是‘第一类的’，且使用spam.名字的方式可以访问spam.py文件中定义的名字，spam.名字与test.py中的名字来自两个完全不同的地方。
 

为模块名起别名，相当于m1=1;m2=m1 

    import spam as sm
    print(sm.money)
    
    from spam import read1 as read

为模块起别名的方式对编写可扩展的代码很有用，假设有两个模块xmlreader.py和csvreader.py，它们都定义了函数read_data(filename):用来从文件中读取一些数据，但采用不同的输入格式。可以编写代码来选择性地挑选读取模块，例如

    1 if file_format == 'xml':
    2     import xmlreader as reader
    3 elif file_format == 'csv':
    4     import csvreader as reader
    5 data=reader.read_date(filename)

在一行导入多个模块

    import sys,os,re
    
也支持导入多行

    1 from spam import (read1,
    2                   read2,
    3                   money)



from spam import \*

把spam中所有的不是以下划线(_)开头的名字都导入到当前位置，大部分情况下我们的python程序不应该使用这种导入方式，因为*你不知道你导入什么名字，很有可能会覆盖掉你之前已经定义的名字。而且可读性极其的差，在交互式环境中导入时没有问题。

     1 from spam import * #将模块spam中所有的名字都导入到当前名称空间
     2 print(money)
     3 print(read1)
     4 print(read2)
     5 print(change)
     6 
     7 '''
     8 执行结果:
     9 from the spam.py
    10 1000
    11 <function read1 at 0x1012e8158>
    12 <function read2 at 0x1012e81e0>
    13 <function change at 0x1012e8268>
    14 '''

可以使用__all__来控制\* ,在spam.py中新增一行

\_\_all\_\_=['money','read1'] #这样在另外一个文件中用from spam import *就这能导入列表中规定的两个名字


注意：考虑到性能的原因，每个模块只被导入一次,放入字典sys.modules中，如果你改变了模块的内容，你必须重启程序，python不支持重新加载或卸载之前导入的模块.



\_\_name\_\_使用:



.py文件当做脚本运行：
\_\_name\_\_ 等于'\_\_main\_\_'

当做模块导入：
\_\_name\_\_= 等于模块名称

作用：用来控制.py文件在不同的应用场景下执行不同的逻辑

if \_\_name\_\_ == '\_\_main\_\_':



模块搜索路径

python解释器在启动时会自动加载一些模块，可以使用sys.modules查看

在第一次导入某个模块时（比如spam），会先检查该模块是否已经被加载到内存中（当前执行文件的名称空间对应的内存），如果有则直接引用

如果没有，解释器则会查找同名的内建模块，如果还没有找到就从sys.path给出的目录列表中依次寻找spam.py文件。

所以总结模块的查找顺序是：内存中已经加载的模块->内置模块->sys.path路径中包含的模块


需要特别注意的是：我们自定义的模块名不应该与系统内置模块重名。

----
## 包(package)

如果不同的人编写的模块名相同怎么办？为了避免模块名冲突，Python又引入了按目录来组织模块的方法，称为包（Package）。


包是一种通过使用‘.模块名’来组织python模块名称空间的方式。

1.无论是import形式还是from...import形式，凡是在导入语句中（而不是在使用时）遇到带点的，都要第一时间提高警觉：这是关于包才有的导入语法


2.包是目录级的（文件夹级），文件夹是用来组成py文件（包的本质就是一个包含__init__.py文件的目录）

3.import导入文件时，产生名称空间中的名字来源于文件，import 包，产生的名称空间的名字同样来源于文件，即包下的__init__.py，导入包本质就是在导入该文件

说明：包A和包B下有同名模块也不会冲突，如A.a与B.a来自俩个命名空间


创建以下一个包文件：

    pack/                   
    
    ├── __init__.py     
    
    ├── bin                  
    
    │   ├── __init__.py
    
    │   └── bin.py
    
    │   
    
    ├── calculate               
    
    │   ├── __init__.py
    
    │   └── sc_cal.py
    
    └── log                 
    
        ├── __init__.py
    
        ├── func.py
        
        └── logger.py
文件内容:
    
    #bin.py
    import os,sys
    BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
    print(BASE_DIR)
    sys.path.insert(0,BASE_DIR)
    from log import logger
    from calculate import sc_cal
    
    logger_obj = logger.get_logger()
    logger_obj.error("error")
    sc_cal.add(2,3)

    #sc_cal.py
    def add(x,y):
    print(x+y)


    # func.py
    def mul(x,y):
    return x*y


     #logger.py
    import logging
    from log import  func
    def get_logger():
        logger = logging.getLogger()
        fh = logging.FileHandler("log.txt")
        logger.addHandler(fh)
        return logger
    
    print(func.mul(2,3))

