---
title: Java从入门到入土
date: 2022-06-03 22:19:17
tags: [Java]
---

<meta name="referrer" content="no-referrer"/>

# java概述

## JDK

​	即Java Development Kit，是Java开发工具包，其中包含了JRE和一些开发中可能用到的工具（比如Java的编译器Javac等）。

## JRE

​	即Java Runtime Environment，是Java的运行环境，其内部包含JVM和一些类库。

## JVM

​	即Java Virtual Machine，是Java虚拟机，Java程序运行在这个上面，引入它使得Java程序跨平台时无需修改和重新编译即可运行，后面会有对JVM的详解。

## JVM、JRE、JDK的关系

![image-20220604193448518](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220604193448518.png)

## Java的应用体系

### JavaSE（J2SE）

​	Java Platform Standard Edition，即Java平台标准版，用于开发和部署桌面、服务器以及嵌入设备和实时环境中的Java应用程序。

### JavaEE（J2EE）

​	Java Platform Enterprise Edition，是Java的企业级应用，在JavaSE的基础上搭建而成。

### JavaME（J2ME）

​	Java Platform Micro Edition，主要针对消费类电子产品如手机、导航、机顶盒等设备进行开发。

# Java文档注释

​	用该方法写成的注释可以被javadoc.exe进行解析并生成相应报告，主要用来告知别人程序的信息及各方法的用途等，生成一套以网页文件形式体现的该程序的说明文档。

语法：

```java
/**
@author <指定java程序的作者>
@version <指定源文件的版本>
......
*/
```

# Java中的名称命名规范

## 包名

多单词组成时所有字母都小写：xxyy

## 类名、接口名

多单词组成时，所有单词的首字母大写：XxYy

## 变量名、方法名

多单词组成时，第一个单词首字母小写，第二个单词开始每个单词首字母大写：xxYyZz

## 常量名

所有字母都大写。多单词时每个单词用下划线连接：XX_YY_ZZ

# Java面向对象

## Java面向对象学习的三条主线

1、Java类及类的成员：属性、方法、构造器、代码块、内部类

2、面向对象的四大特征：**抽象性、封装性、继承性、多态性**

3、其它关键字：this、super、static、final、abstract、interface、package、import等



# Java的异常分类

- 今天是2022年的9月13号啊，今天我刚明白过来java的异常分类到底是个什么意思，实在是惭愧惭愧。
- 众所周知，java的异常分为**非受检异常（运行时异常）**和**受检异常（编译时异常）**。
- 非受检异常有**Error及其子类、RuntimeException及其子类**，剩下的都是受检异常。
- 这个**受检异常**是个什么意思呢，就是说你这个异常，**在编译阶段会被IDE亲切的提醒你要显式地处理它**，因为Java觉得你这个地方可能会出现异常，这也是它被称为编译时异常的原因，因为如果你不显式处理他，你的代码就过不了编译。
- 再看**非受检异常**，它一般是因为你的**代码逻辑出了问题，从而导致了java代码在运行时出现了问题，这个问题被jvm发现了，所以jvm要抛出异常提醒你这个地方出问题了，而这种异常一般是不会在编译阶段被Java发现的**，毕竟Java的分析能力是有限的，总不能先预运行一下找找异常存不存在吧，那样效率也太低了。
- 直到今天我才分清这俩的区别，之前我一直以为所有被抛出并打印到终端上的都是受检异常而非受检异常就是运行时遇到了程序直接寄了啥也不打印的那种，现在想想这个想法也太逆天了。

# Java的输入输出流

# Java流式编程

- 这是Java8中新支持的编程范式，我觉得很优雅，所以记录一下。
- 流式操作，是 Java 8除了Lambda表达式外的又一重大改变。**学习流式操作，就是学习java.util.stream包下的API，我们称之为Stream API**，它把真正的函数式编程引入到了 Java 中。
- 本小节我们将了解到**什么是Stream**，**为什么使用Stream API**， **流式操作的执行流程**，**如何实例化Stream**，**Stream的中间操作**、**Stream的终止操作**等内容。
- **基本上是用这个Stream操作来代替对集合的迭代操作的**，但是效率比for循环稍低。

## 什么是Stream

- Stream是数据渠道，**用于操作数据源所生成的元素序列，它可以实现对集合（Collection）的复杂操作**，例如**查找、替换、过滤和映射数据等操作**。
- 我们**这里说的Stream不同于java的输入输出流**。另外，Collection 是一种静态的数据结构，存储在内存中，而Stream是用于计算的，通过CPU实现计算。注意不要混淆。
- `Stream`**自己不会存储数据**；`Stream`**不会改变源对象，而是返回一个新的持有结果的`Stream`（不可变性）**；`Stream`**操作是延迟执行的**（这一点将在后面介绍）。

## 为什么使用Stream API

- 我们在实际开发中，项目中的很多数据都来源于关系型数据库（例如 MySQL、Oracle 数据库），我们使用`SQL`的条件语句就可以实现对数据的筛选、过滤等等操作；
- 但也有很多数据来源于非关系型数据库（`Redis`、`MongoDB`等），想要处理这些数据，往往需要在 Java 层面去处理。
- **使用`Stream API`对集合中的数据进行操作，就类似于 SQL 执行的数据库查询**。也**可以使用`Stream API`来执行并行操作**。简单来说，**`Stream API`提供了一种高效且易于使用的处理数据的方式**。

## 流式操作的执行流程

- 流式操作通常分为以下3个步骤：

  1. **创建`Stream`对象**：**通过一个数据源（例如集合、数组），获取一个流**；
  2. **中间操作**：一个**中间的链式操作，对数据源的数据进行处理（例如过滤、排序等），直到执行终止操作才执行**；
  3. **终止操作**：**一旦执行终止操作，就执行中间的链式操作，并产生结果**。

- 下图展示了`Stream`的执行流程：

  ![image-20221108201744658](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221108201744658.png)

- 接下来我们就按照这3个步骤的顺序来展开学习`Stream API`。

## Stream对象的创建

- 有4种方式来创建`Stream`对象

### 通过集合创建Stream

- Java 8 的**`java.util.Collection` **接口被扩展，提供了两个获取流的默认方法：
  1. **`default Stream<E> stream()`**：返回一个**串行流（顺序流）**；
  2. **`default Stream<E> parallelStream()`**：返回一个**并行流**。

- 代码示例：

  ```java
  // 创建一个集合，并添加几个元素
  List<String> stringList = new ArrayList<>();
  stringList.add("hello");
  stringList.add("world");
  stringList.add("java");
  ​
  // 通过集合获取串行 stream 对象
  Stream<String> stream = stringList.stream();
  // 通过集合获取并行 stream 对象
  Stream<String> personStream = stringList.parallelStream();
  ```

- 串行流并行流的区别是：**串行流从集合中取数据是按照集合的顺序的；而并行流是并行操作的，获取到的数据是无序的**。

### 通过数组创建Stream

- Java 8 中的**`java.util.Arrays`的静态方法`stream()`可以获取数组流**：

  - **`static <T> Stream<T> stream(T[] array)`**：返回一个数组流。

- 此外，`stream()`还有几个重载方法，能够**处理对应的基本数据类型的数组**：

  - **`public static IntStream stream(int[] array)`**：返回以指定数组作为其源的连续`IntStream`；
  - **`public static LongStream stream(long[] array)`**：返回以指定数组作为其源的连续`LongStream`；
  - **`public static DoubleStream stream(double[] array)`**：返回以指定数组作为其源的连续`DoubleStream`。
  
- 代码示例：

  ```java
  import java.util.Arrays;
  import java.util.stream.IntStream;
  import java.util.stream.Stream;
  
  public class StreamDemo1 {
  
      public static void main(String[] args) {
          // 初始化一个整型数组
          int[] arr = new int[]{1,2,3};
          // 通过整型数组，获取整形的 stream 对象
          IntStream stream1 = Arrays.stream(arr);
  
          // 通过字符串类型的数组，获取泛型类型为 String 的 stream 对象
          String[] stringArr = new String[]{"Hello", "imooc"};
          Stream<String> stream2 = Arrays.stream(stringArr);
      }
  }
  ```

### 通过Stream的of()方法

- 可以**通过`Stream`类下的`of()`方法来创建 Stream 对象**，代码示例如下：

  ```java
  import java.util.stream.Stream;
  
  public class StreamDemo1 {
  
      public static void main(String[] args) {
          // 通过 Stream 类下的 of() 方法，创建 stream 对象、
          Stream<Integer> stream = Stream.of(1, 2, 3);
      }
  }
  ```

### 创建无限流

- 可以**使用`Stream`类下的静态方法`iterate()`以及`generate()`创建无限流**：

  - **`public static<T> Stream<T> iterate(final T seed, final UnaryOperator<T> f)`**：遍历；

  - **`public static<T> Stream<T> generate(Supplier<T> s)`**：生成。
- 创建无限流的这种方式实际使用较少，大家了解一下即可。

## Stream的中间操作

- **多个中间操作可以连接起来形成一个流水线**，**除非流水线上触发终止操作，否则中间操作不会执行任何的处理**。在**终止操作时会一次性全部处理这些中间操作，称为“惰性求值”**。下面，我们来学习一下常用的中间操作方法。

### 筛选与切片

- 关于筛选和切片中间操作，有下面几个常用方法：

  1. **`filter(Predicate p)`**：接收 `Lambda`，从流中清除某些元素；
  2. **`distinct()`**：筛选，通过流生成元素的`hashCode`和`equals()`方法去除重复元素；
  3. **`limit(long maxSize)`**：截断流，使其元素不超过给定数量；
  4. **`skip(long n)`**：跳过元素，返回一个扔掉了前 `n` 个元素的流。若流中元素不足 `n` 个，则返回一个空流。与`limit(n)`互补。

- **过滤集合元素**的代码示例：

  ```java
  import java.util.ArrayList;
  import java.util.List;
  import java.util.stream.Stream;
  
  public class StreamDemo2 {
  
      static class Person {
          private String name;
          private int age;
  
          public Person() { }
  
          public Person(String name, int age) {
              this.name = name;
              this.age = age;
          }
  
          public String getName() {
              return name;
          }
  
          public void setName(String name) {
              this.name = name;
          }
  
          public int getAge() {
              return age;
          }
  
          public void setAge(int age) {
              this.age = age;
          }
  
          @Override
          public String toString() {
              return "Person{" +
                      "name='" + name + '\'' +
                      ", age=" + age +
                      '}';
          }
      }
  
      /**
       * 创建一个 Person 的集合
       * @return List
       */
      public static List<Person> createPeople() {
          ArrayList<Person> people = new ArrayList<>();
          Person person1 = new Person("小明", 15);
          Person person2 = new Person("小芳", 20);
          Person person3 = new Person("小李", 18);
          Person person4 = new Person("小付", 23);
          Person person5 = new Person("大飞", 22);
          people.add(person1);
          people.add(person2);
          people.add(person3);
          people.add(person4);
          people.add(person5);
          return people;
      }
  
      public static void main(String[] args) {
          List<Person> people = createPeople();
          // 创建 Stream 对象
          Stream<Person> stream = people.stream();
          // 过滤年龄大于 20 的 person
          Stream<Person> personStream = stream.filter(person -> person.getAge() >= 20);
          // 触发终止操作才能执行中间操作，遍历列表中元素并打印
          personStream.forEach(System.out::println);
      }
  }
  ```

  运行结果：

  ```java
  Person{name='小芳', age=20}
  Person{name='小付', age=23}
  Person{name='大飞', age=22}
  ```

  实例中，有一个静态内部类`Person`以及一个创建`Person`的集合的静态方法`createPeople()`，在主方法中，我们先调用该静态方法获取到一个`Person`列表，然后创建了`Stream`对象，再执行中间操作（即调用`fliter()`方法），这个方法的参数类型是一个**断言型的函数式接口**，接口下的抽象方法`test()`要求返回`boolean`结果，因此我们使用`Lambda`表达式，`Lambda`体为`person.getAge() >= 20`，其返回值就是一个布尔型结果，这样就实现了对年龄大于等于 20 的`person`对象的过滤。

  由于必须触发终止操作才能执行中间操作，我们又调用了`forEach(System.out::println)`，在这里记住它作用是遍历该列表并打印每一个元素即可，我们下面将会讲解。另外，`filter()`等这些由于中间操作返回类型为 Stream，所以支持链式操作，我们可以将主方法中最后两行代码合并成一行：

  ```java
  stream.filter(person -> person.getAge() >= 20).forEach(System.out::println);
  ```

- 我们再来看一个**截断流**的使用实例：

  ```java
  import java.util.ArrayList;
  import java.util.List;
  import java.util.stream.Stream;
  
  public class StreamDemo3 {
  
      static class Person {
          private String name;
          private int age;
  
          public Person() { }
  
          public Person(String name, int age) {
              this.name = name;
              this.age = age;
          }
  
          public String getName() {
              return name;
          }
  
          public void setName(String name) {
              this.name = name;
          }
  
          public int getAge() {
              return age;
          }
  
          public void setAge(int age) {
              this.age = age;
          }
  
          @Override
          public String toString() {
              return "Person{" +
                      "name='" + name + '\'' +
                      ", age=" + age +
                      '}';
          }
      }
  
      /**
       * 创建一个 Person 的集合
       * @return List
       */
      public static List<Person> createPeople() {
          ArrayList<Person> people = new ArrayList<>();
          Person person1 = new Person("小明", 15);
          Person person2 = new Person("小芳", 20);
          Person person3 = new Person("小李", 18);
          Person person4 = new Person("小付", 23);
          Person person5 = new Person("大飞", 22);
          people.add(person1);
          people.add(person2);
          people.add(person3);
          people.add(person4);
          people.add(person5);
          return people;
      }
  
      public static void main(String[] args) {
          List<Person> people = createPeople();
          // 创建 Stream 对象
          Stream<Person> stream = people.stream();
          // 截断流，并调用终止操作打印集合中元素
          stream.limit(2).forEach(System.out::println);
      }
  }
  ```

  运行结果：

  ```java
  Person{name='小明', age=15}
  Person{name='小芳', age=20}
  ```

  根据运行结果显示，我们只打印了集合中的前两条数据。

- **跳过前 2 条数据**的代码实例如下：

  ```java
  // 非完整代码
  public static void main(String[] args) {
      List<Person> people = createPeople();
      // 创建 Stream 对象
      Stream<Person> stream = people.stream();
      // 跳过前两个元素，并调用终止操作打印集合中元素
      stream.skip(2).forEach(System.out::println);
  }
  ```

  运行结果：

  ```java
  Person{name='小李', age=18}
  Person{name='小付', age=23}
  Person{name='大飞', age=22}
  ```

- **`distinct()`方法会根据`equals()`和`hashCode()`方法筛选重复数据**，我们在`Person`类内部重写这两个方法，并且在`createPerson()`方法中，添加几个重复的数据 ，实例如下：

  ```java
  import java.util.ArrayList;
  import java.util.List;
  import java.util.Objects;
  import java.util.stream.Stream;
  
  public class StreamDemo4 {
  
      static class Person {
          private String name;
          private int age;
  
          public Person() { }
  
          public Person(String name, int age) {
              this.name = name;
              this.age = age;
          }
  
          public String getName() {
              return name;
          }
  
          public void setName(String name) {
              this.name = name;
          }
  
          public int getAge() {
              return age;
          }
  
          public void setAge(int age) {
              this.age = age;
          }
  
          @Override
          public String toString() {
              return "Person{" +
                      "name='" + name + '\'' +
                      ", age=" + age +
                      '}';
          }
  
          @Override
          public boolean equals(Object o) {
              if (this == o) return true;
              if (o == null || getClass() != o.getClass()) return false;
              Person person = (Person) o;
              return age == person.age &&
                      Objects.equals(name, person.name);
          }
  
          @Override
          public int hashCode() {
              return Objects.hash(name, age);
          }
      }
  
      /**
       * 创建一个 Person 的集合
       * @return List
       */
      public static List<Person> createPeople() {
          ArrayList<Person> people = new ArrayList<>();
          people.add(new Person("小明", 15));
          people.add(new Person("小芳", 20));
          people.add(new Person("小李", 18));
          people.add(new Person("小付", 23));
          people.add(new Person("大飞", 22));
          return people;
      }
  
      public static void main(String[] args) {
          List<Person> people = createPeople();
          // 创建 Stream 对象
          Stream<Person> stream = people.stream();
  
          System.out.println("去重前，集合中元素有：");
          stream.forEach(System.out::println);
  
          System.out.println("去重后，集合中元素有：");
          // 创建一个新流
          Stream<Person> stream1 = people.stream();
          // 截断流，并调用终止操作打印集合中元素
          stream1.distinct().forEach(System.out::println);
      }
  }
  ```

  运行结果：

  ```java
  去重前，集合中元素有：
  Person{name='小明', age=15}
  Person{name='小芳', age=20}
  Person{name='小李', age=18}
  Person{name='小付', age=23}
  Person{name='大飞', age=22}
  去重后，集合中元素有：
  Person{name='小明', age=15}
  Person{name='小芳', age=20}
  Person{name='小李', age=18}
  Person{name='小付', age=23}
  Person{name='大飞', age=22}
  ```

### 映射

- 关于映射中间操作，有下面几个常用方法：

  - **`map(Function f)`**：接收一个方法作为参数，该方法会被应用到每个元素上，并将其映射成一个新的元素；
  - **`mapToDouble(ToDoubleFunction f)`**：接收一个方法作为参数，该方法会被应用到每个元素上，产生一个新的`DoubleStream`；
  - **`mapToLong(ToLongFunction f)`**：接收一个方法作为参数，该方法会被应用到每个元素上，产生一个新的`LongStream`；
  - **`flatMap(Function f)`**：接收一个方法作为参数，将流中的每个值都换成另一个流，然后把所有流连接成一个流。

- 请查看如下实例：

  ```java
  import java.util.Arrays;
  import java.util.List;
  
  public class StreamDemo5 {
  
      public static void main(String[] args) {
          // 创建一个包含小写字母元素的字符串列表
          List<String> stringList = Arrays.asList("php", "js", "python", "java");
          // 调用 map() 方法，将 String 下的 toUpperCase() 方法作为参数，这个方法会被应用到每个元素上，映射成一个新元素，最后打印映射后的元素
          stringList.stream().map(String::toUpperCase).forEach(System.out::println);
      }
  
  }
  ```

  运行结果：

  ```java
  PHP
  JS
  PYTHON
  JAVA
  ```

  可参考下图，理解映射的过程：

  ![image-20221108230358670](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20221108230358670.png)

### 排序

- 关于排序中间操作，有下面几个常用方法：

  - **`sorted()`**：产生一个新流，其中按照自然顺序排序；
  - **`sorted(Comparator com)`**：产生一个新流，其中按照比较器顺序排序。

- 请查看如下实例：

  ```java
  import java.util.Arrays;
  import java.util.List;
  
  public class StreamDemo6 {
  
      public static void main(String[] args) {
          List<Integer> integers = Arrays.asList(10, 12, 9, 8, 20, 1);
          // 调用 sorted() 方法自然排序，并打印每个元素
          integers.stream().sorted().forEach(System.out::println);
      }
  
  }
  ```

  运行结果：

  ```java
  1
  8
  9
  10
  12
  20
  ```

  上面实例中，我们调用`sorted()`方法对集合元素进行了从小到大的自然排序，那么如果想要实现从大到小排序，任何实现呢？此时就要用到`sorted(Comparator com)`方法定制排序，查看如下实例：

  ```java
  import java.util.Arrays;
  import java.util.List;
  
  public class StreamDemo6 {
  
      public static void main(String[] args) {
          List<Integer> integers = Arrays.asList(10, 12, 9, 8, 20, 1);
          // 定制排序
          integers.stream().sorted(
                  (i1, i2) -> -Integer.compare(i1, i2)
          ).forEach(System.out::println);
      }
  
  }
  ```

  运行结果：

  ```java
  20
  12
  10
  9
  8
  1
  ```

  实例中，`sorted()`方法接收的参数是一个函数式接口`Comparator`，因此使用`Lambda`表达式创建函数式接口实例即可，**要想从大到小排序，只需在传入`Lambda`体中调用整型的比较方法，对返回的整型值做一个取反即可**。

## Stream的终止操作

- **执行终止操作会从流的流水线上生成结果，其结果可以是任何不是流的值**，例如`List`、`String`、`void`。
- 在上面实例中，我们一直在使用`forEach()`方法来执行流的终止操作，下面我们看看还有哪些其他终止操作。

### 匹配与查找

- 关于匹配与查找的终止操作，有下面几个常用方法：

  - **`allMatch(Predicate p)`**：检查是否匹配所有元素；
  - **`anyMatch(Predicate p)`**：检查是否至少匹配一个元素；
  - **`noneMatch(Predicate p)`**：检查是否没有匹配所有元素；
  - **`findFirst()`**：返回第一个元素；
  - **`findAny()`**：返回当前流中的任意元素；
  - **`count()`**：返回流中元素总数；
  - **`max(Comparator c)`**：返回流中最大值；
  - **`min(Comparator c)`**：返回流中最小值；
  - **`forEach(Consumer c)`**：内部迭代（使用 Collection 接口需要用户去做迭代，称为外部迭代；相反 `Stream API`使用内部迭代）。

- 如下实例，演示了**几个匹配元素相关方法**的使用：

  ```java
  import java.util.Arrays;
  import java.util.List;
  
  public class StreamDemo7 {
  
      public static void main(String[] args) {
          // 创建一个整型列表
          List<Integer> integers = Arrays.asList(10, 12, 9, 8, 20, 1);
          // 使用 allMatch(Predicate p) 检查是否匹配所有元素，如果匹配，则返回 true；否则返回 false
          boolean b1 = integers.stream().allMatch(integer -> integer > 0);
          if (b1) {
              System.out.println(integers + "列表中所有的元素都大于 0");
          } else {
              System.out.println(integers + "列表中不是所有的元素都大于 0");
          }
  
          // 使用 anyMatch(Predicate p) 检查是否至少匹配一个元素
          boolean b2 = integers.stream().anyMatch(integer -> integer >= 20);
          if (b2) {
              System.out.println(integers + "列表中至少存在一个的元素都大于等于 20");
          } else {
              System.out.println(integers + "列表中不存在任何一个大于等于 20 的元素");
          }
  
          // 使用 noneMath(Predicate p) 检查是否没有匹配所有元素
          boolean b3 = integers.stream().noneMatch(integer -> integer > 100);
          if (b3) {
              System.out.println(integers + "列表中不存在大于 100 的元素");
          } else {
              System.out.println(integers + "列表中存在大于 100 的元素");
          }
      }
  
  }
  ```

  运行结果：

  ```java
  [10, 12, 9, 8, 20, 1] 列表中所有的元素都大于 0
  [10, 12, 9, 8, 20, 1] 列表中至少存在一个的元素都大于等于 20
  [10, 12, 9, 8, 20, 1] 列表中不存在大于 100 的元素
  ```

- **查找元素的相关方法**使用实例如下：

  ```java
  import java.util.Arrays;
  import java.util.List;
  import java.util.Optional;
  
  public class StreamDemo8 {
  
      public static void main(String[] args) {
          // 创建一个整型列表
          List<Integer> integers = Arrays.asList(10, 12, 9, 8, 20, 1);
  
          // 使用 findFirst() 获取当前流中的第一个元素
          Optional<Integer> first = integers.stream().findFirst();
          System.out.println(integers + "列表中第一个元素为：" + first);
  
          // 使用 findAny() 获取当前流中的任意元素
          Optional<Integer> any = integers.stream().findAny();
          System.out.println("列表中任意元素：" + any);
  
          // 使用 count() 获取当前流中元素总数
          long count = integers.stream().count();
          System.out.println(integers + "列表中元素总数为" + count);
  
          // 使用 max(Comparator c) 获取流中最大值
          Optional<Integer> max = integers.stream().max(Integer::compare);
          System.out.println(integers + "列表中最大值为" + max);
  
          // 使用 min(Comparator c) 获取流中最小值
          Optional<Integer> min = integers.stream().min(Integer::compare);
          System.out.println(integers + "列表中最小值为" + min);
      }
  
  }
  ```

  运行结果：

  ```java
  [10, 12, 9, 8, 20, 1] 列表中第一个元素为：Optional[10]
  列表中任意元素：Optional[10]
  [10, 12, 9, 8, 20, 1] 列表中元素总数为 6
  [10, 12, 9, 8, 20, 1] 列表中最大值为 Optional[20]
  [10, 12, 9, 8, 20, 1] 列表中最小值为 Optional[1]
  ```

  实例中，我们观察到`findFirst()`、`findAny()`、`max()`等方法的**返回值类型为`Optional`类型**，关于这个`Optional`类，**Optional类(java.util.Optional)是一个容器类，代表一个值存在或不存在，原来用null表示一个值不存在，现在Optional可以更好的表达这个概念。并且可以避免空指针异常**。

### 归约

- 通常用于**将整个流中的元素按照某个约定归为一个值**。

- 关于归约的终止操作，有下面几个常用方法：

  - **`reduce(T identity, BinaryOperator b)`**：可以将流中的元素反复结合起来，得到一个值。返回 T；
  - **`reduce(BinaryOperator b)`**：可以将流中的元素反复结合起来，得到一个值，返回 `Optional<T>`。

- 归约相关方法的使用实例如下：

  ```java
  import java.util.Arrays;
  import java.util.List;
  import java.util.Optional;
  
  public class StreamDemo9 {
  
      public static void main(String[] args) {
          // 创建一个整型列表
          List<Integer> integers = Arrays.asList(10, 12, 9, 8, 20, 1);
  
          // 使用 reduce(T identity, BinaryOperator b) 计算列表中所有整数和
          Integer sum = integers.stream().reduce(0, Integer::sum);
          System.out.println(sum);
  
          // 使用 reduce(BinaryOperator b) 计算列表中所有整数和，返回一个 Optional<T>
          Optional<Integer> reduce = integers.stream().reduce(Integer::sum);
          System.out.println(reduce);
      }
  
  }
  ```

  运行结果：

  ```java
  60
  Optional[60]
  ```

### 收集

- **`collect(Collector c)`**：将流转换为其他形式。接收一个`Collector`接口的实现，用于给`Stream`中元素做汇总的方法。

- 实例如下：

  ```java
  import java.util.Arrays;
  import java.util.List;
  import java.util.Set;
  import java.util.stream.Collectors;
  
  public class StreamDemo10 {
  
      public static void main(String[] args) {
          // 创建一个整型列表
          List<Integer> integers = Arrays.asList(10, 12, 9, 8, 20, 1, 10);
          Set<Integer> collect = integers.stream().collect(Collectors.toSet());
          System.out.println(collect);
      }
  
  }
  ```

  运行结果：

  ```java
  [1, 20, 8, 9, 10, 12]
  ```

  **Collector 接口中的实现决定了如何对流执行收集的操作**（如收集到 List、Set、Map）。**`java.util.stream.Collectors` 类提供了很多静态方法，可以方便地创建常用收集器实例**，常用静态方法如下：

  - **`static List<T> toList()`**：把流中元素收集到`List`；
  - **`static Set<T> toSet()`**：把流中元素收集到`Set`；
  - **`static Collection<T> toCollection()`**：把流中元素收集到创建的集合。

## Optional类

- Optional类(java.util.Optional)是一个容器类，**代表一个值存在或不存在，原来用null表示一个值不存在，现在Optional可以更好的表达这个概念。并且可以避免空指针异常**。

## 小结

- 通过本小节的学习，我们知道了**`Stream`不同于`java.io`下的输入输出流，它主要用于处理数据**。**`Stream API`可用于处理非关系型数据库中的数据**；想要使用流式操作，就要知道创建`Stream`对象的几种方式；**流式操作可分为创建`Stream`对象、中间操作和终止操作三个步骤**。多个中间操作可以连接起来形成一个流水线，**除非流水线上触发终止操作，否则中间操作不会执行任何的处理**。**执行终止操作会从流的流水线上生成结果，其结果可以是任何不是流的值**。

# Java关于i++是否是原子操作的讨论

- 什么是原子操作，就是一个操作不能再分了，已经是最小单位了，这样的操作在多线程中会表现出绝对的线程安全。
- 那么i++是不是个原子操作呢，在java中很明显它不是一个原子操作，因为首先java是支持多线程的，这就不得不考虑这个代码在多线程环境下的表现，再看操作本身，被java解析成的汇编操作是**先取i的值，然后再加1，然后再把新值赋值回去**，其本身是可以再被细分的，而且这种性质使得他在多线程的环境下是线程不安全的，所以综上所述，**i++在java中并不是一个原子操作**。
