### Java魔法类：Unsafe应用解析
链接：(https://tech.meituan.com/2019/02/14/talk-about-java-magic-class-unsafe.html)
####
通过这篇文章了解到了堆外内存（如DirectByteBuffer）的分配和释放，以及CAS原子操作
CAS是一条CPU的原子指令（cmpxchg指令），不会造成所谓的数据不一致问题，
Unsafe提供的CAS方法（如compareAndSwapXXX）底层实现即为CPU指令cmpxchg。在java的AQS就依赖于CAS操作进行非阻塞获取锁操作，并且使用了
Unsafe的调用LockSupport.park()和LockSupport.unpark()实现线程的阻塞和唤醒的。这篇文章的一些知识点把之前看AQS的一些方面串了起来，
关于AQS，可查看本人博文：（https://blog.csdn.net/ack_Finding/article/details/81165749）
