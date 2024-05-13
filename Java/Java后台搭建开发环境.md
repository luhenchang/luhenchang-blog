## 一、项目创建

### 1、常用依赖：

**Language**:可以选择Java或者Kotlin、我这里选择Kotlin。

**Type**:库的依赖方式选择Maven，Gradle

![image-20240226130204259](https://gitee.com/LuHenChang/blog_pic/raw/master/image-20240226130204259.png)

然后选择自己常用的依赖库：常见依赖列举了下面6个。当然也可以在项目新建完成之后在pom.xml里面进行添加依赖配置。

![image-20240226215856855](/Users/wangfeiwangfei/Library/Application Support/typora-user-images/image-20240226215856855.png)

**Dependencies**：常用的依赖库以及作用
**1、Spring Web：**Spring Web框架是一个开源的Java框架，它被广泛用于构建Web应用程序和RESTful服务。它基于经典的Spring框架，提供了一组功能强大且灵活的工具和类，用于简化Web应用程序的开发。特点：MVC模式、请求处理、视图解析、数据验证和绑定、RESTful支持、安全性。
**2、Spring Boot Devtolls：**[热部署](https://so.csdn.net/so/search?q=热部署&spm=1001.2101.3001.7020)是对修改的类和配置文件进行重新加载，所以在重新加载的过程中会看到项目启动的过程，其本质上只是对修改类和配置文件的重新加载，所以速度极快。
**3、Lombok：**在项目中使用Lombok可以减少很多重复代码的书写。比如说getter/setter/toString等方法的编写。

>@Getter/@Setter: 作用类上，生成所有成员变量的getter/setter方法。
>@ToString : 作用于类，覆盖默认的toString()方法 ,可以通过of属性限定显示某些字段，通过exclude属性排除某些字段。
>@AllArgsConstructor：生成全参构造器。
>@NoArgsConstructor：生成无参构造器。
>@Data: 该注解使用在类上，该注解会提供 getter 、 setter 、 equals 、 hashCode 、
>toString 方法。

**4、Thymeleaf：**是一个Java库。它是一个XML/XHTML/HTML5模板引擎,能够应用于转换模板文件,以显示您的应用程序产生的数据和文本。
**5、MySQL Driver：**使用MySQL数据库驱动包当然也可以选择
**6、MyBatis Framework：**支持自定义SQL、存储过程和高级映射。MyBatis 使用 XML 描述符或注解将对象与存储过程或 SQL 语句耦合。

点击继续创建完成项目，创建项目完成。进行数据库和数据表的创建。

### 2、创建数据库

数据库可根据项目需要，自行选择，例如MySQL、PostgreSQL、Oracle等.....
MySQL需要电脑端进行MySql服务的安装。
PostgreSQL需要PostgreSql服务的安装。
然后通过navicate进行创建数据库。

### 3、yml配置

#### **服务相关配置：**

```xml
server:
  port: 8080
  address: localhost #本地
  #address: 116.62.149.237  #116.62.149.237这个是阿里云端地址
```

> 1. `server:` - 这是一个标识符，表明下面的配置是关于服务器的设置。
> 2. `port: 8080` - 这一行设置了服务器的端口号为8080，意味着应用程序将会在8080端口监听HTTP请求。
> 3. `address: localhost` - 这一行设置了服务器的地址为本地主机，也就是localhost，表示应用程序将只接受来自本地的连接。
> 4. `#address: 116.62.149.237` 设置服务器的地址为116.62.149.237，可以是阿里云的一个IP地址或者腾讯等IP地址。

#### **Spring相关配置**

 配置可以参考 [**Spring官方配置**](https://spring.io/guides/gs/accessing-data-mysql)。

```yaml
#表明下面的配置是关于Spring框架的设置。
spring:
  #这表明下面的配置是关于Java Persistence API (JPA) 的设置。 
  jpa:
    #这一行设置了JPA使用的数据库类型为PostgreSQL。
    database: postgresql
    #下面的配置是关于Hibernate的设置，Hibernate是一个流行的对象关系映射工具。
    hibernate:
    #设置了Hibernate在启动时更新数据库模式，它会自动更新数据库结构以匹配实体类的更改，这在开发阶段很方便。
      ddl-auto: update
      #这表明下面的配置是关于命名策略的设置。
      naming:
        #physical-strategy: org.hibernate.cfg.DefaultNamingStrategy#过期
        implicit-strategy: org.springframework.boot.orm.jpa.hibernate.SpringImplicitNamingStrategy
        physical-strategy: org.springframework.boot.orm.jpa.hibernate.SpringPhysicalNamingStrategy


  #Public Key Retrieval is not allowed
  datasource:
    url: jdbc:postgresql://localhost:5432/java_study?useUnicode=true&characterEncoding=utf-8&useSSL=false&allowPublicKeyRetrieval=true
    username: postgres
    password: 123456
    #在升级到commons-dbcp2之后过期了
    #initialSize: 5
    #minIdle: 5
    #maxActive: 20
    #maxWait: 60000
    #timeBetweenEvictionRunsMillis: 60000
    #minEvictableIdleTimeMillis: 300000
    dbcp2:
      initial-size: 5
      max-total: 20
      min-idle: 5
      max-wait-millis: 60000
      time-between-eviction-runs-millis: 60000
      min-evictable-idle-time-millis: 300000
       #MyWebAppConfiguration进行了配置，所以不需要在此进行配置，且在此配置失败，可能不同版本配置问题。
        #web:
        #resources:
      #static-locations:
      #[ classpath:/statics/]
```

> 这个配置文件涉及到数据源（DataSource）的配置，主要用于连接数据库，以下是每一行的解释和作用：
>
> 1. `datasource:` - 这是一个标识符，表明下面的配置是关于数据源的设置。
>
> 2. `url: jdbc:postgresql://localhost:5432/java_study?useUnicode=true&characterEncoding=utf-8&useSSL=false&allowPublicKeyRetrieval=true` - 这一行设置了数据库的连接URL。其中：
>    - `jdbc:postgresql://localhost:5432/java_study` 是连接到 PostgreSQL 数据库的URL，其中 `localhost` 是数据库服务器的主机名，`5432` 是 PostgreSQL 服务器的默认端口，`java_study` 是数据库的名称。
>    - `useUnicode=true&characterEncoding=utf-8&useSSL=false&allowPublicKeyRetrieval=true` 是连接参数，用于指定数据库连接的一些属性，比如使用UTF-8编码、不使用SSL等。
>
> 3. `username: postgres` - 这一行设置了连接数据库的用户名为 `postgres`。
>
> 4. `password: 123456` - 这一行设置了连接数据库的密码为 `123456`。
>
> 5. `dbcp2:` - 这一行表明下面的配置是关于连接池（Apache Commons DBCP2）的设置，连接池用于管理数据库连接的复用和分配。
>
> 6. `initial-size: 5` - 这一行设置了连接池的初始大小为5，即连接池初始化时创建的数据库连接的数量。
>
> 7. `max-total: 20` - 这一行设置了连接池中允许的最大活动连接数为20，即连接池中同时可以活跃的最大连接数。
>
> 8. `min-idle: 5` - 这一行设置了连接池中保持的最小空闲连接数为5，即连接池中保持的最少空闲连接数，当连接池空闲连接数低于这个值时，会创建新的连接。
>
> 9. `max-wait-millis: 60000` - 这一行设置了获取连接的最大等待时间（毫秒），当连接池中没有可用连接且达到最大连接数时，请求连接的线程会等待，直到超过这个时间。
>
> 10. `time-between-eviction-runs-millis: 60000` - 这一行设置了连接池的空闲连接检测周期（毫秒），即连接池定期检测并关闭空闲时间超过一定阈值的连接。
>
> 11. `min-evictable-idle-time-millis: 300000` - 这一行设置了连接池中连接的最小空闲时间（毫秒），即连接池中的连接空闲时间超过这个值时才会被关闭。
>
> 这个配置文件的作用是配置应用程序连接到 PostgreSQL 数据库的数据源，并设置了连接池的一些参数，以便于管理和优化数据库连接的使用。

#### **mybatis配置**

```yaml
mybatis:
  mapper-locations: classpath*:mapper/*.xml #resources下的mapper文件夹目录下的xml
  type-aliases-package: org.example.study.entity #bean所在的目录
  configuration:
    map-underscore-to-camel-case: true
    cache-enabled: false
```

> 这个配置文件涉及到 MyBatis 框架的配置，主要用于配置 MyBatis 的一些参数和设置，以下是每一行的解释和作用：
>
> 1. `mybatis:` - 这是一个标识符，表明下面的配置是关于 MyBatis 框架的设置。
>
> 2. `mapper-locations: classpath*:mapper/*.xml` - 这一行设置了 MyBatis 的 Mapper 文件的位置。`classpath*:mapper/*.xml`表示在类路径下寻找名为 `mapper` 的文件夹中的所有以 `.xml` 结尾的文件作为 MyBatis 的 Mapper 文件。
>
> 3. `type-aliases-package: org.example.study.entity` - 这一行设置了 MyBatis 的类型别名包，即告诉 MyBatis 在指定的包下寻找 Java 类，以便在 MyBatis 的 XML 映射文件中可以直接使用类名，而不需要使用全限定类名。
>
> 4. `configuration:` - 这是 MyBatis 的配置项，用于配置 MyBatis 的一些参数。
>
> 5. `map-underscore-to-camel-case: true` - 这一行设置了是否开启驼峰命名自动映射功能。当设置为 true 时，MyBatis 会自动将数据库字段中的下划线命名转换为 Java 对象的驼峰命名规则，例如：`first_name` 转换为 `firstName`。
>
> 6. `cache-enabled: false` - 这一行设置了是否开启 MyBatis 的缓存功能。当设置为 false 时，MyBatis 将禁用所有的缓存。
>
> 这个配置文件的作用是配置 MyBatis 框架的一些重要参数，包括 Mapper 文件位置、类型别名包、是否开启驼峰命名自动映射以及是否启用缓存等。

#### MyBatis-Plus配置：[MyBatis-Plus](https://baomidou.com/)

Mybatis-plus一般在spring-boot的基础上需要依赖mybatis-plus-boot-starter，如果依赖mybatis-plus会出现application.yml配置文件的mapper-locations无法加载。从而导致BaseMapper.selectList等自带的函数无法被加载问题，且需要注意，如果添加的依赖是mybatis-plus那么，配置文件中就需要写mybatis-plus而不是mybatis，否则会运行时候提示错误。

![image-20240228202025668](/Users/wangfeiwangfei/Library/Application Support/typora-user-images/image-20240228202025668.png)

```
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-boot-starter</artifactId>
    <version>3.5.2</version>
</dependency>
```

mybatis-plus常用的配置如下：

```yaml
mybatis-plus:
  mapper-locations: classpath*:mapper/*.xml #resources下的mapper文件夹目录下的xml
  type-aliases-package: org.example.study.entity #bean所在的目录
  configuration:
    map-underscore-to-camel-case: true
    cache-enabled: false
```

配置application.yml

```yaml
server:
  port: 8080
  address: localhost #本地
  #address: 116.62.149.237  #116.62.149.237这个是阿里云端地址
spring:
  jpa:
    database: postgresql
    hibernate:
      ddl-auto: update
      naming:
        #physical-strategy: org.hibernate.cfg.DefaultNamingStrategy#过期
        implicit-strategy: org.springframework.boot.orm.jpa.hibernate.SpringImplicitNamingStrategy
        physical-strategy: org.springframework.boot.orm.jpa.hibernate.SpringPhysicalNamingStrategy


  #Public Key Retrieval is not allowed
  datasource:
    url: jdbc:postgresql://localhost:5432/java_study?useUnicode=true&characterEncoding=utf-8&useSSL=false&allowPublicKeyRetrieval=true
    username: postgres
    password: 123456
    #在升级到commons-dbcp2之后过期了
    #initialSize: 5
    #minIdle: 5
    #maxActive: 20
    #maxWait: 60000
    #timeBetweenEvictionRunsMillis: 60000
    #minEvictableIdleTimeMillis: 300000
    dbcp2:
      initial-size: 5
      max-total: 20
      min-idle: 5
      max-wait-millis: 60000
      time-between-eviction-runs-millis: 60000
      min-evictable-idle-time-millis: 300000
        #MyWebAppConfiguration进行了配置，所以不需要在此进行配置，且在此配置失败，可能是不同版本配置问题。
        #web:
        #resources:
      #static-locations:
      #[ classpath:/statics/]
mybatis-plus:
  mapper-locations: classpath*:mapper/*.xml #resources下的mapper文件夹目录下的xml
  type-aliases-package: org.example.study.entity #bean所在的目录
  configuration:
    map-underscore-to-camel-case: true
    cache-enabled: false


```

## 二、架构分层

在Java项目中可以手写架构分层，在mybatis的基础上是很简单编写的。
常见的分层为：
**mapper：**所在的Java层是和mapper的xml层进行映射的。
**IService：**接口函数的封装。
**impl：**层进行IService接口的实现，对mapper层查询结果数据进行分装处理返回给controller层。
**Controller：**控制层，可以拿到接口实现的实例，通过逻辑判断进行调用实现层的接口到达mapper和db交互。

#### 手写分层结构代码如下：

Resources/mapper/userMapper.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="org.example.study.mapper.UserMapper">
    <insert id="insertUser">
        insert into t_user  (name,age,email) values(#{name},#{age},#{email})
    </insert>


    <select id="getUsers" resultType="org.example.study.entity.User">
        select  * from t_user
        <where>
            <if test="name!=null and name != ''">
                name = #{name}
            </if>
        </where>
    </select>
</mapper>
```

包名/mapper/UserMapper

```java
import org.apache.ibatis.annotations.Param;
import org.example.study.entity.User;
import com.baomidou.mybatisplus.extension.service.IService;

import java.util.List;

/**
 * <p>
 *  服务类
 * </p>
 *
 * @author wangfei
 * @since 2024-02-26
 */
public interface IUserService extends IService<User> {

    List<User> getUsers(@Param("username") String username);
    int insertUsers(@Param("user") User user);
}
```

包名/service/impl

```java
package org.example.study.service.impl;

import org.example.study.entity.Msg;
import org.example.study.mapper.MsgMapper;
import org.example.study.service.IMsgService;
import com.baomidou.mybatisplus.extension.service.impl.ServiceImpl;
import org.springframework.stereotype.Service;

import javax.annotation.Resource;
import java.util.List;

/**
 * <p>
 * 服务实现类
 * </p>
 *
 * @author wang fei
 * @since 2024-02-28
 */
@Service
public class MsgServiceImpl extends ServiceImpl<MsgMapper, Msg> implements IMsgService {
    @Resource
    MsgMapper msgMapper;

    @Override
    public List<Msg> getMsgList(String name, int age) {
        return msgMapper.getMsgList(name, age);
    }
}

```

包名/controller/UserController

```java
package org.example.study.controller;

import com.baomidou.mybatisplus.core.conditions.query.QueryWrapper;
import org.example.study.entity.User;
import org.example.study.service.IUserService;
import org.springframework.web.bind.annotation.*;

import javax.annotation.Resource;
import java.util.Collections;
import java.util.List;

/**
 * <p>
 * 前端控制器
 * </p>
 *
 * @author wangfei
 * @since 2024-02-26
 */
//@Controller view 视图例如jsp页面之类的
//data 纯数据，就用RestController
@RestController
@RequestMapping("/user")
public class UserController {
    @Resource
    private IUserService userService;

    @GetMapping("/getUserList")
    public List<User> getUserList(String name) {
          //如果是mybatis-plus是可以通过IService所提供的下面方法进行简单的单表查询。
          //List<User> list = userService.list();
          //1、插入
          //userService.save(new User());
          //2、查询
          //userService.list(new QueryWrapper<User>().eq("name","zhangsan"));
          // select * from user where name = 'zhangsan'
          //3、更新
          //userService.update(new User(),new QueryWrapper<User>().eq("name","zhangsan"));
          //4、删除
          //userService.remove(new QueryWrapper<User>().eq("name","zhangsan"))
           return userService.getUsers(name);
    }

    @PostMapping("insert")
    public Integer insert(@RequestBody User user) {
       if (user!=null){
           return userService.insertUsers(user);
       }
       return 0;
    }
}
```

#### 通过[MyBatis-Plus代码生成器](https://baomidou.com/pages/981406/#%E6%95%B0%E6%8D%AE%E5%BA%93%E9%85%8D%E7%BD%AE-datasourceconfig)生成架构模版

对于新旧版本都有案例，如下是我用的最新版本生成器工具。只需要修改表名称即可，当然你也可以自己分装一个终端输入的表名的好用点的工具。

```kotlin
package org.example.study.utils

import com.baomidou.mybatisplus.generator.FastAutoGenerator
import com.baomidou.mybatisplus.generator.config.*
import com.baomidou.mybatisplus.generator.engine.FreemarkerTemplateEngine
import java.util.*

object GenerationUtils {
    @JvmStatic
    fun main(args: Array<String>) {
        FastAutoGenerator.create("jdbc:postgresql://127.0.0.1:5432/java_study", "postgres", "123456")
            .globalConfig { builder: GlobalConfig.Builder ->
                builder.author("wang fei") // 设置作者
                    .enableSwagger() // 开启 swagger 模式
                    .outputDir(System.getProperty("user.dir") + "/src/main/java") // 指定输出目录
            }
            .packageConfig { builder: PackageConfig.Builder ->
                builder.parent("org.example.study") // 设置父包名
                    //.moduleName("system") // 设置父包模块名
                    .pathInfo(
                        Collections.singletonMap(
                            OutputFile.xml,
                            "/Users/wangfeiwangfei/wangfei/Java/JavaStudy/src/main/resources/mapper/"
                        )
                    ) // 设置mapperXml生成路径
            }
            .strategyConfig { builder: StrategyConfig.Builder ->
                builder.addInclude("msg") // 设置需要生成的表名
                    .addTablePrefix("t_", "c_") // 设置过滤表前缀
            }
            .templateEngine(FreemarkerTemplateEngine()) // 使用Freemarker引擎模板，默认的是Velocity引擎模板
            .execute()
    }
}
```

执行之后，会自动在不同的目录下生成对应的文件。提高了效率，告别了手写。

## 三、关联数据库-增删改查

常见的可以直接和数据库操作的几个位置。

#### Mybatisplus/IService：

#### **Mybatisplus/BaseMapper：**

#### Mapper.xml：

## 四、编写简单接口

## 五、常见错误

### 1、org.thymeleaf.exceptions.TemplateInputException:

```java
@Controller
@RequestMapping("/msg")
public class MsgController {
    @Resource
    IMsgService iMsgService;
    @GetMapping("/getMsgList")
    public List<Msg> getMsgList(String name, int age){
        return iMsgService.getMsgList(name,age);
    }

}
```

错误如下

```xml
2024-02-28 19:00:26.331 ERROR 3949 --- [0.1-8080-exec-2] o.a.c.c.C.[.[.[/].[dispatcherServlet]    : Servlet.service() for servlet [dispatcherServlet] in context with path [] threw exception [Request processing failed; nested exception is org.thymeleaf.exceptions.TemplateInputException: Error resolving template [msg/getMsgList], template might not exist or might not be accessible by any of the configured Template Resolvers] with root cause

org.thymeleaf.exceptions.TemplateInputException: Error resolving template [msg/getMsgList], template might not exist or might not be accessible by any of the configured Template Resolvers
	at org.thymeleaf.engine.TemplateManager.resolveTemplate(TemplateManager.java:869) ~[thymeleaf-3.0.15.RELEASE.jar:3.0.15.RELEASE]
......
```

[@Controller**](https://m.baidu.com/s?word=@Controller&sa=re_dqa_zy) 和 [@RestController](https://m.baidu.com/s?word=@RestController&sa=re_dqa_zy) 的区别主要在于它们的设计目的和使用场景：

1. 共同点：两者都用于指示 [Spring](https://m.baidu.com/s?word=Spring&sa=re_dqa_zy) 应用程序中某个类是否能够处理 [HTTP**](https://m.baidu.com/s?word=HTTP&sa=re_dqa_zy) 请求。

2. 不同点：

   @Controller 主要用于 Spring MVC 架构下的控制器类。它允许开发者在其方法中直接返回 [JSP**](https://m.baidu.com/s?word=JSP&sa=re_dqa_zy) 或 [HTML](https://m.baidu.com/s?word=HTML&sa=re_dqa_zy) 等视图页面。当使用 `@RequestMapping` 注解时，这些视图可以被映射到不同的 URI 上，从而实现动态路由功能。        @RestController 是为了支持前后端分离而设计的。它的设计理念是在不需要视图的情况下，直接将模型对象以 JSON 或 XML 等格式返回给客户端。这样做的优势是可以减少服务器端的负担，提高响应速度。然而，由于使用了 `@RestController`，可能会导致配置的视图解析器（如 `InternalResourceViewResolver`）不起作用，因此Controller层的方法只能返回 `return` 里定义的内容。

总结来说，如果你希望你的控制器类既能处理视图也能处理模型对象并将其作为响应发送给客户端，那么你应该使用 `@Controller`。如果你的应用是基于 RESTful API 设计，并且希望简化服务器的职责，避免不必要的视图渲染，那么你应该选择 `@RestController`。

解决方案：RestController替换Controller。或者在接口函数上用@ResponseBody进行修饰。

### 2、com.mysql.cj.jdbc.exceptions.CommunicationsException

问题分析:

> CommunicationsException
>
> 主要表明Java应用无法建立与MyS数据库的连接。这种情况可能是由多种因素造成的，包括网络问题、数据库配置错误、服务器不可达等。
>
> 出现问题的场景
> 1、应用程序尝试连接到数据库时。
> 2、长时间运行的应用因为网络波动或数据库服务器重启而失去与数据库的连接。
> 3、数据库连接超时。
> 4、服务应为电脑重启而关闭MySql服务。

```
com.mysql.cj.jdbc.exceptions.CommunicationsException: Communications link failure

The last packet sent successfully to the server was 0 milliseconds ago. The driver has not received any packets from the server.
	at com.mysql.cj.jdbc.exceptions.SQLError.createCommunicationsException(SQLError.java:172) ~[mysql-connector-java-8.0.11.jar:8.0.11]
	at com.mysql.cj.jdbc.exceptions.SQLExceptionsMapping.translateException(SQLExceptionsMapping.java:64) ~[mysql-connector-java-8.0.11.jar:8.0.11]
```

解决方案：从新启动MySql服务。

```sql
#macOs命令如下
sudo mysql.server start
```

### 3、端口占用

Java启动程序提示端口占用。解决方案：停止掉所占用的端口。
 sudo lsof -i :8080 
![image-20240229191503501](/Users/wangfeiwangfei/Library/Application Support/typora-user-images/image-20240229191503501.png)

通过进程Id进行关闭端口暂用。

![image-20240229191615248](/Users/wangfeiwangfei/Library/Application Support/typora-user-images/image-20240229191615248.png)





ST_GeometryFromText(text,SRID)
