---
title: JavaWeb核心技术
date: 2022-06-25 21:17:57
tags: [Java,JavaWeb,HTML,CSS,JavaScript,Tomcat,Servlet,JSP,JSTL,EL,Ajax]
---

<meta name="referrer" content="no-referrer"/>

# 软件的结构

![image-20220627111044498](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220627111044498.png)

![image-20220720095912548](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220720095912548.png)

# 前端的开发流程

![image-20220627112715856](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220627112715856.png)

不过现在jsp基本上已经被淘汰掉了。

# 网页的组成部分

​	页面由三部分内容组成，分别是**内容（结构）、表现、行为**。 

​	内容（结构），是我们在页面中可以看到的数据。我们称之为内容。一般内容 我们使用html技术来展示。 

​	表现，指的是这些内容在页面上的展示形式。比如说。布局，颜色，大小等等。一般使用 CSS 技术实现。

​	行为，指的是页面中元素与输入设备交互的响应。一般使用 javascript 技术实现。

# HTML

## HTML简介

Hyper Text Markup Language （超文本标记语言） 简写：HTML 

HTML 通过**标签**来标记要显示的网页中的各个部分。网页文件本身是一种文本文件， 通过在文本文件中添加标记符，可以告诉浏览器如何显示其中的内容（如：文字如何处理，画 面如何安排，图片如何显示等） 

## HTML文件的书写规范

```html
<!DOCTYPE html>                 告知浏览器使用的html版本
<html lang="en">                表示整个 html 页面的开始，属性中声明所用语言 
	<head>                     	头信息
        <meta charset="UTF-8">  声明编码格式
		<title>标题</title>     标题 
	</head>
	<body>                      body 是页面的主体内容
    	页面主体内容 
	</body>
</html>                         表示整个 html 页面的结束

<!--这是html中的代码注释-->
```

## HTML标签介绍

1.标签的格式: 

​	<标签名>封装的数据</标签名> 

2.**标签名大小写不敏感**。 

3.标签拥有自己的属性。 

​	i. 分为**基本属性**：bgcolor=*"red"*   可以修改简单的样式效果 

​	ii.**事件属性**： onclick="alert('你好！');"  可以直接设置事件响应后的代码。 

4.标签又分为，单标签和双标签。 

​	i. 单标签格式： <标签名 /> **br 换行 hr 水平线**

​	ii. 双标签格式: <标签名> ...封装的数据...</标签名>

![image-20220627113930863](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220627113930863.png)

### 标签的语法规则

```html
<!-- ①标签不能交叉嵌套 --> 
正确：<div><span>早安，尚硅谷</span></div> 
错误：<div><span>早安，尚硅谷</div></span>
<hr /> 

<!-- ②标签必须正确关闭 --> 
<!-- i.有文本内容的标签： -->
正确：<div>早安，尚硅谷</div> 
错误：<div>早安，尚硅谷 <hr /> 
<!-- ii.没有文本内容的标签： --> 
正确：<br /> 错误：<br>
<hr /> 

<!-- ③属性必须有值，属性值必须加引号 -->
正确：<font color="blue">早安，尚硅谷</font> 
错误：<font color=blue>早安，尚硅谷</font>
错误：<font color>早安，尚硅谷</font>
<hr /> 

<!-- ④注释不能嵌套 --> 
正确：<!-- 注释内容 --> <br/> 
错误：<!-- <!-- 这是错误的 html 注释 --> -->
<hr />
```

有的时候出现例如标签没有闭合等错误时，页面仍然能正常显示，这是因为浏览器帮我们智能修复了我们的代码错误（浏览器是容错的）。

## 常用标签介绍

在w3cschool.CHM文档中有详细描述。

### font字体标签

```html
<body> 
   	<!-- 字体标签
	需求 1：在网页上显示 我是字体标签 ，并修改字体为 宋体，颜色为红色。 

	font 标签是字体标签,它可以用来修改文本的字体,颜色,大小(尺寸)
	color 属性修改颜色
	face 属性修改字体
	size 属性修改文本大小 
-->
    <font color="red" face="宋体" size="7">我是字体标签</font>
</body>
```

### 特殊字符

​	当我们想要把能被浏览器解析的html标签或者某些关键字作为文本输出到屏幕上的时候，如果直接将标签或关键字显式地写出来，那么就可能会导致浏览器错误解析，所以这种时候应该使用字符实体拼接成想要输出的内容来避免歧义。

#### 常用特殊字符表

![image-20220627114737035](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220627114737035.png)

#### 其他特殊字符表

![image-20220627115026563](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220627115026563.png)

```html
<body>
    <!-- 特殊字符 
	需求 1：把 <br> 换行标签 变成文本 转换成字符显示在页面上 
	
	常用的特殊字符: 
		< ===>>>> &lt;
		> ===>>>> &gt;
		空格 ===>>>> &nbsp;
	--> 
    我是&lt;br&gt;标签<br/> 国哥好 &nbsp;&nbsp;帅啊! 
</body>
```

### 标题标签

```html
<body> 
    <!-- 标题标签 需求 1：演示标题 1 到 标题 6 的
	h1 - h6 都是标题标签 h1 最大 h6 最小
	
	align 属性是对齐属性 
		left 左对齐(默认)
		center 居中
		right 右对齐 
--> 
	<h1 align="left">标题 1</h1>
	<h2 align="center">标题 2</h2>
	<h3 align="right">标题 3</h3>
	<h4>标题 4</h4>
	<h5>标题 5</h5>
	<h6>标题 6</h6>
	<h7>标题 7</h7>
</body>
```

### 超链接

在网页中所有点击之后可以跳转的内容都是超链接。

```html
<body>
    <!-- a 标签是 超链接 
		href 属性设置连接的地址 
		target 属性设置哪个目标进行跳转 
			_self 表示当前页面(默认值) 
			_blank 表示打开新页面来进行跳转
			_parent 在父窗口打开
			_top 在顶层窗口打开
-->
<a href="http://localhost:8080">百度</a><br/>
<a href="http://localhost:8080" target="_self">百度_self</a><br/>
<a href="http://localhost:8080" target="_blank">百度_blank</a><br/> </body>
```

### 列表标签

```html
<body>
    <!--需求 1：使用无序，列表方式，把东北 F4，赵四，刘能，小沈阳，宋小宝，展示出来 
	ol是有序列表
		type 属性可以修改列表项前面的符号，有A a I i 1（默认）五种选项，A是大写字母，a是小写字母，I是大写希腊数字，i是小写希腊数字，1是数字。
		start 表示从第几号开始
	ul 是无序列表 
		type 属性可以修改列表项前面的符号，有disc(默认)、circle、square等选项，详情见帮助文档。
	li 是列表项 --> 
    <ul type="none"> 
        <li>赵四</li> 
        <li>刘能</li> 
        <li>小沈阳</li> 
        <li>宋小宝</li> 
    </ul>
</body>
```

### img标签

img标签可以在html页面上显示图片。

```html
<body> 
    <!--需求 1：使用 img 标签显示一张美女的照片。并修改宽高，和边框属性 
	img 标签是图片标签,用来显示图片 
		src 属性可以设置图片的路径 
		width 属性设置图片的宽度 
		height 属性设置图片的高度 
		border 属性设置图片边框大小 
		alt 属性设置当指定路径找不到图片时,用来代替显示的文本内容
	在 JavaSE 中路径也分为相对路径和绝对路径. 
		相对路径:从工程名开始算 
		绝对路径:盘符:/目录/文件名 
	在 web 中路径分为相对路径和绝对路径两种 
		相对路径: 
			. 表示当前文件所在的目录 
			.. 表示当前文件所在的上一级目录 
			文件名 表示当前文件所在目录的文件,相当于 ./文件名 ./ 可以省略 
		绝对路径:
			正确格式是: http://ip:port/工程名/资源路径 
			错误格式是: 盘符:/目录/文件名 --> 
<img src="1.jpg" width="200" height="260" border="1" alt="美女找不到"/>
<img src="../2.jpg" width="200" height="260" /> 
<img src="../imgs/3.jpg" width="200" height="260" /> 
<img src="../imgs/4.jpg" width="200" height="260" />
<img src="../imgs/5.jpg" width="200" height="260" />
<img src="../imgs/6.jpg" width="200" height="260" /> 
</body>
```

### 表格标签

```html
<body> 
    <!--需求 1：做一个 带表头的 ，三行，三列的表格，并显示边框 
		需求 2：修改表格的宽度，高度，表格的对齐方式，单元格间距。 			table 标签是表格标签 
			border 设置表格标签 
			width 设置表格宽度 
			height 设置表格高度 
			align 设置表格相对于页面的对齐方式
			cellspacing 设置单元格间距
			cellpadding 设置单元格边沿与其内容之间的空白
		tr 是行标签 
		th 是表头标签 
		td 是单元格标签
			align 设置单元格文本对齐方式 
		b 是加粗标签 --> 
<table align="center" border="1" width="300" height="300" cellspacing="0"> 
    <tr>
        <th>1.1</th> 
        <th>1.2</th> 
        <th>1.3</th> 
    </tr> 
    <tr>
        <td>2.1</td>
        <td>2.2</td>
        <td>2.3</td> 
    </tr> 
    <tr>
        <td>3.1</td> 
        <td>3.2</td> 
        <td>3.3</td>
    </tr> 
</table> 
</body>
```

###  跨行跨列表格

```html
<body> 
    <!-- 需求 1： 新建一个五行，五列的表格， 
		第一行，第一列的单元格要跨两列，
		第二行第一列的单元格跨两行，
		第四行第四列的单元格跨两行两列。 
		colspan 属性设置跨列 
		rowspan 属性设置跨行 --> 
<table width="500" height="500" cellspacing="0" border="1"> 	<tr>
    	<td colspan="2">1.1</td>
    	<td>1.3</td> 
    	<td>1.4</td> 
    	<td>1.5</td> 
    </tr> 
    <tr>
		<td rowspan="2">2.1</td> 
        <td>2.2</td> <td>2.3</td> 
        <td>2.4</td> <td>2.5</td> 
    </tr> 
    <tr>
        <td>3.2</td> 
        <td>3.3</td>
        <td>3.4</td>
        <td>3.5</td>
    </tr>
    <tr>
        <td>4.1</td> 
        <td>4.2</td> 
        <td>4.3</td>
        <td colspan="2" rowspan="2">4.4</td> 
    </tr> 
    <tr>
        <td>5.1</td> 
        <td>5.2</td>
        <td>5.3</td> 
    </tr> 
</table> 
</body>
```

### 了解iframe框架标签（内嵌窗口）

```html
<body> 
    我是一个单独的完整的页面<br/><br/>
    <!--ifarme 标签可以在页面上开辟一个小区域显示一个单独的页面 
		ifarme 和 a 标签组合使用的步骤: 
			1 在 iframe 标签中使用 name 属性定义一个名称
			2 在 a 标签的 target 属性上设置 iframe 的 name 的属性值 --> 
<iframe src="3.标题标签.html" width="500" height="400" name="abc"></iframe> 
<br/>
<ul>
    <li><a href="0-标签语法.html" target="abc">0-标签语法.html</a></li>
    <li><a href="1.font 标签.html" target="abc">1.font 标签.html</a></li>
    <li><a href="2.特殊字符.html" target="abc">2.特殊字符.html</a></li>
</ul> 
</body>

<!--
	下面两个标签几乎已经被淘汰了
	<frameset></frameset> 里面可以放入多个frame页面
	<frame></frame> 一个页面 src属性标识页面文件的路径
-->
```

### 表单标签

![image-20220703233836729](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220703233836729.png)

#### 表单的显示

```html
<body> 
    <!--需求 1:创建一个个人信息注册的表单界面。包含用户名，密码，确认密码。性别（单选），兴趣爱好（多选），国籍（下拉列表）。 隐藏域，自我评价（多行文本域）。重置，提交。--> 
    <!--
		form 标签就是表单 
			input type=text 是文件输入框 value 设置默认显示内容 
			input type=password 是密码输入框 value 设置默认显示内容 
			input type=radio 是单选框 name 属性可以对其进行分组 checked="checked"表示默认选中
			input type=checkbox 是复选框 checked="checked"表示默认选中
			input type=reset 是重置按钮 value 属性修改按钮上的文本 
			input type=submit 是提交按钮 value 属性修改按钮上的文本 
			input type=button 是按钮 value 属性修改按钮上的文本 				input type=file 是文件上传域
			input type=hidden 是隐藏域 当我们要发送某些信息，而这些信息，不需要用户参与，就可以使用隐藏域（提交的 时候同时发送给服务器） 		select 标签是下拉列表框 
			option 标签是下拉列表框中的选项 selected="selected"设置默认选中
			textarea 表示多行文本输入框 （起始标签和结束标签中的内容是默认值） 
				rows 属性设置可以显示几行的高度 
				cols 属性设置每行可以显示几个字符宽度 --> 
<form> 
    用户名称：<input type="text" value="默认值"/><br/> 
    用户密码：<input type="password" value="abc"/><br/> 
    确认密码：<input type="password" value="abc"/><br/> 
    性别：<input type="radio" name="sex"/>男<input type="radio" name="sex" checked="checked" />女<br/> 
    兴趣爱好：<input type="checkbox" checked="checked" />Java<input type="checkbox" />JavaScript<input type="checkbox" />C++<br/> 
    国籍：<select> 
    		<option>--请选择国籍--</option> 
    		<option selected="selected">中国</option> 				<option>美国</option> 
    		<option>小日本</option> 
    	</select><br/> 
    自我评价：<textarea rows="10" cols="20">我才是默认值</textarea><br/> 
    <input type="reset" value="abc" /> 
    <input type="submit"/> 
</form> 
</body>
```

#### 表单格式化

```html
<form> 
    <h1 align="center">用户注册</h1> 
    <table align="center"> 
        <tr>
            <td> 用户名称：</td> 
            <td><input type="text" value="默认值"/> </td> 
        </tr> 
        <tr>
            <td> 用户密码：</td> 
            <td><input type="password" value="abc"/></td> 
        </tr> 
        <tr>
            <td>确认密码：</td> 
            <td><input type="password" value="abc"/></td> 
        </tr> 
        <tr>
            <td>性别：</td>
            <td>
                <input type="radio" name="sex"/>男 
                <input type="radio" name="sex" checked="checked" />女 
            </td> 
        </tr> 
        <tr>
            <td> 兴趣爱好：</td> 
            <td>
                <input type="checkbox" checked="checked" />Java 
                <input type="checkbox" />JavaScript 
                <input type="checkbox" />C++ 
            </td> 
        </tr> 
        <tr>
            <td>国籍：</td> 
            <td>
                <select> 
                    <option>--请选择国籍--</option> 
                    <option selected="selected">中国</option> 
                    <option>美国</option> 
                    <option>小日本</option> 
                </select> 
            </td> 
        </tr> 
        <tr>
            <td>自我评价：</td>
            <td><textarea rows="10" cols="20">我才是默认值</textarea></td> 
        </tr> 
        <tr>
            <td><input type="reset" /></td> 
            <td align="center"><input type="submit"/></td> 
        </tr> 
    </table> 
</form> 
</body>
```

#### 表单提交细节

```html
<body> 
    <!--
		form 标签是表单标签
			action 属性设置提交的服务器地址
			method 属性设置提交的方式 GET(默认值)或 POST 
		表单提交的时候，数据没有发送给服务器的三种情况： 
			1、表单项没有 name 属性值 
			2、单选、复选（下拉列表中的 option 标签）都需要添加 value 属性，以便发送给服务器 
			3、表单项不在提交的 form 标签中 
		GET 请求的特点是：
			1、浏览器地址栏中的地址是：action 属性[+?+请求参数] 请求参数的格式是：name=value&name=value
			2、不安全 
			3、它有数据长度的限制
		POST 请求的特点是： 
			1、浏览器地址栏中只有 action 属性值
			2、相对于 GET 请求要安全 
			3、理论上没有数据长度的限制 --> 
<form action="http://localhost:8080" method="post"> 
    <input type="hidden" name="action" value="login" />
    <h1 align="center">用户注册</h1> 
    <table align="center"> 
        <tr>
            <td> 用户名称：</td>
            <td>
                <input type="text" name="username" value="默认值"/> 
            </td> 
        </tr> 
        <tr>
            <td> 用户密码：</td> 
            <td>
                <input type="password" name="password" value="abc"/>
            </td> 
        </tr> 
        <tr>
            <td>性别：</td> 
            <td>
                <input type="radio" name="sex" value="boy"/>男 
                <input type="radio" name="sex" checked="checked" value="girl" />女 
            </td> 
        </tr> 
        <tr>
            <td> 兴趣爱好：</td> 
            <td>
                <input name="hobby" type="checkbox" checked="checked" value="java"/>Java 
                <input name="hobby" type="checkbox" value="js"/>JavaScript 
                <input name="hobby" type="checkbox" value="cpp"/>C++ 
            </td> 
        </tr> 
        <tr>
            <td>国籍：</td> 
            <td>
                <select name="country"> 
                    <option value="none">--请选择国籍--</option> 
                    <option value="cn" selected="selected">中国</option> 
                    <option value="usa">美国</option> 
                    <option value="jp">小日本</option> 
                </select> 
            </td>
        </tr> 
        <tr>
            <td>自我评价：</td>
            <td><textarea name="desc" rows="10" cols="20">我才是默认值</textarea></td>
        </tr>
        <tr>
            <td><input type="reset" /></td> 
            <td align="center"><input type="submit"/></td> 
        </tr> 
    </table>
</form> 
</body>
```

### 其他常用标签

```html
<body> 
    <!--需求 1：div、span、p 标签的演示 
		div 标签 默认独占一行 
		span 标签 它的长度是封装数据的长度 
		p 段落标签 默认会在段落的上方或下方各空出一行来（如果已有就不再空）
		<b> </b> 文本加粗
		<i> </i> 文本变斜体
		<u> </u> 文本加下划线
		<sub> </sub> 文本变下标
		<sup> </sup> 文本变上标
--> 
    <div>div 标签 1</div>
    <div>div 标签 2</div>
    <span>span 标签 1</span>
    <span>span 标签 2</span>
    <p>p 段落标签 1</p> 
    <p>p 段落标签 2</p> 
</body>
```

# CSS技术

## CSS技术介绍

- CSS 是「层叠样式表单」。是用于(增强)控制网页样式并允许将样式信息与网页内容分离的一种标记性语言。

## CSS语法规则

![image-20220711161816444](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220711161816444.png)

- **选择器**：浏览器根据“选择器”决定受CSS样式影响的HTML元素（标签）。

- **属性（property）**是你要改变的样式名，并且每个属性都有一个或多个**值**。属性和值被冒号分开，并由花括号包围，这样就组成了一个完整的样式声明（declaration），例如：p{color:blue}

- **多个声明**：如果要定义不止一个声明，则需要用分号将每个声明分开。虽然最后一条声明的最后可以不加分号（但尽量在每条声明的末尾都加上分号）例如：

  ```css
  p{
      color:red;
      font-size:30px;
  }/*一般每行只描述一个属性*/
  ```

- **CSS注释**：

  ```css
  /*
  多行注释内容
  */
  ```

## CSS和HTML的结合方式

### 第一种：在属性上设置样式（内联样式）

- 在标签的 **style 属性**上设置”key:value value;”，修改标签样式。

```html
<!DOCTYPE html>
<html lang="en"> 
<head> 
	<meta charset="UTF-8"> 
	<title>Title</title> 
</head> 
<body> 
	<!--需求 1：分别定义两个 div、span 标签，分别修改每个 div 标签的样式为：边框 1 个像素，实线，红色。--> 
	<div style="border: 1px solid red;">div 标签 1</div>
	<div style="border: 1px solid red;">div 标签 2</div>
	<span style="border: 1px solid red;">span 标签 1</span> 
	<span style="border: 1px solid red;">span 标签 2</span> 
</body> 
</html>
```

- 缺点：
  1. 如果标签多了。样式多了。代码量非常庞大。
  2. 可读性非常差。
  3. 这样的代码没什么复用性可言。

### 第二种：在head标签中定义样式

- 在 head 标签中，使用**style 标签**来定义各种自己需要的 css 样式。

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
	<!--style标签专门用来定义css样式代码-->
	<style type="text/css">
		/*需求1:分别定义两个div、span标签，分别修改每个div标签的样式为:边框1个像素，实线，红色。*/
		div{
			border: 1px solid red;
		}
		span{
			border: 1px solid red;
		}
	</ style>
</ head>
        
<body>
	<div>div标签1</div>
	<div>div标签2</div>
	<span>span标签1</span>
	<span>span标签2</span>
</ body>
</html>

```

- 缺点：
  1. 只能在同一页面内复用代码，不能在多个页面中复用 css 代码。
  2. 维护起来不方便，实际的项目中会有成千上万的页面，要到每个页面中去修改。工作量太大了。

### 第三种：编写独立的CSS文件再引用

- 把 css 样式写成一个单独的 css 文件，再通过 link 标签引入即可复用。

- 使用 html 的 `<link rel="stylesheet" type="text/css" href="./styles.css" />` 标签 导入 css 样式文件。

- CSS文件内容：

  ```css
  div{
      border: 1px solid yellow; 
  }
  span{
      border: 1px solid red; 
  }
  ```

- HTML文件代码：

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
      <title>Title</title>
      <!--link标签专门用来引入css样式代码-->
      <link rel="stylesheet" type="text/css" href="1.css" />
  </head>
  <body>
  	<div>div标签1</div>
      <div>div标签2</div>
      <span>span标签1</span>
      <span>span标签2</span>
  </body>
  </html>
  ```

## 常用CSS选择器

### 标签名选择器

- 标签名选择器的格式是：

  ```css
  标签名{
      属性:值...;
      ...
  }
  ```

  标签名选择器，可以决定哪些标签会被动地使用这个样式。

- 示例代码：

  ```html
  <!DOCTYPE html>
  <html>
      <head>
          <meta charset="UTF-8">
          <title>CSS 选择器</title> 
          <style type="text/css"> 
              div{
                  border: 1px solid yellow; 
                  color: blue;
                  font-size: 30px;
              }
              span{ 
                  border: 5px dashed blue; 
                  color: yellow; 
                  font-size: 20px; 
              } 
          </style> 
      </head> 
      <body> 
          <!-- 需求 1：在所有 div 标签上修改字体颜色为蓝色，字体大小 30 个像素。边框为 1 像素黄色实线。
  并且修改所有 span 标签的字体颜色为黄色，字体大小 20 个像素。边框为 5 像素蓝色虚线。 --> 
          <div>div 标签 1</div>
          <div>div 标签 2</div> 
          <span>span 标签 1</span>
          <span>span 标签 2</span> 
      </body> 
  </html>
  ```

### id选择器

- id选择器的格式是：

  ```css
  #id属性值{
      属性:值...;
      ...
  }
  ```

  id选择器，可以决定具有特定id属性值的标签会被动地使用这个样式，每个标签的id属性值尽可能不重复。

- 示例代码：

  ```html
  <!DOCTYPE html>
  <html> 
      <head>
          <meta charset="UTF-8"> 
          <title>ID 选择器</title> 
          <style type="text/css"> 
              #id001{ 
                  color: blue; 
                  font-size: 30px;
                  border: 1px yellow solid;
              }
              #id002{ 
                  color: red; 
                  font-size: 20px; 
                  border: 5px blue dotted ; 
              } 
          </style> 
      </head> 
      <body> 
          <!-- 需求 1：分别定义两个 div 标签， 第一个 div 标签定义 id 为 id001 ，然后根据 id 属性定义 css 样式修改字体颜色为蓝色， 字体大小 30 个像素。边框为 1 像素黄色实线。 第二个 div 标签定义 id 为 id002 ，然后根据 id 属性定义 css 样式 修改的字体颜色为红色，字体大小 20 个像素。 边框为 5 像素蓝色点线。 --> 
          <div id="id002">div 标签 1</div>
          <div id="id001">div 标签 2</div> 
      </body> 
  </html>
  ```

### class选择器（类选择器）

- 类选择器的格式是：

  ```css
  .class属性值{
      属性:值...;
      ...
  }
  ```

  类选择器，可以决定具有特定class属性值的标签会被动地使用这个样式，每个标签的class属性值是可以重复的。

- 示例代码：

  ```html
  <!DOCTYPE html>
  <html>
      <head> 
          <meta charset="UTF-8">
          <title>class 类型选择器</title>
          <style type="text/css"> 
              .class01{ 
                  color: blue; 
                  font-size: 30px;
                  border: 1px solid yellow;
              }
              .class02{ 
                  color: grey; 
                  font-size: 26px;
                  border: 1px solid red; 
              } 
          </style>
      </head> 
      <body> 
          <!--需求 1：修改 class 属性值为 class01 的 span 或 div 标签，字体颜色为蓝色，字体大小 30 个像素。边框为 1 像素黄色实线。 需求 2：修改 class 属性值为 class02 的 div 标签，字体颜色为灰色，字体大小 26 个像素。边框为 1 像素红色实线。 --> 
          <div class="class02">div 标签 class01</div>
          <div class="class02">div 标签</div>
          <span class="class02">span 标签 class01</span> 
          <span>span 标签 2</span>
      </body>
  </html>
  ```

### 组合选择器（并集选择器）

- 组合选择器的格式是：

  ```css
  选择器1,选择器2,...,选择器n{
      属性:值...;
      ...
  }
  ```

  组合选择器，可以让多个选择器共用同一个css样式代码，也就是说只要标签中有其中之一的选择器，这个标签就会套用组合选择器里面的样式。

- 示例代码：

  ```html
  <!DOCTYPE html> 
  <html>
      <head> 
          <meta charset="UTF-8"> 
          <title>class 类型选择器</title> 
          <style type="text/css"> 
              .class01 , #id01{ 
                  color: blue; 
                  font-size: 20px; 
                  border: 1px yellow solid; 
              } 
          </style> 
      </head>
      <body> 
          <!-- 需求 1：修改 class="class01" 的 div 标签 和 id="id01" 所有的 span 标签， 字体颜色为蓝色，字体大小 20 个像素。边框为 1 像素黄色实线。 -->
          <div id="id01">div 标签 class01</div> <br />
          <span >span 标签</span> <br /> 
          <div>div 标签</div> <br /> 
          <div>div 标签 id01</div> <br /> 
      </body> 
  </html>
  ```

### 交集选择器

- 交集选择器的格式是：
	```css
	选择器1选择器2...选择器n{
    	属性:值...;
    	...
	}
	```

交集选择器，标签中必须有其中所有的选择器，这个标签才会套用交集选择器里面的样式。

### 后代选择器

- 后代选择器的格式是：
	```css
	选择器1 选择器2{
    	属性:值...;
    	...
	}
	```

后代选择器，选择的是具有选择器1的标签的后代中具有选择器2的标签，只有满足这种情况这个标签才会套用后代选择器里面的样式。

## 常用样式

### 内嵌元素和块级元素

我对这方面的认知还只停留在，内嵌元素无法对设置的宽高做出响应，也就是说只有块级元素才能按照设置的宽高进行显示，而采用flex的display后，该标签的子标签就自动变为块级元素了。

还有父容器的大小会被子元素”撑开“。

### 字体颜色

- color：red； 
- 颜色可以写颜色名如：black, blue, red, green 等 
- 颜色也可以写 rgb 值和十六进制表示值：如 rgb(255,0,0)，#00F6DE，如果写十六进制值必须加#

### 宽度

- width:19px;
- 宽度可以写像素值：19px;
- 也可以写百分比值：20%;

### 高度

- height:20px;
- 高度可以写像素值：19px；
- 也可以写百分比值：20%；

### 背景颜色

- background-color:#0F2D4C

### 字体样式

- color：#FF0000；字体颜色红色
- font-size：20px; 字体大小

### 红色1像素实线边框

- border：1px solid red;

### div居中

- margin-left: auto;
- margin-right: auto;

### 文本居中

- text-align: center;

### 超链接去掉下划线

- text-decoration: none;

### 表格细线

```css
table { 
    border: 1px solid black; /*设置边框*/ 
    border-collapse: collapse; /*将边框合并*/ 
}
td,th {
    border: 1px solid black; /*设置边框*/ 
}
```

### 列表去除修饰

```css
ul { 
    list-style: none; 
}
```

### 间距

- margin-top/right/bottom/left:20px 上右下左边距
- margin: auto; 上右下左边距平分，体现在元素的逻辑中心出现在父容器的几何正中心

### 填充

- padding: 20px 10px; 上下20px边距 左右10px边距

用法几乎和margin差不多，详情可以查资料。

### 定位

- 最左上角为原点，从左往右是x轴正向，从上往下是y轴正向。

- position: relative/absolute/... 相对/绝对/...定位，搭配top、left、right、bottom和像素值属性可以进行相应的定位。
- 绝对定位寻找最近的开启定位的祖先为定位的参考系
- 相对定位以父容器为定位的参考系

### 浮动

- float: top/right/bottom/left 向上/右/下/左浮动，直到碰到父元素的边界，浮动后对立面的空间会被空出来，从而可以使某些元素合并到对立面上。

### 设置显示优先级

- z-index: 100 默认为0，越高显示在越上面

### 设置圆角

- border-radius: 50%; 后面也可以跟像素，数值越大就越圆

### 设置布局

- display: flex; 弹性布局，默认横向
- flex-direction: column;设置弹性布局为纵向

### 旋转的动画效果

```css
.something{
    transform-origin: 40px 0;/*运动轴改为向右40像素，默认为左上角的点*/
  	transform: rotate(-20deg);/*逆时针旋转20度*/
    transition: transform 1s;/*设置transform的时间为1s*/
}
```

### CSS盒子模型

1. border 边框
2. margin 间距
3. padding 填充



**未完待续**



### 示例代码

```html
<!DOCTYPE html>
<html> 
    <head>
        <meta charset="UTF-8">
        <title>06-css 常用样式.html</title> 
        <style type="text/css"> 
            div{
                color: red; 
                border: 1px yellow solid;
                width: 300px; height: 300px;
                background-color: green; 
                font-size: 30px; margin-left: auto;
                margin-right: auto; 
                text-align: center;
            }
            table{ 
                border: 1px red solid;
                border-collapse: collapse; 
            }td{
                border: 1px red solid; 
            }
            a{ 
                text-decoration: none; 
            }
            ul{ 
                list-style: none; 
            } 
        </style> 
    </head> 
    <body>
        <ul>
            <li>11111111111</li> 
            <li>11111111111</li>
            <li>11111111111</li>
            <li>11111111111</li> 
            <li>11111111111</li> 
        </ul>
        <table>
            <tr>
                <td>1.1</td>
                <td>1.2</td> 
            </tr> 
        </table> 
        <a href="http://www.baidu.com">百度</a>
        <div>我是 div 标签</div>
    </body> 
</html>
```

## CSS样式覆盖规则

### 规则一：由于继承而发生样式冲突时，最近祖先获胜。

CSS的继承机制使得元素可以从包含它的祖先元素中继承样式，考虑下面这种情况：

```html
<html>
<head>
<title>rule 1</title>
<style>
body {color:black;}
p {color:blue;}
</style>
</head>
<body>
    <p>welcome to <strong>gaodayue的网络日志</strong></p>
</body>
</html>
```

strong分别从body和p中继承了color属性，但是由于p在继承树上离strong更近，因此strong中的文字最终继承p的蓝色。

### 规则二：继承的样式和直接指定的样式冲突时，直接指定的样式获胜。

在上面的例子中，假如还指定了strong元素的样式，如：

`strong {color:red;}`

那么根据规则二，strong中的文字最终显示为红色。

### 规则三：直接指定的样式发生冲突时，样式权值高者获胜。

样式的权值取决于样式的选择器，权值定义如下表:

| CSS选择器               | 权值 |
| :---------------------- | ---- |
| 标签选择器              | 1    |
| 类选择器                | 10   |
| ID选择器                | 100  |
| 内联样式                | 1000 |
| 伪元素（first-child等） | 1    |
| 伪类（link等）          | 10   |

可以看到，内联样式的权值>>ID选择器>>类选择器>>标签选择器，除此以外，**后代选择器的权值为每项权值之和**，比如”#nav .current a”的权值为100 + 10 + 1 = 111。

### 规则四：样式权值相同时，后者获胜。

考虑下面这种情况：

![image-20220712161900257](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220712161900257.png)

“.byline a”与”p .email”都直接指定了上面的a元素，且权值都为11，根据规则四，最终显示蓝色。

由于样式表可以是外部的，也可以是内部的，**规则四提醒我们要注意外部样式表引入的顺序**（及<link>元素的顺序），以及外部样式表与内部样式表的出现位置。**一般来说，内部样式表出现在所有外部样式表的引入之后，一般是在</head>之前**。

### 规则五：!important的样式属性不被覆盖

!important可以看做是万不得已的时候，打破上述四个规则的”金手指”。如果你一定要采用某个样式属性，而不让它被覆盖的，可以在属性值后 加上!important，以规则四的例子为例，`.byline a {color:red !important;}`可以强行使链接显示红色。大多数情况下都可以通过其他方式来控制样式的覆盖，不能滥用!important。

# JavaScript

## JavaScript介绍

- Javascript 语言诞生主要是完成页面的数据验证。因此它运行在客户端，需要运行浏览器来解析执行 JavaScript 代码。 

- JS 是 Netscape 网景公司的产品，最早取名为 LiveScript;为了吸引更多 java 程序员。更名为 JavaScript。 （蹭热度）

- JS 是弱类型，Java 是强类型。 

- 特点：
  1. 交互性（它可以做的就是信息的动态交互）
  2. 安全性（不允许直接访问本地硬盘）
  3. 跨平台性（只要是可以解释 JS 的浏览器都可以执行，和平台无关）

## JavaScript 和 html 代码的结合方式

### 第一种方式：内嵌

只需要在 head 标签中，或者在 body 标签中， 使用 script 标签 来书写 JavaScript 代码。

```html
<!DOCTYPE html> 
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title> 
        <script type="text/javascript">
            // alert 是 JavaScript 语言提供的一个警告框函数。
            // 它可以接收任意类型的参数，这个参数就是警告框的提示信息 alert("hello javaScript!"); 
        </script> 
    </head> 
    <body>
    </body> 
</html>
```

### 第二种方式：引入

使用 script 标签引入 单独的 JavaScript 代码文件。

```html
<!DOCTYPE html>
<html lang="en">
    <head> 
        <meta charset="UTF-8"> 
        <title>Title</title> 
        <!--现在需要使用 script 引入外部的 js 文件来执行 src 属性专门用来引入 js 文件路径（可以是相对路径，也可以是绝对路径） script 标签可以用来定义 js 代码，也可以用来引入 js 文件 但是，两个功能二选一使用。不能同时使用两个功能 --> 
        <script type="text/javascript" src="1.js"></script> 
        <script type="text/javascript">
            alert("国哥现在可以帅了"); 
        </script>
    </head> 
    <body>
    </body>
</html>
```

## 变量

### js中的变量类型

- 数值类型：number
- 字符串类型：string
- 对象类型：object
- 布尔类型：boolean
- 函数类型：function

### js中特殊的值

- undefined：未定义，所有js变量未赋予初始值的时候，默认值都是undefined。
- null：空值
- NaN：全称是：Not a Number。即非数值。

### js中的定义变量的格式

#### var关键字

- var 变量名;
- var 变量名 = 值;
- 用var声明的变量的作用域是函数作用域

#### let关键字

- let 变量名;
- let 变量名 = 值;
- 用let声明的变量的作用域是块作用域，通常在块内为了防止污染外面的区域从而使用let声明变量。

#### const关键字

- const 变量名 = 值;
- 用const声明的是常量，作用域是块作用域，必须在声明时赋值，之后不能改变值。

### 示例代码

```html
<!DOCTYPE html> 
<html lang="en"> 
    <head>
        <meta charset="UTF-8"> 
        <title>Title</title> 
        <script type="text/javascript"> 
            var i; 
            // alert(i); // undefined 
            i = 12; 
            // typeof()是 JavaScript 语言提供的一个函数。
            // alert( typeof(i) ); // number
            i = "abc"; 
            // 它可以取变量的数据类型返回 
            // alert( typeof(i) ); // String 
            var a = 12; 
            var b = "abc"; 
            alert( a * b );
            // NaN 是非数字，非数值。 
        </script> 
    </head> 
    <body> 
    </body>
</html>
```

## 关系（比较）运算

- 等于： ==  等于是简单的做字面值的比较，类型不同时会先进行类型转换为相同类型再进行比较。
- 全等于： ===  先比较两个变量的数据类型，如果类型不同直接false，类型相同再比较值。

```html
<!DOCTYPE html>
<html lang="en">
    <head> 
        <meta charset="UTF-8">
        <title>Title</title> 
        <script type="text/javascript"> 
            var a = "12"; 
            var b = 12; 
            alert( a == b ); // true 
            alert( a === b ); // false 
        </script> 
    </head>
    <body>
    </body>
</html>
```

## 逻辑运算

- 且运算：&&
- 或运算：||
- 取反运算：!
- 在JavaScript语言中，所有的变量，都可以作为一个boolean类型的变量去使用。**0、null、undefined、空串都认为是false**。

- 逻辑运算会**返回决定逻辑运算结果的表达式的值**。
- 逻辑运算是**短路**的，如果其中一个表达式决定了逻辑运算的值，那么剩下的表达式不再执行。

```html
<!DOCTYPE html> 
<html lang="en"> 
    <head>
        <meta charset="UTF-8">
        <title>Title</title> 
        <script type="text/javascript"> 
            /* 在 JavaScript 语言中，所有的变量，都可以做为一个 boolean 类型的变量去使用。 0 、null、 undefined、””(空串) 都认为是 false；*/ 
            // var a = 0; 
            // if (a) { 
            // alert("零为真"); 
            // } else {
            // alert("零为假"); 
            // } 
            // var b = null; 
            // if (b) { 
            // alert("null 为真"); 
            // } else { 
            // alert("null 为假"); 
            // } 
            // var c = undefined; 
            // if (c) { 
            // alert("undefined 为真"); 
            // } else { 
            // alert("undefined 为假");
            // } 
            // var d = ""; 
            // if (d) { 
            // alert("空串为真"); 
            // } else { 
            // alert("空串为假");
            // } 
            /* && 且运算。 有两种情况： 第一种：当表达式全为真的时候。返回最后一个表达式的值。 第二种：当表达式中，有一个为假的时候。返回第一个为假的表达式的值*/ 
            var a = "abc"; 
            var b = true; 
            var d = false; 
            var c = null; 
            // alert( a && b );
            //true 
            // alert( b && a );
            //true 
            // alert( a && d );
            // false 
            // alert( a && c );
            // null 
            /*  || 或运算 第一种情况：当表达式全为假时，返回最后一个表达式的值 第二种情况：只要有一个表达式为真。就会把回第一个为真的表达式的值*/ 
            // alert( d || c );
            // null 
            // alert( c|| d );
            //false 
            // alert( a || c );
            //abc
            // alert( b || c ); 
            //true
        </script>
    </head>
    <body> 
    </body> 
</html>
```

## 数组

### 数组的定义方式

- var/let 数组名 = []; 空数组
- var/let 数组名 = [1,'abc',true]; 定义数组同时赋值元素，可以同时存放不同数据类型的数据。

```html
<!DOCTYPE html> 
<html lang="en"> 
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
        <script type="text/javascript"> 
            var arr = [true,1]; 
            // 定义一个空数组 
            // alert( arr.length ); // 0 
            arr[0] = 12; 
            // alert( arr[0] );//12 
            // alert( arr.length ); // 0
            // javaScript 语言中的数组，只要我们通过数组下标赋值，那么最大的下标值，就会自动的给数组做扩容操作。 
            arr[2] = "abc"; 
            alert(arr.length); //3
            // alert(arr[1]);// undefined 
            // 数组的遍历 
            for (var i = 0; i < arr.length; i++){ alert(arr[i]); } 
        </script>
    </head>
    <body> 
    </body>
</html>
```

## 函数

### 函数的定义方式

#### 第一种：使用function关键字

- 使用的格式如下：

```javascript
function 函数名(形参列表){ 
    函数体 
}
```

- 在js中如何定义带有返回值的函数：只需要在函数体内直接使用return语句返回值即可。
- 示例代码：

```html
<!DOCTYPE html>
<html lang="en"> 
    <head> 
        <meta charset="UTF-8">
        <title>Title</title>
        <script type="text/javascript"> 
            // 定义一个无参函数 
            function fun(){ 
                alert("无参函数 fun()被调用了"); 
            }
            // 函数调用===才会执行 
            // fun(); 
            function fun2(a ,b) { 
                alert("有参函数 fun2()被调用了 a=>" + a + ",b=>"+b); 
            }
            // fun2(12,"abc"); 
            // 定义带有返回值的函数
            function sum(num1,num2) { 
                var result = num1 + num2;
                return result; 
            }
            alert( sum(100,50) ); 
        </script>
    </head>
    <body>
    </body> 
</html>
```

#### 第二种：定义函数变量

- 使用格式如下：

  `var 函数名 = function(形参列表) { 函数体 }`

- 示例代码：

  ```html
  <!DOCTYPE html> 
  <html lang="en"> 
      <head> 
          <meta charset="UTF-8"> 
          <title>Title</title> 
          <script type="text/javascript"> 
              var fun = function () { 
                  alert("无参函数"); 
              }
              // fun(); 
              var fun2 = function (a,b) { 
                  alert("有参函数 a=" + a + ",b=" + b);
              }
              // fun2(1,2); 
              var fun3 = function (num1,num2) { 
                  return num1 + num2; 
              }
              alert( fun3(100,200) );
          </script>
      </head>
      <body>
      </body> 
  </html>
  ```

- 在Java中函数允许重载，但是在js中函数的重载会直接覆盖掉上一次的定义：

  ```html
  <!DOCTYPE html> 
  <html lang="en"> 
      <head> 
          <meta charset="UTF-8">
          <title>Title</title> 
          <script type="text/javascript"> 
              function fun() { 
                  alert("无参函数 fun()"); 
              }
              function fun(a,b) { 
                  alert("有参函数 fun(a,b)"); 
              }
              fun(); 
          </script> 
      </head>
      <body>
      </body> 
  </html>
  ```

#### 第三种：匿名函数

- js中可以使用类似java中lambda表达式的语法来定义一个匿名函数，通常用在给方法传递函数类型的参数的时候。
- 语法：`(参数) => {函数体}`

### 函数的 arguments 隐形参数（只在function函数内）

- 就是在 function 函数中不需要定义，但却可以直接用来获取所有参数的变量arguments。我们管它叫隐形参数。隐形参数特别像 java 基础的可变长参数一样（`public void fun( Object ... args );`），可变长参数其实就是一个数组。那么js中的隐形参数也跟java的可变长参数一样，操作类似数组，但arguments本身并不是一个数组，实际上arguments是一个对象，可以利用该对象的属性和方法来实现一些功能。

- 示例代码：

  ```html
  <!DOCTYPE html>
  <html lang="en">
      <head> 
          <meta charset="UTF-8"> 
          <title>Title</title>
          <script type="text/javascript">
              function fun(a) { 
                  alert( arguments.length );//可看参数个数 
                  alert( arguments[0] ); 
                  alert( arguments[1] ); 
                  alert( arguments[2] ); 
                  alert("a = " + a); 
                  for (var i = 0; i < arguments.length; i++){ 
                      alert( arguments[i] ); 
                  }
                  alert("无参函数 fun()"); 
              }
              // fun(1,"ad",true); 
              // 需求：要求 编写 一个函数。用于计算所有参数相加的和并返回 
              function sum(num1,num2) { 
                  var result = 0; 
                  for (var i = 0; i < arguments.length; i++) { 
                      if (typeof(arguments[i]) == "number") { 
                          result += arguments[i]; 
                      } 
                  }
                  return result; 
              }
              alert( sum(1,2,3,4,"abc",5,6,7,8,9) ); 
          </script> 
      </head> 
      <body>
      </body> 
  </html>
  ```

## js中的自定义对象

### Object形式的自定义对象

- 对象的定义：
  - var 变量名 = new Object();  // 对象实例（空对象）
  - 变量名.属性名 = 值;  // 定义一个属性
  - 变量名.函数名 = function(参数){函数体};  //定义一个函数

- 对象的访问：变量名.属性 / 函数名(参数);

- 示例代码：

  ```html
  <!DOCTYPE html> 
  <html lang="en"> 
      <head> 
          <meta charset="UTF-8">
          <title>Title</title> 
          <script type="text/javascript"> 
              // 对象的定义： 
              // var 变量名 = new Object(); // 对象实例（空对象） 
              // 变量名.属性名 = 值; // 定义一个属性 
              // 变量名.函数名 = function(){} // 定义一个函数 
              var obj = new Object(); 
              obj.name = "华仔"; 
              obj.age = 18; 
              obj.fun = function () { 
                  alert("姓名：" + this.name + " , 年龄：" + this.age); 
              }
              // 对象的访问： 
              // 变量名.属性 / 函数名(); 
              // alert( obj.age ); 
              obj.fun(); 
          </script>
      </head> 
      <body>
      </body> 
  </html>
  ```

### {}花括号形式的自定义对象

- 对象的定义：

  ```javascript
  var 变量名 = { // 空对象 
      属性名：值, // 定义一个属性 
      属性名：值, // 定义一个属性 
      函数名：function(){} // 定义一个函数 
  };
  ```

- 对象的访问：变量名.属性 / 函数名(参数);

- 示例代码：

  ```html
  <!DOCTYPE html> 
  <html lang="en"> 
      <head> 
          <meta charset="UTF-8"> 
          <title>Title</title> 
          <script type="text/javascript"> 
              // 对象的定义： 
              // var 变量名 = { // 空对象 
              // 属性名：值, // 定义一个属性 
              // 属性名：值, // 定义一个属性 
              // 函数名：function(){} // 定义一个函数 
              // }; 
              var obj = { 
                  name:"国哥", 
                  age:18, 
                  fun : function () {
                      alert("姓名：" + this.name + " , 年龄：" + this.age); 
                  } 
              };
              // 对象的访问： 
              // 变量名.属性 / 函数名(); 
              alert(obj.name);
              obj.fun();
          </script>
      </head>
      <body>
      </body>
  </html>
  ```

## js中的事件

- 什么是事件？事件是电脑输入设备与页面进行交互的响应。我们称之为事件。
- 常用的事件：
  - onload 加载完成事件：页面加载完成之后，常用于做页面 js 代码初始化操作
  - onclick 单击事件：常用于按钮的点击响应操作。
  - onblur 失去焦点事件：常用用于输入框失去焦点后验证其输入内容是否合法。
  - onchange 内容发生改变事件：常用于下拉列表和输入框内容发生改变后操作。
  - onsubmit 表单提交事件：常用于表单提交前，验证所有表单项是否合法。

### 事件注册（绑定）

- 什么是事件的注册（绑定）？其实就是告诉浏览器，当事件响应后要执行哪些操作代码，叫事件注册或事件绑定。

- 静态注册事件：通过**html标签的事件属性**直接赋予事件响应后的代码（给事件属性设置回调函数），这种方式我们叫静态注册。
- 动态注册事件：是指先通过 js 代码得到标签的 dom 对象，然后再通过**dom 对象.事件名 = function(){}**这种形式赋于事件响应后的代码，叫动态注册。动态注册的基本步骤如下：
  1. 获取标签对象
  2. 标签对象.事件名 = function(){}

- onload加载完成事件：

  ```html
  <!DOCTYPE html> 
  <html lang="en"> 
      <head> 
          <meta charset="UTF-8">
          <title>Title</title> 
          <script type="text/javascript"> 
              // onload 事件的方法 
              function onloadFun() { 
                  alert('静态注册 onload 事件，所有代码'); 
              }
              // onload 事件动态注册。是固定写法
              window.onload = function () { 
                  alert("动态注册的 onload 事件"); 
              } 
          </script> 
      </head> 
      <!--静态注册 onload 事件 
  		onload 事件是浏览器解析完页面之后就会自动触发的事件 
  		<body onload="onloadFun();"> 
  --> 
      <body> 
      </body> 
  </html>
  ```

- onclick单击事件：

  ```html
  <!DOCTYPE html>
  <html lang="en">
      <head>
          <meta charset="UTF-8"> 
          <title>Title</title> 
          <script type="text/javascript"> 
              function onclickFun() {
                  alert("静态注册 onclick 事件");
              }
              // 动态注册 onclick 事件 
              window.onload = function () { 
                  // 1 获取标签对象 
                  /** document 是 JavaScript 语言提供的一个对象（文档）<br/> 
                  * get 获取 
                  * Element 元素（就是标签） 
                  * By 通过。。 由。。经。。。 
                  * Id id 属性 
                  *
                  * getElementById 通过 id 属性获取标签对象 
                  **/ 
                  var btnObj = document.getElementById("btn01"); 
                  // alert( btnObj ); 
                  // 2 通过标签对象.事件名 = function(){} 
                  btnObj.onclick = function () { 
                      alert("动态注册的 onclick 事件"); 
                  } 
              }
          </script>
      </head> 
      <body> 
          <!--静态注册 onClick 事件--> 
          <button onclick="onclickFun();">按钮 1</button> 
          <button id="btn01">按钮 2</button> 
      </body> 
  </html>
  ```

- onblur 失去焦点事件：

  ```html
  <!DOCTYPE html>
  <html lang="en">
      <head> 
          <meta charset="UTF-8"> 
          <title>Title</title> 
          <script type="text/javascript"> 
              // 静态注册失去焦点事件 
              function onblurFun() { 
                  // console 是控制台对象，是由 JavaScript 语言提供，专门用来向浏览器的控制器打印输出， 用于测试使用 
                  // log() 是打印的方法 
                  console.log("静态注册失去焦点事件"); 
              }
              // 动态注册 onblur 事件 
              window.onload = function () { 
                  //1 获取标签对象 
                  var passwordObj = document.getElementById("password"); 
                  // alert(passwordObj); 
                  //2 通过标签对象.事件名 = function(){}; 
                  passwordObj.onblur = function () { 
                      console.log("动态注册失去焦点事件"); 
                  } 
              } 
          </script> 
      </head> 
      <body> 
          用户名:<input type="text" onblur="onblurFun();"><br/> 
          密码:<input id="password" type="text" ><br/> 
      </body> 
  </html>
  ```

- onchange 内容发生改变事件：

  ```html
  <!DOCTYPE html> 
  <html lang="en"> 
      <head> 
          <meta charset="UTF-8">
          <title>Title</title>
          <script type="text/javascript"> 
              function onchangeFun() {
                  alert("女神已经改变了"); 
              }
              window.onload = function () {
                  //1 获取标签对象 
                  var selObj = document.getElementById("sel01"); 
                  // alert( selObj ); 
                  //2 通过标签对象.事件名 = function(){} 
                  selObj.onchange = function () { 
                      alert("男神已经改变了"); 
                  } 
              }
          </script> 
      </head> 
      <body> 
          请选择你心中的女神： 
          <!--静态注册 onchange 事件--> 
          <select onchange="onchangeFun();"> 
              <option>--女神--</option> 
              <option>芳芳</option> 
              <option>佳佳</option> 
              <option>娘娘</option>
          </select> 
          
          请选择你心中的男神： 
          <select id="sel01"> 
              <option>--男神--</option>
              <option>国哥</option>
              <option>华仔</option>
              <option>富城</option>
          </select> 
      </body> 
  </html>
  ```

- onsubmit表单提交事件：

  ```html
  <!DOCTYPE html> 
  <html lang="en"> 
      <head> 
          <meta charset="UTF-8">
          <title>Title</title> 
          <script type="text/javascript" > 
              // 静态注册表单提交事务 
              function onsubmitFun(){ 
                  // 要验证所有表单项是否合法，如果，有一个不合法就阻止表单提交 
                  alert("静态注册表单提交事件----发现不合法"); 
                  return flase; 
              }
              window.onload = function () { 
                  //1 获取标签对象 var formObj = document.getElementById("form01"); 
                  //2 通过标签对象.事件名 = function(){} 
                  formObj.onsubmit = function () {
                      // 要验证所有表单项是否合法，如果，有一个不合法就阻止表单提交 
                      alert("动态注册表单提交事件----发现不合法"); 
                      return false;
                  } 
              } 
          </script> 
      </head> 
      <body> 
          <!--return false 可以阻止 表单提交 --> 
          <form action="http://localhost:8080" method="get" onsubmit="return onsubmitFun();"> 
              <input type="submit" value="静态注册"/> 
          </form> 
          <form action="http://localhost:8080" id="form01"> 
              <input type="submit" value="动态注册"/>
          </form> 
      </body>
  </html>
  ```

## DOM模型

- DOM 全称是 Document Object Model 文档对象模型。
- 大白话，就是把文档中的标签，属性，文本，**转换成为对象**来管理。

### Document对象

![image-20220716225423308](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220716225423308.png)

- Document对象的理解：
  1. Document它管理了所有的HTML文档内容。
  2. document它是一种树结构的文档。有层级关系。
  3. 它让我们把所有的标签都对象化。
  4. 我们可以通过document访问所有的标签对象。

- 标签模拟对象化举例：

  ```html
  <body> 
      <div id="div01">div01</div>
  </body>
  ```

  模拟对象化，相当于：

  ```java
  class Dom{
      private String id; // id 属性 
      private String tagName; //表示标签名 
      private Dom parentNode; //父亲 
      private List<Dom> children; // 孩子结点 
      private String innerHTML; // 起始标签和结束标签中间的内容 
  }
  ```

### Document对象中的常用方法介绍

- **document.getElementById(elementId)** 通过标签的 id 属性查找标签 dom 对象，elementId 是标签的 id 属性值
- **document.getElementsByName(elementName)** 通过标签的 name 属性查找标签 dom 对象，elementName 标签的 name 属性值
- **document.getElementsByTagName(tagname)** 通过标签名查找标签 dom 对象。tagname 是标签名
- **document.createElement( tagName)** 通过给定的标签名，创建一个标签对象。tagName 是要创建的标签名

- document 对象的三个查询方法，如果有 id 属性，优先使用 **getElementById** 方法来进行查询 

  如果没有 id 属性，则优先使用 **getElementsByName** 方法来进行查询 

  如果 id 属性和 name 属性都没有最后再按标签名查 **getElementsByTagName** 

  以上三个方法，一定要在页面加载完成之后执行，才能查询到标签对象。

- **getElementById**方法示例代码：

  ```html
  <!DOCTYPE html> 
  <html lang="en"> 
      <head> <meta charset="UTF-8"> 
          <title>Title</title> 
          <script type="text/javascript" > 
              /** 
              需求：当用户点击了较验按钮，要获取输出框中的内容。然后验证其是否合法。<br/> 
              * 验证的规则是：必须由字母，数字。下划线组成。并且长度是 5 到 12 位。 
              * */ 
              function onclickFun() { 
                  // 1 当我们要操作一个标签的时候，一定要先获取这个标签对象。 
                  var usernameObj = document.getElementById("username"); // [object HTMLInputElement] 它就是 dom 对象 
                  var usernameText = usernameObj.value; 
                  // 如何 验证 字符串，符合某个规则 ，需要使用正则表达式技术 
                  var patt = /^\w{5,12}$/; 
                  /*js中正则表达式用一对斜线（/）包裹
                  * test()方法用于测试某个字符串，是不是匹配我的规则 ， 
                  * 匹配就返回 true。不匹配就返回 false. 
                  * */ 
                  var usernameSpanObj = document.getElementById("usernameSpan"); 
                  // innerHTML 表示起始标签和结束标签中的内容
                  // innerHTML 这个属性可读，可写 
                  usernameSpanObj.innerHTML = "国哥真可爱！"; 
                  if (patt.test(usernameText)) { 
                      // alert("用户名合法！"); 
                      // usernameSpanObj.innerHTML = "用户名合法！"; 
                      usernameSpanObj.innerHTML = "<img src=\"right.png\" width=\"18\" height=\"18\">"; 
                  } else { 
                      // alert("用户名不合法！");
                      // usernameSpanObj.innerHTML = "用户名不合法！";
                      usernameSpanObj.innerHTML = "<img src=\"wrong.png\" width=\"18\" height=\"18\">"; 
                  } 
              } 
          </script> 
      </head> 
      <body> 
          用户名：<input type="text" id="username" value="wzg"/> 
          <span id="usernameSpan" style="color:red;"> 
          
          </span> 
          <button onclick="onclickFun()">较验</button>
      </body>
  </html>
  ```

- **getElementsByName**方法示例代码：

  ```html
  <!DOCTYPE html> 
  <html lang="en"> 
      <head>
          <meta charset="UTF-8"> 
          <title>Title</title>
          <script type="text/javascript"> 
              // 全选 
              function checkAll() {
                  // 让所有复选框都选中 
                  // document.getElementsByName();是根据 指定的 name 属性查询返回多个标签对象集合
                  // 这个集合的操作跟数组 一样 
                  // 集合中每个元素都是 dom 对象 
                  // 这个集合中的元素顺序是他们在 html 页面中从上到下的顺序 
                  var hobbies = document.getElementsByName("hobby"); 
                  // checked 表示复选框的选中状态。如果选中是 true，不选中是 false 
                  // checked 这个属性可读，可写 
                  for (var i = 0; i < hobbies.length; i++){ 
                      hobbies[i].checked = true;
                  } 
              }
              //全不选 
              function checkNo() {
                  var hobbies = document.getElementsByName("hobby"); 
                  // checked 表示复选框的选中状态。如果选中是 true，不选中是 false 
                  // checked 这个属性可读，可写 
                  for (var i = 0; i < hobbies.length; i++){ 
                      hobbies[i].checked = false; 
                  } 
              }
              // 反选 
              function checkReverse() { 
                  var hobbies = document.getElementsByName("hobby"); 
                  for (var i = 0; i < hobbies.length; i++) { 
                      hobbies[i].checked = !hobbies[i].checked; 
                      // if (hobbies[i].checked) { 
                      // hobbies[i].checked = false; 
                      // }else { 
                      // hobbies[i].checked = true; 
                      // }
                  }
              } 
          </script>
      </head> 
      <body>
          兴趣爱好：
          <input type="checkbox" name="hobby" value="cpp" checked="checked">C++ 
          <input type="checkbox" name="hobby" value="java">Java 
          <input type="checkbox" name="hobby" value="js">JavaScript
          <br/> 
          <button onclick="checkAll()">全选</button>
          <button onclick="checkNo()">全不选</button> 
          <button onclick="checkReverse()">反选</button> 
      </body>
  </html>
  ```

- **getElementsByTagName**方法示例代码：

  ```html
  <!DOCTYPE html> 
  <html lang="en">
      <head>
          <meta charset="UTF-8"> 
          <title>Title</title>
          <script type="text/javascript"> 
              // 全选 
              function checkAll() { 
                  // document.getElementsByTagName("input"); 
                  // 是按照指定标签名来进行查询并返回集合 
                  // 这个集合的操作跟数组 一样 
                  // 集合中都是 dom 对象 
                  // 集合中元素顺序 是他们在 html 页面中从上到下的顺序。 
                  var inputs = document.getElementsByTagName("input"); 
                  for (var i = 0; i < inputs.length; i++){ 
                      inputs[i].checked = true; 
                  } 
              } 
          </script>
      </head> 
      <body> 
          兴趣爱好： 
          <input type="checkbox" value="cpp" checked="checked">C++ 
          <input type="checkbox" value="java">Java
          <input type="checkbox" value="js">JavaScript
          <br/> 
          <button onclick="checkAll()">全选</button>
      </body>
  </html>
  ```

- **createElement**方法示例代码：

  ```html
  <!DOCTYPE html>
  <html lang="en">
      <head>
          <meta charset="UTF-8"> 
          <title>Title</title>
          <script type="text/javascript"> 
              window.onload = function () { 
                  // 现在需要我们使用 js 代码来创建 html 标签，并显示在页面上 
                  // 标签的内容就是：<div>国哥，我爱你</div> 
                  var divObj = document.createElement("div"); // 在内存中 <div></div> 
                  var textNodeObj = document.createTextNode("国哥，我爱你"); // 有一个文本节点对象 #国哥，我 爱你 
                  divObj.appendChild(textNodeObj); // <div>国哥，我爱你</div> 
                  // divObj.innerHTML = "国哥，我爱你"; // <div>国哥，我爱你</div>,但，还只是在内存中 
                  // 添加子元素 
                  document.body.appendChild(divObj); 
              } 
          </script>
      </head> 
      <body>
      </body>
  </html>
  ```

### 节点的常用属性和方法

- 节点就是标签对象
- 常用方法：
  1. **getElementsByTagName()** 方法，获取当前节点的指定标签名孩子节点
  2. **appendChild( oChildNode ) **方法，可以添加一个子节点，oChildNode 是要添加的孩子节点

- 常用属性：
  1. **childNodes** 属性，获取当前节点的所有子节点
  2. **firstChild** 属性，获取当前节点的第一个子节点
  3. **lastChild** 属性，获取当前节点的最后一个子节点
  4. **parentNode** 属性，获取当前节点的父节点
  5. **nextSibling** 属性，获取当前节点的下一个节点
  6. **previousSibling** 属性，获取当前节点的上一个节点
  7. **className** 用于获取或设置标签的 class 属性值
  8. **innerHTML** 属性，表示获取/设置起始标签和结束标签中的内容 
  9. **innerText** 属性，表示获取/设置起始标签和结束标签中的文本

- DOM查询示例代码

  ```html
  <!DOCTYPE html>
  <html> 
      <head> 
          <meta charset="UTF-8"> 
          <title>dom 查询</title>
          <link rel="stylesheet" type="text/css" href="style/css.css" /> 
          <script type="text/javascript"> 
              window.onload = function(){ 
                  //1.查找#bj 节点 
                  document.getElementById("btn01").onclick = function () { 
                      var bjObj = document.getElementById("bj"); 
                      alert(bjObj.innerHTML);
                  }
                  //2.查找所有 li 节点 
                  var btn02Ele = document.getElementById("btn02"); 
                  btn02Ele.onclick = function(){
                      var lis = document.getElementsByTagName("li"); 
                      alert(lis.length);
                  };
                  //3.查找 name=gender 的所有节点 
                  var btn03Ele = document.getElementById("btn03"); 
                  btn03Ele.onclick = function(){ 
                      var genders = document.getElementsByName("gender");
                      alert(genders.length) 
                  };
                  //4.查找#city 下所有 li 节点 
                  var btn04Ele = document.getElementById("btn04"); 
                  btn04Ele.onclick = function(){ 
                      //1 获取 id 为 city 的节点 
                      //2 通过 city 节点.getElementsByTagName 按标签名查子节点 
                      var lis = document.getElementById("city").getElementsByTagName("li"); 
                      alert(lis.length) 
                  };
                  //5.返回#city 的所有子节点 
                  var btn05Ele = document.getElementById("btn05");
                  btn05Ele.onclick = function(){ 
                      //1 获取 id 为 city 的节点 
                      //2 通过 city 获取所有子节点
                      alert(document.getElementById("city").childNodes.length); 
                  };
                  //6.返回#phone 的第一个子节点 
                  var btn06Ele = document.getElementById("btn06"); 
                  btn06Ele.onclick = function(){ 
                      // 查询 id 为 phone 的节点 
                      alert( document.getElementById("phone").firstChild.innerHTML ); 
                  };
                  //7.返回#bj 的父节点
                  var btn07Ele = document.getElementById("btn07");
                  btn07Ele.onclick = function(){ 
                      //1 查询 id 为 bj 的节点 
                      var bjObj = document.getElementById("bj"); 
                      //2 bj 节点获取父节点 
                      alert( bjObj.parentNode.innerHTML ); 
                  };
                  //8.返回#android 的前一个兄弟节点 
                  var btn08Ele = document.getElementById("btn08");
                  btn08Ele.onclick = function(){ 
                      // 获取 id 为 android 的节点
                      // 通过 android 节点获取前面兄弟节点 
                      alert( document.getElementById("android").previousSibling.innerHTML ); 
                  };
                  //9.读取#username 的 value 属性值 
                  var btn09Ele = document.getElementById("btn09"); 
                  btn09Ele.onclick = function(){ 
                      alert(document.getElementById("username").value);
                  };
                  //10.设置#username 的 value 属性值 
                  var btn10Ele = document.getElementById("btn10"); 
                  btn10Ele.onclick = function(){ 
                      document.getElementById("username").value = "国哥你真牛逼"; 
                  };
                  //11.返回#bj 的文本值 
                  var btn11Ele = document.getElementById("btn11"); 
                  btn11Ele.onclick = function(){ 
                      alert(document.getElementById("city").innerHTML); 
                      // alert(document.getElementById("city").innerText); 
                  }; 
              }; 
          </script> 
      </head>
      <body>
          <div id="total">
              <div class="inner"> 
                  <p>
                      你喜欢哪个城市?
                  </p> 
                  <ul id="city"> 
                      <li id="bj">北京</li>
                      <li>上海</li> 
                      <li>东京</li> 
                      <li>首尔</li> 
                  </ul> 
                  
                  <br> 
                  <br>
                  
                  <p>
                      你喜欢哪款单机游戏?
                  </p> 
                  <ul id="game"> 
                      <li id="rl">红警</li>
                      <li>实况</li> 
                      <li>极品飞车</li> 
                      <li>魔兽</li> 
                  </ul>
                  
                  <br />
                  <br />
                  
                  <p>
                      你手机的操作系统是?
                  </p> 
                  <ul id="phone"><li>IOS</li><li id="android">Android</li><li>Windows Phone</li></ul> 
              </div> 
              
              <div class="inner"> 
                  gender: 
                  <input type="radio" name="gender" value="male"/> 
                  Male 
                  <input type="radio" name="gender" value="female"/> 
                  Female 
                  <br> 
                  <br>
                  name: 
                  <input type="text" name="name" id="username" value="abcde"/> 
              </div> 
          </div> 
          <div id="btnList"> 
              <div><button id="btn01">查找#bj 节点</button></div> 
              <div><button id="btn02">查找所有 li 节点</button></div> 
              <div><button id="btn03">查找 name=gender 的所有节点</button></div>
              <div><button id="btn04">查找#city 下所有 li 节点</button></div>
              <div><button id="btn05">返回#city 的所有子节点</button></div> 
              <div><button id="btn06">返回#phone 的第一个子节点</button></div> 
              <div><button id="btn07">返回#bj 的父节点</button></div>
              <div><button id="btn08">返回#android 的前一个兄弟节点</button></div> 
              <div><button id="btn09">返回#username 的 value 属性值</button></div> 
              <div><button id="btn10">设置#username 的 value 属性值</button></div> 
              <div><button id="btn11">返回#bj 的文本值</button></div> 
          </div>
      </body>
  </html>
  ```

# jQuery

## jQuery介绍

- jQuery，顾名思义，也就是 **JavaScript 和查询（Query）**，它就是辅助 JavaScript 开发的 js 类库。
- 它的核心思想是 write less,do more(写得更少,做得更多)，所以它实现了很多浏览器的兼容问题。
- jQuery 现在已经成为最流行的 JavaScript 库，在世界前 10000 个访问最多的网站中，有超过 55%在使用 jQuery。
- jQuery 是免费、开源的，jQuery 的语法设计可以使开发更加便捷，例如操作文档对象、选择 DOM 元素、 制作动画效果、事件处理、使用 Ajax 以及其他功能

## jQuery初体验

- 使用jQuery给一个按钮绑定单击事件的示例代码：

  ```html
  <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd"> 
  <html> 
      <head> 
          <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
          <title>Insert title here</title> 
          <script type="text/javascript" src="../script/jquery-1.7.2.js"></script><!--引入jQuery库-->
          <script type="text/javascript"> 
              // window.onload = function () { 
              // var btnObj = document.getElementById("btnId"); 
              // // alert(btnObj);//[object HTMLButtonElement] ====>>> dom 对象 
              // btnObj.onclick = function () { 
              // alert("js 原生的单击事件"); 
              // } 
              // }
              $(function () { // 表示页面加载完成 之后，相当 window.onload = function () {} 
                  var $btnObj = $("#btnId"); // 表示按 id 查询标签对象 
                  $btnObj.click(function () { // 绑定单击事件 
                      alert("jQuery 的单击事件"); 
                  }); 
              });
          </script> 
      </head> 
      <body> 
          <button id="btnId">SayHello</button> 
      </body> 
  </html>
  <!--
  如何为按钮添加点击响应函数？
  1、使用jQuery查询到标签对象
  2、使用标签对象.click(function(){});
  -->
  ```

## jQuery核心函数

- `$` 是 jQuery 的核心函数，能完成 jQuery 的很多功能。`$()`就是调用`$`这个函数。
  1. 传入参数为 [ 函数 ] 时：表示页面加载完成之后。相当于 window.onload = function(){}
  2. 传入参数为 [ HTML 字符串 ] 时：会对我们创建这个 html 标签对象
  3. 传入参数为 [ 选择器字符串 ] 时：
     - $(“#id 属性值”);     id 选择器，根据 id 查询标签对象
     - $(“标签名”);      标签名选择器，根据指定的标签名查询标签对象 
     - $(“.class 属性值”);     类型选择器，可以根据 class 属性查询标签对象

  4. 传入参数为 [ DOM 对象 ] 时：会把这个 dom 对象转换为 jQuery 对象

## jQuery对象和dom对象的区分

### Dom对象

1. 通过 **getElementById()**查询出来的标签对象是 Dom 对象
2. 通过 **getElementsByName()**查询出来的标签对象是 Dom 对象
3. 通过 **getElementsByTagName()**查询出来的标签对象是 Dom 对象
4. 通过 **createElement()** 方法创建的对象，是 Dom 对象
5. DOM 对象 Alert 出来的效果是：**[object HTML 标签名 Element]**

### jQuery对象

1. 通过 jQuery 提供的 API 创建的对象，是 jQuery 对象
2. 通过 jQuery 包装的 Dom 对象，也是 jQuery 对象
3. 通过 jQuery 提供的 API 查询到的对象，是 jQuery 对象
4. jQuery 对象 Alert 出来的效果是：[object Object]

### jQuery对象的本质是什么？

jQuery 对象是 dom 对象的数组 + jQuery 提供的一系列功能函数。

### jQuery对象和Dom对象使用区别

- jQuery 对象不能使用 DOM 对象的属性和方法
- DOM 对象也不能使用 jQuery 对象的属性和方法

### Dom对象和jQuery对象互转

![image-20220717224438530](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220717224438530.png)

#### Dom对象转化为jQuery对象

1. 先有 DOM 对象
2. $( DOM 对象 ) 就可以转换成为 jQuery 对象

#### jQuery对象转为Dom对象

1. 先有 jQuery 对象
2. jQuery 对象[下标]取出相应的 DOM 对象

## jQuery选择器

### 基本选择器

- \#ID 选择器：根据 id 查找标签对象 
- .class 选择器：根据 class 查找标签对象
- element 选择器：根据标签名查找标签对象
- \* 选择器：表示任意的，所有的元素
- selector1，selector2 组合选择器：合并选择器 1，选择器 2 的结果并返回
- selector1selector2 交集选择器：选择器 1，选择器 2 的结果取交集返回

### 层级选择器

- ancestor descendant 后代选择器 ：在给定的祖先元素下匹配所有的后代元素
- parent > child 子元素选择器：在给定的父元素下匹配所有的子元素
- prev + next 相邻元素选择器：匹配所有紧接在 prev 元素后的 next 元素
- prev ~ sibings 之后的兄弟元素选择器：匹配 prev 元素之后的所有 siblings 元素

### 过滤选择器

#### 基本过滤器

- **:first** 获取第一个元素
- **:last** 获取最后个元素
- **:not(selector)** 去除所有与给定选择器匹配的元素
- **:even** 匹配所有索引值为偶数的元素，从 0 开始计数
- **:odd** 匹配所有索引值为奇数的元素，从 0 开始计数
- **:eq(index)** 匹配一个给定索引值的元素
- **:gt(index)** 匹配所有大于给定索引值的元素
- **:lt(index)** 匹配所有小于给定索引值的元素
- **:header** 匹配如 h1, h2, h3 之类的标题元素
- **:animated** 匹配所有正在执行动画效果的元素

#### 内容过滤器

- **:contains(text)** 匹配包含给定文本的元素
- **:empty** 匹配所有不包含子元素或者文本的空元素
- **:parent** 匹配含有子元素或者文本的元素
- **:has(selector)** 匹配含有选择器所匹配的元素的元素

#### 属性过滤器

- **[attribute]** 匹配包含给定属性的元素。
- **[attribute=value]** 匹配给定的属性是某个特定值的元素。
- **[attribute!=value]** 匹配所有不含有指定的属性，或者属性不等于特定值的元素。
- **[attribute^=value]** 匹配给定的属性是以某些值开始的元素
- **[attribute$=value]** 匹配给定的属性是以某些值结尾的元素
- **[attribute*=value]** 匹配给定的属性是以包含某些值的元素
- [attrSel1]\[attrSel2][attrSelN] 复合属性选择器，需要同时满足多个条件时使用。

#### 表单过滤器

- **:input** 匹配所有 input, textarea, select 和 button 元素 
- **:text** 匹配所有 文本输入框 
- **:password** 匹配所有的密码输入框 
- **:radio** 匹配所有的单选框 
- **:checkbox** 匹配所有的复选框
- **:submit** 匹配所有提交按钮
- **:image** 匹配所有 img 标签 
- **:reset** 匹配所有重置按钮 
- **:button** 匹配所有 input type=button \<button>按钮 
- **:file** 匹配所有 input type=file 文件上传 
- **:hidden** 匹配所有不可见元素 display:none 或 input type=hidden

#### 表单对象属性过滤器

- **:enabled** 匹配所有可用元素
- **:disabled** 匹配所有不可用元素
- **:checked** 匹配所有选中的单选，复选，和下拉列表中选中的 option 标签对象
- **:selected** 匹配所有选中的 option

## jQuery元素筛选

- **eq()** 获取给定索引的元素 功能跟 :eq() 一样 
- **first()**获取第一个元素 功能跟 :first 一样 
- **last()** 获取最后一个元素 功能跟 :last 一样
- **filter(exp)** 留下匹配的元素 
- **is(exp)** 判断是否匹配给定的选择器，只要有一个匹配就返回，true 
- **has(exp)** 返回包含有匹配选择器的元素的元素 功能跟 :has 一样 
- **not(exp)** 删除匹配选择器的元素 功能跟 :not 一样 
- **children(exp)** 返回匹配给定选择器的子元素 功能跟 parent>child 一样 
- **find(exp)** 返回匹配给定选择器的后代元素 功能跟 ancestor descendant 一样
- **next()** 返回当前元素的下一个兄弟元素 功能跟 prev + next 功能一样 
- **nextAll()** 返回当前元素后面所有的兄弟元素 功能跟 prev ~ siblings 功能一样 
- **nextUntil()** 返回当前元素到指定匹配的元素为止的后面元素 
- **parent()** 返回父元素 
- **prev(exp)** 返回当前元素的上一个兄弟元素 
- **prevAll()** 返回当前元素前面所有的兄弟元素 
- **prevUnit(exp)** 返回当前元素到指定匹配的元素为止的前面元素 
- **siblings(exp)** 返回所有兄弟元素 
- **add()** 把 add 匹配的选择器的元素添加到当前 jquery 对象中



jQuery部分未完待续。。。。。。



# Tomcat

- tomcat是用java等语言编写成的一种web容器，是一种**轻量级的web服务器**，**可以通过处理发送过来的请求来进行相应的操作、返回响应的数据**。

- tomcat中**存放着各种web资源**，每当服务端发送请求想要请求某个web资源时，tomcat就会**解析这些请求，然后将应该响应的内容返回**。

![image-20220720100425675](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220720100425675.png)

## Tomcat的安装和配置

1. 解压：安装路径**不要出现中文和空格**
2. 目录结构说明：
   - bin：可执行文件目录，通过执行里面的**startup.dat**以启动Tomcat服务器，在执行之前需要在环境变量中配置好JAVA_HOME，不然窗口会一闪而过，服务器也不会启动。
   - conf：配置文件目录
   - lib：存放lib的目录
   - logs：日志文件目录
   - webapps：项目部署的目录
   - work：工作目录
   - temp：临时目录

3. 配置JAVA_HOME环境变量，让tomcat能够运行，因为tomcat也是用java和c来写的，因此需要JRE，所以**需要配置JAVA_HOME**
4. 通过bin目录下的**startup.dat**启动tomcat服务器，然后**可以通过本地的8080（默认端口，可以修改）端口来访问主页**。

## 在Tomcat中部署web项目

1. **在webapps下新建一个自定义名称的文件夹**，这个文件夹的名称就是tomcat用来寻找资源的**context root**。
2. **在自定义的文件夹中新建一个名为WEB-INF的文件夹**，至此，一个最基本的web项目已经被部署到Tomcat服务器中了，不过一般部署项目会通过各种IDE进行，基本不会手动进行配置，主要就是了解被部署到Tomcat服务器中的web项目的最基本的结构。
3. 通过**http://localhost:8080/context root/资源路径**来访问相应的资源。

## 设置编码

### Tomcat8之前

#### get请求方式

```java
//如果是get请求发送的中文数据，转码稍微有点麻烦（tomcat8之前）
String fname = request.getParameter("fname");
//1.将字符串打散成字节数组
byte[] bytes = fname.getBytes("ISO-8859-1");
//2.将字节数组按照设定的编码重新组装成字符串
fname = new String(bytes,"UTF-8");
```

#### post请求方式

```java
request.setCharacterEncoding("UTF-8");
```

### Tomcat8之后

- Tomcat8之后，只需要针对post方式设置编码了。
- 无论何时，设置编码这一操作必须在所有的获取参数的操作之前。

## Servlet

- Servlet是Tomcat服务器中用来处理请求的小组件，它决定了客户端发来请求后需要做的操作，需要通过**书写配置文件或者使用@WebServlet(映射路径)**的方式来将访问路径和指定的Servlet进行绑定，这样访问特定路径的时候就会激活对应的Servlet进行处理。

![image-20220720102159693](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220720102159693.png)

### Servlet的继承关系-重点是服务方法service()

#### 继承关系

- javax.servlet.Servlet接口
  - javax.servlet.GenericServlet抽象类
    -  javax.servlet.http.HttpServlet抽象子类

#### 相关方法

-  javax.servlet.Servlet接口:
  - void init(config) - 初始化方法
  - void service(request,response) - 服务方法
  - void destory() - 销毁方法

-  javax.servlet.GenericServlet抽象类：
  - void service(request,response) - 仍然是抽象的

-  javax.servlet.http.HttpServlet 抽象子类：
  - void service(request,response) - 不是抽象的
    1. String method = req.getMethod(); 获取请求的方式
    2. 各种if判断，根据请求方式不同，决定去调用不同的do方法
                   if (method.equals("GET")) {
                       this.doGet(req,resp);
                   } else if (method.equals("HEAD")) {
                       this.doHead(req, resp);
                   } else if (method.equals("POST")) {
                       this.doPost(req, resp);
                   } else if (method.equals("PUT")) {
    3. 在HttpServlet这个抽象类中，do方法都差不多:
               protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
                   String protocol = req.getProtocol();
                   String msg = lStrings.getString("http.method_get_not_supported");
                   if (protocol.endsWith("1.1")) {
                       resp.sendError(405, msg);
                   } else {
                       resp.sendError(400, msg);
                   }
               }

#### 小结

1. 继承关系：**HttpServlet -> GenericServlet -> Servlet**
2. Servlet中的**核心方法： init() , service() , destroy()**
3. 服务方法： 当有请求过来时，**service方法会自动响应（其实是tomcat容器调用的）**，在HttpServlet中我们会去分析请求的方式：到底是get、post、head还是delete等等，然后再决定调用的是哪个do开头的方法，在HttpServlet中这些do方法默认都是405的实现风格-要我们**子类去实现对应的方法**，否则默认会报405错误。
4. **自定义Servlet，需要继承HttpServlet，然后根据需求重写方法，然后在配置文件中书写相应的配置或者时候@WebServlet(映射路径)来进行路径和Servlet的绑定。**

### Servlet的生命周期

1. 生命周期：从出生到死亡的过程就是生命周期。对应Servlet中的三个方法：**init(),service(),destroy()**。
2. 默认情况下：**第一次接收请求时，这个Servlet会进行实例化(调用构造方法)、初始化(调用init())、然后服务(调用service())，从第二次请求开始，每一次都是服务，当容器关闭时，其中的所有的servlet实例会被销毁，调用销毁方法**。
3.  通过案例我们发现：
      - **Servlet实例tomcat只会创建一个，所有的请求都是这个实例去响应**。
      - 默认情况下，第一次请求时，tomcat才会去实例化，初始化，然后再服务.这样的好处是什么？ 提高系统的启动速度 。 这样的缺点是什么？ 第一次请求时，耗时较长。
      - 因此得出结论： 如果需要提高系统的启动速度，当前默认情况就是这样。**如果需要提高响应速度，我们应该设置Servlet的初始化时机**。
4.  Servlet的初始化时机：
      - 默认是第一次接收请求时，实例化，初始化
      - 我们可以在**WEB-INF中的web.xml配置文件**中通过\<load-on-startup>来设置servlet启动的先后顺序,数字越小，启动越靠前，最小值0，设置为1后就会在系统启动的同时实例化Servlet（？）。
5.  Servlet在容器中是：**单例的、线程不安全的**
      - 单例：所有的请求都是同一个实例去响应
      - 线程不安全：一个线程需要根据这个实例中的某个成员变量值去做逻辑判断。但是在中间某个时机，另一个线程改变了这个成员变量的值，从而导致第一个线程的执行路径发生了变化
      - 我们已经知道了servlet是线程不安全的，给我们的启发是： **尽量的不要在servlet中定义成员变量**。如果不得不定义成员变量，那么不要去：①不要去修改成员变量的值 ②不要去根据成员变量的值做一些逻辑判断

![image-20220720114304123](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220720114304123.png)

# http协议

1. http 被称之为 **超文本传输协议**
2. **http 是无状态的，也就是说，http协议无法将多次请求的用户进行区分**，所以要引入**session会话跟踪技术**。
3. http 请求响应包含两个部分：请求和响应
   - 请求：
     - 请求包含三个部分：**请求行、请求消息头、请求主体**
       - **请求行**包含三个信息：**请求的方式、请求的URL、请求的协议（一般都是HTTP1.1）**
       - **请求消息头**中**包含了很多客户端需要告诉服务器的信息**，比如：我的浏览器型号、版本、我能接收的内容的类型、我给你发的内容的类型、内容的长度等等。
       - **请求体**，有三种情况：
         - **get方式**，没有请求体，但是有一个queryString
         - **post方式**，有请求体，form data
         - **json格式**，有请求体，request payload
   - 响应：
     - 响应也包含三个部分：**响应行、响应头、响应体**
       - **响应行**包含三个信息：**协议、响应状态码（例：200）、响应状态（例：ok）**
       - **响应头**：包含了**服务器的信息**，**服务器发送给浏览器的内容的信息**（内容的媒体类型、编码、内容长度等）
       - **响应体**：响应的实际内容（比如请求html页面时，响应的内容就是\<html>\<head>\<body><form....）
       - 常见**响应状态码**：**200正常响应、404找不到资源、405请求方式不支持、500服务器内部错误等**。

# 会话(session)

- **http是无状态的**
  - http无状态：服务器无法判断这两次请求是同一个客户端发过来的，还是不同的客户端发过来的。
  - 无状态带来的现实问题：第一次请求时添加商品到购物车，第二次请求是结账，如果这两次请求服务器无法区分是同一个用户的，那么就会导致混乱。
  - 可以通过**会话跟踪技术**来解决无状态的问题。

- **会话跟踪技术**
  - 客户端第一次发请求给服务器，服务器获取session，如果获取不到，则创建一个新的session，然后响应给客户端。
  - 下次客户端给服务器发请求时，会把sessionID带给服务器，那么服务器就能获取到了，服务器就能判断这一次请求和之前某次请求是同一个客户端，从而能够区分开客户端。
  - 常用API：
    - **request.getSession()** -> 获取当前的会话，没有则创建一个新的会话
    - **request.getSession(true)** -> 效果和不带参数相同
    - **request.getSession(false)** -> 获取当前会话，没有则返回null，不会创建新的
    - **session.getId()** -> 获取sessionID
    - **session.isNew()** -> 判断当前session是否是新的
    - **session.getMaxInactiveInterval()** -> session的非激活间隔时长，默认1800秒
    - **session.setMaxInactiveInterval()** -> 获取session的非激活间隔时长，默认1800秒
    - **session.invalidate()** -> 强制性让会话立即失效
    - ......

![image-20220720114341631](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220720114341631.png)

- **session保存作用域**
  - session保存作用域是和具体的某一个session对应的
  - 可以在session的保存作用域中保存数据，数据在session存在时有效，随着session的销毁而销毁
  - 常用API：
    - void session.setAttribute(k,v) 向对应session中以键值对的形式存放数据
    - Object session.getAttribute(k) 通过键来取出对应session中key对应的值
    - void removeAttribute(k) 删除对应session中的通过key指定的键值对

![image-20220720114919192](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220720114919192.png)

# 服务器内部转发以及客户端重定向

## 服务器内部转发

`request.getRequestDispatcher("...").forward(request,response);`

- 一次请求响应的过程，对于客户端而言，内部经过了多少次转发，客户端是不知道的。
- 浏览器地址栏没有变化

![image-20220720115242902](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220720115242902.png)

## 客户端重定向

`response.sendRedirect("....");`

- 两次请求响应的过程。客户端知道请求URL有变化
- 浏览器的地址栏有变化

![image-20220720115401086](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220720115401086.png)

# Thymeleaf视图模板技术

- thymeleaf是用来帮助我们做视图渲染的一个技术

1. 添加Thymeleaf的jar包

2. 新建一个Servlet类ViewBaseServlet

3. 在web.xml文件中添加配置，配置前缀view-prefix，配置后缀view-suffix

4. 使得我们的Servlet继承ViewBaseServlet

5. 根据逻辑视图名称得到物理视图名称

    //此处的视图名称是 index
    //那么thymeleaf会将这个 逻辑视图名称 对应到 物理视图 名称上去
    //逻辑视图名称 ：   index
    //物理视图名称 ：   view-prefix + 逻辑视图名称 + view-suffix
    //所以真实的视图名称是：      /       index       .html
    super.processTemplate("index",request,response);

6. 使用Thymeleaf的标签：th:if（if）、th:unless（else）、th:each（for）、th:text等

![image-20220720221917826](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220720221917826.png)

![image-20220720223838871](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220720223838871.png)

- 其中**th:href="@{相对路径}"**会自动将其中填写的相对路径补全为绝对路径，补全的内容由**\<base href="基路径" />**决定。

- index.html示例代码：

```html
<html xmlns:th="http://www.thymeleaf.org">
	<head>
		<meta charset="utf-8">
		<link rel="stylesheet" href="css/index.css">
        <script language="JavaScript" src="js/index.js"></script>
	</head>
	<body>
		<div id="div_container">
			<div id="div_fruit_list">
				<p class="center f30">欢迎使用水果库存后台管理系统</p>
				<div style="border:0px solid red;width:60%;margin-left:20%;text-align:right;">
					<a th:href="@{/add.html}" style="border:0px solid blue;margin-bottom:4px;">添加新库存记录</a>
				</div>
				<table id="tbl_fruit">
					<tr>
						<th class="w20">名称1</th>
						<th class="w20">单价</th>
						<th class="w20">库存</th>
						<th>操作</th>
					</tr>
					<tr th:if="${#lists.isEmpty(session.fruitList)}">
						<td colspan="4">对不起，库存为空！</td>
					</tr>
					<tr th:unless="${#lists.isEmpty(session.fruitList)}" th:each="fruit : ${session.fruitList}">
						<!-- <td><a th:text="${fruit.fname}" th:href="@{'/edit.do?fid='+${fruit.fid}}">苹果</a></td> -->
						<td><a th:text="${fruit.fname}" th:href="@{/edit.do(fid=${fruit.fid})}">苹果</a></td>
						<td th:text="${fruit.price}">5</td>
						<td th:text="${fruit.fcount}">20</td>
						<!-- <td><img src="imgs/del.jpg" class="delImg" th:onclick="'delFruit('+${fruit.fid}+')'"/></td> -->
                        <td><img src="imgs/del.jpg" class="delImg" th:onclick="|delFruit(${fruit.fid})|"/></td>
					</tr>
				</table>
			</div>
		</div>
	</body>
</html>
```

- indexServlet.java示例代码：

```java
//Servlet从3.0版本开始支持注解方式的注册
@WebServlet("/index")
public class IndexServlet extends ViewBaseServlet {
    @Override
    public void doGet(HttpServletRequest request , HttpServletResponse response)throws IOException, ServletException {
        FruitDAO fruitDAO = new FruitDAOImpl();
        List<Fruit> fruitList = fruitDAO.getFruitList();
        //保存到session作用域
        HttpSession session = request.getSession() ;
        session.setAttribute("fruitList",fruitList);
        //此处的视图名称是 index
        //那么thymeleaf会将这个 逻辑视图名称 对应到 物理视图 名称上去
        //逻辑视图名称 ：   index
        //物理视图名称 ：   view-prefix + 逻辑视图名称 + view-suffix
        //所以真实的视图名称是：      /       index       .html
        super.processTemplate("index",request,response);
    }
}
```

# 保存作用域

- 原始情况下，保存作用域我们可以认为有四个：**page（页面级别，现在几乎不用了，jsp时期用得多），request（一次请求响应范围），session（一次会话范围），application（整个应用程序范围）**

## request保存作用域

![image-20220720222422220](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220720222422220.png)

- request保存作用域是一次请求响应范围内有效，上面第一个例子是进行了客户端重定向，客户端发送了多个请求，所以第二次请求时取不到第一次请求时向request中存放的数据；第二个例子是进行了服务器内部的转发，客户端只进行了一次请求响应，所以在内部转发后仍能从request中取出对应数据。

```java
//演示request保存作用域（demo01和demo02）
@WebServlet("/demo01")
public class Demo01Servlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1.向request保存作用域保存数据
        request.setAttribute("uname","lili");
        //2.客户端重定向
        //response.sendRedirect("demo02");

        //3.服务器端转发
        request.getRequestDispatcher("demo02").forward(request,response);
    }
}

@WebServlet("/demo02")
public class Demo02Servlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1.获取request保存作用域保存的数据，key为uname
        Object unameObj = request.getAttribute("uname");
        System.out.println("unameObj = " + unameObj);
    }
}
```



## session保存作用域

![image-20220720222809230](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220720222809230.png)

- 在session中存放的数据，在session失效之前都可以被取出，尽管不是同一次请求，只要session相同，那就可以取出对应session中的数据。

```java
//演示session保存作用域（demo03和demo04）
@WebServlet("/demo03")
public class Demo03Servlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1.向session保存作用域保存数据
        request.getSession().setAttribute("uname","lili");
        //2.客户端重定向
        response.sendRedirect("demo04");

        //3.服务器端转发
        //request.getRequestDispatcher("demo04").forward(request,response);
    }
}

@WebServlet("/demo04")
public class Demo04Servlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1.获取session保存作用域保存的数据，key为uname
        Object unameObj = request.getSession().getAttribute("uname");
        System.out.println("unameObj = " + unameObj);
    }
}
```



## application保存作用域

![image-20220720222936314](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220720222936314.png)

- 其中application是ServletContext类的实例，通过request.getServletContext()获取，ServletContext是一个全局的储存信息的空间，服务器开始就存在，服务器关闭才释放。

```java
//演示application保存作用域（demo05和demo06）
@WebServlet("/demo05")
public class Demo05Servlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1.向application保存作用域保存数据
        //ServletContext : Servlet上下文
        ServletContext application = request.getServletContext();
        application.setAttribute("uname","lili");
        //2.客户端重定向
        response.sendRedirect("demo06");

        //3.服务器端转发
        //request.getRequestDispatcher("demo04").forward(request,response);
    }
}

@WebServlet("/demo06")
public class Demo06Servlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1.获取application保存作用域保存的数据，key为uname
        ServletContext application = request.getServletContext() ;
        Object unameObj = application.getAttribute("uname");
        System.out.println("unameObj = " + unameObj);
    }
}
```

# 优化Servlet

- 最初的做法是：一个请求对应一个Servlet，但是这样存在的问题就是，Servlet太多了，随着请求的逐渐增多，**太多的Servlet不利于管理**，并且**用静态代码编写的Servlet形式过于冗杂，耦合度较高，不好维护**，因此可以从这几个方面下手来对Servlet进行优化。

![image-20220722094927919](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220722094927919.png)

- 首先从优化访问流程结构入手，**把一些列的请求都对应一个Servlet**, IndexServlet/AddServlet/EditServlet/DelServlet/UpdateServlet -> 合并成FruitServlet**通过一个operate的值来决定调用FruitServlet中的哪一个方法**（使用的是switch-case）。

![image-20220722095904751](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220722095904751.png)

- 但是如果使用switch-case，那么用于处理所有请求的转发Servlet中就会充斥着大量的switch-case语句，随着项目业务规模的扩大，会产生更多的Servlet，这也就意味着switch-case语句会变得更冗杂，这是一种代码冗余，所以我们**考虑使用反射技术编写动态代码**，使得代码具有动态性，减少代码的冗余。在servlet中使用了反射技术，我们规定operate的值和方法名一致，那么接收到operate的值是什么就表明我们需要调用对应的方法进行响应，如果找不到对应的方法，则抛异常。不过要注意，java是一门静态语言，反射的实现只是赋予了java一定的动态性，但是java还是一门静态语言。

- 在上一个版本中我们使用了反射技术，但是其实还是存在一些问题：每个Servlet中都有类似的反射技术的代码，为了**提高可读性、降低耦合度、增加复用性和降低维护难度**，我们将其中的反射代码和参数进行抽取，设计出中央控制器类：**DispatcherServlet**

  - DispatcherServlet这个类的工作分为两大部分：

    - 根据url定位到能够处理这个请求的controller组件（从servlet改过来的）：
      1. 从url中提取servletPath：/fruit.do -> fruit
      2. 根据fruit找到对应的组件：FruitController，这个**对应的依据我们存储在applicationContext.xml中**，`<bean id="fruit" class="com.atguigu.fruit.controllers.FruitController/>`，**通过DOM技术去解析XML文件**，在中央控制器中形成一个**beanMap容器**，用来存放所有的Controller组件。在DispatcherServlet进行初始化的时候，应该**使用类加载器读取配置文件**，**生成文档对象**，再根据键值对的形式，**将所有的键值对存放到Map<String,Object>中方便之后取用**，实际上这也是一种非常常见的处理配置文件内容的方式。后面的代码部分有演示到。
      3. 根据获取到的operate的值定位到我们FruitController中需要调用的方法。

    - 调用Controller组件中的方法：

      1. **获取参数**：主要就是将Controller中的getAttribute获取参数给提取到方法参数列表中，让参数直接传到方法中，这样做可以降低耦合。首先获取即将要调用的方法的参数签名信息:**Parameter[] parameters = method.getParameters();**然后通过**parameter.getName()**获取参数的名称；准备了**Object[] parameterValues**这个数组用来存放对应参数的参数值；另外，我们需要考虑参数的类型问题，需要做类型转化的工作，通过**parameter.getType()**获取参数的类型。

      2. **执行方法**：**Object returnObj = method.invoke(controllerBean , parameterValues);**

      3. **视图处理**：将视图的处理放到DispatcherServlet中**统一进行处理**，**Controller只需要返回特定格式的字符串**，然后DispatcherServlet就会根据字符串的格式和内容做出相应的操作，这样做实际上也是降低了耦合。

         ​	 String returnStr = (String)returnObj;
         ​       if(returnStr.startWith("redirect:")){
         ​        ....
         ​       }else if.....

![image-20220722113927251](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220722113927251.png)

- ViewBaseServlet、DispatcherServlet、FruitController示例代码：

  总体也是遵循先将通用的内容写成ViewBaseServlet后再用DispatcherServlet去继承ViewBaseServlet，然后再写额外的内容。

  ```java
  //ViewBaseServlet
  public class ViewBaseServlet extends HttpServlet {
  
      private TemplateEngine templateEngine;
  
      @Override
      public void init() throws ServletException {
  
          // 1.获取ServletContext对象
          ServletContext servletContext = this.getServletContext();
  
          // 2.创建Thymeleaf解析器对象
          ServletContextTemplateResolver templateResolver = new ServletContextTemplateResolver(servletContext);
  
          // 3.给解析器对象设置参数
          // ①HTML是默认模式，明确设置是为了代码更容易理解
          templateResolver.setTemplateMode(TemplateMode.HTML);
  
          // ②设置前缀
          String viewPrefix = servletContext.getInitParameter("view-prefix");
  
          templateResolver.setPrefix(viewPrefix);
  
          // ③设置后缀
          String viewSuffix = servletContext.getInitParameter("view-suffix");
  
          templateResolver.setSuffix(viewSuffix);
  
          // ④设置缓存过期时间（毫秒）
          templateResolver.setCacheTTLMs(60000L);
  
          // ⑤设置是否缓存
          templateResolver.setCacheable(true);
  
          // ⑥设置服务器端编码方式
          templateResolver.setCharacterEncoding("utf-8");
  
          // 4.创建模板引擎对象
          templateEngine = new TemplateEngine();
  
          // 5.给模板引擎对象设置模板解析器
          templateEngine.setTemplateResolver(templateResolver);
  
      }
  
      protected void processTemplate(String templateName, HttpServletRequest req, HttpServletResponse resp) throws IOException {
          // 1.设置响应体内容类型和字符集
          resp.setContentType("text/html;charset=UTF-8");
  
          // 2.创建WebContext对象
          WebContext webContext = new WebContext(req, resp, getServletContext());
  
          // 3.处理模板数据
          templateEngine.process(templateName, webContext, resp.getWriter());
      }
  }
  
  
  
  
  //----------------------------------------------------------------------------------------------
  
  
  
  
  
  //DispatcherServlet
  @WebServlet("*.do")
  public class DispatcherServlet extends ViewBaseServlet{
  
      private Map<String,Object> beanMap = new HashMap<>();
  
      public DispatcherServlet(){
      }
  
      public void init() throws ServletException {//主要就是通过读取配置文件，创建文本对象，然后通过配置文件中的键值对，利用反射，创建Map<String,Object>类型的实体映射集保存起来，以后可以利用反射通过名称访问到实体。
          super.init();
          try {
              InputStream inputStream = getClass().getClassLoader().getResourceAsStream("applicationContext.xml");
              //1.创建DocumentBuilderFactory
              DocumentBuilderFactory documentBuilderFactory = DocumentBuilderFactory.newInstance();
              //2.创建DocumentBuilder对象
              DocumentBuilder documentBuilder = documentBuilderFactory.newDocumentBuilder() ;
              //3.创建Document对象
              Document document = documentBuilder.parse(inputStream);
  
              //4.获取所有的bean节点
              NodeList beanNodeList = document.getElementsByTagName("bean");
              for(int i = 0 ; i<beanNodeList.getLength() ; i++){
                  Node beanNode = beanNodeList.item(i);
                  if(beanNode.getNodeType() == Node.ELEMENT_NODE){
                      Element beanElement = (Element)beanNode ;
                      String beanId =  beanElement.getAttribute("id");
                      String className = beanElement.getAttribute("class");
                      Class controllerBeanClass = Class.forName(className);
                      Object beanObj = controllerBeanClass.newInstance() ;
                      beanMap.put(beanId , beanObj) ;
                  }
              }
          } catch (ParserConfigurationException e) {
              e.printStackTrace();
          } catch (SAXException e) {
              e.printStackTrace();
          } catch (IOException e) {
              e.printStackTrace();
          } catch (IllegalAccessException e) {
              e.printStackTrace();
          } catch (InstantiationException e) {
              e.printStackTrace();
          } catch (ClassNotFoundException e) {
              e.printStackTrace();
          }
      }
  
      @Override
      protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          //设置编码
          request.setCharacterEncoding("UTF-8");
          //假设url是：  http://localhost:8080/pro15/hello.do
          //那么servletPath是：    /hello.do
          // 我的思路是：
          // 第1步： /hello.do ->   hello   或者  /fruit.do  -> fruit
          // 第2步： hello -> HelloController 或者 fruit -> FruitController
          String servletPath = request.getServletPath();
          servletPath = servletPath.substring(1);
          int lastDotIndex = servletPath.lastIndexOf(".do") ;
          servletPath = servletPath.substring(0,lastDotIndex);
  
          Object controllerBeanObj = beanMap.get(servletPath);
  
          String operate = request.getParameter("operate");
          if(StringUtil.isEmpty(operate)){
              operate = "index" ;
          }
  
          try {
              Method[] methods = controllerBeanObj.getClass().getDeclaredMethods();
              for(Method method : methods){
                  if(operate.equals(method.getName())){
                      //1.统一获取请求参数
  
                      //1-1.获取当前方法的参数，返回参数数组
                      Parameter[] parameters = method.getParameters();
                      //1-2.parameterValues 用来承载参数的值
                      Object[] parameterValues = new Object[parameters.length];
                      for (int i = 0; i < parameters.length; i++) {
                          Parameter parameter = parameters[i];
                          String parameterName = parameter.getName() ;
                          //如果参数名是request,response,session 那么就不是通过请求中获取参数的方式了
                          if("request".equals(parameterName)){
                              parameterValues[i] = request ;
                          }else if("response".equals(parameterName)){
                              parameterValues[i] = response ;
                          }else if("session".equals(parameterName)){
                              parameterValues[i] = request.getSession() ;
                          }else{
                              //从请求中获取参数值
                              String parameterValue = request.getParameter(parameterName);
                              String typeName = parameter.getType().getName();
  
                              Object parameterObj = parameterValue ;
  
                              if(parameterObj!=null) {
                                  if ("java.lang.Integer".equals(typeName)) {
                                      parameterObj = Integer.parseInt(parameterValue);
                                  }
                              }
  
                              parameterValues[i] = parameterObj ;
                          }
                      }
                      //2.controller组件中的方法调用
                      method.setAccessible(true);
                      Object returnObj = method.invoke(controllerBeanObj,parameterValues);
  
                      //3.视图处理
                      String methodReturnStr = (String)returnObj ;
                      if(methodReturnStr.startsWith("redirect:")){        //比如：  redirect:fruit.do
                          String redirectStr = methodReturnStr.substring("redirect:".length());
                          response.sendRedirect(redirectStr);
                      }else{
                          super.processTemplate(methodReturnStr,request,response);    // 比如：  "edit"
                      }
                  }
              }
  
              /*
              }else{
                  throw new RuntimeException("operate值非法!");
              }
              */
          } catch (IllegalAccessException e) {
              e.printStackTrace();
          } catch (InvocationTargetException e) {
              e.printStackTrace();
          }
      }
  }// 常见错误： IllegalArgumentException: argument type mismatch
  
  
  
  
  //--------------------------------------------------------------------------------------------------------
  
  
  
  
  //经过优化后的FruitController
  //可以看出来，经过一堆优化后的FruitController耦合度已经比较低了，并且便于阅读和维护。
  public class FruitController {
      private FruitDAO fruitDAO = new FruitDAOImpl();
  
      private String update(Integer fid , String fname , Integer price , Integer fcount , String remark ){
          //3.执行更新
          fruitDAO.updateFruit(new Fruit(fid,fname, price ,fcount ,remark ));
          //4.资源跳转
          return "redirect:fruit.do";
      }
  
      private String edit(Integer fid , HttpServletRequest request){
          if(fid!=null){
              Fruit fruit = fruitDAO.getFruitByFid(fid);
              request.setAttribute("fruit",fruit);
              //super.processTemplate("edit",request,response);
              return "edit";
          }
          return "error" ;
      }
  
      private String del(Integer fid  ){
          if(fid!=null){
              fruitDAO.delFruit(fid);
              return "redirect:fruit.do";
          }
          return "error";
      }
  
      private String add(String fname , Integer price , Integer fcount , String remark ) {
          Fruit fruit = new Fruit(0,fname , price , fcount , remark ) ;
          fruitDAO.addFruit(fruit);
          return "redirect:fruit.do";
      }
  
      private String index(String oper , String keyword , Integer pageNo , HttpServletRequest request ) {
          HttpSession session = request.getSession() ;
  
          if(pageNo==null){
              pageNo = 1;
          }
          if(StringUtil.isNotEmpty(oper) && "search".equals(oper)){
              pageNo = 1 ;
              if(StringUtil.isEmpty(keyword)){
                  keyword = "" ;
              }
              session.setAttribute("keyword",keyword);
          }else{
              Object keywordObj = session.getAttribute("keyword");
              if(keywordObj!=null){
                  keyword = (String)keywordObj ;
              }else{
                  keyword = "" ;
              }
          }
  
          // 重新更新当前页的值
          session.setAttribute("pageNo",pageNo);
  
          FruitDAO fruitDAO = new FruitDAOImpl();
          List<Fruit> fruitList = fruitDAO.getFruitList(keyword , pageNo);
          session.setAttribute("fruitList",fruitList);
  
          //总记录条数
          int fruitCount = fruitDAO.getFruitCount(keyword);
          //总页数
          int pageCount = (fruitCount+5-1)/5 ;
          session.setAttribute("pageCount",pageCount);
  
          return "index" ;
      }
  }
  ```

# 利用Servlet的初始化方法获取初始化设置的数据

## Servlet的初始化方法（init()）

- Servlet生命周期：**实例化、初始化、服务、销毁**

- Servlet中的初始化方法有两个：**init()、init(config)**

  - 其中带参数的方法代码如下：

    ```java
    public void init(ServletConfig config) throws ServletException {
         this.config = config ;
         init();
    }
    ```

  - 另外一个无参的init方法如下：

    ```java
    public void init() throws ServletException{
    }
    ```

## 初始化参数的配置

- 配置方法共有两种。

### 在web.xml文件中配置Servlet

```xml
<servlet>
    <servlet-name>Demo01Servlet</servlet-name>
    <servlet-class>com.atguigu.servlet.Demo01Servlet</servlet-class>
    <init-param>
        <param-name>hello</param-name>
        <param-value>world</param-value>
    </init-param>
    <init-param>
        <param-name>uname</param-name>
        <param-value>jim</param-value>
    </init-param>
</servlet>
<servlet-mapping>
    <servlet-name>Demo01Servlet</servlet-name>
    <url-pattern>/demo01</url-pattern>
</servlet-mapping>
```

### 通过注解的方法进行配置

```java
@WebServlet(urlPatterns = {"/demo01"} ,
initParams = {
    @WebInitParam(name="hello",value="world"),
    @WebInitParam(name="uname",value="jim")
})
```



## 初始化参数的获取

- 如果我们想要在Servlet初始化时做一些准备工作，那么我们可以重写init方法，我们可以通过如下步骤去获取初始化设置的数据：
  1. 获取config对象：`ServletConfig config = getServletConfig();`
  2. 获取初始化参数值：`config.getInitParameter(key);`

# 通过ServletContext获取初始化值

## 获取ServletContext

- 这里列举两种获取ServletContext的方法

### 在初始化方法中

`ServletContxt servletContext = getServletContext();`

### 在服务方法中

`request.getServletContext();`

或

`session.getServletContext()`

## 获取初始化值

`servletContext.getInitParameter();`

# MVC模型

## MVC模型简介

- 分为Model1和Model2，Model1是很早之前的jsp技术用到的，主要是HTML做视图，java做控制和持久化，然后现在都是Model2了。

![MVC模型大体结构](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220723220512965.png)

- MVC：**Model（模型层）、View（视图层）、Controller（控制层）**
  - 视图层：用于做**数据展示以及和用户交互的界面**。
  - 控制层：能够**接受客户端的请求并作出相应操作**，具体的业务功能还是需要借助于模型组件来完成。
  - 模型层：模型分为很多种，有比较简单的**pojo/vo(value object)**，有**业务模型组件(service)**，有**数据访问层组件(DAO)**。
    - POJO：Plain Ordinary Java Object，简单java对象，实际上就是普通的JavaBeans，通常用来做某个实体的Java对象。
    - VO：Value Object，值对象
    - DAO：Data Access Object，数据访问对象
    - BO：Business Object，业务对象

## 区分业务对象（BO）和数据访问对象（DAO）

1. DAO中的方法都是**单精度方法**或者称之为**细粒度方法**。什么叫单精度？**一个方法只考虑一个操作**，比如添加，那就是insert操作、查询那就是select操作...

2.  BO中的方法属于业务方法，也实际的业务是比较复杂的，可能是由多个DAO中的方法写成，因此**业务方法的粒度是比较粗的。**举个例子：注册这个功能属于业务功能，也就是说注册这个方法属于业务方法。 那么这个业务方法中包含了多个DAO方法。也就是说注册这个业务功能需要通过多个DAO方法的组合调用，从而完成注册功能的开发。

   >  注册：
   >                 1. 检查用户名是否已经被注册 - DAO中的select操作
   >                                 2. 向用户表新增一条新用户记录 - DAO中的insert操作
   >                                 3. 向用户积分表新增一条记录（新用户默认初始化积分100分） - DAO中的insert操作
   >                                                 4. 向系统消息表新增一条记录（某某某新用户注册了，需要根据通讯录信息向他的联系人推送消息） - DAO中的insert操作
   >                                                    5. 向系统日志表新增一条记录（某用户在某IP在某年某月某日某时某分某秒某毫秒注册） - DAO中的insert操作

# 控制反转(IOC)和依赖注入(DI)

## 耦合和依赖

- 依赖指的是某某某离不开某某某， 在软件系统中，层与层之间是存在依赖的。我们也称之为耦合。
- 我们系统架构或者是设计的一个原则是： **高内聚低耦合**。
- **层内部的组成应该是高度聚合的**，而**层与层之间的关系应该是低耦合的**，最理想的情况0耦合（就是没有耦合，比如某些可自选模块自定义的系统）

## 控制反转(IOC)

- 之前在Servlet中，我们创建service对象用的是`FruitService fruitService = new FruitServiceImpl();`这句话如果出现在servlet中的某个方法内部，那么这个fruitService的作用域（生命周期）应该就是这个方法级别；如果这句话出现在servlet的类中，也就是说fruitService是一个成员变量，那么这个fruitService的作用域（生命周期）应该就是这个servlet实例级别；很明显这样做使得两个对象之间存在一定的耦合，可以进一步通过控制反转进行优化。
- 之后我们在applicationContext.xml中定义了这个fruitService。然后通过解析XML，产生fruitService实例，存放在beanMap中，这个beanMap在一个BeanFactory中，因此，我们转移（改变）了之前的service实例、dao实例等等他们的生命周期。**控制权从程序员转移到BeanFactory。这个现象我们称之为控制反转。**
- **beanMap中的beans都是单例的**
- applicationContext.xml代码示例：

```xml
<?xml version="1.0" encoding="utf-8"?>

<beans>

    <bean id="fruitDAO" class="com.atguigu.fruit.dao.impl.FruitDAOImpl"/>
    <bean id="fruitService" class="com.atguigu.fruit.service.impl.FruitServiceImpl">
        <!-- property标签用来表示属性；name表示属性名；ref表示引用其他bean的id值，这个property标签的意思是，需要将该bean中的名为fruitDAO的属性赋值为名为fruitDAO的bean的实例-->
        <property name="fruitDAO" ref="fruitDAO"/>
    </bean>
    <bean id="fruit" class="com.atguigu.fruit.controllers.FruitController">
        <property name="fruitService" ref="fruitService"/>
    </bean>
</beans>
        
<!--
Node 节点
    Element 元素节点，就是标签
    Text 文本节点，回车和空格也算文本节点
例如：
<sname>jim</sname>中有两个元素节点，一个文本节点

<bean id="fruit" class="com.atguigu.fruit.controllers.FruitController">
        <property name="fruitService" ref="fruitService"/>
 </bean>中有三个元素节点和两个文本节点，这两个文本节点分别是第一个元素节点后的回车和空格、第二个元素节点后的回车和空格
-->




<!--
1.概念
HTML : 超文本标记语言
XML : 可扩展的标记语言
HTML是XML的一个子集

2.XML包含三个部分：
1) XML声明 ， 而且声明这一行代码必须在XML文件的第一行
2) DTD 文档类型定义
3) XML正文
 -->
```

- BeanFactory.java代码示例：

  ```java
  package com.atguigu.myssm.io;
  
  public interface BeanFactory {
      Object getBean(String id);//用来根据javaBean的name来获取javaBean实例
  }
  ```

- ClassPathXmlApplicationContext.java代码示例：

  ```java
  //主要是将之前在DispatcherServlet中读取配置文件、生成文档对象、构建beanMap的步骤移动到了这里。
  public class ClassPathXmlApplicationContext implements BeanFactory {
  
      private Map<String,Object> beanMap = new HashMap<>();
  
      public ClassPathXmlApplicationContext(){
          try {
              InputStream inputStream = getClass().getClassLoader().getResourceAsStream("applicationContext.xml");
              //1.创建DocumentBuilderFactory
              DocumentBuilderFactory documentBuilderFactory = DocumentBuilderFactory.newInstance();
              //2.创建DocumentBuilder对象
              DocumentBuilder documentBuilder = documentBuilderFactory.newDocumentBuilder() ;
              //3.创建Document对象
              Document document = documentBuilder.parse(inputStream);
  
              //4.获取所有的bean节点
              NodeList beanNodeList = document.getElementsByTagName("bean");
              for(int i = 0 ; i<beanNodeList.getLength() ; i++){
                  Node beanNode = beanNodeList.item(i);
                  if(beanNode.getNodeType() == Node.ELEMENT_NODE){
                      Element beanElement = (Element)beanNode ;
                      String beanId =  beanElement.getAttribute("id");
                      String className = beanElement.getAttribute("class");
                      Class beanClass = Class.forName(className);
                      //创建bean实例
                      Object beanObj = beanClass.newInstance() ;
                      //将bean实例对象保存到map容器中
                      beanMap.put(beanId , beanObj) ;
                      //到目前为止，此处需要注意的是，bean和bean之间的依赖关系还没有设置
                  }
              }
              //5.组装bean之间的依赖关系，手动注入依赖
              for(int i = 0 ; i<beanNodeList.getLength() ; i++){
                  Node beanNode = beanNodeList.item(i);
                  if(beanNode.getNodeType() == Node.ELEMENT_NODE) {
                      Element beanElement = (Element) beanNode;
                      String beanId = beanElement.getAttribute("id");
                      NodeList beanChildNodeList = beanElement.getChildNodes();
                      for (int j = 0; j < beanChildNodeList.getLength() ; j++) {
                          Node beanChildNode = beanChildNodeList.item(j);
                          if(beanChildNode.getNodeType()==Node.ELEMENT_NODE && "property".equals(beanChildNode.getNodeName())){
                              Element propertyElement = (Element) beanChildNode;
                              String propertyName = propertyElement.getAttribute("name");
                              String propertyRef = propertyElement.getAttribute("ref");
                              //1) 找到propertyRef对应的实例
                              Object refObj = beanMap.get(propertyRef);
                              //2) 将refObj设置到当前bean对应的实例的property属性上去
                              Object beanObj = beanMap.get(beanId);
                              Class beanClazz = beanObj.getClass();
                              Field propertyField = beanClazz.getDeclaredField(propertyName);
                              propertyField.setAccessible(true);
                              propertyField.set(beanObj,refObj);
                          }
                      }
                  }
              }
          } catch (ParserConfigurationException e) {
              e.printStackTrace();
          } catch (SAXException e) {
              e.printStackTrace();
          } catch (IOException e) {
              e.printStackTrace();
          } catch (IllegalAccessException e) {
              e.printStackTrace();
          } catch (InstantiationException e) {
              e.printStackTrace();
          } catch (ClassNotFoundException e) {
              e.printStackTrace();
          } catch (NoSuchFieldException e) {
              e.printStackTrace();
          }
      }
  
  
      @Override
      public Object getBean(String id) {
          return beanMap.get(id);
      }
  }
  ```

- DispatcherServlet.java代码示例：

  ```java
  //主要修改了init方法和修复了后面的一些因代码专业而产生的bug
  @WebServlet("*.do")
  public class DispatcherServlet extends ViewBaseServlet{
  
      private BeanFactory beanFactory ;
  
      public DispatcherServlet(){
      }
  
      public void init() throws ServletException {
          super.init();
          beanFactory = new ClassPathXmlApplicationContext();//之后通过beanFactory来获取javaBean实例。
      }
  
      @Override
      protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          //设置编码
          request.setCharacterEncoding("UTF-8");
          //假设url是：  http://localhost:8080/pro15/hello.do
          //那么servletPath是：    /hello.do
          // 我的思路是：
          // 第1步： /hello.do ->   hello   或者  /fruit.do  -> fruit
          // 第2步： hello -> HelloController 或者 fruit -> FruitController
          String servletPath = request.getServletPath();
          servletPath = servletPath.substring(1);
          int lastDotIndex = servletPath.lastIndexOf(".do") ;
          servletPath = servletPath.substring(0,lastDotIndex);
  
          Object controllerBeanObj = beanFactory.getBean(servletPath);
  
          String operate = request.getParameter("operate");
          if(StringUtil.isEmpty(operate)){
              operate = "index" ;
          }
  
          try {
              Method[] methods = controllerBeanObj.getClass().getDeclaredMethods();
              for(Method method : methods){
                  if(operate.equals(method.getName())){
                      //1.统一获取请求参数
  
                      //1-1.获取当前方法的参数，返回参数数组
                      Parameter[] parameters = method.getParameters();
                      //1-2.parameterValues 用来承载参数的值
                      Object[] parameterValues = new Object[parameters.length];
                      for (int i = 0; i < parameters.length; i++) {
                          Parameter parameter = parameters[i];
                          String parameterName = parameter.getName() ;
                          //如果参数名是request,response,session 那么就不是通过请求中获取参数的方式了
                          if("request".equals(parameterName)){
                              parameterValues[i] = request ;
                          }else if("response".equals(parameterName)){
                              parameterValues[i] = response ;
                          }else if("session".equals(parameterName)){
                              parameterValues[i] = request.getSession() ;
                          }else{
                              //从请求中获取参数值
                              String parameterValue = request.getParameter(parameterName);
                              String typeName = parameter.getType().getName();
  
                              Object parameterObj = parameterValue ;
  
                              if(parameterObj!=null) {
                                  if ("java.lang.Integer".equals(typeName)) {
                                      parameterObj = Integer.parseInt(parameterValue);
                                  }
                              }
  
                              parameterValues[i] = parameterObj ;
                          }
                      }
                      //2.controller组件中的方法调用
                      method.setAccessible(true);
                      Object returnObj = method.invoke(controllerBeanObj,parameterValues);
  
                      //3.视图处理
                      String methodReturnStr = (String)returnObj ;
                      if(methodReturnStr.startsWith("redirect:")){        //比如：  redirect:fruit.do
                          String redirectStr = methodReturnStr.substring("redirect:".length());
                          response.sendRedirect(redirectStr);
                      }else{
                          super.processTemplate(methodReturnStr,request,response);    // 比如：  "edit"
                      }
                  }
              }
  
              /*
              }else{
                  throw new RuntimeException("operate值非法!");
              }
              */
          } catch (IllegalAccessException e) {
              e.printStackTrace();
          } catch (InvocationTargetException e) {
              e.printStackTrace();
          }
      }
  }
  
  // 常见错误： IllegalArgumentException: argument type mismatch
  ```

## 依赖注入(DI)

- 之前我们在控制层出现代码：`FruitService fruitService = new FruitServiceImpl();`那么，控制层和service层存在耦合。
- 之后，我们将代码修改成`FruitService fruitService = null ;`
         然后，在配置文件中配置:
        ` <bean id="fruit" class="FruitController">
              <property name="fruitService" ref="fruitService"/>
        </bean>`
- 通过上面的ClassPathXmlApplicationContext.java的代码可以知道，我们是**通过在构建完beanMap后利用反射来处理xml文件中的内容实现依赖注入**的，**依赖注入实际上就是给beanMap中的javaBean实例中的某些属性赋上指定的值**，要注意beanMap中的javaBean实例都是单例的，所以只需要注入一次依赖，后面就都可以使用了。

# 过滤器Filter

- Filter也属于Servlet规范
- 通过Filter我们可以实现拦截某些请求，对其进行相应的处理后放行给后面的controller
- 一个Filter可以对应多个Servlet，同样，一个Servlet也可以对应多个Filter。
- 配置了相应的Filter后，请求发送到服务器的时候，Filter会进行拦截并执行自定义的操作，然后**需要手动将请求向后放行**，同时，在响应发回客户端的时候，相应的Filter同样也会做出拦截并执行自定义的操作。
- 为了降低耦合，在大项目种通常一个过滤器只执行一种过滤操作，不过还是要具体情况具体分析。

![image-20220725112247959](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220725112247959.png)

## Filter开发步骤

1. 新建类**实现Filter接口**
2. 实现Filter接口中的三个方法：**init、doFilter、destroy**
3. 配置（注册）Filter：可以使用**注解@WebFilter(url)**或者使用**xml文件的\<filter> 和 \<filter-mapping>**进行注册，Filter在配置时，和servlet一样，**也可以配置通配符**，例如 @WebFilter("*.do")表示拦截所有以.do结尾的请求。

## doFilter方法的编写规则

- 向后放行请求的api是：`filterChain.doFilter(servletRequest,servletResponse);`
- 在向后放行之前要做的自定义操作需要写在向后放行的代码之前
- 在传回响应的时候要做的自定义操作需要写在向后放行的代码之后

## 过滤器链

- 一个Servlet可以对应多个Filter，这多个Filter会以链状的形式进行响应，如果采取的是**注解的方式进行配置**，那么过滤器链的**拦截顺序是按照全类名的先后顺序排序**的。如果采取的是**xml的方式进行配置**，那么过滤器链的**拦截顺序是按照配置的先后顺序进行排序**。

![image-20220725114357536](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220725114357536.png)

## 实际应用举例

- 可以将之前在**DispatcherServlet**中设置编码方式的操作移交给Filter进行处理

![image-20220725114152655](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220725114152655.png)

- CharacterEncodingFilter.java代码示例

```java
@WebFilter(urlPatterns = {"*.do"},initParams = {@WebInitParam(name = "encoding",value = "UTF-8")})//设置初始配置数据
public class CharacterEncodingFilter implements Filter {

    private String encoding = "UTF-8";//设置encoding的默认值

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {//读取初始配置数据中的编码格式，如果没有配置，那么encoding就是默认值UTF-8
        String encodingStr = filterConfig.getInitParameter("encoding");
        if(StringUtil.isNotEmpty(encodingStr)){//如果关于encoding的初始化配置数据不为空，则对encoding进行更新。
            encoding = encodingStr ;
        }
    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        ((HttpServletRequest)servletRequest).setCharacterEncoding(encoding);//先强转，再设置编码格式，在这里设置了编码格式后，就可以把DispatcherServlet中设置编码格式的操作注释掉了。
        filterChain.doFilter(servletRequest,servletResponse);//向后放行

    }

    @Override
    public void destroy() {

    }
}
```

# 事务管理

- 由于一个业务逻辑中可能包含多个DAO层的语句，根据**事务的一致性**，事务中只要有一个部分出了问题，那么整个事务都要回滚，所以肯定不能在DAO层处理事务的问题，得出结论：**事务管理不能以DAO层的单精度方法为单位，而应该以业务层的方法为单位**。

![image-20220725203653427](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220725203653427.png)

![image-20220725203732595](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220725203732595.png)

- 之前讲过Filter，可以**利用Filter进行事务管理**，因为Filter运行在较高层，下层出的任何问题都可以通过Filter进行捕获然后做出响应的操作。但是这样做有个问题，就是需要**让用到的所有的DAO语句用同一个Connection，这样才能让多个操作处于同一个事务中**。

![image-20220725203938932](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220725203938932.png)

- **为了让多个DAO语句使用同一个Connection，我们可以利用ThreadLocal**，就像吃旋转小火锅一样，多个人共用一套食材盆，我们也可以用ThreadLocal中的set和get方法实现让多个DAO语句使用同一个Connection。

![image-20220725204255665](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220725204255665.png)

## 涉及到的组件

- OpenSessionInViewFilter
- TransactionManager
- ThreadLocal
- ConnUtil
- BaseDAO

## ConnUtil

- 将之前写在BaseDAO中的与数据库连接相关的操作单独抽取成一个工具类，在降低耦合的同时，也简化了使用步骤。
- 在其中使用了ThreadLocal作为同一事务的存放唯一Connection的容器。

```java
public class ConnUtil {

    private static ThreadLocal<Connection> threadLocal = new ThreadLocal<>();
    //private static ThreadLocal<Object> threadLocal2 = new ThreadLocal<>();
    //private static ThreadLocal<Object> threadLocal3 = new ThreadLocal<>();

    public static final String DRIVER = "com.mysql.jdbc.Driver" ;
    public static final String URL = "jdbc:mysql://localhost:3306/fruitdb?useUnicode=true&characterEncoding=utf-8&useSSL=false";
    public static final String USER = "root";
    public static final String PWD = "123456" ;

    private static Connection createConn(){
        try {
            //1.加载驱动
            Class.forName(DRIVER);
            //2.通过驱动管理器获取连接对象
            return DriverManager.getConnection(URL, USER, PWD);
        } catch (ClassNotFoundException | SQLException e) {
            e.printStackTrace();
        }
        return null ;
    }

    public static Connection getConn(){
        Connection conn = threadLocal.get();
        if(conn==null){
            conn =createConn();
            threadLocal.set(conn);
        }
        return threadLocal.get() ;
    }

    public static void closeConn() throws SQLException {
        Connection conn = threadLocal.get();
        if(conn==null){
            return ;
        }
        if(!conn.isClosed()){
            conn.close();
            threadLocal.set(null);
        }
    }
}
```

## BaseDAO

- 在写完ConnUtil工具类后，要将开启、使用、关闭连接的操作替换成工具类中的方法。

```java
public abstract class BaseDAO<T> {
    protected Connection conn ;
    protected PreparedStatement psmt ;
    protected ResultSet rs ;

    //T的Class对象
    private Class entityClass ;

    public BaseDAO() {
        //getClass() 获取Class对象，当前我们执行的是new FruitDAOImpl() , 创建的是FruitDAOImpl的实例
        //那么子类构造方法内部首先会调用父类（BaseDAO）的无参构造方法
        //因此此处的getClass()会被执行，但是getClass获取的是FruitDAOImpl的Class
        //所以getGenericSuperclass()获取到的是BaseDAO的Class
        Type genericType = getClass().getGenericSuperclass();
        //ParameterizedType 参数化类型
        Type[] actualTypeArguments = ((ParameterizedType) genericType).getActualTypeArguments();
        //获取到的<T>中的T的真实的类型
        Type actualType = actualTypeArguments[0];

        try {
            entityClass = Class.forName(actualType.getTypeName());
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
            throw new DAOException("BaseDAO 构造方法出错了，可能的原因是没有指定<>中的类型");
        }

    }

    protected Connection getConn(){
        return ConnUtil.getConn();
    }

    protected void close(ResultSet rs , PreparedStatement psmt , Connection conn){

    }

    //给预处理命令对象设置参数
    private void setParams(PreparedStatement psmt , Object... params) throws SQLException {
        if(params!=null && params.length>0){
            for (int i = 0; i < params.length; i++) {
                psmt.setObject(i+1,params[i]);
            }
        }
    }

    //执行更新，返回影响行数
    protected int executeUpdate(String sql , Object... params) {
        boolean insertFlag = false ;
        insertFlag = sql.trim().toUpperCase().startsWith("INSERT");

        conn = getConn();
        try{
            if(insertFlag){
                psmt = conn.prepareStatement(sql,Statement.RETURN_GENERATED_KEYS);
            }else {
                psmt = conn.prepareStatement(sql);
            }
            setParams(psmt,params);
            int count = psmt.executeUpdate() ;

            if(insertFlag){
                rs = psmt.getGeneratedKeys();
                if(rs.next()){
                    return ((Long)rs.getLong(1)).intValue();
                }
            }
            return 0 ;
        }catch (SQLException e){
            e.printStackTrace();
            throw new DAOException("BaseDAO executeUpdate出错了");
        }
    }

    //通过反射技术给obj对象的property属性赋propertyValue值
    private void setValue(Object obj ,  String property , Object propertyValue) throws NoSuchFieldException, IllegalAccessException {
        Class clazz = obj.getClass();

        //获取property这个字符串对应的属性名 ， 比如 "fid"  去找 obj对象中的 fid 属性
        Field field = clazz.getDeclaredField(property);
        if(field!=null){
            field.setAccessible(true);
            field.set(obj,propertyValue);
        }

    }

    //执行复杂查询，返回例如统计结果
    protected Object[] executeComplexQuery(String sql , Object... params){
        conn = getConn() ;
        try{
            psmt = conn.prepareStatement(sql);
            setParams(psmt,params);
            rs = psmt.executeQuery();

            //通过rs可以获取结果集的元数据
            //元数据：描述结果集数据的数据 , 简单讲，就是这个结果集有哪些列，什么类型等等

            ResultSetMetaData rsmd = rs.getMetaData();
            //获取结果集的列数
            int columnCount = rsmd.getColumnCount();
            Object[] columnValueArr = new Object[columnCount];
            //6.解析rs
            if(rs.next()){
                for(int i = 0 ; i<columnCount;i++){
                    Object columnValue = rs.getObject(i+1);     //33    苹果      5
                    columnValueArr[i]=columnValue;
                }
                return columnValueArr ;
            }
        }catch(SQLException e){
            e.printStackTrace();
            throw new DAOException("BaseDAO executeComplexQuery出错了");
        }

        return null ;
    }

    //执行查询，返回单个实体对象
    protected T load(String sql , Object... params){
        conn = getConn() ;
        try{
            psmt = conn.prepareStatement(sql);
            setParams(psmt,params);
            rs = psmt.executeQuery();

            //通过rs可以获取结果集的元数据
            //元数据：描述结果集数据的数据 , 简单讲，就是这个结果集有哪些列，什么类型等等

            ResultSetMetaData rsmd = rs.getMetaData();
            //获取结果集的列数
            int columnCount = rsmd.getColumnCount();
            //6.解析rs
            if(rs.next()){
                T entity = (T)entityClass.newInstance();

                for(int i = 0 ; i<columnCount;i++){
                    String columnName = rsmd.getColumnName(i+1);            //fid   fname   price
                    Object columnValue = rs.getObject(i+1);     //33    苹果      5
                    setValue(entity,columnName,columnValue);
                }
                return entity ;
            }
        }catch (Exception e){
            e.printStackTrace();
            throw new DAOException("BaseDAO load出错了");
        }

        return null ;
    }

    //执行查询，返回List
    protected List<T> executeQuery(String sql , Object... params){
        List<T> list = new ArrayList<>();
        conn = getConn() ;
        try{
            psmt = conn.prepareStatement(sql);
            setParams(psmt,params);
            rs = psmt.executeQuery();

            //通过rs可以获取结果集的元数据
            //元数据：描述结果集数据的数据 , 简单讲，就是这个结果集有哪些列，什么类型等等

            ResultSetMetaData rsmd = rs.getMetaData();
            //获取结果集的列数
            int columnCount = rsmd.getColumnCount();
            //6.解析rs
            while(rs.next()){
                T entity = (T)entityClass.newInstance();

                for(int i = 0 ; i<columnCount;i++){
                    String columnName = rsmd.getColumnName(i+1);            //fid   fname   price
                    Object columnValue = rs.getObject(i+1);     //33    苹果      5
                    setValue(entity,columnName,columnValue);
                }
                list.add(entity);
            }
        }catch (Exception e){
            e.printStackTrace();
            throw new DAOException("BaseDAO executeQuery出错了");
        }
        return list ;
    }
}
```

## TransactionManager

- 将**开启、提交、回滚事务的方法**整合到这个类中，其中每个方法都是多精度的方法，用到了Connection的和ConnUtil的单精度方法。

```java
public class TransactionManager {

    //开启事务
    public static void beginTrans() throws SQLException {
        ConnUtil.getConn().setAutoCommit(false);
    }

    //提交事务
    public static void commit() throws SQLException {
        Connection conn = ConnUtil.getConn();
        conn.commit();
        ConnUtil.closeConn();
    }

    //回滚事务
    public static void rollback() throws SQLException {
        Connection conn = ConnUtil.getConn();
        conn.rollback();
        ConnUtil.closeConn();
    }
}
```

## OpenSessionInViewFilter

- 这个拦截器用来在向后**放行之前开启事务**，在**放行之后提交事务**，如果**中间捕获到异常，则回滚事务**。
- 注意，**由于这个组件所在的层次比较高，因此如果想要在这个组件中catch到你想catch到的异常，那么需要将层次比较低的组件中的关于你想catch到的异常的try-catch语句删掉，不然异常会在层次比较低的组件中被catch到，使得这个组件无法catch到相关的异常，从而无法将事务进行回滚**。

```java
@WebFilter("*.do")
public class OpenSessionInViewFilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        try{
            TransactionManager.beginTrans();
            System.out.println("开启事务....");
            filterChain.doFilter(servletRequest, servletResponse);
            TransactionManager.commit();
            System.out.println("提交事务...");
        }catch (Exception e){
            e.printStackTrace();
            try {
                TransactionManager.rollback();
                System.out.println("回滚事务....");
            } catch (SQLException ex) {
                ex.printStackTrace();
            }
        }
    }

    @Override
    public void destroy() {

    }
}
```

## ThreadLocal

- ThreadLocal称之为**本地线程变量** 。 我们可以**通过set方法在当前线程上存储数据、通过get方法在当前线程上获取数据**。但是要注意数据并不是存储在线程上的，而是存在map中。

- 主要是两个方法：get()用来获取当前线程上的数据、set(obj)用来在当前线程上存储数据。
- 从源码分析可得：**一个ThreadLocal实例只代表一个本地线程变量**。如果需要多个本地线程变量，就需要多个ThreadLocal实例。

### set(obj)方法源码分析

```java
public void set(T value) {
    Thread t = Thread.currentThread(); //获取当前的线程
    ThreadLocalMap map = getMap(t);    //每一个线程都维护各自的一个容器（ThreadLocalMap）
    if (map != null)
        map.set(this, value);          //这里的key对应的是ThreadLocal，因为我们的组件中需要传输（共享）的对象可能会有多个（不止Connection）
    else
        createMap(t, value);           //默认情况下map是没有初始化的，那么第一次往其中添加数据时，会去初始化
}
```

### get()源码分析

```java
public T get() {
    Thread t = Thread.currentThread(); //获取当前的线程
    ThreadLocalMap map = getMap(t);    //获取和这个线程（企业）相关的ThreadLocalMap（也就是工作纽带的集合）
    if (map != null) {
        ThreadLocalMap.Entry e = map.getEntry(this);   //this指的是ThreadLocal对象，通过它才能知道是哪一个工作纽带
        if (e != null) {
            @SuppressWarnings("unchecked")
            T result = (T)e.value;     //entry.value就可以获取到工具箱了
            return result;
        }
    }
    return setInitialValue();
}
```

# 监听器

- 监听器中含有很多的回调函数，当对应的情况出现的时候，回调函数就会被自动地调用。

## Servlet监听器接口种类

- ServletContextListener - 监听ServletContext对象的创建和销毁的过程
- HttpSessionListener - 监听HttpSession对象的创建和销毁的过程
- ServletRequestListener - 监听ServletRequest对象的创建和销毁的过程



- ServletContextAttributeListener - 监听ServletContext的保存作用域的改动(add,remove,replace)
- HttpSessionAttributeListener - 监听HttpSession的保存作用域的改动(add,remove,replace)
- ServletRequestAttributeListener - 监听ServletRequest的保存作用域的改动(add,remove,replace)



- HttpSessionBindingListener - 监听某个对象在Session域中的创建与移除
- HttpSessionActivationListener - 监听某个对象在Session域中的序列化和反序列化

## 自定义监听器

- 自定义监听器需要根据自己想要监听的内容**选择相应的接口进行实现**，然后**重写接口中的方法**，最后**在自定义监听器上写上@WebListener**即可。

## 监听器实践-ContextLoaderListener

- 在之前的代码中，创建IOC容器的步骤是放在DispatcherServlet的init方法中的，由于DispatcherServlet是在第一次被调用的时候进行init的，所以这样做可能会使得第一次响应的时间过长，ServletContext随着Tomcat服务器的启动而启动，所以可以考虑**监听ServletContext的启动，在ServletContext启动的时候去创建IOC容器，然后将其保存到application作用域也就是ServletContext中，然后在DispatcherServlet进行初始化（init）的时候，从ServletContext中获取IOC容器**，这样可以优化第一次的访问效率。

- ContextLoaderListener代码示例：

  ```java
  //监听上下文启动，在上下文启动的时候去创建IOC容器,然后将其保存到application作用域
  //后面中央控制器再从application作用域中去获取IOC容器
  @WebListener
  public class ContextLoaderListener implements ServletContextListener {
      @Override
      public void contextInitialized(ServletContextEvent servletContextEvent) {
          //1.获取ServletContext对象
          ServletContext application = servletContextEvent.getServletContext();
          //2.获取上下文的初始化参数
          String path = application.getInitParameter("contextConfigLocation");
          //3.创建IOC容器
          BeanFactory beanFactory = new ClassPathXmlApplicationContext(path);
          //4.将IOC容器保存到application作用域
          application.setAttribute("beanFactory",beanFactory);
      }
  
      @Override
      public void contextDestroyed(ServletContextEvent servletContextEvent) {
  
      }
  }
  ```

- 修改后的DispatcherServlet的init方法：

  ```java
  public void init() throws ServletException {
  	super.init();
      //之前是在此处主动创建IOC容器的
      //现在优化为从application作用域去获取
      //beanFactory = new ClassPathXmlApplicationContext();
      ServletContext application = getServletContext();
      Object beanFactoryObj = application.getAttribute("beanFactory");
      if(beanFactoryObj!=null){
          beanFactory = (BeanFactory)beanFactoryObj ;
      }else{
          throw new RuntimeException("IOC容器获取失败！");
      }
  }
  ```

- 为了实现可以自定义IOC容器的配置文件，也对ClassPathXmlApplicationContext.java进行了调整，不过**除了下面这种使用有参构造器的方式外也可以通过读取配置文件中的初始化数据来实现**：

  ```java
  public class ClassPathXmlApplicationContext implements BeanFactory {
  
      private Map<String,Object> beanMap = new HashMap<>();
      private String path = "applicationContext.xml" ;
      public ClassPathXmlApplicationContext(){
          this("applicationContext.xml");
      }
      public ClassPathXmlApplicationContext(String path){
          if(StringUtil.isEmpty(path)){
              throw new RuntimeException("IOC容器的配置文件没有指定...");
          }
          try {
              InputStream inputStream = getClass().getClassLoader().getResourceAsStream(path);
              //1.创建DocumentBuilderFactory
              DocumentBuilderFactory documentBuilderFactory = DocumentBuilderFactory.newInstance();
              //2.创建DocumentBuilder对象
              DocumentBuilder documentBuilder = documentBuilderFactory.newDocumentBuilder() ;
              //3.创建Document对象
              Document document = documentBuilder.parse(inputStream);
  
              //4.获取所有的bean节点
              NodeList beanNodeList = document.getElementsByTagName("bean");
              for(int i = 0 ; i<beanNodeList.getLength() ; i++){
                  Node beanNode = beanNodeList.item(i);
                  if(beanNode.getNodeType() == Node.ELEMENT_NODE){
                      Element beanElement = (Element)beanNode ;
                      String beanId =  beanElement.getAttribute("id");
                      String className = beanElement.getAttribute("class");
                      Class beanClass = Class.forName(className);
                      //创建bean实例
                      Object beanObj = beanClass.newInstance() ;
                      //将bean实例对象保存到map容器中
                      beanMap.put(beanId , beanObj) ;
                      //到目前为止，此处需要注意的是，bean和bean之间的依赖关系还没有设置
                  }
              }
              //5.组装bean之间的依赖关系
              for(int i = 0 ; i<beanNodeList.getLength() ; i++){
                  Node beanNode = beanNodeList.item(i);
                  if(beanNode.getNodeType() == Node.ELEMENT_NODE) {
                      Element beanElement = (Element) beanNode;
                      String beanId = beanElement.getAttribute("id");
                      NodeList beanChildNodeList = beanElement.getChildNodes();
                      for (int j = 0; j < beanChildNodeList.getLength() ; j++) {
                          Node beanChildNode = beanChildNodeList.item(j);
                          if(beanChildNode.getNodeType()==Node.ELEMENT_NODE && "property".equals(beanChildNode.getNodeName())){
                              Element propertyElement = (Element) beanChildNode;
                              String propertyName = propertyElement.getAttribute("name");
                              String propertyRef = propertyElement.getAttribute("ref");
                              //1) 找到propertyRef对应的实例
                              Object refObj = beanMap.get(propertyRef);
                              //2) 将refObj设置到当前bean对应的实例的property属性上去
                              Object beanObj = beanMap.get(beanId);
                              Class beanClazz = beanObj.getClass();
                              Field propertyField = beanClazz.getDeclaredField(propertyName);
                              propertyField.setAccessible(true);
                              propertyField.set(beanObj,refObj);
                          }
                      }
                  }
              }
          } catch (ParserConfigurationException e) {
              e.printStackTrace();
          } catch (SAXException e) {
              e.printStackTrace();
          } catch (IOException e) {
              e.printStackTrace();
          } catch (IllegalAccessException e) {
              e.printStackTrace();
          } catch (InstantiationException e) {
              e.printStackTrace();
          } catch (ClassNotFoundException e) {
              e.printStackTrace();
          } catch (NoSuchFieldException e) {
              e.printStackTrace();
          }
      }
  
  
      @Override
      public Object getBean(String id) {
          return beanMap.get(id);
      }
  }
  ```

# MVC各个层的设计小总结

![image-20220728232151550](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220728232151550.png)

# Cookie

## Cookie简介

- HTTP Cookie（也叫 Web Cookie 或浏览器 Cookie）是**服务器发送到用户浏览器**并**保存在本地**的一小块数据，它**会在浏览器下次向同一服务器再发起请求时被携带并发送到服务器上**。通常，它用于告知服务端两个请求是否来自同一浏览器，如保持用户的登录状态。Cookie 使基于无状态的 HTTP 协议记录稳定的状态信息成为了可能。

## Cookie和Session有什么不同

- **作用范围不同**，Cookie 保存在客户端（浏览器），Session 保存在服务器端。
- **存取方式的不同**，Cookie 只能保存 ASCII，Session 可以存任意数据类型，一般情况下我们可以在 Session 中保持一些常用变量信息，比如说 UserId 等。
- **有效期不同**，Cookie 可设置为长时间保持，比如我们经常使用的默认登录功能，Session 一般失效时间较短，客户端关闭或者 Session 超时都会失效。
- **隐私策略不同**，Cookie 存储在客户端，比较容易遭到不法获取，早期有人将用户的登录名和密码存储在 Cookie 中导致信息被窃取；Session 存储在服务端，安全性相对 Cookie 要好一些。
- **存储大小不同**， 单个 Cookie 保存的数据不能超过 4K，Session 可存储数据远高于 Cookie。

## 使用Cookie

1. 创建Cookie对象，**Cookie cookie = new Cookie(k,v);**
2. 在客户端保存Cookie(在response中添加cookie)，**response.addCookie(Cookie);**
3. 可设置Cookie的有效时长
   - **cookie.setMaxAge(60);**  //设置cookie的有效时长是60秒
   - **cookie.setDomain(pattern);**  //设置在什么域可以访问Cookie，域必须以“ . ”开头，默认是当前域，如果要是设置了别的域且没有显式设置当前域，则当前域无法访问到自己产生的Cookie，这个方法可以**实现Cookie的跨域共享**。
   - **cookie.setPath(url);**  //设置Cookie可以在什么url下可以被访问到，默认是当前应用的url，如果设置了别的url且没有显式设置当前应用的url，则当前应用无法访问到自己产生的Cookie，这个方法可以实现**同一服务器内的Cookie共享**。

4. Cookie的一些基本应用：
   - 记住用户名和密码十天：`setMaxAge(60 * 60 * 24 * 10)`，将Cookie中的信息绑定到输入框中。
   - 十天免登录：验证完Cookie中用户的用户名和密码后直接重定向或者转发到登录后的界面。

5. CookieServlet示例代码：

   ```java
   @WebServlet("/cookie01")
   public class CookieServlet01 extends HttpServlet {
       @Override
       protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
       //1.创建一个Cookie对象
       Cookie cookie = new Cookie("uname","jim");
       //2.将这个Cookie对象保存到浏览器端
       response.addCookie(cookie);
       //转发
   	request.getRequestDispatcher("hello01.html").forward(request,response);
   
       }
   }
   ```

# 用Kaptcha实现验证码

## 为什么要使用验证码

1. 为了防止机器冒充人类做暴力破解
2. 防止大规模在线注册滥用服务
3. 防止滥用在线批量化操作
4. 防止自动发布
5. 防止信息被大量采集聚合

## 如何使用Kaptcha

1. 添加相关jar包

2. 在web.xml文件中注册KaptchaServlet，并设置验证码图片的相关属性

3. 在html页面上编写一个img标签，然后设置src等于KaptchaServlet对应的url-pattern，kaptcha验证码图片的各个属性在**常量接口：Constants**中

4. KaptchaServlet在生成验证码图片时，会**同时将验证码信息保存到session中**，因此，我们在注册请求时，首先将用户文本框中输入的验证码值和session中保存的值进行比较，若相等，则进行注册

5. 后端KaptchaServlet代码示例：

   ```java
   @WebServlet("/kaptcha01")
   public class KaptchaServletDemo01 extends HttpServlet {
       @Override
       protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
           HttpSession session = request.getSession() ;
           Object obj = session.getAttribute("KAPTCHA_SESSION_KEY");//获取验证码的答案
           System.out.println("obj = " + obj);
       }
   }
   ```

6. web.xml中的设置：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
            version="4.0">
       <servlet>
           <servlet-name>KaptchaServlet</servlet-name>
           <servlet-class>com.google.code.kaptcha.servlet.KaptchaServlet</servlet-class>
           <init-param>
               <param-name>kaptcha.border.color</param-name>
               <param-value>red</param-value>
           </init-param>
           <init-param>
               <param-name>kaptcha.textproducer.char.string</param-name>
               <param-value>abcdefg</param-value>
           </init-param>
           <init-param>
               <param-name>kaptcha.noise.impl</param-name>
               <param-value>com.google.code.kaptcha.impl.NoNoise</param-value>
           </init-param>
       </servlet>
       <servlet-mapping>
           <servlet-name>KaptchaServlet</servlet-name>
           <url-pattern>/kaptch.jpg</url-pattern>
       </servlet-mapping>
   </web-app>
   ```

7. H5测试代码：

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <title>Title</title>
   </head>
   <body>
       <img src="kaptch.jpg"/>
   </body>
   </html>
   ```

   

# 正则表达式

## 学习目标

* 掌握正则表达式的作用
* 掌握正则表达式的语法
* 了解常见的正则表达式

## 内容讲解

### 正则表达式的概念

正则表达式是对字符串操作的一种逻辑公式，就是用事先定义好的一些特定字符、及这些特定字符的组合，组成一个“规则字符串”，这个“规则字符串”用来表达对字符串的一种过滤逻辑。用我们自己的话来说: **正则表达式用来校验字符串是否满足一定的规则的公式**

### 正则表达式的用途

所以正则表达式有三个主要用途：

- 模式验证: 检测某个字符串是否符合规则，例如检测手机号、身份证号等等是否符合规范
- 匹配读取:  将目标字符串中满足规则的部分**读取**出来，例如将整段文本中的邮箱地址读取出来
- 匹配替换:  将目标字符串中满足标准的部分**替换**为其他字符串,例如将整段文本中的"hello"替换成"haha"

### 正则表达式的语法

#### js创建正则表达式对象

* 对象形式：`var reg = new RegExp("正则表达式")`当正则表达式中有"/"那么就使用这种
* 直接量形式：`var reg = /正则表达式/`一般使用这种声明方式 

#### 正则表达式入门案例

##### 模式验证: 校验字符串中是否包含'o'字母

**注意**：这里是使用**正则表达式对象**来**调用**方法。

```javascript
// 创建一个最简单的正则表达式对象
var reg = /o/;

// 创建一个字符串对象作为目标字符串
var str = 'Hello World!';

// 调用正则表达式对象的test()方法验证目标字符串是否满足我们指定的这个模式，返回结果true
console.log("字符串中是否包含'o'="+reg.test(str));
```

##### 匹配读取: 读取字符串中的所有'o'

```javascript
//匹配读取: 读取一个字符串中的所有'l'字母
// g表示全文查找,如果不使用g那么就只能查找到第一个匹配的内容
//1. 编写一个正则表达式
var reg2 = /l/g
//2. 使用正则表达式去读取字符串
var arr = str.match(reg2);
console.log(arr)
```

##### 匹配替换: 将字符串中的第一个'o'替换成'@'

```javascript
var newStr = str.replace(reg,'@');
// 只有第一个o被替换了，说明我们这个正则表达式只能匹配第一个满足的字符串
console.log("str.replace(reg)="+newStr);//Hell@ World!
// 原字符串并没有变化，只是返回了一个新字符串
console.log("str="+str);//str=Hello World!
```

#### 正则表达式的匹配模式

##### 全文查找

如果不**在正则表达式后使用g对正则表达式对象进行修饰**，则使用正则表达式进行查找时，仅返回第一个匹配；使用g后，返回所有匹配。

```javascript
// 目标字符串
var targetStr = 'Hello World!';

// 没有使用全局匹配的正则表达式
var reg = /[A-Z]/;
// 获取全部匹配
var resultArr = targetStr.match(reg);
// 数组长度为1
console.log("resultArr.length="+resultArr.length);

// 遍历数组，发现只能得到'H'
for(var i = 0; i < resultArr.length; i++){
    console.log("resultArr["+i+"]="+resultArr[i]);
}
```

对比代码：

```javascript
// 目标字符串
var targetStr = 'Hello World!';

// 使用了全局匹配的正则表达式
var reg = /[A-Z]/g;
// 获取全部匹配
var resultArr = targetStr.match(reg);
// 数组长度为2
console.log("resultArr.length="+resultArr.length);

// 遍历数组，发现可以获取到“H”和“W”
for(var i = 0; i < resultArr.length; i++){
    console.log("resultArr["+i+"]="+resultArr[i]);
}
```

##### 忽略大小写

**在正则表达式后使用i对正则表达式对象进行修饰**。

```javascript
//目标字符串
var targetStr = 'Hello WORLD!';

//没有使用忽略大小写的正则表达式
var reg = /o/g;
//获取全部匹配
var resultArr = targetStr.match(reg);
//数组长度为1
console.log("resultArr.length="+resultArr.length);
//遍历数组，仅得到'o'
for(var i = 0; i < resultArr.length; i++){
    console.log("resultArr["+i+"]="+resultArr[i]);
}
```

对比代码：

```javascript
//目标字符串
var targetStr = 'Hello WORLD!';

//使用了忽略大小写的正则表达式
var reg = /o/gi;
//获取全部匹配
var resultArr = targetStr.match(reg);
//数组长度为2
console.log("resultArr.length="+resultArr.length);
//遍历数组，得到'o'和'O'
for(var i = 0; i < resultArr.length; i++){
    console.log("resultArr["+i+"]="+resultArr[i]);
}
```

##### 多行查找

**在正则表达式后使用m对正则表达式对象进行修饰**，若不使用多行查找模式，目标字符串中不管有没有换行符都会被当作一行。

```javascript
//目标字符串1
var targetStr01 = 'Hello\nWorld!';
//目标字符串2
var targetStr02 = 'Hello';

//匹配以'Hello'结尾的正则表达式，没有使用多行匹配
var reg = /Hello$/;
console.log(reg.test(targetStr01));//false

console.log(reg.test(targetStr02));//true
```

对比代码：

```javascript
//目标字符串1
var targetStr01 = 'Hello\nWorld!';
//目标字符串2
var targetStr02 = 'Hello';

//匹配以'Hello'结尾的正则表达式，使用了多行匹配
var reg = /Hello$/m;
console.log(reg.test(targetStr01));//true

console.log(reg.test(targetStr02));//true
```

#### 元字符

 在正则表达式中被赋予特殊含义的字符，不能被直接当做普通字符使用。如果要匹配元字符本身，需要对元字符进行转义，转义的方式是在元字符前面加上“\”，例如：\^ 

##### 常用的元字符

| 代码 | 说明                                                         |
| ---- | ------------------------------------------------------------ |
| .    | 匹配除换行字符以外的任意字符。                               |
| \w   | 匹配字母或数字或下划线等价于[a-zA-Z0-9_]                     |
| \W   | 匹配任何非单词字符。等价于\[^A-Za-z0-9_]                     |
| \s   | 匹配任意的空白符，包括空格、制表符、换页符等等。等价于[\f\n\r\t\v]。 |
| \S   | 匹配任何非空白字符。等价于\[^\f\n\r\t\v]。                   |
| \d   | 匹配数字。等价于[0-9]。                                      |
| \D   | 匹配一个非数字字符。等价于\[^0-9]                            |
| \b   | 匹配单词的开始或结束                                         |
| ^    | 匹配字符串的开始，但在[]中使用表示取反                       |
| $    | 匹配字符串的结束                                             |

##### 例子一

```javascript
var str = 'one two three four';
// 匹配全部空格
var reg = /\s/g;
// 将空格替换为@
var newStr = str.replace(reg,'@'); // one@two@three@four
console.log("newStr="+newStr);
```

##### 例子二

```javascript
var str = '今年是2014年';
// 匹配至少一个数字
var reg = /\d+/g;
str = str.replace(reg,'abcd');
console.log('str='+str); // 今年是abcd年
```

##### 例子三

```javascript
var str01 = 'I love Java';
var str02 = 'Java love me';
// 匹配以Java开头
var reg = /^Java/g;
console.log('reg.test(str01)='+reg.test(str01)); // flase
console.log("<br />");
console.log('reg.test(str02)='+reg.test(str02)); // true
```

##### 例子四

```javascript
var str01 = 'I love Java';
var str02 = 'Java love me';
// 匹配以Java结尾
var reg = /Java$/g;
console.log('reg.test(str01)='+reg.test(str01)); // true
console.log("<br />");
console.log('reg.test(str02)='+reg.test(str02)); // flase
```

#### 字符集合

| 语法格式    | 示例                                                         | 说明                                               |
| ----------- | ------------------------------------------------------------ | -------------------------------------------------- |
| [字符列表]  | 正则表达式：[abc] 含义：目标字符串包含abc中的任何一个字符 目标字符串：plain 是否匹配：是 原因：plain中的“a”在列表“abc”中 | 目标字符串中任何一个字符出现在字符列表中就算匹配。 |
| [^字符列表] | [^abc] 含义：目标字符串包含abc以外的任何一个字符 目标字符串：plain 是否匹配：是 原因：plain中包含“p”、“l”、“i”、“n” | 匹配字符列表中未包含的任意字符。                   |
| [字符范围]  | 正则表达式：[a-z] 含义：所有小写英文字符组成的字符列表 正则表达式：[A-Z] 含义：所有大写英文字符组成的字符列表 | 匹配指定范围内的任意字符。                         |

```javascript
var str01 = 'Hello World';
var str02 = 'I am Tom';
//匹配abc中的任何一个
var reg = /[abc]/g;
console.log('reg.test(str01)='+reg.test(str01));//flase
console.log('reg.test(str02)='+reg.test(str02));//true
```

#### 出现次数

| 代码  | 说明           |
| ----- | -------------- |
| *     | 出现零次或多次 |
| +     | 出现一次或多次 |
| ?     | 出现零次或一次 |
| {n}   | 出现n次        |
| {n,}  | 出现n次或多次  |
| {n,m} | 出现n到m次     |

```javascript
console.log("/[a]{3}/.test('aa')="+/[a]{3}/g.test('aa')); // flase
console.log("/[a]{3}/.test('aaa')="+/[a]{3}/g.test('aaa')); // true
console.log("/[a]{3}/.test('aaaa')="+/[a]{3}/g.test('aaaa')); // true
```

#### 在正则表达式中表达『或者』

使用符号：|

```javascript
// 目标字符串
var str01 = 'Hello World!';
var str02 = 'I love Java';
// 匹配'World'或'Java'
var reg = /World|Java/g;
console.log("str01.match(reg)[0]="+str01.match(reg)[0]);//World
console.log("str02.match(reg)[0]="+str02.match(reg)[0]);//Java
```

### 常用正则表达式

| 需求     | 正则表达式                                            |
| -------- | ----------------------------------------------------- |
| 用户名   | /^\[a-zA-Z\_][a-zA-Z_\-0-9]{5,9}$/                    |
| 密码     | /^[a-zA-Z0-9_\-\@\#\&\*]{6,12}$/                      |
| 前后空格 | /^\s+\|\s+$/g                                         |
| 电子邮箱 | /^[a-zA-Z0-9_\.-]+@([a-zA-Z0-9-]+[\.]{1})+[a-zA-Z]+$/ |

# 原生Ajax

- Ajax 的全称是 **A**synchronous **J**avascript **A**nd **X**ML（异步JavaScript和XML），是一种web数据交互方式，使用Ajax技术网页应用能够快速地将增量更新呈现在用户界面上，而不需要重载（刷新）整个页面，这使得程序能够更快地回应用户的操作。
- 目的：用来发送异步的请求，然后当服务器给我响应的时候再进行回调操作。
- 好处：提高用户体验；局部刷新：降低服务器负担、减轻浏览器压力、减轻网络带宽压力。

## 使用步骤

1. 客户端发送异步请求，并绑定对结果处理的回调函数
   - \<input type="text" name="uname" onblur="ckUname()"/>
   - 定义ckUname方法：
     - 创建XMLHttpRequest对象
     - XMLHttpRequest对象操作步骤：
       - 调用open(url,"GET",true)设置部分信息
       - 给onreadyStateChange函数属性绑定状态改变时要执行的回调函数
       - 调用send()发送请求
   - 编写回调函数，在回调函数中需要判断XMLHttpRequest对象的状态：readyState(0-4) , status(200)，readyState的状态码含义如下：
     - 0 － （未初始化）还没有调用send()方法
     - 1 － （载入）已调用send()方法，正在发送请求
     - 2 － （载入完成）send()方法执行完成，已经接收到全部响应内容
     - 3 － （交互）正在解析响应内容
     - 4 － （完成）响应内容解析完成，可以在客户端调用了
   
2. 服务器端做校验，然后将校验结果响应给客户端。

3. regist.js代码示例：

      ```javascript
      function $(id){
          return document.getElementById(id);
      }
      
      function preRegist(){
          //用户名不能为空，而且是6~16位数字和字母组成
          var unameReg = /[0-9a-zA-Z]{6,16}/;
          var unameTxt = $("unameTxt");
          var uname = unameTxt.value ;
          var unameSpan = $("unameSpan");
          if(!unameReg.test(uname)){
              unameSpan.style.visibility="visible";
              return false ;
          }else{
              unameSpan.style.visibility="hidden";
          }
      
          //密码的长度至少为8位
          var pwdTxt = $("pwdTxt");
          var pwd = pwdTxt.value ;
          var pwdReg = /[\w]{8,}/; // /^(?![0-9]+$)(?![a-zA-Z]+$)[0-9A-Za-z]{8,}$/;
          var pwdSpan = $("pwdSpan");
          if(!pwdReg.test(pwd)){
              pwdSpan.style.visibility="visible";
              return false ;
          }else{
              pwdSpan.style.visibility="hidden";
          }
      
          //密码两次输入不一致
          var pwd2 = $("pwdTxt2").value ;
          var pwdSpan2 = $("pwdSpan2") ;
          if(pwd2!=pwd){
              pwdSpan2.style.visibility="visible";
              return false ;
          }else{
              pwdSpan2.style.visibility="hidden";
          }
      
          //请输入正确的邮箱格式
          var email = $("emailTxt").value ;
          var emailSpan = $("emailSpan");
          var emailReg = /^[a-zA-Z0-9_\.-]+@([a-zA-Z0-9-]+[\.]{1})+[a-zA-Z]+$/;
          if(!emailReg.test(email)){
              emailSpan.style.visibility="visible";
              return false ;
          }else{
              emailSpan.style.visibility="hidden";
          }
      
          return true ;
      }
      
      //如果想要发送异步请求，我们需要一个关键的对象 XMLHttpRequest
      var xmlHttpRequest ;
      
      function createXMLHttpRequest(){
          if(window.XMLHttpRequest){
              //符合DOM2标准的浏览器 ，xmlHttpRequest的创建方式
              xmlHttpRequest = new XMLHttpRequest() ;
          }else if(window.ActiveXObject){//IE浏览器
              try{
                  xmlHttpRequest = new ActiveXObject("Microsoft.XMLHTTP");
              }catch (e) {
                  xmlHttpRequest = new ActiveXObject("Msxml2.XMLHTTP")
              }
          }
      }
      
      function ckUname(uname){
          createXMLHttpRequest();
          var url = "user.do?operate=ckUname&uname="+uname ;
          xmlHttpRequest.open("GET",url,true);
          //设置回调函数
          xmlHttpRequest.onreadystatechange = ckUnameCB ;
          //发送请求
          xmlHttpRequest.send();
      }
      
      function ckUnameCB(){
          if(xmlHttpRequest.readyState==4 && xmlHttpRequest.status==200){
              //xmlHttpRequest.responseText 表示 服务器端响应给我的文本内容
              //alert(xmlHttpRequest.responseText);
              var responseText = xmlHttpRequest.responseText ;
              // {'uname':'1'}
              //alert(responseText);
              if(responseText=="{'uname':'1'}"){
                  alert("用户名已经被注册！");
              }else{
                  alert("用户名可以注册！");
              }
          }
      }
      ```

# Vue

- vue是一套用javascript实现的用来构建用户界面的渐进式声明式框架
- vue只关注视图层，采用自底向上增量开发的设计
- vue的目标是通过尽可能简单的API实现响应的数据绑定和组合的视图组件
- vue提供了一种简单的操作dom对象的方法，每个vue对象可以通过"el"属性来作为选择器利用css选择器的语法来选择符合条件的标签，然后这些标签就都可以被vue对象操纵了。

## vue的使用

### 引入vue.js

- 作为一个由javascript开发的框架，肯定是要先引入相关的依赖vue.js，然后才能进行使用。
- 首先将vue.js文件放到/web/script中
- 然后可在head标签中进行资源的引入：**\<script language="JavaScript" src="script/vue.js">\</script>**

### 创建vue对象并绑定dom对象

- 引入vue.js后，就可以在之后的javascript代码中使用vue的内容了，通过js创建对象的方式可以创建vue对象。

#### vue对象的参数

- **"el"**：**参数类型为String**，这个参数**表示与当前vue对象绑定的标签**，可以用类似css选择器语法的方式来进行指定，例如绑定id为div0的标签：**"el":"#div0"**

  

- **data**：**参数类型为Object**，这个参数**表示当前vue对象提供的数据**，后面可以通过特定方式将这些数据绑定到标签的属性或内容上。

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
      <script language="JavaScript" src="script/vue.js"></script>
      <script language="JavaScript">
          window.onload=function(){
              var vue = new Vue({
                  "el":"#div0",
                  data:{
                      msg:"hello!!!",
                      uname:"鸠摩智"
                  }
              });
          }
      </script>
  </head>
  <body>
      <div id="div0">
          <span>{{msg}}</span>
          <!-- v-bind:value表示绑定value属性 , v-bind可以省略，也就是 :value -->
          <!--<input type="text" v-bind:value="uname"/>-->
          <input type="text" :value="uname"/>
      </div>
  </body>
  </html>
  ```

  

- **method**：**参数类型为Object**，这个参数**表示当前vue对象提供的方法**，后面可以通过特定方式将这些方法绑定到标签的属性上。

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
      <script language="JavaScript" src="script/vue.js"></script>
      <script language="JavaScript">
          window.onload=function(){
              var vue = new Vue({
                  "el":"#div0",
                  data:{
                      msg:"hello world!"
                  },
                  methods:{
                      myReverse:function(){
                          this.msg = this.msg.split("").reverse().join("");
                      }
                  }
              });
          }
      </script>
  </head>
  <body>
      <div id="div0">
          <span>{{msg}}</span><br/>
          <!-- v-on:click 表示绑定点击事件 -->
          <!-- v-on可以省略，变成 @click -->
          <!--<input type="button" value="反转" v-on:click="myReverse"/>-->
          <input type="button" value="反转" @click="myReverse"/>
      </div>
  </body>
  </html>
  ```

- **watch**：**参数类型为Object**，这个参数**表示当前vue对象提供的对属性进行侦听的方法**，如果被侦听的属性发生改动，那么后面绑定的方法就会被自动调用。

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
      <script language="JavaScript" src="script/vue.js"></script>
      <script language="JavaScript">
          window.onload=function(){
              var vue = new Vue({
                  "el":"#div0",
                  data:{
                      num1:1,
                      num2:2,
                      num3:0
                  },
                  watch:{
                      //侦听属性num1和num2
                      //当num1的值有改动时，那么需要调用后面定义的方法 , newValue指的是num1的新值
                      num1:function(newValue){
                          this.num3 = parseInt(newValue) + parseInt(this.num2);
                      },
                      num2:function(newValue){
                          this.num3 = parseInt(this.num1) + parseInt(newValue) ;
                      }
                  }
              });
          }
      </script>
  </head>
  <body>
      <div id="div0">
          <input type="text" v-model="num1" size="2"/>
          +
          <input type="text" v-model="num2" size="2"/>
          =
          <span>{{num3}}</span>
      </div>
  </body>
  </html>
  ```

### 在vue对象的参数中放入内容完善vue对象

- 根据上面写到过的对vue对象参数的解释，在vue对象的参数中放入内容，将vue对象完善。

### 将vue对象参数中的内容绑定到标签中

#### 相关语法

- **{{vue对象中数据名}}** ：相当于innerText，将vue对应的数据绑定到innerText中。

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
      <script language="JavaScript" src="script/vue.js"></script>
      <script language="JavaScript">
          window.onload=function(){
              var vue = new Vue({
                  "el":"#div0",
                  data:{
                      msg:"hello!!!",
                      uname:"鸠摩智"
                  }
              });
          }
      </script>
  </head>
  <body>
      <div id="div0">
          <span>{{msg}}</span>
          <!-- v-bind:value表示绑定value属性 , v-bind可以省略，也就是 :value -->
          <!--<input type="text" v-bind:value="uname"/>-->
          <input type="text" :value="uname"/>
      </div>
  </body>
  </html>
  ```

- **v-bind:标签属性="vue对象中数据名"**：将vue对象中的数据**单向绑定**到指定的标签属性中，vue对象中的数据发生改变时，对应的标签属性值改变，对应的标签属性值改变时，vue对象中的数据不变，可以简写为**:标签属性="vue对象中数据名"**

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
      <script language="JavaScript" src="script/vue.js"></script>
      <script language="JavaScript">
          window.onload=function(){
              var vue = new Vue({
                  "el":"#div0",
                  data:{
                      msg:"hello!!!",
                      uname:"鸠摩智"
                  }
              });
          }
      </script>
  </head>
  <body>
      <div id="div0">
          <span>{{msg}}</span>
          <!-- v-bind:value表示绑定value属性 , v-bind可以省略，也就是 :value -->
          <!--<input type="text" v-bind:value="uname"/>-->
          <input type="text" :value="uname"/>
      </div>
  </body>
  </html>
  ```

- **v-model:标签属性="vue对象中数据名"**：将vue对象中的数据与指定的标签属性进行**双向绑定**，任何一方数据发生改变，与之绑定的另一方的数据也会发生改变。**v-model:value="vue对象中数据名"可以简写为v-model="vue对象中数据名"**。

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
      <script language="JavaScript" src="script/vue.js"></script>
      <script language="JavaScript">
          window.onload=function(){
              var vue = new Vue({
                  "el":"#div0",
                  data:{
                      msg:"hello!!!"
                  }
              });
          }
      </script>
  </head>
  <body>
      <div id="div0">
          <span>{{msg}}</span><br/>
          <!--
              v-model指的是双向绑定，
              也就是说之前的v-bind是通过msg这个变量的值来控制input输入框
              现在 v-model 不仅msg来控制input输入框，反过来，input输入框的内容也会改变msg的值
           -->
          <!--<input type="text" v-model:value="msg"/>-->
          <!-- v-model:value 中 :value可以省略，直接写成v-model -->
          <!-- trim可以去除首尾空格 -->
          <input type="text" v-model.trim="msg"/>
      </div>
  </body>
  </html>
  ```

- **v-if="条件"、v-else="条件"、v-show="条件"**：v-if 和 v-else成对使用，之间不可以插入其他元素节点，当后面的条件为true时，有v-if的标签显示，当后面的条件为false时，有v-else的标签显示，它们是通过是否将绑定的标签当作代码进行渲染来控制显示的，也就是说，如果不显示，则代码中不出现相关的内容。**v-show是通过样式表display来控制节点是否显示**，条件为true则显示，条件为false则不显示，无论条件为何值，对应标签都会被当作代码来进行渲染。

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
      <script language="JavaScript" src="script/vue.js"></script>
      <script language="JavaScript">
          window.onload=function(){
              var vue = new Vue({
                  "el":"#div0",
                  data:{
                      num:2
                  }
              });
          }
      </script>
  </head>
  <body>
      <div id="div0">
          <input type="text" v-model="num"/>
  
          <!-- v-if和v-else之间不可以插入其他节点 -->
          <!--<div v-if="num%2==0" style="width:200px;height:200px;background-color: chartreuse;">&nbsp;</div>-->
          <!--<br/>-->
          <!--<div v-else="num%2==0" style="width:200px;height:200px;background-color: coral">&nbsp;</div>-->
  
  
          <!-- v-show -->
          <!-- v-show是通过display属性来控制这个div是否显示 -->
          <div v-show="num%2==0" style="width:200px;height:200px;background-color:blueviolet;">&nbsp;</div>
      </div>
  </body>
  </html>
  ```

- **v-for="item in list"**：可以用这个语句实现迭代，每次迭代的元素用in前面的变量表示，被遍历的列表放在in后面。

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
      <script language="JavaScript" src="script/vue.js"></script>
      <script language="JavaScript">
          window.onload=function(){
              var vue = new Vue({
                  "el":"#div0",
                  data:{
                      fruitList:[
                          {fname:"苹果",price:5,fcount:100,remark:"苹果很好吃"},
                          {fname:"菠萝",price:3,fcount:120,remark:"菠萝很好吃"},
                          {fname:"香蕉",price:4,fcount:50,remark:"香蕉很好吃"},
                          {fname:"西瓜",price:6,fcount:100,remark:"西瓜很好吃"}
                      ]
                  }
              });
          }
      </script>
  </head>
  <body>
      <div id="div0">
          <table border="1" width="400" cellpadding="4" cellspacing="0">
              <tr>
                  <th>名称</th>
                  <th>单价</th>
                  <th>库存</th>
                  <th>备注</th>
              </tr>
              <!-- v-for表示迭代 -->
              <tr align="center" v-for="fruit in fruitList">
                  <td>{{fruit.fname}}</td>
                  <td>{{fruit.price}}</td>
                  <td>{{fruit.fcount}}</td>
                  <td>{{fruit.remark}}</td>
              </tr>
          </table>
      </div>
  </body>
  </html>
  ```

- **v-on:事件名="vue对象中方法名"**：为指定事件绑定相应的方法，可以简写为**@事件名="vue对象中方法名"**。

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
      <script language="JavaScript" src="script/vue.js"></script>
      <script language="JavaScript">
          window.onload=function(){
              var vue = new Vue({
                  "el":"#div0",
                  data:{
                      msg:"hello world!"
                  },
                  methods:{
                      myReverse:function(){
                          this.msg = this.msg.split("").reverse().join("");
                      }
                  }
              });
          }
      </script>
  </head>
  <body>
      <div id="div0">
          <span>{{msg}}</span><br/>
          <!-- v-on:click 表示绑定点击事件 -->
          <!-- v-on可以省略，变成 @click -->
          <!--<input type="button" value="反转" v-on:click="myReverse"/>-->
          <input type="button" value="反转" @click="myReverse"/>
      </div>
  </body>
  </html>
  ```

## vue的生命周期

![img](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/20210324205213585.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script language="JavaScript" src="script/vue.js"></script>
    <script language="JavaScript">
        window.onload=function(){
            var vue = new Vue({
                "el":"#div0",
                data:{
                    msg:1
                },
                methods:{
                    changeMsg:function(){
                        this.msg = this.msg + 1 ;
                    }

                },
                /*vue对象创建之前*/
                beforeCreate:function(){
                    console.log("beforeCreate:vue对象创建之前---------------");
                    console.log("msg:"+this.msg);
                },
                /*vue对象创建之后*/
                created:function(){
                    console.log("created:vue对象创建之后---------------");
                    console.log("msg:"+this.msg);
                },
                /*数据装载之前，数据装载是指将vue对象的数据装载到html的和vue绑定的标签中*/
                beforeMount:function(){
                    console.log("beforeMount:数据装载之前---------------");
                    console.log("span:"+document.getElementById("span").innerText);
                },
                /*数据装载之后*/
                mounted:function(){
                    console.log("mounted:数据装载之后---------------");
                    console.log("span:"+document.getElementById("span").innerText);
                },
                beforeUpdate:function(){
                    console.log("beforeUpdate:数据更新之前---------------");
                    console.log("msg:"+this.msg);
                    console.log("span:"+document.getElementById("span").innerText);
                },
                updated:function(){
                    console.log("Updated:数据更新之后---------------");
                    console.log("msg:"+this.msg);
                    console.log("span:"+document.getElementById("span").innerText);
                }
            });
        }
    </script>
</head>
<body>
    <div id="div0">
        <span id="span">{{msg}}</span><br/>
        <input type="button" value="改变msg的值" @click="changeMsg"/>
    </div>
</body>
</html>
```

# Axios

- Axios是Ajax的一个框架，可以用来简化Ajax操作。

![image-20220730234239267](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220730234239267.png)

## 使用Axios

### 引入Axios

- 和vue一样，Axios是由js写成的，所以在html中使用之前要先将Axios.js引入head标签中：**\<script language="JavaScript" src="script/axios.min.js">\</script>**

### 客户端向服务器端异步发送普通参数值

- 基本格式：**axios().then().catch()**

- 客户端示例代码：

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>01.演示Axios发送普通的参数值给服务器端</title>
      <script language="JavaScript" src="script/vue.js"></script>
      <script language="JavaScript" src="script/axios.min.js"></script>
      <script language="JavaScript">
          window.onload=function(){
              var vue = new Vue({
                  "el":"#div0",
                  data:{
                      uname:"lina",
                      pwd:"ok"
                  },
                  methods:{
                      axios01:function(){
                          axios({
                              method:"POST",
                              url:"axios01.do",
                              params:{//发送普通格式数据的时候这里是设置params参数，发送json格式的数据时，这里是设置data参数。
                                  uname:vue.uname,
                                  pwd:vue.pwd//这地方用this访问不到，具体什么原因还不是很清楚
                              }
                          })
                              .then(function (value) {//成功响应时执行的回调        value.data可以获取到服务器响应内容
                                  console.log(value);
                              })
                              .catch(function (reason) {//有异常时执行的回调          reason.response.data可以获取到响应的内容
                                  console.log(reason);
                              });
                      }
                  }
              });
          }
      </script>
  </head>
  <body>
      <div id="div0">
          uname:<input type="text" v-model="uname"/><br/>
          pwd:<input type="text" v-model="pwd"/><br/>
          <input type="button" @click="axios01" value="发送一个带普通请求参数值的异步请求"/>
      </div>
  </body>
  </html>
  ```

- 服务端示例代码：

  ```java
  @WebServlet("/axios01.do")
  public class Axios01Servlet extends HttpServlet {
      @Override
      protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          request.setCharacterEncoding("utf-8");
  
          String uname = request.getParameter("uname");
          String pwd = request.getParameter("pwd");
  
          System.out.println("uname = " + uname);
          System.out.println("pwd = " + pwd);
  
          response.setCharacterEncoding("utf-8");
          response.setContentType("text/html;charset=utf-8");//注意普通格式的数据的ContentType和json格式的数据的ContentType不同
          PrintWriter out = response.getWriter();
          out.write(uname+"_"+pwd);
  
          throw new NullPointerException("这里故意抛出一个空指针异常....");
      }
  }
  ```

  

### 客户端向服务器发送JSON格式的数据

- 普通的数据可以被直接解析，可是对于空间的利用率缺不理想，包括xml格式的数据，格式非常清晰，但是非常占空间，为了**提高空间利用率和节约网络带宽**，我们可以使用JSON风格的数据来进行传输。

- 我们要先将发送方的对象转换为json格式后，发送给接收方，然后接收方要将json数据解析为接收方的对象。

- 由于发送的数据格式的改动，**客户端中的axios中的params参数要改成data参数**，同时，**服务器中也不能直接使用getParameter()获取参数**了，而是先用流读下来，然后再解析。

- 客户端示例代码：

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>02.演示Axios发送JSON格式的参数值给服务器端</title>
      <script language="JavaScript" src="script/vue.js"></script>
      <script language="JavaScript" src="script/axios.min.js"></script>
      <script language="JavaScript">
          window.onload=function(){
              var vue = new Vue({
                  "el":"#div0",
                  data:{
                      uname:"lina",
                      pwd:"ok"
                  },
                  methods:{
                      axios02:function(){
                          axios({
                              method:"POST",
                              url:"axios02.do",
                              data:{
                                  uname:vue.uname,
                                  pwd:vue.pwd
                              }
                          })
                              .then(function (value) {
                                  console.log(value);
                              })
                              .catch(function (reason) {
                                  console.log(reason);
                              });
                      }
                  }
              });
          }
      </script>
  </head>
  <body>
      <div id="div0">
          uname:<input type="text" v-model="uname"/><br/>
          pwd:<input type="text" v-model="pwd"/><br/>
          <input type="button" @click="axios02" value="发送JSON格式的参数值的异步请求"/>
      </div>
  </body>
  </html>

- 服务端示例代码：

  ```java
  @WebServlet("/axios02.do")
  public class Axios02Servlet extends HttpServlet {
      @Override
      protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
  
          StringBuffer stringBuffer = new StringBuffer("");
          BufferedReader bufferedReader = request.getReader();
          String str = null ;
          while((str=bufferedReader.readLine())!=null){
              stringBuffer.append(str);
          }
          str = stringBuffer.toString() ;
  
          //已知 String
          //需要转化成 Java Object
  
          Gson gson = new Gson();
          //Gson有两个API
          //1.fromJson(string,T) 将字符串转化成java object
          //2.toJson(java Object) 将java object转化成json字符串，这样才能响应给客户端
  
          User user = gson.fromJson(str, User.class);
  
          System.out.println(user);
      }
  }
  ```

  

## json格式的数据与js object和java object之间的转换

### js object转json

- **string JSON.stringify(object)**   //object->string

### json转js object

- **object JSON.parse(string)**     //string->object

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>03.演示Axios发送异步请求给服务器端，服务器响应json格式的数据给客户端</title>
    <script language="JavaScript" src="script/vue.js"></script>
    <script language="JavaScript" src="script/axios.min.js"></script>
    <script language="JavaScript">
        window.onload=function(){
            var vue = new Vue({
                "el":"#div0",
                data:{
                    uname:"lina",
                    pwd:"ok"
                },
                methods:{
                    axios03:function(){
                        axios({
                            method:"POST",
                            url:"axios03.do",
                            data:{
                                uname:vue.uname,
                                pwd:vue.pwd
                            }
                        })
                            .then(function (value) {
                                var data = value.data;
                                // data对应的数据：
                                // {uname:"鸠摩智",pwd:"ok"}
                                vue.uname=data.uname;
                                vue.pwd=data.pwd;

                                //此处value中的data返回的是 js object，因此可以直接点出属性
                                //如果我们获取的是一个字符串：  "{uname:\"鸠摩智\",pwd:\"ok\"}"

                                //js语言中 也有字符串和js对象之间互转的API
                                //string JSON.stringify(object)     object->string
                                //object JSON.parse(string)         string->object
                            })
                            .catch(function (reason) {
                                console.log(reason);
                            });
                    }
                }
            });
        }
    </script>
</head>
<body>
    <div id="div0">
        uname:<input type="text" v-model="uname"/><br/>
        pwd:<input type="text" v-model="pwd"/><br/>
        <input type="button" @click="axios03" value="服务器响应json格式的数据给客户端"/>
    </div>
</body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>04.JS中的字符串和Object之间互转的API</title>
    <script language="JavaScript">
        function hello01(){
            /*
            //1. js string - > js object
            var str = "{\"uname\":\"lina\",\"age\":20}";
            var user = JSON.parse(str);
            alert(typeof user);
            alert(user.uname+"_"+user.age);
            */

            //2. js object -> js string
            var user = {"uname":"lina","age":99};
            alert(typeof user);
            var userStr = JSON.stringify(user);
            alert(typeof userStr);
            alert(userStr);
        }
    </script>
</head>
<body>
    <div id="div0">
        <input type="button" value="确定" onclick="hello01()"/>
    </div>
</body>
</html>
```

### json转java object

- 首先new一个Gson对象：**Gson gson = new Gson();**
- 使用Gson中的API：**gson.fromJson(string,T)** //将字符串转化成java object

### java object转json

- 首先new一个Gson对象：**Gson gson = new Gson();**
- 使用Gson中的API：**gson.toJson(java Object)** //将java object转化成json字符串，这样才能响应给客户端

```java
@WebServlet("/axios03.do")
public class Axios03Servlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        StringBuffer stringBuffer = new StringBuffer("");
        BufferedReader bufferedReader = request.getReader();
        String str = null ;
        while((str=bufferedReader.readLine())!=null){
            stringBuffer.append(str);
        }
        str = stringBuffer.toString() ;

        //已知 String
        //需要转化成 Java Object

        Gson gson = new Gson();
        //Gson有两个API
        //1.fromJson(string,T) 将字符串转化成java object
        //2.toJson(java Object) 将java object转化成json字符串，这样才能响应给客户端

        User user = gson.fromJson(str, User.class);
        user.setUname("鸠摩智");
        user.setPwd("123456");

        //假设user是从数据库查询出来的，现在需要将其转化成json格式的字符串，然后响应给客户端
        String userJsonStr = gson.toJson(user);
        response.setCharacterEncoding("UTF-8");
        //MIME-TYPE
        response.setContentType("application/json;charset=utf-8");//做出json格式的响应时要注意设置ContentType
        response.getWriter().write(userJsonStr);//将json数据写入response
    }
}
```

