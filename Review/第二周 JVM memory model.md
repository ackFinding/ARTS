### [JVM memory model](http://coding-geek.com/jvm-memory-model/)
#### 1.这篇文章开头简述了jvm加载的过程
源代码->javac编译成.class的字节码文件->为了避免i/o,jvm的classloader加载字节码到jvm的runtime data areas
->字节码文件通过jvm的execution engine进行编译和执行
#### 2.基于栈的结构
描述了操作数栈的操作
#### 3.字节码  
概述了字节码操作  
eg：  
字节码操作类别：  
**Constants**: for pushing values from the constant pool (we’ll see it later) or from known values into the operand stack.  
**Math**: for basic mathematical operations on values from the operand stack.   
**Stack**: for handling the operand stack.  
**Stores**: for storing from the operand stack into local variables.  
**Conversions**: for converting from one type to another.  
**Extended**: operations from the others categories that were added after.   
**References**: for allocating objects or arrays, getting or checking references on objects, method or static methods. Also used for invoking (static) methods.  
**Reserved**: for internal use by each Java Virtual Machine implementation.  
**Comparisons**: for basic comparison between two values.  
**Control**: the basics operations like goto, return, … that allows more advanced operation like loops or functions that return values.  
**Loads**: for loading values from local variables into the operand stack.   
字节码操作：  
The operand i2l (0x85) converts an integer to a long  
The operand arraylength (0xbe)  gives the size of an array  
The operand pop (0x57) pops the first value from the operand stack
#### 4.运行时数据区  
（1）堆  
线程共享  
（2）方法区  
线程共享，通过classloader从字节码中加载来的
保存了：  
①类信息  
②方法和构造器字节码  
③运行时常量池（每个类一个）  
（3）运行时常量池
是方法区的一部分  
（4）程序计数器（每个线程都有）
包含了当前执行jvm指令（在方法区）的地址  
（5）java虚拟机栈（每个线程都有，线程创建会随之创建）  
①帧  
包含了多个数据代表当前线程状态  
a.操作数栈  
b.局部变量数组（表）  
包含当前线程作用范围的局部变量  
c.运行时常量池引用  
当前被执行的类的方法在常量池的引用。( ex: myInstance.method())  
②栈  
一个栈包含多个帧。只有一个帧（当前帧）是当前执行的方法（当前方法）  
（6）本地方法栈（每个线程一个）  
**总结：**作者介绍了java内存模型的各个部分，在描述栈的时候还举了例子，但在本地方法栈中没有说明也可能会抛出StackOverflowError。
还有一点要补充的就是虽然直接内存并不是虚拟机运行时数据区的一部分，也不是jvm规范中定义的内存区域。但是这部分内存也被频繁使用，而且有可能导致OutOfMemoryError
