[markdown语法格式](https://www.jianshu.com/p/191d1e21f7ed/)

#python如何运行程序

##程序员视角下的python程序
最简单的一个python程序，就是只有一个包含python语句的文本文件。
如下的script0.py的简单实例：

```cython
print("hello world")
print(2 ** 100)
```
按照惯例，python文件都是以.py结尾的。从技术上来说，这种命名方案只有在"导入"时才是必须的，但是绝大多数python文件为了统一都是以.py结尾。


##python的视角
当python运行脚本时，在代码开始进行处理之前，python还会进行一些步骤。准确说，第一步是编译成所谓的“字节码”，之后将其转发到所谓的“虚拟机”中。

###字节码编译
当程序执行时，python内部会先将源代码编译成字节码的形式。编译是一个简单的翻译步骤，而且字节码是源代码底层的、与平台无关的表现形式。
如果python进程有对服务器的写权限，那么它将程序的字节码保存为一个以.pyc为扩展名的文件。

###python虚拟机
 一旦程序编译成字节码，之后的字节码发送到python虚拟机(PVM)上来执行。事实上，PVM就是一个迭代运行字节码指令的大循环。
 PVM是python的运行引擎，时常表现为python系统的一部分，并且它是实际运行脚本的组件。从技术上来说，它才是python解释器的最后一步。
 
 
 ##python实现的替代者 
 三种主要的实现方式：CPython JPython IronPython。
 其中CPython是标准实现
 
 ##冻结二进制文件
 主要有3种系统能生成冻结二进制文件：py2exe(windows下使用) PyInstaller(能在linux及unix上使用)
 