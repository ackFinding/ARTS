### 1.什么时候进行垃圾回收
当对象没有被gc root引用的时候
#### （1）什么可以作为gc root？
局部变量、活跃的java线程、静态变量、本地方法栈中JNI的引用的对象
### 2.内存泄漏
可能出现的场景：无限地往静态集合放数据，超过java内存设置，会抛出java.lang.OutOfMemoryError
### 3、引用
#### （1）强引用
最常见的：MyClass obj = new MyClass ();
只要强引用还存在，被引用的对象就永远不会被回收。
#### （2）软引用
用来描述一些还有用但是不是必需的对象。这类引用的对象会在内存溢出之前被列入回收范围进行第二次回收，
如若回收完之后还没有获得足够的内存才会抛出内存溢出异常。
如果垃圾回收器判定需要内存，会进行清理。对软引用的回收策略可能会由于虚拟机的不同有所差异
在Hotspot 虚拟机，虚引用的回收设定了一个定时清除，如果这个对象没有被强引用了，只有虚引用
到时间后会被清除。
需要注意的是这个被虚引用的对象会被清除，但是这个虚引用（也是对象）不会被回收，仍然可能造成内存泄漏。
可以传入一个队列，自行删除
```
 public SoftReference(T referent, ReferenceQueue<? super T> q)；
 ```
#### （3）弱引用
是用来描述非必需的对象，但是强度比软引用更弱，被引用的对象只能存活到下一次GC之前。
当进行GC的时候不论内存是否足够都会对该引用的对象进行回收。
当垃圾回收器检测到object只有虚引用，没有弱引用或强引用来引用的话会进行回收。
示例：
WeakHashMap当除了自身有对key的引用外，此key没有其他引用那么此map会自动丢弃此值 
#### （4）虚引用
最弱的引用关系。虚引用的存在不会对对象的存活造成任何影响，也不能通过虚引用来获得任何对象实例。
设置虚引用的唯一目的就是在关联对象被回收时会获得一个系统通知。
垃圾回收过程中，在被删除前会调用 finalize()方法，此时就是对象和gc root只有虚引用。
使用虚引用可以防止对象被删除，除非你自己删除虚引用，可通过ReferenceQueue显式删除
****
### 总结：
这篇文章简介了下jvm内存进行垃圾回收的时机以及可能产生内存泄漏的情况，分析讲解了java的引用（强引用、软引用、弱引用、虚引用）。
作者结合了底层原理分析得比较完善，如果能再具体讲下各个引用的应用场景就更好了
