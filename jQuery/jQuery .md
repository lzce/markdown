

# jQuery 第一天



## jQuery本质

在jQuery中不需要遍历对象,它是一个伪数组,能够自动遍历对象,是基于js的一个js库,有自己的方法

$的本质就是jQuery  

有length属性



## JQuery的三大特色

- 隐式迭代
- 链式编程
- 能够解决绝大部分浏览器的兼容性问题 (**不是绝对**)

## jq入口函数

第一种方式 : 

```js
//认识
$(document).ready(function () {
  console.log("这是jQuery入口函数的第一种写法");
});
```

第二种方式 :

```js
$(function () {
  console.log("这是jQuery入口函数的第二种写法");
});
```

### 面试题->Window.onload 和 $.ready()

`window.onload`只执行一次入口函数, 多次会覆盖 , 后面的会覆盖前面的

- 等待页面的DOM树, 和图片,多媒体资源 , 以及外部引用资源加载完毕后执行函数

`$.ready`入口函数不会覆盖, 按照代码顺序执行

- 等待DOM树, 加载完成后执行函数



## JS对象和jquery对象的区别

### 什么是DOM对象

使用JS方法获取到的页面元素返回对象就是`DOM对象`

### 什么是jq对象

使用jQuery方法获取得页面元素返回的对象就是`jq对象`

**通过JQ获取的对象都是伪数组  , 数组中的成员是DOM对象** 



### 区别和联系

区别

- **jq对象不能使用DOM对象的方法 ,DOM对象也不能使用jq对象的方法**

联系 

- **jq对象就是DOM对象的一个集合,伪数组,里面存放了很多的DOM对象**



### 相互转换

**花钱才能变得强大**

DOM对象用 `$(dom对象) `包裹就能变成 jq对象

jq对象是一个伪数组, 可以使用下标就可以变成 js对象 也可以使用 get () 方法

> jq对象中存放的是DOM对象

```js
DOM ---> jQuery  $()

jQuery--> DOM   $li[0]  $li.get(0)
```



## jq选择器

### 基本选择器

> JQuery完全兼容CSS选择器

| 名称       | 用法               | 描述                                 |
| ---------- | ------------------ | :----------------------------------- |
| ID选择器   | $(“#id”);          | 获取指定ID的元素                     |
| 类选择器   | $(“.class”);       | 获取同一类class的元素                |
| 标签选择器 | $(“div”);          | 获取同一类标签的所有元素             |
| 并集选择器 | $(“div,p,li”);     | 使用逗号分隔，只要符合条件之一就可。 |
| 交集选择器 | $(“div.redClass”); | 获取class为redClass的div元素         |

> 总结：跟css的选择器用法一模一样。

### 层级选择器

| 名称       | 用法        | 描述                                                        |
| ---------- | ----------- | :---------------------------------------------------------- |
| 子代选择器 | $(“ul>li”); | 使用>号，获取儿子层级的元素，注意，并不会获取孙子层级的元素 |
| 后代选择器 | $(“ul li”); | 使用空格，代表后代选择器，获取ul下的所有li元素，包括孙子等  |

> 跟CSS的选择器一模一样。

### 过滤选择器

> 这类选择器都带冒号: , 常配合CSS选择器使用

| 名称         | 用法                               | 描述                                                         |
| ------------ | ---------------------------------- | :----------------------------------------------------------- |
| :eq（index） | $(“li:eq(2)”).css(“color”, ”red”); | 获取到的li元素中，选择索引号为2的元素，索引号index从0开始。**()中可以写变量** |
| :odd         | $(“li:odd”).css(“color”, ”red”);   | 获取到的li元素中，选择索引号为奇数的元素                     |
| :even        | $(“li:even”).css(“color”, ”red”);  | 获取到的li元素中，选择索引号为偶数的元素                     |
| :first       | $('li:first')                      | 获取li中的第一个元素                                         |
| :last        | $('li:last')                       | 获取li中的最后一个元素                                       |
| :checked     | $("#abc  input:checked")           | 获取被选中的input标签                                        |
| :gt(index)   | $("li : gt(索引)")                 | 获取所有给定大于索引值得元素 , 不包括自己                    |

【案例：隔行变色】

### 筛选选择器(方法)

> 筛选选择器的功能与过滤选择器有点类似，但是用法不一样，筛选选择器主要是方法。

| 名称               | 用法                        | 描述                           |
| ------------------ | --------------------------- | :----------------------------- |
| children(selector) | $(“ul”).children(“li”)      | 相当于$(“ul>li”)，子类选择器   |
| find(selector)     | $(“ul”).find(“li”);         | 相当于$(“ul li”),后代选择器    |
| siblings(selector) | $(“#first”).siblings(“li”); | 查找兄弟节点，不包括自己本身。 |
| parent()           | $(“#first”).parent();       | 查找父亲                       |
| eq(index)          | $(“li”).eq(2);              | 通过下标筛选指定元素           |
| next()             | $(“li”).next()              | 找下一个兄弟                   |
| prev()             | $(“li”).prev()              | 找上一次兄弟                   |
| index()            |                             | 获取元素的下标                 |

## jQuery的方法

### css() 方法

css ("样式属性" , "值" ) 可以对jq对象设置css的样式

```js
$(".green.yellow").css("backgroundColor", "pink");
```

### ready() 方法

该方法用于jQuery的入口函数

```js
$(document).ready(function(){
  //注册事件，把on去掉，是一个方法
  $("#btn1").click(function () {
    //隐式迭代：偷偷的遍历，jQuery会自动的遍历，不需要我们遍历。
    $("div").show(1000);
  });
```

### show () 方法

能射设置元素的显示  可以设置动画效果 show (1000) 括号中可以设置数值

### hide () 方法

能够设置元素的隐藏 也可以设置隐藏的动画效果

### mouseover()  /  mouseenter () 

鼠标经过,jq中推荐使用 mouseenter

### mouseleave()  /mouseout ()

鼠标离开,推荐使用 mouseleave 

### index() 方法

能够获取对象的索引值



# jQuery 第二天



## CSS（）方法

css（name ，value）修改单个样式属性值

```js
$("li")
  .css("backgroundColor", "pink")
  .css("color", "red")
  .css("fontSize", "32px");
```

css（对象）修改多个属性值

```js
$("li").css({
  backgroundColor:"pink",
  color: "red",
  fontSize:"32px",
  border: "1px solid black"
});
```

css （name）获取样式的属性值

当有li 有多个时，只能获取的是第一个li 的样式属性值 ，jQuery认为其他li的样式属性都一样，只获取第一个

```js
console.log($("li").css("fontSize"));//16px
```



## Class（）方法

**与JS中的class操作一一对应**

- classList.add()        添加类

- classList.remove()  移除类

- classList.contains()  判断类

- classList.toggle()      切换类

### addClass () 添加类 

> jq只会在对象的class中添加这个类名字，不管这个类样式存在与否，添加多个类样式时，具体哪个生效根据css中类样式的权重决定根jq没有关系

```js
$("input").eq(0).click(function () {
  
  // 添加一个类
  $("li").addClass("basic");
});
```

### removeClass () 移除类

> 不传参数, 则移除全部类 , 传参数则移除指定的类名

```js
$("input").eq(2).click(function () {
  //移除一个类
  $("li").removeClass("bigger");
});
```

### hasClass () 判断类

> 返回 `true` 或者 `false`

```js
console.log($("li").hasClass("bigger"));
```

### toggleClass () 切换类

> 判断对象中有没有这个类，如果对象中有这个类，则把这个类删除，如果没有这个类则把这个类添加上

```js
$("input").eq(4).click(function () {
  
    //判断li有没有basic类，如果有，就移除他，如果没有，添加他
    //toggle
    $("li").toggleClass("basic");
  });
});
```

### 应用案例

tab栏切换

```js
<script src="../jquery-1.12.4.js"></script>
<script>
  $(function () {
    //上面的tab栏 li标签
    $(".tab-item").mouseenter(function () {
      //两件事件===排他
      $(this).addClass("active").siblings().removeClass("active");
      //下面主体的排他
      var idx = $(this).index();
      $(".main").eq(idx).addClass("selected").siblings().removeClass("selected");
    });
    
  });
</script>
```

![](E:\jQuery\image\tab.png)

## attr （） 属性操作

### 和 css （）方法的区别

css（）设置的样式是在style中 style也是标签对象的一个属性

attr（）设置的是标签对象的属性

### attr (name , value) 设置单个属性

```js
$("img").attr("alt", "图破了");
$("img").attr("title", "错错错错");
```

### attr ( 对象 )  设置多个属性

在对象中使用键值对的方式，传入多个属性和属性值

```js
$("img").attr({
  alt:"图破了",
  title:"错错错",
  aa:"bb"
});
```

### attr ( name ) 获取属性

```js
$("img").attr("alt"); ==============返回的是字符串
```

### removeAttr ()  移除属性

> 可以移除多个属性, 中间以空格隔开

```js
removeAttr(name):移除某个属性
removeAttr('title alt')
```

### 应用案例

美女相册

```js
<script src="../jquery-1.12.4.js"></script>
<script>
  $(function () {
    //1. 给所有的a注册点击事件
    $("#imagegallery a").click(function () {
      var href = $(this).attr("href");//获取a的href 把a的href 给下面的div
      $("#image").attr("src", href);
      
      var title = $(this).attr("title");//获取a 的title 给下面的 P
      $("#des").text(title);
      
      return false; //阻止a跳转
    });
  });
</script>
```

![](E:\jQuery\image\meinv.png)

## prop () 方法

**和attr()的区别**

- `prop()`只能操作固有属性, 不能操作自定义是属性
- `attr()`  可操作固有属性, 也可以操作自定义属性

用法和attr一样，对于布尔类型的属性，不能用attr进行设置属性，否则就会失效，在事件中使用attr设置的属性，只能使用一次

应用场景 ：selected ， checked ，等等布尔类型的属性

```js
$(function () {
  $("input").eq(0).click(function () {
    $("#ck").prop("checked", true);//使用attr设置checked设置属性，点击一次后就失效了
  });

  $("input").eq(1).click(function () {
    $("#ck").prop("checked", false);
  });
});
```

### 应用案例

菜单全选和不选

```js
$(function () {
  
  $("#j_cbAll").click(function () {
    //修改下面的哪些checkbox
    $("#j_tb input").prop("checked", $(this).prop("checked"));
  });

  $("#j_tb input").click(function () {

    if($("#j_tb input:checked").length  ===  $("#j_tb input").length){
      $("#j_cbAll").prop("checked", true)
    }else {
      $("#j_cbAll").prop("checked", false)
    }
  });
  
});
```

![](E:\jQuery\image\caidan.png)

## 三组基本动画

### 显示隐藏动画

#### show () 

> 默认没有动画效果
>
> 不传参数时， 没有动画效果，只能使隐藏的元素的显示

传参数时 show （speed , [callback]）

speed : 动画持续的时间， 可以是毫秒值 ，可以是特定字符串

特定字符串： “fast” ：200ms     normal:400ms      slow : 600ms   传其他字符串时都是normal（400ms）的效果

show中还可以传入回调函数 ，在动画执行完时，回调函数才会执行

```js
$("div").show(1000, function () {
  console.log("哈哈，动画执行完成啦");
})
```

#### hide （）

用法和show () 方法完全一样

```js
$("input").eq(1).click(function () {
  $("div").hide();
})
```

#### toggle()

展示隐藏动画切换



### 下拉上卷 动画

> 特定字符串： “fast” ：200ms     normal:400ms      slow : 600ms  
>
> 不惨参数时, 默认为 normal = 400ms

#### slideDown/slideUp

如果不传参数，默认是normal 有动画效果

参数

 slide(speed, [callback])

```js
//$("div").slideDown();
//$("div").slideDown(1000);
```

slideDown (1000, [ callback ] ) 传入回调函数

在动画执行完毕后再执行回调函数

```js
$("div").slideDown(1000, function () {
  console.log("额呵呵");
});
```

#### slideToggle ()  切换动画

如果是滑入动画，就切换成滑出动画，如果是滑出动画就切换成滑入动画

```js
//如果是滑入状态，就执行滑出的动画，
$('div').slideToggle();
```

案例 下拉菜单

```js
var $li = $(".wrap>ul>li");

//给li注册鼠标经过事件，让自己的ul显示出来
$li.mouseenter(function () {
  //找到所有的儿子，并且还得是ul
  
  //stop：停止当前正在执行的动画
  $(this).children("ul").stop().slideDown();
});

$li.mouseleave(function () {
  $(this).children("ul").stop().slideUp();
});
```

![](E:\jQuery\image\xiala.png)



### 淡入淡出动画 

> 特定字符串： “fast” ：200ms     normal:400ms      slow : 600ms  
>
> 不惨参数时, 默认为 normal = 400ms

参数

​	speed: 动画时间

​	[callback] : 回调函数

#### 淡入fadeIn()

```js
$("input").eq(0).click(function () {
  
  $("div").fadeIn(2000);
  
});
```

#### 淡出 fadeOut

```js
$("input").eq(1).click(function () {
    
  $("div").fadeOut(1000);
})
```

#### 切换 fadeToggle

```js
$("input").eq(2).click(function () {
  
  //如果是淡入状态，就执行淡出的动画，
  $('div').fadeToggle();
})
```

案例  京东轮播呼吸灯效果

```js
$(function () {
  
  var count = 0;
  
  $(".arrow-right").click(function () {
    count++;//count 为索引
    
    //判断是不是最后一个 +1
    if(count == $(".slider li").length){
      count = 0;
    }
    console.log(count);
    //让count渐渐的显示，其他兄弟渐渐的隐藏
    $(".slider li").eq(count).fadeIn().siblings("li").fadeOut();
  });
  
  $(".arrow-left").click(function () {
    count--;
	//判断是不是最后一张 -1
    if(count == -1){
      count = $(".slider li").length - 1;
    }
    console.log(count);
    //让count渐渐的显示，其他兄弟渐渐的隐藏
    $(".slider li").eq(count).fadeIn().siblings("li").fadeOut();
  })
  
});
```

![](E:\jQuery\image\lunbo.png)

## 自定义动画 （animate）

animate （）中可以传四个参数

第一个参数 ： 样式对象   传入需要设置的样式和值  {left：100}  必传参数

第二个参数 ：speed  动画的速度  （数值）

第三个参数 ：动画的执行效果  swing  秋千形态(默认)（先慢后快在慢） linear  线性（匀速）

第四个参数 ： 回调函数

```js
$("#box1").animate({left:800}, 8000);

//swing:秋千 摇摆
$("#box2").animate({left:800}, 8000, "swing");

//linear:线性 匀速
$("#box3").animate({left:800}, 8000, "linear", function () {
  console.log("hahaha");
});
```

案例 ： 手风琴案例

```js
$(function () {
  var $li = $("#box li");
  
    //循环遍历，给每个li添加背景图 由于jQuery隐式迭代，只能设置同样的样式属性 此处只能for循环遍历
  for (var i = 0; i < $li.length; i++) {
    $li.eq(i).css("backgroundImage", "url(images/" + (i + 1) + ".jpg)").mouseleave(function () {
      $li.fadeOut({width:240});
    });
  }


  //给所有的li注册鼠标经过事件
  $li.mouseenter(function () {
    $(this).stop().animate({width:800}).siblings().stop().animate({width:100});
  }).mouseleave(function () {
    $li.stop().animate({width:240});
  });
 
  
});
```

![](E:\jQuery\image\shoufengqin.png)



**案例音乐导航**

```html
 
<style>
    * {
      margin: 0;
      padding: 0;
      list-style: none;
    }

    ul {
      width: 700px;
      height: 60px;
      margin: 0 auto;
    }

    li {
      float: left;
      width: 100px;
      height: 60px;
      text-align: center;
      line-height: 60px;
      background-color: #000;
      position: relative;
      overflow: hidden;
    }

    a {
      color: blue;
      font-size: 24px;
      text-decoration: none;
      position: relative;
      z-index: 1;
    }

    span {
      position: absolute;
      width: 100%;
      height: 100%;
      top: 60px;
      left: 0;
      background-color: yellow;
    }
  </style>



<ul>
    <li>
      <a href="#">导航1</a>
      <span></span>
    </li>
    <li>
      <a href="#">导航2</a>
      <span></span>
    </li>
    <li>
      <a href="#">导航3</a>
      <span></span>
    </li>
    <li>
      <a href="#">导航4</a>
      <span></span>
    </li>
    <li>
      <a href="#">导航5</a>
      <span></span>
    </li>
    <li>
      <a href="#">导航6</a>
      <span></span>
    </li>
    <li>
      <a href="#">导航7</a>
      <span></span>
    </li>
  </ul> 

<div>
    <audio src="mp3/1.mp3"></audio>
    <audio src="mp3/2.mp3"></audio>
    <audio src="mp3/3.mp3"></audio>
    <audio src="mp3/4.mp3"></audio>
    <audio src="mp3/5.mp3"></audio>
    <audio src="mp3/6.mp3"></audio>
    <audio src="mp3/7.mp3"></audio>
  </div>

<script src="jquery-1.12.4.js"></script>

  <script>
  
    //入口函数
    $(function () {

      //加载的音频
      $('audio').load()

      //给每一个注册鼠标经过事件
      $('ul > li').mouseenter(function () {
        //让当前li的的下面的span的 top为0
        $(this).children('span').stop().animate({'top': 0})
      })
      $('ul > li').mouseleave(function () {
        //让当前li的的下面的span的 top为0
        $(this).children('span').stop().animate({'top': 60})

        //获取下标
        var idx = $(this).index()
        $('audio').get(idx).play()
      })

      
    })
  
  </script>
```





## transitionend事件

能够监听CSS3元素动画的执行, 在动画执行完毕后执行, 执行回调函数

```js
lis[0].addEventListener('transitionend', function () {
			flag = true
})
```



**旋转木马案例**

```html
<!DOCTYPE html>
<html>

<head lang="en">
	<meta charset="UTF-8">
	<title>旋转木马轮播图</title>
	<link rel="stylesheet" href="css/css.css" />
	<style>
		.slide li {
			transition: all 0.4s;
		}

		.slide .slide1 {
			width: 400px;
			top: 20px;
			left: 50px;
			opacity: 0.2;
			z-index: 2;
		}

		.slide .slide2 {
			width: 600px;
			top: 70px;
			left: 0;
			opacity: 0.8;
			z-index: 3;
		}

		.slide .slide3 {
			width: 800px;
			top: 100px;
			left: 200px;
			opacity: 1;
			z-index: 4;
		}

		.slide .slide4 {
			width: 600px;
			top: 70px;
			left: 600px;
			opacity: 0.8;
			z-index: 3;
		}

		.slide .slide5 {
			width: 400px;
			top: 20px;
			left: 750px;
			opacity: 0.2;
			z-index: 2;
		}
	</style>
</head>

<body>
	<div class="wrap" id="wrap">
		<div class="slide" id="slide">
			<ul>
				<li><a href="#"><img src="images/slidepic1.jpg" alt="" /></a></li>
				<li><a href="#"><img src="images/slidepic2.jpg" alt="" /></a></li>
				<li><a href="#"><img src="images/slidepic3.jpg" alt="" /></a></li>
				<li><a href="#"><img src="images/slidepic4.jpg" alt="" /></a></li>
				<li><a href="#"><img src="images/slidepic5.jpg" alt="" /></a></li>
			</ul>
			<div class="arrow" id="arrow">
				<a href="javascript:;" class="prev" id="arrLeft"></a>
				<a href="javascript:;" class="next" id="arrRight"></a>
			</div>
		</div>
	</div>

	<script src="../jquery-1.12.4.js"></script>
	<script>
        //类的数组
		var arr = ['slide5', 'slide1', 'slide2', 'slide3', 'slide4']

		//获取所有的li
		var lis = $('#slide ul li')
		//初始页面, 渲染页面
		//封装成一个函数
		function assign() {
			for (let i = 0; i < lis.length; i++) {
				$(lis[i]).removeClass().addClass(arr[i])
			}
		}
		//初始化重新分配
		assign()

		//节流阀
		var flag = true

		//鼠标经过wrap显示左右箭头
		$('.wrap').on('mouseenter', function () {
			$('.arrow').stop().animate({
				opacity: 1
			})
		})
		$('.wrap').on('mouseleave', function () {
			$('.arrow').stop().animate({
				opacity: 0
			})
		})


		//注册点击事件
		$('#arrRight').on('click', function () {
			if (flag) {
				flag = false
				//操作数组 , 删除第一个追加到最后
				arr.push(arr.shift())
				assign()
			}
		})

		$('#arrLeft').on('click', function () {
			if (flag) {
				flag = false
				arr.unshift(arr.pop())
				assign()
			}
		})

		//transtionend事件
		lis[0].addEventListener('transitionend', function () {
			flag = true
		})
		
	</script>
</body>

</html>
```





## delay （）方法

设置一个延时来推迟执行队列中之后的项目。

jQuery 1.4新增。用于将队列中的函数延时执行。他既可以推迟动画队列的执行，也可以用于自定义队列

```
$(function () {
  //fadeIn执行后延时两秒在执行fadeOut动画
  $("div").fadeIn(1000).delay(2000).fadeOut(1000);
  
});
```

## 动画队列

什么是动画队列 ？

在jQuery中可以为同一个对象添加多个动画 ，每个动画会存在动画队列中，一个一个的执行，咋确保每个动画都能执行的情况下，也出现一些弊端，例如在同时触发几个动画时，必须等待上一个动画执行完才能执行下一个动画，且必须执行完

为了解决这以弊端，可以使用 stop（），在每个动画前调用stop 在执行当前动画时，如果上一个动画没执行完，就把上一个动画停止，执行当前动画

```js
//给所有的li注册鼠标经过事件
$li.mouseenter(function () {
  $(this).stop().animate({width:800}).siblings().stop().animate({width:100});
}).mouseleave(function () {
  $li.stop().animate({width:240});
});
```

stop () 中有两个参数

> 默认两个参数都是false

第一个参数 ： clearQueue : 是否清除动画队列  （true false）

第二个参数 ： 是否跳转到**当前动画**的最终执行结果 （true false）

不传参数 : 停止当前动画, 不清空动画队列 , 不跳转到动画执行结果

传一个参数 : 清空动画队列, 不跳转到最终的执行结果

```js
$("div").stop(true);
```

```js
$("div").stop(true, true);
```



## 节点操作 （append）

### 创建节点 

```
 创建节点:  $("<span></span>")
```

### 添加节点

### 父子元素之间的节点操作

#### append （）

父元素 . append (子元素)   

append中直接写要添加元素的HTML代码

子元素必须是jq对象 或者是子元素的HTML代码 不能是选择器  并且是添加在父元素内容的后面

```js
$("#box").append('<a href="http://web.itcast.cn" target="_blank">传智大前端</a>'); 	
```

#### appenTo （）

子元素 . appendTo (父元素)    父元素可以是jq对象也可以是选择器

```js
//添加到子元素的最后面
//$("div").append($("p"));
//$("p").appendTo($("div"));
```

#### prepend （）

父元素  . prepend (子元素)    添加在父元素的前面

```js
//$("div").prepend($("p"));
```

#### prependTo （）

子元素 .  prependTo ( 父元素)

```js
//$("p").prependTo($("div"));
```

### 兄弟元素之间的节点操作

#### after （）

jq对象 . after ( 添加的对象 )   在元素的后面添加一个兄弟元素

```js
 $('div').after($("p"));
```

#### before （） 

在元素的前面添加一个兄弟元素

```js
   $('div').before($("p"));
```

案例 城市选择

```js
$(function () {
  $("#btn1").click(function () {
    $("#src-city>option").appendTo("#tar-city");
  });
  
  $("#btn2").click(function () {
    $("#src-city").append($("#tar-city>option"));
  });
  
  $("#btn3").click(function () {
    $("#src-city>option:selected").appendTo("#tar-city");
  });

  $("#btn4").click(function () {
    $("#src-city").append($("#tar-city>option:selected"));
  });
});
```

![](E:\jQuery\image\city.png)

案例  微博评论

```js
$(function () {
  
  $("#btn").click(function () {
    
    if($("#txt").val().trim().length == 0) {//txt=文本域
      return;
    }
    //就是文本框的值
    $("<li></li>").text($("#txt").val()).prependTo("#ul");

    $("#txt").val("");==清空文本域的值
  })
  
});
```

![](E:\jQuery\image\pinglun.png)



## 清空节点和删除节点

### html （）

可以清空元素内的内容

缺点：只会清空元素内的元素，但是不会清除元素的事件  导致内存泄漏

```js
//$("div").html("");
```

### empty （）

清空元素的内容和绑定的事件

```
//$("div").empty();
```

### remove （）

html (" ") 和empty （）只能清除元素的内容 ，自己不会清除   =====清理门户

remove （） 会把自己和子元素全部清除掉 ============连自己也不放过

```
//$("div").remove();
```



## 克隆节点

### clone （）

克隆元素 ，有一个参数 值是布尔类型 （true / false）

- false:不传参数是浅克隆 , 会克隆元素和样式 , 不会克隆事件
- true:是深克隆，会克隆事件

```
$(".des").clone(true).appendTo("div");
```

### 案例 弹幕效果

```js
$(function () {
  
  //注册事件
  var colors = ["red", "green", "hotpink", "pink", "cyan", "yellowgreen", "purple", "deepskyblue"];
  $("#btn").click(function () {
    var randomColor = parseInt(Math.random() * colors.length);
    var randomY = parseInt(Math.random() * 400);
    
    $("<span></span>")//创建span
      .text($("#text").val())//设置内容
      .css("color", colors[randomColor])//设置字体颜色
      .css("left", "1400px")//设置left值
      .css("top", randomY)//设置top值
      .animate({left: -500}, 10000, "linear", function () {
        //到了终点，需要删除
        $(this).remove();
      })//添加动画
      .appendTo("#boxDom");
    
    //清空文本框中的值
    $("#text").val("");
  });
  
  
  $("#text").keyup(function (e) {
    if (e.keyCode == 13) {
      $("#btn").click();
    }
  });
  
});
```

![](E:\jQuery\image\danmu.png)





# jQuery 第三天



## 特殊属性操作

### val （）方法

能够获取表单，文本域的value的值，当然value的值通过attr （属性）也可以获取，但是jQuery给我们提供了更简单的方法，获取value的值

```js
$("#btn").attr("value");

$("#btn").val("");  //不传参数获取
```

但是val （）传参数的时候，也可以设置value的值

```
$("#btn").val("哈哈");
```

案例 ：文本框提示文本

```js
$("#txt").focus(function () {
  //如果是默认值，清空内容
  if($(this).val() === "洋酒"){
    $(this).val("");
  }
});

$("#txt").blur(function () {
  if($(this).val() === ""){
    $(this).val("洋酒");
  }
});
```

![](E:\jQuery\image\val.png)

### html （）和  text （）

html （）和 text （）分别对应 js中的innerHTML （）和  innerText （）；

特点和使用和innerHTML （）和  innerText （）一模一样， 在设置的时候，html （）可以中添加识别标签 

text （）不识别标签； 在获取的时候，html（）获取的是对象下面的所有子内容 包括标签也会获取 ， 而text 

（）只会把文本获取， 不会获取里面的标签

```js
<div><h3>我是标题</h3></div>

console.log($("div").html());//<h3>我是标题</h3>
console.log($("div").text());//我是标题
```



### width （）和  height （）

对于 标签的width 和height 通过css（）也可以获取并就行设置 但是同样jQuery也给我们提供了更直接的方法获取的设置标签的width和height 

css方法获取的是字符串 ，而width （）获取的数字类型更方便操作	

```js
//console.log($("div").css("width"));
//$("div").css("width", "400px");
```

### width（）和height（）系列的方法

width （）不传参数时获取，传参数就输设置元素的width

width（）获取的就是 width

innerWidth（）获取元素的 padding+width

outWidth （）获取的是padding+width+border   //方法里的参数默认是false

outWidth （true）获取的是padding+width+border+margin

```js
//console.log($("div").width());//width   就是获取的width的值
//console.log($("div").innerWidth());//padding+width
//console.log($("div").outerWidth());//padding+width+border
//console.log($("div").outerWidth(true));//padding+width+border+margin

在设置时，width的参数也要是数字类型
//$("div").width(400);
```

案例 

```js
window下面的一个方法onresize(); 在jq中把on去掉就行，当调整浏览器窗口的大小时，发生 resize 事件。

//需要获取页面可视区的宽度和高度
$(window).resize(function () {
  console.log($(window).width());
  console.log($(window).height());
});
```



## scrollTop （）和scrollLeft （）

获取元素相对于窗口顶部向上滚动出去的top和left值，也可以设置相对于窗口顶部向上滚动的值

不传参数时获取，传参数时设置

> 可获取可设置
>
> **pageXOffset 和 pageYOffset 只能获取不能设置**

```js
//相当于窗口顶部卷曲出去的值
$(window).scrollTop(400);
console.log($(window).scrollTop());//400
```

案例  固定导航

```js
$(window).scroll(function () {
  //判断卷去的高度超过topPart的高度
  //1. 让navBar有固定定位
  //2. 让mainPart有一个marginTop
  if($(window).scrollTop() >= $(".top").height() ){
    $(".nav").addClass("fixed");
    $(".main").css("marginTop", $(".nav").height() + 10);
  }else {
    $(".nav").removeClass("fixed");
    $(".main").css("marginTop", 10);
  }
  
});
```

![](E:\jQuery\image\scroll.png)

案例 下火箭返航

```js
//当页面超出去1000px的时候，让小火箭显示出来,如果小于1000，就让小火箭隐藏
$(window).scroll(function () {
  if($(window).scrollTop() >= 1000 ){
    $(".actGotop").stop().fadeIn(1000);
  }else {
    $(".actGotop").stop().fadeOut(1000);
  }
});
```

![](E:\jQuery\image\huojian.png)

## offset（）和 position （）

offset 方法时获取针对于浏览器窗口而言的left 和top 的值

position 方法时获取针对于**最近的带有定位的父级元素**的left 和 top 的值

```html
<div class="father">
  <div class="son"></div>
</div>

<script>
	//获取元素的相对于document的位置
    console.log($(".son").offset()); / {top: 200, left: 200}
    
	//获取元素相对于有定位的父元素的位置
    console.log($(".son").position()); /{top: 100, left: 100}
</script>
```



## jQuery事件的发展机制

### 注册简单事件

缺点：一次只能够一个对象注册事件

`.click ()  `方式是只能注册单个事件

`.bind () `方法能够为同一对象注册多个事件

> 事件类型可以注册多个 , 中间以空格隔开 , 也可以传对象, 以键值对的形式 , 传不同的事件名 , 和事件处理函数

```js
//bind方式
$("p").bind({
  click:function () {
    alert("呵呵")
  },
  mouseenter:function () {
    alert("哈哈")
  }
});
```

### 委托事件 （delegate）

委托事件给元素的父元素添加，子元素没有这个事件，当子元素发生相应的事件时，通过事件冒泡给父元素，父元素就会把事件给符合条件的子元素

**语法**

> 事件类型可以写多个 , 中间以空格隔开
>
> 委托子元素可以写 多个子元素(并集选择器), 但是不推荐, 在解绑的时候会出问题

```js
parentNode.delegate('委托的子元素', '事件类型', [data], 事件处理函数) 
```

优点：能够给通过动态给后添加的子元素有相应的事件 ，并且事件只需要注册一次

```js
 	//要给div注册一个委托事件,但是最终不是由执行，而是有p执行
    //第一个参数：selector:事件最终由谁来执行。
    //第二个参数：事件的类型
	//实际第三个参数时data，没有什么用
    //第三个参数：函数，要做什么
$("#box").delegate("p", "click", function () {
  //alert("呵呵");
  console.log(this);
});
```



## on（）注册事件

在jQuery 1.7版本以后，为元素注册事件都统一为on （），on（）可以注册简单事件也可以注册委托事件

**语法**

**注册委托事件**

```js
parentNode.on('事件类型', '委托的后代元素', [data], 事件处理函数)
```

**给自己注册事件**

```js
Obj.on('事件类型', [data] , 事件处理函数)
```

**参数**

on （）中的参数 有四个

type ：事件的类型

selector : 事件委托的对象 ，不传就是给自己注册

data ：事件参数 e 中的属性data  , 必须使用`e.data`  获取传入的数据 , 传入的是一个**对象**

fn : 事件处理函数

```js
//委托事件
$("div").on("click", "p", function () {
    
    /委托事件的this指向委托的对象
  alert("呵呵")
});

//给自己注册事件
$("#btn").on("click", function () {
  $("<p>我是新建的p元素</p>").appendTo("div");
});
$('#btn').on()
```



## parents()

能够获取当前元素的所有父辈元素, 返回一个JQ伪数组

**参数**

- 指定的父级元素

```js
childNode.parents('父级元素')
```



## 事件的执行顺序

对于一个对象有多个事件时，首先执行自己的事件，然后才会执行委托事件 ，最后执行冒泡给父元素的事件



## 移除事件绑定 （off）

**常用off解绑事件和委托事件**

**解绑普通事件**

简单事件没有解绑的API

- off （''）方法可以移除事件绑定，可以移除多个事件，也可以移除指定事件

```js
obj.off('click   mouseenter') //移除特定事件
```

- off （）解绑全部事件    

**解绑委托事件**

`parentObj.off('事件类型', 后代元素(选择器), [fn])`

```js
#解绑指定后代元素的委托事件
parentObj.off('click', 'p')
parentObj.off('click mouseenter', 'p')

#解绑所有后代元素的委托事件
parentObj.off('click', '**')
```



**不常用的解绑API**



## 触发事件 （trigger）

trigger ：触发

```js
obj.trigger('需要触发的事件')
```

toggle ：切换

```js
$("#btn").on("click",function () {
    
  //触发p元素的点击事件  两种大师都可以触发p元素的点击事件
  //$("p").click();
  //$("p").trigger("click");
});
```



**键盘触发钢琴案例**

```js
 $(function () {    
      
      //给li注册鼠标进入事件,让li下面的span top：0  播放音乐
      $(".nav li").mouseenter(function () {
        $(this).children("span").stop().animate({top: 0});
        //播放音乐
        var idx = $(this).index();
        $(".nav audio").get(idx).load();
        $(".nav audio").get(idx).play();
      }).mouseleave(function () {
        $(this).children("span").stop().animate({top: 60});
      });
         
      
      //定义一个节流阀
      var flag=true;
      
      $(document).keydown(function (e) {
        if (flag){
          flag=false;
          if (e.keyCode>=49&&e.keyCode<=55){
            $('.nav li').eq(e.keyCode-49).trigger('mouseenter');
          }
        }
        
      });
      
      //当键盘抬起时,使flag = true
      $(document).keyup(function (e) {
        flag=true;
        if (e.keyCode>=49&&e.keyCode<=55){
          $('.nav li').eq(e.keyCode-49).trigger('mouseleave');
        }
      });
      
    });
```





## 事件对象 （e）

在jQuery中也有事件函数对象 e , 对原生的事件对象`e` 进行了一次兼容性处理 

在on（）中第三个参数是data  这个data就是e 的一个属性

```
//on(types, selector, data, callback)
```

data的作用 ：在事件中想要传某个数据data就可以通过事件函数对象e.data

```js
var money = 100;
//on(types, selector, data, callback)
//使用on方法的时候，可以给data参数传一个值，可以在事件里面通过e.data获取到。
$("div").on("click",100, function (e) {
  console.log(e);
  console.log("哈哈，我有"+e.data);
});
```

#### 事件对象e下方法和属性

**offset(offsetX与offsetY)坐标:相对于事件源的XY坐标.**

**screen（screenX与screenY）坐标：屏幕的左上角到我触发点的距离**

**client（clientX与clientY）坐标：浏览器可视区域的左上角距离触发点的距离**

**page（pageX与pageY）坐标：不管浏览器是否滚动，都是距离浏览器左上角的距离**

![](E:\jQuery\image\事件对象e.png)

## 阻止事件冒泡和浏览器的默认行为

e . stopPropagation （）可以阻止阻止事件冒泡

e . preventDefault  （）可以阻止浏览器的默认行为

return   false   既能够阻止事件冒泡， 也能够阻止浏览器分默认行为

**注意**

> return false 万能阻止 , 但是不推荐

## 链式编程

链式编程并不是可以一直链式下去，当是设置性操作的时候可以继续链式下去，设置操作返回的还是当前的jq对象

当时获取操作时和还找亲戚，不能链式，因为获取操作可以会返回字符串数值，或者其他jq对象，改变了当前的jq对象就不能再继续链式下去

**总结 :**

- 设置性操作可以继续链式编程
- 获取性操作和找亲戚元素后, 不能继续链式编程-----------> `end()` 应运而生

案例 五星好评

- `prevAll()`  获取元素前面的所有兄弟元素
- `nextAll()`  获取元素后面所有兄弟元素

```js
$(function () {
  
  //1. 给li注册鼠标经过事件，让自己和前面所有的兄弟都变成实心
  var wjx_k = "☆";
  var wjx_s = "★";
  $(".comment>li").on("mouseenter", function () {
    $(this).text(wjx_s).prevAll().text(wjx_s);/此处就不能继续链式，因为prevall()获取当前对象的前面的所有对象，返回的就是当前对象前面所有的对象，不在是this这个对象
    $(this).nextAll().text(wjx_k);
  });
  
  //2. 给ul注册鼠标离开时间，让所有的li都变成空心
  $(".comment").on("mouseleave", function () {
    $(this).children().text(wjx_k);
    
    //再做一件事件，找到current，让current和current前面的变成实心就行。
    $("li.current").text(wjx_s).prevAll().text(wjx_s);
  });
  
  //3. 给li注册点击事件
  $(".comment>li").on("click", function () {
      //打标记
    $(this).addClass("current").siblings().removeClass("current");
  });
  
  
});
```

### end （）方法

在链式编程中jQuery在获取操作返回对象时，还做了另外一件事，当返回的jq对象改变时，jQuery会把上一次的jq对象保存在返回对象的 `prevObject ` 这个属性中 ，如果想继续链式编程下去可以使用end （）方法改变当前的jq对象，转换成上一个对象继续链式编程

```js
$(".comment>li").on("mouseenter", function () {
    //$(this).text(wjx_s).prevAll().text(wjx_s);
    //$(this).nextAll().text(wjx_k);
    $(this).text(wjx_s).prevAll().text(wjx_s).end ().nextAll().text(wjx_k);
  });
```



### each （）方法

jQuery遍历是隐士迭代，只能设置同样的属性样式，对于需要不同样式的设置，还需要for循环，这时候我们可以使用for循环，也可以使用each （）方法，对jq对象设置不同的属性样式

jquery的`each` 方法不仅可以用来遍历 jQuery对象, 效果和原生JS的array对象的`foreach()`类似

each （）中的参数  fn 

> index ：每个操作元素的索引
>
> dom ：要操作的元素  **这个形参是dom对象**

可以使用`return false` 跳出each 循环

```js
$("li").each(function (index, dom) {
  $(dom).css("opacity", (index+1)/10);
})
```



## `$`冲突的问题

在jQuery中使用在其他语言中也有可能是使用 $  就会出现冲突

在jQuery中可以使用jQuery代替$ 但是不方便与程序员写代码

当jQuery获得的使用权时，可以释放$ 的控制权，用一个变量替代 

```html
<script src="itcast.js"></script>
<script src="jquery-1.12.4.js"></script>
//jQuery释放$的控制权
var $$=$.noConflict();
```





# jQuery 第四天



## jQuery插件原理

给 jQuery的原型中添加一个方法，  $中的原型是fn,只要把方法添加到fn中，jQuery对象就有这个方法，jq对象就可调用这个方法



## jQuery常用插件

jquery功能性插件网站 `Jq22` :[jQuery插件网站](http://www.jq22.com)

依赖性插件 : 依赖于某个库或者语言扩展的插件

### jQuery.color.js

jQuery插件中的一些方法还是基于jQuery，所有引入jQuery插件需要在jQuery后面引入

jQuery不支持颜色的渐变，animate动画函数，不能实现颜色的渐变，这个插件就可以实现颜色的渐变

```js
<!--1. 引入jquery的js文件-->
<script src="jquery-1.12.4.js"></script>
<!--2. 引入插件的js文件-->
<script src="jquery.color.js"></script>
//说明jquery不支持颜色的渐变,颜色最好用16进制
$('div').animate({backgroundColor:"#ffc0cb"}, 3000, function () {
        alert("呵呵");
    });
```



### jQuery. lazyload.js  

在一些比较长的页面中，如果有许多图片，全部加载需要很长的时间这样就会影响用户体验，可以使用懒加载技术

让页面下面的图片暂时不加载，当用户滑到时在把图片加载出来

需要给img 添加一个data-original="  " ，代替src属性  通常还会加一个类，方便统一管理

```js
<img class="lazy" data-original="02.gif" alt="">
```

```js
//使用时 ：
<script src="jquery-1.12.4.js" type="text/javascript"></script>
<script src="jquery.lazyload.js" type="text/javascript"></script>
<script>
  //直接调用lazyload方法即可
  $(function () {
  
    $("img.lazy").lazyload();
  
  });
```