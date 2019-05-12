### 享元模式在jdk应用
#### 1.简介
享元模式（Flyweight Pattern）主要用于减少创建对象的数量，以减少内存占用和提高性能。
#### 2.举例
当使用Integer.valueOf创建对象会是怎样的呢？查看源码：  
如果创建的数在[-128,127]会先从缓存直接返回，不是才进行new
```java
    public static Integer valueOf(int i) {
        if (i >= IntegerCache.low && i <= IntegerCache.high)
            return IntegerCache.cache[i + (-IntegerCache.low)];
        return new Integer(i);
    }
```
Long、Integer并没有照搬享元模式，类内部维护了一个静态的对象池，仅缓存了 [-128,127] 之间的数字，这个对象池在 JVM 启动的时候就创建好了，而且这个对象池一直都不会变化，也就是说它是静态的。因为这个范围的数字利用率最高。  
除了Integer，Long、Short、Byte这些基本数据类型的包装类都有用到享元模式。  
#### 3.总结
享元模式本质上其实就是一个对象池：创建之前，首先去对象池里看看是不是存在；如果已经存在，就利用对象池里的对象；如果不存在，就会新创建一个对象，并且把这个新创建出来的对象放进对象池里。
