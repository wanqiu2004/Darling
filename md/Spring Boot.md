# 来瞧瞧Spring Boot有什么功能吧

**用来创建可独立运行，适合生产环境，基于Spring的程序**
提出了“约定优于配置”的设计理念

使用 Maven 安装 Spring Boot
```
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>3.4.1</version>
</parent>

<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

Spring Boot CLI（命令行工具）是一款可以快速构建 Spring 原型应用的工具。
使用 java -jar 命令直接运行 .jar 文件



































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































v
## Spring Boot 让基于 Spring 的独立、生产级应用程序创建变得轻而易举,只需“运行即可”。

对 Spring 平台及第三方库采取了“约定优于配置”的观点，使您可以以最小的精力快速上手。大多数 Spring Boot 应用只需最少的 Spring 配置。


创建独立的 Spring 应用程序
直接嵌入 Tomcat、Jetty 或 Undertow（无需部署 WAR 文件）
提供“约定优于配置”的依赖项（Starter），简化构建配置
在可能的情况下自动配置 Spring 和第三方库
提供生产就绪的功能，如指标监控、健康检查和外部化配置
绝无代码生成，也无需 XML 配置


Spring initializr[项目地址](https://github.com/spring-io/initializr)

```
快速开始：
[start.spring.io](https://start.spring.io/)
添加Spring Web依赖

添加代码
将构建一个经典的 “Hello World!” 端点，任何浏览器都可以连接到它。您甚至可以告诉它您的名字，它将以更友好的方式响应。
推荐使用 BellSoft 的 Liberica JDK 版本 17。
找到 src/main/java/com/example/demo 文件夹中的 DemoApplication.java 文件。现在将以下代码方法和注解添加到文件中：


package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@SpringBootApplication
@RestController
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

    @GetMapping("/hello")
    public String hello(@RequestParam(value = "name", defaultValue = "World") String name) {
        return String.format("Hello %s", name);
    }
}


hello() 方法接收一个名为 name 的字符串参数，并将其与代码中的 "Hello" 组合。如果在请求中设置 name 为 "Amy"，响应将是 “Hello Amy”。
@RestController 注解告诉 Spring，此代码定义了一个可以通过 Web 访问的端点。
@GetMapping("/hello") 注解告诉 Spring，将 hello() 方法用于响应访问 http://localhost:8080/hello 地址的请求。
@RequestParam 注解告诉 Spring 期望请求中有一个 name 值，如果未提供，则默认为 "World"。


maven spring-boot:run
```



---------------------------------------------------------------------------------------



























**构建一个 RESTful Web 服务**
将创建一个服务，它将接受位于 http://localhost:8080/greeting 的 HTTP GET 请求。
还可以通过查询字符串中的可选参数 name 自定义问候内容，http://localhost:8080/greeting?name=User


它会以 JSON 格式返回一个问候信息：
{"id":1,"content":"Hello, World!"} or {"id":1,"content":"Hello, User!"}


- **从 Spring Initializr 开始**
- **通过 Git 克隆：git clone https://github.com/spring-guides/gs-rest-service.git**


从Spring Initializr开始
GET 请求应返回 200 OK 状态，并在响应体中返回以 JSON 表示的问候语。例如：
{
    "id": 1,
    "content": "Hello, World!"
}

id 是问候语的唯一标识符，content 是问候语的文本表示。

为了建模问候语的表示，请创建一个 Java 记录类来包含 id 和 content 数据。如下所示：
文件路径： src/main/java/com/example/restservice/Greeting.java
```
package com.example.restservice;
public record Greeting(long id, String content) { }
```


在 Spring 构建 RESTful Web 服务的方式中，HTTP 请求由控制器处理。这些组件通过 @RestController 注解标识。以下代码展示一个控制器 GreetingController（路径：src/main/java/com/example/restservice/GreetingController.java），它通过返回一个新的 Greeting 类实例来处理针对 /greeting 的 GET 请求：

package com.example.restservice;

import java.util.concurrent.atomic.AtomicLong;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class GreetingController {

    private static final String template = "Hello, %s!";
    private final AtomicLong counter = new AtomicLong();

    @GetMapping("/greeting")
    public Greeting greeting(@RequestParam(value = "name", defaultValue = "World") String name) {
        return new Greeting(counter.incrementAndGet(), String.format(template, name));
    }
}


1. HTTP 请求映射
@GetMapping 注解将针对 /greeting 的 HTTP GET 请求映射到 greeting() 方法。
对于其他 HTTP 方法（如 POST），可以使用相应的注解，例如 @PostMapping。
所有这些注解都继承自 @RequestMapping，也可以直接使用 @RequestMapping(method=GET) 作为 GET 请求的等价写法。
2. 查询参数绑定
@RequestParam 将查询字符串参数 name 的值绑定到 greeting() 方法的 name 参数中。
如果请求中缺少 name 参数，则使用默认值 "World"。
3. 方法实现逻辑
方法体创建并返回一个新的 Greeting 对象，其中：
id 属性是通过 counter.incrementAndGet() 获取的递增计数值。
content 属性是基于模板 template 和给定的 name 格式化生成的字符串。
4. RESTful 控制器 vs 传统 MVC 控制器
传统 MVC 控制器依赖视图技术（如 JSP）进行服务器端渲染，将数据渲染为 HTML 返回。
此 RESTful 控制器直接返回一个 Greeting 对象。该对象的数据会直接以 JSON 格式写入到 HTTP 响应体中。
5. 注解功能
@RestController 是一个复合注解，相当于同时使用了 @Controller 和 @ResponseBody。
@Controller 标记该类为一个控制器。
@ResponseBody 表示每个方法的返回值直接作为 HTTP 响应体内容。
6. 自动 JSON 转换
Greeting 对象必须被转换为 JSON 格式。
得益于 Spring 的 HTTP 消息转换器支持，这种转换是自动完成的：
当类路径中存在 Jackson 2 时，Spring 会自动选择 MappingJackson2HttpMessageConverter 将 Greeting 实例转换为 JSON。
因此，开发者无需手动进行 JSON 转换。


Spring Initializr 会为你创建一个应用程序类。在本例中，无需进一步修改此类。以下是应用程序类的代码（位于 src/main/java/com/example/restservice/RestServiceApplication.java）：
package com.example.restservice;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class RestServiceApplication {

    public static void main(String[] args) {
        SpringApplication.run(RestServiceApplication.class, args);
    }
}

@SpringBootApplication 注解
@SpringBootApplication 是一个便捷注解，它整合了以下功能：

@Configuration：将该类标记为应用程序上下文的 Bean 定义源。
@EnableAutoConfiguration：
告诉 Spring Boot 根据类路径设置、其他 Bean 和各种属性配置自动添加 Bean。
例如，当类路径中存在 spring-webmvc 时，该注解会将应用标记为 Web 应用，并启用关键行为，如设置 DispatcherServlet。
@ComponentScan：
告诉 Spring 在 com/example 包中查找其他组件、配置和服务，从而能够自动发现控制器。
main() 方法
使用 Spring Boot 的 SpringApplication.run() 方法启动应用程序。
你可能注意到，整个过程中没有一行 XML 配置代码，也没有 web.xml 文件。
该 Web 应用程序完全使用纯 Java 编写，无需处理任何底层配置或基础设施。

./mvnw clean package
服务启动后，访问 http://localhost:8080/greeting。你应看到以下 JSON 响应：

```






---
# Spring Boot



































































# Spring 


## 啊啊啊，该使用什么版本的JDK
从 Spring Framework 6.0 开始，Spring 要求使用 Java 17 或更高版本。



## Spring 与 EE 是你死我活嘛？
Spring 于 2003 年诞生，旨在应对早期 J2EE 规范的复杂性。
虽然有人认为Jakarta EE 与 Spring 竞争，但它们实际上是互补的。

Spring 兼容精心挑选EE产品如：

- Servlet API（JSR 340）
- WebSocket API（JSR 356）
- 并发工具（JSR 236）
- JSON 绑定 API（JSR 367）
- Bean 验证（JSR 303）
- JPA（JSR 338）
- JMS（JSR 914）


自 Spring Framework 6.0 起，Spring 已经升级至 Jakarta EE 9 版本
并基于 Jakarta 命名空间，而不是传统的 javax 包。
Spring 已为 EE 9 作为最低支持，并已经支持 EE 10。

Spring Framework 6.0 完全兼容 Tomcat 10.1、Jetty 11 和 Undertow 2.3 作为 Web 服务器，
同时也与 Hibernate ORM 6.1 兼容。

有关完整的 Spring 项目列表，请访问 spring.io/projects。



## 太棒啦，那么Spring 的核心是什么？
1. 控制反转（Inversion of Control, IoC）容器
容器通过依赖注入（Dependency Injection, DI）的方式管理对象的生命周期和依赖关系

2. 面向切面编程（Aspect-Oriented Programming, AOP）技术
Spring 提供了自己的 AOP 框架，可以高效地满足 Java 企业级编程中 80% 的 AOP 需求。

Spring 的 AOP 框架支持动态代理和字节码生成，可以灵活地在运行时为目标类添加切面逻辑。

Spring 还支持与 AspectJ 集成。企业级开发中功能最丰富、最成熟的 AOP 实现之一。
Spring 开发者可以利用其全面的功能集，例如编译时织入和加载时织入，来满足更复杂的 AOP 场景需求。

3. Ahead-of-Time (AOT) Processing
Spring 提供 AOT 处理，这种技术通常用于结合 GraalVM 的原生镜像部署场景。



## 简单说说 IoC 容器与 Bean 呗
依赖注入是IoC的一种特殊方式，对象通过参数接受其他对象并使用它们
IoC容器在创建Bean时注入这些依赖
**BeanFactory**提供了这个框架的基本功能，ApplicationContext更加强大

IoC 以 org.springframework.beans 和 org.springframework.context
这两个包为基础，BeanFactory接口可以管理任何对象奥
IoC容器创建的对象是Bean



## 
容器读取配置来获取哪些Bean应该创建，这些Bean分别应该去哪里
可以用一下方式来配置
带注解的类
含工场方法的类
外部xml文件

外部xml是将Bean添加到xml的Beans元素下，然后将文件的路径提供：
ApplicationContext context = new ClassPathXmlApplicationContext("services.xml", "daos.xml");
也可以使用 <import/> 元素将Bean定义从另一个文件或多个文件加载。

大部分情况下，我们无需手动编写代码实例化IoC

通过使用方法 T getBean(String name, Class<T> requiredType)，可以检索到Bean实例。
```
// 创建并配置Bean
ApplicationContext context = new ClassPathXmlApplicationContext("services.xml", "daos.xml");

// 检索已配置的实例
PetStoreService service = context.getBean("petStore", PetStoreService.class);

// 使用已配置的实例
List<String> userList = service.getUsernameList();
```


尽管可以通过 getBean() 方法获取Bean实例，但理想情况下，应用程序代码不应该直接调用它。实际上，应用程序代码应该完全不依赖Spring API。


























