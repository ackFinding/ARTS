### 25. Profiles
Spring Profiles提供了隔离应用配置，@Component或者@Configuration都可以标识上@Profile来限制什么时候加载
#### I.通过注解标识
```java
@Configuration
@Profile("production")
public class ProductionConfiguration {

	// ...

}
```
#### II.在application.properties配置
```
spring.profiles.active=dev,hsqldb
```
#### III.命令行指定
```
--spring.profiles.active=dev,hsqldb
```
#### 1.添加激活的profile
在spring.profiles.active配置，可以被命令行覆盖
#### 2.在编码设置Profiles
(1)
```java
SpringApplication.setAdditionalProfiles(…​)
```
(2)使用ConfigurableEnvironment接口
#### 3.指定profiles配置文件
除了直接在application.properties配置，也可以通过application-{profile}.properties命名
### 26.Logging
#### 1.spring boot控制台默认输出ERROR-level, WARN-level, INFO级别的日志
可以通过以下命令输出debug级别日志：
```
$ java -jar myapp.jar --debug
```
或者在application.properties指定debug=true
#### 2.指定不同日志级别输出颜色
(1)如果终端支持ANSI，可进行如下配置：  
spring.output.ansi.enabled=ALWAYS / DETECT / NEVER（总是开启、支持ANSI则开启、不开启）  
(2)也可以自定义颜色  
#### 3.输出文件
spring boot的日志只输出在控制台，如果想要输出到文件，需要在application.properties配置logging.file或者logging.path属性  
**ps**：日志系统会在application生命周期前进行初始化，因此如果通过@PropertySource注解配置日志属性不会找到。
#### 4.日志级别
```
logging.level.root=WARN
logging.level.org.springframework.web=DEBUG
logging.level.org.hibernate=ERROR
```
#### 5.日志分组
将相关联的日志分组，可以方便地同时配置  
(1)比如：  
指定tomcat分组
```
logging.group.tomcat=org.apache.catalina, org.apache.coyote, org.apache.tomcat
```
然后配置tomcat分组
```
logging.level.tomcat=TRACE
```
(2)spring boot已经包含了下面的分组  
web=org.springframework.core.codec, org.springframework.http, org.springframework.web  
sql=org.springframework.jdbc.core, org.hibernate.SQL  
### 27.国际化
By default, Spring Boot looks for the presence of a messages resource bundle at the root of the classpath.  
(1)默认属性配置文件：messages.properties  
(2)  
```
## 定义资源包basename
spring.messages.basename=messages,config.i18n.messages
spring.messages.fallback-to-system-locale=false
```
