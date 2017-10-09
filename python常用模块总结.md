
## 常用模块介绍



模块本质就是一个.py文件。可以理解成是把一堆相关类型的函数写进一个py文件里面，直接拿出来使用就可以了
分为三部分：内置模块、第三方模块、自定义模块（模块调用、包）


-----
#### Time模块
在Python中，通常有这三种方式来表示时间：时间戳、元组(struct_time)、格式化的时间字符串。

(1)时间戳(timestamp) ：通常来说，时间戳表示的是从1970年1月1日00:00:00开始按秒计算的偏移量。我们运行“type(time.time())”，返回的是float类型。

(2)格式化的时间字符串(Format String)： ‘1988-03-16’

(3)结构化时间元组(struct_time) ：struct_time元组共有9个元素共九个元素:(年，月，日，时，分，秒，一年中第几周，一年中第几天等）

 <1>时间戳

    import time
    In [16]: time.time()  #返回当前时间的时间戳（给计算机看 ），从Unix元年到现在经过的秒
    Out[16]: 1498030482.9540176
    
    In [17]: c = time.time()
    
    In [18]: c/3600/24/365
    Out[18]: 47.502235409268984

 <2>格式化时间字符串

    time.strftime("%Y-%m-%d %X")
    '2017-04-26 00:32:18'


<3> 结构化时间元组

    time.localtime()
    time.struct_time(tm_year=2017, tm_mon=4, tm_mday=26,
                     tm_hour=0, tm_min=32, tm_sec=42, tm_wday=2,
                     tm_yday=116, tm_isdst=0)
    
    In [12]: c = time.localtime(）
    In [13]: c.tm_year
    Out[13]: 2017

**小结：时间戳是计算机能够识别的时间；时间字符串是人能够看懂的时间；元组则是用来操作时间的**


##### 几种时间形式的转换：

**1.时间戳------》结构化时间：  localtime/gmtime**

    In [19]: time.localtime()  #不给参数默认当前时间戳
    Out[19]: time.struct_time(tm_year=2017, tm_mon=6, tm_mday=21, tm_hour=15, tm_min=45, tm_sec=44, tm_wday=2, tm_yday=172, tm_isdst=0)
    
    In [20]: time.gmtime()     #不给参数默认当前时间戳   
    Out[20]: time.struct_time(tm_year=2017, tm_mon=6, tm_mday=21, tm_hour=7, tm_min=45, tm_sec=56, tm_wday=2, tm_yday=172, tm_isdst=0)
    
**备注：gmtime是时间是标准时间UTC。**

**2.结构化时间-----》时间戳：mktime**

    In [21]: time.mktime()    #不给参数就报错
    TypeError                                 Traceback (most recent call last)
    <ipython-input-21-68ccb7b7a629> in <module>()
    ----> 1 time.mktime()
    
    TypeError: mktime() takes exactly one argument (0 given)
    
    In [22]: time.mktime(time.localtime())
    Out[22]: 1498031424.0
3.**结构化时间：－－－－》字符串时间： strftime**

    In [24]: time.strftime("%Y-%m-%d %X", time.localtime())
    Out[24]: '2017-06-21 15:56:14'
    
    In [25]: time.strftime('%Y-%m-%d',time.localtime(time.time()-365*24*3600))
    Out[25]: '2016-06-21'


**4.字符串时间-----》结构化时间  strptime**

    In [29]: time.strptime("2017-03-16","%Y-%m-%d")
    Out[29]: time.struct_time(tm_year=2017, tm_mon=3, tm_mday=16, tm_hour=0, tm_min=0, tm_sec=0, tm_wday=3, tm_yday=75, tm_isdst=-1)
    In [31]: time.strptime("2017-06-21 16:05:45","%Y-%m-%d %X")
    Out[31]: time.struct_time(tm_year=2017, tm_mon=6, tm_mday=21, tm_hour=16, tm_min=5, tm_sec=45, tm_wday=2, tm_yday=172, tm_isdst=-1)


##### 其余两种直接转换成字符串时间格式

**1.时间戳------》字符串时间格式**

    In [32]: time.ctime()   #不给参数默认为当前时间戳  等同于 time.ctime(time.time（）)
    Out[32]: 'Wed Jun 21 16:10:57 2017'
    In [33]: time.ctime(2315554656)
    Out[33]: 'Mon May 18 17:37:36 2043'
    
**2.结构化时间------》字符串时间格式**

    In [34]: time.asctime()   #不给参数默认为当前结构化时间  等同于time.asctime(time.localtime())
    Out[34]: 'Wed Jun 21 16:16:11 2017'
 
##### 其他方法
**sleep(secs)  #相当于一个IO，不占用CPU，线程推迟指定的时间运行，单位为秒。**

----

### random模块


    >>> import random
    >>> random.random()      # 大于0且小于1之间的小数，float类型
    0.7664338663654585
    
    >>> random.randint(1,5)  # 大于等于1且小于等于5之间的整数
    2
    
    >>> random.randrange(1,3) # 大于等于1且小于3之间的整数，顾头不顾尾
    1
    
    >>> random.choice([1,'23',[4,5]])  # 1或者23或者[4,5]，随机一次取列表中任意一个元素。
    1
    
    >>> random.sample([1,'23',[4,5]],2)  #列表元素任意2个组合成列表显
    [[4, 5], '23']
    
    >>> random.uniform(1,3) #随机取一个大于1小于3的小数
    1.6270147180533838
    
    >>> item=[1,3,5,7,9]
    >>> random.shuffle(item) # 打乱次序
    >>> item
    [5, 1, 3, 7, 9]
    >>> random.shuffle(item)
    >>> item
    [5, 9, 7, 1, 3]
    import random

例子：随机生成一个包含数字，大小写字母的五位随机数：

    def vadate_code():
        ret = ''
        for i in range(5):
            num =random.randint(0,9)
            alfa = chr(random.randint(97,122))
            alfa2 = chr(random.randint(65,90))
            s = random.choice([str(num),alfa,alfa2])
            ret = ret + s
        return ret
    
    print(vadate_code())

**注意一点：写py文件时一定不要跟我们模块重名，一旦重名就会导致模块无法使用！！！**

-----
#### hashlib 模块

3.1 算法介绍

Python的hashlib提供了常见的摘要算法，如MD5，SHA1等等。
什么是摘要算法呢？摘要算法又称哈希算法、散列算法。它通过一个函数，把任意长度的数据转换为一个长度固定的数据串（通常用16进制的字符串表示）。
摘要算法就是通过摘要函数f()对任意长度的数据data计算出固定长度的摘要digest，目的是为了发现原始数据是否被人篡改过。
摘要算法之所以能指出数据是否被篡改过，就是因为摘要函数是一个单向函数，计算f(data)很容易，但通过digest反推data却非常困难。而且，对原始数据做一个bit的修改，都会导致计算出的摘要完全不同。

我们以常见的摘要算法MD5为例，计算出一个字符串的MD5值：

     md5(string=b'')
        Return a new MD5 hash object; optionally initialized with a string.
    In [37]: import hashlib
    In [39]: m = hashlib.md5()
    In [41]: print(m)   #返回的是一个hash对象
    <_md5.md5 object at 0x7fc266746030>
    
    In [49]:  m1 = hashlib.md5(b'hello')
    In [50]: m1
    Out[50]: <_md5.md5 at 0x7fc2667069d0>
    In [51]: m1.hexdigest()
    Out[51]: '5d41402abc4b2a76b9719d911017c592'
    
    
    In [52]:  m = hashlib.md5()
    In [54]: m.update(b'hello')  #update相当于更新
    In [56]: m.hexdigest()
    Out[56]: '5d41402abc4b2a76b9719d911017c592'
    In [57]: m.update(b'hello')  #这次是在上次的基础上更新相当于b’hellohello‘,所以两次生成的结果是不相同的
    In [58]: m.hexdigest()
    Out[58]: '23b431acfeb41e15d466d75de822307c'
    In [59]: n = hashlib.md5()
    In [60]: n.update(b'hellohello')  #这个跟上面update两次hello的结果是相同的
    In [61]: n.hexdigest()
    Out[61]: '23b431acfeb41e15d466d75de822307c'

**其余算法**

m = hashlib.sha1()   #只要把我们上面md5换成sha1就可以了，其余的跟上面一样。

**摘要算法应用：**

任何允许用户登录的网站都会存储用户登录的用户名和口令。如何存储用户名和口令呢？方法是存到数据库表中：

name    | password

--------+----------

michael | 123456

bob            | abc999

alice   | alice2008


如果以明文保存用户口令，如果数据库泄露，所有用户的口令就落入黑客的手里。此外，网站运维人员是可以访问数据库的，也就是能获取到所有用户的口令。正确的保存口令的方式是不存储用户的明文口令，而是存储用户口令的摘要，比如MD5：


username | password

---------+---------------------------------

michael  | e10adc3949ba59abbe56e057f20f883e

bob      | 878ef96e86145580c38c87f0410ad153

alice    | 99b1c2188db85afee403b1536010c2c9

考虑这么个情况，很多用户喜欢用123456，888888，password这些简单的口令，于是，黑客可以事先计算出这些常用口令的MD5值，得到一个反推表：

'e10adc3949ba59abbe56e057f20f883e': '123456'

'21218cca77804d2ba1922c33e0151105': '888888'


'5f4dcc3b5aa765d61d8327deb882cf99': 'password'

这样，无需破解，只需要对比数据库的MD5，黑客就获得了使用常用口令的用户账号。
对于用户来讲，当然不要使用过于简单的口令。但是，我们能否在程序设计上对简单口令加强保护呢？
由于常用口令的MD5值很容易被计算出来，所以，要确保存储的用户口令不是那些已经被计算出来的常用口令的MD5，这一方法通过对原始口令加一个复杂字符串来实现，俗称“加盐”：

hashlib.md5("salt".encode("utf8"))

经过Salt处理的MD5口令，只要Salt不被黑客知道，即使用户输入简单口令，也很难通过MD5反推明文口令。
但是如果有两个用户都使用了相同的简单口令比如123456，在数据库中，将存储两条相同的MD5值，这说明这两个用户的口令是一样的。有没有办法让使用相同口令的用户存储不同的MD5呢？
如果假定用户无法修改登录名，就可以通过把登录名作为Salt的一部分来计算MD5，从而实现相同口令的用户也存储不同的MD5。
摘要算法在很多地方都有广泛的应用。要注意摘要算法不是加密算法，不能用于加密（因为无法通过摘要反推明文），只能用于防篡改，但是它的单向计算特性决定了可以在不存储明文口令的情况下验证用户口令。
------

#### OS模块：跟文件系统打交道接口，跨系统的API.   

**常用：**

os.getcwd() 获取当前工作目录，即当前python脚本工作的目录路径   相当于linux pwd

    In [4]: os.getcwd()
    Out[4]: '/root'
os.chdir("dirname")  改变当前脚本工作目录；相当于shell下cd

os.makedirs('dirname1/dirname2')    可生成多层递归目录， 相当于shell中mkdir  -p dirname

os.removedirs('dirname1')    若目录为空，则删除，并递归到上一级目录，如若也为空，则删除，依此类推

os.mkdir('dirname')    生成单级目录；相当于shell中mkdir dirname

os.rmdir('dirname')    删除单级空目录，若目录不为空则无法删除，报错；相当于shell中rmdir dirname

os.listdir('dirname')    列出指定目录下的所有文件和子目录，包括隐藏文件，并以列表方式打印

os.remove()  删除一个文件

os.rename("oldname","newname")  重命名文件/目录

os.stat('path/filename')  获取文件/目录信息

    In [5]: os.stat('aaa')
    Out[5]: os.stat_result(st_mode=33188, st_ino=136945, st_dev=2051, st_nlink=1, st_uid=0, st_gid=0, st_size=0, st_atime=1494057367, st_mtime=1494057367, st_ctime=1494057367)

os.path.abspath(path)  返回path规范化的绝对路径

os.path.dirname(path)  返回path的目录。其实就是os.path.split(path)的第一个元素

os.path.basename(path)  返回path最后的文件名。如何path以／或\结尾，那么就会返回空值。即

os.path.exists(path)  如果path存在，返回True；如果path不存在，返回False

os.path.join(path1[, path2[, ...]])  将多个路径组合后返回，第一个绝对路径之前的参数将被忽略

os.path.getatime(path)  返回path所指向的文件或者目录的最后存取时间

os.path.getmtime(path)  返回path所指向的文件或者目录的最后修改时间

os.path.getsize(path) 返回path的大小

os.symlink = symlink(src, dst, target_is_directory=False, *, dir_fd=None) 创建链接文件

    os.symlink('test2.txt','test.syslink')
utime() 更新文件时间戳

tmpfile() 创建并打开（w+b）一个新的临时文件

os.walk() 目录树生成器，相当于shell的tree命令。




**不常用：**

os.chroot():设定当前进程的根目录

os.curdir  返回当前目录: ('.')

os.pardir  获取当前目录的父目录字符串名：('..')

os.sep    输出操作系统特定的路径分隔符，win下为"\\",Linux下为"/"

os.linesep    输出当前平台使用的行终止符，win下为"\t\n",Linux下为"\n"

os.pathsep    输出用于分割文件路径的字符串 win下为;,Linux下为:

os.name    输出字符串指示当前使用平台。win->'nt'; Linux->'posix'

os.system("bash command")  运行shell命令，直接显示


mkfifo()    创建命名管道

mknod 创建设备文件

unlink 删除链接文件

os.environ  获取系统环境变量

os.path.split(path)  将path分割成目录和文件名二元组返回

os.path.splitext(path) 返回（filename,extension）元组

os.path.isabs(path)  如果path是绝对路径，返回True

os.path.isfile(path)  如果path是一个存在的文件，返回True。否则返回False

os.path.isdir(path)  如果path是一个存在的目录，则返回True。否则返回False

os.path.islink(path)  如果path是一个存在的链接文件，则返回True。否则返回False

os.path.ismount(path)  如果path是一个挂载点，则返回True。否则返回False

os.access('test2.txt',0) 判定某用户对文件是否有访问权限，返回布尔值。 

os.chmod() 修改权限

os.chown() 修改属主属组

umask() 设置默认权限模式


------

#### sys模块：跟python解释器打交道的

sys.argv           命令行参数List，第一个元素是程序本身路径

sys.exit(n)        退出程序，正常退出时exit(0)

sys.version        获取Python解释程序的版本信息

sys.maxint         最大的Int值  python没有这个

sys.path           返回模块的搜索路径，初始化时使用PYTHONPATH环境变量的值

sys.platform       返回操作系统平台名称

----

#### logging模块

函数式简单配置

    import logging  
    logging.debug('debug message')  
    logging.info('info message')  
    logging.warning('warning message')  
    logging.error('error message')  
    logging.critical('critical message') 

默认情况下Python的logging模块将日志打印到了标准输出中，且只显示了大于等于WARNING级别的日志，这说明默认的日志级别设置为WARNING（日志级别等级CRITICAL > ERROR > WARNING > INFO > DEBUG），默认的日志格式为日志级别：Logger名称：用户输出消息

**灵活配置日志级别，日志格式，输出位置:**

    import logging  
    
    logging.basicConfig(level=logging.DEBUG,  
                        format='%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s',  
                        datefmt='%a, %d %b %Y %H:%M:%S',   改变默认输出格式
                        filename='/tmp/test.log',  #输出到文件，不在在屏幕输出。
                        filemode='w')   #写文件模式，大部分是a追加模式写
      
    logging.debug('debug message')  
    logging.info('info message')  
    logging.warning('warning message')  
    logging.error('error message')  
    logging.critical('critical message')
  
    
**配置参数：**

    logging.basicConfig()函数中可通过具体参数来更改logging模块默认行为，可用参数有
    filename：用指定的文件名创建FiledHandler，这样日志会被存储在指定的文件中。
    filemode：文件打开方式，在指定了filename时使用这个参数，默认值为“a”还可指定为“w”。
    format：指定handler使用的日志显示格式。
    datefmt：指定日期时间格式。
    level：设置rootlogger（后边会讲解具体概念）的日志级别
    stream：用指定的stream创建StreamHandler。可以指定输出到sys.stderr,sys.stdout或者文件(f=open(‘test.log’,’w’))，默认为sys.stderr。若同时列出了filename和stream两个参数，则stream参数会被忽略。


**format参数中可能用到的格式化串：**

    %(name)s Logger的名字
    %(levelno)s 数字形式的日志级别
    %(levelname)s 文本形式的日志级别
    %(pathname)s 调用日志输出函数的模块的完整路径名，可能没有
    %(filename)s 调用日志输出函数的模块的文件名
    %(module)s 调用日志输出函数的模块名
    %(funcName)s 调用日志输出函数的函数名
    %(lineno)d 调用日志输出函数的语句所在的代码行
    %(created)f 当前时间，用UNIX标准的表示时间的浮 点数表示
    %(relativeCreated)d 输出日志信息时的，自Logger创建以 来的毫秒数
    %(asctime)s 字符串形式的当前时间。默认格式是 “2003-07-08 16:49:45,896”。逗号后面的是毫秒
    %(thread)d 线程ID。可能没有
    %(threadName)s 线程名。可能没有
    %(process)d 进程ID。可能没有
    %(message)s用户输出的消息   


**logger对象配置**

    import logging

    logger = logging.getLogger()    #创建一个对象，对象就一定有对应的方法
    
    fh = logging.FileHandler('test.log') # 创建一个handler，用于写入日志文件
    
    ch = logging.StreamHandler() # 再创建一个handler，用于输出到控制台
    
    formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
    
    fh.setFormatter(formatter)
    
    ch.setFormatter(formatter)
    
    logger.addHandler(fh) #logger对象可以添加多个fh和ch对象
    
    logger.addHandler(ch)
    
    logger.debug('logger debug message')
    logger.info('logger info message')
    logger.warning('logger warning message')
    logger.error('logger error message')
    logger.critical('logger critical message')
logging库提供了多个组件：Logger、Handler、Filter、Formatter。Logger对象提供应用程序可直接使用的接口，Handler发送日志到适当的目的地，Filter提供了过滤日志信息的方法，Formatter指定日志显示格式。另外，可以通过：logger.setLevel(logging.Debug)设置级别。



------


#### 序列化模块
之前我们学习过用eval内置方法可以将一个字符串转成python对象，不过，eval方法是有局限性的，对于普通的数据类型，json.loads和eval都能用，但遇到特殊类型的时候，eval就不管用了,所以eval的重点还是通常用来执行一个字符串表达式，并返回表达式的值。

转换类型

    d={"name":"yuan"}
    
    s=str(d)
    
    print(type(s))
    
    d2=eval(s)
    
    print(d2[1])
    
    with open("test") as f:
    
        for i in f :
    
            if type(eval(i.strip()))==dict:
                print(eval(i.strip())[1])
                
计算

print(eval("12*7+5-3"))

什么是序列化？

我们把对象(变量)从内存中变成可存储或传输的过程称之为序列化，在Python中叫pickling，在其他语言中也被称之为serialization，marshalling，flattening等等，都是一个意思。序列化之后，就可以把序列化后的内容写入磁盘，或者通过网络传输到别的机器上。反过来，把变量内容从序列化的对象重新读到内存里称之为反序列化，即unpickling。

**json模块**

如果我们要在不同的编程语言之间传递对象，就必须把对象序列化为标准格式，比如XML，但更好的方法是序列化为JSON，因为JSON表示出来就是一个字符串，可以被所有语言读取，也可以方便地存储到磁盘或者通过网络传输。JSON不仅是标准格式，并且比XML更快，而且可以直接在Web页面中读取，非常方便。
JSON表示的对象就是标准的JavaScript语言的对象一个子集，JSON和Python内置的数据类型对应如下：
 

    import json
    i=10
    s='hello'
    t=(1,4,6)
    l=[3,5,7]
    d={'name':"yuan"}
    
    json_str1=json.dumps(i)
    json_str2=json.dumps(s)
    json_str3=json.dumps(t)
    json_str4=json.dumps(l)
    json_str5=json.dumps(d)

    print(json_str1)   #'10'
    print(json_str2)   #'"hello"'
    print(json_str3)   #'[1, 4, 6]'  #元组在json里面存的形式是跟列表存的类似的。
    print(json_str4)   #'[3, 5, 7]'
    print(json_str5)   #'{"name": "yuan"}'

**python在文本中的使用：**

**#----------------------------序列化**

第一写法：

    import json
    
    dic={'name':'alvin','age':23,'sex':'male'}
    f=open('a.txt','w')
    data=json.dumps(dic)
    f.write(data)  
    f.close()
第二种写法：
    
    import json
    
    dic={'name':'alvin','age':23,'sex':'male'}
    f=open('a.txt','w')
    json.dump(dic,f)
    f.close()

**#-----------------------------反序列化**

    import json
    
    f=open('序列化对象')
    new_data=json.loads(f.read())#  等价于data=json.load(f)
    
    print(type(new_data))

-----
**pickle模块**

**##----------------------------序列化**

    import pickle
     
    dic={'name':'alvin','age':23,'sex':'male'}
     
    print(type(dic))   #<class 'dict'>
     
    j=pickle.dumps(dic)
    print(type(j))    #<class 'bytes'>
     
     
    f=open('序列化对象_pickle','wb')    #注意是w是写入str,wb是写入bytes,j是'bytes'
    f.write(j)  #-------------------等价于pickle.dump(dic,f)  推荐使用这种
     
    f.close()
    
    
**#-------------------------反序列化**

    import pickle
    f=open('序列化对象_pickle','rb')
     
    data=pickle.loads(f.read())#  等价于data=pickle.load(f)
     
    print(data['age'])    

----
#### shelve模块

shelve模块比pickle模块简单，只有一个open函数，返回类似字典的对象，可读可写;key必须为字符串，而值可以是python所支持的数据类型


    import shelve
      
    f = shelve.open(r'shelve.txt')
      
    f['stu1_info']={'name':'alex','age':'18'}
     
    f['stu2_info']={'name':'alvin','age':'20'}
    f['school_info']={'website':'oldboyedu.com','city':'beijing'}
    f.close()
    print(f.get('stu_info')['age'])
        



----

#### re模块

就其本质而言，正则表达式（或 RE）是一种小型的、高度专业化的编程语言，（在Python中）它内嵌在Python中，并通过 re 模块实现。正则表达式模式被编译成一系列的字节码，然后由用 C 编写的匹配引擎执行。

类似shell扩展正则表达式：

元字符：
-  \. 通配 任意单个字符，除\n不能匹配。最后加re.S就是使.通配任意字符，包括\n.

        In [1]: s = 'aaass1234\n112klljl'
    
        In [2]: import re
        
        In [3]: re.findall("ss.*k",s)
        Out[3]: []
        
        In [4]: re.findall("ss.*k",s,re.S)
        Out[4]: ['ss1234\n112k']



- [...]任意单个字符  # 在字符集里有功能的符号: - ^ \


    In [18]: re.findall(r"a[\d]c","asda2c1231asd31121as") #\d在[]中也可以使用。
    Out[18]: ['a2c']

- [^....]不在范围内任意单个字符 


次数匹配：

- \*   任意次
- \+ 【1，+00】
- \？【0,1】
- {}   {n,m}
- {m}  m次
- {0，n } 最多n次
- {m,}  最少m次

锚定：
- ^ 行首
- $ 行尾
- \b 词首，词尾，匹配一个特殊字符边界，比如空格 ，&，＃等

分组：
- (...) 


    In [5]: re.findall('(123)+','asd123adsa123123123asd')
    Out[5]: ['123', '123']  #findall分组中优先级高显示
    
    In [6]: re.findall('(?:123)+','asd123adsa123123123asd')
    Out[6]: ['123', '123123123']  #？：在分组中可以去掉分组的优先级

- (？P<xx>...)：命名分组


    In [8]: ret = re.search(r"-blog-aticles-(?P<year>20[01]\d)-(?P<month>\d+)","-blog-aticles-2005-12")

    In [9]: ret.group("year")
    Out[9]: '2005'
    
    In [10]: ret.group("month")
    Out[10]: '12'

转义符号 \ ,加r原生转义，所以使用转义符时尽量使用r

1、反斜杠后边跟元字符去除特殊功能,比如\.

2、反斜杠后边跟普通字符实现特殊功能,比如\d
- \d  匹配任何十进制数；它相当于类 [0-9]。
- \D 匹配任何非数字字符；它相当于类 [^0-9]。
- \s  匹配任何空白字符；它相当于类 [ \t\n\r\f\v]。
- \S 匹配任何非空白字符；它相当于类 [^ \t\n\r\f\v]。
- \w 匹配任何字母数字字符；它相当于类 [a-zA-Z0-9_]。
- \W 匹配任何非字母数字字符；它相当于类 [^a-zA-Z0-9_]
- \nn：后项引用


|或者：path1 | path

贪婪匹配：在满足匹配时，匹配尽可能长的字符串，默认情况下，采用贪婪匹配

    In [34]: re.findall("abc{2,5}","abcccccasd")
    Out[34]: ['abccccc']


非贪婪匹配：在满足匹配时，匹配尽可能短的字符串，在次数匹配后加？

    In [35]: re.findall("abc{2,5}?","abcccccasd")
    Out[35]: ['abcc']


*? 重复任意次，但尽可能少重复

+? 重复1次或更多次，但尽可能少重复

?? 重复0次或1次，但尽可能少重复

{n,m}? 重复n到m次，但尽可能少重复

{n,}? 重复n次以上，但尽可能少重复


    .*?的用法：
    . 是任意字符
    * 是取 0 至 无限长度
    ? 是非贪婪模式。
    何在一起就是 取尽量少的任意字符，一般不会这么单独写，他大多用在：
    .*?x
    
    就是取前面任意长度的字符，直到一个x出现
    
非贪婪匹配一个小例子：

     In [36]: s = "<div>zeng<img></div><a href=""></div>"

    In [37]: re.findall("<div>.*?</div>",s)
    Out[37]: ['<div>zeng<img></div>']
    
    
**re模块的常用方法：**

findall(): # 返回所有满足匹配条件的结果,放在列表里

    re.findall('a','alvin yuan')    

search():只到找到第一个匹配然后返回一个包含匹配信息的对象,通过调用group()方法得到匹配的字符串,如果字符串没有匹配，则返回None。

    In [20]:  re.search('a','alvin yuan').group()  
    Out[20]: 'a'
  

match(): #同search,不过是从字符串开始处进行匹配 ,相当于行首锚定匹配            

    In [23]:  re.match('a','bbabc') #没匹配到不返回结果

    In [24]:  re.match('a','abc')
    Out[24]: <_sre.SRE_Match object; span=(0, 1), match='a'>
    
    In [25]:  re.match('a','abc').group()
    Out[25]: 'a'

split(): #分割,以列表返回分隔结果

    In [26]: re.split("\d+","dff12hjsg1jkhsd145jhasdj")
    Out[26]: ['dff', 'hjsg', 'jkhsd', 'jhasdj']

    
    In [27]: re.split("\d+","dff12hjsg1jkhsd145jhasdj",2) #最多分隔2次
    Out[27]: ['dff', 'hjsg', 'jkhsd145jhasdj']
    
    In [38]: re.split("(\d+)","dff12hjsg1jkhsd145jhasdj") #模式括号括起来也可以把分隔符一起拿到。
    Out[38]: ['dff', '12', 'hjsg', '1', 'jkhsd', '145', 'jhasdj']


sub():替换

    In [28]: re.sub("\d+","xxx","kdfjkj2132js1jkh112")
    Out[28]: 'kdfjkjxxxjsxxxjkhxxx'

    In [29]: re.sub("\d+","xxx","kdfjkj2132js1jkh112",1) #最后1代表我们需要替换几次
    Out[29]: 'kdfjkjxxxjs1jkh112'
    
补充：字符串的替换使用replace

subn():替换并把替换的次数返回给我们

    In [30]: re.subn("\d+","xxx","kdfjkj2132js1jkh112")
    Out[30]: ('kdfjkjxxxjsxxxjkhxxx', 3)

    In [31]: re.subn("\d+","xxx","kdfjkj2132js1jkh112",2)
    Out[31]: ('kdfjkjxxxjsxxxjkh112', 2)


compile():编译,好处是如果匹配多次相同模式，我们编译一次，后续直接调用该编译模式就可以使用，不用每次重复去写模式。

    In [32]: c = re.compile("\d+")
    In [33]: c.findall("jashd11jkasjhd45jkd12")
    Out[33]: ['11', '45', '12']


finditer(): #返回的是一个迭代器对象

    In [39]: ret = re.finditer("\d+","asds123shd145shghd1jshdj45hjshg778jksj225jhsdhh445jskhd5")

    In [40]: type(ret)
    Out[40]: builtins.callable_iterator
    
    In [41]: next(ret)
    Out[41]: <_sre.SRE_Match object; span=(4, 7), match='123'>
    
    In [42]: next(ret).group()
    Out[42]: '145'
    
    In [43]: next(ret).group()
    Out[43]: '1'
    
    In [44]: next(ret).group()
    Out[44]: '45'

正则匹配几个小练习：

    1、 匹配一段文本中的每行的邮箱

    import re
    res = re.findall(r"\w+\@\w{2,3}\.com","asdfg,aas1233@qq.com,hjghgjj,4444,jhgjgs1233@163.com,1112")
    print(res)


2、 匹配一段文本中的每行的时间字符串，比如：‘1990-07-12’；

    import re
    res = re.findall(r"(?:1[0-9]{3}|20[10][1-9])-(?:0?[1-9]|1[0-2])-(?:0?[1-9]|[1,2][0-9]|3[01])","asdd,1990-07-12,aaasd1992-05-05asasdd,aaasddf")
    print(res)
   



3、 匹配一段文本中所有的身份证数字。

    import re
    res = re.findall("\d{17}[0-9X]","ksdjkljlk421182199005046552lkfllkdk,slkklkliofjoifa")
    print(res)


4、 匹配qq号。(腾讯QQ号从10000开始)  

    import re
    res = re.findall("[1-9][0-9]{4,}","10000,12255546,140000222,854905819")
    print(res)




5、 匹配一个浮点数。 

    import re
    res = re.findall(r"-?[0-9]+\.[0-9]+","11224,5588,5.223,412.235,1025,0.125,-12.12")
    print(res)
    


6、 匹配汉字。 

    import re
    res = re.findall(r"[\u4e00-\u9fa5]+","钢蛋，122,xxx，曾")
    print(res)



7、 匹配出所有整数

    import re
    res = re.findall(r"-?[1-9][0-9]*","11224,-5588,dddfff,klkjlkj")
    print(res)

使用正则爬豆瓣电影

    import requests
    import re
    def init(func):
        def wrapper(*args,**kwargs):
            res = func(*args,**kwargs)
            next(res)
            return res
        return wrapper
    
    def getPage(target):
        count = 0
        for i in range(10):
    
            respase_str = requests.get("https://movie.douban.com/top250?start=%d&filter="%count)
            # print(respase_str.text)
            count +=25
            target.send(respase_str.text)
    @init
    def run():
        l2 = [ ]
        while True:
            resonse = yield
            # print(resonse)
            obj = re.compile('<div class="item">.*?<em.*?>(\d+)</em>.*?<span class="title">(.*?)</span>'\
                             '.*?<p.*?>.*?(导演:.*?)&nbsp.*?<span class="rating_num".*?>(.*?)</span>'\
                             '.*?<span>(.*?)</span>',re.S)
            ret = obj.findall(resonse)
            # print(ret)
            l1 = [ ]
            for i in ret:
    
                dic1 = dict(zip(('ID','片名','导演','评分','评论数'),i))
                l1.append(dic1)
            for i in l1:
                date = str(i)+'\n'
                with open('dianying.txt','a',encoding='utf8') as f:
                    f.write(date)
    
    getPage(run())


使用正则实现计算器功能：

    # 实现能计算类似
    # 1 - 2 * ( (60-30 +(-40/5) * (9-2*5/3 + 7 /3*99/4*2998 +10 * 568/14 )) - (-4*3)/ (16-3*2) )等类似公式的计算器程序
    
    import re
    
    s = '1 - 2 * ( (60-30 +(-40/5) * (9-2*5/3 + 7 /3*99/4*2998 +10 * 568/14 )) - (-4*3)/ (16-3*2) )'
    
    def fun2(res):    #计算括号里面匹配出来的式子
        res = res.strip('()')
        res = res.replace(' ','')
        find1 = re.search("[*/]",res)
    
        if find1:
            find2 = re.search(r"(?P<a>-?\d+\.?\d*)[*/](?P<b>-?\d+\.?\d*)", res)
            # print(find2.group())
            if find1.group() == '/':
                res2 = float(find2.group("a"))/float(find2.group("b"))
                res = res.replace(find2.group(),str(res2))
                # print(res)
                return fun2(res)
            if find1.group() == '*':
                res2 = float(find2.group("a")) * float(find2.group("b"))
                res = res.replace(find2.group(),str(res2))
                return fun2(res)
    
        find3 = re.search("[+\-]",res)
        if find3:
            find4 = re.search(r"(?P<a>-?\d+\.?\d*)(?P<c>[+\-])(?P<b>-?\d+\.?\d*)", res)
            if find4:  # 如果找到不是一个表达式不执行
                if find4.group("c") == '+':
                    res4 = float(find4.group("a")) + float(find4.group("b"))
                    res = res.replace(find4.group(),str(res4))
                    return fun2(res)
                if find4.group("c") == '-':
                    res4 = float(find4.group("a")) - float(find4.group("b"))
                    res = res.replace(find4.group(),str(res4))
                    return fun2(res)
        return res
    
    def fun1(s):
        s = s.replace(' ','')
        if '(' in s or ')' in s:   #判断式子是否有括号
            res = re.search(r"\([^()]+\)", s).group()
            res2 = fun2(res)
            s = s.replace(res,res2)
            # print(s)
            return fun1(s)
        else:
            res3 = fun2(s)
            return res3
    
    print(fun1(s))

-----
#### subprocess模块
   当我们需要调用系统的命令的时候，最先考虑的os模块。用os.system()和os.popen()来进行操作。但是这两个命令过于简单，不能完成一些复杂的操作，如给运行的命令提供输入或者读取命令的输出，判断该命令的运行状态，管理多个命令的并行等等。这时subprocess中的Popen命令就能有效的完成我们需要的操作。 
 




\#win下

    import subprocess
    s = subprocess.Popen('dir',shell=True,stdout=subprocess.PIPE)
    print(s.stdout.read().decode('gbk'))

\#linux下

    import subprocess
    s = subprocess.Popen('ls')
    s = subprocess.Popen('ls -l',shell=True)
    s = subprocess.Popen(['ls','-l'])


备注：s.wait()  执行完子进程再去执行父进程后面的程序。
   
常用subprocess方法示例

#执行命令，返回命令执行状态 ， 0 or 非0

    >>> retcode = subprocess.call(["ls", "-l"])

#执行命令，如果命令结果为0，就正常返回，否则抛异常

    >>> subprocess.check_call(["ls", "-l"])
    0

#接收字符串格式命令，返回元组形式，第1个元素是执行状态，第2个是命令结果 

    >>> subprocess.getstatusoutput('ls /bin/ls')
    (0, '/bin/ls')

#接收字符串格式命令，并返回结果

    >>> subprocess.getoutput('ls /bin/ls')
    '/bin/ls'

#执行命令，并返回结果，注意是返回结果，不是打印，下例结果返回给res

    >>> res=subprocess.check_output(['ls','-l'])
    >>> res
    b'total 0\ndrwxr-xr-x 12 alex staff 408 Nov 2 11:05 OldBoyCRM\n'

#上面那些方法，底层都是封装的subprocess.Popen

    poll()
    Check if child process has terminated. Returns returncode
    
    wait()
    Wait for child process to terminate. Returns returncode attribute.
    
    
    terminate() 杀掉所启动进程
    communicate() 等待任务结束
    
    stdin 标准输入
    
    stdout 标准输出
    
    stderr 标准错误
    
    pid
    The process ID of the child process.

#例子

    >>> p = subprocess.Popen("df -h|grep disk",stdin=subprocess.PIPE,stdout=subprocess.PIPE,shell=True)
    >>> p.stdout.read()
    b'/dev/disk1 465Gi 64Gi 400Gi 14% 16901472 104938142 14% /\n'   
       
    
----
#### configparser模块
该模块适用于配置文件的格式与windows ini文件类似，可以包含一个或多个节（section），每个节可以有多个参数（键=值）。

来看一个好多软件的常见文档格式如下：


    [DEFAULT]
    ServerAliveInterval = 45
    Compression = yes
    CompressionLevel = 9
    ForwardX11 = yes
      
    [bitbucket.org]
    User = hg
      
    [topsecret.server.com]
    Port = 50022
    ForwardX11 = no

如果想用python生成一个这样的文档怎么做呢？

创建文件：

    import configparser
    
    config = configparser.ConfigParser() #创建一个对象，当做一个字典
    
    config["DEFAULT"] = {'ServerAliveInterval': '45',
                          'Compression': 'yes',
                         'CompressionLevel': '9',
                         'ForwardX11':'yes'
                         }
    
    config['bitbucket.org'] = {'User':'hg'}
    
    config['topsecret.server.com'] = {'Host Port':'50022','ForwardX11':'no'}
    
    with open('example.ini', 'w') as f:
    
       config.write(f)  #格式就是这样把我们的config对象写进文件f。

 
 查找文件


    import configparser
    
    config = configparser.ConfigParser()
    
    #---------------------------查找文件内容,基于字典的形式
    
    print(config.sections())        # sections打印配置文件的字段信息，想当于最最外层字典key。此时还没读文件为空。
    
    config.read('example.ini')  #要先把文件读出来
    
    print(config.sections())   # ['bitbucket.org', 'topsecret.server.com']，还有一个DEFAULT没有显示出来，这个项相当于公共的，每个里面都有
    
    print('bytebong.com' in config) # False  跟判断某个字符串是不是字典的key类似
    print('bitbucket.org' in config) # True
    
    
    print(config['bitbucket.org']["user"])  # hg
    
    print(config['DEFAULT']['Compression']) #yes
    
    print(config['topsecret.server.com']['ForwardX11'])  #no
    
    
    print(config['bitbucket.org'])          #<Section: bitbucket.org>拿的是一个对象 
    
    for key in config['bitbucket.org']:     # 注意,有default会把默认里面的键也取出来。
        print(key)
    
    print(config.options('bitbucket.org'))  # 同for循环,找到'bitbucket.org'下所有键
    
    print(config.items('bitbucket.org'))    #找到'bitbucket.org'下所有键值对
    
    print(config.get('bitbucket.org','compression')) # yes       get方法取深层嵌套的值
 
 
增删改操作


    import configparser
    
    config = configparser.ConfigParser()
    
    config.read('example.ini')
    
    config.add_section('yuan')
    
    
    
    config.remove_section('bitbucket.org')
    config.remove_option('topsecret.server.com',"forwardx11")
    
    
    config.set('topsecret.server.com','k1','11111')
    config.set('yuan','k2','22222')
    
    config.write(open('new2.ini', "w")) 
