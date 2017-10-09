 # python对象的相关术语
 - python程序中保存的所有数据都是围绕对象的概念展开的
- 程序中存储的所有数据都是对象
- 每个对象都有一个身份、一个类型和一个值
对象的身份：

      In [4]: name = 'xiangge'

      In [5]: id(name)
    
      Out[5]: 139851606368640
对象的类型：

    In [6]: type(name)
    Out[6]: builtins.str

- 对象的类型决定对象可以参与的操作（可以理解成支持的函数操作），python是属性强类型的语言。
- 创建特定类型的对象时，也可以称该对象为该类型的事例化。
- 事例被创建后，其身份和类型就不可改变。值分两种可变和不可变的，可变称可变对象，如列表，字典。不可变的称为不可变对象如字符串，元组，数字都是不可变对象。
- 某个对象包含对其他对象的引用，则将其称为容器,如：列表。 
- 大多数对象都拥有大量特有的数据属性和方法
属性：与对象相关的值（对象事例化时给对象内部变量赋的值）
方法：被调用时讲在对象上执行某些操作的函数。
使用点（）运算符可以访问属性和方法。

- 查询某一种内置类型所支持的内置方法

    help（类型）

两对象的比较：

1.值比较：对象中的数据是否相同

     In [7]: num1 = 5

    In [8]: num2 = 5

    In [9]: num1 == num2
    Out[9]: True


2.身份比较：两个变量名引用的是
 
    In [10]: id(num1)
    Out[10]: 9306112

    In [11]: id(num2)
    Out[11]: 9306112

    In [12]: num1 is num2
    Out[12]: True



3.类型比较：两个对象的类型是否相同

    In [13]: type(num1) is type(num2)
    Out[13]: True

----

## python核心数据类型
对象的类型

- 数字:int,long,float,complex,bool
- 字符:str,unicod
- 列表:list
- 字典:dict
- 元组:tuple
- 文件:file
- 其他类型:集合（set）,冻结集合(frozenset)，类类型等。

类型转换的函数：
str(),repr()或format()：将非字符型数据转换成字符型

int（）：转为整型

float（）：转为浮点型

    In [14]: str1 = '45'
    In [15]: type(str1)
    Out[15]:str
    In [16]: num3 =int(str1)  
    In [19]: type(num3)
    Out[19]: int
    
list():可以将字串转成列表
   
    In [20]: str3 = 'xiangge'
    In [21]: l1 = list(str3)
    In [23]: print(l1)
    ['x', 'i', 'a', 'n', 'g', 'g', 'e']
    In [24]: type(l1)
    Out[24]: builtins.list

tuple():将字串转换成元组

set():将字串转换成集合，集合没有次序，并且把重复的都去掉。

    In [20]: str3 = 'xiangge'

    In [25]: s1 = set(str3)
    In [26]: type(s1)
    Out[26]: set
    In [27]: print(s1)
    {'a', 'e', 'n', 'g', 'i', 'x'}

dict():转换为字典

    In [28]: l3 = [('a',1),('b',2),('c',3)]

    In [29]: print(l3)
    [('a', 1), ('b', 2), ('c', 3)]

    In [30]: d1 = dict(l3)

    In [31]: print(d1)
    {'a': 1, 'b': 2, 'c': 3}

chr（）:将整数转为字符

ord（）：将字符串转换成整数

hex():将整数转换16进制

bin():将整数转2进制

oct(x):将整数转8进制

-----
### 数字类型
python的数字字面量：布尔型，整数，浮点数，复数。所有数字类型均不可变。
数字操作：
+，-，*，/，\*\*，%，
<<(左移位)，>>(右移位)，&按位与，|按位或

----
### 序列类型

序列表示索引为非负整数的有序对象集合，包括字符串、列表和元组。字符串和元组属于不可变序列，所有序列都支持迭代。


####  适用所有序列的操作和方法

- s[i]: 索引运算
- s[i:j]: 为切片运算符
- s[i:j:stride]: 为扩展切片运算符
- len（s）: 序列长度
- min(s) : s中最小值
- max(s):s中最大值
- sum（s）: s中各项和
- all（s）:检查s中的所有项是否为True
- any(s) : 检查s中的任意项是否为True

#### 适用于可变序列的操作
- s[i] = v  项目赋值
- s[i:j] =t 切片赋值
- s[i:j:stride] = t 扩展切片赋值
- del s[i] 项目删除
- del s[i:j] 切片删除
- del s[i:j:stride] 扩展切片删除
----

### 字符串介绍

定义：它是一个有序的字符的集合，用于存储和表示基本的文本信息，‘’或“”或‘’‘ ’‘’中间包含的内容称之为字符串
特性：
1.只能存放一个值
2.不可变
3.按照从左到右的顺序定义字符集合，下标从0开始顺序访问，有序
补充：
　　1.字符串的单引号和双引号都无法取消特殊字符的含义，如果想让引号内所有字符均取消特殊意义，在引号前面加r，如name＝r'l\thf'
　　2.unicode字符串与r连用必需在r前面，如name＝ur'l\thf' 

2.2.2.1 字符串创建

‘hello world’

2.2.2.2 字符串常用操作

移除空白
S.strip([chars]) -> str  前后空白移除

     def strip(self, chars=None): # real signature unknown; restored from __doc__
        """
        S.strip([chars]) -> str

        Return a copy of the string S with leading and trailing
        whitespace removed.
        If chars is given and not None, remove characters in chars instead.
        """
        return 
分割

     def split(self, sep=None, maxsplit=-1): # real signature unknown; restored from __doc__
        """
        以sep为分割，将S切分成列表，与partition的区别在于切分结果不包含sep，
        如果一个字符串中包含多个sep那么maxsplit为最多切分成几部分
        >>> a='a,b c\nd\te'
        >>> a.split()
        ['a,b', 'c', 'd', 'e']
        S.split(sep=None, maxsplit=-1) -> list of strings

        Return a list of the words in S, using sep as the
        delimiter string.  If maxsplit is given, at most maxsplit
        splits are done. If sep is not specified or is None, any
        whitespace string is a separator and empty strings are
        removed from the result.
        """
        return []

>>>






判断字符串中是否全为数字

        S.isdigit() -> bool
        
        Return True if all characters in S are digits
        and there is at least one character in S, False otherwise.
        """
        return False
       如果字符串的所有字符是数字返回True，至少有一个字符字符串则返回False。
      In [29]: user = '123'
      In [31]: user.isdigit()
      Out[31]: True


判断是否全为空格

        S.isspace() -> bool
        
        Return True if all characters in S are whitespace
        and there is at least one character in S, False otherwise.
        """		
    如果S中的所有字符都是空格，返回True S中至少有一个字符，否则是假的。 		
		
判断字符串是否以什么开头

        S.startswith(prefix[, start[, end]]) -> bool
        
        Return True if S starts with the specified prefix, False otherwise.
        With optional start, test S beginning at that position.
        With optional end, stop comparing S at that position.
        prefix can also be a tuple of strings to try.
        """
		
       In [32]: user ='xiangge'		
       In [33]: user.startswith('xiang')
       Out[33]: True	

判断字符串是否以什么结尾

        def endswith(self, suffix, start=None, end=None): # real signature unknown; restored from __doc__
        """
        S.endswith(suffix[, start[, end]]) -> bool

        Return True if S ends with the specified suffix, False otherwise.
        With optional start, test S beginning at that position.
        With optional end, stop comparing S at that position.
        suffix can also be a tuple of strings to try.
        """
        return False

取出字符索引

      def index(self, sub, start=None, end=None): # real signature unknown; restored from __doc__
        """
        S.index(sub[, start[, end]]) -> int

        Like S.find() but raise ValueError when the substring is not found.
        """
        return 0
 ----       
        
#### 列表介绍

定义：[]内以逗号分隔，按照索引，存放各种数据类型，每个位置代表一个元素
特性：
1.可存放多个值
2.可修改指定索引位置对应的值，可变
3.按照从左到右的顺序定义列表元素，下标从0开始顺序访问，有序

2.2.3.1 列表创建

list_test=[’lhf‘,12,'ok']
或
list_test=list('abc')
In [9]: list_test=list('abc')
In [10]: list_test
Out[10]: ['a', 'b', 'c']

或
list_test=list([’lhf‘,12,'ok'])

2.2.3.2 列表常用操作

索引
list[0]

追加
L.append(object)

L.insert(index, object)

删除
L.pop([index])   #不加参数默认删最后一个，pop(0)删第一个，写操作。

长度 len(list)

切片
list[1:3]
list[1:5:2]

循环


包含  in
'value' in list

其他常用：
L.index(value, [start, [stop]])

extend  和 append区别
L.extend(iterable)

remove  不存在报错，默认删掉第一个找到的。
L.remove(value)

sort（reverse=Trun)
L.sort(key=None, reverse=False)

----

#### 元组介绍

定义：与列表类似，只不过［］改成（）
特性：
1.可存放多个值

2.不可变

3.按照从左到右的顺序定义元组元素，下标从0开始顺序访问，有序

创建元组

ages = (11, 22, 33, 44, 55)
或
ages = tuple((11, 22, 33, 44, 55))

常见操作：

     class tuple(object):
    """
    tuple() -> empty tuple
    tuple(iterable) -> tuple initialized from iterable's items
    
    If the argument is a tuple, the return value is the same object.
    """
    def count(self, value): # real signature unknown; restored from __doc__
        """ T.count(value) -> integer -- return number of occurrences of value """
        return 0

    def index(self, value, start=None, stop=None): # real signature unknown; restored from __doc__
        """
        T.index(value, [start, [stop]]) -> integer -- return first index of value.
        Raises ValueError if the value is not present.
        """
        return 0
        
        
        
----
#### 字典介绍

定义：｛key1:value1,key2:value2｝,key-value结构，key必须可hash

特性：

1.可存放多个值

2.可修改指定key对应的值，可变

3.无序


字典创建

person = {"name": "sb", 'age': 18}
或
person = dict(name='sb', age=18)
person = dict({"name": "sb", 'age': 18})
person = dict((['name','sb'],['age',18]))
{}.fromkeys(seq,100) #不指定100默认为None
注意：
>>> dic={}.fromkeys(['k1','k2'],[])
>>> dic
{'k1': [], 'k2': []}
>>> dic['k1'].append(1)
>>> dic
{'k1': [1], 'k2': [1]} 


字典常用操作

        def clear(self): # real signature unknown; restored from __doc__
        """ 清除内容 """
        """ D.clear() -> None.  Remove all items from D. """
        pass
        
    def keys(self): # real signature unknown; restored from __doc__
        """ 所有的key列表 """
        """ D.keys() -> list of D's keys """
        return []

    def pop(self, k, d=None): # real signature unknown; restored from __doc__
        """ 获取并在字典中移除 """
        """
        D.pop(k[,d]) -> v, remove specified key and return the corresponding value.
        If key is not found, d is returned if given, otherwise KeyError is raised
        """
        pass

    def update(self, E=None, **F): # known special case of dict.update
        """ 更新
            {'name':'alex', 'age': 18000}
            [('name','sbsbsb'),]
        """
        """
        D.update([E, ]**F) -> None.  Update D from dict/iterable E and F.
        If E present and has a .keys() method, does:     for k in E: D[k] = E[k]
        If E present and lacks .keys() method, does:     for (k, v) in E: D[k] = v
        In either case, this is followed by: for k in F: D[k] = F[k]
        """
        pass

    def values(self): # real signature unknown; restored from __doc__
        """ 所有的值 """
        """ D.values() -> list of D's values """
        return []
        
----

#### 集合介绍

定义：由不同元素组成的集合，集合中是一组无序排列的可hash值，可以作为字典的key

特性：
集合的目的是将不同的值存放到一起，不同的集合间用来做关系运算，无需纠结于集合中单个值

    
集合创建

{1,2,3,1}
或
定义可变集合set
>>> set_test=set('hello')
>>> set_test
{'l', 'o', 'e', 'h'}

改为不可变集合frozenset
>>> f_set_test=frozenset(set_test)
>>> f_set_test
frozenset({'l', 'e', 'h', 'o'})

集合常见操作：

    def discard(self, *args, **kwargs): # real signature unknown
        """ 移除元素 """
        """
        Remove an element from a set if it is a member.
        
        If the element is not a member, do nothing.
        """
        pass

    def intersection(self, *args, **kwargs): # real signature unknown
        """ 取交集，新创建一个set """
        """
        Return the intersection of two or more sets as a new set.
        
        (i.e. elements that are common to all of the sets.)
        """
        pass

    def intersection_update(self, *args, **kwargs): # real signature unknown
        """ 取交集，修改原来set """
        """ Update a set with the intersection of itself and another. """
        pass

    def isdisjoint(self, *args, **kwargs): # real signature unknown
        """ 如果没有交集，返回true  """
        """ Return True if two sets have a null intersection. """
        pass

    def issubset(self, *args, **kwargs): # real signature unknown
        """ 是否是子集 """
        """ Report whether another set contains this set. """
        pass

    def issuperset(self, *args, **kwargs): # real signature unknown
        """ 是否是父集 """
        """ Report whether this set contains another set. """
        pass

    def pop(self, *args, **kwargs): # real signature unknown
        """ 移除 """
        """
        Remove and return an arbitrary set element.
        Raises KeyError if the set is empty.
        """
        pass

    def remove(self, *args, **kwargs): # real signature unknown
        """ 移除 """
        """
        Remove an element from a set; it must be a member.
        
        If the element is not a member, raise a KeyError.
        """
        pass

    def symmetric_difference(self, *args, **kwargs): # real signature unknown
        """ 差集，创建新对象"""
        """
        Return the symmetric difference of two sets as a new set.
        
        (i.e. all elements that are in exactly one of the sets.)
        """
        pass

    def symmetric_difference_update(self, *args, **kwargs): # real signature unknown
        """ 差集，改变原来 """
        """ Update a set with the symmetric difference of itself and another. """
        pass

    def union(self, *args, **kwargs): # real signature unknown
        """ 并集 """
        """
        Return the union of sets as a new set.
        
        (i.e. all elements that are in either set.)
        """
        pass

    def update(self, *args, **kwargs): # real signature unknown
        """ 更新 """
        """ Update a set with the union of itself and others. """
        pass

----

#### 文件类型介绍

一、打开文件

1
文件句柄 = file('文件路径', '模式')
注：python中打开文件有两种方式，即：open(...) 和  file(...) ，本质上前者在内部会调用后者来进行文件操作，推荐使用 open。

打开文件时，需要指定文件路径和以何等方式打开文件，打开后，即可获取该文件句柄，日后通过此文件句柄对该文件操作。

打开文件的模式有：

- r，只读模式（默认）。
- w，只写模式。【不可读；不存在则创建；存在则删除内容；】
- a，追加模式。【可读；   不存在则创建；存在则只追加内容；】
- "+" 表示可以同时读写某个文件

- r+，可读写文件。【可读；可写；可追加】
- w+，写读
- a+，同a

- "b"表示处理二进制文件（如：FTP发送上传ISO镜像文件，linux可忽略，windows处理二进制文件时需标注）

- rb
- wb
- ab

二、操作操作


    class file(object):
  
    def close(self): # real signature unknown; restored from __doc__
        关闭文件
        """
        close() -> None or (perhaps) an integer.  Close the file.
         
        Sets data attribute .closed to True.  A closed file cannot be used for
        further I/O operations.  close() may be called more than once without
        error.  Some kinds of file objects (for example, opened by popen())
        may return an exit status upon closing.
        """
 
    def fileno(self): # real signature unknown; restored from __doc__
        文件描述符  
         """
        fileno() -> integer "file descriptor".
         
        This is needed for lower-level file interfaces, such os.read().
        """
        return 0    
 
    def flush(self): # real signature unknown; restored from __doc__
        刷新文件内部缓冲区
        """ flush() -> None.  Flush the internal I/O buffer. """
        pass
 
 
    def isatty(self): # real signature unknown; restored from __doc__
        判断文件是否是同意tty设备
        """ isatty() -> true or false.  True if the file is connected to a tty device. """
        return False
 
 
    def next(self): # real signature unknown; restored from __doc__
        获取下一行数据，不存在，则报错
        """ x.next() -> the next value, or raise StopIteration """
        pass
 
    def read(self, size=None): # real signature unknown; restored from __doc__
        读取指定字节数据
        """
        read([size]) -> read at most size bytes, returned as a string.
         
        If the size argument is negative or omitted, read until EOF is reached.
        Notice that when in non-blocking mode, less data than what was requested
        may be returned, even if no size parameter was given.
        """
        pass
 
    def readinto(self): # real signature unknown; restored from __doc__
        读取到缓冲区，不要用，将被遗弃
        """ readinto() -> Undocumented.  Don't use this; it may go away. """
        pass
 
    def readline(self, size=None): # real signature unknown; restored from __doc__
        仅读取一行数据
        """
        readline([size]) -> next line from the file, as a string.
         
        Retain newline.  A non-negative size argument limits the maximum
        number of bytes to return (an incomplete line may be returned then).
        Return an empty string at EOF.
        """
        pass
 
    def readlines(self, size=None): # real signature unknown; restored from __doc__
        读取所有数据，并根据换行保存值列表
        """
        readlines([size]) -> list of strings, each a line from the file.
         
        Call readline() repeatedly and return a list of the lines so read.
        The optional size argument, if given, is an approximate bound on the
        total number of bytes in the lines returned.
        """
        return []
 
    def seek(self, offset, whence=None): # real signature unknown; restored from __doc__
        指定文件中指针位置
        """
        seek(offset[, whence]) -> None.  Move to new file position.
         
        Argument offset is a byte count.  Optional argument whence defaults to
        0 (offset from start of file, offset should be >= 0); other values are 1
        (move relative to current position, positive or negative), and 2 (move
        relative to end of file, usually negative, although many platforms allow
        seeking beyond the end of a file).  If the file is opened in text mode,
        only offsets returned by tell() are legal.  Use of other offsets causes
        undefined behavior.
        Note that not all file objects are seekable.
        """
        pass
        
        f.seek(偏移量,[起始位置])

        用来移动文件指针
        
        偏移量:单位:比特,可正可负
        
        起始位置:0-文件头,默认值;1-当前位置;2-文件尾

 
    def tell(self): # real signature unknown; restored from __doc__
        获取当前指针位置
        """ tell() -> current file position, an integer (may be a long integer). """
        pass
 
    def truncate(self, size=None): # real signature unknown; restored from __doc__
        截断数据，仅保留指定之前数据
        """
        truncate([size]) -> None.  Truncate the file to at most size bytes.
         
        Size defaults to the current file position, as returned by tell().
        """
        pass
 
    def write(self, p_str): # real signature unknown; restored from __doc__
        写内容
        """
        write(str) -> None.  Write string str to file.
         
        Note that due to buffering, flush() or close() may be needed before
        the file on disk reflects the data written.
        """
        pass
 
    def writelines(self, sequence_of_strings): # real signature unknown; restored from __doc__
        将一个字符串列表写入文件
        """
        writelines(sequence_of_strings) -> None.  Write the strings to the file.
         
        Note that newlines are not added.  The sequence can be any iterable object
        producing strings. This is equivalent to calling write() for each string.
        """
        pass
 
    def xreadlines(self): # real signature unknown; restored from __doc__
        可用于逐行读取文件，非全部
        """
        xreadlines() -> returns self.
         
        For backward compatibility. File objects now include the performance
        optimizations previously implemented in the xreadlines module.
        """
        pass
三、with

为了避免打开文件后忘记关闭，可以通过管理上下文，即：

    with open('log','r') as f:
     
    ...
    如此方式，当with代码块执行完毕时，内部会自动关闭并释放文件资源。