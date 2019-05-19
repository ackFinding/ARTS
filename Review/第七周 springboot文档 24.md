### springboot文档 24
#### 1.随机数产生  
可以使用RandomValuePropertySource 
#### 2.通过命令行设置属性
参数以'--'开头，如--server.port=9000，会添加到spring的环境中,如果不想把这个添加到环境中，可以设置
SpringApplication.setAddCommandLineProperties(false)
#### 3.application.properties属性文件
可以更改属性文件名：
```shell
$ java -jar myproject.jar --spring.config.name=myproject
```
可以添加多个属性文件位置：
```shell
$ java -jar myproject.jar --spring.config.location=classpath:/default.properties,classpath:/override.properties
```
