## 面向对象的编程（oop）
面向过程编程：程序具有一系列线性步骤：主体思想是代码作用于数据。

面向对象编程：围绕数据及为数据严格定义的接口来组织程序，用数据控制对代码的访问。

面向对象的核心概念：

类型由状态集合（数据）和转换这些状态的操作集合组成

所有东西都是对象

程序是一大堆对象的组合。通过消息传递，各对象知道自己该做什么，消息就是调用请求，它调用的是从属于目标对象的一个方法。

每个对象都有自己的存储空间，命名空间，一个伟大的想法。

每个对象都属于某一个类型，即类，对象就是类的事例化。

定义一个类后，可以根据需要事例化多个对象

面向对象的程序设计的优点是：解决了程序的扩展性。对某一个对象单独修改，会立刻反映到整个体系中，如对游戏中一个人物参数的特征和技能修改都很容易。

应用场景：需求经常变化的软件，一般需求的变化都集中在用户层，互联网应用，企业内部软件，游戏等都是面向对象的程序设计大显身手的好地方


### python类和实例化

python中一切皆为对象，且python3统一了类与类型的概念，类型就是类。

类是一种数据结构，可用于创建实例，类封装了数据和可用于该数据的方法。

python中使用class关键字创建类，语法格式如下：

    class ClassName(bases):
        'class documentation string'（可选）
         class_suite
        

类体可以包含：声明语句、类成员定义、数据属性、方法   


class语句的一般形式：

    class ClassName(bases):
        date = value  #定义数据属性
        def method(self,...) #定义方法属性
            pass

python中，class语句类似def，是可执行代码。

每个实例对象都会继承类的属性并获得自己的名称空间。

大前提：

1.只有在python2中才分新式类和经典类，python3中统一都是新式类

2.新式类和经典类声明的最大不同在于,所有新式类必须继承至少一个父类

3.所有类甭管是否显式声明父类，都有一个默认继承object父类（讲继承时会讲，先记住）
在python2中的区分

经典类：

    class 类名:
    
        pass

新式类：

    class 类名(父类):
        pass

在python3中，上述两种定义方式全都是新式类


在本节开头介绍得出结论，类是数据与函数的结合，二者称为类的属性

    class Garen:    #定义英雄盖伦的类，不同的玩家可以用它实例出自己英雄;
        camp='Demacia'  #所有玩家的英雄(盖伦)的阵营都是Demacia;
        def attack(self,enemy):   #普通攻击技能，enemy是敌人;
            enemy.life_value-=self.aggressivity #根据自己的攻击力，攻击敌人就减掉敌人的生命值。


类有两种作用：属性引用和实例化

1.属性引用（类名.属性）

    >>> Garen.camp #引用类的数据属性，该属性与所有对象/实例共享
    'Demacia'
    >>> Garen.attack #引用类的函数属性，该属性也共享
    <function Garen.attack at 0x101356510>
    >>> Garen.name='Garen' #增加属性
    >>> del Garen.name #删除属性


2.实例化（\_\_init\_\_与self）

    类名加括号就是实例化，会自动触发__init__函数的运行，可以用它来为每个实例定制自己的特征


    class Garen:        #定义英雄盖伦的类，不同的玩家可以用它实例出自己英雄;
        camp='Demacia'  #所有玩家的英雄(盖伦)的阵营都是Demacia;
        def __init__(self,nickname,aggressivity=58,life_value=455): #英雄的初始攻击力58...;
            self.nickname=nickname  #为自己的盖伦起个别名;
            self.aggressivity=aggressivity #英雄都有自己的攻击力;
            self.life_value=life_value #英雄都有自己的生命值;
        def attack(self,enemy):   #普通攻击技能，enemy是敌人;
            enemy.life_value-=self.aggressivity #根据自己的攻击力，攻击敌人就减掉敌人的生命值。
    


实例化：类名+括号

    >>> g1=Garen('草丛伦') #就是在执行Garen.__init__(g1,'草丛伦')，然后执行__init__内的代码g1.nickname=‘草丛伦’等
    
    
self的作用是在实例化时自动将对象/实例本身传给\_\_init\_\_的第一个参数，self可以是任意名字,但是约定俗成的都是写self。

这种自动传递的机制还体现在g1.attack的调用上，后续会介绍。    
    
查看类和对象的名称空间

类名.\_\_dict\_\_:查出的是一个字典，key为属性名，value为属性值

对象（实例化）.\_\_dict\_\_:查出的是一个字典，key为属性名，value为属性值


特殊的类属性

类名.\_\_name\_\_  # 类的名字(字符串)

类名.\_\_doc\_\_  # 类的文档字符串

类名.\_\_base\_\_  # 类的第一个父类(在讲继承时会讲)

类名.\_\_bases\_\_  # 类所有父类构成的元组(在讲继承时会讲)

类名.\_\_dict\_\_   # 类的字典属性

类名.\_\_module\_\_  # 类定义所在的模块

类名.\_\_class\_\_  # 实例对应的类(仅新式类中)


补充：挑出一个错误

    raise IndexError
    
对象是关于类而实际存在的一个例子，即实例

    >>> g1=Garen('草丛伦') #类实例化得到g1这个实例，基于该实例我们讲解实例相关知识
    >>> type(g1) #查看g1的类型就是类Garen
    <class '__main__.Garen'>
    >>> isinstance(g1,Garen) #g1就是Garen的实例
    True

对象/实例只有一种作用：属性引用  

    #对象/实例本身其实只有数据属性
    >>> g1.nickname
    '草丛伦'
    >>> g1.aggressivity
    58
    >>> g1.life_value
    455
    '''
    查看实例属性
    dir和内置__dict__两种方式
    特殊实例属性
    __class__
    __dict__
    ....
    '''

对象/实例本身只有数据属性，但是python的class机制会将类的函数绑定到对象上，称为对象的方法，或者叫绑定方法，绑定方法唯一绑定一个对象，同一个类的方法绑定到不同的对象上，属于不同的方法，内存地址都不会一样

    >>> g1.attack #对象的绑定方法
    <bound method Garen.attack of <__main__.Garen object at 0x101348dd8>>
    
    >>> Garen.attack #对象的绑定方法attack本质就是调用类的函数attack的功能，二者是一种绑定关系
    <function Garen.attack at 0x101356620>


备注：对象的绑定方法的特别之处在于：obj.func()会把obj传给func的第一个参数。



#### 对象之间的交互

我们可以仿照garen类再创建一个Riven类


    class Riven:
        camp='Noxus'  #所有玩家的英雄(锐雯)的阵营都是Noxus;
        def __init__(self,nickname,aggressivity=54,life_value=414): #英雄的初始攻击力54;
            self.nickname=nickname  #为自己的锐雯起个别名;
            self.aggressivity=aggressivity #英雄都有自己的攻击力;
            self.life_value=life_value #英雄都有自己的生命值;
        def attack(self,enemy):   #普通攻击技能，enemy是敌人;
            enemy.life_value-=self.aggressivity #根据自己的攻击力，攻击敌人就减掉敌人的生命值。 
    
实例出一个Riven来

    >>> r1=Riven('锐雯雯')


交互：锐雯雯攻击草丛伦，反之一样

    >>> g1.life_value
    455
    >>> r1.attack(g1)
    >>> g1.life_value
    401 


 #### 类名称空间与对象/实例名称空间

创建一个类就会创建一个类的名称空间，用来存储类中定义的所有名字，这些名字称为类的属性

而类有两种属性：数据属性和函数属性

其中类的数据属性是共享给所有对象的

    >>> id(r1.camp) #本质就是在引用类的camp属性，二者id一样
    4315241024
    >>> id(Riven.camp)
    4315241024
     

而类的函数属性是绑定到所有对象的：

    >>> id(r1.attack) 
    4302501512
    >>> id(Riven.attack)
    4315244200
    
    '''
    r1.attack就是在执行Riven.attack的功能，python的class机制会将Riven的函数属性attack绑定给r1，r1相当于拿到了一个指针，指向Riven类的attack功能
    
    除此之外r1.attack()会将r1传给attack的第一个参数
    '''

#### 类名称空间和对象的名称空间
**创建一个对象/实例就会创建一个对象/实例的名称空间，存放对象/实例的名字，称为对象/实例的属性**

**在obj.name会先从obj自己的名称空间里找name，找不到则去类中找，类也找不到就找父类...最后都找不到就抛出异常**

-----
### 继承与派生
什么是继承

继承是一种创建新类的方式，在python中，新建的类可以继承一个或多个父类，父类又可称为基类或超类，新建的类称为派生类或子类

python中类的继承分为：单继承和多继承

    class People: #定义父类
        pass
    class Animal:  #定义父类
        pass
        
    class Student1(People):  #单继承，基类是People，派生类是Student
        pass
    
    class Student2(People,Animal): #python支持多继承，用逗号分隔开多个继承的类
        pass
        
        
查看继承
    
    print(Student1__bases__)
    print(People.__bases__)

提示：如果没有指定基类，python3的类会默认继承object类，object是所有python3类的基类，它提供了一些常见方法（如\_\_str\_\_）的实现。

    >>>print(People.__bases__)
    (<class 'object'>,)

python2中

但凡是继承了object类的子类，以及该子类的子类，都称为新式类（在python3中所有的类都是新式类）
没有继承object类的子类称为经典类（没有继承object的类，以及它的子类，都是经典类）

-----
### 继承与抽象（先抽象再继承）

抽象即抽取类似或者说比较像的部分。

抽象分成两个层次： 

1.将奥巴马和梅西这俩对象比较像的部分抽取成类； 

2.将人，猪，狗这三个类比较像的部分抽取成父类。

抽象最主要的作用是划分类别（可以隔离关注点，降低复杂度）


继承：是基于抽象的结果，通过编程语言去实现它，肯定是先经历抽象这个过程，才能通过继承的方式去表达出抽象的结构。

抽象只是分析和设计的过程中，一个动作或者说一种技巧，通过抽象可以得到类

通过继承建立了派生类与基类之间的关系，它是一种'是'的关系，比如白马是马，人是动物。

当类之间有很多相同的功能，提取这些共同的功能做成基类，用继承比较好.


什么是派生？

子类继承了父类的属性，然后衍生出自己新的属性，
如果子类衍生出的新的属性与父类的某个属性名字相同，
那么再调用子类的这个属性，就以子类自己这里的为准了

继承加派生的生的例子

    class People:
    def __init__(self,name,age,sex):
        self.name = name
        self.age = age
        self.sex = sex
    def walk(self):
        print('%s is walking'%self.name)
    def foo(self):
        print('from father %s'%self.name)


    class Teacher(People):
        school = 'oldboy'
        def __init__(self,name,age,sex,level,salary):
            People.__init__(self,name,age,sex)  #子类引用父类属性
            self.level = level  #子类派生数据属性
            self.salary = salary
        def teach(self):  #子类派生出来的函数属性
            print('%s is teaching'%self.name)
    
        def foo(self):
            People.foo(self)
            print('from teacher')

    class Student(People):
        def __init__(self,name,age,sex,group):
            People.__init__(self,name,age,sex)
            self.group = group  
        def study(self):
            print('%s is studying' %self.name)
    
    
    t = Teacher('agon',18,'male',10,3000)
    t.foo()

----
### 组合的方式
软件重用的重要方式除了继承之外还有另外一种方式，即：组合

组合指的是，在一个类中以另外一个类的对象作为数据属性，称为类的组合

用组合的方式建立了类与组合的类之间的关系，它是一种‘有’的关系,比如老师有生日，学生有生日。


    class People:
    def __init__(self,name,age,year,mon,day):
        self.name = name
        self.age = age
        self.birth = Date(year,mon,day)  #生成一个日期对象，作为人这个类的数据属性。

    def walk(self):
        print('%s is walking'%self.name)

    class Date:  #定义一个日期的类
        def __init__(self,year,mon,day):
            self.year = year
            self.mon = mon
            self.day = day
    
        def tell_birth(self):
            print('出生于<%s>年 <%s>月 <%s>日'%(self.year,self.mon,self.day))
    
    class Teacher(People):
        def __init__(self,name,age,year,mon,day,level,salary):
            People.__init__(self,name,age,year,mon,day)
            self.level = level
            self.salary = salary
    
        def teach(self):
            print('%s is teaching'%self.name)
    
    class Student(People):
        def __init__(self,name,age,year,mon,day,group):
            People.__init__(self,name,age,year,mon,day)
            self.group = group
        def study(self):
            print('%s is studying'%self.name)
    
    t = Teacher('agon',18,1990,5,18,10,3000)
    t.birth.tell_birth()
    
----
### 接口与归一化设计
接口提取了一群类共同的函数，可以把接口当做一个函数的集合。然后让子类去实现接口中的函数。
这么做的意义在于归一化，什么叫归一化，就是只要是基于同一个接口实现的类，那么所有的这些类产生的对象在使用时，从用法上来说都一样。
归一化，让使用者无需关心对象的类是什么，只需要的知道这些对象都具备某些功能就可以了，这极大地降低了使用者的使用难度。

在python中使用继承来模拟接口作用。

继承有两种用途：

一：继承基类的方法，并且做出自己的改变或者扩展（代码重用）

二：声明某个子类兼容于某基类，定义一个接口类Interface，接口类中定义了一些接口名（就是函数名）且并未实现接口的功能，子类继承接口类，并且实现接口中的功能

    class Interface: #定义接口Interface类来模仿接口的概念，python中压根就没有interface关键字来定义一个接口。
    def read(self):  #定接口函数read
        pass
    def write(self):  #定义接口函数write
        pass
    class Txt(File): #文本，具体实现read和write
        def read(self):
            print('文本数据的读方法')
    
        def write(self):
            print('文本数据的写方法')
    
    class Sata(File): #磁盘，具体实现read和write
        def read(self):
            print('硬盘数据的读方法')
    
        def write(self):
            print('硬盘数据的写方法')
    
    class Process(File):
        def read(self):
            print('进程数据的读方法')
    
        def write(self):
            print('进程数据的写方法')
            
    t = Txt()
    t.read()
    t.write()
    
---- 
### 抽象类

什么是抽象类

与java一样，python也有抽象类的概念但是同样需要借助模块实现，抽象类是一个特殊的类，它的特殊之处在于只能被继承，不能被实例化

为什么要有抽象类

如果说类是从一堆对象中抽取相同的内容而来的，那么抽象类就是从一堆类中抽取相同的内容而来的，内容包括数据属性和函数属性。
    
比如我们有香蕉的类，有苹果的类，有桃子的类，从这些类抽取相同的内容就是水果这个抽象的类，你吃水果时，要么是吃一个具体的香蕉，要么是吃一个具体的桃子。。。。。。你永远无法吃到一个叫做水果的东西。

从设计角度去看，如果类是从现实对象抽象而来的，那么抽象类就是基于类抽象而来的。

从实现角度来看，抽象类与普通类的不同之处在于：抽象类中只能有抽象方法（没有实现功能），该类不能被实例化，只能被继承，且子类必须实现抽象方法。这一点与接口有点类似，但其实是不同的.
　 

在python中实现抽象类
    
    import abc  #利用abc模块实现抽象类
    class File(metaclass=abc.ABCMeta):  #定义抽象方法，无需实现功能
        @abc.abstractmethod
        def read(self):
            '子类必须定义读功能'
            pass
        @abc.abstractmethod  #定义抽象方法，无需实现功能
        def write(self):
            '子类必须定义写功能'
            pass
    class Txt(File): #子类继承抽象类，但是必须定义read和write方法
        def read(self):
            print('文本数据的读方法')
    
        def write(self):
            print('文本数据的写方法')
    
    class Sata(File): #子类继承抽象类，但是必须定义read和write方法
        def read(self):
            print('硬盘数据的读方法')
    
        def write(self):
            print('硬盘数据的写方法')
    
    class Process(File):  #子类继承抽象类，但是必须定义read和write方法
        def read(self):
            print('进程数据的读方法')
    
        def write(self):
            print('进程数据的写方法')
            
    wenbenwenjian=Txt()

    yingpanwenjian=Sata()
    
    jinchengwenjian=Process()
    
    #这样大家都是被归一化了,也就是一切皆文件的思想
    wenbenwenjian.read()
    yingpanwenjian.write()
    jinchengwenjian.read()   

抽象类与接口

抽象类的本质还是类，指的是一组类的相似性，包括数据属性（如all_type）和函数属性（如read、write），而接口只强调函数属性的相似性。

抽象类是一个介于类和接口之间的一个概念，同时具备类和接口的部分特性，可以用来实现归一化设计 

----
### 继承实现的原理（继承顺序）

Python的类如果继承了多个类，那么其寻找方法的方式有两种，分别是：深度优先和广度优先

- 当类是经典类时，多继承情况下，会按照深度优先方式查找
- 当类是新式类时，多继承情况下，会按照广度优先方式查找


    class A(object):
        def test(self):
            print('from A')
            
    class B(A):
        def test(self):
            print('from B')
    
    class C(A):
        def test(self):
            print('from C')
    
    class D(B):
        def test(self):
            print('from D')
    
    class E(C):
        def test(self):
            print('from E')
    
    class F(D,E):
        # def test(self):
        #     print('from F')
        pass
    f1=F()
    f1.test()
    print(F.__mro__) #只有新式才有这个属性可以查看线性列表，经典类没有这个属性
    
    #新式类继承顺序:F->D->B->E->C->A
    #经典类继承顺序:F->D->B->A->E->C
    #python3中统一都是新式类
    #pyhon2中才分新式类与经典类

继承原理（python如何实现的继承）

python到底是如何实现继承的，对于你定义的每一个类，python会计算出一个方法解析顺序(MRO)列表，这个MRO列表就是一个简单的所有基类的线性顺序列表，例如

    >>> F.mro() #等同于F.__mro__
    [<class '__main__.F'>, <class '__main__.D'>, <class '__main__.B'>, <class '__main__.E'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>]

为了实现继承,python会在MRO列表上从左到右开始查找基类,直到找到第一个匹配这个属性的类为止。
而这个MRO列表的构造是通过一个C3线性化算法来实现的。它实际上就是合并所有父类的MRO列表并遵循如下三条准则:

- 1.子类会先于父类被检查
- 2.多个父类会根据它们在列表中的顺序被检查
- 3.如果对下一个类存在两个合法的选择,选择第一个父类

----
### 子类中调用父类方法
子类继承了父类的方法，然后想进行修改，注意了是基于原有的基础上修改，那么就需要在子类中调用父类的方法

方法一：父类名.父类方法()

    # 日期的类
    class Date:
        def __init__(self,name,year,mon,day):
            self.name = name
            self.year = year
            self.mon = mon
            self.day = day
        def tell_birth(self):
            print('%s:%s-%s-%s' %(self.name,self.year,self.mon,self.day))
    # 课程类
    class Course:
        def __init__(self,name,price,period):
            self.name = name
            self.price = price
            self.period = period
        def tell_course(self):
            print('''
            ---------%s info----------
            course name:%s
            course price:%s
            course period:%s
            '''%(self.name,self.name,self.price,self.period))
    
    # 人的类
    class People:
        def __init__(self,name,age,sex):
            self.name = name
            self.age = age
            self.sex = sex
            self.courses = []
    
        def walk(self):
            print('%s is walking' % self.name)
        def tell_course(self):
            for obj in self.courses:
                obj.tell_course()
    
    # 老师类
    class Teacher(People):
        def __init__(self,name,age,sex,salary,level):
            People.__init__(self,name,age,sex) #调用父类属性，父类名.父类方法()
            self.salary = salary
            self.level = level
    
        def teach(self):
            print('%s is teaching' %self.name)
    
        def tell_info(self):
            print('''
            ---------%s info------------
            NAME:%s
            AGE:%s
            SEX:%s
            SAL:%s
            LEVEL:%s
            '''%(self.name,self.name,self.age,self.sex,self.salary,self.level))
    
    
    # 学生类
    class Student(People):
        def __init__(self,name,age,sex,group):
            People.__init__(self,name,age,sex)  #调用父类属性，父类名.父类方法()
            self.group = group
        def study(self):
            print('%s is studying' %self.name)
    
        def tell_info(self):
            print('''
            ---------%s info------------
            NAME:%s
            AGE:%s
            SEX:%s
            group:%s
            '''%(self.name,self.name,self.age,self.sex,self.group))
    
    #课程实例化
    python = Course('Python',15800,'6mons')
    linux =  Course('Linux',19800,'4mons')
    go = Course('Go',5000,'3mons')
    
    
    # 老师实例化
    print('----------------->teacher info ')
    alex = Teacher('alex',84,'female',300000,-1)
    alex_Birth = Date(alex.name,1900,13,43)
    alex.birth = alex_Birth
    alex.tell_info()
    alex.birth.tell_birth()
    alex.courses.append(python)
    alex.courses.append(go)
    alex.tell_course()
    
    
    #学生的实例化
    print('----------------->student info ')
    gd = Student('gangdan',18,'male','group8')
    gd_Birth = Date(gd.name,1992,5,8)
    gd.tell_info()
    gd.birth = gd_Birth
    gd.birth.tell_birth()
    gd.courses.append(python)
    gd.courses.append(go)
    gd.tell_course()


方法二：super()  


     # 人的类
    class People:
        def __init__(self,name,age,sex):
            self.name = name
            self.age = age
            self.sex = sex
            self.courses = []
    
        def walk(self):
            print('%s is walking' % self.name)
        def tell_course(self):
            for obj in self.courses:
                obj.tell_course()

     # 老师类
    class Teacher(People):
        def __init__(self,name,age,sex,salary,level):
            
            #super(Teacher,self) 就相当于实例本身 在python3中super()等同于super(Teacher,self)
            super().__init__(name,age,sex) #调用父类属性
            self.salary = salary
            self.level = level
    
        def teach(self):
            print('%s is teaching' %self.name)
    
        def tell_info(self):
            print('''
            ---------%s info------------
            NAME:%s
            AGE:%s
            SEX:%s
            SAL:%s
            LEVEL:%s
            '''%(self.name,self.name,self.age,self.sex,self.salary,self.level))
    
    alex = Teacher('alex',84,'female',300000,-1)


补充知识点：对对象数据进行序列化和反序列化操作

    import pickle
    gd = Student('gangdan',18,'male','group8')
    with open('studentdb.pkl','wb') as f:
        pickle.dump(gd,f)
    with open('studentdb.pkl','rb') as f:
        obj = pickle.load(f)
        obj.tell_info()


注意：

当你使用super()函数时,Python会在MRO列表上继续搜索下一个类。只要每个重定义的方法统一使用super()并只调用它一次,那么控制流最终会遍历完整个MRO列表,每个方法也只会被调用一次（注意注意注意：使用super调用的所有属性，都是从MRO列表当前的位置往后找，千万不要通过看代码去找继承关系，一定要看MRO列表）


-----
### 多态与多态性

多态

多态指的是一类事物有多种形态，比如水分为固态，液态，气态三种不同的形态。


动物有多种形态：人，狗，猪

    import abc
    class Animal(metaclass=abc.ABCMeta): #同一类事物:动物
        @abc.abstractmethod
        def talk(self):
            pass
    
    class People(Animal): #动物的形态之一:人
        def talk(self):
            print('say hello')
    
    class Dog(Animal): #动物的形态之二:狗
        def talk(self):
            print('say wangwang')
    
    class Pig(Animal): #动物的形态之三:猪
        def talk(self):
            print('say aoao')
            

在面向对象方法中一般是这样表述多态性：向不同的对象发送同一条消息（！！！obj.func():是调用了obj的方法func，又称为向obj发送了一条消息func），不同的对象在接收时会产生不同的行为（即方法）。也就是说，每个对象可以用自己的方式去响应共同的消息。所谓消息，就是调用函数，不同的行为就是指不同的实现，即执行不同的函数。

例子一：  
   s = 'hello'
    l = [1,2,3]
    t = ('a','b')
    
    def check_len(obj):
        return len(obj)
    
    print(check_len(s))
    print(check_len(l))
    print(check_len(t))
    
例子二：
 
    import abc
    class Animal(metaclass=abc.ABCMeta):
        @abc.abstractmethod
        def talk(self):
            pass
    class People(Animal):
        def talk(self):
            print('say hello')
    
    class pig(Animal):
        def talk(self):
            print('哼哼哼')
    class dog(Animal):
        def talk(self):
            print('汪汪汪')
    
    class cat(Animal):
        def talk(self):
            print('喵喵喵')
    
    
    alex = People()
    yuanhao = pig()
    wupeiqi = dog()
    agon = cat()
    
    
    def talk(obj):
        obj.talk()
    
    talk(alex)
    talk(yuanhao)
    talk(wupeiqi)

综上我们也可以说，多态性是‘一个接口（函数talk），多种实现（如obj.talk()）’


多态性的好处:

1.增加了程序的灵活性

　　以不变应万变，不论对象千变万化，使用者都是同一种形式去调用，如func(animal)

2.增加了程序额可扩展性

通过继承animal类创建了一个新的类，使用者无需更改自己的代码，还是用func(animal)去调用 　　　　

----
### 绑定方法与非绑定方法
类中定义的函数分成两大类：

一：绑定方法（绑定给谁，谁来调用就自动将它本身当作第一个参数传入）：

1. 绑定到类的方法：用classmethod装饰器装饰的方法。

为类量身定制

类.boud_method(),自动将类当作第一个参数传入

（其实对象也可调用，但仍将类当作第一个参数传入）


2 .绑定到对象的方法：没有被任何装饰器装饰的方法。

为对象量身定制

对象.boud_method(),自动将对象当作第一个参数传入

（属于类的函数，类可以调用，但是必须按照函数的规则来，没有自动传值那么一说）

    class People:
        def __init__(self,name):
            self.name = name
        def bar(self):   #绑定给对象的方法
            print('----->',self.name)
    
        @classmethod  #绑定给类方法
        def func(cls):
            print(cls)
    
    f = People('egon')
    
    print(People.func)
    print(f.bar)
    
    People.func()


定义MySQL类

    class MySQL:
        def __init__(self,ip,port):
            self.ip = ip
            self.port = port
        @classmethod
        def from_conf(cls):
            import  settings
            obj = cls(settings.ip,settings.port)
            obj.x = 11111
            return obj
    obj = MySQL.from_conf()
    print(obj.ip)
    print(obj.port)
    print(obj.x)    
    
    -----------------------------
    #  settings
    ip = '172.16.1.1'
    port = '8080'


非绑定方法：用staticmethod装饰器装饰的方法

不与类或对象绑定，类和对象都可以调用，但是没有自动传值那么一说。就是一个普通工具而已

注意：与绑定到对象方法区分开，在类中直接定义的函数，没有被任何装饰器装饰的，都是绑定到对象的方法，可不是普通函数，对象调用该方法会自动传值，而staticmethod装饰的方法，不管谁来调用，都没有自动传值一说


    import hashlib
    import pickle
    import os
    student_path = r'E:\py_code\py_s5\py_s5\day25\student'
    
    class People:
        def __init__(self,name,sex,user_id):
            self.name = name
            self.sex = sex
            self.user_id = user_id
            self.id = self.create_id()
    
        def tell_info(self):
            print('''
            ----------%s info----------
            id:%s
            name:%s
            sex:%s
            user_id:%s
            '''%(self.name,self.id,self.name,self.sex,self.user_id))
    
        def create_id(self):
            m = hashlib.md5()
            m.update(self.name.encode('utf-8'))
            m.update(self.sex.encode('utf-8'))
            m.update(str(self.user_id).encode('utf-8'))
            return m.hexdigest()
    
        def save(self):
            with open(self.id,'wb') as f:
                pickle.dump(self,f)
        @staticmethod  #非绑定方法，就是一个函数，就是一个工具而已，不需要类，也不需对象
        def get_all():
            res = os.listdir(student_path)
            for item in res:
                file_path = r'%s\%s' % (student_path, item)
                with open(file_path, 'rb') as f:
                    obj = pickle.load(f)
                    obj.tell_info()
    
    p=People('egon','male',123123123)
    p.save()
    People.get_all() #类直接调用非绑定方法
    p1.get_all()  #对象调用非绑定方法

----
### 封装
隐藏实现方案的细节，将代码及其处理的数据绑定在一起的一种编程机制，用于保证程序和数据不受外部干扰且不会被误用。


封装要对外界提供好访问你内部隐藏内容的接口（接口可以理解为入口，有了这个入口，使用者无需且不能够直接访问到内部隐藏的细节，只能走接口，并且我们可以在接口的实现上附加更多的处理逻辑，从而严格控制使用者的访问。


封装分为两个层面：

第一个层面的封装（什么都不用做）：创建类和对象会分别创建二者的名称空间，我们只能用类名.或者obj.的方式去访问里面的名字，这本身就是一种封装

    >>> r1.nickname
    '草丛伦'
    >>> Riven.camp
    'Noxus'

注意：对于这一层面的封装（隐藏），类名.和实例名.就是访问隐藏属性的接口


第二个层面的封装：类中把某些属性和方法隐藏起来(或者说定义成私有的)，只在类的内部使用、外部无法访问，或者留下少量接口（函数）供外部访问。
在python中用双下划线的方式实现隐藏属性（设置成私有的）

类中所有双下划线开头的名称如\_\_x都会自动变形成：_类名__x的形式：

    class People:
        def __init__(self,name,age,sex,height,weight,permission=False):
            self.__name = name  #对属性实现隐藏,变形为self._People__name
            self.__age = age
            self.__sex = sex
            self.__height = height
            self.__weight = weight
            self.permission = permission
        
        def tell_info(self):  #访问详细信息接口
            print('''
            ---------%s info------------
            name:%s
            age:%s
            sex:%s
            height:%s
            weight:%s
            '''%(self.__name,self.__name,self.__age,
                 self.__sex,self.__height,self.__weight)
            )
    
    gd = People('gangdan',18,'male',1.7,65)
    gd.tell_info()  #访问人的详细信息
    
    
这种自动变形的特点：

1.类中定义的\_\_x只能在内部使用，如self.__x，引用的就是变形的结果。

2.这种变形其实正是针对外部的变形，在外部是无法通过\_\_x这个名字访问到的。

3.在子类定义的\_\_x不会覆盖在父类定义的\_\_x，因为子类中变形成了：\_子类名\_\_x,而父类中变形成了：_父类名__x，即双下滑线开头的属性在继承给子类时，子类是无法覆盖的。
    
这种变形需要注意的问题是：

1.这种机制也并没有真正意义上限制我们从外部直接访问属性，知道了类名和属性名就可以拼出名字：\_类名\_\_属性，然后就可以访问了，如a._A__N

2.变形的过程只在类的定义是发生一次,在定义后的赋值操作，不会变形

3.在继承中，父类如果不想让子类覆盖自己的方法，可以将方法定义为私有的

    #把fa定义成私有的，即__fa
    >>> class A:
    ...     def __fa(self): #在定义时就变形为_A__fa
    ...         print('from A')
    ...     def test(self):
    ...         self.__fa() #只会与自己所在的类为准,即调用_A__fa
    ... 
    >>> class B(A):
    ...     def __fa(self):
    ...         print('from B')
    ... 
    >>> b=B()
    >>> b.test()
    from A

python并不会真的阻止你访问私有的属性，模块也遵循这种约定，如果模块名以单下划线开头，那么from module import *时不能被导入,但是你from module import _private_module依然是可以导入的

其实很多时候你去调用一个模块的功能时会遇到单下划线开头的(socket._socket,sys._home,sys._clear_type_cache),这些都是私有的，原则上是供内部调用的，作为外部的你，一意孤行也是可以用的


### 特性（property）

property是一种特殊的属性，访问它时会执行一段功能（函数）然后返回值,把类的函数属性，伪装成数据属性，对外提供接口。

例一：BMI指数（bmi是计算而来的，但很明显它听起来像是一个属性而非方法，如果我们将其做成一个属性，更便于理解）

成人的BMI数值：
过轻：低于18.5
正常：18.5-23.9
过重：24-27
肥胖：28-32
非常肥胖, 高于32
　　体质指数（BMI）=体重（kg）÷身高^2（m）
　　EX：70kg÷（1.75×1.75）=22.86

    class People:
        def __init__(self,name,weight,height):
            self.name=name
            self.weight=weight
            self.height=height
        @property
        def bmi(self):
            return self.weight / (self.height**2)
    
    p1=People('egon',75,1.85)
    print(p1.bmi)



例二：圆的周长和面积
    import math
    class Circle:
        def __init__(self,radius): #圆的半径radius
            self.radius=radius
    
        @property
        def area(self):
            return math.pi * (self.radius**2) #计算面积
    
        @property
        def perimeter(self):
            return 2*math.pi*self.radius #计算周长
    
    c=Circle(10)
    print(c.radius)
    print(c.area) #可以向访问数据属性一样去访问area,会触发一个函数的执行,动态计算出一个值
    print(c.perimeter) #同上
    '''
    输出结果:
    10
    314.1592653589793
    62.83185307179586
    '''


注意：此时的特性arear和perimeter不能被赋值

    c.area=3 #为特性area赋值
    '''
    抛出异常:
    AttributeError: can't set attribute
    '''

为什么要用property

将一个类的函数定义成特性以后，对象再去使用的时候obj.name,根本无法察觉自己的name是执行了一个函数然后计算出来的，这种特性的使用方式遵循了统一访问的原则.

    class People:
        def __init__(self,name,age,sex,height,weight,permission=False):
            self.__name = name
            self.__age = age
            self.__sex = sex
            self.__height = height
            self.__weight = weight
            self.permission = permission
        @property
        def bmi(self):  #访问人的BMI指数
            res = self.__weight / (self.__height **2)
            return res
        @property
        def name(self):  #提供访问姓名接口
            return self.__name
        @name.setter
        def name(self,val):  #提供修改姓名接口
            if not isinstance(val,str):
                raise TypeError('must be str')
            self.__name = val
        @name.deleter
        def name(self):  #提供删除接口
            if not self.permission:
                raise PermissionError('不让删')
            del self.__name
            self.permission = False
    
        def tell_info(self):  #访问详细信息接口
            print('''
            ---------%s info------------
            name:%s
            age:%s
            sex:%s
            height:%s
            weight:%s
            '''%(self.__name,self.__name,self.__age,
                 self.__sex,self.__height,self.__weight)
            )
    
    gd = People('gangdan',18,'male',1.7,65)
    gd.tell_info()  #访问人的详细信息
    print(gd.name)  #访问姓名
    gd.name = '钢蛋' #修改姓名
    print(gd.name)
    gd.permission = True
    del gd.name  #删除姓名
    # print(gd.name)
    print(gd.bmi) #访问人的BMI指数
    
封装意义：

封装在于明确区分内外，使得类实现者可以修改封装内的东西而不影响外部调用者的代码；而外部使用用者只知道一个接口(函数)，只要接口（函数）名、参数不变，使用者的代码永远无需改变。这就提供一个良好的合作基础——或者说，只要接口这个基础约定不变，则代码改变不足为虑。 


------
### 关于类的几个内置函数介绍



#### isinstance(obj,cls)和issubclass(sub,super)

isinstance(obj,cls)检查是否obj是否是类 cls 的对象
    
    1 class Foo(object):
    2     pass
    3  
    4 obj = Foo()
    5  
    6 isinstance(obj, Foo)

issubclass(sub, super)检查sub类是否是 super 类的派生类(子类)

    class Foo(object):
        pass
    class Bar(Foo):
        pass
    
    print(issubclass(Bar, Foo))

-----

###反射

python面向对象中的反射：通过字符串的形式操作对象相关的属性。python中的一切事物都是对象（都可以使用反射）

#### hasattr(object,name)
判断object中有没有一个name字符串对应的方法或属性

    class Teacher:
        school = 'oldboy'
        def __init__(self,name,age):
            self.name = name
            self.age = age
    
        def teach(self):
            print('%s teach '%self.name)   

    >>>hasattr(Teacher,'teach')
    True
    
#### getattr(object, name, default=None)

    >>>getattr(Teacher,'teach')
    <function Teacher.teach at 0x00000210EDC7B950>
    
####  setattr(x, y, v)
    >>>setattr(Teacher,'x',1)
    >>>getattr(Teacher,'x')
    1

#### delattr(x, y)

    >>>setattr(Teacher,'x',1)
    >>>delattr(Teacher,'x')
    >>>getattr(Teacher,'x')
    AttributeError: type object 'Teacher' has no attribute 'x'
        


反射的应用场景

    class Cmd:
        def __init__(self,name):
            self.name = name
        def run(self):
            while True:
                cmd = input('>>>: ').strip()
                if not cmd:continue
                if hasattr(self,cmd):
                    func = getattr(self,cmd)
                    func()
                else:
                    print('not valid func')
        def ls(self):
            print('ls function')
    
        def pwd(self):
            print('pwd function')
    
        def cat(self):
            print('cat function')
    
    c = Cmd('egon')
    c.run()

#### \_\_str\_\_

    class Teacher:
        def __init__(self,name,age):
            self.name = name
            self.age = age
            self.courses = []
    
        def teach(self):
            print('%s teach'%self.name)
    
        def __str__(self):
            return '<name:%s age:%s>' %(self.name,self.age)  #答应这个实例化对象时重写这个方法里面return什么我们结果就是什么。
    
    gangdan = Teacher('gangdan',18)
    print(gangdan)


    class Course:
        def __init__(self,name,price,period):
            self.name = name
            self.price = price
            self.period = period
            
        def __str__(self):
            return '<name:%s price:%s period:%s>' %(self.name,self.price,self.period)


    python = Course('python',50000,'36mons')
    print(python)
    
#### \_\_del\_\_
析构方法，当对象在内存中被释放时，自动触发执行。

注：此方法一般无须定义，因为Python是一门高级语言，程序员在使用时无需关心内存的分配和释放，因为此工作都是交给Python解释器来执行，所以，析构函数的调用是由解释器在进行垃圾回收时自动触发执行的。

    import time
    class Foo:
        def __init__(self,x):
            self.x = x
            print('connect mysql')
    
        def __del__(self):
            '''做一些与这个对象有关的清理操作'''
            print('---------------->')
    
    f = Foo(10)
    del f  #对象被清理的时候触发执行__del__()
    time.sleep(3)
    print('主程序')
    
    #输出结果
    connect mysql
    ---------------->
    主程序

#### \_\_setitem\_\_,\_\_getitem,\_\_delitem\_\_


    class People:
        def __init__(self,name,age,sex):
            self.name = name
            self.age = age
            self.sex = sex
        def __getitem__(self, item):
            return getattr(self,item) #另外一种写法self.__dict__[item]
        def __setitem__(self, key, value):
            setattr(self,key,value)  #self.__dict__[key] = value
        def __delitem__(self, key):
            delattr(self,key)  #del self.__dict__[key]
    
    gangdan =People('gangdan',18,'male')
    print(gangdan['name'])
    gangdan['x'] = 1
    print(gangdan.__dict__)
    del gangdan['x']
    print(gangdan.__dict__)
    
    #执行结果：
    gangdan
    {'name': 'gangdan', 'age': 18, 'sex': 'male', 'x': 1}
    {'name': 'gangdan', 'age': 18, 'sex': 'male'}

----
### optparse模块

        from optparse import OptionParser 
    parser = OptionParser() 
    parser.add_option("-p", "--pdbk", action="store_true", 
                      dest="pdcl", 
                      default=False, 
                      help="write pdbk data to oracle db") 
    parser.add_option("-z", "--zdbk", action="store_true", 
                  dest="zdcl", 
                  default=False, 
                  help="write zdbk data to oracle db") 

    (options, args) = parser.parse_args() 
    
    if options.pdcl==True: 
        print 'pdcl is true' 
    if options.zdcl==True: 
        print 'zdcl is true' 
        
add_option用来加入选项，action是有store，store_true，store_false等，dest是存储的变量，default是缺省值，help是帮助提示 

最后通过parse_args()函数的解析，获得选项，如options.pdcl的值。

使用例子：
    
    #test.py
    import optparse
    class FtpClient(object):
        """ftp客户端"""
        MSG_SIZE = 1024  # 消息最长1024
        def __init__(self):
            self.username = None
            parser = optparse.OptionParser()  # 使用optparse模块进行命令行参数解析
            parser.add_option("-s", "--server", dest="server", help="ftp server ip_addr")
            parser.add_option("-P", "--port", type="int", dest="port", help="ftp server port")
            parser.add_option("-u", "--username", dest="username", help="username info")
            parser.add_option("-p", "--password", dest="password", help="password info")
            self.options, self.args = parser.parse_args()
    
            print(self.options,self.args,type(self.options),self.options.server)
            #E:\py_code\py_s5>python E:\py_code\py_s5\py_s5\LuffyFTP\server\core\test.py 1 10 -s 172.1.1.1 -P 9999
            #{'server': '172.1.1.1', 'port': 9999, 'username': None, 'password': None} ['1', '10'] <class 'optparse.Values'> 172.1.1.1
    
    
    
    if __name__ == "__main__":
        client = FtpClient()  #事例化出client对象，并初始化