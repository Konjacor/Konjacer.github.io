---
title: Dart语言入门教程
date: 2022-05-15 15:18:24
tags: [Dart]
---

<meta name="referrer" content="no-referrer"/>

# Dart语言介绍

​	Dart是由谷歌开发的计算机编程语言,它可以被用于web、服务器、移动应用 和物联网等领域的开发。

  Dart诞生于2011年，号称要取代JavaScript。但是过去的几年中一直不温不火。直到Flutter的出现现在被人们重新重视。

  要学Flutter的话我们必须首先得会Dart。

  官网：https://dart.dev/

# Dart环境搭建

要在我们本地开发Dart程序的话首先需要安装Dart Sdk

 官方文档：https://dart.dev/get-dart

   windows(推荐):

​    http://www.gekorm.com/dart-windows/

   mac：

​    如果mac电脑没有安装brew这个工具首先第一步需要安装它：  https://brew.sh/

```
brew tap dart-lang/dart

brew install dart
```

# Dart开发工具

Dart的开发工具有很多： IntelliJ IDEA  、 WebStorm、 Atom、Vscode等

  这里我们主要给大家讲解的是如果在Vscode中配置Dart。

   1、找到vscode插件安装dart

   2、找到vscode插件安装code runner   Code Runner  可以运行我们的文件

# Dart变量、常量命名规则

## Dart变量

- dart是一个强大的脚本类语言，可以不预先定义变量类型，类型会自动推导

- dart中定义变量可以通过**var关键字**或通过**指定对应类型**来声明变量

   如：

  ```dart
    var str='this is var';
    String str='this is var';
    int str=123;
  ```

## Dart常量

常用**final**和**const**修饰符来修饰常量。

比如：

```dart
final name = 'Bob'; // Without a type annotation
final String nickname = 'Bobby';

const bar = 1000000; // Unit of pressure (dynes/cm2)
const double atm = 1.01325 * bar; // Standard atmosphere
```



### const关键字

- 用const关键字修饰的变量是常量，但是**这个常量必须一开始就指定它的值**，后续这个值不能再被修改。

### final关键字

- 用final关键字修饰的变量也是常量，但是**这个常量可以一开始不指定值，但是在后面赋值的时候只能赋值一次，一旦赋值后就不能再更改**。
- final不仅有const的编译时常量的特性，最重要的它是运行时常量，并且final是惰性初始化，即在运行时第一次使用前才初始化

## Dart的命名规则

1. 变量名称必须由数字、字母、下划线和美元符($)组成。
2. 标识符开头不能是数字
3. 标识符不能是保留字和关键字。
4. 变量的名字是区分大小写的如: age和Age是不同的变量。在实际的运用中建议不要用一个单词大小写区分两个变量。
5. 标识符(变量名称)一定要见名思意 ：变量名称建议用名词，方法名称建议用动词

# main方法的两种定义方式

```dart
/*
 入口方法的两种定义方式
 第一种：
  main(){
    print('你好dart');
  }
*/

///这也是一个注释
//第二种：
//表示main方法没有返回值
void main(){
 print('你好dart');
}
```

# Dart中的数据类型

## 常用的数据类型

- Numbers（数值）：
  - int
  - double

- Strings（字符串）：
  - String

- Booleans（布尔）：
  - bool

- List（数组）：
  - 在Dart中，数组是列表对象，所以大多数人只是称它们为列表

- Maps（字典）：
  - 通常来说，Map是一个键值对相关的对象。键和值可以是任何类型的对象。每个键只出现一次，而每个值可以出现多次

## 字符串类型

```dart
void main(){
  //1、字符串定义的几种方式
  //用var
  // var str1='this is str1';
  // var str2="this is str2";
  // print(str1);
  // print(str2);
  
  //用String
  // String str1='this is str1';
  // String str2="this is str2";
  // print(str1);
  // print(str2);
    
  //三单引号括起来的保留了中间的换行
  // String str1='''this is str1
  // this is str1
  // this is str1
  // ''';
  //  print(str1);
  
  //三双引号和三单引号一样
  //   String str1="""
  //   this is str1
  //   this is str1
  //   this is str1
  //   """;
  //  print(str1);

  //2、字符串的拼接
  String str1='你好';
  String str2='Dart';
  // print("$str1 $str2");
  print(str1 + str2);
  print(str1 +" "+ str2);
}
```

## 数值类型

```dart
/*
Dart数据类型：数值类型
    int 
    double
*/

void main(){
  //1、int   必须是整型
    int a=123;
    a=45;
    print(a);

  //2、double  既可以是整型 也可是浮点型
    double b=23.5;
    b=24;
    print(b);

  //3、运算符
    // + - * / %  
    var c=a+b;
    print(c);
}
```

## 布尔类型

```dart
/*
Dart数据类型：布尔类型
bool 值true/false
*/

void main(){
//1、bool
// bool flag1=true;
// print(flag1);
// bool flag2=false;
// print(flag2);

//2、条件判断语句
	var flag=true;
	if(flag){
		print('真');
	}else{
     	print('假');
	}

// var a=123;
// var b='123';
// if(a==b){
//   print('a=b');
// }else{
//    print('a!=b');
// }
	var a=123;
	var b=123;
	if(a==b){
		print('a=b');
    	}else{
    		print('a!=b');
		}
	}
```

## List集合类型

```dart
/*
Dart数据类型： List（数组/集合）
*/
void main() {
  //1、第一种定义List的方式

  // var l1=["张三",20,true];

  // print(l1);  //[张三, 20, true]

  // print(l1.length);  //3

  // print(l1[0]); //张三

  // print(l1[1]); //20

  //2、第二种定义List的方式 指定类型

  // var l2=<String>["张三","李四"];

  // print(l2);

  // var l3 = <int>[12, 30];
  // print(l3);

  //3、第三种定义List的方式 增加数据 ,通过[]创建的集合它的容量可以变化

  // var l4 = [];
  // print(l4);
  // print(l4.length);

  // l4.add("张三");
  // l4.add("李四");
  // l4.add(20);
  // print(l4);
  // print(l4.length);

  // var l5 = ["张三", 20, true];
  // l5.add("李四");
  // l5.add("zhaosi");
  // print(l5);

  //4、第四种定义List的方式

  //  var l6=new List();  //在新版本的dart里面没法使用这个方法了

  // var l6=List.filled(2, "");  //创建一个固定长度的集合
  // print(l6);
  // print(l6[0]);

  // l6[0]="张三";   //修改集合的内容
  // l6[1]="李四";

  // print(l6);  //[张三, 李四]

  // l6.add("王五");  //错误写法

  //通过List.filled创建的集合长度是固定
  // var l6=List.filled(2, "");
  // print(l6.length);
  // l6.length=0;  //修改集合的长度   报错

  // var l7=<String>["张三","李四"];
  // print(l7.length);  //2
  // l7.length=0;  //可以改变的
  // print(l7);  //[]

  // var l8=List<String>.filled(2, "");

  // l8[0]="string";
  // // l8[0]=222;
  // print(l8);

  // List list1 = ['香蕉', '苹果', '西瓜'];

  // var l1=['香蕉', '苹果', '西瓜',true,12];
  // print(l1);

  // var l1=<String>['香蕉', '苹果', '西瓜'];
  // print(l1);

  // List l2=<String>['香蕉', '苹果', '西瓜'];
  // print(l2);
  // print(l2.length);
  // l2.add("草莓");
  // print(l2);
  // print(l2.length);

  // List l3 = List<String>.filled(2, "");
  // // l3.add("草莓");
  // l3[0]="苹果";
  // print(l3);
  
  // var l=new List();
  // l.add("苹果");
}
```

## Maps字典类型

```dart
/*
Dart数据类型： Maps（字典）  
*/
void main(){  
  //第一种定义 Maps的方式
  // var person={
  //   "name":"张三",
  //   "age":20,
  //   "work":["程序员","送外卖"]
  // };
  // print(person);
  // print(person["name"]);
  // print(person["age"]);
  // print(person["work"]);

  //第二种定义 Maps的方式
   var p=new Map();
   p["name"]="李四";
   p["age"]=22;
   p["work"]=["程序员","送外卖"];
   print(p);
   print(p["age"]);
}
```

## Dart类型判断

```dart
/*
Dart判断数据类型    
is 关键词来判断类型
*/

void main(){
  // var str='1234';

  // if(str is String){
  //   print('是string类型');
  // }else if(str is int){

  //    print('int');
  // }else{
  //    print('其他类型');
  // }
  var str=123;
  if(str is String){
    print('是string类型');
  }else if(str is int){

     print('int');
  }else{
     print('其他类型');
  }
}
```

