## 我应该如何使用MyBatis？用Maven呢？

要使用 MyBatis， 只需将 mybatis-x.x.x.jar 文件置于类路径（classpath）中即可。

如果使用 Maven 来构建项目，则需将下面的依赖代码置于 pom.xml 文件中：
```
<dependency>
  <groupId>org.mybatis</groupId>
  <artifactId>mybatis</artifactId>
  <version>x.x.x</version>
</dependency>
```

## Maven应用的核心是什么 ？

Maven围绕着它最喜欢的最关心的对象 SqlSessionFactory 玩，SqlSessionFactory的形状取决于SqlSessionFactoryBuilder，它是妈妈，妈妈听钞票xml的，Configuration 

## 天啊天啊，我该如何展示我的钞票？

放在显眼的class路径奥，也可以让银行Resources 的工具类加载奥，InputStream也可以奥，来看看如何让银行出具：
```
String resource = "org/mybatis/example/mybatis-config.xml";
InputStream inputStream = Resources.getResourceAsStream(resource);
SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
```

## 不使用 XML 构建 SqlSessionFactory？这与使用xml有什么区别？

## SqlSessionFactory是如何生出如此SqlSession尤物的？

```
try (SqlSession session = sqlSessionFactory.openSession()) {
  BlogMapper mapper = session.getMapper(BlogMapper.class);
  Blog blog = mapper.selectBlog(101);
}
```

## MyBatis的爱既可以通过 XML 定义，也可以通过注解定义。

xml形式的爱什么样啊？
```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="org.mybatis.example.BlogMapper">
  <select id="selectBlog" resultType="Blog">
    select * from Blog where id = #{id}
  </select>
</mapper>
```

我们似乎写了不少配置，但其实并不多。在一个 XML 映射文件中，可以定义无数个映射语句，这样一来，XML 头部和文档类型声明部分就显得微不足道了。

它在命名空间 “org.mybatis.example.BlogMapper” 中定义了一个名为 “selectBlog” 的映射语句，
这样你就可以用全限定名 “org.mybatis.example.BlogMapper.selectBlog” 来调用映射语句了，

这种方式和用全限定名调用 Java 对象的方法类似。

所以我们可以将爱归为java类


## 阶段性补充

SqlSessionFactoryBuilder妈妈一旦创建了 SqlSessionFactory，就不再需要它劳动啦。保证所有的 XML 解析资源可以被释放给更重要的事情。

SqlSessionFactory一旦被娶就应该一直爱她，没有任何理由丢弃它或重娶一个。

SqlSession都应该有它自己的线程 。SqlSession 的实例不是线程安全的，因此是不能被共享的

换句话说，每次收到 HTTP 请求，就可以打开一个 SqlSession，返回一个响应后，就关闭它。


---


## 让我们来看看你的钞票

1. properties
我们经常要提到的值可以在该子标签使用奥：
可以在典型的 Java 属性文件中配置这些，也可以在 properties 元素的子元素中设置
```
<properties resource="org/mybatis/example/config.properties">
  <property name="username" value="dev_user"/>
  <property name="password" value="F2Fa3!33TYyg"/>
</properties>
```

也可以在 SqlSessionFactoryBuilder.build() 方法中传入属性值。



2. settings
一个配置完整的 settings 元素的示例如下：

<settings>
  <setting name="cacheEnabled" value="true"/>
  <setting name="lazyLoadingEnabled" value="true"/>
  <setting name="multipleResultSetsEnabled" value="true"/>
  <setting name="useColumnLabel" value="true"/>
  <setting name="useGeneratedKeys" value="false"/>
  <setting name="autoMappingBehavior" value="PARTIAL"/>
  <setting name="autoMappingUnknownColumnBehavior" value="WARNING"/>
  <setting name="defaultExecutorType" value="SIMPLE"/>
  <setting name="defaultStatementTimeout" value="25"/>
  <setting name="defaultFetchSize" value="100"/>
  <setting name="safeRowBoundsEnabled" value="false"/>
  <setting name="mapUnderscoreToCamelCase" value="false"/>
  <setting name="localCacheScope" value="SESSION"/>
  <setting name="jdbcTypeForNull" value="OTHER"/>
  <setting name="lazyLoadTriggerMethods" value="equals,clone,hashCode,toString"/>
</settings>



3. typeAliases
仅用于 XML 配置，意在降低冗余的全限定类名书写。
```
<typeAliases>
  <typeAlias alias="Author" type="domain.blog.Author"/>
  <typeAlias alias="Blog" type="domain.blog.Blog"/>
  <typeAlias alias="Comment" type="domain.blog.Comment"/>
  <typeAlias alias="Post" type="domain.blog.Post"/>
  <typeAlias alias="Section" type="domain.blog.Section"/>
  <typeAlias alias="Tag" type="domain.blog.Tag"/>
</typeAliases>
```

通过在 typeAliases 配置中指定一个包名，MyBatis 会扫描该包下的所有 Java 类，并自动为每个类设置一个别名。默认情况下，别名为类名的首字母小写形式。
```
<typeAliases>
  <package name="domain.blog"/>
</typeAliases>
```

这段配置表示 MyBatis 会扫描 domain.blog 包下的所有类，并为每个类自动设置别名。假设 domain.blog 包下有以下 Java 类：
Author
Blog
Post

则它们会自动对应以下别名：
author
blog
post
即，domain.blog.Author 类的别名是 author，domain.blog.Blog 类的别名是 blog，依此类推。



4. TypeHandler
当 MyBatis 从数据库获取数据或将数据插入数据库时，通常需要将数据库中的字段值转换成 Java 对象或反之。
这时，类型处理器就起到了桥梁的作用，将 Java 对象与数据库中存储的值匹配起来。



5. objectFactory
每次 MyBatis 创建结果对象的新实例时，它都会使用一个对象工厂（ObjectFactory）实例来完成实例化工作。 
默认的对象工厂需要做的仅仅是实例化目标类，要么通过默认无参构造方法，要么通过存在的参数映射来调用带有参数的构造方法。 
如果想覆盖对象工厂的默认行为，可以通过创建自己的对象工厂来实现。
即在 MyBatis 执行 SQL 查询时，如何实例化查询结果的 Java 对象。它负责根据查询结果的数据映射，生成一个对应的 Java 对象实例。



6. plugins
MyBatis 的插件机制允许你通过拦截执行过程中某些方法的调用来扩展 MyBatis 的功能。
你可以通过实现 Interceptor 接口，指定要拦截的方法，然后添加自己的逻辑来增强或修改 MyBatis 的默认行为。



7. environments
MyBatis 的 environments 元素允许根据不同的环境（如开发、测试、生产）设置不同的数据库连接和事务管理方式。



8. databaseIdProvider
使用 databaseIdProvider 来区分不同数据库厂商，从而加载适合当前数据库的 SQL 映射语句。



9. mappers
我们需要告诉 MyBatis 到哪里去找到这些语句。 最好的办法是直接告诉 MyBatis 到哪里去找映射文件。 
你可以使用相对于类路径的资源引用，或完全限定资源定位符（包括 file:/// 形式的 URL），或类名和包名等。例如：

<!-- 使用相对于类路径的资源引用 -->
<mappers>
  <mapper resource="org/mybatis/builder/AuthorMapper.xml"/>
  <mapper resource="org/mybatis/builder/BlogMapper.xml"/>
  <mapper resource="org/mybatis/builder/PostMapper.xml"/>
</mappers>
<!-- 使用完全限定资源定位符（URL） -->
<mappers>
  <mapper url="file:///var/mappers/AuthorMapper.xml"/>
  <mapper url="file:///var/mappers/BlogMapper.xml"/>
  <mapper url="file:///var/mappers/PostMapper.xml"/>
</mappers>
<!-- 使用映射器接口实现类的完全限定类名 -->
<mappers>
  <mapper class="org.mybatis.builder.AuthorMapper"/>
  <mapper class="org.mybatis.builder.BlogMapper"/>
  <mapper class="org.mybatis.builder.PostMapper"/>
</mappers>
<!-- 将包内的映射器接口实现全部注册为映射器 -->
<mappers>
  <package name="org.mybatis.builder"/>
</mappers>
这些配置会告诉 MyBatis 去哪里找映射文件



## XML 映射器
SQL 映射文件只有8个顶级元素（按照应被定义的顺序列出）：

cache – 该命名空间的缓存配置。
cache-ref – 引用其它命名空间的缓存配置。
resultMap – 描述如何从数据库结果集中加载对象，是最复杂也是最强大的元素。
sql – 可被其它语句引用的可重用语句块。
insert – 映射插入语句。
update – 映射更新语句。
delete – 映射删除语句。
select – 映射查询语句。


1. select
一个简单查询的 select 元素是非常简单的。比如：
```
<select id="selectPerson" parameterType="int" resultType="hashmap">
  SELECT * FROM PERSON WHERE ID = #{id}
</select>
```

这个语句名为 selectPerson，接受一个 int（或 Integer）类型的参数，并返回一个 HashMap 类型的对象，其中的键是列名，值便是结果行中的对应值。

#{id}这就告诉 MyBatis 创建一个预处理语句（PreparedStatement）参数
用来绑定查询时传递的参数（id）。

完整的是：
```
<select
  id="selectPerson"
  parameterType="int"
  parameterMap="deprecated"
  resultType="hashmap"
  resultMap="personResultMap"
  flushCache="false"
  useCache="true"
  timeout="10"
  fetchSize="256"
  statementType="PREPARED"
  resultSetType="FORWARD_ONLY">
```


2. insert、update 和 delete 元素
这三个元素的完整示例是：
```
<insert
  id="insertAuthor"
  parameterType="domain.blog.Author"
  flushCache="true"
  statementType="PREPARED"
  keyProperty=""
  keyColumn=""
  useGeneratedKeys=""
  timeout="20">

<update
  id="updateAuthor"
  parameterType="domain.blog.Author"
  flushCache="true"
  statementType="PREPARED"
  timeout="20">

<delete
  id="deleteAuthor"
  parameterType="domain.blog.Author"
  flushCache="true"
  statementType="PREPARED"
  timeout="20">
```

使用示例是：
```
<insert id="insertAuthor">
  insert into Author (id,username,password,email,bio)
  values (#{id},#{username},#{password},#{email},#{bio})
</insert>

<update id="updateAuthor">
  update Author set
    username = #{username},
    password = #{password},
    email = #{email},
    bio = #{bio}
  where id = #{id}
</update>

<delete id="deleteAuthor">
  delete from Author where id = #{id}
</delete>
```

如果数据库支持自动生成主键的字段（比如 MySQL 和 SQL Server），
那么可以设置 useGeneratedKeys=”true”，然后再把 keyProperty 设置为目标属性就 OK 了。
```
<insert id="insertAuthor" useGeneratedKeys="true"
    keyProperty="id">
  insert into Author (username,password,email,bio)
  values (#{username},#{password},#{email},#{bio})
</insert>
```

如果数据库还支持多行插入, 也可以传入一个 数组或集合，并返回自动生成的主键。
```
<insert id="insertAuthor" useGeneratedKeys="true"
    keyProperty="id">
  insert into Author (username, password, email, bio) values
  <foreach item="item" collection="list" separator=",">
    (#{item.username}, #{item.password}, #{item.email}, #{item.bio})
  </foreach>
</insert>


3. sql与include
用于定义一个可重用的 SQL 代码片段。这个片段在 MyBatis 配置中可以在其他 SQL 语句中引用。
参数可以静态地（在加载的时候）确定下来，并且可以在不同的 include 元素中定义不同的参数值。
`<sql id="userColumns"> ${alias}.id,${alias}.username,${alias}.password </sql>`

这个 SQL 片段可以在其它语句中使用，例如：
```
<select id="selectUsers" resultType="map">
  select
    <include refid="userColumns"><property name="alias" value="t1"/></include>,
    <include refid="userColumns"><property name="alias" value="t2"/></include>
  from some_table t1
    cross join some_table t2
</select>
```

4. 参数
MyBatis 支持简单的参数映射，即直接在 SQL 语句中使用 #{} 占位符来引用参数。例如：
```
<select id="selectUsers" resultType="User">
  select id, username, password
  from users
  where id = #{id}
</select>
```
命名参数可以被自由命名，并且MyBatis会自动处理参数类型映射。
在MyBatis中，如果传入的是简单数据类型（例如 Integer 或 String），MyBatis会直接使用它们的值作为SQL语句中的参数。

然而，如果传入的是复杂的对象，MyBatis会根据该对象的属性来替代SQL语句中的命名参数。在这个例子中：
```
<insert id="insertUser" parameterType="User">
  insert into users (id, username, password)
  values (#{id}, #{username}, #{password})
</insert>
```
parameterType="User" 表示传入的参数是 User 类型的对象。
在SQL语句中，#{id}、#{username} 和 #{password} 是命名参数，
它们会从传入的 User 对象中查找对应的属性（id、username 和 password）并将它们的值填充到SQL语句中。

#{property,javaType=int,jdbcType=NUMERIC}
表示 property 参数的 Java 类型为 int，而数据库列类型为 NUMERIC。

对于 HashMap 这样的参数对象，MyBatis可能无法自动推断其类型，因此需要显式指定 javaType 和 jdbcType，以确保正确的类型处理。


在MyBatis中，#{} 参数语法 是通过占位符 ? 来设置SQL语句中的参数，这样做非常安全，因为它会自动处理参数的转义，防止SQL注入攻击。

但是，有时我们需要直接在SQL语句中插入一个未经过转义的字符串（例如，动态表名或列名）。在这种情况下，可以使用 ${} 语法。例如：

ORDER BY ${columnName}

${columnName} 会直接替换成你传递给MyBatis的参数值，而不会经过转义或占位符处理。




5. resultMap 
resultMap 元素是 MyBatis 中最重要最强大的元素。它可以让你从 90% 的 JDBC ResultSets 数据提取代码中解放出来，并在一些情形下允许你进行一些 JDBC 不支持的操作。

<select id="selectUsers" resultType="map">
  select id, username, hashedPassword
  from some_table
  where id = #{id}
</select>
上述语句只是简单地将所有的列映射到 HashMap 的键上，这由 resultType 属性指定。

JavaBean 类与 MyBatis 的映射： 该段首先介绍了一个标准的 JavaBean 类 User，它有 3 个属性：id、username 和 hashedPassword。这些属性将与数据库查询结果中的列进行映射。

java
复制代码
public class User {
  private int id;
  private String username;
  private String hashedPassword;
  // getters 和 setters 方法
}
这个 User 类遵循 JavaBean 的规范，包含私有的成员变量以及相应的 getter 和 setter 方法。

MyBatis 中如何使用 JavaBean 映射查询结果： 通过在 MyBatis 映射文件中使用 resultType="com.someapp.model.User"，MyBatis 会自动将查询结果映射到 User 类的对象上。这里，查询中的列 id、username 和 hashedPassword 会自动与 User 类中的属性进行匹配。

xml
复制代码
<select id="selectUsers" resultType="com.someapp.model.User">
  select id, username, hashedPassword
  from some_table
  where id = #{id}
</select>
自动创建 ResultMap： 如果你使用了 resultType 来指定 JavaBean 类，MyBatis 会自动创建一个 ResultMap，不需要手动配置。它会根据列名和 JavaBean 属性名的匹配来自动映射。如果列名与属性名不完全相同，你可以在 SQL 查询中使用列的别名来使它们匹配。

例如，在以下的 SQL 查询中：

xml
复制代码
<select id="selectUsers" resultType="User">
  select
    user_id             as "id",
    user_name           as "userName",
    hashed_password     as "hashedPassword"
  from some_table
  where id = #{id}
</select>
这里，user_id 被重命名为 id，user_name 被重命名为 userName，hashed_password 被重命名为 hashedPassword，这样就可以匹配到 User 类的属性，即使数据库列名与类的属性名不完全一致。

无需显式配置 ResultMap： 这段话的重点是，MyBatis 在这种情况下会自动生成 ResultMap 来处理列与属性之间的映射。你不需要显式地定义 ResultMap，这使得使用 MyBatis 映射 JavaBean 更加简便和高效。






## Java API

我们知道了如何编写MyBatis的配置文件及映射文件啦，我们看看如何在Java里面使用

我们假定目录结构是这样的：
 /data           MyBatis 配置文件在这里，包括映射器类、XML 配置、XML 映射文件。
 /properties     在 XML 配置中出现的属性值在这里。

使用MyBatis的主要的Java接口就是SqlSession，它可以来执行命令，管理事务等等。

SqlSessionFactoryBuilder有5个build方法，通过它们可以创建SqlSessionFactory实例
```
SqlSessionFactory build(InputStream inputStream)
SqlSessionFactory build(InputStream inputStream, String environment)
SqlSessionFactory build(InputStream inputStream, Properties properties)
SqlSessionFactory build(InputStream inputStream, String env, Properties props)
SqlSessionFactory build(Configuration config)
```

第一种方法是最常用的，它接受一个指向 XML 文件（也就是之前讨论的 mybatis-config.xml 文件）的 InputStream 实例。

那么我们如何获取mybatis配置文件的InputStream实例？
```
String resource = "org/mybatis/builder/mybatis-config.xml";
InputStream inputStream = Resources.getResourceAsStream(resource);
SqlSessionFactoryBuilder builder = new SqlSessionFactoryBuilder();
SqlSessionFactory factory = builder.build(inputStream);
```

那么我们得到了SqlSessionFactory，它有6个方法创建SqlSession，我们需要考虑一下：
事务处理：你希望在 session 作用域中使用事务作用域，还是使用自动提交（auto-commit）？
数据库连接：你希望 MyBatis 帮你从已配置的数据源获取连接，还是使用自己提供的连接？
语句执行：你希望 MyBatis 复用 PreparedStatement 和/或批量更新语句（包括插入语句和删除语句）吗？

```
SqlSession openSession()
SqlSession openSession(boolean autoCommit)
SqlSession openSession(Connection connection)
SqlSession openSession(TransactionIsolationLevel level)
SqlSession openSession(ExecutorType execType, TransactionIsolationLevel level)
SqlSession openSession(ExecutorType execType)
SqlSession openSession(ExecutorType execType, boolean autoCommit)
SqlSession openSession(ExecutorType execType, Connection connection)
Configuration getConfiguration();
```

默认的 openSession() 方法没有参数，它会创建具备如下特性的 SqlSession：

事务作用域将会开启（也就是不自动提交）。
将由当前环境配置的 DataSource 实例中获取 Connection 对象。
事务隔离级别将会使用驱动或数据源的默认设置。
预处理语句不会被复用，也不会批量处理更新。


SqlSession 类的方法超过了 20 个，为了方便理解，我们将它们分成几种组别

语句执行方法
这些方法被用来执行定义在映射文件中的 SELECT、INSERT、UPDATE 和 DELETE 语句。
每一方法都接受语句的 ID 以及参数










