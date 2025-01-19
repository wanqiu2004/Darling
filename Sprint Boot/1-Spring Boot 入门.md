Spring Boot 创建可独立运行、适用于生产环境的基于 Spring 的程序。
基于“约定优于配置”的设计理念，能够以最小的精力快速上手。



Spring Boot 3.4.1 至少需要 **Java 17**，并兼容 **Java 23**。
此外，还需要 **Spring Framework 6.2.1** 或更高版本。

| 构建工具 | 版本要求 |
| --- | --- |
| Maven | 3.6.3 或更高 |
| Gradle | Gradle 7.x（7.6.4 或更高）或 8.x（8.4 或更高） |



### 安装 Spring Boot
使用 Maven 安装 Spring Boot

Spring Boot 与 **Apache Maven 3.6.3** 或更高版本兼容。

Spring Boot 的依赖库使用 `org.springframework.boot` 作为 Group ID。
通常，Maven **POM 文件**会从 `spring-boot-starter-parent` 项目继承

此外，Spring Boot 提供了一个可选的 Maven 插件，用于生成可执行的 JAR 文件。

以下是 POM 文件的示例配置：
```xml
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

**Spring Boot CLI**（命令行工具）是一款可以快速构建 Spring 原型应用的工具。



### 开发第一个 Spring Boot 应用程序

使用 Maven，首先需要创建一个 **pom.xml** 文件，这是构建项目的核心配置文件。
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 \
         https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>myproject</artifactId>
    <version>0.0.1-SNAPSHOT</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.4.1</version>
    </parent>

    <dependencies>
        <!-- Spring Boot Web Starter -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>

</project>
```

Spring Boot 提供了多个 **Starter** 来简化开发，自动包含开发特定类型应用所需的依赖项。


 **`spring-boot-starter-parent`**，是一个特殊的 Starter，提供了以下功能：
*   有用的 Maven 默认配置。
*   **依赖管理**，自动管理许多常见库的版本，因此在 `dependencies` 中通常可以省略版本。


在 **`src/main/java/MyApplication.java`** 文件中，添加以下代码：
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@SpringBootApplication
public class MyApplication {

    @RequestMapping("/")
    String home() {
        return "Hello World!";
    }

    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```


恭喜您完成了🎉


由于我们使用了 `spring-boot-starter-parent` POM，已经包含了一个有用的 `run` 目标，
可以直接用来启动应用程序。在项目根目录下运行以下命令：
```bash
mvn spring-boot:run
```



### 解释一下刚才的所作所为
**@RestController 和 @RequestMapping 注解**

1.  **`@RestController`**
    
    *   **作用：**
        *   这是一个 **“标注型注解（stereotype annotation）”**，\
        *   表明当前类是一个 **Web 控制器（Controller）**。
        *   Spring 会将带有此注解的类识别为处理 HTTP 请求的类。
    *   **特性：**
        *   结合了 `@Controller` 和 `@ResponseBody` 的功能：\
        *   方法返回的值直接作为 HTTP 响应体内容，而不是视图名称。
2.  **`@RequestMapping`**
    
    *   **作用：**
        *   提供 “路由信息”，指定哪些路径的 HTTP 请求映射到某个方法处理。
    *   **在代码中：**
        *   `@RequestMapping("/")` 将路径 `/` 的 HTTP 请求映射到 `home()` 方法。
    *   **示例：**  
        当客户端访问 http://localhost:8080/，返回字符串 **"Hello World!"**。
3.  **两者的关系：**
    
    *   `@RestController` 告诉 Spring 框架返回的内容是直接响应，而不是试图渲染视图。
    *   `@RequestMapping` 则定义了路由规则。


**@SpringBootApplication 注解**

1.  **作用：**
    
    *   这是一个 **元注解（meta-annotation）**，组合了以下注解：
        *   **`@SpringBootConfiguration`**：表明这是一个 Spring Boot 配置类。
        *   **`@EnableAutoConfiguration`**：启用自动配置
        *   **`@ComponentScan`**：扫描当前包及其子包中的组件并注册到 Spring 容器。
2.  **重要特性：**
    
    *   **`@EnableAutoConfiguration`**：
        *   这是自动配置的核心。
        *   Spring Boot 根据添加的依赖自动推断并配置应用程序。例如：
            *   如果项目中包含 `spring-boot-starter-web`，\
            *   Spring Boot 会自动配置一个内嵌的 Tomcat 和 Spring MVC。
            *   如果有 `spring-boot-starter-data-jpa`，会配置数据源、JPA 程序等。


1.  **Starters 的作用：**
    
    *   **Starters** 是 Spring Boot 提供的依赖集合，简化了开发中所需的依赖管理。例如：
        *   **`spring-boot-starter-web`**：包含了 Spring MVC、Tomcat 和相关依赖。
        *   **`spring-boot-starter-data-jpa`**：包含 JPA 和 Hibernate 依赖。
2.  **自动配置的独立性：**
    *   自动配置不依赖 Starters，可自由选择其他依赖。



**总结：**

*   **`@RestController` 和 `@RequestMapping`：** 定义路由和处理请求逻辑。
*   **`@SpringBootApplication`：** 启用自动配置和组件扫描，简化项目配置。
*   **Starters**和自动配置方便依赖管理与配置


 `main` 方法。通过调用 Spring Boot 提供的 `SpringApplication` 类的 `run` 方法，
 完成了对 Spring Boot 的启动过程：

*   **SpringApplication 的作用：**  
    `SpringApplication` 引导应用程序，启动 Spring 框架，\
    而 Spring 框架又会启动自动配置的 Tomcat Web 服务器。
*   **方法参数解析：**
    *   将 `MyApplication.class` 作为参数传递给 `run` 方法，\
        用以告诉 SpringApplication 哪个类是主要的 Spring 组件。
    *   `args` 数组也会被传递，以便在运行时处理任何命令行参数。




### 创建可执行 Jar 文件收尾
通过创建一个完全自包含的可执行 Jar 文件来完成示例。

需要在 `pom.xml` 中添加 `spring-boot-maven-plugin` 插件。
在 `dependencies` 部分下方添加以下内容：
```xml
<build>
	<plugins>
		<plugin>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-maven-plugin</artifactId>
		</plugin>
	</plugins>
</build>
```


如果您使用的是 `spring-boot-starter-parent` POM，
已经包含了 `<executions>` 配置，可以自动绑定 `repackage` 目标。
