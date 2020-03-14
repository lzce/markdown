# Web API 第一天

JavaScript分三个部分:
* ECMAScript标准:JS的基本的语法
* DOM:Document Object Model --->文档对象模型----操作页面的元素
* BOM:Browser Object Model----->浏览器对象模型---操作的是浏览器

## 获取元素的方法

### null对象

> `null`也是一种对象 , 但是它没有任何属性, 不能对他进行任何操作 , 当获取对象时, 由于各种原因获取不到时, 浏览器就会把null对象返回

### 按id方式获取

> 当页面中的 id 重复时, 浏览器只能拿到, 页面中第一次出现的id , 后面的

**document . getElementById(" ") ;**

```js
<input type="button" value="显示效果" id="btn"/>
<script>
  //最终极的点击按钮弹出对话框的代码
  document.getElementById("btn").onclick=function () {
      alert("哈哈,我又变帅了");
  };
</script>
```

### 按标签名获取元素

**document . getElementsByTagName( " " ) ;**

使用这种方法获取的元素,返回的是数组,有长度,可以进行遍历

> 不管要找的元素存在不存在, 都会返回一个伪数组 , 不存在则 返回一个空数组

```javascript
 //根据标签的名字获取图片标签,分别注册点击事件
  var imgObjs=document.getElementsByTagName("img");
  //循环遍历数组,获取每个图片标签,注册点击事件,添加事件处理函数
  for(var i=0;i<imgObjs.length;i++){
    imgObjs[i].onclick=function () {
      alert("被点击了");
    };
  }jav
```

### 按Name属性获取元素

**document . getElementsByName( " " ) ;**   获取的也是一个伪数组

```javascript
my$("btn").onclick=function () {
  //通过name属性值获取元素-------表单的标签
  var inputs=document.getElementsByName("name1");
  for(var i=0;i<inputs.length;i++){
    inputs[i].value="我很好";
  }
};
```

### 按类样式获取元素

**document.getElementsClassName (" ") ;    获取的也是一个伪数组**

```javascript
my$("btn").onclick = function () {
  //根据类样式的名字来获取元素
  var objs = document.getElementsByClassName("cls");
  for (var i = 0; i < objs.length; i++) {
    //设置每个元素的背景颜色
    objs[i].style.backgroundColor = "red";
  }
};
```



### 根据选择器的方式获取元素

> **参数是css选择器, css可以写的,都可以作为里面的参数**

**document . querySelector( " 选择器的名字") ;**   返回来的是一个对象

> **即使有多个，也只会的返回第一个找到的对象 ， 对象不存在就返回null**

```javascript
var btnObj= document.querySelector("#btn");
 btnObj.onclick=function () {
     alert("哈哈,我又变帅了");
 };
```

**document . querySelectorAll( " 选择器的名字") ;**    返回来的是一个伪数组

```javascript
var btnObj= document.querySelector(".cls");
 btnObj.onclick=function () {
     alert("哈哈,我又变帅了");
 };
```



## 元素的类样式操作(className)

对象 . className= 值

对象 . style= 值

需要在style中写好对应的类样式,才能通过className给标签增加或者修改类样式

```javascript
<input type="button" value="隐藏" id="btn"/>
<div id="dv"></div>
<script src="common.js"></script>
<script>
  //点击按钮,通过类样式的方式设置div的显示和隐藏
  my$("btn").onclick = function () {
    // console.log(my$("dv").className);

    //判断的是div是否应用了类样式
    if (my$("dv").className != "cls") {
      //现在是显示的,应该隐藏
      my$("dv").className = "cls";
      this.value = "显示";
    } else {
      //隐藏的状态----立刻显示
      my$("dv").className = "";
      this.value = "隐藏";
    }
  };
```





## this关键字的使用

在某个元素的事件中, 可以用this代替的当前这个元素对象

可以实现点击事件的共享, this都指向当前的事件对象

```js
var btnObj = document.getElementById("btn");
btnObj.onclick = function () {//  此时的this就代表btn.Obj
   //修改按钮的value属性
   this.value = "我是按钮,谁咬我,我就咬谁";
   this.type = "text";
   this.id = "btn2";
};
```

事件是异步API, 再循环中, 给元素遍历注册事件, 循环不会等点击事件, 会先执行循环 

> 注: 任何函数没有写返回值, 默认返回 `undefined`

## js控制元素的样式

> js控制的是元素的行内样式

```js
//当想要设置元素的显示和隐藏, 但是又不想影响到元素的其他样式属性, 但是元素的其他样式属性, 又依赖于它的显示和隐藏属性 , 例如 
div {
    display:flex;
    justify-content: center;
    align-items:center;
}
//对下下面两个延时来说, 是依赖于flex , 当改变display时, 其他的依赖样式就会被隐藏 ,
//此时我们想我干掉元素的行内样式的display = '';
var div = docuemnt.getElementById('div')
div.style.dispaly = '' //  清空行内样式, 使用css样式
```



## 排他功能

```javascript

<input type="button" value="没怀孕"/>
<input type="button" value="没怀孕"/>
<input type="button" value="没怀孕"/>
<input type="button" value="没怀孕"/>
<input type="button" value="没怀孕"/>
<input type="button" value="没怀孕"/>

<script>
  //获取所有的按钮,分别注册点击事件
  var btnObjs = document.getElementsByTagName("input");
  //循环遍历所有的按钮
  for (var i = 0; i < btnObjs.length; i++) {
    //为每个按钮都要注册点击事件
    btnObjs[i].onclick = function () {
      //把所有的按钮的value值设置为默认的值:没怀孕
      for (var j = 0; j < btnObjs.length; j++) {
        btnObjs[j].value = "没怀孕";
      }
      //当前被点击的按钮设置为:怀孕了
      this.value = "怀孕了";
    };
  }
```

## 特殊的表单属性的取值

**checked**     **selected    readonly(只读)    disabled()只读,不可修改**

```
my$("ck1").checked=true; //checked后面的值非空字符串即为true

<textarea name="" id="tt" cols="30" rows="10" readonly="readonly" >  
readonly====>只读 , 用户不可以修改
```





# Web API 第二天

## 阻止a链接跳转

在点击事件后加上   return false:

```javascript
<a href="images/1.jpg" id="ak"><img src="images/1-small.jpg" alt=""></a>
<img src="" alt="" id="big">
<script src="common.js"></script>
<script>
  //点击小图,下面显示大图
  //点击超链接
  my$("ak").onclick=function () {
    my$("big").src=this.href;
    return false;
  };
```



## 阻止浏览器的默认行为

- e.preventDefault   ====> 阻止a链接跳转
- e. stopPropagation （）可以住址阻止事件冒泡
- return false    两个都能阻止

在元素的事件处理函数中调用`e.stopPropagation()`  将不会继续向外冒泡

默认情况下 , 目标阶段执行目标事件, 然后冒泡执行其父元素身上的事件

> 当父元素绑定事件addEventlistener('clcik' , function() {}, trur)

也就是说, 父元素上的事件, 默认在冒泡阶段执行, 当参数为 `true`时, 会在捕获阶段执行,冒泡不执行 

## 页面中直接获取的元素

- body : document . body
- head : docuement . head
- html : document . documentElement
- title : docuement . title ======> 获取的不是对象 , 是title内容, 是字符串 , 可设置title



## 案例:美女相册

```javascript
<script>
  //点击a标签,把a标签中的href的属性值给id为image的src属性
  //把a的title属性的值给id为des的p标签赋值
  //从ul中标签获取获取所有的a标签
  var aObjs=my$("imagegallery").getElementsByTagName("a");
  //循环遍历所有的a标签
  for(var i=0;i<aObjs.length;i++){
    //为每个a标签注册点击事件
    aObjs[i].onclick=function () {
      //为id为image的标签的src赋值
      my$("image").src=this.href;
      //为p标签赋值
      my$("des").innerText=this.title;
      //阻止超链接默认的跳转
      return false;
    };
  }
```



## 对象事件

### 事件三要素

- 事件源   -------> 事发主体
- 事件类型------------> `click` , `mouseover`
- 事件处理函数

### 点击事件

对象 . onclick=function () {};

```javascript
my$("btn").onclick = function () {
  //获取所有的li标签
  var list = my$("uu").getElementsByTagName("li");
  for (var i = 0; i < list.length; i++) {
    list[i].style.backgroundColor = i % 2 == 0 ? "red" : "yellow";
  }
};
```

### 鼠标经过事件

对象 . onmouseover 

### 鼠标离开 

对象 . onmouseout 

```javascript
//鼠标进入和鼠标离开两个事件
//获取所有的li标签
var list = document.getElementsByTagName("li");
for (var i = 0; i < list.length; i++) {
  //为li注册鼠标进入事件
  list[i].onmouseover = function () {
    this.style.backgroundColor = "yellow";
  };
  //为li注册鼠标离开事件
  list[i].onmouseout = function () {
    //恢复到这个标签默认的颜色
    this.style.backgroundColor = "";
  };
}
```

### 焦点事件

```javascript
对象 . onfocus = function () {
    
};
```

### 失去焦点事件

```javascript
对象 . onblur = function () {
    
};
```

### 键盘抬起事件

```
对象 . onkeyup = function () {
    
};
```

### 键盘按下事件

```js
#不区分大小写, 都是大写的数字码
对象 . onkeydown = function () {};
```

### 键盘按下时触发

```js
#和onkeydown 区别是区分大小写, 键盘输入的 Q 和 q  获取的数字码不同
# Q = 81  q = 113
对象.onkeypress = function () {}
```

### 鼠标双击事件

```js
对象.ondblclick = function () {}
```

### 鼠标按下事件

````js
对象.mousedown = function () {}
````

### 鼠标松开

```js
对象.mouseup = function () {}
```



### 元素移动事件

```
document.onmousemove =function () {};
```

### 监听元素滚动条滚动事件

```
元素.onscroll=function () {};
```



### 模拟搜索框案例

```javascript
<input type="text" value="请输入搜索内容" id="txt"/>
<script src="common.js"></script>
<script>
  //获取文本框
  //注册获取焦点的事件
  my$("txt").onfocus = function () {
    //判断文本框的内容是不是默认的内容
    if (this.value == "请输入搜索内容") {
      this.value = "";//清空文本框
      this.style.color = "black";
    }
  };

  //注册失去焦点的事件
  my$("txt").onblur = function () {
//    if (this.value == "") {
//      this.value = "请输入搜索内容";
//      this.style.color = "gray";
//    }

    if (this.value.length == 0) {
      this.value = "请输入搜索内容";
      this.style.color = "gray";
    }
  };
</script>
```

案例: 验证密码长度 (失去焦点事件)

```javascript
<input type="text" value="" id="txt"/>

//获取文本框
my$("txt").onblur=function () {
  //判断密码的长度
  if(this.value.length>=6&&this.value.length<=10){
    this.style.backgroundColor="red";
  }else{
    this.style.backgroundColor="green";
  }
};
```

## innerText和textContent

```handlebars
设置标签中的文本内容,应该使用textContent属性,谷歌,火狐支持,IE8不支持

设置标签中的文本内容,应该使用innerText属性,谷歌,火狐,IE8都支持
```

## 兼容代码

```javascript
//设置任意的标签中间的任意文本内容
function setInnerText(element,text) {
  //判断浏览器是否支持这个属性
  if(typeof element.textContent =="undefined"){//不支持
    element.innerText=text;
  }else{//支持这个属性
    element.textContent=text;
  }
}

//获取任意标签中间的文本内容
  function getInnerText(element) {
    if(typeof element.textContent=="undefined"){
     return element.innerText;
    }else{
      return element.textContent;
    }
  }
  
   //测试
  my$("btn").onclick=function () {
    //console.log(getInnerText(my$("dv")));
    setInnerText(my$("dv"),"哈哈,我又变帅了");
  };
```

## innerText和innerHTML的区别

```javascript
//总结:如果使用innerText主要是设置文本的,设置标签内容,是没有标签的效果的, 标签不会被解析

//总结:innerHTML也可以设置文本内容

//总结:innerHTML主要的作用是在标签中设置新的html标签内容,是有标签效果的, 可以解析标签

//总结:想要设置标签内容,使用innerHTML,想要设置文本内容,innerText或者textContent,或者innerHTML,推荐用innerHTML

//获取的时候:
  //innerText :可以获取标签中间的文本内容,但是标签中如果还有标签,那么最里面的标签的文本内容也能获取
  //           但是标签不会被获取, 只能拿到文本
  //innerHTML :才是真正的获取标签中间的所有内容(包括标签也会获取 , 回车, 换行)
```

## 自定义属性

标签的属性 : Attribute , 

元素(对象) 的属性: property

> JS对象对元素的属性进行操作,浏览器会自动作用到标签身上
>
> 而对于JS对象自己的属性, 不会作用到标签身上

本身html标签没有这个属性,自己(程序员)添加的,----自定义属性---为了存储一些数据

在html标签中添加的自定义属性,如果想要获取这个属性的值,需要使用getAttribute("自定义属性的名字")才能获取这个属性的值 , 不能通过 `对象.自定义属性`的方法来获取

> 自定义属性,可以作用于自定义属性,也可以作用于本身就有的属性

```javascript
//总结:设置自定义属性:setAttribute("属性的名字","属性的值");========会把给定的属性值转换成字符串

//获取自定义属性的值:getAttribute("属性的名字")

//删除给定的自定义属性 : removeAttribute('属性名')
//对于值是布尔类型, 可以使用removeAttribute
```

### 案例 添加自定义属性

```javascript
<ul id="uu">
  <li>助教的数学成绩</li>
  <li>班主任的成绩</li>
  <li>小苏的成绩</li>
  <li>小杰老师成绩</li>
  <li>乔峰成绩</li>
</ul> 

//根据id获取ul标签,并且或者该标签中所有的li
var list=my$("uu").getElementsByTagName("li");
//循环遍历
for(var i=0;i<list.length;i++){
  //先为每个li添加自定义属性
  //list[i].score=(i+1)*10;//此方式,自定义属性在DOM对象上,不在标签中
  list[i].setAttribute("score",(i+1)*10);
  //点击每个li标签,显示对应的自定义属性值
  list[i].onclick=function(){
    alert(this.getAttribute("score"));
  };
}
```

## 移除自定义属性

```javascript
//移除自定义属性:removeAttribute("属性的名字")

而且removeAttribute("");还可以移除标签自带的属性
```



## Tab栏切换案例(排他功能)

```javascript
<div class="box" id="box">
  <div class="hd">
    <span class="current">体育</span>
    <span>娱乐</span>
    <span>新闻</span>
    <span>综合</span>
  </div>
  <div class="bd">
    <ul>
      <li class="current">我是体育模块</li>
      <li>我是娱乐模块</li>
      <li>我是新闻模块</li>
      <li>我是综合模块</li>
    </ul>
  </div>
</div>

<script>
  //获取最外面的div
  var box=my$("box");
  //获取的是里面的第一个div
  var hd=box.getElementsByTagName("div")[0];
  //获取的是里面的第二个div
  var bd=box.getElementsByTagName("div")[1];
  //获取所有的li标签
  var list=bd.getElementsByTagName("li");//=================================
  //获取所有的span标签
  var spans=hd.getElementsByTagName("span");
  //循环遍历的方式,添加点击事件
  for(var i=0;i<spans.length;i++){
   
      //在点击之前就把索引保存在span标签中
   	spans[i].setAttribute("index",i);//================================
    
     spans[i].onclick=function () {
      //第一件事,所有的span的类样式全部移除
      for(var j=0;j<spans.length;j++){
        spans[j].removeAttribute("class");
      }

      //第二件事,当前被点击的span应用类样式
      this.className="current";
      //span被点击的时候获取存储的索引值
      //alert(this.getAttribute("index"));
      var num=this.getAttribute("index");//==============================

      //获取所有的li标签,每个li标签先全部隐藏
      for(var k=0;k<list.length;k++){
        list[k].removeAttribute("class");
      }
      //当前被点击的span对应的li标签显示
      list[num].className="current";
    };
  }
</script>
```


# Web  API 第三天

## 节点的引入

页面中的内容:

文档: document  页面顶级对象

元素 : 页面中所有的标签

节点 :页面中所有的内容 包括标签 , 元素  , 内容 (回车,空格)



### 节点的优点

可以获取页面中的任意元素和内容,并且筛选出自己想要的标签或者是内容

### 节点的相关属性

1、 nodeType : 节点的类型 

```javascript
/*取值
1----标签;   2-----属性   3----文本 */
```

2 、nodeName: 节点的名字

```js
/*取值:
标签节点 : 名字是大写的标签
属性节点 : 小写的属性名字
文本节点 : #text
*/
```

3、nodeValue : 节点的值

```js
/*
	标签节点 : null
	属性节点 : 属性值
	文本节点 : 文本内容
*/
```

## 获取节点(12行代码)

```js
	var ul=document.getElementById("uu");

	//父级元素==============一般情况下没有区别,但是html的父元素是null
	console.log(ul.parentElement);
	//父级节点
	console.log(ul.parentNode);
	
	//子级元素
	console.log(ul.children);
	//子级节点
	console.log(ul.childNodes);
	
	//元素的第一个子节点
	console.log(ul.firstChild);
	//元素的第一个子元素
	console.log(ul.firstElementChild);
	
	//元素最后一个子节点
	console.log(ul.lastChild);
	//元素最后一个子元素
	console.log(ul.lastElementChild);
	
	//元素的前一个兄弟节点
	console.log(ul.previousSibling);
	//元素的前一个兄弟元素
	console.log(ul.previousElementSibling);
	
	//元素的后一个兄弟节点
	console.log(ul.nextSibling);
	//元素的后一个兄弟元素
	console.log(ul.nextElementSibling);
```

## 节点案例

### 点击按钮修改div中的p标签

```js
<input type="button" value="变色" id="btn"/>
<div id="dv">
   <span>这是span</span>
   <p>这是p</p>
   <span>这是span</span>
   <p>这是p</p>
   <span>这是span</span>
   <p>这是p</p>
   <span>这是span</span>
   <a href="http://www.baidu.com">百度</a>
</div>
<script src="common.js"></script>
<script>
   my$("btn").onclick = function () {
      //先获取div
      var dvObj = my$("dv");
      var nodes = dvObj.childNodes;
      for (var i = 0; i < nodes.length; i++) {
         if (nodes[i].nodeType == 1 && nodes[i].nodeName == "P") {
            nodes[i].style.backgroundColor = "red";
         }
      }
   };
```



### 节点操作隔行变色

```js
<input type="button" value="变色" id="btn"/>
<ul id="uu">
  <li>爆炒助教</li>
  <li>油炸班主任</li>
  <li>清蒸小苏</li>
  <li>红烧班长</li>
  <li>红烧肉</li>
  <li>糖醋排骨</li>
  <li>凉拌秋葵</li>
  <li>鱼香胡萝卜丝</li>
</ul>
<script src="common.js"></script>
<script>
  //隔行变色--li
  my$("btn").onclick = function () {
    var count=0;//记录有多少个li
    //获取ul中所有的子节点
    var nodes = my$("uu").childNodes;
    for (var i = 0; i < nodes.length; i++) {
      //判断这个节点是不是li标签
      if (nodes[i].nodeType == 1 && nodes[i].nodeName == "LI") {
        nodes[i].style.backgroundColor=count%2==0?"red":"yellow";
        count++;//8个
        //nodes[i].style.backgroundColor = i % 2 == 0 ? "red" : "yellow";
      }
    }
  };
```

### 案例 切换背景图片

```js
<body id="bd">
<div id="mask">
   <img src="images/1.jpg" alt="">
   <img src="images/2.jpg" alt="">
   <img src="images/3.jpg" alt="">
</div>
<script src="common.js"></script>
<script>
   var imgObjs = my$("mask").children;//获取的所有的子元素
   //循环遍历所有img,注册点击事件
   for (var i = 0; i < imgObjs.length; i++) {
      imgObjs[i].onclick = function () {
         document.body.style.backgroundImage = "url(" + this.src + ")";
      };
   }
</script>
```

### 菜单全选和全不选案例

```js
   //获取全选的这个复选框
   var ckAll = my$("j_cbAll");
   //获取tbody中所有的小复选框
   var cks = my$("j_tb").getElementsByTagName("input");
   //点击全选的这个复选框,获取他当前的状态,然后设置tbody中所有复选框的状态
   ckAll.onclick = function () {
      //console.log(this.checked);
      for (var i = 0; i < cks.length; i++) {
         cks[i].checked = this.checked;
      }
   };
   //获取tbody中所有的复选框,分别注册点击事件
   for (var i = 0; i < cks.length; i++) {
      cks[i].onclick = function () {
         var flag = true;//默认都被选中了
         //判断是否所有的复选框都选中
         for (var j = 0; j < cks.length; j++) {
            if (!cks[j].checked) {
               //没选中就进来了
               flag = false;
               break;
            }
         }
         //全选的这个复选框的状态就是flag这个变量的值
         ckAll.checked = flag;
      };
   }
</script>
```

## 节点的兼容代码(已不用考虑)

```js
//获取任意一个父级元素的第一个子级元素
function getFirstElementChild(element) {
  if(element.firstElementChild){//true--->支持
    return element.firstElementChild;
  }else{
    var node=element.firstChild;//第一个节点
    while (node&&node.nodeType!=1){
      node=node.nextSibling;
    }
    return node;
  }
}
```

```json
//获取任意一个父级元素的最后一个子级元素
function getLastElementChild(element) {
  if(element.lastElementChild){//true--->支持
    return element.lastElementChild;
  }else{
    var node=element.lastChild;//第一个节点
    while (node&&node.nodeType!=1){
      node=node.previousSibling;
    }
    return node;
  }
}
```
```js
//最后一个节点和最后一个元素的获取的代码在IE8中可能不支持
//前一个节点和前一个元素的获取的代码在IE8中可能不支持
//后一个节点和后一个元素的获取的代码在IE8中可能不支持
```

## 元素的创建

### 第一种方式

> 如果在页面加载的时候, 创建元素, 不会覆盖页面中已存在的元素,只会在执行script代码的时候追加创建元素
>
> 如果是在页面加载完毕之后, 创建元素, 会把以前已经存在的元素都干掉

document. write("标签代码及内容");

```js
my$("btn").onclick=function () {
  document.write("<p>这是一个p</p>");
};
/*缺点:
	如果在页面加载完毕后,使用此方式创建元素,页面上的所有的内容会被全部干掉
```

### 第二种方式

对象 . innerHTML = "标签内容及代码"=====>在创建元素的时候能够解析标签

```js
my$("btn").onclick=function () {
    //此时页面已经加载完毕可以使用
  my$("dv").innerHTML="<p>窗前明月光,疑是地上霜,举头望明月,低头思故乡</p>";
};
/* 注意:
在页面加载完毕后,创建新元素也会干掉对象中的内容 , 包括原有内容的事件也会被清除掉
```

**使用场景** 

> 对于需要给页面加一个很多元素, 字符串的拼接要比一次一次的创建速度要快
>
> 但是用于原有元素没有绑定的事件

### 第三种方式

**创建元素**

创建元素只能使用`document`创建元素

```js
document . createElement("标签名字");======创建的是一个对象
```

**追加元素**

父级元素 . appendChild (创建的元素)

> 不光可以把创建的节点追加到文档中, 也可以把文档的中的元素移动到另一个文档中

```js
my$("btn").onclick = function () {
  //创建元素的
  var pObj = document.createElement("p");
  setInnnerText(pObj, "这是一个p");
  //把创建后的子元素追加到父级元素中
  my$("dv").appendChild(pObj);
};
```

**克隆元素**

会把克隆的对象返回,克隆出来的节点会游离在内存中 , 需要追加到页面中

```js
//之间调用,不会克隆对象的内容,只会克隆节点
克隆的对象.cloneNode()
// 参数 : true ===> 深度克隆,克隆本身以及内容
//		false====>浅克隆,值克隆节点本身,不包括内容, 默认是false
```

```js
var clone = div.cloneNode()  //克隆元素
my('dv').appendChild(clone)	 //追加元素
```





## 元素的相关方法

### **插入元素**

 父节点. insertBefore ( 要追加的元素, 参照元素) ;

```js
如果第二个参数时null , 等同于appendChild,会将节点插入(移动)到最后面
parentNode = insertBefore(newNode , oldNode)

// 把obj元素添加到 dv第一个子元素的前面
my$("dv").insertBefore(obj,my$("dv").firstElementChild);
```



### 删除元素

`removeChild()` 调用者是要删除元素的父元素调用

> 元素不能	自杀, 只能父元素出面

```js
//父元素.removeChild(要删除的子元素)

p.parentNode.removeChild(p)
```



### **替换元素**

对象 . replaceChild( 新节点 ,  老节点)

有返回值, 会把替换掉的元素返回

### 案例   移除元素按钮

对象 . removeChild ( 要移除的元素)

案例: 添加 和 删除 按钮

```js
<input type="button" value="显示效果" id="btn"/>
<input type="button" value="干掉第一个子元素" id="btn2"/>
<input type="button" value="干掉所有子元素" id="btn3"/>
<div id="dv"></div>
<script>

  var i=0;
  my$("btn").onclick=function () {
    i++;
   var obj= document.createElement("input");
    obj.type="button";
    obj.value="按钮"+i;
    //my$("dv").appendChild(obj);//追加子元素
    //把新的子元素插入到第一个子元素的前面
    my$("dv").insertBefore(obj,my$("dv").firstElementChild);
    //my$("dv").replaceChild();---自己玩
  };

  my$("btn2").onclick=function () {
    //移除父级元素中第一个子级元素
    my$("dv").removeChild(my$("dv").firstElementChild);
  };
  
  my$("btn3").onclick=function () {
    //点击按钮删除div中所有的子级元素
    //判断父级元素中有没有第一个子元素
    while(my$("dv").firstElementChild){
      my$("dv").removeChild(my$("dv").firstElementChild);
    }

  };
</script>
```

### 创建元素的BUG问题

​	方法一:有则删除,无则创建

```js
<input type="button" value="显示效果" id="btn"/>
<div id="dv"></div>

//先判断有没有,有就删除,然后再创建
 my$("btn").onclick=function () {
   //判断,div中有没有这个按钮,有就删除
   //判断这个按钮的子元素是否存在
   if(my$("btn2")){//如果为true就有
     my$("dv").removeChild(my$("btn2"));
   }
   var obj=document.createElement("input");
   obj.type="button";
   obj.value="按钮";
   obj.id="btn2";
   my$("dv").appendChild(obj);
 };
```

方法二 :  无则创建 有则不管

```js
my$("btn").onclick = function () {
   //判断,div中有没有这个按钮,有就删除
   //判断这个按钮的子元素是否存在
   if (!my$("btn2")) {//如果为true就有
      var obj = document.createElement("input");
      obj.type = "button";
      obj.value = "按钮";
      obj.id = "btn2";
      my$("dv").appendChild(obj);
   }
};
```

## 元素创建案例

### 点击按钮创建一个图片

```js
<input type="button" value="来个图片" id="btn"/>
<div id="dv"></div>
<script src="common.js"></script>
<script>
  //点击按钮,在div中创建一个图片
  my$("btn").onclick=function () {
     my$("dv").innerHTML="<img src='images/liuyan.jpg' alt='美女' />";
  };
```

### 点击按钮创建列表

```js
<input type="button" value="创建列表" id="btn"/>
<div id="dv"></div>
<script>
  var names = ["杨过", "郭靖", "张无忌", "张三丰", "乔峰", "段飞", "丁棚"];
  my$("btn").onclick = function () {
    var str = "<ul style='list-style-type: none;cursor: pointer'>";
    //根据循环创建对应对数的li
    for (var i = 0; i < names.length; i++) {
      str += "<li>" + names[i] + "</li>";
    }
    str += "</ul>";
    my$("dv").innerHTML = str;

    //代码执行到这里,li已经有了
    //获取所有的li,遍历,添加鼠标进入事件,鼠标离开事件
    var list = my$("dv").getElementsByTagName("li");
    for (var i = 0; i < list.length; i++) {
      //鼠标进入
      list[i].onmouseover = function () {
        this.style.backgroundColor = "yellow";
      };
      //鼠标离开
      list[i].onmouseout = function () {
        this.style.backgroundColor = "";
      };
    }
  };
</script>
```

### 动态创建列表

```js
<input type="button" value="创建列表" id="btn"/>
<div id="dv"></div>

<script>
  var kungfu = ["降龙十八掌", "黯然销魂掌", "葵花宝典", "九阴真经", "吸星大法",
    "如来神掌", "化骨绵掌", "玉女心经", "极乐神功", "辟邪剑谱"];

  //点击按钮动态的创建列表,把列表加到div中
  my$("btn").onclick = function () {
    //创建ul,把ul立刻加入到父级元素div中
    var ulObj = document.createElement("ul");
    my$("dv").appendChild(ulObj);
    //动态的创建li,加到ul中
    for (var i = 0; i < kungfu.length; i++) {
      var liObj = document.createElement("li");
      //设置li中间的文字内容
      liObj.innerHTML = kungfu[i];
      ulObj.appendChild(liObj);
      //为li添加鼠标进入事件
      liObj.onmouseover = mouseoverHandle;
      //为li添加鼠标离开事件
      liObj.onmouseout = mouseoutHandle;
    }
  };

  //此位置.按钮的点击事件的外面
  function mouseoverHandle() {
    this.style.backgroundColor = "red";
  }
  function mouseoutHandle() {
    this.style.backgroundColor = "";
  }
//  注意:=======>
  //如果是循环的方式添加事件,推荐用命名函数
  //如果不是循环的方式添加事件,推荐使用匿名函数
  
</script>
```

### 创建一个表格

```js
<input type="button" value="创建表格" id="btn"/>
<div id="dv"></div>
<script>
  var arr=[
    {name:"百度",href:"http://www.baidu.com"},
    {name:"谷歌",href:"http://www.google.com"},
    {name:"优酷",href:"http://www.youku.com"},
    {name:"土豆",href:"http://www.tudou.com"},
    {name:"快播",href:"http://www.kuaibo.com"},
    {name:"爱奇艺",href:"http://www.aiqiyi.com"}
  ];
  //点击按钮创建表格
  my$("btn").onclick=function () {
    //创建table加入到div中
    var tableObj=document.createElement("table");
    tableObj.border="1";
    tableObj.cellPadding="0";
    tableObj.cellSpacing="0";
    my$("dv").appendChild(tableObj);
    //创建行,把行加入到table中
    for(var i=0;i<arr.length;i++){
      var dt=arr[i];//每个对象
      var trObj=document.createElement("tr");
      tableObj.appendChild(trObj);
      //创建第一个列,然后加入到行中
      var td1=document.createElement("td");
      td1.innerText=dt.name;
      trObj.appendChild(td1);
      //创建第二个列
      var td2=document.createElement("td");
      td2.innerHTML="<a href="+dt.href+">"+dt.name+"</a>";
      trObj.appendChild(td2);
    }
  };
</script>
```



## 元素绑定事件

### 应用场景

```js
/*
对于同一个对象,不同JS编写者可能对他注册不同的事件,且想要他的所有事件都执行时,我们则可以为这个对象添加绑定事件
```

### 第一种方式

1、 对象 `. addEventListener("事件类型",事件处理函数,false)`========>谷歌和火狐支持,IE8不支持

这种方式的事件类型不加 On

事件处理函数可以是命名函数也可以是匿名函数

```js
<input type="button" value="按钮" id="btn"/>
<script src="common.js"></script>

	my$("btn").addEventListener("click", function () {
		console.log("小苏猥琐啊");
	}, false);
	my$("btn").addEventListener("click", function () {
		console.log("小苏龌龊啊");
	}, false);
	my$("btn").addEventListener("click", function () {
		console.log("小苏邪恶啊");
	}, false);
	my$("btn").addEventListener("click", function () {
		console.log("小苏下流啊");
	}, false);
	
```

### 第二种方式

2 、`对象 . attachEvent("有on的事件类型",事件处理函数)`=====>谷歌不支持,火狐不支持,IE8支持

注 : webstom 已经将这个方法干掉了;

```js
my$("btn").attachEvent("onclick",function () {
  console.log("小杨好帅哦1");
});

my$("btn").attachEvent("onclick",function () {
  console.log("小杨好帅哦2");
});

my$("btn").attachEvent("onclick",function () {
  console.log("小杨好帅哦3");
});
```

### 元素绑定事件的兼容代码

```js
//为任意元素.绑定任意的事件, 任意的元素,事件的类型,事件处理函数
function addEventListener(element,type,fn) {
  //判断浏览器是否支持这个方法
  if(element.addEventListener){
    element.addEventListener(type,fn,false);
  }else if(element.attachEvent){
    element.attachEvent("on"+type,fn);
  }else{
    element["on"+type]=fn;
  }
}

//测试
  addEventListener(my$("btn"),"click",function () {
    console.log("哦1");
  });
  addEventListener(my$("btn"),"click",function () {
    console.log("哦2");
  });
  addEventListener(my$("btn"),"click",function () {
    console.log("哦3");
  });
```


# Web API 第四天

## 元素解绑事件

### 第一种方式

重新设置一个事件使那个事件的处理函数为null

```js
// 1 对象.on事件名字=事件处理函数----绑定事件
my$("btn").onclick=function () {
  console.log("猥琐");
};
my$("btn2").onclick=function () {
  //1.解绑事件
  my$("btn").onclick=null;
};
```

### 第二种方式

`对象.addEventListener("没有on的事件类型",命名函数,false)`=======>绑定事件

`对象.removeEventListener("没有on的事件函数",命名函数,false)`====>解绑事件

> 只能解绑命令函数的事件处理函数, 匿名函数无法找到对应的处理函数无法注销

```js
function f1() {
  console.log("第一个");
}
function f2() {
  console.log("第二个");
}
my$("btn").addEventListener("click",f1,false);
my$("btn").addEventListener("click",f2,false);
```

### 第三种方式(IE)

​	对象.attachEvent("on事件类型",命名函数);========>绑定事件

​	对象.detachEvent("on事件类型",函数名字);=========>解绑事件



## 绑定事件和解绑事件的兼容代码

### 绑定事件的兼容代码

```js
function addEventListener(element,type,fn) {
  if(element.addEventListener){
    element.addEventListener(type,fn,false);
  }else if(element.attachEvent){
    element.attachEvent("on"+type,fn);
  }else{
    element["on"+type]=fn;
  }
}
```

### 解绑事件的兼容代码

```js
//解绑事件的兼容
//为任意的一个元素,解绑对应的事件
function removeEventListener(element,type,fnName) {
  if(element.removeEventListener){
    element.removeEventListener(type,fnName,false);
  }else if(element.detachEvent){
    element.detachEvent("on"+type,fnName);
  }else{
    element["on"+type]=null;
  }
}
```



## 事件冒泡

### 产生场景

当在嵌套关系中,父级元素也有相同的事件处理函数时, 子级元素的事件函数触发时,父级元素的事件函数也会触发

对象 . addEventListener("事件类型", 事件函数 , true / false)

true==>事件只存在捕获阶段和目标阶段

false===>事件存在冒泡阶段和目标阶段

触发的事件函数都为目标阶段

因为触发事件而触发的事件函数会处于冒泡或者捕获阶段



### 事件的两种类型

**冒泡事件**

> 默认就是冒泡事件, 由里到外触发事件

**捕获事件**

`addEventListener(事件类型, 事件处理函数, true)` , 必须使用`addEventListener`

### 事件阶段

分为三个阶段:

1 事件捕获阶段 ====> 从外向内

2 事件目标阶段=====>鼠标选择的那个

3 事件冒泡阶段=====>从内向外	> 

> ​                   获取注册的事件					触发事件

> 捕获阶段--------------------------------->目标阶段----------------------------------> 冒泡阶段

> 目标阶段的事件触发顺序,有代码书写的顺序

**为元素绑定事件**

* addEventListener("没有on的事件类型",事件处理函数,控制事件阶段的)
* 事件触发的过程中,可能会出现事件冒泡的效果,为了阻止事件冒泡



### 事件对象

每一个事件处理函数都有一个事件对象, 事件对象记录了事件触发时所有的参数都记录在这个对象, 包括鼠标的位置,

事件对象 : `e`

`pageX`   距离页面的水平距离

`pageY`   距离页面的垂直距离

### 阻止事件冒泡

#### 第一种方式

window.event.cancelBubble=true;======>谷歌,IE8支持,火狐不支持

window.event就是一个对象,是IE中的标准

#### 第二种方式

` e.stopPropagation()`=======>阻止事件冒泡---->谷歌和火狐支持

e 是事件函数中的一个隐含参数

```js
my$("btn").onmouseover=function (e) {
  console.log(e);
};
//e输出的是一个对象
```

目标事件调用此方法可以阻止,目标事件以外的事件函数的触发

**window.event和e都是事件参数对象,一个是IE的标准,一个是火狐的标准**

通过e.eventPhase这个属性====>可以输出事件处于什么阶段

```js
/*如果这个属性的值是:
* 1---->捕获阶段
* 2---->目标阶段
* 3---->冒泡

```

```js
<div id="dv1">
  <div id="dv2">
    <div id="dv3"></div>
  </div>
</div>
<script src="common.js"></script>
<script>
      var objs = [my$("dv3"), my$("dv2"), my$("dv1")];
  //遍历注册事件
  objs.forEach(function (ele) {
    //为每个元素绑定事件
    ele.addEventListener("click", function (e) {
      console.log(this.id+"====>"+e.eventPhase);
    }, true);
  });
	/*  点击dv3
	dv1====>1   1是捕获阶段
	dv2====>1   
	dv3====>2   2是目标阶段
	
```

### 案例 : 绑定事件

​	为同一个元素绑定多个不同的事件,指向相同的事件处理函数

```js
<input type="button" value="小苏" id="btn"/>
<script src="common.js"></script>

//为同一个元素绑定多个不同的事件,指向相同的事件处理函数
my$("btn").onclick = f1;
my$("btn").onmouseover = f1;
my$("btn").onmouseout = f1;
function f1(e) {
  switch (e.type) {
    case "click":
      alert("好帅哦");
      break;
    case "mouseover":
      this.style.backgroundColor = "red";
      break;
    case "mouseout":
      this.style.backgroundColor = "green";
      break;
  }
}
 my$("btn").onmouseover=function (e) {
   console.log(e);
 };
```

### 案例 : 百度大项目

```js
<div id="box">
  <input type="text" id="txt" value="">
  <input type="button" value="搜索" id="btn">
</div>
<script src="common.js"></script>

<script>
  var keyWords = ["小杨才是最纯洁的", "小杨才是最帅的", "小段是最猥琐的", "小超是最龌龊的",
    "传智播客是一个培训机构", "传说在传智有个很帅很纯洁的小杨", "苹果好吃", "苹果此次召回还是没有中国"];
  //获取文本框注册键盘抬起事件
  my$("txt").onkeyup = function () {
    
    //每一次的键盘抬起都判断页面中有没有这个div
    if (my$("dv")) {
      //删除一次
      my$("box").removeChild(my$("dv"));
    }
      
    //获取文本框输入的内容
    var text = this.value;
    //临时数组--空数组------->存放对应上的数据
    var tempArr = [];
    //把文本框输入的内容和数组中的每个数据对比
    for (var i = 0; i < keyWords.length; i++) {
      //是否是最开始出现的
      if (keyWords[i].indexOf(text) == 0) {
        tempArr.push(keyWords[i]);//追加
      }
    }
      
    //如果文本框是空的,临时数组是空的,不用创建div
    if (this.value.length == 0 || tempArr.length == 0) {
      //如果页面中有这个div,删除这个div
      if (my$("dv")) {
        my$("box").removeChild(my$("dv"));
      }
      return;
    }
      
    //创建div,把div加入id为box的div中
    var dvObj = document.createElement("div");
    my$("box").appendChild(dvObj);
    dvObj.id = "dv";
    dvObj.style.width = "350px";
    //dvObj.style.height="100px";//肯定是不需要的------
    dvObj.style.border = "1px solid green";
    //循环遍历临时数组,创建对应的p标签
    for (var i = 0; i < tempArr.length; i++) {
      //创建p标签
      var pObj = document.createElement("p");
      //把p加到div中
      dvObj.appendChild(pObj);
      setInnerText(pObj, tempArr[i]);
      pObj.style.margin = 0;
      pObj.style.padding = 0;
      pObj.style.cursor = "pointer";
      pObj.style.marginTop = "5px";
      pObj.style.marginLeft = "5px";
      //鼠标进入
      pObj.onmouseover = function () {
        this.style.backgroundColor = "yellow";
      };
      //鼠标离开
      pObj.onmouseout = function () {
        this.style.backgroundColor = "";
      };
    }   
  };
</script>
```


## BOM

> 浏览器中的顶级对象是: window====>皇上
>
> 页面中的顶级对象是 : docum======>总管太监

### window(top)

在**全局声明变量**都相当于给window对象添加属性,声明的变量都会挂载都window身上

对于window本身已有的属性, 相当于重新赋值

> 在全局声明变量慎用: 一下三个变量

`name`  属性是window已经有的属性, 默认是空字符串, 不管给`name`赋值是什么数据类型, 都会转成字符串类型

`top` 属性默认指向window对象自己 , window在被占用的时候可以用`top` 代替

`status`  属性默认是一个空字符串 , 不管赋值什么数据类型都会转成字符串类型

### 加载事件(onload)

> 触发时机 : 在页面中的所有外部文件和代码都加载完毕才会触发

在浏览器资源加载完毕后,在加载onload中的内容

```js
window.onload=function { }
```

### location对象

> location下面有很多属性和方法

`location.reload() `  重新加载页面 , 可能拿到缓存数据

> 参数 true ===> 强制刷新 , 不拿缓存数据 



浏览器的属性,也是一个对象有自己的属性,一定程度上可以理解为方法也是函数,函数就是方法

```js
	 #href 获取地址栏中的地址=====> 可以赋值
   window.location.href = '/'
	 #地址栏上#及后面的内容
   console.log(window.location.hash);
	  #主机名及端口号
    console.log(window.location.host);
	  #主机名
    console.log(window.location.hostname);
	  #文件的路径---相对路径
    console.log(window.location.pathname);
 	   #端口号
   console.log(window.location.port);
  	   #协议
    console.log(window.location.protocol);
	   #搜索的内容
    console.log(window.location.search);
```

### 页面跳转的方式

```js
location.href="http://www.jd.com";//属性----------------->必须记住
location.assign("http://www.jd.com");//方法-----和href功能一样--有历史记录
location.reload();//重新加载--刷新
location.replace("http://www.jd.com");//没有历史记录
```

### history对象

```js
/history.forward====前进====方法
my$("btn2").onclick = function () {
    window.history.forward();
  };

/history.back=====>后退
my$("btn").onclick = function () {
    window.history.back();
  };
```

### nevigator对象

```js
/通过userAgent可以判断用户浏览器的类型

console.log(window.navigator.userAgent);
```



## 定时器(setInterval)

###多次定时器

```js
# setInterval(回调函数,毫秒时间)  
```

返回值就是定时器的Id

```js
var timeId = setInterval(function () {
  alert("hello");//断言
}, 1000);
document.getElementById("btn").onclick = function () {
  //点击按钮,停止定时器
  
  #清理定时器, 参数时时器的Id
  clearInterval(timeId);
};
```

### 一次性定时器

```js
#一次性定时器, 只会执行一次
setTimeout(回调函数, 毫秒时间)
#清除定时器 , 使用完清除掉, 防止占用内存
clearTimeout(定时器Id) 
```



### 案例

亮晶晶案例

```js
<input type="button" value="亮起来" id="btn"/>
<div id="dv"></div>
<script src="common.js"></script>
<script>
  my$("btn").onclick=function () {
    setInterval(function () {
      my$("dv").innerHTML="<span>★</span>";//span应该脱标拜托标准流
      var x = parseInt(Math.random() * 600 + 1);
      var y = parseInt(Math.random() * 600 + 1);
      my$("dv").firstElementChild.style.left=x+"px";
      my$("dv").firstElementChild.style.top=y+"px";
    },5);

  };
</script>
```

美女时钟

```js
/在页面加载的时候就执行一次函数
function f1 () {
    //获取当前时间
    var dt=new Date();
    var hour=dt.getHours();
    var second=dt.getSeconds();
    
    second=second>10?second:"0"+second;
    hour=hour>10?hour:"0"+hour;
    my$("im").src="meimei/"+hour+"_"+second+".jpg";
  }
  f1();
  setInterval(f1,1000);
</script>
```




# Web  API 第五天



## 一次性定时器

setTimeout(函数 , 时间)

一次性定时器,也需要清除,否则依旧存在,只不过没有作用

```js
//页面加载后
window.onload=function () {
  //一次性的定时器
  var timeId=window.setTimeout(function () {
    alert("您好");
  },1000);
    
    //点击这个按钮,停止这个一次性的定时器
      document.getElementById("btn").onclick=function () {
        clearTimeout(timeId);
      };
    };  
```



## 定时器案例

### 案例一 禁用按钮

```js
<textarea name="texta" id="" cols="30" rows="10">
  这个世界就是这么疯狂,你不同意,我就让你注册,秦始皇,打钱
</textarea>
<input type="button" value="请仔细阅读协议(5)" id="btn" disabled="disabled" />
<script src="common.js"></script>
<script>

  var time=5;
 var timeId= setInterval(function () {

    time--;
   my$("btn").value="请仔细阅读协议("+time+")";
    if(time<=0){
      //停止定时器就可以
      clearInterval(timeId);
      //按钮可以被点击了
      my$("btn").disabled=false;
      my$("btn").value="同意";
    }

  },1000);
</script>
```



### 案例二  div渐变

```js
<style>
  div{
    width: 300px;
    height: 200px;
    background-color: hotpink;
  }
</style>

<div id="dv"></div>
<input type="button" value="渐变" id="btn"/>
<script src="common.js"></script>
<script>

  my$("btn").onclick=function () {

    var opacity=10;===========================>块级元素的透明度属性
    //按钮的点击事件
    var timeId=setInterval(function () {
      //透明化了
      opacity--;
      if(opacity<=0){
        clearInterval(timeId);//清理定时器
      }
      //设置div的透明度
      my$("dv").style.opacity=opacity/10;
    },200);
  };
```

### 案例三 设置div变宽

```js
div {
      width: 200px;
      height: 150px;
      background-color: red;
      border-radius: 100px;
    }
<input type="button" value="变宽" id="btn"/>
<div id="dv"></div>
<script src="common.js"></script>
<script>
  my$("btn").onclick = function () {
    var width = 200;
    var timeId = setInterval(function () {
      width+=10;
      if(width==800){
        clearInterval(timeId);
      }
      my$("dv").style.width=width+"px";
    }, 20);
  };
</script>
```



### 案例三  移动div

```js
<input type="button" value="移动到400px" id="btn1"/>
<input type="button" value="移动到800px" id="btn2"/>
<div id="dv"></div>==============================>需要脱离标准流

my$("btn1").onclick = function () {
    animate(my$("dv"), 400);====================>动画函数
  };
  //点击第二个按钮移动到800px

  my$("btn2").onclick = function () {
    animate(my$("dv"), 800);
  };
```



## 封装动画函数(重点)

```js
//设置任意的一个元素,移动到指定的目标位置
function animate(element, target) {
    //先清理一次定时器,同百度大项目一样
  clearInterval(element.timeId);
  //定时器的id值存储到对象的一个属性中
  element.timeId = setInterval(function () {
    //获取元素的当前的位置,数字类型
    var current = element.offsetLeft;
    //每次移动的距离
    var step = 10;
    step = current < target ? step : -step;
    //当前移动到位置
    current += step;
    if (Math.abs(current - target) > Math.abs(step)) {
      element.style.left = current + "px";
    } else {
      //清理定时器
      clearInterval(element.timeId);
      //直接到达目标
      element.style.left = target + "px";
    }
  }, 20);
}
```



## 完整的轮播图案例

```js
<div class="all" id='box'>
  <div class="screen"><!--相框-->
    <ul>
      <li><img src="images/1.jpg" width="500" height="200"/></li>
      <li><img src="images/2.jpg" width="500" height="200"/></li>
      <li><img src="images/3.jpg" width="500" height="200"/></li>
      <li><img src="images/4.jpg" width="500" height="200"/></li>
      <li><img src="images/5.jpg" width="500" height="200"/></li>
    </ul>
    <ol>
    </ol>
  </div>
  <div id="arr"><span id="left">&lt;</span><span id="right">&gt;</span></div>
</div>

<script src="common.js"></script>

<script>
  //获取最外面的div
  var box = my$("box");
  //获取相框
  var screen = box.children[0];
  //获取相框的宽度
  var imgWidth = screen.offsetWidth;
  //获取ul
  var ulObj = screen.children[0];
  //获取ul中的所有的li
  var list = ulObj.children;
  //获取ol
  var olObj = screen.children[1];
  //焦点的div
  var arr = my$("arr");

  var pic = 0;//=============================>全局变量,存储图片的索引值 
 
//首先在ol中创建li作为轮播的按钮
//创建小按钮----根据ul中的li个数
  for (var i = 0; i < list.length; i++) {
    //创建li标签,加入到ol中
    var liObj = document.createElement("li");
    olObj.appendChild(liObj);
    liObj.innerHTML = (i + 1);
    //在每个ol中的li标签上添加一个自定义属性,存储索引值
    liObj.setAttribute("index", i);
    //注册鼠标进入事件
    liObj.onmouseover = function () {
      //先干掉所有的ol中的li的背景颜色
      for (var j = 0; j < olObj.children.length; j++) {
        liObj[j].removeAttribute("class");
      }
      //设置当前鼠标进来的li的背景颜色
      this.className = "current";
      //获取鼠标进入的li的当前索引值
      pic = this.getAttribute("index");
      //移动ul
      animate(ulObj, -pic * imgWidth);
    };
  }
  //设置ol中第一个li有背景颜色
  olObj.children[0].className = "current";


  //克隆一个ul中第一个li,加入到ul中的最后=====克隆
  ulObj.appendChild(ulObj.children[0].cloneNode(true));

  //自动播放 重复执行鼠标点击右焦点的事件
 var timeId= setInterval(clickHandle,1000);

  //鼠标进入到box的div显示左右焦点的div
  box.onmouseover = function () {
    arr.style.display = "block";
    //鼠标进入废掉之前的定时器
    clearInterval(timeId);
  };
  //鼠标离开到box的div隐藏左右焦点的div
  box.onmouseout = function () {
    arr.style.display = "none";
    //鼠标离开自动播放
    timeId= setInterval(clickHandle,1000);
  };
  //右边按钮
  my$("right").onclick =clickHandle;
  function clickHandle() {
    //如果pic的值是5,恰巧是ul中li的个数-1的值,此时页面显示第六个图片,而用户会认为这是第一个图,
    //所以,如果用户再次点击按钮,用户应该看到第二个图片
    if (pic == list.length - 1) {
      //如何从第6个图,跳转到第一个图
      pic = 0;//先设置pic=0
      ulObj.style.left = 0 + "px";//把ul的位置还原成开始的默认位置
    }
    pic++;//立刻设置pic加1,那么此时用户就会看到第二个图片了
    
    animate(ulObj, -pic * imgWidth);//pic从0的值加1之后,pic的值是1,然后ul移动出去一个图片
    //如果pic==5说明,此时显示第6个图(内容是第一张图片),第一个小按钮有颜色,
    if (pic == list.length - 1) {
      //第五个按钮颜色干掉
      olObj.children[olObj.children.length - 1].className = "";
      //第一个按钮颜色设置上
      olObj.children[0].className = "current";
    } else {
      //干掉所有的小按钮的背景颜色
      for (var i = 0; i < olObj.children.length; i++) {
        olObj.children[i].removeAttribute("class");
      }
      olObj.children[pic].className = "current";
    }

  };
  //左边按钮
  my$("left").onclick = function () {
    if (pic == 0) {
      pic = 5;
      ulObj.style.left = -pic * imgWidth + "px";
    }
    pic--;
    animate(ulObj, -pic * imgWidth);
    //设置小按钮的颜色---所有的小按钮干掉颜色
    for (var i = 0; i < olObj.children.length; i++) {
      olObj.children[i].removeAttribute("class");
    }
    //当前的pic索引对应的按钮设置颜色
    olObj.children[pic].className = "current";

  };

  //设置任意的一个元素,移动到指定的目标位置
  function animate(element, target) {
    clearInterval(element.timeId);
    //定时器的id值存储到对象的一个属性中
    element.timeId = setInterval(function () {
      //获取元素的当前的位置,数字类型
      var current = element.offsetLeft;
      //每次移动的距离
      var step = 10;
      step = current < target ? step : -step;
      //当前移动到位置
      current += step;
      if (Math.abs(current - target) > Math.abs(step)) {
        element.style.left = current + "px";
      } else {
        //清理定时器
        clearInterval(element.timeId);
        //直接到达目标
        element.style.left = target + "px";
      }
    }, 10);
  }
</script>
```



## offset系列(三大系列之一)

应用场景:

```js
//console.log(my$("dv1").style.width);
//console.log(my$("dv1").style.height);
```

在style标签中的样式通过这种方式获取不到

可以通过offset系列属性可以获取道目标元素的宽高的left,top的值

缺点:  不脱标无法获取left和top值

 对于没有脱标的元素,给了元素的left , top 的值,offset系列获取不到元素真实的left top的值

没有脱标我们设置元素的left和top值,虽然没有效果,但是属性值应该存在

```js
/* offsetWidth:获取元素的宽
* offsetHeight:获取元素的高
* offsetLeft:获取元素距离左边位置的值
* offsetTop:获取元素距离上面位置的值
```

```js
//没有脱离文档流:
/*
*
* offsetLeft:父级元素margin+父级元素padding+父级元素的border+自己的margin
*
*
* 脱离文档流了
* 主要是自己的left和自己的margin
* */
```

## document获取元素

```js
console.log(document.body);//获取的是元素--标签
//获取title
console.log(document.title);//标签中的值
document.title="嘎嘎去";
//获取html
console.log(document.documentElement);
```

## 图片跟着鼠标走

```js

<img src="images/tianshi.gif" alt="" id="im">=======>需要脱离文档流
<script src="common.js"></script>
<script>
  //鼠标在页面中移动,图片跟着鼠标移动
  document.onmousemove=function (e) {
    //鼠标的移动的横纵坐标
    //可视区域的横坐标
    //可视区域的纵坐标
    my$("im").style.left=e.clientX+"px";
    my$("im").style.top=e.clientY+"px";
  };
</script>
```




# Web  API 第六天



## 三大家族

### offset系列

offsetLeft : 返回当前元素距离定位父元素的左偏移量

offsetTop : 返回距离定位父元素的上偏移量

> 能够获取元素css样式的left和top值

> 父元素没有定位时,找距离body的left偏移量, 包括body的`margin`  和 `padding`
>
> 父亲有定位时, 找距离定位父元素的left的偏移量,包括父元素和自己的`margin`  和 `padding`

> 在js控制css时,会重新渲染元素, 会重新加载css样式, 如果元素有margin和padding会影响到元素的left和top



offsetWidth :  当前元素的宽 (加边框, 内边距)  , 不包括margin

offsetHeight :当前元素的高(加边框, 内边距)  , 不包括margin

> 注意: 当元素中的内容超出时,获取的width和height是元素盒子的大小

当元素没有脱标,给元素设置left 和 top值,offsetleft 和offsetTop是无法获取

可以通过window.getComputedstyle(元素 , 伪元素(null))方法可以获取元素所有的样式属性需要什么属性直接在后面 .属性 即可获取



offsetParent : 返回离自己最近的**定位父元素**, 父元素没有定位, 返回body



### scroll系列  ====  卷曲

scrollLeft : 内容向左卷曲出去的距离    **可以赋值**

scrollTop : 内容向上卷曲出去的距离     **可以赋值**

> 边框也算在卷曲出去的距离, 只要内容看不到的地方都算在卷曲出去的距离



scrollWidth : 元素内容的实际宽(不加边框)  没有内容就是盒子的宽

scrollHeight : 元素内容实际的高(不加边框) 没有内容就是盒子的高

> 当元素的内容没有超出盒子大小的时候,获取的是元素的宽高(不加边框)
>
> 当元素的内容超出盒子大小的时候,获取的内容的宽高





**获取元素向上获取向左卷曲出去的距离的兼容代码**

```js
//获取页面向上或者向左卷曲出去的距离的值
function getScroll() {
  return {
    left: window.pageXOffset || document.documentElement.scrollLeft || document.body.scrollLeft||0,
    top: window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop || 0
  };
}
```



### client系列===可视区域

**clientLeft : 左边边框的宽度**

**clientTop : 上边边框的宽度**

> 注意: 获取的元素的左边框和上边框的宽度



clientWidth : 返回元素可视区域的宽(没有边框) , 边框内部的宽度, 就是内容的宽度

clientHeight : 返回元素可是区域的高(没有边框) , 边框内部的高度, 内容的高度

> border 不算是元素可视区的内容



clientX  : 鼠标横坐标

clientY :  鼠标纵坐标

> 在事件处理函数中有一个事件处理对象(e)=======IE 8 没有  e=windiw.event

```js
//图片跟着鼠标走====>有BUG  当页面高度太大时,会出现BUG
document.onmousemove = function (e) {
  e = window.event || e;
  //可视区域的横坐标
  //可视区域的纵坐标
  my$("im").style.left = e.clientX + "px";
  my$("im").style.top = e.clientY + "px";
};
```



## 获取浏览器的可视区的宽高

```js
#获取浏览器窗口可视区的宽
window.innerWidth
#获取浏览器可视区的高
window.innerHeight
```



## 获取浏览器滚动出来的距离

pageXOffset 和 pageYOffset: 返回文档在窗口左上角水平和垂直方向滚动的距离。 

```js
#页面滚动出去的距离
window.pageXOffset
window.pageYOffset
```





## 获取页面的 Left  TOP属性值

在事件处理函数中有一个事件处理对象(e)=======IE 8 没有  e=windiw.event

pageX / pageY 则获取的页面的 left和 top 值 能够解决上面的BUG

```js
document.onmousemove = function (e) {
  //相对于页面顶部的坐标
 my$("im").style.left = e.pageX + "px";
 my$("im").style.top = e.pageY + "px";
 // pageX和pageY在谷歌和火狐可以使用,IE8不能用
```



## 获取元素计算后的样式属性

我们可以通过offset系列获取元素的宽高和left top 的值,但是对于没有脱离标准流的元素来说,即使给元素设置left 和top值也无法获取真的值

`window . getComputedStyle ( 元素对象 , null(伪元素)  )`样式属性  获取元素对象的所有样式属性 需要什么属性直接 .属性 即可获取   (IE 8 不兼容)

IE 8 ======元素对象 . currentStyle.属性  可以获取元素的真实属性值



## 补充css属性

```css
user-select : none; //防止用户选中文字
```

**a标签的href属性**

```html
<!-可以阻止a标签的默认跳转行为->
<a href="javascript:;">
```



## 模态框案例









## 变速动画函数的封装(一)

封装任意一个元素的任意一个属性的要到达的值  参数 ( 元素 , 属性 , 目标   )

```js
//element---元素
//attr---属性名字
//target---目标位置
function animate(element,attr ,target) {
  //清理定时器
  clearInterval(element.timeId);
  element.timeId = setInterval(function () {
    //获取元素的当前位置
    var current = parseInt(getStyle(element,attr));//数字类型//===============================
    //移动的步数=======/10 可以出现先快后慢的效果
    var step = (target-current)/10;
      //正值则向上取整 负值则向下取整
    step = step>0?Math.ceil(step):Math.floor(step);
    current += step;
    element.style[attr] = current + "px";//============================================
    if(current==target) {
      //清理定时器
      clearInterval(element.timeId);
    }
    //测试代码:
    console.log("目标位置:"+target+",当前位置:"+current+",每次移动步数:"+step);
  }, 20);
}
```

## 变速动画函数的封装(二)

**任意元素的多个属性**

将多个属性用对象的形式表示 使用 Json 键值对的形式

```js
function animate(element,json,fn) {
  clearInterval(element.timeId);
  element.timeId=setInterval(function () {
    var flag=true;//默认,假设,全部到达目标=====解决有一个元素到达目标就清理定时器的BUG
    for(var attr in json){
      //获取元素这个属性的当前的值
      var current=parseInt((window.getComputedStyle(element,null)[attr]));
      //当前的属性对应的目标值
      var target=json[attr];
      //移动的步数
      var step=(target-current)/10;
      step=step>0?Math.ceil(step):Math.floor(step);
      current+=step;//移动后的值
      element.style[attr]=current+"px";
        //有一个属性没达到目标就不清理定时器
      if(current!=target){
        flag=false;
      }
    }
      //当所有属性都达到目标时
    if(flag){
      //清理定时器
      clearInterval(element.timeId);
        //回调函数在所有属性都执行完毕后再执行回调函数
        if(fn) {
            fn();
        }
    }

    //测试代码
    console.log("目标:"+target+",当前:"+current+",每次的移动步数:"+step);
  },20);
}

//回调函数的作用 : 能够使一个对象执行多个动画
my$("btn1").onclick=function () {
    var json1={"width":400,"height":500,"left":500,"top":80};
      animate(my$("dv"),json1,function () {
        var json2={"width":40,"height":50,"left":50,"top":800};
        animate(my$("dv"),json2,function () {
          var json3={"width":450,"height":550,"left":550,"top":600};
          animate(my$("dv"),json3);
        });
      });
  };

```

## 变速动画-终极版本

**可以设置层级和透明度**

```js
function animate(element, json, fn) {
  clearInterval(element.timeId);//清理定时器
  //定时器,返回的是定时器的id
  element.timeId = setInterval(function () {
    var flag = true;//默认,假设,全部到达目标
    //遍历json对象中的每个属性还有属性对应的目标值
    for (var attr in json) {
      //判断这个属性attr中是不是opacity
      if (attr == "opacity") {======================//透明度
        //获取元素的当前的透明度,当前的透明度放大100倍
        var current = (window.getComputedStyle(element,null)[attr]) * 100;
        //目标的透明度放大100倍
        var target = json[attr] * 100;
        var step = (target - current) / 10;
        step = step > 0 ? Math.ceil(step) : Math.floor(step);
        current += step;//移动后的值
        element.style[attr] = current / 100;
      } else if (attr == "zIndex") {===================== //判断这个属性attr中是不是zIndex
        //层级改变就是直接改变这个属性的值
        element.style[attr] = json[attr];
      } else {==============================================================//普通的属性
        //获取元素这个属性的当前的值
        var current = parseInt((window.getComputedStyle(element,null)[attr]));
        //当前的属性对应的目标值
        var target = json[attr];
        //移动的步数
        var step = (target - current) / 10;
        step = step > 0 ? Math.ceil(step) : Math.floor(step);
        current += step;//移动后的值
        element.style[attr] = current + "px";
      }
      //是否到达目标
      if (current != target) {
        flag = false;
      }
    }
    if (flag) {
      //清理定时器
      clearInterval(element.timeId);
      //所有的属性到达目标才能使用这个函数,前提是用户传入了这个函数
      if (fn) {
        fn();
      }
    }
    //测试代码
    console.log("目标:" + target + ",当前:" + current + ",每次的移动步数:" + step);
  }, 20);
}
```



## 动画函数案例(重点)

### 一 固定导航栏

```js
<div class="top" id="topPart">
  <img src="images/top.png" alt=""/>
</div>
<div class="nav" id="navBar">
  <img src="images/nav.png" alt=""/>
</div>
<div class="main" id="mainPart">
  <img src="images/main.png" alt=""/>
</div>
<script src="common.js"></script>

window.onscroll=function () {
    //向上卷曲出去的距离和最上面的div的高度对比
    if(getScroll().top>=my$("topPart").offsetHeight){
      //设置第二个div的类样式
     my$("navBar").className="nav fixed";
      //设置第三个div的marginTop的值
      my$("mainPart").style.marginTop=my$("navBar").offsetHeight+"px";
    }else{
      my$("navBar").className="nav";
      my$("mainPart").style.marginTop="10px";
    }
  };
```

### 二 筋斗云

```js
<div class="nav">
  <span id="cloud"></span>
  <ul id="navBar">
    <li>北京校区</li>
    <li>上海校区</li>
    <li>广州校区</li>
    <li>深圳校区</li>
    <li>武汉校区</li>
    <li>关于我们</li>
    <li>联系我们</li>
    <li>招贤纳士</li>
  </ul>
</div>


//获取云彩
  var cloud = my$("cloud");
  //获取所有的li标签
  var list = my$("navBar").children;
  //循环遍历分别注册鼠标进入,鼠标离开,点击事件
  for (var i = 0; i < list.length; i++) {
    //鼠标进入事件
    list[i].onmouseover = mouseoverHandle;
    //点击事件
    list[i].onclick = clickHandle;
    //鼠标离开事件
    list[i].onmouseout = mouseoutHandle;
  }
  function mouseoverHandle() {//进入
    //移动到鼠标此次进入的li的位置
    animate(cloud, this.offsetLeft);
  }
  //点击的时候,记录此次点击的位置
  var lastPosition = 0;
  function clickHandle() {//点击
    lastPosition = this.offsetLeft;
  }
  function mouseoutHandle() {//离开
    animate(cloud, lastPosition);
  }
```

### 三 手风琴

```js
<div id="box">
  <ul>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
  </ul>
</div>

 function animate(element, json, fn) =====//需要动画函数
     
  //先获取所有的li标签=====默认每一li的宽度为240px
  var list = my$("box").getElementsByTagName("li");
  for (var i = 0; i < list.length; i++) {
    list[i].style.backgroundImage = "url(images/" + (i + 1) + ".jpg)";
    //鼠标进入
    list[i].onmouseover = mouseoverHandle;
    //鼠标离开
    list[i].onmouseout = mouseoutHandle;
  }
  //进入
  function mouseoverHandle() {====//鼠标经过当期li变成800宽 ,其他li为 100宽
    for (var j = 0; j < list.length; j++) {
      animate(list[j], {"width": 100});//动画效果
    }
    animate(this, {"width": 800});
  }
  //离开
  function mouseoutHandle() {
    for (var j = 0; j < list.length; j++) {
      animate(list[j], {"width": 240});//动画效果
    }
  }

```

### 四 开机动画效果

```js
<div class="box" id="box">
  <span id="closeButton"></span>
  <div class="hd" id="headPart">
    <img src="images/t.jpg" alt=""/>
  </div>
  <div class="bd" id="bottomPart">
    <img src="images/b.jpg" alt=""/>
  </div>
	
my$("closeButton").onclick=function () {
    //设置最下面的div的高渐渐的变成0
    animate(my$("bottomPart"),{"height":0},function () {
      animate(my$("box"),{"width":0});====//将整个box的宽度变为0
    });
  };
```

### 五 旋转木马

```css
<div class="wrap" id="wrap">
  <div class="slide" id="slide">
    <ul>
      <li><a href="#"><img src="images/slidepic1.jpg" alt=""/></a></li>
      <li><a href="#"><img src="images/slidepic2.jpg" alt=""/></a></li>
      <li><a href="#"><img src="images/slidepic3.jpg" alt=""/></a></li>
      <li><a href="#"><img src="images/slidepic4.jpg" alt=""/></a></li>
      <li><a href="#"><img src="images/slidepic5.jpg" alt=""/></a></li>
    </ul>
    <div class="arrow" id="arrow">
      <a href="javascript:;" class="prev" id="arrLeft"></a>
      <a href="javascript:;" class="next" id="arrRight"></a>
    </div>
  </div>
</div>

//数组中存储的对象,每一对象不同的透明度,每个li对应每个数组中的对象
    var config = [
      {
        width: 400,
        top: 20,
        left: 50,
        opacity: 0.2,
        zIndex: 2
      },//0
      {
        width: 600,
        top: 70,
        left: 0,
        opacity: 0.8,
        zIndex: 3
      },//1
      {
        width: 800,
        top: 100,
        left: 200,
        opacity: 1,
        zIndex: 4
      },//2
      {
        width: 600,
        top: 70,
        left: 600,
        opacity: 0.8,
        zIndex: 3
      },//3
      {
        width: 400,
        top: 20,
        left: 750,
        opacity: 0.2,
        zIndex: 2
      }//4

    ];

    //页面加载的事件
    window.onload = function () {
      var flag=true;//假设所有的动画执行完毕了---锁==================
        //锁 ---只有上一次动画执行完毕才会执行下一次动画函数
      var list = my$("slide").getElementsByTagName("li");
      //1---图片散开
      function assign() {
        for (var i = 0; i < list.length; i++) {
          //设置每个li,都要把宽,层级,透明度,left,top到达指定的目标位置
          animate(list[i], config[i],function () {
            flag=true;//========================================执行动画
          });
        }
      }
      assign();
      //右边按钮
      my$("arrRight").onclick = function () {
        if(flag){//===============================================锁
          flag=false;
          config.push(config.shift());
          assign();//重新分配
        }

      };
      //左边按钮
      my$("arrLeft").onclick = function () {
        if(flag){//=============================================锁
          flag=false;
          config.unshift(config.pop());
          assign();
        }

      };
      //鼠标进入,左右焦点的div显示
      my$("slide").onmouseover = function () {
        animate(my$("arrow"), {"opacity": 1});
      };
      //鼠标离开,左右焦点的div隐藏
      my$("slide").onmouseout = function () {
        animate(my$("arrow"), {"opacity": 0});
      };
    };
```




# Web API 第七天

## 获取坐标的总结

把各种函数封装在对象中

```js
var evt={
  //window.event和事件参数对象e的兼容
  getEvent:function (evt) {
    return window.event||evt;
  },
  //可视区域的横坐标的兼容代码
  getClientX:function (evt) {
    return this.getEvent(evt).clientX;
  },
  //可视区域的纵坐标的兼容代码
  getClientY:function (evt) {
    return this.getEvent(evt).clientY;
  },
  //页面向左卷曲出去的横坐标
  getScrollLeft:function () {
    return window.pageXOffset||document.body.scrollLeft||document.documentElement.scrollLeft||0;
  },
  //页面向上卷曲出去的纵坐标
  getScrollTop:function () {
    return window.pageYOffset||document.body.scrollTop||document.documentElement.scrollTop||0;
  },
  //相对于页面的横坐标(pageX或者是clientX+scrollLeft)
  getPageX:function (evt) {
    return this.getEvent(evt).pageX? this.getEvent(evt).pageX:this.getClientX(evt)+this.getScrollLeft();
  },
  //相对于页面的纵坐标(pageY或者是clientY+scrollTop)
  getPageY:function (evt) {
    return this.getEvent(evt).pageY?this.getEvent(evt).pageY:this.getClientY(evt)+this.getScrollTop();
  }
```



## 案例 

### 拖拽对话框

```js
<div class="login-header"><a id="link" href="javascript:void(0);">点击，弹出登录框</a></div>
<div id="login" class="login">====登录框
	<div id="title" class="login-title">登录会员
	 <span><a id="closeBtn" href="javascript:void(0);" class="close-login">关闭</a></span>
</div>
<div id="bg" class="login-bg"></div><!--遮挡层-->


 //获取超链接,注册点击事件,显示登录框和遮挡层
  my$("link").onclick = function () {
    my$("login").style.display = "block";
    my$("bg").style.display = "block";
  };

//获取关闭,注册点击事件,隐藏登录框和遮挡层
  my$("closeBtn").onclick = function () {
    my$("login").style.display = "none";
    my$("bg").style.display = "none";
  };

//按下鼠标,移动鼠标,移动登录框
  my$("title").onmousedown = function (e) {
    //获取此时的可视区域的横坐标-此时登录框距离左侧页面的横坐标
    var spaceX = e.clientX - my$("login").offsetLeft;
    var spaceY = e.clientY - my$("login").offsetTop;
    //移动的事件
    document.onmousemove = function (e) {
      //新的可视区域的横坐标-spaceX====>新的值--->登录框的left属性
      var x = e.clientX - spaceX+250;
      var y = e.clientY - spaceY-140;
      my$("login").style.left = x + "px";
      my$("login").style.top = y + "px";

    }
  };
document.onmouseup=function () {
    document.onmousemove=null;//当鼠标抬起的时候,把鼠标移动事件干掉
  };
```

### 放大镜案例

```js
<div class="box" id="box">
  <div class="small"><!--小层-->
    <img src="images/small.png" width="350" alt=""/>
    <div class="mask"></div><!--遮挡层-->
  </div><!--小图-->
  <div class="big"><!--大层-->
    <img src="images/big.jpg" width="800" alt=""/><!--大图-->
  </div><!--大图-->
</div>


    y = y - 100;
    //横坐标的最小值
    x = x < 0 ? 0 : x;
    //纵坐标的最小值
    y = y < 0 ? 0 : y;
    //横坐标的最大值
    x = x > small.offsetWidth - mask.offsetWidth ? small.offsetWidth - mask.offsetWidth : x;
    //纵坐标的最大值
    y = y > small.offsetHeight - mask.offsetHeight ? small.offsetHeight - mask.offsetHeight : y;
    //为遮挡层的left和top赋值
    mask.style.left = x + "px";
    mask.style.top = y + "px";

    //遮挡层的移动距离/大图的移动距离=遮挡层的最大移动距离/大图的最大移动距离
    //大图的移动距离=遮挡层的移动距离*大图的最大移动距离/遮挡层的最大移动距离

    //大图的横向的最大移动距离
    var maxX = bigImg.offsetWidth - big.offsetWidth;

    //大图的纵向的最大移动距离
    //var maxY = bigImg.offsetHeight - big.offsetHeight;

    //大图的横向移动的坐标
    var bigImgMoveX = x * maxX / (small.offsetWidth - mask.offsetWidth);
    //大图的纵向移动的坐标
    var bigImgMoveY = y * maxX / (small.offsetWidth - mask.offsetWidth);

    //设置图片移动
    bigImg.style.marginLeft = -bigImgMoveX + "px";
    bigImg.style.marginTop = -bigImgMoveY + "px";

  };
```




# Web API 第八天



## mouseover和mouseout的问题

在放大镜案例中, 在IE 8 中就会出现闪烁问题

当鼠标进入`父盒子` , `子盒子`就会显示, 鼠标在`子盒子`身上 , 父盒子就检测不到`鼠标`就会触发大盒子的鼠标离开事件, 鼠标离开大盒子子盒子就要隐藏 , 子盒子隐藏,`鼠标`又会暴露在大盒子上面, 子盒子又会显示, 所以就会出现闪烁问题

在事件冒泡角度, 由于父元素检测不到子元素, 就会触发鼠标离开的事件 , 而`mouseenter` 能够检测到嵌套的子元素, 就不会触发其身上的鼠标离开事件



## mouseenter 和 mouseleave 事件

浏览器重新提供了两个鼠标离开和进入事件 , 就能够解决mouseover 和 mouseout , 因为 父子嵌套关系 , 鼠标在子盒子上面显示 , 父盒子检测不到鼠标, 触发鼠标离开事件

也就是说, 父盒子能够检测到在自己身上的鼠标 , 即使存在子元素的遮挡 , 也能够检测的到



## classList 操作类样式

className能够操作元素的类样式  , 但是有缺点 , 会直接覆盖掉元素本身的样式

Web API 提供了一个新的 API 操作元素类样式 `classList`

**获取**

> 能够获取元素身上的所有类名, 返回一个**伪数组**

**添加类名 add**

```js
# 不会覆盖元素身上已有的类样式
box.classList.add('bor')
```

**删除指定类名 remove**

```js
box.classList.remove('bor')
```

**切换类名toggle** 

```js
# 在点击按钮中切换
btn.onclick = function () {
    //没有bor这个类, 会添加这个类, 有这个类, 会删除这个类
    box.classList.toggle('bor')
}
```

**判断是否包含一个类名 contains**	

```js
var flag  = box.classList.contains('bor') // true or false
```





## 操作自定义属性

对于W3C规定中的属性, 操作标准属性, 操作直接通过对象操作

对非标准属性 , 自定义属性 , 标签身上的属性 , 不是JS对象中的属性

> 开发者在元素身上自己定义的属性, 非标准属性 , 不能通过点语法直接操作自定义属性

为什么对于元素身上有的属性, 为什么可以使用点语法使用呢?

> 因为浏览提供了这个API , 浏览器支持, 我们这么写



对于非标准属性 , 设置自定义属性, 约定都这么写: `data-自定义属性 `

```js
元素.getAttribute('data-index')
```

**dataset**

通过data设置的自定义属性 , dataset 可以获取所有`data-自定义属性`的属性

`元素 . dataset`  是一个对象 , 里面存储着所有的`data`方式设置的自定义属性

> dataset能够设置和获取元素身上的自定义属性



## keyCode

在键盘抬起和按下的事件对象中

`e.keyCode` 能够获取按下的某个键 , 是一个数字类型 , 某个键对应的数字码

> 键盘上的每一个键都有自己对应的数字码

**使用场景**

能够获取键盘按下的是不是某个键 , 做 相应的事件处理	

```js
enter键 的keyCode = 13 
```



## 事件委托

原理 : 事件冒泡

把子元素要触发的事件, 注册在父元素身上, 子元素需要触发事件, 会冒泡到父元素身上, 父元素在把事件给子元素 , 只需要注册一次, 能够节省内存, 而且支持动态创建的元素

事件对象中的`e.target` 属性 -->永远指向` 事件目标`

注意点 : 在 子元素之间存在 空白的时候 , 点击空白的时候 , `e.target` 就指向父元素 , 就会把父元素的事件触发, 我们可以使用 `nodeName`  或者 `nodeType`  筛选 

```js
ul.onclick = function (e) {
    console.log(e.target.innerText)
    //e.target永远指向事件目标
    //就可以对当前事件对象进行操作
}
```



## 本地存储

window下的一个属性`localStorage`

`localStorage`有几个方法 -> **只能存字符串**

- setItem(键 , 值) , 以键值对的形式存储
  - 第一个参数时键 , 第二个是值
  - 如果需要存数组, 对象, 需要把对象先转成字符串形式的对象 , 在存储
  - JSON.stringify(对象) ==> 转字符串
- getItem(键): 获取数据
  - JSON.parser() => 把字符串形式的对象, 转成对象
- removeItem(键) , 移除



## 移动端触摸事件



### `touchstart` 触摸时触发

```js
#手指触摸屏幕就会触发
//常用 `e.touches`
box.ontouchstart = function () {}
```



### `touchmove`  移动时触发

```js
#手指在屏幕移动时触发
//常用 `e.touches`
box.ontouchmove = function () {}
```



### `touchend` 手机离开时触发

```js
#手指离开屏幕时就会触发
//在离开时, 常用 `e.changedTouch`
box.ontouchend = function () {}
```



### `touchcancel` 中断触摸时触发

突然来电时, 触摸事件就会终止, 事件就会被触发



## 如何获取手指在屏幕上的触摸点

手指触摸屏幕的坐标

移动端也有事件对象 `e`

`e.touches`  屏幕上所有的触摸点 (两个指头触摸或更多)  =====常用

`e.targetTouches`  元素上的触摸点 和 `e.touches` 基本一样

`e.changedTouches`   触点改变的触摸点 , **记录的是变化的触点** , 就是从无到有, 从有到无时的触点 , 在手指离开时, `e.touches ` 和  `e.targetTouches`  



## 封装 Tap事件

### 移动端的点击事件 (Tap)

`click`在移动端触发会延时300ms , 所以在移动端不适用 `click`事件

在移动端使用 click不能使用 click 这时我们就需要 封装一个 tap事件 替代 click



### 点击事件注意点

- 只能有一个触摸点
- 坐标差  , 兼容手抖用户, 允许开始触摸和结束触摸有一定的坐标差
- 时间差 , 触摸开始到触摸结束允许有300ms的误差



### 封装代码

- 只能有一个触摸点

- 坐标差不能大于 5 px , 自定义
- 手指按下和抬起的时间不能超过 300ms

> 函数名 : tap
>
> 函数的参数 : 
>
> ​		1、事件源 : ele
>
> ​		2、事件处理函数
>
> 函数的返回值 : 只需执行函数里的代码, 不需要哦返回值



```js
function tap(ele, fn) {
    //手指按下的坐标
    var startX
    var startY 
    
    //手指按下的时间戳
    var startT
    
    //手指按下
    ele.ontouchstart = function (e) {
        #只能有一个触摸点 , 就return掉================条件1
        if (e.touches.length > 1)  return
        
        //获取手指触摸时的坐标
        startX = e.touches[0].pageX
        startY = e.touches[0].pageY
        
        #开始的时间戳
        startT = new Date()
    }
    
    //手指离开
    ele.ontouchend = function (e) {
        #离开时也只能有一个触点=================条件1
        if (e.changedTouches.length > 1)  return
        
        //获取手指离开时的坐标
        var endX = e.touches[0].pageX
        var endY = e.touches[0].pageY
        
        #手指不能按下和抬起的坐标差不能超过5px===================条件2
        if (Math.abs(endX - startX > 5) || Math.abs(endX - startX > 5)  return
        
       var endT = new Date()
        #时间差不能超过300ms ===============================条件3
        if (endT - startT > 300) return
        
        //如果以上三个条件呢能够满足 ,说明是点击事件===============满足条件,触发事件处理函数
        fn()
    }
}
```





## Zepto

### 概念

针对于移动端的JS库, 简化版的`JQuery`

**Zepto**是一个轻量级的 **针对现代手机端浏览器的 JavaScript 库**。

因为 Zepto 封装了移动端的手势模块，直接把很多手机端手势直接封装成了事件，我们可以直接使用。

Zepto 中文官网地址：https://www.html.cn/doc/zeptojs_api



### zepto使用

touch模块zepto默认没有这个模块, 需要单独下载

![](E:\Web API\img\zepto.png)



### 常用的 touch 事件

| 移动端事件 | 事件类型名称 | 备注                                                        |
| ---------- | ------------ | ----------------------------------------------------------- |
| 快速点击   | tap          | touchstart 和 touchend                                      |
| 左滑动     | swipeLeft    | 驼峰写法，和快速点击差别主要是 触摸开始和触摸结束坐标值差值 |
| 右滑动     | swipeRight   |                                                             |



## Swiper 轮播图插件

### 目标

使用 swiper 快速实现轮播图效果

### 概念

Web 插件：就是别人封装好的一个 js 代码 或 css代码，可以直接拿来用。

Swiper 就是一个轮播图的插件，由其他团队写好的，开源免费，全世界开发者都可以使用。

Swiper插件官网： https://www.swiper.com.cn

### 使用

- 1.首先加载插件，需要用到的文件有swiper.min.js和swiper.min.css文件 

```html
<!DOCTYPE html>
<html>
<head>
    ...
    <link rel="stylesheet" href="dist/css/swiper.min.css">
</head>
<body>
    ...
    <script src="dist/js/swiper.min.js"></script>
    ...
</body>
</html>
```

- 2、准备HTML

```html
<div class="swiper-container">
    <div class="swiper-wrapper">
        <div class="swiper-slide">Slide 1</div>
        <div class="swiper-slide">Slide 2</div>
        <div class="swiper-slide">Slide 3</div>
    </div>
    <!-- 如果需要分页器 -->
    <div class="swiper-pagination"></div>
    
    <!-- 如果需要导航按钮 -->
    <div class="swiper-button-prev"></div>
    <div class="swiper-button-next"></div>
    
    <!-- 如果需要滚动条 -->
    <div class="swiper-scrollbar"></div>
</div>
导航等组件可以放在container之外
```

- 3.你可能想要给Swiper定义一个大小，当然不要也行。 

```html
.swiper-container {
    width: 600px;
    height: 300px;
}
```

- 4.初始化Swiper：最好是挨着</body>标签 

```js
<script>        
  var mySwiper = new Swiper ('.swiper-container', {
         // 左右箭头
            navigation: {
              nextEl: '.swiper-button-next',
              prevEl: '.swiper-button-prev',
            },

            // 小圆点
            pagination: {
              el: '.swiper-pagination',
              //此参数设置为true时，点击分页器的指示点分页器会控制Swiper切换。
              clickable :true,
            }

            // 无缝效果
            loop: true,

            // 滑动方向
             direction: 'vertical',
          
		   //即slider滑动开始到结束的时间
             speed: 1000,

            // 自动播放
            autoplay: {         
            	//自动播放间隔时间
                delay: 1000,
                
                //用户操作swiper之后，是否禁止autoplay。默认为true：停止。
                disableOnInteraction: false
            },

            // 切换效果
             effect: "fade",
  })        
  </script>
```

