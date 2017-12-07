&nbsp;&nbsp;Spring Boot提供了一些“启动器(Starters)”，可以方便地将jar添加到类路径中。我们的示例应用程序已经在POM的父部分使用了spring-boot-starter-parent。spring-boot-starter-parent是一个特殊启动器，提供一些Maven的默认值。它还提供依赖管理 dependency-management 标签，以便您可以省略子模块依赖关系的版本标签。

#### @RestController和@RequestMapping 注解（SpringMVC注解）
&nbsp;&nbsp;@RestController被称为 stereotype annotation。它为人们阅读代码提供了一些提示，对于Spring来说，这个类具有特定的作用。@RestController注解告诉Spring将生成的字符串直接返回给调用者。

#### @EnableAutoConfiguration注解
&nbsp;&nbsp;这个注解告诉 Spring Boot 根据您添加的jar依赖关系来“猜(guess)”你将如何配置Spring。由于spring-boot-starter-web添加了Tomcat和Spring MVC，自动配置将假定您正在开发Web应用程序并相应地配置Spring。

#### main方法
&nbsp;&nbsp;main()方法通过调用run()委托(delegates)给Spring Boot的SpringApplication类。 SpringApplication将引导我们的应用程序，启动Spring，然后启动自动配置的Tomcat Web服务器。 我们需要将A.class作为一个参数传递给run方法来告诉SpringApplication，它是主要的Spring组件。 还传递了args数组以传递命令行参数。
```java
    public static void main(String[] args) {
        SpringApplication.run(A.class, args);
    }
```

#### 查找主应用程序类
&nbsp;&nbsp;通常建议将应用程序主类放到其他类之上的根包(root package)中。@EnableAutoConfiguration注解通常放置在您的主类上，它隐式定义了某些项目的基本“搜索包”。 
&nbsp;&nbsp;使用根包(root package)还可以使用@ComponentScan注释，而不需要指定basePackage属性。 如果您的主类在根包中，也可以使用@SpringBootApplication注释。

&nbsp;&nbsp;这是一个经典的布局：
``` java
com
 +- example
     +- myproject
         +- Application.java
         |
         +- domain
         |   +- Customer.java
         |   +- CustomerRepository.java
         |
         +- service
         |   +- CustomerService.java
         |
         +- web
             +- CustomerController.java
```

#### 禁用指定的自动配置
&nbsp;&nbsp;如果发现正在使用一些不需要的自动配置类，可以使用@EnableAutoConfiguration的exclude属性来禁用它们。
``` java
import org.springframework.boot.autoconfigure.*;
import org.springframework.boot.autoconfigure.jdbc.*;
import org.springframework.context.annotation.*;

@Configuration
@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})
public class MyConfiguration {
}
```

### Spring Beans 和 依赖注入
&nbsp;&nbsp;可以自由使用任何标准的Spring Framework技术来定义bean及其依赖注入关系。 为了简单起见，使用@ComponentScan搜索bean，结合@Autowired构造函数(constructor)注入效果很好。
&nbsp;&nbsp;按照上述建议（将应用程序类放在根包(root package)中）构建代码，则可以使用 @ComponentScan而不使用任何参数。 所有应用程序组件（@Component，@Service，@Repository，@Controller等）将自动注册为Spring Bean。

### 使用@SpringBootApplication注解
&nbsp;&nbsp;许多Spring Boot开发人员总是使用@Configuration，@EnableAutoConfiguration和@ComponentScan来标注它们的主类。 由于这些注解经常一起使用，Spring Boot提供了一个方便的@SpringBootApplication注解作为这三个的替代方法。
&nbsp;&nbsp;@SpringBootApplication注解相当于使用@Configuration，@EnableAutoConfiguration和@ComponentScan和他们的默认属性