---
title: SpringBoot入门
date: 2022-09-11 17:22:45
tags: [SpringBoot]
---

<meta name="referrer" content="no-referrer"/>

# Spring 与 SpringBoot

## Spring能做什么

### Spring的能力

![image-20221123164723364](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221123164723364.png)

### Spring的生态

- 详情可见：**https://spring.io/projects/spring-boot**
- 覆盖了：web开发、数据访问、安全控制、分布式、消息服务、移动开发、批处理......

### Spring5重大升级

#### 响应式编程

![image-20221123165218680](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221123165218680.png)

#### 内部源码设计

- 基于Java8的一些新特性，如：接口的默认实现，重新设计源码架构等。

## 为什么用SpringBoot

- Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run".即能快速创建出生产级别的Spring应用。

### SpringBoot的优点

- Create stand-alone Spring applications 创建独立Spring应用
- Embed Tomcat, Jetty or Undertow directly (no need to deploy WAR files) 内嵌web服务器
- Provide opinionated 'starter' dependencies to simplify your build configuration 自动starter依赖，简化构建配置
- Automatically configure Spring and 3rd party libraries whenever possible 自动配置Spring以及第三方功能
- Provide production-ready features such as metrics, health checks, and externalized configuration 提供生产级别的监控、健康检查及外部化配置
- Absolutely no code generation and no requirement for XML configuration 无代码生成、无需编写XML
- SpringBoot是整合Spring技术栈的一站式框架
- SpringBoot是简化Spring技术栈的快速开发脚手架

### SpringBoot的缺点

- 人称版本帝，迭代快，需要时刻关注变化。
- 封装太深，内部原理复杂，不容易精通。

## 时代背景

### 微服务

- [James Lewis and Martin Fowler (2014)](https://martinfowler.com/articles/microservices.html)  提出微服务完整概念。https://martinfowler.com/microservices/

  > In short, the **microservice architectural style** is an approach to developing a single application as a **suite of small services**, each **running in its own process** and communicating with **lightweight** mechanisms, often an **HTTP** resource API. These services are **built around business capabilities** and **independently deployable** by fully **automated deployment** machinery. There is a **bare minimum of centralized management** of these services, which may be **written in different programming languages** and use different data storage technologies.-- [James Lewis and Martin Fowler (2014)](https://martinfowler.com/articles/microservices.html)

- 微服务是一种架构风格
- 一个应用拆分为一组小型服务
- 每个服务运行在自己的进程内，也就是可独立部署和升级
- 服务之间使用轻量级HTTP交互
- 服务围绕业务功能拆分
- 可以由全自动部署机制独立部署
- 去中心化，服务自治。服务可以使用不同的语言、不同的存储技术

### 分布式

- 分布式系统是**多个服务器通过网络互联而构建的松耦合系统**：![image-20221123170745193](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221123170745193.png)

#### 分布式的困难

- 远程调用
- 服务发现
- 负载均衡
- 服务容错
- 配置管理
- 服务监控
- 链路追踪
- 日志管理
- 任务调度
- ......

#### 分布式的解决

- SpringBoot+SpringCloud

  ![image-20221123190035913](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221123190035913.png)

### 云原生

- 原生应用如何上云。-Cloud Native

#### 上云的困难

- 服务自愈
- 弹性伸缩
- 服务隔离
- 自动化部署
- 灰度发布
- 流量治理
- ......

## 如何学习SpringBoot

### 官网文档架构

![image-20221123190342774](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221123190342774.png)

![image-20221123190358243](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221123190358243.png)

- 查看版本新特性：https://github.com/spring-projects/spring-boot/wiki#release-notes

  ![image-20221123190453858](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221123190453858.png)

# SpringBoot2入门

## 系统要求

- Java 8 & 兼容java14 .
- Maven 3.3+
- idea 2019.1.2

## maven配置文件设置

```xml
<mirrors>
    <mirror>
      <id>nexus-aliyun</id>
      <mirrorOf>central</mirrorOf>
      <name>Nexus aliyun</name>
      <url>http://maven.aliyun.com/nexus/content/groups/public</url>
    </mirror>
</mirrors>

<profiles>
    <profile>
         <id>jdk-1.8</id>
         <activation>
           <activeByDefault>true</activeByDefault>
           <jdk>1.8</jdk>
         </activation>
         <properties>
           <maven.compiler.source>1.8</maven.compiler.source>
           <maven.compiler.target>1.8</maven.compiler.target>
           <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>
         </properties>
    </profile>
</profiles>
```

## HelloWorld

- 需求：浏览发送/hello请求，响应Hello，Spring Boot 2

### 创建maven工程

- 在IDEA中创建maven工程

### 引入依赖

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.3.4.RELEASE</version>
</parent>


<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

</dependencies>
```

### 创建主程序

```java
/**
 * 主程序类
 * @SpringBootApplication：这是一个SpringBoot应用
 */
@SpringBootApplication
public class MainApplication {

    public static void main(String[] args) {
        SpringApplication.run(MainApplication.class,args);
    }
}
```

### 编写业务

```java
@RestController
public class HelloController {
    @RequestMapping("/hello")
    public String handle01(){
        return "Hello, Spring Boot 2!";
    }
}
```

### 测试

- 直接运行main方法

### 简化配置

- 可以将配置写到自己在Resources中创建的application.properties中，写在其中的配置对整个应用都生效：

  ```properties
  server.port=8888
  ```

### 简化部署

- 可以在项目的pom文件中添加以下插件，这样把项目打成jar包后直接在目标服务器执行即可。

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

# 了解自动配置原理

## SpringBoot特点

### 依赖管理

- 父项目做依赖管理（话说这个不是maven工程的特点嘛）

  ```xml
  依赖管理
  <parent>
  	<groupId>org.springframework.boot</groupId>
  	<artifactId>spring-boot-starter-parent</artifactId>
  	<version>2.3.4.RELEASE</version>
  </parent>
  
  他的父项目
  <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-dependencies</artifactId>
      <version>2.3.4.RELEASE</version>
  </parent>
  
  几乎声明了所有开发中常用的依赖的版本号,自动版本仲裁机制
  ```

- 开发导入starter场景启动器：

  ```xml
  1、见到很多 spring-boot-starter-* ： *就某种场景
  2、只要引入starter，这个场景的所有常规需要的依赖我们都自动引入
  3、SpringBoot所有支持的场景
  https://docs.spring.io/spring-boot/docs/current/reference/html/using-spring-boot.html#using-boot-starter
  4、见到的  *-spring-boot-starter： 第三方为我们提供的简化开发的场景启动器。
  5、所有场景启动器最底层的依赖
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter</artifactId>
      <version>2.3.4.RELEASE</version>
      <scope>compile</scope>
  </dependency>
  ```

- 无需关注版本号，自动版本仲裁：

  ```xml
  1、引入依赖默认都可以不写版本
  2、引入非版本仲裁的jar，要写版本号。
  ```

- 可以修改默认版本号：

  ```xml
  1、查看spring-boot-dependencies里面规定当前依赖的版本 用的 key。
  2、在当前项目里面重写配置
  <properties>
      <mysql.version>5.1.43</mysql.version>
  </properties>
  ```

### 自动配置

- 自动配置好Tomcat：手动引入Tomcat依赖，SpringBoot会帮我们自动配置好Tomcat。

  ```xml
  <dependency>
  	<groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-tomcat</artifactId>
      <version>2.3.4.RELEASE</version>
      <scope>compile</scope>
  </dependency>
  ```

- 自动配置好SpringMVC：

  - 引入SpringMVC全套组件
  - 自动配好SpringMVC常用组件（功能）。

- 自动配好Web常见功能，如：字符编码问题：

  - SpringBoot帮我们配置好了所有web开发的常见场景

- 具有默认的包结构：

  - **主程序所在包及其下面的所有子包里面的组件都会被默认扫描进来**

  - 无需以前的包扫描配置

  - 想要改变扫描路径，可以在主程序的注解中添加参数显式指定@SpringBootApplication(scanBasePackages=**"路径"**)或者使用@ComponentScan(**"路径"**)注解指定扫描路径

    ```java
    @SpringBootApplication
    等同于
    @SpringBootConfiguration
    @EnableAutoConfiguration
    @ComponentScan("默认路径")
    ```

- 各种配置拥有默认值：

  - **默认配置最终都是映射到某个类上**，如：MultipartProperties
  - **配置文件的值最终会绑定每个类上，这个类会在容器中创建对象**

- 按需加载所有自动配置项：

  - 非常多的starter
  - **引入了哪些场景这个场景的自动配置才会开启**
  - SpringBoot所有的**自动配置功能都在 spring-boot-autoconfigure 包里面**

- 还有很多自动配置方面的特性，这里就不继续往下写了。

## 容器功能

### 组件添加

#### @Configuration

- **被这个注解修饰的类会被springboot识别为配置类，在其中做操作相当于在配置文件中做配置**。

- 这个注解可以在**Full模式和Lite模式**中选其一使用。

- 配置类组件之间无依赖关系用Lite模式加速容器启动过程，减少判断；配置类组件之间有依赖关系，方法会被调用得到之前单实例组件，用Full模式。

  ```java
  #############################Configuration使用示例######################################################
  /**
   * 1、配置类里面使用@Bean标注在方法上给容器注册组件，默认也是单实例的
   * 2、配置类本身也是组件
   * 3、proxyBeanMethods：代理bean的方法
   *      Full(proxyBeanMethods = true)、【保证每个@Bean方法被调用多少次返回的组件都是单实例的】
   *      Lite(proxyBeanMethods = false)【每个@Bean方法被调用多少次返回的组件都是新创建的】
   *      组件依赖必须使用Full模式默认。其他默认是否Lite模式
   *
   *
   *
   */
  @Configuration(proxyBeanMethods = false) //告诉SpringBoot这是一个配置类 == 配置文件，这是使用的Lite模式，不使用代理检查Bean是否已经存在，直接用到的时候new。
  public class MyConfig {
  
      /**
       * Full:外部无论对配置类中的这个组件注册方法调用多少次获取的都是之前注册容器中的单实例对象
       * @return
       */
      @Bean //给容器中添加组件。以方法名作为组件的id。返回类型就是组件类型。返回的值，就是组件在容器中的实例
      public User user01(){
          User zhangsan = new User("zhangsan", 18);
          //user组件依赖了Pet组件
          zhangsan.setPet(tomcatPet());
          return zhangsan;
      }
  
      @Bean("tom")
      public Pet tomcatPet(){
          return new Pet("tomcat");
      }
  }
  
  
  ################################@Configuration测试代码如下########################################
  @SpringBootConfiguration
  @EnableAutoConfiguration
  @ComponentScan("com.atguigu.boot")
  public class MainApplication {
      public static void main(String[] args) {
          //1、返回我们IOC容器
          ConfigurableApplicationContext run = SpringApplication.run(MainApplication.class, args);
  
          //2、查看容器里面的组件
          String[] names = run.getBeanDefinitionNames();
          for (String name : names) {
              System.out.println(name);
          }
  
          //3、从容器中获取组件
  
          Pet tom01 = run.getBean("tom", Pet.class);
  
          Pet tom02 = run.getBean("tom", Pet.class);
  
          System.out.println("组件："+(tom01 == tom02));
  
  
          //4、com.atguigu.boot.config.MyConfig$$EnhancerBySpringCGLIB$$51f1e1ca@1654a892
          MyConfig bean = run.getBean(MyConfig.class);
          System.out.println(bean);
  
          //如果@Configuration(proxyBeanMethods = true)代理对象调用方法。SpringBoot总会检查这个组件是否在容器中有。
          //保持组件单实例
          User user = bean.user01();
          User user1 = bean.user01();
          System.out.println(user == user1);
  
  
          User user01 = run.getBean("user01", User.class);
          Pet tom = run.getBean("tom", Pet.class);
  
          System.out.println("用户的宠物："+(user01.getPet() == tom));
      }
  }
  ```

#### @Bean、@Component、@Controller、@Service、@Repository

- 这些都是**用来向spring容器中注册组件的注解**，他们的作用基本相同，但是为了体现我们项目的层次规范，我们用不同的注解来注册不同层的组件。
- **@Bean**：@Bean 需要在配置类中使用，即类上需要加上@Component或者@Configuration注解， 通常加上@Configuration。这个注解用来修饰方法，表示一个方法实例化、配置或者初始化一个Spring ioc容器管理的新对象。
- **@Component**：用来修饰类，表示被注解的类会被ComponentScan扫描，然后被注册到spring ioc容器中。
- **@Controller**：和@Component效果相同，只不过我们通常用它来修饰控制器类或者表现层组件。
- **@Service**：和@Component效果相同，只不过我们通常用它来修饰业务层的组件。
- **@Repository**：和@Component效果相同，只不过我们通常用它来修饰持久层的组件。

#### @ComponentScan、@Import

