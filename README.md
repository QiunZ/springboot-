# springboot学习总结

## 一、快速入门

#### 1.创建springboot项目两种方式

- spring Initializr页面工具
- IDEA中的spring Initializr工具

#### 2.springboot属性配置文件application.properties

1)**自定义属性与加载**
	自定义属性方式：name=张巧宁;加载方式用@Value("${name}")

2)**可以在application.properties文件中引用自定义的属性**

3)**使用随机数**：可以通过${random}产生随机数
	随机字符串：${random.value}
	随机int：random.int
	随机long:random.long
	10以内随机数:random.int(10)
	10到20随机数:random.int[10,20]

4)**通过命令行设置属性值**

- java -jar xxx.jar --server.port=8888，连续两个--就是对application.properties中的属性值进行赋值的标识。
- 为了安全可以屏蔽命令行设置：SpringApplication.setAddCommandLineProperties(false)

5)**多环境配置**

- 创建多个配置文件，配置文件名格式为application-{profile}.properties的格式
- application-dev.properties:开发环境，application-test.properties：测试环境，application-prod.properties:生产环境
- 然后在application.properties文件中通过spring.profiles.active属性来设置，如：spring.profiles.active=test就会加载application-test.properties配置文件内容
- 也可以通过命令行设置：java -jar xxx.jar --spring.profiles.active=test

## 二、Web开发

#### 1.核心注解和参数注解

1）核心注解：

- @Controller:修饰class,用来创建处理http请求的对象
- @RestController：spring4之后加入的注解，原来在@Controller中返回json需要@ResponseBody来配合，现在直接用@RestController就可以了
- @RequestMapping：配置url映射

2）参数注解：

- @PathVariable 
- @ModelAttribute
- @RequestParam 

#### 2.Spring Boot中使用Swagger2构建强大的RESTful API文档

1）添加两个依赖springfox-swagger2，springfox-swagger-ui

2）创建swagger2配置类，要跟启动类Application.java同级

3）配置类中要有@Configuration@EnableSwagger2

#### 3.自制的spring-boot-starter-swagger

- 查看网站文档

#### 4.统一异常管理

- 先创建一个异常信息pojo:ErrorInfo，封装相关异常信息：比如url,data,message
- 然后创建一个全局异常处理器，通过@ExceptionHandler的value属性匹配各种异常，通过@ResponseBody返回json格式数据，将异常信息传入ErrorInfo对象，返回ErrorInfo对象
- 或者可以通过模版，将异常信息封装入ModelAndView对象，然后将这个ModelAndView对象传入模版
