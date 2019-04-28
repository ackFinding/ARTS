### Spring AOP内部方法调用失效
最近看极客时间的Spring全家桶的课程，里面讲到这样一个问题：  
```java
@Service
public class FooServiceImpl implements FooService{

    @Autowired
    private JdbcTemplate jdbcTemplate;

    @Override
    @Transactional
    public void insertRecord() {
        jdbcTemplate.execute("INSERT INTO FOO(BAR) VALUES ('AAA')");
    }

    @Transactional(rollbackFor = RollbackException.class)//当抛出RollbackException，回滚事务
    @Override
    public void insertThenRollback() throws RollbackException {
        jdbcTemplate.execute("INSERT INTO FOO(BAR) VALUES ('BBB')");
        throw new RollbackException();
    }

    @Override
    public void invokeInsertThenRollback() throws RollbackException {
        insertThenRollback();//调用了内部方法，事务失效
    }
}
```
invokeInsertThenRollback()调用了有事务的insertThenRollback的方法，但是事务会失效，所以能成功插入数据。那么这是为什么呢？  
在spring aop中，看似调用自己的方法，本质上调用的是增强后的代理类。invokeInsertThenRollback()这个调用的是this对象，就是直接调用了本身，是
不会有aop效果的，导致事务失效。  
**解决方法**：
```java
@Service
public class FooServiceImpl implements FooService{

    @Autowired
    private JdbcTemplate jdbcTemplate;

    @Autowired
    private FooService fooService;

    @Override
    @Transactional
    public void insertRecord() {
        jdbcTemplate.execute("INSERT INTO FOO(BAR) VALUES ('AAA')");
    }

    @Transactional(rollbackFor = RollbackException.class)
    @Override
    public void insertThenRollback() throws RollbackException {
        jdbcTemplate.execute("INSERT INTO FOO(BAR) VALUES ('BBB')");
        throw new RollbackException();
    }

    @Override
    public void invokeInsertThenRollback() throws RollbackException {
        insertThenRollback();
    }

    //方法一、调用方也加上@Transactional
    @Transactional(rollbackFor = RollbackException.class)
    public void dealInsertThenRollback1() throws RollbackException {
        insertThenRollback();
    }

    //方法二、调用代理对象方法("自调用",不推荐)
    public void dealInsertThenRollback2() throws RollbackException {
        ((FooService)AopContext.currentProxy()).insertThenRollback();
    }

    //方法三、从IOC容器中获取FooService代理对象(推荐使用)
    public void dealInsertThenRollback3() throws RollbackException {
        fooService.insertThenRollback();
    }
}
```
方法三为啥获取到的是代理对象呢？  
因为在使用Spring AOP的时候，我们从IOC容器中获取的Bean对象其实都是代理对象，而不是那些Bean对象本身
注意：  
（1）需要在application加上@EnableTransactionManagement// 启动注解事务管理，等同于xml配置方式的 <tx:annotation-driven />  
（2）如果使用方法二需要配置@EnableAspectJAutoProxy(exposeProxy=true,proxyTargetClass=true)，或者在xml上配置<aop:aspectj-autoproxy expose-proxy="true" />
