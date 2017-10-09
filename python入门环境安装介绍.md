# Python的种类

Cpython
    Python的官方版本，使用C语言实现，使用最为广泛，CPython实现会将源文件（py文件）转换成字节码文件（pyc文件），然后运行在Python虚拟机上。
    
Jyhton
    Python的Java实现，Jython会将Python代码动态编译成Java字节码，然后在JVM上运行。
    
IronPython
    Python的C#实现，IronPython将Python代码编译成C#字节码，然后在CLR上运行。（与Jython类似）
    
PyPy（特殊）
    Python实现的Python，将Python的字节码字节码再编译成机器码。
RubyPython、Brython ...

----
# python软件安装

- windows：（python3.6）

1、下载安装包
    https://www.python.org/downloads/
    
2、安装
    默认安装路径：C:\python3
    
3、配置环境变量
    【右键计算机】--》【属性】--》【高级系统设置】--》【高级】--》【环境变量】--》【在第二个内容框中找到 变量名为Path 的一行，双击】 --> 【Python安装目录追加到变值值中，用 ； 分割】
    如：原来的值;C:\python3，切记前面有分号

- linux：
1、下载源码

    https://www.python.org/downloads/

2、编译安装（需要cd到解压目录执行）

  ./configure --prefix=/usr/local/python3

3、make&&make install

4.创建一个软链接
ln -sv /usr/local/python3/bin/python3.6 /usr/bin/python3

----

# 编译安装iPython
1.下载源码包

ipython的源码下载页面为：https://pypi.python.org/pypi/ipython

或者是到git页面下载：https://github.com/ipython/ipython/downloads

2.解压下载安装包

tar xf ipythoon-0.8.2.tar.gz

3.编译

/usr/bin/python3 build

4.安装

/usr/bin/python3 install

5.创建软链接

ln -sv /usr/local/python3/bin/ipython /usr/bin/ipython



