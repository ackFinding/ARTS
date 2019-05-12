### springboot文档23
#### （1）springboot入口
```java
public static void maian(String[] args) {
	SpringApplication.run(MySpringConfiguration.class, args);
}
```
#### （2）springboot日志默认隔离级别是INFO  
可以在application.properties配置文件修改
####（3）访问应用启动时传入的参数（SpringApplication.run(…)）  
通过ApplicationArguments来访问：
```java
	@Autowired
	public MyBean(ApplicationArguments args) {
		boolean debug = args.containsOption("debug");
		List<String> files = args.getNonOptionArgs();
		// if run with "--debug logfile.txt" debug=true, files=["logfile.txt"]
	}
```
#### （4）ApplicationRunner 、CommandLineRunner
应用启动时如果需要运行某些程序，可以通过实现其中一个接口重写方法:
```java
	public void run(String... args) {
		// Do something...
	}
```
#### （5）Application Exit
可以实现ExitCodeGenerator接口，返回特定exit code。SpringApplication.exit()运行后，该码会传给System.exit()  
eg：
```java
@SpringBootApplication
public class ExitCodeApplication {

	@Bean
	public ExitCodeGenerator exitCodeGenerator() {
		return () -> 42;
	}

	public static void main(String[] args) {
		System.exit(SpringApplication
				.exit(SpringApplication.run(ExitCodeApplication.class, args)));
	}

}
```  
控制台打印的exit code就变成了42
