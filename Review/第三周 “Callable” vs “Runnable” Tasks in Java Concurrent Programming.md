### [“Callable” vs “Runnable” Tasks in Java Concurrent Programming](https://medium.com/@aayushbhatnagar_10462/callable-vs-runnable-tasks-in-java-concurrent-programming-26b478fe6dfa)
#### 1.这篇文章简介了Runnbale和Callable    
Callable相较于Runnable的优势为：   
（1）可以获取返回值
  可以通过FutureTask包装Callable,提交到Executor线程池中，通过get()方法获取返回值   
（2）执行中的线程可以抛出异常    
#### 2.总结    
这篇文章简介了Runnble的用法，介绍了Callable相较于Runnable的不同。但它分成了3点讲述，第一点讲了Callable可以获取返回值，却在第三点举了个例子。
分点不够明确。
