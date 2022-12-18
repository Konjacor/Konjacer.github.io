---
title: Flutter项目中路由的使用
date: 2022-05-10 22:43:57
tags: [dart,flutter,移动端开发]
---

# 1、引入所有要进行路由跳转的页面

​	在项目中使用路由一般都是会**将配置路由的部分单独抽离出来**，抽离成dart文件，然后在main里面引入路由的包来实现路由操作。

​	在配置路由时除了引入必要的material.dart之外，还要引入所有要进行路由跳转的页面，之后配置会用到。

# 2、配置路由

​	所有路径和页面的映射都放在这个部分，通常是用一个**Map<String,Function>**来存放所有的路由，以下是一个例子：

```dart
final Map<String,Function> routes = {
  '/' : (context) => Tabs(),
};
```

别的路由可以参照里面那个写法进行配置。

# 3、写好onGenerateRoute

​	这个部分的写法比较固定，我现在学的很浅还不知道为什么要这样写，但是我感觉这个东西是在配置进行路由跳转时为了让页面显示出来而进行的操作。

```dart
var onGenerateRoute = (RouteSettings settings) {
  final String? name = settings.name;
  final Function? pageContentBuilder = routes[name];
  if (pageContentBuilder != null) {
    if (settings.arguments != null) {
      final Route route = MaterialPageRoute(
          builder: (context) =>
              pageContentBuilder(context, arguments: settings.arguments));
      return route;
    } else {
      final Route route =
          MaterialPageRoute(builder: (context) => pageContentBuilder(context));
      return route;
    }
  }
};
```

- 完整Routes.dart代码示例：

  ```dart
  import 'dart:js';
  
  import 'package:flutter/material.dart';
  import 'package:questionnaire/pages/tabs/Detail.dart';
  import 'package:questionnaire/pages/tabs/Exam.dart';
  import '../pages/Tabs.dart';
  import '../pages/tabs/Find.dart';
  import '../pages/tabs/User.dart';
  
  // import '../pages/Tabs.dart';
  // import '../pages/Form.dart';
  // import '../pages/Search.dart';
  // import '../pages/Product.dart';
  // import '../pages/ProductInfo.dart';
  
  //配置路由,定义Map类型的routes,Key为String类型，Value为Function类型
  final Map<String, Function> routes = {
    '/': (context) => Tabs(),
    '/find': (context) => Find(),
    '/user': (context) => User(),
    '/exam': (context,{arguments}) => Exam(arguments: arguments),
    '/detail': (context, {arguments}) => Detail(arguments: arguments), //路由传参
    // '/':(context)=>Tabs(),
    // '/form':(context)=>FormPage(),
    // '/product':(context)=>ProductPage(),
    // '/productinfo':(context,{arguments})=>ProductInfoPage(arguments:arguments),
    // '/search':(context,{arguments})=>SearchPage(arguments:arguments),
  };
  
  //固定写法
  var onGenerateRoute = (RouteSettings settings) {
    //String? 表示name为可空类型
    final String? name = settings.name;
    //Function? 表示pageContentBuilder为可空类型
    final Function? pageContentBuilder = routes[name];
    if (pageContentBuilder != null) {
      if (settings.arguments != null) {
        final Route route = MaterialPageRoute(
            builder: (context) =>
                pageContentBuilder(context, arguments: settings.arguments));
        return route;
      } else {
        final Route route =
            MaterialPageRoute(builder: (context) => pageContentBuilder(context));
        return route;
      }
    }
  };
  ```

# 4、到main中进行路由相关的设置

- 首先要在main中引入刚才写好的路由文件，然后在MaterialApp中设置相关的参数。

- 完整的main路由配置：

  ```dart
  import 'package:flutter/material.dart';
  import 'package:questionnaire/pages/tabs/Find.dart';
  import '../pages/Tabs.dart';
  import '../routes/Routes.dart';
  
  void main() {
    runApp(const Questionnaire());
  }
  
  class Questionnaire extends StatelessWidget {
    const Questionnaire({Key? key}) : super(key: key);
  
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        initialRoute: '/',
        onGenerateRoute: onGenerateRoute,
        debugShowCheckedModeBanner: false,
      );
    }
  }
  ```

## initialRoute

​	这个参数是在设置项目的根路由，即应用一开始应该显示的路由。

## onGenerateRoute

​	值应该是RouteFactory类型的函数，是路由钩子，可以对某些指定的路由进行拦截，有时候不想改变页面结构，但是又想要求跳转到这个页面的时候可以用到，比如，页面设定了传参你进行跳转的时候。

​	钩子函数：钩子函数是在一个事件触发的时候，在系统级捕获到了他，然后做一些操作。一段用以处理系统消息的程序。“钩子”就是在某个阶段给你一个做某些处理的机会。钩子函数由系统而非用户调用。那些生命周期函数好像都是钩子函数。

## onUnknownRoute

​	值应该是RouteFactory类型的函数，在路由匹配不到的时候用到，一般都返回一个统一的错误页面或404页面。

# 5、路由传参

## 配置Route.dart文件

- 首先要配置一下上面刚写好的Route.dart文件，**将想要接收参数的路由项上增加一个用于接收参数的形参**：

  ![image-20220919122547179](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220919122547179.png)

- 然后在进行路由跳转的时候，将参数**以键值对的形式写到请求的参数列表中**：

  ![image-20220919122656286](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220919122656286.png)

- 然后在想要跳转到的页面中**声明接收参数的变量，并将其写进其构造器的形参中来接收参数**：

  ![image-20220919123009563](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220919123009563.png)

  如果要是StatefulWidget，情况会变得复杂一点，需要再按照同样的方式把参数传到对应的State对象中才能进行操作，因为操作都是写在State对象中的：

  ![image-20220919143330741](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220919143330741.png)

- 最后**通过上面声明的接收到参数的变量来访问参数**：

  ![image-20220919123117782](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220919123117782.png)
