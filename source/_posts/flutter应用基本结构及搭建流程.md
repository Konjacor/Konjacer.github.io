---
title: flutter应用基本结构及搭建流程
date: 2022-08-24 11:46:22
tags: [flutter,移动应用开发]
---

<meta name="referrer" content="no-referrer"/>

# Flutter避坑

## xxxx is not a valid Dart package name

- 文件夹路径根目录不能有大写字母。

## Error: The getter 'body1' isn't defined for the class 'TextTheme'.

![image-20220824220653658](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220824220653658.png)

- body1在TextTheme中好像改名成**bodyText1**了。

## Flutter显示有依赖不符合空安全规范不让启动

- 使用**flutter run --no-sound-null-safety**，可以在启动的时候避开空安全检查。

## Flutter访问阿里云oss中的图片产生的跨域问题

- 要在阿里云oss的后台配置跨域规则：
  1. 点开你想要设置跨域规则的**bucket**
  2. 点击**权限管理**，找到**跨域设置**一栏，点击**设置**
  3. 点击**创建规则**，在来源处写对应的来源，**直接写\*就是允许所有跨域请求**，然后根据需要填写下面的内容，填写完毕后点击**确定**即可完成设置。
  4. 然后再在前端访问阿里云oss中的图片就能访问到了。

## Another exception was thrown: A RenderFlex overflowed by 150 pixels on the bottom.

- 一般是由于在Row或者Column布局中，可变大小的子元素没有使用Expanded包裹导致的越界问题，将Row或者Column中的可变大小的子元素使用Expanded进行包裹即可。

## Unexpected Null Value

- 这个一般是**flutter在渲染页面的时候使用到了值为空的对象**，比如这个对象是用来接收异步数据的，在第一次渲染页面的时候异步数据还没到达，此时如果使用这个对象来对页面进行渲染的话就会报这个错，因此应该保证在flutter渲染页面的时候使用到的数据都已经存在。

![image-20220919151513259](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220919151513259.png)

## 如何快速定位报错位置

- 根据报错时flutter输出到终端上的日志，从上往下找，直到找到第一个自己写的文件的具体位置，那就是报错的位置。

# Flutter常用技巧

## 实现瀑布流式布局

### 效果展示

![image-20220826211908936](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220826211908936.png)

### 实现方式

1. 要实现这个瀑布流式布局方式，可以自己手写，但是最方便的还是使用一个名为**flutter_staggered_grid_view**的包来实现，还需要一个包**cached_network_image**，来将图片放入缓存中然后再显示，具体的包的版本如下，不同版本的包的类和方法名有不小的出入，实现代码的写法也不同，因此尽量使用相同版本的包，防止出现问题，还有这些包的版本好像都不支持空安全，所以启动的时候要在关闭空安全检查的情况下启动。

   ```yaml
   flutter_staggered_grid_view: ^0.4.0
   cached_network_image: ^2.2.0+1
   ```

   

2. 然后要将包导入你想要写代码的页面中：

   ```dart
   import 'package:flutter_staggered_grid_view/flutter_staggered_grid_view.dart';
   import 'package:cached_network_image/cached_network_image.dart';
   ```

3. 编写瀑布流的每个子项：

   ```dart
   //瀑布流的每个子项
   Widget itemWidget(context, int index) {
     // if (_isLoad < 2) _isLoad++;
     // print(_isLoad);
     String imgPath = dataList[index]["url"];
     int isLoad = dataList[index]["isLoad"] < 2
         ? dataList[index]["isLoad"]++
         : dataList[index]["isLoad"];
     //print(imgPath+" "+isLoad.toString());
     return new Material(
       elevation: 8.0, //海拔为8，显得更加立体
       borderRadius: new BorderRadius.all(new Radius.circular(8.0)), //圆角
       child: new InkWell(
         //被包裹起来的元素可以被点击
         // child:
         // new Hero(
         //实现元素共享动画效果
         // tag: imgPath,
         // child: CachedNetworkImage(
         //   // 加载网络图片过程中显示的内容 , 这里显示进度条
         //   placeholder: (context, url) => CircularProgressIndicator(),
         //   // 网络图片地址
         //   imageUrl: imgPath,
         // ),
         child: Column(
           //竖直方向容器
           // mainAxisSize: MainAxisSize.min,
           children: [
             // Expanded(
             // child:
             Padding(
               //让图片和左右边界有点距离
               padding: EdgeInsets.fromLTRB(0, 0, 0, 0),
               child: ClipRRect(
                 //让图片有个圆角效果
                 borderRadius: new BorderRadius.only(
                     topLeft: new Radius.circular(8.0),
                     topRight: new Radius.circular(8.0)),
                 child: // isLoad == 2
                     // ?
                     Hero(
                   tag: imgPath,
                   child: Image(image: CachedNetworkImageProvider(imgPath)),
                 ),
                 // : CachedNetworkImage(
                 //     //将网络图片缓存到本地并显示
                 //     // 加载网络图片过程中显示的内容 , 这里显示进度条
                 //     placeholder: (context, url) =>
                 //         CircularProgressIndicator(),
                 //     // 网络图片地址
                 //     imageUrl: imgPath,
                 //     //图片加载失败时的动作
                 //     errorWidget: (context, url, error) =>
                 //         Icon(Icons.error),
                 //     // imageBuilder: (context, imageProvider) => Container(
                 //     //   decoration: BoxDecoration(
                 //     //     image: DecorationImage(
                 //     //         image: imageProvider,
                 //     //         fit: BoxFit.cover,
                 //     //         colorFilter: ColorFilter.mode(
                 //     //             Colors.red, BlendMode.colorBurn)),
                 //     //   ),
                 //     // ),
                 //   ),
               ),
             ),
             // ),
             // SizedBox(height: 12,),
             SizedBox(
               //间隔12逻辑像素
               height: 12,
             ),
             // Expanded(
             // child:
             Text(
               "   测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字",
               maxLines: 2,
               overflow: TextOverflow.fade,
             ),
             // ),
             SizedBox(
               height: 6,
             ),
           ],
         ),
         // ),
         onTap: () {
           Navigator.pushNamed(context, '/detail', arguments: {
             "imgPath": imgPath,
             "text":
                 "   测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字测试文字",
           });
         },
       ),
     );
   }
   ```

4. 编写实现瀑布流的body代码：

   ```dart
   Widget TabsBody() {
     // return Center(
     //     child: LinearProgressIndicator(
     //   minHeight: 8.0,
     //   value: 0,
     //   backgroundColor: Colors.yellow,
     //   valueColor: AlwaysStoppedAnimation<Color>(Colors.red),
     // ));
     return new StaggeredGridView.countBuilder(
       //瀑布流式布局
       shrinkWrap: true,
       padding: EdgeInsets.all(8.0),
       crossAxisCount: 4,
       itemCount: dataList.length,
       itemBuilder: (context, i) {
         //构建流式布局的item，item放到tile里面
         return itemWidget(context, i);
       },
       staggeredTileBuilder: (int index) =>
           new StaggeredTile.fit(2), //fit是让每个tile都自适应，里面的参数是交叉轴上tile的数量。
       //new StaggeredTile.count(2, index == 0 ? 2.5 : 3),
       mainAxisSpacing: 8.0,
       crossAxisSpacing: 8.0,
     );
   }
   ```


## 利用Hero组件实现路由切换时的图片飞行动画

- 使用Hero组件可以使路由切换时，图片从原本的页面飞行到切换到的页面。

- 首先要在原页面中**将且只将图片用Hero组件包裹起来**，并设置一个tag值：

  ```dart
  Hero(
  	tag: imgPath,
      child: Image(image: CachedNetworkImageProvider(imgPath)),
  ),
  ```

- 然后在想要切换到的页面中也**将且仅将图片包裹起来**，tag的值要和原页面Hero中的tag值相同：

  ```dart
  Hero(
  	tag: arguments!["imgPath"],
      //因为前面加载图片是用的cached_network_image，加载完了直接存在缓存中了，因此可以直接从缓存中拿，减少加载时间，提升Hero动画的流畅性。
  	child:Image(image: CachedNetworkImageProvider(arguments!["imgPath"])),
  ),
  ```

- 然后在切换页面时就能看到图片的飞行动画了，要注意使用**Hero只能包裹图片（以我目前的水平来看）**，因为之前在使用的时候由于包裹了其他东西，在路由切换的时候报了**Another exception was thrown: A RenderFlex overflowed by 150 pixels on the bottom.**导致debug了好几个小时，最后才发现是Hero位置的问题。

## 给Flutter中的有状态组件(StatefulWidget)传参

1. 类中定义final全局变量：

   ```dart
   class QYInput extends StatefulWidget {
     final int minLines;
   }
   ```

2. 构造函数中初始化变量：

   ```dart
   class QYInput extends StatefulWidget {
     final int minLines;
     const QYInput({Key? key, this.minLines = 1}) : super(key: key);
   }
   ```

3. 继承于State抽象类的类中通过widget.xxx调用变量：

   ```dart
   class _QYInputState extends State<QYInput> {
     @override
     Widget build(BuildContext context) {
       return TextField(minLines: widget.minLines);
     }
   }
   ```

## 写一个带图标、文字的方形按钮，并调整到合适的大小

```dart
ElevatedButton.icon(
  //带图标、文字的方形按钮
  onPressed: () {//点击事件
    Navigator.pushNamed(context, '/exam',
        arguments: {"id": arguments!["id"]});
  },
  icon: Icon(Icons.create),//图标
  label: Text("开始填写"),//文字
  style: ElevatedButton.styleFrom(
    //调整按钮大小用
    minimumSize: const Size(150, 60),
  ),
),
```

## 写一个进度条

```dart
LinearProgressIndicator(
    value: 0.3,//当前进度（最高为1）
    minHeight: 8,//进度条最小高度
),
```

## 写一个多行输入框

```dart
TextField(
    maxLines: 4,//最大行数
    decoration: InputDecoration(//装饰器
   		hintText: "请输入回答",//没输入之前默认显示的文本
    	border: OutlineInputBorder()//边框样式
	),
),
```

- 可以通过**在其Controller属性中增加TextEditingController然后在之后的代码中访问TextEditingController的text属性来实现从控制器中取到输入的内容**，这是flutter官方推荐的技术方案。

  ```dart
  TextField(
    controller: questionData[index]
        ["textFieldController"], //官方推荐通过这个来获取textfield中的内容
    maxLines: 4, //最大行数
    decoration: InputDecoration(
        hintText: "请输入回答", //没输入之前默认显示的文本
        border: OutlineInputBorder() //边框样式
        ),
  ),
  ```

  

## 写一个可以选择时间的按钮，选择的时间显示到按钮上

- 需要一个第三方库，不过这个库好像不怎么兼容Flutter3，会报一点错，要么等更新，要么自己根据提示改改：

  ```yaml
  flutter_datetime_picker: ^1.5.1
  ```

- 然后就是代码实现：

  ```dart
  ElevatedButton(
      onPressed: () {
        DatePicker.showDatePicker(context,
            showTitleActions: true,
            minTime: DateTime(1500, 1, 1),
            maxTime: DateTime(3000, 12, 31), onChanged: (date) {//选项切换时的行为
          //print('change $date');
        }, onConfirm: (selected) {//选好后的行为
          //print(date);
          setState(() {
            //更新date
            //拼接成年/月/日的日期格式
            date = selected.year.toString() +
                "/" +
                selected.month.toString() +
                "/" +
                selected.day.toString();
            //print(date);
          });
        }, currentTime: DateTime.now(), locale: LocaleType.en);
      },
      child: date.compareTo("") == 0
          ? Text("请选择时间")
          : Text(date), //文字
      style: ElevatedButton.styleFrom(
        //调整按钮大小用
        minimumSize: const Size(150, 60),
      ),
  ),
  ```


## 循环动态生成组件

- 有一个需求，让你生成一个问题，问题的选项不固定，怎么搞？可以用循环生成组件的方式来动态生成组件：

- 单选版本：

  ```dart
  List<Widget> options = []; //问题选项
  Widget optionsContainer = new Column(
    //这个封装了一下所有循环生成的组件，就可以用在别的地方了。
    children: options,
  );
  if (questionType < 3) {
    for (int i = 0; i < optionNum; ++i) {
      //循环生成选项
      Widget option = new Row(
        mainAxisAlignment: MainAxisAlignment.center, //居中
        children: [
          Radio(
              value: i, //当前这个单选框的id
              groupValue: this.optionSelected, //当前这个组中被选中的单选框的id
              onChanged: (v) {
                //在改变选择的时候的行为，v是重新选择的那个单选框的id
                setState(() {
                  if (v is int) {
                    //加个类型判断，不然不好过编译
                    this.optionSelected = v;
                  }
                });
              }),
          SizedBox(
            width: 10,
          ),
          Text(questions[index]["options"][i]["optionContent"]),
        ],
      );
      options.add(option);
      options.add(new SizedBox(
        height: 30,
      ));
    }
  }
  ```
  
- 多选版本：

  ```dart
  else if (questionType == 1) {
  	for (int i = 0; i < optionNum; ++i) {
  	  optionSelectedMulti.add(false);
  	}
  	for (int i = 0; i < optionNum; ++i) {
  	  //循环生成选项
  	  Widget option = new Row(
  	    mainAxisAlignment: MainAxisAlignment.center, //居中
  	    children: [
  	      Checkbox(
  	          value: optionSelectedMulti[i],//是否被选中，是个bool
  	          onChanged: (v) {//这个v是true
  	            //print(v);
  	            if (v is bool) {
  	              setState(() {
  	                optionSelectedMulti[i] = v;
  	              });
  	            }
  	          }),
  	      SizedBox(
  	        width: 10,
  	      ),
  	      Text(questions[index]["options"][i]["optionContent"]),
  	    ],
  	  );
  	  options.add(option);
  	  options.add(new SizedBox(
  	    height: 30,
  	  ));
  	}
  }
  ```


## 写一个下拉选择列表

- 写这个的时候挺有讲究，我改的官方的例子，官方的例子写的真不错，我写的flutter老是推断不出来泛型= =

  ```dart
  else if (questionType == 2) {
  	String value = "";
  	List<String> temp = [];
  	for (int i = 0; i < optionNum; ++i) {
  	  temp.add(questions[index]["options"][i]["optionContent"]);
  	}
  	if (dropdownValue.isEmpty)
  	  value = temp[0];
  	else
  	  value = dropdownValue;
  	//dropdownValue = temp[0];
  	//print(temp);
  	optionsContainer = new DropdownButton<String>(
  	    hint: Text("请输入"),
  	    value: value, //显示的值
  	    items: temp.map<DropdownMenuItem<String>>((String value) {
  	      //列表项，这里用map来生成
  	      return DropdownMenuItem<String>(
  	        value: value,
  	        child: Text(value),
  	      );
  	    }).toList(),
  	    onChanged: (v) {
  	      //改变选择时的行为
  	      //print(v);
  	      setState(() {
  	        if (v is String) this.dropdownValue = v;
  	      });
  	    }
      );
  }
  ```


## 显示SnackBar

- SnackBar就是最下面的那个提示信息。

![image-20220921111214108](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220921111214108.png)

- 示例代码：

  ```dart
  ScaffoldMessenger.of(context).showSnackBar(//不能直接在Scaffold里使用
      SnackBar(
    content: Text('没有上一题了哦'),
    action: SnackBarAction(
      label: "关闭",
      onPressed: () {
        //print('撤回');
      },
    ),
  ));
  ```


## flutter实现组件的绝对定位

- 平时写组件的位置都是相对位置，但是需求需要实现组件的绝对定位，于时就去网上看了看实现方式，实现起来也不是很复杂。

- 效果图如下，最下面的两个按钮是绝对位置：

  ![image-20220921113214382](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220921113214382.png)

- 需要使用到的组件：
  1. ConstrainedBox：尺寸限制类容器组件。
  2. Stack：将子组件叠加显示。
  3. Positioned：用于定位Stack子组件

- 实现代码：

  ```dart
  @override
  Widget build(BuildContext context) {
    //print(widget.arguments!["id"]);
    return Scaffold(
      appBar: new AppBar(
        title: new Text(
          "正在填写:" + arguments!["title"],
          style: new TextStyle(color: Colors.white),
        ),
      ),
      body: Center(
        //搞绝对定位
        child: ConstrainedBox(
          constraints: BoxConstraints.expand(),
          child: Stack(
            alignment: Alignment.center,
            children: <Widget>[
              ExamBody(), //进度条和问题部分
              Positioned(//对其包裹的组件进行绝对定位
                bottom: 70,//距离底部70的绝对位置
                child: Row(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: [
                    ElevatedButton(
                        style: ElevatedButton.styleFrom(
                          minimumSize: Size(100, 50),
                        ),
                        onPressed: () {
                          if (questionNow == 0) {
                            ScaffoldMessenger.of(context)
                                .showSnackBar(//不能直接在Scaffold里使用
                                    SnackBar(
                              content: Text('没有上一题了哦'),
                              action: SnackBarAction(
                                label: "关闭",
                                onPressed: () {
                                  //print('撤回');
                                },
                              ),
                            ));
                          } else {
                            setState(() {
                              questionNow--;
                              // print(questionNow.toString() +
                              //     " " +
                              //     questionTotal.toString());
                            });
                          }
                        },
                        child: Text("上一题")),
                    SizedBox(
                      width: 150,
                    ),
                    ElevatedButton(
                        style: ElevatedButton.styleFrom(
                          minimumSize: Size(100, 50),
                        ),
                        onPressed: () {
                          if (questionNow == questionTotal - 1) {
                            ScaffoldMessenger.of(context)
                                .showSnackBar(//不能直接在Scaffold里使用
                                    SnackBar(
                              content: Text('没有下一题了哦'),
                              action: SnackBarAction(
                                label: "关闭",
                                onPressed: () {
                                  //print('撤回');
                                },
                              ),
                            ));
                          } else {
                            setState(() {
                              questionNow++;
                              // print(questionNow.toString() +
                              //     " " +
                              //     questionTotal.toString());
                            });
                          }
                        },
                        child: Text("下一题")),
                  ],
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }
  ```

## 在顶部导航栏上增加按钮

- 效果图：

  ![image-20220921114740153](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220921114740153.png)

- 示例代码：

  ```dart
  class Home extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Scaffold(
          appBar: AppBar(
            leading: IconButton(
              icon: Icon(Icons.menu),
              tooltip: 'Navigreation',
              onPressed: () => debugPrint('Navigreation button is pressed'),
            ),
            title: Text('导航'),
            actions: <Widget>[
              IconButton(//也可以换成TextButton啥的=w=
                icon: Icon(Icons.search),
                tooltip: 'Search',
                onPressed: () => debugPrint('Search button is pressed'),
              ),
              IconButton(
                icon: Icon(Icons.more_horiz),
                tooltip: 'More',
                onPressed: () => debugPrint('More button is pressed'),
              )
            ],
          ),
          body: null);
    }
  }
  ```

### AppBar:leading

- 它是顶部导航栏最左边的按钮,IconButton便是按钮组件，里面的icon就是按钮图标,Icons是内置的一些图标样式。tooltip是按钮说明，onPressed是按钮事件，我们通过debugPrint可以看到点击按钮后，在控制台输出对应的文字。

### AppBar:actions

- 它是顶部导航栏右方的一排组件。 上面代码我们定义了搜索和...两个按钮，分别设置了其对应的按钮事件。

## Dio类中的方法的参数说明

- queryParameters：这个是指明请求参数，就是在请求路径后面拼接的参数。
- data：这个是请求体，别和上面那个搞混了。

- 网络请求类代码示例：

  ```dart
  import 'package:dio/dio.dart';
  import 'Config.dart';
  
  class Request {
    static Future<T> request<T>(String url,
        {String method = 'get', Map<String, dynamic>? params}) async {
      url = Config.qvsHost + url;
      try {
        if (method.toLowerCase().compareTo("get") == 0) {
          Response response = await Dio().get(url,
              queryParameters: params,
              options:
                  new Options(contentType: 'application/json;charset=utf-8'));
          //print(response);
          return response.data;
        } else if (method.toLowerCase().compareTo("post") == 0) {
          //print(params);
          var response = await Dio().post(url,
              data: params,
              options:
                  new Options(contentType: 'application/json;charset=utf-8'));
          return response.data;
        } else if (method.toLowerCase().compareTo("put") == 0) {
          var response = await Dio().put(url,
              data: params,
              options:
                  new Options(contentType: 'application/json;charset=utf-8'));
          return response.data;
        } else if (method.toLowerCase().compareTo("delete") == 0) {
          var response = await Dio().delete(url,
              data: params,
              options:
                  new Options(contentType: 'application/json;charset=utf-8'));
          return response.data;
        } else {
          throw Exception();
        }
      } catch (e) {
        return Future.error(e);
      }
      //return Future.error(new Exception());
    }
  }
  ```


## 弹出提示框

- 可以用**showDialog方法**实现，不过里面的builder比较难写，要返回一个具体的提示框实例，下面是示例代码：

  ```dart
  showDialog(
    context: context,
    builder: (context) {
      return AlertDialog(
        title: Text("提示"),
        //title 的内边距，默认 left: 24.0,top: 24.0, right 24.0
        //默认底部边距 如果 content 不为null 则底部内边距为0
        //            如果 content 为 null 则底部内边距为20
        titlePadding: EdgeInsets.all(10),
        //标题文本样式
        titleTextStyle: TextStyle(
            color: Colors.black87, fontSize: 25),
        //中间显示的内容
        content: Text("提交成功！"),
        //中间显示的内容边距
        //默认 EdgeInsets.fromLTRB(24.0, 20.0, 24.0, 24.0)
        contentPadding: EdgeInsets.all(10),
        //中间显示内容的文本样式
        contentTextStyle: TextStyle(
            color: Colors.black54, fontSize: 20),
        //底部按钮区域
        actions: <Widget>[
          // TextButton(
          //   child: Text("取消"),
          //   onPressed: () {
          //     关闭 返回 false
          //     Navigator.of(context).pop(false);
          //   },
          // ),
          TextButton(
            child: Text(
              "确认",
              style: TextStyle(fontSize: 15),
            ),
            onPressed: () {
              //关闭 返回true
              Navigator.of(context).pop(true);
              Navigator.pop(context);
            },
          ),
        ],
      );
  });
  ```


## 写一个巨丑无比的上导航栏搜索框

![image-20220921182908894](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220921182908894.png)

- 实现代码：

  ```dart
  AppBar(
    title: Text("山师问卷系统"),
    actions: [
      Container(
        //在这儿TextField必须要设置长宽，不然会报错
        alignment: Alignment.center, //居中
        height: 20,
        width: 270,
        child: TextField(
          controller: textFieldController,
          decoration: InputDecoration(
            hintText: "搜索",
            hintStyle: TextStyle(
              color: Color.fromARGB(255, 80, 80, 80),
            ),
            border: InputBorder.none, //设置为无边框
          ),
          maxLines: 1,
        ),
      ),
      IconButton(
          //图标按钮
          onPressed: () {
            print(textFieldController.text);
          },
          icon: Icon(Icons.search)),
    ],
  ),
  ```

## 写个宽度无限的按钮，并设置成自己喜欢的颜色

- 宽度无限关键在于**给Container中的width属性设置为double.infinite**，颜色的设置主要通过ButtonStyle实现，不过里面的写法有点讲究：

  ```dart
  Container(
    height: 300,
    width: double.infinity,
    child: ElevatedButton.icon(
        style: new ButtonStyle(
            backgroundColor: MaterialStateProperty.all(Colors.blue),//设置按钮颜色
        ),
        onPressed: () {
          print("我要登录了！！！");
        },
        icon: Icon(
          Icons.person,
          size: 100,
        ),
        label: user["id"].isEmpty
            ? Text(
                "点击登录",
                style: TextStyle(fontSize: 30),
              )
            : Text(
                user["username"],
                style: TextStyle(fontSize: 30),
              )),
  ),
  ```

## 给Container加上边框

- 主要是用到了Container的decoration属性

  ```dart
  decoration:
  	//黑色，宽度为1的全包围边框
  	BoxDecoration(border: Border.all(color: Colors.black, width: 1)),
  ```


## 写一个可以填写内容的弹框

- 从网上毛的，有好几个组成部分，结构挺清晰的，可以根据自己的需要进行魔改：

- 工具类：

  ```dart
  import 'package:flutter/cupertino.dart';
  
  import 'package:flutter/material.dart';
  
  import 'package:flutter/widgets.dart';
  
  import '../../ui/Alert/ShowInputAlertWidget.dart';
  
  // import 'package:flutter_app1/module/dialogs/widget/bottom_widget.dart';
  
  // import 'package:flutter_app1/module/dialogs/widget/center_dialog.dart';
  
  // import 'package:flutter_app1/module/dialogs/widget/define_widget.dart';
  
  // import 'package:flutter_app1/module/dialogs/widget/input_dialog.dart';
  
  // import 'package:flutter_app1/module/dialogs/widget/style_dialog.dart';
  
  ///
  
  /// 自定义弹窗
  
  ///
  
  ///
  
  class AppTool {
    /// 底部弹出2个选项框
  
  //  showBottomAlert(BuildContext context, confirmCallback, String title,
  
  //  String option1, String option2) {
  
  // showCupertinoModalPopup(
  
  // context: context,
  
  //  builder: (context) {
  
  // return BottomCustomAlterWidget(
  
  // confirmCallback, title, option1, option2);
  
  //  });
  
  //  }
  
    /// 中间弹出提示框
  
  //  showCenterTipsAlter(
  
  // BuildContext context, confirmCallback, String title, String desText) {
  
  // showDialog(
  
  // context: context,
  
  //  builder: (BuildContext context) {
  
  // return CenterTipsAlterWidget(confirmCallback, title, desText);
  
  //  });
  
  //  }
  
    /// 中间弹出输入框
  
    showCenterInputAlert(BuildContext context, String title, String placeholder,
        String placeholder2) {
      showDialog(
          context: context,
          builder: (BuildContext context) {
            return ShowInputAlertWidget(title, placeholder, placeholder2);
          });
    }
  
    ///自定义弹框
  
  //  showStyleAlert(BuildContext context, confirmCallback, String title,
  
  //  String contentTitle) {
  
  // showDialog(
  
  // context: context,
  
  //  builder: (BuildContext context) {
  
  // return StyleDialog(confirmCallback, title, contentTitle);
  
  //  });
  
  //  }
  
    ///只有一个确定按钮的弹窗
  
  //  showDefineAlert(
  
  // BuildContext context, confirmCallback, String title, String hintText) {
  
  // showDialog(
  
  // context: context,
  
  //  builder: (BuildContext context) {
  
  // return ShowDefineAlertWidget(confirmCallback, title, hintText);
  
  //  });
  
  //  }
  
  }
  ```

- 弹框本体：

  ```dart
  import 'package:flutter/cupertino.dart';
  import 'package:flutter/gestures.dart';
  
  import 'package:flutter/widgets.dart';
  import 'package:questionnaire/utils/requests/Request.dart';
  
  ///
  
  /// 输入提示框
  
  ///
  
  class ShowInputAlertWidget extends StatefulWidget {
    final title;
  
    final placeholder;
  
    final Placeholder2;
  
    const ShowInputAlertWidget(this.title, this.placeholder, this.Placeholder2);
  
    @override
    _ShowInputAlertWidgetState createState() => _ShowInputAlertWidgetState();
  }
  
  class _ShowInputAlertWidgetState extends State<ShowInputAlertWidget> {
    String number = '';
    String password = '';
  
    @override
    Widget build(BuildContext context) {
      return CupertinoAlertDialog(
        title: Text(widget.title),
        content: Column(
          children: [
            SizedBox(
              height: 10,
            ),
            CupertinoTextField(
              placeholder: widget.placeholder,
              onChanged: (value) {
                number = value;
              },
            ),
            SizedBox(
              height: 5,
            ),
            CupertinoTextField(
              placeholder: widget.Placeholder2,
              onChanged: (value) {
                password = value;
              },
            )
          ],
        ),
        actions: [
          CupertinoDialogAction(
            child: Text('取消'),
            onPressed: () {
              Navigator.pop(context);
            },
          ),
          CupertinoDialogAction(
            child: Text('确定'),
            onPressed: () {
              //print("进行登录操作。。。" + number + " " + password);
              Request.request("ucenter/uni/user/login",
                      method: 'post',
                      params: {"number": number, "password": password},
                      service: 'ucenter')
                  .then((value) {
                print(value["data"]);
              });
            },
          )
        ],
      );
    }
  }
  ```


- 调用：

  ```dart
  AppTool().showCenterInputAlert(context, "登录", "帐号", "密码");
  ```


## 路由pop时携带参数返回，返回到的页面接收返回的参数

- 携带参数返回时要将参数写到**Navigator.pop()方法的第二个参数中**，然后调用该方法的方法**返回值写成Future\<T>**，然后**在调用处用then接收异步参数**。

- 路由pop的位置：

  ```dart
  if (value["success"]) {
    Navigator.pop(context, {
      "success": value["success"],
      "id": value["data"]["userVo"]["id"],
      "username": value["data"]["userVo"]["name"]
    });
  } else {
    Navigator.pop(context, {"success": value["success"]});
  }
  ```

- 封装的方法：

  ```dart
  Future<T?> showCenterInputAlert<T>(BuildContext context, String title,
      String placeholder, String placeholder2) {
    var value;
    showDialog(
        context: context,
        builder: (BuildContext context) {
          return ShowInputAlertWidget(title, placeholder, placeholder2);
        }).then((v) {
      value = v;
    });
    return value;
  }
  ```

- 调用处（这里没用封装的方法来调用）：

  ```dart
  showDialog(
      context: context,
      builder: (BuildContext context) {
        return ShowInputAlertWidget("登录", "帐号", "密码");
      }).then((value) {
    if (value["success"]) {
      ScaffoldMessenger.of(context)
          .showSnackBar(//不能直接在Scaffold里使用
              SnackBar(
        content: Text('登录成功！'),
        action: SnackBarAction(
          label: "关闭",
          onPressed: () {
            //print('撤回');
          },
        ),
      ));
      setState(() {
        user["id"] = value["id"];
        user["username"] = value["username"];
      });
    } else {
      ScaffoldMessenger.of(context)
          .showSnackBar(//不能直接在Scaffold里使用
              SnackBar(
        content: Text('用户名或密码错误！'),
        action: SnackBarAction(
          label: "关闭",
          onPressed: () {
            //print('撤回');
          },
        ),
      ));
    }
  });
  ```


## 以键值对的形式向缓存中存入数据

- 需要用到**shared_preferences**这个包，**支持int, double, bool, string与 stringList**类型的数据存储

- 异步获取实例：

  ```dart
  void initCacheInstance() async {
    cache = await SharedPreferences.getInstance();//使用await会阻塞该方法后面的代码，保证了异步数据可以到达
    if (cache.containsKey("id") && cache.containsKey("username")) {
      setState(() {
        user["id"] = cache.getString("id");
        user["username"] = cache.getString("username");
      });
    }
  }
  ```

- 存入数据，存别的类型的数据的话方法名以此类推：

  ```dart
  cache.setString("id", value["id"]);
  cache.setString("username", value["username"]);
  ```

- 取出数据：

  ```dart
  user["id"] = value.getString("id");
  user["username"] = value.getString("username");
  ```


## 路由返回时刷新ui界面

- 只需要**在路由跳转后面的.then方法中setState()即可**。

  ```dart
  Navigator.pushNamed(context, "/user").then((value) {
    setState(() {
      if (cache.containsKey("id") && cache.containsKey("username")) {
        user["id"] = cache.getString("id");
        user["username"] = cache.getString("username");
      }
    });
  });
  ```


## 做一个可以点击的title

- 用InkWell实现：

  ```dart
  title: InkWell(
    child: Text("山师问卷系统"),
    onTap: () {
      tapNum++;
      print(tapNum);
    },
  ),
  ```


# Flutter打包项目

- 使用命令**flutter build apk --no-sound-null-safety**可以不开空安全来打包项目
- 在打包的时候往往会报一堆错，报的错基本跟着他说的内容改改就差不多能改好，其它改不好的就往这写写以后长个记性。
