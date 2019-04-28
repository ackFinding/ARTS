### springboot文档 14~17
#### 14.代码结构
建议将含Main方法的Application放在顶层的包下
#### 15.配置  
（1）推荐使用基于java而不是xml的configuration  
（2）可以通过@Import注解添加额外的configuration classes   
（3）也可以通过@ImportResource加载xml的配置文件  
#### 16.自动配置
选择@EnableAutoConfiguration或者@SpringBootApplication加载@Configuration类上  
（1）可以通过自己配置替换springboot的一些自动配置  
（2）排除某些自动配置类  
通过@EnableAutoConfiguration注解的exclude属性
#### 17.描述了spring的注入
@ComponentScan (to find your beans) and using @Autowired (to do constructor injection)   
@ComponentScan该注解默认会扫描该类所在的包下所有的配置类，相当于xml配置的 <context:component-scan>。 
@ComponentScan注解默认会装配标识了@Controller，@Service，@Repository，@Component注解的类到spring容器中（@ComponentScan里面的useDefaultFilters默认为true），
可以通过excludeFilters 来按照规则排除某些包的扫描。
