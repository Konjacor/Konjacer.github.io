---
title: Spring
date: 2022-09-11 17:22:29
tags: [Spring]
---

<meta name="referrer" content="no-referrer"/>

# Spring5框架概述

- Spring是轻量级的开源的JavaEE框架
- Spring可以解决企业应用开发的复杂性
- Spring有两个核心部分：**IOC 和 AOP**
  - IOC：即**控制反转**，把创建对象的过程交给Spring进行管理
  - AOP：即**面向切面编程**，能够不修改源代码而对其功能进行增强
- Spring的特点：
  1. 方便解耦，简化开发
  2. 支持aop编程
  3. 方便程序测试
  4. 方便和其他框架进行整合
  5. 方便进行事务操作
  6. 降低API的开发难度
- 以下的内容选取Spring的版本是5.x

# Spring5入门案例

## 下载Spring5

1. 使用Spring的最新稳定版（Lastest Stable）：

   ![image-20221126191152434](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221126191152434.png)

2. 下载地址：https://repo.spring.io/release/org/springframework/spring/

   ![image-20221126191224742](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221126191224742.png)

## 创建工程

- 打开idea工具，创建普通java工程：

  ![image-20221126191350331](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221126191350331.png)

## 导包

- 导入Spring5相关jar包，主要是导入几个核心的包，以及关于日志的一个包：

  ![image-20221126191551005](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221126191551005.png)

  ![image-20221126191610031](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221126191610031.png)

  ![image-20221126191620655](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221126191620655.png)

## 创建类

- 创建一个普通类，在这个类中创建普通方法：

  ```java
  public class User {
  	public void add() {
  		System.out.println("add......");
  	}
  }
  ```

## 创建Spring配置文件

- 创建Spring配置文件，**在配置文件配置刚才创建的对象，配置之后这个类创建对象的过程就被委托给Spring了，Spring会在需要的时候创建对象**。

  ![image-20221126191949719](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221126191949719.png)

- Spring配置文件使用xml格式：

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
  	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  	xsi:schemaLocation="http://www.springframework.org/schema/beans
  http://www.springframework.org/schema/beans/spring-beans.xsd">
  	<!--配置 User 对象创建-->
  	<bean id="user" class="com.atguigu.spring5.User"></bean>
  </beans>
  ```

## 测试

- 编写测试代码进行测试，注意这里获取刚才创建类的对象是先读取了刚才写的配置文件生成ApplicationContext对象，然后再利用ApplicationContext对象获取对象：

  ```java
  @Test
  public void testAdd() {
  	//1 加载 spring 配置文件
  	ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
  	//2 获取配置创建的对象
  	User user = context.getBean("user", User.class);
  	System.out.println(user);
  	user.add();
  }
  ```

  ![image-20221126192309190](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221126192309190.png)

# IOC

## 概念和原理

### 什么是IOC

1. **控制反转**，**把对象创建和对象之间的调用过程，交给Spring进行管理**。
2. 使用IOC的目的：为了**降低客户端代码和客户端使用到的包中类的对象的耦合度**。
3. 上面的案例的实现就是利用到了IOC。

## IOC容器相关接口

1. IOC思想基于IOC容器实现，**IOC容器底层就是对象工厂**。

2. Spring提供IOC容器实现的两种方式（两个接口）：

   - **BeanFactory**：IOC容器的基本实现，是**Spring内部的使用接口，不提供给开发人员进行使用**。使用这个接口，**加载配置文件的时候不会创建对象，在获取对象的时候才去创建对象**。
   - **ApplicationContext**：**BeanFactory接口的子接口，提供更多更强大的功能，一般由开发人员进行使用**。使用这个接口，**加载配置文件的时候就会把在配置文件中注册的对象进行创建**。

3. ApplicationContext接口有实现类：

   ![image-20221126193548520](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221126193548520.png)

## Bean管理的概念

### 什么是Bean管理

- Spring管理Bean指的是两个操作：
  1. Spring创建Bean对象
  2. Spring向Bean对象中注入属性
- Bean管理操作有两种方式：
  1. 基于xml配置文件方式实现
  2. 基于注解方式实现

## 基于xml的方式实现Bean管理




## 基于注解的方式实现Bean管理

### 什么是注解

1. 注解**是代码的特殊标记**，**格式为：@注解名称(属性名称=属性值，属性名称=属性值......)**
2. **注解可以作用在类、方法、属性上面**
3. 使用注解实现Bean管理的目的：简化xml配置（不得不说，配置xml太繁琐了）

### Spring针对Bean管理中创建对象的操作提供的注解

1. **@Component**
2. **@Service**
3. **@Controller**
4. **@Repository**
5. 上面的四个注解功能是一样的，都是**写在类上面，能够被ComponentScan扫描到，被扫描到之后将会把被注解的类注册到IOC容器中**，但是**为了保证项目的层次结构清晰明了，我们对不同层的Bean进行注册的时候，应该使用该层对应的注解**，比如业务层注册Bean就应该使用@Service，控制层注册Bean就应该使用@Controller，持久层注册Bean就应该使用@Repository。

### Spring针对Bean管理中注入属性的操作提供的注解

1. **@Autowired**：根据类型进行注入

   ```java
   @Service
   public class UserService {
   	//定义 dao 类型属性
   	//不需要添加 set 方法
   	//添加注入属性注解
   	@Autowired
   	private UserDao userDao;
   	public void add() {
   		System.out.println("service add.......");
   		userDao.add();
   	}
   }
   ```

2. **@Qualifier**：根据名称进行注入，需要一个名为value的参数，可以和@Autowired搭配进行使用

   ```java
   //定义 dao 类型属性
   //不需要添加 set 方法
   //添加注入属性注解
   @Autowired
   //根据类型进行注入
   @Qualifier(value = "userDaoImpl1")
   //根据名称进行注入
   private UserDao userDao;
   ```

3. **@Resource**：带名称参数name使用就是根据名称进行注入，不带名称参数name使用就是根据类型进行注入

   ```java
   //@Resource //根据类型进行注入
   @Resource(name = "userDaoImpl1")
   //根据名称进行注入
   private UserDao userDao;
   ```

4. **@Value**：注入普通类型的属性，需要一个名为value的参数

   ```java
   @Value(value = "abc")
   private String name;
   ```

### 基于注解的方式实现对象的创建

1. 引入依赖：

   ![image-20221126195059119](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221126195059119.png)

2. 开启组件扫描，**组件扫描会扫描指定的包及其子包，扫描到被标识为Bean的类，会将其加入注册到IOC容器中**（这里我有个问题，扫描到的时候会直接创建对象吗？还是说等使用的时候再创建相应的对象？），这里是使用xml配置的方式开启组件扫描，这一步也可以用注解进行实现。

3. 创建类，在类上面添加注解将其标识为Bean：

   ```java
   //在注解里面 value 属性值可以省略不写，
   //默认值是类名称，首字母小写
   //UserService -- userService
   @Component(value = "userService")
   //<bean id="userService" class=".."/>
   public class UserService {
   	public void add() {
   		System.out.println("service add.......");
   	}
   }
   ```

4. 详细配置组件扫描的参数：

   ```xml
   <!--示例 1
   	use-default-filters="false" 表示现在不使用默认 filter，自己配置 filter
   	context:include-filter ，设置扫描哪些内容
   -->
   <context:component-scan base-package="com.atguigu" use-default-filters="false">
   	<context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
   </context:component-scan>
   <!--示例 2
   	下面配置扫描包所有内容
   	context:exclude-filter： 设置哪些内容不进行扫描
   -->
   <context:component-scan base-package="com.atguigu">
   	<context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
   </context:component-scan>
   ```

5. 基于注解方式实现属性注入：第一步 把 service 和 dao 对象创建，在 service 和 dao 类添加创建对象注解；第二步 在 service 注入 dao 对象，在 service 类添加 dao 类型属性，在属性上面使用注解：

   ```java
   @Service
   public class UserService {
   	//定义 dao 类型属性
   	//不需要添加 set 方法
   	//添加注入属性注解
   	@Autowired
   	private UserDao userDao;
   	public void add() {
   		System.out.println("service add.......");
   		userDao.add();
   	}
   }
   ```

6. 完全注解开发：上面的实现中还设计到xml配置文件的编写，这样实际上是比较不方便的，但是**xml配置文件也可以用注解来实现**，可以使用**@Configuration**注解，**被这个注解修饰的类会作为配置类，替代 xml 配置文件，在这个类上做的操作就相当于在之前的xml文件中做的配置**，这样整个实现就是完全基于注解的了：

   ```java
   @Configuration//被这个注解修饰的类会作为配置类，替代 xml 配置文件，在这个类上做的操作就相当于在之前的xml文件中做的配置
   @ComponentScan(basePackages = {"com.atguigu"})//配置组件扫描
   public class SpringConfig {
   }
   ```

   编写测试类进行测试：

   ```java
   @Test
   public void testService2() {
   	//加载配置类
   	ApplicationContext context = new AnnotationConfigApplicationContext(SpringConfig.class);
   	UserService userService = context.getBean("userService",
   	UserService.class);
   	System.out.println(userService);
       userService.add();
   }
   ```

# AOP

## 什么是AOP

- AOP即是**面向切面（方面）编程**，利用AOP可以**对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高了开发的效率**。

- 对于面向切面编程比较通俗的描述是：**不通过修改源代码的方式，在主干功能里面添加新功能**。

- 使用登录例子来说明AOP：

  ![image-20221127195023595](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221127195023595.png)

## AOP的底层原理

- AOP的底层使用的是动态代理，有两种动态代理，分别是**JDK动态代理和CGLIB动态代理**。

### 被增强的类实现了接口的情况使用JDK动态代理

- 创建接口实现类代理对象，增强类的方法：

  ![image-20221127195703994](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221127195703994.png)

### 被增强的类没实现接口的情况使用CGLIB动态代理

- 创建子类的代理对象增强类的方法：

  ![image-20221127195742084](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221127195742084.png)

## JDK动态代理

### 使用JDK动态代理，使用Proxy类里面的方法创建代理对象

- 用到的类在这儿：

  ![image-20221127201557295](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221127201557295.png)

- 调用newProxyInstance方法来创建代理对象：

  ![image-20221127201704106](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221127201704106.png)

  这个方法有三个参数：

  第一个参数是类加载器

  第二个参数是增强方法所在的类实现的接口，支持多个接口

  第三个参数是InvocationHandler这个接口的实现类，创建代理对象，写增强的部分

### 编写JDK动态代理的代码

1. 创建接口，定义方法：

   ```java
   public interface UserDao {
   	public int add(int a,int b);
   	public String update(String id);
   }
   ```

2. 创建接口实现类，实现方法：

   ```java
   public class UserDaoImpl implements UserDao {
   	@Override
   	public int add(int a, int b) {
   		return a+b;
   	}
   	@Override
   	public String update(String id) {
   		return id;
   	}
   }
   ```

3. 使用Proxy类创建接口代理对象：

   ```java
   public class JDKProxy {
   	public static void main(String[] args) {
   		//创建接口实现类代理对象
   		Class[] interfaces = {UserDao.class};
   		//Proxy.newProxyInstance(JDKProxy.class.getClassLoader(), interfaces, new InvocationHandler() {
   			//@Override
   			//public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
   				//return null;
   			//}
   		//});
   		UserDaoImpl userDao = new UserDaoImpl();
   		UserDao dao = (UserDao)Proxy.newProxyInstance(JDKProxy.class.getClassLoader(), interfaces,new UserDaoProxy(userDao));
   		int result = dao.add(1, 2);
   		System.out.println("result:"+result);
   	}
   }
   //创建代理对象代码
   class UserDaoProxy implements InvocationHandler {
   	//1 把创建的是谁的代理对象，把谁传递过来
   	//有参数构造传递
   	private Object obj;
   	public UserDaoProxy(Object obj) {
   		this.obj = obj;
   	}
   	//增强的逻辑
   	@Override
   	public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
   		//方法之前
   		System.out.println("方法之前执行...."+method.getName()+" :传递的参数..."+ Arrays.toString(args));
   		//被增强的方法执行
   		Object res = method.invoke(obj, args);
   		//方法之后
   		System.out.println("方法之后执行...."+obj);
   		return res;
   	}
   }
   ```

## AOP常用术语

### 连接点

- **类里面那些可以被增强的方法称为连接点**。

### 切入点

- **实际被真正增强的方法称为切入点**。

### 增强（通知）

- **实际增强的逻辑部分称为增强（通知）**。
- 增强（通知）有多种类型：**前置增强（通知）、后置增强（通知）、环绕增强（通知）、异常增强（通知）、最终增强（通知）**。

### 切面

- 是一种动作，就是**把增强（通知）应用到切入点的过程**。

## AOP操作的准备工作

- **Spring框架一般都是基于AspectJ实现AOP操作，但是AspectJ不是Spring的组成部分**，它是一个独立的AOP框架，一般我们把AspectJ和Spring框架一起使用，进行AOP操作。

- 基于AspectJ实现AOP操作有两种方式：**第一种是基于xml配置文件实现，第二种是基于注解方式实现，第二种方式是我们普遍采用的方式**。

- 在项目工程里面引入AOP相关依赖：

  ![image-20221128110244039](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221128110244039.png)

- **切入点表达式**：

  切入点表达式的作用：**表示对哪个类里面的哪个方法进行增强**。

  语法结构：**execution ( [权限修饰符] [返回类型] [类全路径] [方法名称] \( [参数列表] \) )**

  举例 1：对 com.atguigu.dao.BookDao 类里面的 add 进行增强 

  execution(* com.atguigu.dao.BookDao.add(..))
  举例 2：对 com.atguigu.dao.BookDao 类里面的所有的方法进行增强
  execution(* com.atguigu.dao.BookDao.* (..))

  举例 3：对 com.atguigu.dao 包里面所有类，类里面所有方法进行增强
  execution(* com.atguigu.dao.\*.\* (..))

## 基于AspectJ相关注解实现AOP操作

1. 创建类，在类里面定义方法：

   ```java
   public class User {
   	public void add() {
   		System.out.println("add.......");
   	}
   }
   ```

2. 创建增强类（编写增强逻辑）

   - 在增强类里面创建方法，**可以让不同方法代表不同的增强（通知）类型**：

     ```java
     //增强的类
     public class UserProxy {
     	public void before() {//前置通知
     		System.out.println("before......");
     	}
     }
     ```

3. 进行增强（通知）的配置：

   - 在spring的配置文件中**开启注解扫描**：

     ```xml
     <?xml version="1.0" encoding="UTF-8"?>
     <beans xmlns="http://www.springframework.org/schema/beans"
     	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
     	xmlns:context="http://www.springframework.org/schema/context"
     	xmlns:aop="http://www.springframework.org/schema/aop"
     	xsi:schemaLocation="http://www.springframework.org/schema/beans
     http://www.springframework.org/schema/beans/spring-beans.xsd
     http://www.springframework.org/schema/context
     http://www.springframework.org/schema/context/spring-context.xsd
     http://www.springframework.org/schema/aop
     http://www.springframework.org/schema/aop/spring-aop.xsd">
     	<!-- 开启注解扫描 -->
     	<context:component-scan base-package="com.atguigu.spring5.aopanno"></context:component-scan>
     ```

   - **使用注解注册User和UserProxy对象**：

     ![image-20221128111224087](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221128111224087.png)

   - **在增强类上面添加注解@Aspect表示生成代理对象**：

     ```java
     //增强的类
     @Component
     @Aspect //生成代理对象
     public class UserProxy {
     }
     ```
     
   - 在spring配置文件中**开启Aspect生成代理对象的功能**：

     ```xml
     <!-- 开启 Aspect 生成代理对象-->
     <aop:aspectj-autoproxy></aop:aspectj-autoproxy>
     ```

4. 配置不同类型的增强（通知）：

   - 在增强类的里面，**在作为增强（通知）方法上面添加增强（通知）类型注解，使用切入点表达式配置**：

     ```java
     //增强的类
     @Component
     @Aspect //生成代理对象
     public class UserProxy {
     	//前置通知
     	//@Before 注解表示作为前置通知
     	@Before(value = "execution(* com.atguigu.spring5.aopanno.User.add(..))")
     	public void before() {
     		System.out.println("before.........");
     	}
     	//后置通知（返回通知）
     	@AfterReturning(value = "execution(*com.atguigu.spring5.aopanno.User.add(..))")
     	public void afterReturning() {
     		System.out.println("afterReturning.........");
     	}
     	//最终通知
     	@After(value = "execution(* com.atguigu.spring5.aopanno.User.add(..))")
     	public void after() {
     		System.out.println("after.........");
     	}
     	//异常通知
     	@AfterThrowing(value = "execution(* com.atguigu.spring5.aopanno.User.add(..))")
     	public void afterThrowing() {
     		System.out.println("afterThrowing.........");
     	}
         //环绕通知
     	@Around(value = "execution(* com.atguigu.spring5.aopanno.User.add(..))")
     	public void around(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
     		System.out.println("环绕之前.........");
     		//被增强的方法执行
     		proceedingJoinPoint.proceed();
     		System.out.println("环绕之后.........");
     	}
     }
     ```

5. **相同的切入点抽取**：

   - 可以**在类上使用@Pointcut(value = 切入点表达式)来将被修饰的类作为切入点表达式的别名，以后可以直接使用"类名()"的形式来代指对应的切入点表达式**：

     ```java
     //相同切入点抽取
     @Pointcut(value = "execution(* com.atguigu.spring5.aopanno.User.add(..))")
     public void pointdemo() {
     }
     //前置通知
     //@Before 注解表示作为前置通知
     @Before(value = "pointdemo()")
     public void before() {
     	System.out.println("before.........");
     }
     ```

6. 有多个增强类对同一个方法进行增强，可以**设置增强类的优先级**：

   - **在增强类上面添加注解@Order(数字类型值)，数字类型值越小优先级越高**：

     ```java
     @Component
     @Aspect
     @Order(1) //提问：这个注解可以应用在增强方法上吗？如果不能，那么对于被这个增强类增强的多个类对这个类分别有不同的优先级要求该怎么办？还是说不可能出现这种情况？
     public class PersonProxy
     ```

7. 完全使用注解开发：

   - 创建配置类，不需要创建xml配置文件，**使用@EnableAspectJAutoProxy(proxyTargetClass = true)来开启 Aspect 生成代理对象的功能**：

     ```java
     @Configuration
     @ComponentScan(basePackages = {"com.atguigu"})
     @EnableAspectJAutoProxy(proxyTargetClass = true)
     public class ConfigAop {
     }
     ```

## 基于配置文件中AspectJ的相关配置实现AOP操作



# JDBCTemplate

## 概念和准备

### 什么是JDBCTemplate

- Spring框架对JDBC进行了封装，使用JDBCTemplate方便对数据库进行操作。

### 准备工作

1. 引入相关jar包：

   ![image-20221129103952874](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221129103952874.png)

2. 在spring配置文件中配置数据库连接池：

   ```xml
   <!-- 数据库连接池 -->
   <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource" destroy-method="close">
   	<property name="url" value="jdbc:mysql:///user_db" />
   	<property name="username" value="root" />
   	<property name="password" value="root" />
   	<property name="driverClassName" value="com.mysql.jdbc.Driver" />
   </bean>
   ```

3. 配置JDBCTemplate对象，注入DataSource：

   ```xml
   <!-- JdbcTemplate 对象 -->
   <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
   	<!--注入 dataSource-->
   	<property name="dataSource" ref="dataSource"></property>
   </bean>
   ```

4. 创建service类，创建dao接口实现类，在dao类中注入JDBCTemplate对象：

   配置文件中开启组件扫描：

   ```xml
   <!-- 组件扫描 -->
   <context:component-scan base-package="com.atguigu"></context:component-scan>
   ```

   Service类：

   ```java
   @Service
   public class BookService {
   	//注入 dao
   	@Autowired
   	private BookDao bookDao;
   }
   ```

   Dao接口实现类：

   ```java
   @Repository
   public class BookDaoImpl implements BookDao {
   	//注入 JdbcTemplate
   	@Autowired
   	private JdbcTemplate jdbcTemplate;
   }
   ```

## JDBCTemplate操作数据库

### 添加操作

1. 创建对应数据库表的实体类：

   ![image-20221129104705354](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221129104705354.png)

2. 编写service和dao：

   - 调用JDBCTemplate对象里面的update方法实现添加操作，在dao接口的实现类中对数据库进行添加操作：

     ![image-20221129105140096](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221129105140096.png)

     ```java
     @Repository
     public class BookDaoImpl implements BookDao {
     	//注入 JdbcTemplate
     	@Autowired
     	private JdbcTemplate jdbcTemplate;
     	//添加的方法
     	@Override
     	public void add(Book book) {
     		//1 创建 sql 语句
     		String sql = "insert into t_book values(?,?,?)";
     		//2 调用方法实现
     		Object[] args = {book.getUserId(), book.getUsername(), book.getUstatus()};
     		int update = jdbcTemplate.update(sql,args);
     		System.out.println(update);
     	}
     }
     ```

3. 测试类：

   ```java
   @Test
   public void testJdbcTemplate() {
   	ApplicationContext context =
   		new ClassPathXmlApplicationContext("bean1.xml");
   	BookService bookService = context.getBean("bookService",BookService.class);
   	Book book = new Book();
   	book.setUserId("1");
   	book.setUsername("java");
   	book.setUstatus("a");
   	bookService.addBook(book);
   }
   ```

   ![image-20221129104920764](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221129104920764.png)

### 修改和删除操作

- 修改：

  ```java
  @Override
  public void updateBook(Book book) {
  	String sql = "update t_book set username=?,ustatus=? where user_id=?";
  	Object[] args = {book.getUsername(), book.getUstatus(),book.getUserId()};
  	int update = jdbcTemplate.update(sql, args);
  	System.out.println(update);
  }
  ```

- 删除：

  ```java
  @Override
  public void delete(String id) {
  	String sql = "delete from t_book where user_id=?";
  	int update = jdbcTemplate.update(sql, id);
  	System.out.println(update);
  }
  ```

### 查询返回某个值

- 场景：查询表里面有多少条记录，返回的是某个值

- 使用JDBCTemplate实现查询返回某个值的代码：
![image-20221129105851998](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221129105851998.png)
```java
//查询表记录数
@Override
public int selectCount() {
	String sql = "select count(*) from t_book";
	Integer count = jdbcTemplate.queryForObject(sql, Integer.class);
	return count;
}
```

### 查询返回对象

- 场景：查询图书详情

- 使用JDBCTemplate实现查询返回对象：

  ![image-20221129110122369](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221129110122369.png)

  ```java
  //查询返回对象
  @Override
  public Book findBookInfo(String id) {
  	String sql = "select * from t_book where user_id=?";
  	//调用方法
  	Book book = jdbcTemplate.queryForObject(sql, new BeanPropertyRowMapper<Book>(Book.class), id);
  	return book;
  }
  ```

### 查询返回集合

- 场景：查询图书列表分页

- 使用JDBCTemplate实现查询返回集合：

  ![image-20221129110640049](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221129110640049.png)

  ```java
  //查询返回集合
  @Override
  public List<Book> findAllBook() {
  	String sql = "select * from t_book";
  	//调用方法
  	List<Book> bookList = jdbcTemplate.query(sql, new
  	BeanPropertyRowMapper<Book>(Book.class));
  	return bookList;
  }
  ```

### 批量操作

- 批量操作：操作表里面多条记录

- JDBCTemplate实现批量添加操作：

  ![image-20221129110903601](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221129110903601.png)

  ```java
  //批量添加
  @Override
  public void batchAddBook(List<Object[]> batchArgs) {
  	String sql = "insert into t_book values(?,?,?)";
  	int[] ints = jdbcTemplate.batchUpdate(sql, batchArgs);
  	System.out.println(Arrays.toString(ints));
  }
  //批量添加测试
  List<Object[]> batchArgs = new ArrayList<>();
  Object[] o1 = {"3","java","a"};
  Object[] o2 = {"4","c++","b"};
  Object[] o3 = {"5","MySQL","c"};
  batchArgs.add(o1);
  batchArgs.add(o2);
  batchArgs.add(o3);
  //调用批量添加
  bookService.batchAdd(batchArgs);
  ```

- JDBCTemplate实现批量修改操作：

  ```java
  //批量修改
  @Override
  public void batchUpdateBook(List<Object[]> batchArgs) {
  	String sql = "update t_book set username=?,ustatus=? where user_id=?";
  	int[] ints = jdbcTemplate.batchUpdate(sql, batchArgs);
  	System.out.println(Arrays.toString(ints));
  }
  //批量修改
  List<Object[]> batchArgs = new ArrayList<>();
  Object[] o1 = {"java0909","a3","3"};
  Object[] o2 = {"c++1010","b4","4"};
  Object[] o3 = {"MySQL1111","c5","5"};
  batchArgs.add(o1);
  batchArgs.add(o2);
  batchArgs.add(o3);
  //调用方法实现批量修改
  bookService.batchUpdate(batchArgs);
  ```

- JDBCTemplate实现批量删除操作：

  ```java
  //批量删除
  @Override
  public void batchDeleteBook(List<Object[]> batchArgs) {
  	String sql = "delete from t_book where user_id=?";
  	int[] ints = jdbcTemplate.batchUpdate(sql, batchArgs);
  	System.out.println(Arrays.toString(ints));
  }
  //批量删除
  List<Object[]> batchArgs = new ArrayList<>();
  Object[] o1 = {"3"};
  Object[] o2 = {"4"};
  batchArgs.add(o1);
  batchArgs.add(o2);
  //调用方法实现批量删除
  bookService.batchDelete(batchArgs);
  ```

# 事务操作

## 事务的概念

### 什么是事务

- 事务**是数据库操作最基本的单元**，事务**是逻辑上的一组操作**，其**具有原子性**，**要么都成功，如果其中有一个操作失败那么所有的操作都会失败**。
- 典型场景：银行转账，a转账100给b，a会少100而b会多100，转账这个操作实际上就是一个事务，a少100和b多100要么都成功，如果a没有少100或者b没有多100，事务都会失败，然后回滚，如果事务没有原子性，很明显像上面这种场景下就没有办法保证转账的安全性了。

### 事务的四个特性（ACID）

- **原子性（Atomicity）**：**一系列操作，要么都成功，要么都失败**。
- **一致性（Consistency）**：一致性是指事务**必须使数据库从一个一致性状态变换到另一个一致性状态，也就是说一个事务执行之前和执行之后都必须处于一致性状态**。以上面的转账操作为例就是，这100元不能凭空消失，必须在a和b两者之一的手中。
- **隔离性（Isolation）**：**多个并发的事务之间应该相互隔离，不能相互干扰**。
- **持久性（Durability）**：**一个事务一旦提交，对于数据库中的数据的改变是永久性的**，即便是在数据库系统遇到故障的情况下也不会丢失提交事务的操作。

## 搭建事务的操作环境

- 以上面的转账场景为例子，需要实现的结构大致如下图：

  ![image-20221130170842331](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221130170842331.png)

1. 创建数据库表，添加记录：

   ![image-20221130170943485](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221130170943485.png)

2. 创建service，搭建dao，完成对象创建和注入关系：

   - **service注入dao，在dao注入JDBCTemplate，在JDBCTemplate注入DataSource**：

     ```java
     @Service
     public class UserService {
     	//注入 dao
     	@Autowired
     	private UserDao userDao;
     }
     @Repository
     public class UserDaoImpl implements UserDao {
     	@Autowired
     	private JdbcTemplate jdbcTemplate;
     }
     ```

3. 在dao创建两个方法：多钱和少钱的方法（分成两个方法主要是为了**遵守单一职责原则**），在service创建转账的方法：

   ```java
   @Repository
   public class UserDaoImpl implements UserDao {
       
   	@Autowired
   	private JdbcTemplate jdbcTemplate;
       
   	//lucy 转账 100 给 mary
   	//少钱
   	@Override
   	public void reduceMoney() {
   		String sql = "update t_account set money=money-? where username=?";
   		jdbcTemplate.update(sql,100,"lucy");
   	}
       
   	//多钱
   	@Override
   	public void addMoney() {
   		String sql = "update t_account set money=money+? where username=?";
   		jdbcTemplate.update(sql,100,"mary");
   	}
   }
   
   @Service
   public class UserService {
   	//注入 dao
   	@Autowired
   	private UserDao userDao;
       
   	//转账的方法
   	public void accountMoney() {
   		//lucy 少 100
   		userDao.reduceMoney();
           
   		//mary 多 100
   		userDao.addMoney();
   	}
   }
   ```

4. 上面代码，如果正常执行没有问题的，但是如果代码执行过程中出现异常的话：

   ![image-20221130231843794](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221130231843794.png)

   如果中间没有出现异常的话，转账的流程是正确的，但是**由于中间出现了一个异常，所以后面加钱的操作就无法执行了，这样就不满足一致性了，因为100块钱凭空消失了，并不是从一个一致性的状态转移道另外一个一致性状态了，这样的情况肯定是我们不想看到的**，那么上面的问题该如何解决呢？可以**使用事务进行解决**，因为**事务天生自带四个特性，中间出现异常之后由于事务的原子性，整个操作会回滚，虽然转账也没有成功，但是保证了一致性，100块钱没有凭空消失，这样的结果是我们可以接受的**。

5. 对上面的操作进行事务操作的理论流程：

   ![image-20221130232519954](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221130232519954.png)

## Spring事务管理介绍

- **事务应该添加到JavaEE三层结构里面的Service层（业务逻辑层）中**

- 利用Spring进行事务管理操作有两种方式：**编程式事务管理和声明式事务管理**，后者是我们普遍使用的。

- 声明式事务管理有两种实现方式：可以**基于注解方式实现（这也是普遍使用的方式）**，也可以**基于xml配置文件方式实现**。

- 利用Spring进行声明式事务管理，**底层使用到了AOP的原理**。

- Spring事务管理的API：

  - **Spring提供了一个接口，代表事务管理器，这个接口针对不同的框架提供不同的实现类**：

    ![image-20221130233116323](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221130233116323.png)

## 注解声明式事务管理（基于注解实现事务操作）

1. 在Spring配置文件中**配置事务管理器**：

   ```xml
   <!--创建事务管理器-->
   <bean id="transactionManager"
   class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
   	<!--注入数据源-->
   	<property name="dataSource" ref="dataSource"></property>
   </bean>
   ```

2. 在Spring配置文件中**开启事务注解**：

   - 在Spring配置文件**引入名称空间tx**：

     ```xml
     <beans xmlns="http://www.springframework.org/schema/beans"
     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
     xmlns:context="http://www.springframework.org/schema/context"
     xmlns:aop="http://www.springframework.org/schema/aop"
     xmlns:tx="http://www.springframework.org/schema/tx"
     xsi:schemaLocation="http://www.springframework.org/schema/beans
     http://www.springframework.org/schema/beans/spring-beans.xsd
     http://www.springframework.org/schema/context
     http://www.springframework.org/schema/context/spring-context.xsd
     http://www.springframework.org/schema/aop
     http://www.springframework.org/schema/aop/spring-aop.xsd
     http://www.springframework.org/schema/tx
     http://www.springframework.org/schema/tx/spring-tx.xsd">
     ```

   - **开启事务注解**：

     ```xml
     <!--开启事务注解-->
     <tx:annotation-driven transaction-
     manager="transactionManager"></tx:annotation-driven>
     ```

3. 在service类上面（或者service类里面的方法上面）添加事务注解：

   - **@Transactional，这个注解可以添加到类上面，也可以添加方法上面**

   - 如果把这个注解添加类上面，这个类里面所有的方法都添加事务

   - 如果把这个注解添加方法上面，为这个方法添加事务

     ```java
     @Service
     @Transactional
     public class UserService {
     ```


## 声明式事务管理参数配置

- 在service类上面添加注解**@Transactional**，在这个注解里面可以配置事务相关参数：

  ![image-20221201103415495](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221201103415495.png)

### propagation参数设置事务传播行为

- **有多个事务的方法直接进行调用，这个过程中事务是如何进行管理的？事务的传播行为就是来指定这个问题的解决方案的**，这个问题有多种解决方案，通过设置这个参数来使用最符合场景的解决方案。

- **事务方法：含有对数据库表数据进行变化的操作的方法**。

  ![image-20221201104343196](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221201104343196.png)

- **Spring框架事务传播行为有七种**，可以结合它们的特性和具体场景来选择使用哪种：

  ![image-20221201104621016](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221201104621016.png)

- 参数的设置方式如下，实参是相应常量类中的常量：

  ![image-20221201105014480](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221201105014480.png)

### isolation参数设置事务隔离级别

- 事务有一个特性称为隔离性，这个隔离性也就是让多个事务操作之间不会互相产生影响，在实际应用中，如果不考虑事务的隔离性的话就会产生很多的问题。

- 其中有三种问题是事务的隔离级别不够造成的，它们分别是：**脏读、不可重复读、虚（幻）读**

- **脏读**：即**一个未提交事务读取到另一个未提交事务的数据**，在下面的例子中事务A读取到了事务B中的还未进行提交的**脏数据**60000，而之后事务B进行了回滚，数据还是5000，这样就导致事务A读取到的数据是错误的。

  ![image-20221201110004055](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221201110004055.png)

- **不可重复读**：即**一个事务范围内两个相同的查询却返回了不同数据，这是由于查询时系统中其他事务修改的提交而引起的**，比如下面这个例子，事务A进行了两次查询，第一次查询到的是5000，但是在第二次查询之前，事务B提交了修改数据的操作，事务A第一次读到的数据就被修改了，此时事务A再读一次，结果就和第一次读的时候的结果不同了。

  ![image-20221203113144852](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221203113144852.png)

- **虚（幻）读**：即**一个事务进行多次相同条件的查询或修改时出现了原本不存在的数据或者原本存在的数据消失了，就像是产生幻觉一样，这通常是由于在当前事务的多个操作之间有别的事务添加或删除了一条或多条记录造成的**，**其定义和不可重复读有些相似，只不过造成不可重复读的是记录的修改，而造成幻读的是记录的添加和删除**。比如事务A按照某个条件进行了一次查询，在事务A想要第二次查询的时候，事务B提交了一个增加数据的操作，这样事务A第二次查询出来的内容就和第一次查询出来的内容不同了。

- 对于以上三种读问题，我们可以通过设置参数isolation（即事物的隔离级别）来进行解决，但是要注意，**事务的隔离级别越高，事务的读写性能就越低，因为是通过加锁来实现的嘛**：

  ![image-20221203114513492](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221203114513492.png)

  ![image-20221203114530378](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221203114530378.png)

### timeout参数设置超时时间

- **设置了超时时间之后，事务需要在指定的时间内进行提交，如果在指定的时间内事务没有进行提交，那么事务会进行回滚**。
- **这个参数的默认值是-1，也就是永不超时**；设置的时间是**以秒为单位**的。

### readOnly参数设置是否只读

- **读就是查询操作**，写就是添加、修改、删除操作
- **readOnly的默认值是false，表示可以进行所有crud操作**
- **将readOnly的值设置为true后，事务就只能进行查询操作**

### rollbackFor参数设置哪些异常回滚

- 设置**出现哪些异常后进行事务回滚**

### noRollbackFor参数设置哪些异常不回滚

- 设置**出现哪些异常之后不进行事务回滚**

## XML声明式事务管理（基于XML配置文件实现事务操作）

## 完全注解声明式事务管理

- 创建配置类，使用配置类替代xml配置文件：

  ```java
  @Configuration//配置类
  @ComponentScan(basePackages = "com.atguigu")//组件扫描
  @EnableTransactionManagement//开启事务
  public class TxConfig {
  	//创建数据库连接池
  	@Bean
  	public DruidDataSource getDruidDataSource() {
  		DruidDataSource dataSource = new DruidDataSource();
  		dataSource.setDriverClassName("com.mysql.jdbc.Driver");
  		dataSource.setUrl("jdbc:mysql:///user_db");
  		dataSource.setUsername("root");
  		dataSource.setPassword("root");
  		return dataSource;
  	}
  	//创建 JdbcTemplate 对象
  	@Bean
  	public JdbcTemplate getJdbcTemplate(DataSource dataSource) {
  		//到 ioc 容器中根据类型找到 dataSource
  		JdbcTemplate jdbcTemplate = new JdbcTemplate();
  		//注入 dataSource
  		jdbcTemplate.setDataSource(dataSource);
  		return jdbcTemplate;
      }
  	//创建事务管理器
  	@Bean
  	public DataSourceTransactionManager getDataSourceTransactionManager(DataSource dataSource) {
  		DataSourceTransactionManager transactionManager = new
  		DataSourceTransactionManager();
  		transactionManager.setDataSource(dataSource);
  		return transactionManager;
  	}
  }
  ```

# Spring5框架新功能

## 代码上的修改

- 整个Spring5框架的代码基于Java8，运行时兼容JDK9，许多不建议使用的类和方法在代码库中删除了。

## 通用的日志封装

- Spring5框架自带了通用的日志封装

- Spring5已经移除Log4jConfigListener，官方**建议使用Log4j2**

- Spring5框架整合Log4j2：

  1. 引入jar包：

     ![image-20221206162148512](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221206162148512.png)

  2. 创建log4j2.xml配置文件：

     ```xml
     <?xml version="1.0" encoding="UTF-8"
     ?>
     <!--日志级别以及优先级排序: OFF > FATAL > ERROR > WARN > INFO > DEBUG > TRACE >
     ALL -->
     <!--Configuration 后面的 status 用于设置 log4j2 自身内部的信息输出，可以不设置，
     当设置成 trace 时，可以看到 log4j2 内部各种详细输出-->
     <configuration status="INFO">
     	<!--先定义所有的 appender-->
     	<appenders>
     		<!--输出日志信息到控制台-->
     		<console name="Console" target="SYSTEM_OUT">
     			<!--控制日志输出的格式-->
     			<PatternLayout pattern="%d{yyyy-MM-dd HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
     		</console>
     	</appenders>
     	<!--然后定义 logger，只有定义 logger 并引入的 appender，appender 才会生效-->
     	<!--root：用于指定项目的根日志，如果没有单独指定 Logger，则会使用 root 作为
     默认的日志输出-->
     	<loggers>
     		<root level="info">
     			<appender-ref ref="Console"/>
     		</root>
     	</loggers>
     </configuration>
     ```

## 核心容器支持@Nullable注解

- @Nullable注解**可以使用在方法、属性、参数上面，表示方法返回值、属性值、参数值可以为空**。

- @Nullable注解用在方法上面，表示方法返回值可以为空：

  ![image-20221206162703285](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221206162703285.png)

- @Nullable注解用在方法参数前面，表示方法参数可以为空：

  ![image-20221206162757312](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221206162757312.png)

- @Nullable注解使用在属性上面，表示属性值可以为空：

  ![image-20221206162843955](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221206162843955.png)

## 核心容器支持函数式风格（GenericApplicationContext）

- 下面是一个用函数式风格创建对象交给Spring进行管理的例子：

  ```java
  //函数式风格创建对象，交给 spring 进行管理
  @Test
  public void testGenericApplicationContext() {
  	//1 创建 GenericApplicationContext 对象
  	GenericApplicationContext context = new GenericApplicationContext();
  	//2 调用 context 的方法对象注册
  	context.refresh();
  	context.registerBean("user1",User.class,() -> new User());
      //3 获取在 spring 注册的对象
  	// User user = (User)context.getBean("com.atguigu.spring5.test.User");
  	User user = (User)context.getBean("user1");
  	System.out.println(user);
  }
  ```

## 支持整合JUnit5

- 整合JUnit4：

  1. 引入Spring相关针对测试的依赖：

     ![image-20221206164908060](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221206164908060.png)

  2. 创建测试类，使用注解方式完成：

     ```java
     @RunWith(SpringJUnit4ClassRunner.class)//单元测试框架
     @ContextConfiguration("classpath:bean1.xml")//加载配置文件
     public class JTest4 {
     	@Autowired
     	private UserService userService;
     	@Test
     	public void test1() {
     		userService.accountMoney();
     	}
     }
     ```

- 整合JUnit5：

  1. 引入JUnit5的jar包：

     ![image-20221206165041897](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221206165041897.png)

  2. 创建测试类，使用注解完成：

     ```java
     @ExtendWith(SpringExtension.class)
     @ContextConfiguration("classpath:bean1.xml")
     public class JTest5 {
     	@Autowired
     	private UserService userService;
     	@Test
     	public void test1() {
     		userService.accountMoney();
     	}
     }
     ```

  3. 使用一个**复合注解@SpringJUnitConfig**来替代上面两个注解完成整合：

     ```java
     @SpringJUnitConfig(locations = "classpath:bean1.xml")
     public class JTest5 {
     	@Autowired
     	private UserService userService;
     	@Test
     	public void test1() {
     		userService.accountMoney();
     	}
     }
     ```

## WebFlux



