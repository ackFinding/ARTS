### [Spring DI Patterns: The Good, The Bad, and The Ugly - DZone Java](https://dzone.com/articles/spring-di-patterns-the-good-the-bad-and-the-ugly)
这篇文章主要讲了在Spring中使用依赖注入的三种方式：
##### (1)Field injection (the bad)
```
public class MyBean {
   @Autowired
   private AnotherBean anotherBean;
   //Business logic...
}
```
##### (2)Setter injection (the ugly)
```
public class MyBean {
   private AnotherBean anotherBean;
   @Autowired
   public void setAnotherBean(final AnotherBean anotherBean) {
       this.anotherBean = anotherBean;
   }
   //Business logic...
}
```
##### (3)Constructor injection (the good)
```
public class MyBean {
   private final AnotherBean anotherBean;
   public MyBean(final AnotherBean anotherBean) {
       this.anotherBean = anotherBean;
   }
   //Business logic...
}
```
我们经常使用的Field injection方式容易出现循环依赖问题、难以调试等。推荐使用构造器注入方式
