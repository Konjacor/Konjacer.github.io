---
title: Mybatis入门
date: 2022-09-08 22:25:24
tags: [Mybatis]
---

<meta name="referrer" content="no-referrer"/>

1. 获取参数用${}不会自动加单引号，获取参数用#{}会自动加单引号

# MyBatis简介

## MyBatis历史

- **MyBatis最初是Apache的一个开源项目iBatis**, 2010年6月这个项目由Apache Software Foundation迁移到了Google Code。随着开发团队转投Google Code旗下， iBatis3.x正式更名为MyBatis。代码于2013年11月迁移到Github。
- iBatis一词来源于“internet”和“abatis”的组合，是一个**基于Java的持久层框架**。 iBatis提供的持久层框架包括SQL Maps和Data Access Objects（DAO）。

## MyBatis特性

1. MyBatis 是支持**定制化 SQL**、**存储过程**以及**高级映射**的优秀的持久层框架
2. MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集
3. MyBatis可以使用**简单的XML或注解**用于配置和原始映射，将接口和Java的POJO（Plain Old Java Objects，普通的Java对象）映射成数据库中的记录
4. MyBatis 是一个 半自动的ORM（Object Relation Mapping）框架

## MyBatis下载

- 下载地址：https://github.com/mybatis/mybatis-3

  ![image-20220916105207380](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220916105207380.png)

![image-20220916105221318](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220916105221318.png)

## SpringBoot整合MyBatis

### 引入依赖

- Spring Boot 整合 MyBatis 的第一步，就是在项目的 pom.xml 中引入 mybatis-spring-boot-starter 的依赖，示例代码如下。

  ```xml
  <!--引入 mybatis-spring-boot-starter 的依赖-->
  <dependency>
      <groupId>org.mybatis.spring.boot</groupId>
      <artifactId>mybatis-spring-boot-starter</artifactId>
      <version>2.2.0</version>
  </dependency>
  ```

### 配置MyBatis

- 在 Spring Boot 的配置文件（application.properties/yml）中对 MyBatis 进行配置，例如指定 mapper.xml 的位置、实体类的位置、是否开启驼峰命名法等等，示例代码如下。

  ```yaml
  ###################################### MyBatis 配置######################################
  mybatis:
    # 指定 mapper.xml 的位置
    mapper-locations: classpath:mybatis/mapper/*.xml
    #扫描实体类的位置,在此处指明扫描实体类的包，在 mapper.xml 中就可以不写实体类的全路径名
    type-aliases-package: com.konjacer.service.bean
    configuration:
      #默认开启xia'hua，可以不用设置该属性
      map-underscore-to-camel-case: true  
  ```


> 注意：使用 MyBatis 时，必须配置数据源信息，例如数据库 URL、数据库用户型、数据库密码和数据库驱动等。

### 创建实体类

### 创建Mapper接口

>当 mapper 接口较多时，我们可以在 Spring Boot 主启动类或者配置类上使用 @MapperScan 注解扫描指定包下的 mapper 接口，而不再需要在每个 mapper 接口上都标注@Mapper 注解。

### 创建Mapper映射文件

- 在配置文件 application.properties/yml 通过 mybatis.mapper-locations 指定的位置中创建 UserMapper.xml
- 使用 Mapper 进行开发时，需要遵循以下规则：
  1. mapper 映射文件中 namespace 必须与对应的 mapper 接口的完全限定名一致。
  2. mapper 映射文件中 statement 的 id 必须与 mapper 接口中的方法的方法名一致。
  3. mapper 映射文件中 statement 的 parameterType 指定的类型必须与 mapper 接口中方法的参数类型一致。
  4. mapper 映射文件中 statement 的 resultType 指定的类型必须与 mapper 接口中方法的返回值类型一致。

### 注解方式

- MyBatis 针对实际实际业务中使用最多的“增伤改查”操作，分别提供了以下注解来替换 mapper 映射文件，简化配置：
  1. @Select
  2. @Insert
  3. @Update
  4. @Delete

- 使用示例：

  ```java
  @Mapper
  public interface UserMapper {
      @Select("select * from user where user_name = #{userName,jdbcType=VARCHAR} and password = #{password,jdbcType=VARCHAR}")
      List<User> getByUserNameAndPassword(User user);
      @Delete("delete from user where id = #{id,jdbcType=INTEGER}")
      int deleteByPrimaryKey(Integer id);
      @Insert("insert into user ( user_id, user_name, password, email)" +
              "values ( #{userId,jdbcType=VARCHAR}, #{userName,jdbcType=VARCHAR}, #{password,jdbcType=VARCHAR}, #{email,jdbcType=VARCHAR})")
      int insert(User record);
      @Update(" update user" +
              "    set user_id = #{userId,jdbcType=VARCHAR},\n" +
              "      user_name = #{userName,jdbcType=VARCHAR},\n" +
              "      password = #{password,jdbcType=VARCHAR},\n" +
              "      email = #{email,jdbcType=VARCHAR}\n" +
              "    where id = #{id,jdbcType=INTEGER}")
      int updateByPrimaryKey(User record);
  }
  ```

- 注意事项：mapper 接口中的任何一个方法，都只能使用一种配置方式，即注解和 mapper 映射文件二选一，但不同方法之间，这两种方式则可以混合使用，例如方法 1 使用注解方式，方法 2 使用 mapper 映射文件方式。
- 我们可以根据 SQL 的复杂程度，选择不同的方式来提高开发效率：
  - 如果**没有复杂的连接查询，我们可以使用注解的方式来简化配置**（不过这个可以被MyBatisPlus的基本功能实现代替）；
  - 如果**涉及的 sql 较为复杂时，则使用 XML （mapper 映射文件）的方式更好一些**。

## 和其他持久化层技术对比

- JDBC
  1. SQL 夹杂在Java代码中耦合度高，导致硬编码内伤
  2. 维护不易且实际开发需求中 SQL 有变化，频繁修改的情况多见
  3. 代码冗长，开发效率低

- Hibernate 和 JPA
  1. 操作简便，开发效率高
  2. 程序中的长难复杂 SQL 需要绕过框架
  3. 内部自动生产的 SQL，不容易做特殊优化
  4. 基于全映射的全自动框架，大量字段的 POJO 进行部分映射时比较困难。
  5. 反射操作太多，导致数据库性能下降

- MyBatis
  1. 轻量级，性能出色
  2. SQL 和 Java 编码分开，功能边界清晰。Java代码专注业务、SQL语句专注数据
  3. 开发效率稍逊于Hibernate，但是完全能够接受

# 搭建MyBatis

## 示例开发环境

- IDE：idea 2019.2
- 构建工具：maven 3.5.4
- MySQL版本：MySQL 5.7
- MyBatis版本：MyBatis 3.5.7

## 创建Maven工程

- 打包方式jar：`<packaging>jar</packaging>`

- 引入依赖：

  ```xml
  <dependencies>
  	<!-- Mybatis核心 -->
  	<dependency>
  		<groupId>org.mybatis</groupId>
  		<artifactId>mybatis</artifactId>
  		<version>3.5.7</version>
  	</dependency>
      
  	<!-- junit测试 -->
  	<dependency>
  		<groupId>junit</groupId>
  		<artifactId>junit</artifactId>
  		<version>4.12</version>
  		<scope>test</scope>
  	</dependency>
      
  	<!-- MySQL驱动 -->
  	<dependency>
  		<groupId>mysql</groupId>
  		<artifactId>mysql-connector-java</artifactId>
  		<version>5.1.3</version>
  	</dependency>
  </dependencies>
  ```

## 创建MyBatis的核心配置文件

- 习惯上命名为**mybatis-config.xml**，这个文件名仅仅只是建议，并非强制要求。将来整合Spring之后，这个配置文件可以省略，所以大家操作时可以直接复制、粘贴。

- **核心配置文件主要用于配置连接数据库的环境以及MyBatis的全局配置信息**

- 核心配置文件存放的位置是src/main/resources目录下

- 配置示例：

  ```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <!DOCTYPE configuration
  	PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
  	"http://mybatis.org/dtd/mybatis-3-config.dtd">
  <configuration>
  	<!--设置连接数据库的环境-->
  	<environments default="development">
  		<environment id="development">
  			<transactionManager type="JDBC"/>
  			<dataSource type="POOLED">
  				<property name="driver" value="com.mysql.jdbc.Driver"/>
  				<property name="url" value="jdbc:mysql://localhost:3306/MyBatis"/>
  				<property name="username" value="root"/>
  				<property name="password" value="123456"/>
  			</dataSource>
  		</environment>
  	</environments>
  	<!--引入映射文件-->
  	<mappers>
  		<mapper resource="mappers/UserMapper.xml"/>
  	</mappers>
  </configuration>
  ```

## 创建mapper接口

- MyBatis中的mapper接口**相当于以前的dao**。但是区别在于，mapper仅仅是接口，我们不需要提供实现类。底层估计是用到了**cglib代理**。

- 代码示例：

  ```java
  public interface UserMapper {
  	/**
  	* 添加用户信息
  	*/
  	int insertUser();
  }
  ```

## 创建MyBatis的映射文件

- 相关概念：ORM（Object Relationship Mapping）对象关系映射。
  1. 对象：Java的实体类对象
  2. 关系：关系型数据库
  3. 映射：二者之间的对应关系

- | Java概念 | 数据库概念 |
  | -------- | ---------- |
  | 类       | 表         |
  | 属性     | 字段/列    |
  | 对象     | 记录/行    |

- 映射文件的命名规则：**表所对应的实体类的类名+Mapper.xml**
  例如：表t_user，映射的实体类为User，所对应的映射文件为UserMapper.xml，因此一个映射文件对应一个实体类，对应一张表的操作MyBatis映射文件用于编写SQL，访问以及操作表中的数据，MyBatis映射文件存放的位置是src/main/resources/mappers目录下

- MyBatis中可以面向接口操作数据，要保证两个一致：
  1. **mapper接口的全类名和映射文件的命名空间（namespace）保持一致**
  2. mapper接口中方法的**方法名和映射文件中编写SQL的标签的id属性保持一致**

- 代码示例：

  ```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <!DOCTYPE mapper
  	PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  	"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
  <mapper namespace="com.atguigu.mybatis.mapper.UserMapper">
  	<!--int insertUser();-->
  	<insert id="insertUser">
  		insert into t_user values(null,'张三','123',23,'女')
  	</insert>
  </mapper>
  ```

## 通过junit测试功能

- 示例代码：

  ```java
  //读取MyBatis的核心配置文件
  InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
  
  //创建SqlSessionFactoryBuilder对象
  SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new
  SqlSessionFactoryBuilder();
  
  //通过核心配置文件所对应的字节输入流创建工厂类SqlSessionFactory，生产SqlSession对象
  SqlSessionFactory sqlSessionFactory = sqlSessionFactoryBuilder.build(is);
  
  //创建SqlSession对象，此时通过SqlSession对象所操作的sql都必须手动提交或回滚事务
  //SqlSession sqlSession = sqlSessionFactory.openSession();
  //创建SqlSession对象，此时通过SqlSession对象所操作的sql都会自动提交
  SqlSession sqlSession = sqlSessionFactory.openSession(true);
  
  //通过代理模式创建UserMapper接口的代理实现类对象
  UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
  
  //调用UserMapper接口中的方法，就可以根据UserMapper的全类名匹配元素文件，通过调用的方法名匹配映射文件中的SQL标签，并执行标签中的SQL语句
  int result = userMapper.insertUser();
  
  //sqlSession.commit();
  System.out.println("结果："+result);
  ```

- SqlSession：代表**Java程序和数据库之间的会话**。（HttpSession是Java程序和浏览器之间的会话）
- SqlSessionFactory：是“生产”SqlSession的“工厂”。
- 用到了工厂模式：如果创建某一个对象，使用的过程基本固定，那么我们就可以把创建这个对象的相关代码封装到一个“工厂类”中，以后都使用这个工厂类来“生产”我们需要的对象。

## 加入log4j日志功能

- 加入依赖：

  ```xml
  <!-- log4j日志 -->
  <dependency>
  	<groupId>log4j</groupId>
  	<artifactId>log4j</artifactId>
  	<version>1.2.17</version>
  </dependency>
  ```

- 加入log4j的配置文件（log4j的配置文件名为log4j.xml，存放的位置是src/main/resources目录下）：

  ```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <!DOCTYPE log4j:configuration SYSTEM "log4j.dtd">
  <log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/">
  	<appender name="STDOUT" class="org.apache.log4j.ConsoleAppender">
  		<param name="Encoding" value="UTF-8" />
  		<layout class="org.apache.log4j.PatternLayout">
  			<param name="ConversionPattern" value="%-5p %d{MM-dd HH:mm:ss,SSS} %m (%F:%L) \n" />
  		</layout>
  	</appender>
  	<logger name="java.sql">
  		<level value="debug" />
  	</logger>
  	<logger name="org.apache.ibatis">
  		<level value="info" />
  	</logger>
  	<root>
  		<level value="debug" />
  		<appender-ref ref="STDOUT" />
  	</root>
  </log4j:configuration>
  ```

### 日志的级别

- FATAL(致命)>ERROR(错误)>WARN(警告)>INFO(信息)>DEBUG(调试)  从左到右打印的内容越来越详细

# 核心配置文件详解

- 核心配置文件中的标签必须按照固定的顺序书写：properties?,settings?,typeAliases?,typeHandlers?,objectFactory?,objectWrapperFactory?,reflectorFactory?,plugins?,environments?,databaseIdProvider?,mappers? 如果不按照这个顺序书写的话就会报错。

- 示例配置：

  ```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <!DOCTYPE configuration
  	PUBLIC "-//MyBatis.org//DTD Config 3.0//EN"
  	"http://MyBatis.org/dtd/MyBatis-3-config.dtd">
  
  <configuration>
      
  	<!--引入properties文件，此时就可以${属性名}的方式访问属性值-->
  	<properties resource="jdbc.properties"></properties>
      
  	<settings>
  		<!--将表中字段的下划线自动转换为驼峰-->
  		<setting name="mapUnderscoreToCamelCase" value="true"/>
  		<!--开启延迟加载-->
  		<setting name="lazyLoadingEnabled" value="true"/>
  	</settings>
      
  	<typeAliases>
  		<!--
  			typeAlias：设置某个具体的类型的别名
  			属性：
  			type：需要设置别名的类型的全类名
  			alias：设置此类型的别名，若不设置此属性，该类型拥有默认的别名，即类名且不区分大小写
  			若设置此属性，此时该类型的别名只能使用alias所设置的值
  		-->
  		<!--<typeAlias type="com.atguigu.mybatis.bean.User"></typeAlias>-->
  		<!--<typeAlias type="com.atguigu.mybatis.bean.User" alias="abc">
  </typeAlias>-->
  		<!--以包为单位，设置改包下所有的类型都拥有默认的别名，即类名且不区分大小写-->
  		<package name="com.atguigu.mybatis.bean"/>
  	</typeAliases>
      
  	<!--
  		environments：设置多个连接数据库的环境
  		属性：
  		default：设置默认使用的环境的id
  	-->
  	<environments default="mysql_test">
  		<!--
  			environment：设置具体的连接数据库的环境信息
  			属性：
  			id：设置环境的唯一标识，可通过environments标签中的default设置某一个环境的id，表示默认使用的环境
  		-->
  		<environment id="mysql_test">
  			<!--
  				transactionManager：设置事务管理方式
  				属性：
  				type：设置事务管理方式，type="JDBC|MANAGED"
  				type="JDBC"：设置当前环境的事务管理都必须手动处理
  				type="MANAGED"：设置事务被管理，例如spring中的AOP
  			-->
  			<transactionManager type="JDBC"/>
  			<!--
  				dataSource：设置数据源
  				属性：
  				type：设置数据源的类型，type="POOLED|UNPOOLED|JNDI"
  				type="POOLED"：使用数据库连接池，即会将创建的连接进行缓存，下次使用可以从缓存中直接获取，不需要重新创建
  				type="UNPOOLED"：不使用数据库连接池，即每次使用连接都需要重新创建
  				type="JNDI"：调用上下文中的数据源
  			-->
  			<dataSource type="POOLED">
  				<!--设置驱动类的全类名-->
  				<property name="driver" value="${jdbc.driver}"/>
  				<!--设置连接数据库的连接地址-->
  				<property name="url" value="${jdbc.url}"/>
  				<!--设置连接数据库的用户名-->
  				<property name="username" value="${jdbc.username}"/>
  				<!--设置连接数据库的密码-->
  				<property name="password" value="${jdbc.password}"/>
  			</dataSource>
  		</environment>
  	</environments>
      
  	<!--引入映射文件-->
  	<mappers>
  		<mapper resource="UserMapper.xml"/>
  		<!--
  			以包为单位，将包下所有的映射文件引入核心配置文件
  			注意：此方式必须保证mapper接口和mapper映射文件必须在相同的包下
  		-->
  		<package name="com.atguigu.mybatis.mapper"/>
  	</mappers>
      
  </configuration>
  ```

# MyBatis的增删改查

- 这里的例子是在mapper接口对应的xml文件中进行配置，**一般会将mapper中的方法签名复制到对应的xml文件中当作注释来辅助配置的编写**，除了在配置文件中进行配置外也可以使用注解进行开发。

## 添加

- 示例代码：

	```xml
	<!--int insertUser();-->
	<insert id="insertUser">
		insert into t_user values(null,'admin','123456',23,'男')
	</insert>
	```

## 删除

- 示例代码：

  ```xml
  <!--int deleteUser();-->
  <delete id="deleteUser">
  	delete from t_user where id = 7
  </delete>
  ```

## 修改

- 示例代码：

  ```xml
  <!--int updateUser();-->
  <update id="updateUser">
  	update t_user set username='ybc',password='123' where id = 6
  </update>
  ```

## 查询一个实体类对象

- 示例代码：

  ```xml
  <!--User getUserById();-->
  <select id="getUserById" resultType="com.atguigu.mybatis.bean.User">
  	select * from t_user where id = 2
  </select>
  ```

## 查询集合

- 示例代码：

  ```xml
  <!--List<User> getUserList();-->
  <select id="getUserList" resultType="com.atguigu.mybatis.bean.User">
  	select * from t_user
  </select>
  ```

## 注意事项

1. 查询的标签select必须设置属性**resultType或resultMap**，用于设置实体类和数据库表的映射关系，设置了这个mybatis才直到要把查出来的东西以什么样的规则放到哪里。
   - resultType：自动映射，用于属性名和表中字段名一致的情况，mybatis会把查出来的记录的字段按照名称（或是一定的映射关系，如下划线和驼峰之间的映射）对设置的实体类中的属性进行赋值。**注意：就算是查询结果有多条，也不能声明其类型为list，只需让方法的返回值为List即可，因为这个属性的作用是指定映射关系，所以无论返回值有多少，我们应该在其中声明需要进行映射的实体类而不是其容器。**
   - resultMap：自定义映射，用于一对多或多对一或字段名和属性名不一致的情况

2. **当查询的数据为多条时，不能使用实体类作为返回值，只能使用集合，否则会抛出异常
   TooManyResultsException**；但是若查询的数据只有一条，可以使用实体类或集合作为返回值

# MyBatis获取参数值的两种方式（重点）

- MyBatis获取参数值的两种方式：**${}** 和 **#{}**，${}的本质就是**字符串拼接**，#{}的本质就是**占位符赋值**
- **${}**使用字符串拼接的方式拼接sql，若为字符串类型或日期类型的字段进行赋值时，需要手动加单引号，**不会自动添加单引号**；但是**#{}**使用占位符赋值的方式拼接sql，此时为字符串类型或日期类型的字段进行赋值时，可以**自动添加单引号**。

## 单个字面量类型的参数

- 若mapper接口中的方法参数为单个的字面量类型此时可以使用\${}和#{}在大括号中间指定**以任意的名称**获取参数的值，注意${}需要手动加单引号

## 多个字面量类型的参数

- 若mapper接口中的方法参数为多个时，此时MyBatis会**自动将这些参数放在一个map集合中，以arg0,arg1...为键，以参数为值；以param1,param2...为键，以参数为值**；因此只需要通过\${}和#{}访问map集合的键就可以获取相对应的值，注意${}需要手动加单引号

## map集合类型的参数

- 若mapper接口中的方法需要的参数为多个时，此时可以**手动创建map集合并将其作为参数传入mapper中的方法中**，将这些数据放在map中只需要**通过\${}和#{}访问map集合的键**就可以获取相对应的值，注意${}需要手动加单引号

## 实体类类型的参数

- 若mapper接口中的方法参数为实体类对象时此时可以**使用\${}和#{}，通过访问实体类对象中的属性名**获取属性值，注意${}需要手动加单引号

## 使用@Param标识参数

- 可以**通过@Param注解标识mapper接口中的方法参数**，此时会将这些参数放在map集合中，**以@Param注解的value属性值为键，以参数为值；以param1,param2...为键，以参数为值**；只需要通过\${}和#{}访问map集合的键就可以获取相对应的值，注意${}需要手动加单引号
- 实际情况下mapper中的方法参数有很多种情况，**推荐都使用@Param注解对参数进行标识来实现一种统一的访问形式**。

# MyBatis的各种查询功能的实现

## 查询一个实体类对象

- 示例代码：

  ```java
  /**
  * 根据用户id查询用户信息
  * @param id
  * @return
  */
  User getUserById(@Param("id") int id);
  ```

  ```xml
  <!--User getUserById(@Param("id") int id);-->
  <select id="getUserById" resultType="User">
  	select * from t_user where id = #{id}
  </select>
  ```

## 查询一个list集合

- 示例代码：

  ```java
  /**
  * 查询所有用户信息
  * @return
  */
  List<User> getUserList();
  ```

  ```xml
  <!--List<User> getUserList();-->
  <select id="getUserList" resultType="User">
  	select * from t_user
  </select>
  ```

## 查询单个数据

- 示例代码：

  ```java
  /**
  * 查询用户的总记录数
  * @return
  * 在MyBatis中，对于Java中常用的类型都设置了类型别名
  * 例如：java.lang.Integer-->int|integer
  * 例如：int-->_int|_integer
  * 例如：Map-->map,List-->list
  */
  int getCount();
  ```

  ```xml
  <!--int getCount();-->
  <select id="getCount" resultType="_integer">
  	select count(id) from t_user
  </select>
  ```

## 查询一条数据为map集合

- 通过Map<String,Object>类型来接受查出来的记录，MyBatis会自动将转换后的字段名为key，字段对应的值为value存放到map中，不和List一样，**map类型需要在resultType属性中进行声明**，因为**map本身就表示一种处理映射关系的方式，可以作为一种规则被提供**，还是那句话，**resultType和resultMap是为了指定映射的方式，因此在填这个属性的时候一定要先想一想自己填的这个是否能为MyBatis准确地提供一种映射方式**，不然你懵机器也懵。

### 方式一

- 代码示例：

	```java
	/**
	* 查询所有用户信息为map集合
	* @return
	* 将表中的数据以map集合的方式查询，一条数据对应一个map；若有多条数据，就会产生多个map集合，此
	时可以将这些map放在一个list集合中获取
	*/
	List<Map<String, Object>> getAllUserToMap();
	```
	
	```xml
	<!--Map<String, Object> getAllUserToMap();-->
	<select id="getAllUserToMap" resultType="map">
		select * from t_user
	</select>
	```

### 方式二

- 代码示例：

  ```java
  /**
  * 查询所有用户信息为map集合
  * @return
  * 将表中的数据以map集合的方式查询，一条数据对应一个map；若有多条数据，就会产生多个map集合，并
  且最终要以一个map的方式返回数据，此时需要通过@MapKey注解设置map集合的键，值是每条数据所对应的
  map集合
  */
  @MapKey("id")
  Map<String, Object> getAllUserToMap();
  ```

  ```xml
  <!--Map<String, Object> getAllUserToMap();-->
  <select id="getAllUserToMap" resultType="map">
  	select * from t_user
  </select>
  结果：
  <!--
  {
  	1={password=123456, sex=男, id=1, age=23, username=admin},
  	2={password=123456, sex=男, id=2, age=23, username=张三},
  	3={password=123456, sex=男, id=3, age=23, username=张三}
  }
  -->
  ```

# 特殊SQL的执行

## 模糊查询

```java
/**
* 测试模糊查询
* @param mohu
* @return
*/
List<User> testMohu(@Param("mohu") String mohu);
```

```xml
<!--List<User> testMohu(@Param("mohu") String mohu);-->
<select id="testMohu" resultType="User">
	<!--select * from t_user where username like '%${mohu}%' 会有sql注入的风险，不推荐使用-->
	<!--select * from t_user where username like concat('%',#{mohu},'%')-->
	select * from t_user where username like "%"#{mohu}"%"<!--推荐使用-->
</select>
```

## 批量删除

```java
/**
* 批量删除
* @param ids
* @return
*/
int deleteMore(@Param("ids") String ids);
```

```xml
<!--int deleteMore(@Param("ids") String ids);-->
<delete id="deleteMore">
	delete from t_user where id in (${ids})
</delete>
```

## 动态设置表名

```java
/**
* 动态设置表名，查询所有的用户信息
* @param tableName
* @return
*/
List<User> getAllUser(@Param("tableName") String tableName);
```

```xml
<!--List<User> getAllUser(@Param("tableName") String tableName);-->
<select id="getAllUser" resultType="User">
	select * from ${tableName}<!--注意表名是没有单引号的，所以这个地方不适合用#{}-->
</select>
```

## 添加功能获取自增的主键

- 有表：t_clazz(clazz_id,clazz_name)和t_student(student_id,student_name,clazz_id)
- 要求：
  1. 添加班级信息
  2. 获取新添加的班级的id
  3. 为班级分配学生，即将某学的班级id修改为新添加的班级的id

```java
/**
* 添加用户信息
* @param user
* @return
* useGeneratedKeys：设置使用自增的主键
* keyProperty：因为增删改有统一的返回值是受影响的行数，因此只能将获取的自增的主键放在传输的参
数user对象的某个属性中
*/
int insertUser(User user);
```

```xml
<!--int insertUser(User user);-->
<insert id="insertUser" useGeneratedKeys="true" keyProperty="id">
	insert into t_user values(null,#{username},#{password},#{age},#{sex})
</insert>
```

# 自定义映射resultMap

## resultMap处理字段和属性的映射关系

- 若**字段名和实体类中的属性名不一致或是不能通过特定的映射方式（如下划线映射驼峰）进行映射**，则可以通过resultMap设置自定义映射。

- 实例代码：

  ```xml
  <!--
  	resultMap：设置自定义映射
  
  	属性：
  	id：表示自定义映射的唯一标识
  	type：查询的数据要映射的实体类的类型
  
  	子标签：
  	id：设置主键的映射关系
  	result：设置普通字段的映射关系
  	association：设置多对一的映射关系
  	collection：设置一对多的映射关系
  
  	属性：
  	property：设置映射关系中实体类中的属性名
  	column：设置映射关系中表中的字段名
  -->
  <resultMap id="userMap" type="User">
  	<id property="id" column="id"></id>
  	<result property="userName" column="user_name"></result>
  	<result property="password" column="password"></result>
  	<result property="age" column="age"></result>
  	<result property="sex" column="sex"></result>
  </resultMap>
  <!--List<User> testMohu(@Param("mohu") String mohu);-->
  <select id="testMohu" resultMap="userMap">
  	<!--select * from t_user where username like '%${mohu}%'-->
  	select id,user_name,password,age,sex from t_user where user_name like concat('%',#{mohu},'%')
  </select>
  ```

- 若字段名和实体类中的属性名不一致，但是字段名符合数据库的规则（使用_），实体类中的属性名符合Java的规则（使用驼峰），此时也可通过以下两种方式处理字段名和实体类中的属性的映射关系：
  1. 可以通过**为字段起别名**的方式，保证和实体类中的属性名保持一致
  2. 可以在MyBatis的核心配置文件中设置一个全局配置信息**mapUnderscoreToCamelCase=true**，可以在查询表中数据时，自动将_类型的字段名转换为驼峰，例如：字段名user_name，设置了mapUnderscoreToCamelCase，此时字段名就会转换为
     userName

## 多对一映射处理

- 要求查询员工信息以及员工所对应部门的信息，员工和员工所属部门是多对一的关系。
- 其中这个**“一”可以在resultMap中用association表示**。

### 单步查询并用级联方式处理映射关系

```xml
<resultMap id="empDeptMap" type="Emp">
	<id column="eid" property="eid"></id>
	<result column="ename" property="ename"></result>
	<result column="age" property="age"></result>
	<result column="sex" property="sex"></result>
	<result column="did" property="dept.did"></result>
	<result column="dname" property="dept.dname"></result>
</resultMap>
<!--Emp getEmpAndDeptByEid(@Param("eid") int eid);-->
<select id="getEmpAndDeptByEid" resultMap="empDeptMap">
	select emp.*,dept.* from t_emp emp left join t_dept dept on emp.did = dept.did where emp.eid = #{eid}
</select>
```

### 使用association处理映射关系

```xml
<resultMap id="empDeptMap" type="Emp">
	<id column="eid" property="eid"></id>
	<result column="ename" property="ename"></result>
	<result column="age" property="age"></result>
	<result column="sex" property="sex"></result>
	<association property="dept" javaType="Dept">
		<id column="did" property="did"></id>
		<result column="dname" property="dname"></result>
	</association>
</resultMap>
<!--Emp getEmpAndDeptByEid(@Param("eid") int eid);-->
<select id="getEmpAndDeptByEid" resultMap="empDeptMap">
	select emp.*,dept.* from t_emp emp left join t_dept dept on emp.did = dept.did where emp.eid = #{eid}
</select>
```

### 分步查询

- 这样做往往效率比较高

- 首先查询员工信息：

  ```java
  /**
  * 通过分步查询查询员工信息
  * @param eid
  * @return
  */
  Emp getEmpByStep(@Param("eid") int eid);
  ```

  ```xml
  <resultMap id="empDeptStepMap" type="Emp">
  	<id column="eid" property="eid"></id>
  	<result column="ename" property="ename"></result>
  	<result column="age" property="age"></result>
  	<result column="sex" property="sex"></result>
  	<!--
  		select：设置分步查询，查询某个属性的值的sql的标识（namespace.sqlId）
  		column：将sql以及查询结果中的某个字段设置为分步查询的条件
  	-->
  	<association property="dept" select="com.atguigu.MyBatis.mapper.DeptMapper.getEmpDeptByStep" column="did"><!--在这里配置了下一步要进行的查询语句，查询出来的内容会被映射到这个association中-->
  	</association>
  </resultMap>
  <!--Emp getEmpByStep(@Param("eid") int eid);-->
  <select id="getEmpByStep" resultMap="empDeptStepMap">
  	select * from t_emp where eid = #{eid}
  </select>
  ```

- 然后根据员工所对应的部门id查询部门信息

  ```java
  /**
  * 分步查询的第二步：根据员工所对应的did查询部门信息
  * @param did
  * @return
  */
  Dept getEmpDeptByStep(@Param("did") int did);
  ```

  ```xml
  <!--Dept getEmpDeptByStep(@Param("did") int did);-->
  <select id="getEmpDeptByStep" resultType="Dept">
  	select * from t_dept where did = #{did}
  </select>
  ```

## 一对多映射处理

- 要求查询部门信息以及部门中的所有员工信息，部门和部门下的员工是一对多的关系。

- 这个“多”可以在resultMap中用collection表示

### 单步查询并使用collection处理映射关系

```java
/**
* 根据部门id查新部门以及部门中的员工信息
* @param did
* @return
*/
Dept getDeptEmpByDid(@Param("did") int did);
```

```xml
<resultMap id="deptEmpMap" type="Dept">
	<id property="did" column="did"></id>
	<result property="dname" column="dname"></result>
	<!--
		ofType：设置collection标签所处理的集合属性中存储数据的类型
	-->
	<collection property="emps" ofType="Emp">
		<id property="eid" column="eid"></id>
		<result property="ename" column="ename"></result>
		<result property="age" column="age"></result>
		<result property="sex" column="sex"></result>
	</collection>
</resultMap>
<!--Dept getDeptEmpByDid(@Param("did") int did);-->
<select id="getDeptEmpByDid" resultMap="deptEmpMap">
	select dept.*,emp.* from t_dept dept left join t_emp emp on dept.did = emp.did where dept.did = #{did}
</select>
```

### 分步查询

- 这样做往往效率比较高

- 首先查询部门信息

  ```java
  /**
  * 分步查询部门和部门中的员工
  * @param did
  * @return
  */
  Dept getDeptByStep(@Param("did") int did);
  ```

  ```xml
  <resultMap id="deptEmpStep" type="Dept">
  	<id property="did" column="did"></id>
  	<result property="dname" column="dname"></result>
  	<collection property="emps" fetchType="eager" select="com.atguigu.MyBatis.mapper.EmpMapper.getEmpListByDid" column="did">
  	</collection>
  </resultMap>
  <!--Dept getDeptByStep(@Param("did") int did);-->
  <select id="getDeptByStep" resultMap="deptEmpStep">
  	select * from t_dept where did = #{did}
  </select>
  ```

- 根据部门id查询部门中的所有员工

  ```java
  /**
  * 根据部门id查询员工信息
  * @param did
  * @return
  */
  List<Emp> getEmpListByDid(@Param("did") int did);
  ```

  ```xml
  <!--List<Emp> getEmpListByDid(@Param("did") int did);-->
  <select id="getEmpListByDid" resultType="Emp">
  	select * from t_emp where did = #{did}
  </select>
  ```

## 分步查询的优点

- 可以实现延迟加载，但是必须在核心配置文件中设置全局配置信息：
  1. lazyLoadingEnabled：延迟加载的全局开关。当开启时，所有关联对象都会延迟加载
  2. aggressiveLazyLoading：当开启时，任何方法的调用都会加载该对象的所有属性。 否则，每个属性会按需加载

- 设置完以上的配置后，就可以实现按需加载，获取的数据是什么，就只会执行相应的sql。此时**可通过association和collection中的fetchType属性设置当前的分步查询是否使用延迟加载**，**fetchType="lazy(延迟加载)|eager(立即加载)"**

# 动态SQL

- Mybatis框架的动态SQL技术是一种**根据特定条件动态拼装SQL语句的功能**，它存在的意义是为了解决拼接SQL语句字符串时的痛点问题。

## if

- if标签**可通过test属性的表达式进行判断，若表达式的结果为true，则标签中的内容会执行；反之标签中的内容不会执行**。

- 要注意可能会出现冗余的关键字影响mybatis解析代码。

- 示例代码：

  ```xml
  <!--List<Emp> getEmpListByMoreTJ(Emp emp);-->
  <select id="getEmpListByMoreTJ" resultType="Emp">
  	select * from t_emp where 1=1<!--防止出现冗余的and-->
  	<if test="ename != '' and ename != null">
  		and ename = #{ename}
  	</if>
  	<if test="age != '' and age != null">
  		and age = #{age}
  	</if>
  	<if test="sex != '' and sex != null">
  		and sex = #{sex}
  	</if>
  </select>
  ```

## where

- 是消除冗余的关键字的另外一种可行的方式

- where和if一般结合使用：
  1. 若where标签中的if条件都不满足，则where标签没有任何功能，即不会添加where关键字
  2. 若where标签中的if条件满足，则where标签会自动添加where关键字，并将条件最前方多余的and去
  3. **where标签不能去掉条件最后多余的and**

- 示例代码：

  ```xml
  <select id="getEmpListByMoreTJ2" resultType="Emp">
  	select * from t_emp
  	<where>
  		<if test="ename != '' and ename != null">
  			ename = #{ename}
  		</if>
  		<if test="age != '' and age != null">
  			and age = #{age}
  		</if>
  		<if test="sex != '' and sex != null">
  			and sex = #{sex}
  		</if>
  	</where>
  </select>
  ```

## trim

- trim用于**去掉或者添加标签中的内容**，常用属性：
  1. prefix：在trim标签中的内容的前面添加某些内容
  2. prefixOverrides：在trim标签中的内容的前面去掉某些内容
  3. suffix：在trim标签中的内容的后面添加某些内容
  4. suffixOverrides：在trim标签中的内容的后面去掉某些内容

- 示例代码：

  ```xml
  <select id="getEmpListByMoreTJ" resultType="Emp">
  	select * from t_emp
  	<trim prefix="where" suffixOverrides="and">
  		<if test="ename != '' and ename != null">
  			ename = #{ename} and
  		</if>
  		<if test="age != '' and age != null">
  			age = #{age} and
  		</if>
  		<if test="sex != '' and sex != null">
  			sex = #{sex}
  		</if>
  	</trim>
  </select>
  ```

## choose、when、otherwise

- choose、when、otherwise类似于if...else if...else

- 示例代码：

  ```xml
  <!--List<Emp> getEmpListByChoose(Emp emp);-->
  <select id="getEmpListByChoose" resultType="Emp">
  	select <include refid="empColumns"></include> from t_emp
  	<where>
  		<choose>
  			<when test="ename != '' and ename != null">
  				ename = #{ename}
  			</when>
  			<when test="age != '' and age != null">
  				age = #{age}
  			</when>
  			<when test="sex != '' and sex != null">
  				sex = #{sex}
  			</when>
  			<when test="email != '' and email != null">
  				email = #{email}
  			</when>
  		</choose>
  	</where>
  </select>
  ```

## foreach

- 常用属性：
  1. collection：设置要循环的数组或集合
  2. item：表示集合或数组中的每一个数据
  3. separator：设置循环体之间的分隔符
  4. open：设置foreach标签中的内容的开始符
  5. close：设置foreach标签中的内容的结束符

- 示例代码：

  ```xml
  <!--int insertMoreEmp(List<Emp> emps);-->
  <insert id="insertMoreEmp">
  	insert into t_emp values
  	<foreach collection="emps" item="emp" separator=",">
  		(null,#{emp.ename},#{emp.age},#{emp.sex},#{emp.email},null)
  	</foreach>
  </insert>
  <!--int deleteMoreByArray(int[] eids);-->
  <delete id="deleteMoreByArray">
  	delete from t_emp where
  	<foreach collection="eids" item="eid" separator="or">
  		eid = #{eid}
  	</foreach>
  </delete>
  <!--int deleteMoreByArray(int[] eids);-->
  <delete id="deleteMoreByArray">
  	delete from t_emp where eid in
  	<foreach collection="eids" item="eid" separator="," open="(" close=")">
  		#{eid}
  	</foreach>
  </delete>
  ```

## SQL片段

- sql片段，可以记录一段公共sql片段，在使用的地方通过include标签进行引入

- 代码示例：

  ```xml
  <sql id="empColumns">
      eid,ename,age,sex,did
  </sql>
  
  select <include refid="empColumns"></include> from t_emp
  ```

# MyBatis的缓存

## MyBatis的一级缓存

- 一级缓存是SqlSession级别的，**通过同一个SqlSession查询的数据会被缓存**，下次查询相同的数据，就会从缓存中直接获取，不会从数据库重新访问。

- 使一级缓存失效的四种情况（还是挺容易想到的）：
  1. 不同的SqlSession对应不同的一级缓存
  2. 同一个SqlSession但是查询条件不同
  3. 同一个SqlSession两次查询期间执行了任何一次增删改操作
  4. 同一个SqlSession两次查询期间手动清空了缓存

## MyBatis的二级缓存

- 二级缓存是SqlSessionFactory级别，**通过同一个SqlSessionFactory创建的SqlSession查询的结果会被缓存**；此后若再次执行相同的查询语句，结果就会从缓存中获取
- 二级缓存开启的条件：
  1. 在核心配置文件中，设置**全局配置属性cacheEnabled="true"**，**默认为true**，不需要设置
  2. 在映射文件中设置标签\<cache />
  3. 二级缓存必须在SqlSession关闭或提交之后有效
  4. 查询的数据所转换的实体类类型**必须实现序列化的接口**

- 使二级缓存失效的情况：**两次查询之间执行了任意的增删改，会使一级和二级缓存同时失效**

## 二级缓存的相关配置

- 在mapper配置文件中添加的cache标签可以设置一些属性：

  1. eviction属性：缓存回收策略

     **LRU（Least Recently Used）** – 最近最少使用的：移除最长时间不被使用的对象。
     **FIFO（First in First out）** – 先进先出：按对象进入缓存的顺序来移除它们。
     **SOFT – 软引用**：移除基于垃圾回收器状态和软引用规则的对象。
     **WEAK – 弱引用**：更积极地移除基于垃圾收集器状态和弱引用规则的对象。
     **默认的是 LRU**。

  2. flushInterval属性：刷新间隔，单位毫秒
     **默认情况是不设置，也就是没有刷新间隔，缓存仅仅调用语句时刷新**

  3. size属性：引用数目，正整数
     代表**缓存最多可以存储多少个对象**，太大容易导致内存溢出

  4. readOnly属性：只读，true/false
     true：只读缓存；**会给所有调用者返回缓存对象的相同实例**。因此**这些对象不能被修改**。这提供了很重要的**性能优势**。
     false：读写缓存；会**返回缓存对象的拷贝（通过序列化）**。这会**慢一些**，但是**安全**，因此默认是false。

## MyBatis缓存查询的顺序

- **先查询二级缓存**，因为**二级缓存中可能会有其他程序已经查出来的数据，可以拿来直接使用**。
- 如果二级缓存没有命中，再查询一级缓存
- 如果一级缓存也没有命中，则查询数据库
- **SqlSession关闭之后，一级缓存中的数据会写入二级缓存**

## 整合第三方缓存EHCache

### 添加依赖

```xml
<!-- Mybatis EHCache整合包 -->
<dependency>
	<groupId>org.mybatis.caches</groupId>
	<artifactId>mybatis-ehcache</artifactId>
	<version>1.2.1</version>
</dependency>
<!-- slf4j日志门面的一个具体实现 -->
<dependency>
	<groupId>ch.qos.logback</groupId>
	<artifactId>logback-classic</artifactId>
	<version>1.2.3</version>
</dependency>
```

### 各jar包的功能

| jar包名称       | 作用                            |
| --------------- | ------------------------------- |
| mybatis-ehcache | Mybatis和EHCache的整合包        |
| ehcache         | EHCache核心包                   |
| slf4j-api       | SLF4J日志门面包                 |
| logback-classic | 支持SLF4J门面接口的一个具体实现 |

### 创建EHCache的配置文件ehcache.xml

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:noNamespaceSchemaLocation="../config/ehcache.xsd">
	<!-- 磁盘保存路径 -->
	<diskStore path="D:\atguigu\ehcache"/>
	<defaultCache
		maxElementsInMemory="1000"
		maxElementsOnDisk="10000000"
		eternal="false"
		overflowToDisk="true"
		timeToIdleSeconds="120"
		timeToLiveSeconds="120"
		diskExpiryThreadIntervalSeconds="120"
		memoryStoreEvictionPolicy="LRU">
	</defaultCache>
</ehcache>
```

### 设置二级缓存的类型

```xml
<cache type="org.mybatis.caches.ehcache.EhcacheCache"/>
```

### 加入logback日志

- 存在SLF4J时，作为简易日志的log4j将失效，此时我们需要借助SLF4J的具体实现logback来打印日志。创建**logback的配置文件logback.xml**

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <configuration debug="true">
  	<!-- 指定日志输出的位置 -->
  	<appender name="STDOUT"
  		class="ch.qos.logback.core.ConsoleAppender">
  		<encoder>
  			<!-- 日志输出的格式 -->
  			<!-- 按照顺序分别是：时间、日志级别、线程名称、打印日志的类、日志主体内容、换行 -->
  			<pattern>[%d{HH:mm:ss.SSS}] [%-5level] [%thread][%logger][%msg]%n</pattern>
  		</encoder>
  	</appender>
  	<!-- 设置全局日志级别。日志级别按顺序分别是：DEBUG、INFO、WARN、ERROR -->
  	<!-- 指定任何一个日志级别都只打印当前级别和后面级别的日志。 -->
  	<root level="DEBUG">
  		<!-- 指定打印日志的appender，这里通过“STDOUT”引用了前面配置的appender -->
  		<appender-ref ref="STDOUT" />
  	</root>
  	<!-- 根据特殊需求指定局部日志级别 -->
  	<logger name="com.atguigu.crowd.mapper" level="DEBUG"/>
  </configuration>
  ```

### EHCache配置文件说明

| 属性名                          | 是否必须 | 作用                                                         |
| ------------------------------- | -------- | ------------------------------------------------------------ |
| maxElementsInMemory             | 是       | 在内存中缓存的element的最大数目                              |
| maxElementsOnDisk               | 是       | 在磁盘上缓存的element的最大数目，若是0表示无穷大             |
| eternal                         | 是       | 设定缓存的elements是否永远不过期。 如果为true，则缓存的数据始终有效， 如果为false那么还要根据timeToIdleSeconds、timeToLiveSeconds判断 |
| overflowToDisk                  | 是       | 设定当内存缓存溢出的时候是否将过期的element缓存到磁盘上      |
| timeToIdleSeconds               | 否       | 当缓存在EhCache中的数据前后两次访问的时间超过timeToIdleSeconds的属性取值时， 这些数据便会删除，默认值是0,也就是可闲置时间无穷大 |
| timeToLiveSeconds               | 否       | 缓存element的有效生命期，默认是0.,也就是element存活时间无穷大 |
| diskSpoolBufferSizeMB           | 否       | DiskStore(磁盘缓存)的缓存区大小。默认是30MB。每个Cache都应该有自己的一个缓冲区 |
| diskPersistent                  | 否       | 在VM重启的时候是否启用磁盘保存EhCache中的数据，默认是false。 |
| diskExpiryThreadIntervalSeconds | 否       | 磁盘缓存的清理线程运行间隔，默认是120秒。每个120s， 相应的线程会进行一次EhCache中数据的清理工作 |
| memoryStoreEvictionPolicy       | 否       | 当内存缓存达到最大，有新的element加入的时候， 移除缓存中element的策略。 默认是LRU（最近最少使用），可选的有LFU（最不常使用）和FIFO（先进先出） |

# MyBatis的逆向工程

- 正向工程：**先创建Java实体类，由框架负责根据实体类生成数据库表**。Hibernate是支持正向工程的。
- 逆向工程：**先创建数据库表，由框架负责根据数据库表**，反向生成如下资源：
  1. Java实体类
  2. Mapper接口
  3. Mapper映射文件

## 创建逆向工程的步骤

### 添加依赖和插件

```xml
<!-- 依赖MyBatis核心包 -->
<dependencies>
	<dependency>
		<groupId>org.mybatis</groupId>
		<artifactId>mybatis</artifactId>
		<version>3.5.7</version>
	</dependency>
</dependencies>

<!-- 控制Maven在构建过程中相关配置 -->
<build>
    
	<!-- 构建过程中用到的插件 -->
	<plugins>
        
		<!-- 具体插件，逆向工程的操作是以构建过程中插件形式出现的 -->
		<plugin>
			<groupId>org.mybatis.generator</groupId>
			<artifactId>mybatis-generator-maven-plugin</artifactId>
			<version>1.3.0</version>
            
			<!-- 插件的依赖 -->
			<dependencies>
				<!-- 逆向工程的核心依赖 -->
				<dependency>
					<groupId>org.mybatis.generator</groupId>
					<artifactId>mybatis-generator-core</artifactId>
					<version>1.3.2</version>
				</dependency>
                
				<!-- 数据库连接池 -->
				<dependency>
					<groupId>com.mchange</groupId>
					<artifactId>c3p0</artifactId>
					<version>0.9.2</version>
				</dependency>
                
				<!-- MySQL驱动 -->
				<dependency>
					<groupId>mysql</groupId>
					<artifactId>mysql-connector-java</artifactId>
					<version>5.1.8</version>
				</dependency>
			</dependencies>
		</plugin>
	</plugins>
</build>
```

### 创建MyBatis的核心配置文件

- 前面写过了

### 创建逆向工程的配置文件

- 文件名必须是：**generatorConfig.xml**

- 代码示例：

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE generatorConfiguration 
  	PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
  	"http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
  <generatorConfiguration>
  	<!--
  		targetRuntime: 执行生成的逆向工程的版本
  		MyBatis3Simple: 生成基本的CRUD（清新简洁版）
  		MyBatis3: 生成带条件的CRUD（奢华尊享版）
  	-->
  	<context id="DB2Tables" targetRuntime="MyBatis3Simple">
  		<!-- 数据库的连接信息 -->
  		<jdbcConnection driverClass="com.mysql.jdbc.Driver"
  			connectionURL="jdbc:mysql://localhost:3306/mybatis"
  			userId="root"
  			password="123456">
  		</jdbcConnection>
  		<!-- javaBean的生成策略-->
  		<javaModelGenerator targetPackage="com.atguigu.mybatis.bean" targetProject=".\src\main\java">
  			<property name="enableSubPackages" value="true" />
  			<property name="trimStrings" value="true" />
  		</javaModelGenerator>
  		<!-- SQL映射文件的生成策略 -->
  		<sqlMapGenerator targetPackage="com.atguigu.mybatis.mapper"
  targetProject=".\src\main\resources">
  			<property name="enableSubPackages" value="true" />
  		</sqlMapGenerator>
  		<!-- Mapper接口的生成策略 -->
  		<javaClientGenerator type="XMLMAPPER" targetPackage="com.atguigu.mybatis.mapper" targetProject=".\src\main\java">
  			<property name="enableSubPackages" value="true" />
  		</javaClientGenerator>
  		<!-- 逆向分析的表 -->
  		<!-- tableName设置为*号，可以对应所有表，此时不写domainObjectName -->
  		<!-- domainObjectName属性指定生成出来的实体类的类名 -->
  		<table tableName="t_emp" domainObjectName="Emp"/>
  		<table tableName="t_dept" domainObjectName="Dept"/>
  	</context>
  </generatorConfiguration>
  ```

### 执行MBG插件的generate目标

![image-20220923211033152](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220923211033152.png)

- 效果：

  ![image-20220923211049760](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220923211049760.png)

## QBC查询

- 示例代码：

  ```java
  @Test
  public void testMBG() throws IOException {
  	InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
  	SqlSession sqlSession = new SqlSessionFactoryBuilder().build(is).openSession(true);
  	EmpMapper mapper = sqlSession.getMapper(EmpMapper.class);
  	EmpExample empExample = new EmpExample();
  	//创建条件对象，通过andXXX方法为SQL添加查询添加，每个条件之间是and关系
  empExample.createCriteria().andEnameLike("a").andAgeGreaterThan(20).andDidIsNotNull();
  	//将之前添加的条件通过or拼接其他条件
  	empExample.or().andSexEqualTo("男");
  	List<Emp> list = mapper.selectByExample(empExample);
  	for (Emp emp : list) {
  		System.out.println(emp);
  	}
  }
  ```

# 分页插件

## 分页插件配置步骤

### 添加依赖

```xml
<!-- https://mvnrepository.com/artifact/com.github.pagehelper/pagehelper -->
<dependency>
	<groupId>com.github.pagehelper</groupId>
	<artifactId>pagehelper</artifactId>
	<version>5.2.0</version>
</dependency>
```

### 配置分页插件

- 在MyBatis的核心配置文件中配置插件：

  ```xml
  <plugins>
  	<!--设置分页插件-->
  	<plugin interceptor="com.github.pagehelper.PageInterceptor"></plugin>
  </plugins>
  ```

## 分页插件的使用

- 在**查询功能之前**使用**PageHelper.startPage(int pageNum, int pageSize)**开启分页功能：
  1. pageNum：表示当前页的页码
  2. pageSize：表示每页显示的条数

- 在**查询获取list集合之后**，使用**PageInfo\<T> pageInfo = new PageInfo<>(List\<T> list, int navigatePages)**获取分页相关数据：
  1. list：分页之后的数据
  2. navigatePages：导航分页的页码数

- 分页相关数据示例：

  ```
  PageInfo{
  pageNum=8, pageSize=4, size=2, startRow=29, endRow=30, total=30, pages=8,
  list=Page{count=true, pageNum=8, pageSize=4, startRow=28, endRow=32, total=30,pages=8, reasonable=false, pageSizeZero=false},
  prePage=7, nextPage=0, isFirstPage=false, isLastPage=true, hasPreviousPage=true,hasNextPage=false, navigatePages=5,navigateFirstPage4, navigateLastPage8,
  navigatepageNums=[4, 5, 6, 7, 8]
  }
  ```

- 分页数据中的常用数据，可以通过这些数据的组合来渲染页面：
  1. pageNum：当前页的页码
  2. pageSize：每页显示的条数
  3. size：当前页显示的真实条数
  4. total：总记录数
  5. pages：总页数
  6. prePage：上一页的页码
  7. nextPage：下一页的页码
  8. isFirstPage/isLastPage：是否为第一页/最后一页
  9. hasPreviousPage/hasNextPage：是否存在上一页/下一页
  10. navigatePages：导航分页的页码数
  11. navigatePageNums：导航分页的页码，如[12,3,4,5]
