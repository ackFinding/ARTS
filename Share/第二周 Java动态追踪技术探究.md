### [Java动态追踪技术探究](https://tech.meituan.com/2019/02/28/java-dynamic-trace.html)
这篇文章从上线需要不重启打印日志检查问题引出通过动态修改class文件的方法实现。介绍了java修改字节码的api java.lang.instrument.Instrumentation中的
两个接口：redefineClasses和retransformClasses。一个是重新定义class，一个是修改class。    
直接操作字节码的框架有ASM，更为便捷的工具是BTrace和Arthas。
