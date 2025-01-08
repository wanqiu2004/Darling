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

