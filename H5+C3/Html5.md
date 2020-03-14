# 前端第一天

### 五大浏览器和内核

谷歌chochrome (blink)

火狐Firefox （Gecko）

苹果Safari（webkit）

欧朋  （国外）

IE以及Edge(Trident)

### HTML骨架：

```html
<html>
	<head>
		<title></title>
	</head>
	<body>
    </body>
</html>
```

### HTML标签

HTML标签分为单标签和双标签，单标签为少数，为功能性标签

### 字体的几种格式化：

前者有强调语义，能够为搜索引擎搜索时提高权重，推荐使用

```html
<strong></strong>或者<b></b>   字体加粗
<em>或者<i>                    字体倾斜
<del>或者<S>                   字体加删除线
<ins>或者<U>                   字体下划线

```

### 开发软件 VS Code的常用快捷键

ctrl+c/v     复制粘贴

ctrl+/       注释代码

alt+B        用浏览器打开

alt+z       代码过长时，适应开发界面

shift+alt+F    格式化代码

shift+alt+鼠标左键    多行编辑

ctrl + F    搜索关键字

### 相对路径

1.同级目录：在同一级目录时直接输入文件名即可

2.上一级目录：. . /

3.下一级目录： 文件所在的文件夹名  /  文件名

### 注*块级元素的特例

p和h1 h2等文字类块级元素不能包裹div

行内元素只能容纳文本和其他行内元素，但是a特殊，a中可以放块级元素（ps:div）,而且a中不能再包裹a,a中包裹a标签则无意义。

1.链接里不能再放链接

2.链接中可以放块级元素。



# 前端第二天



### 列表的分类

1. 有序列表(ol)

2. 无序列表(ul)
3. 自定义列表(dl)

```
<dl>
		<dt>列表标题</dt>
		<dd>列表标题的解释说明</dd>
		<dd>列表标题的解释说明</dd>
		<dd>列表标题的解释说明</dd>
		<dd>列表标题的解释说明</dd>
	</dl>
特点：可以针对一个列表标题充分解释 特定情况下使用
```

### 表格标签(table)

```
<table>
		<tr>
			<td>单元格</td>
			<td>单元格</td>
			<td>单元格</td>
		</tr>
</table>
```

#### 表格属性

```
width  表格的宽度 （了解）
height 表格的高度 （了解）
border 表格的边框 （了解）
align  表格的对齐方式 （了解）
cellspacing 单元格与单元格的间距
cellpadding	单元格与单元格内容的间距
```

#### 表格结构化

```
表头标签
<thead>
		<tr>
			<th>姓名</th>
			<th>年纪</th>
			<th>性别</th>
		</tr>
</thead>
<tbody>
		<tr>
			<td>小明</td>
			<td>18</td>
			<td>男</td>
		</tr>
</tbody>
```

#### 合并单元格

跨行合并 rowspan 上下合并  将rowspan写在上面的单元格上  
跨列合并 colspan 左右合并  将colspan写在左边的单元格上

### 特殊字符

在一些情况下，我们需要在页面上显示一些特殊的标识的时候 我们就需要用到字符

< : 小于号 &lt    >  : 大与号 &gt   都面都需要加分号



# H5新增的标签

```
header,nav,section,footer,aside,article  

这些新增的标签不会带来任何视觉效果的改变，它的作用仅是增加了语义性

header 表示header里面包裹的东西是网站的头部区域

nav 表示nav里面包裹的东西是网站的导航

section 表示里面包裹的东西是网页的某一个模块

footet 表示footer标签里面包裹的东西是网页的页脚

aside 表示aside标签里面包裹的东西是网页的侧边栏

article 表示article标签里面包裹的东西是网页的文章页

详细请查阅文档
```

### 多媒体标签

#### 视频标签(video)

网页中插入视频有两种方法

1. 没有兼容性的 将视频文件上传到第三方网站获取其分享代码放到自己的页面中即可

   - 优点：没有兼容性
   - 缺点：有广告植入

2. 使用H5新增的video方法  

   ```
   <video src="视频路径">
   </video>
   ```

   - 优点：没有广告
   - 缺点：有兼容性，一般运用在手机端

video标签的常用属性

1. autoplay  自动播放(已经被谷歌舍弃)
2. controls  播放控件
   . loop 	循环播放

video的格式支持
ogg,MP4,webm 不同的浏览器支持的格式不一样，所以出现了一种兼容写法:前提是准备三种格式的视频文件

```
<video autoplay>
	<source src="视频1.ogg">
	<source src="视频1.mp4">
	<source src="视频1.webm">
	<a href="#">你的浏览器不支持video，点击升级吧</a>
</video>
```

浏览器会从上到下依次去读，在这个过程中，只要读到自己识别的视频文件就直接播放这个视频文件，并且不会再往后继续读取
实测：目前的主流浏览器对Mp4的支持都比较好！！

#### 音频标签(audio)

音频的使用和视频的使用基本一致

```
<audio>
	<source src="音频1.ogg">
	<source src="音频1.mp3">
	<source src="音频1.wav">
	<a href="#">你的浏览器不支持audio，点击升级吧</a>
</audio>
```

### 新增表单标签

#### 新增表单属性

1. placeholder 占位文本 (记忆)  就是表单框中的提示文本 

2. autofocus   自动获取焦点

3. autocomplete  自动补全

4. required    自动验证表单   验证表单不为空

   

# 前端第三天

### 表单标签(input)

```
<input type="">  type 表单类型
	type的取值：
	text 单行文本输入框
	password 密码框
	radio 单选框（在多个里面选择一个） 单选框要生效必须具备name属性 并且同一种类型的单选框的name取值必           须一样
	checkbox 复选框（在多个里面选择某几个）
	button 普通按钮
	file 用户上传控件
	submit 提交按钮
```

### 其他表单

select 下拉菜单      option为下拉选项

 textarea   文本域

​     resize属性可以消除右下角的

### label标签:

​        作用: 将文字和表单做一个绑定  点击了文字相当于点击了表单

使用方式:

1. 直接将表单和文本包裹在一个label标签即可
2. 使用label的for属性  绑定一个input的id值  (即使没有包裹在一个label也是可以的)

### 表单的提交三要素:

1. 表单域
2. 需要提交的表单要有name属性才可以
3. submit提交按钮

### 按钮的选项默认值属性	

```
radio和checkbox 默认选中项  checked
select框的默认选中项 selected
label标签的使用
```

### 表单域(form)	

```
<form action=""></form>

action 提交的后台地址 
```

### HTML骨架含义

```
<head>
  <!-- 设定字符集: 告诉浏览器以"UTF-8"字符集去解析页面 -->
  <meta charset="UTF-8">
  <!-- 视口标签: 针对的是移动端 -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <!-- 让IE默认以edge内核渲染 -->
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
```

