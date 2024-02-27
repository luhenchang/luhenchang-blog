## 一、项目创建

### 1、常用依赖：

**Language**:可以选择Java或者Kotlin、我这里选择Kotlin。

**Type**:库的依赖方式选择Maven，Gradle

![image-20240226130204259](/Users/wangfeiwangfei/Library/Application Support/typora-user-images/image-20240226130204259.png)

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

数据库选择，如果选择了MySql需要电脑端进行MySql服务的安装。如果选择了PostgreSql就需要安装PostgreSql服务。然后通过navicate进行创建数据库。

例如在application.yml里面进行服务器、springBoot、mybatis等的配置。

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

#### **spring相关配置**

```xml
spring:#表明下面的配置是关于Spring框架的设置。
  jpa:#这表明下面的配置是关于Java Persistence API (JPA) 的设置。
    database: postgresql#这一行设置了JPA使用的数据库类型为PostgreSQL。
    hibernate:#下面的配置是关于Hibernate的设置，Hibernate是一个流行的对象关系映射工具。
      ddl-auto: update#设置了Hibernate在启动时更新数据库模式，它会自动更新数据库结构以匹配实体类的更改，这在开发阶段很方便。
      naming:#这表明下面的配置是关于命名策略的设置。
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

```
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

[MyBatis-Plus](https://baomidou.com/)

https://baomidou.com/pages/56bac0/#configlocation

## 二、架构分层

## 三、关联数据库

## 四、编写简单接口







