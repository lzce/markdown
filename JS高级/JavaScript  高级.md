# JavaScript  高级第一天



## 相关书籍

- JavaScript 高级程序设计（第三版）
  - 前端的红宝书
  - 建议每一个前端都完整的看一遍

- JavaScript 权威指南
  - 前端的圣经
- JavaScript面向对象编程指南（第2版）
- JavaScript面向对象精要

- JavaScript 语言精粹
- 你不知道的 JavaScript



## 面向对象编程

面向对象编程 —— Object Oriented Programming，简称 OOP ，是一种编程开发思想。

在面向对象程序开发思想中，每一个对象都是功能中心，具有明确分工，可以完成接受信息、处理数据、发出信息等任务。
因此，面向对象编程具有灵活、代码可复用、高度模块化等特点，容易维护和开发，比起由一系列函数或指令组成的传统的过程式编程（procedural programming），更适合多人合作的大型软件项目。



### 面向对象与面向过程

- 面向过程就是亲历亲为，事无巨细，有条不紊，面向过程是解决问题的一种思维方式，（**执行者的角度**）
  - 关注点在于解决问题的过程（先xx，然后xx，在xx）；
- 面向对象就是找一个对象，让她去做这件事情（**指挥者的角度**）
  - 关注点在找到能解决问题的对象上。
- 面向对象不是面向过程的替代，而是面向过程的封装
- 例如洗衣服（面向过程和面向对象的区别）



### 面向对象的特性

- 封装性
  - 将功能的具体实现，全部封装到对象的内部，外界使用对象时，只需要关注对象提供的方法如何使用，而不需要关心对象的内部具体实现，这就是封装。
- 继承性
  - 在js中，继承的概念很简单，一个对象没有的一些属性和方法，另外一个对象有，拿过来用，就实现了继承。
  - **注意：在其他语言里面，继承是类与类之间的关系，在js中，是对象与对象之间的关系。**
- [多态性]
  - 多态是在强类型的语言中才有的。js是弱类型语言，所以JS不支持多态



## 什么是对象？

> Everything is object （万物皆对象）



对象到底是什么，我们可以从两次层次来理解。

**(1) 对象是具体事物的抽象。**

一本书、一辆汽车、一个人都可以是对象，当实物被抽象成对象，实物之间的关系就变成了对象之间的关系，从而就可以模拟现实情况，针对对象进行编程。

问： 书是对象吗

**(2)对象是无序键值对的集合，其属性可以包含基本值、对象或者函数**

每个对象都是基于一个引用类型创建的，这些类型可以是系统内置的原生类型，也可以是开发人员自定义的类型。



## 创建对象的三种方式

### 字面量的方式

```js
var per1={
    name:"卡卡西",
   age:20,
   sex:"男",
   eat:function () {
     console.log("吃臭豆腐");
   },
```

### 调用系统的构造函数

```js
 var per2=new Object();
 per2.name="大蛇丸";
 per2.age=30;
 per2.sex="男";
 per2.eat=function () {
 console.log("吃榴莲");
 };
```

### 自定义构造函数创建对象

```js
function Person(name,age,sex) {
  this.name=name;
  this.age=age;
  this.sex=sex;
  this.play=function () {
    console.log("天天打游戏");
  };
}
var per=new Person("雏田",18,"女");
console.log(per instanceof Person);
```

自定构造函数时做的四件事情

```js
/* 1.开辟空间存储对象
* 2.把this设置为当前的对象
* 3.设置属性和方法的值
* 4.把this对象返回
```

## 工厂模式创建对象

原理: 将创建对象的方法封装成一个函数,调用这个函数,并且传值即可创建对象,创建对象的原理还是调用系统的构造函数创建对象



### 自定义构造函数和工厂模式创建对象的区别 

```js
/*
* 共同点:都是函数,都可以创建对象,都可以传入参数
*
* 工厂模式:
* 函数名是小写
* 有new,
* 有返回值
* new之后的对象是当前的对象
* 直接调用函数就可以创建对象
*
* 自定义构造函数:
* 函数名是大写(首字母)
* 没有new
* 没有返回值
* this是当前的对象
* 通过new的方式来创建对象
```

```js
/*一个是普通函数一个构造函数*/
function createObject(name,age) {
  var obj=new Object();
  obj.name=name;
  obj.age=age;
  obj.sayHi=function () {
    console.log("您好");
  };
  return obj;============>需要返回值
}
function Person(name,age) {
  this.name=name;
  this.age=age;
  this.sayHi=function () {
    console.log("您好");
  };================可以不写返回值
}

var obj1=new Person();
var obj2=creatObject();
```

## 构造函数和实例对象之间的关系

```js
/*
实例对象是通过构造函数创建的
构造函数中的属性和方法,在实例的对象中有,而在构造函数中没有
```

## 原型

### 出现的背景

在自定义构造函数中, 成员方法如果写在构造函数中 , 在实例化对象的时候, 就会重复创建方法 , 函数是复杂数据类型 ,  会在堆中开辟一块空间存储 , 大量实例化对象就会造成内存空间浪费	

### 原型的概念

`__proto__` 是谷歌的私有属性 , 存在兼容问题 

在实例对象中都有`__proto__` 这个属性--->也叫原型,也是一个对象,这个属性一般是给浏览器使用的,不是标准属性

在任意函数中 , 一般针对构造函数都有`prototype`这个属性--->也叫原型,也是一个对象,这个属性是给程序员用的,是标准属性

实例对象中的`___proto___ ` 和 构造函数中的 __prototype __相等====true

`__proto__`是实例对象中的一个属性,而 prototype是构造函数中的一个属性

### 原型的作用

共享属性和方法,节省内存空间

### 三者的区别

构造函数(麻麻) ---------------------------> 原型对象 (粑粑)

实例对象(孩子)

![](images\三者之间的关系.png)

总的来说:

先有构造函数,有了构造函数才会有prototype这个属性,这个属性中的一些方法和属性是可以共享的,

实例化对象中没有这个属性和方法但是可以直接调用这些属性和方法,实例化对象中的proto属性的地址指向和构造

函数中的prototype的地址指向相同都是堆中那块相同的代码

构造函数的原型对象的constructor(构造器)指向的是构造函数(自己)



### 构造函数和实例对象和原型之间的关系

构造函数中的原型对象和实例化对象中的原型对对象指向的是同一个地址,是相同的,所有实例对象可以调用构造函数中原型的方法

构造函数中的属性和方法,在输出的时候是没有的,在实例化对象中有构造函数的属性和方法,在实例化过程中,把构造函数的属性和方法给了实例化对象

```js
/*  构造函数可以实例化对象
* 构造函数中有一个属性叫prototype,是构造函数的原型对象
* 构造函数的原型对象(prototype)中有一个constructor构造器,这个构造器指向的就是自己所在的原型对象所在的构造函数
* 实例对象的原型对象(__proto__)指向的是该构造函数的原型对象
* 构造函数的原型对象(prototype)中的方法是可以被实例对象直接访问的
```



### constructor 构造器

**构造函数中的原型对象自带的属性 , 其属性值指向当前的构造函数**

实例对象和构造函数之间没有直接的关系 , 但是可以通过原型对象的`constructor` 属性间接和构造函数建立关系

```js
console.log(Person.prototype.constructor)
	=> f Person () {
        
    }
```



### 原型的写法

```js

//第一种写法======相当于给原型添加属性和方法
Student.prototype.height="188";
Student.prototype.weight="55kg";
Student.prototype.study=function () {
  console.log("学习,写500行代码,小菜一碟");
};
Student.prototype.eat=function () {
  console.log("吃一个10斤的西瓜");
};
//实例化对象,并初始化
var stu=new Student("晨光",57,"女");
console.dir(Student);
console.dir(stu);

//原型既然是个对象则可以写在一个{}之中
 //简单的原型写法================相当于重新定义原型
    Student.prototype = {
      //手动修改构造器的指向
      constructor:Student,==========================>注意:要手动添加构造器
      height: "188",
      weight: "55kg",
      study: function () {
        console.log("学习好开心啊");
      },
      eat: function () {
        console.log("我要吃好吃的");
      }
    };
```

## 体会面向对象

```js
/*点击按钮设置div的属性样式*/
<input type="button" value="显示效果" id="btn"/>
<div id="dv"></div>

//面向过程====亲力亲为
 document.getElementById("btn").onclick=function () {
       document.getElementById("dv").style.backgroundColor="yellow";
  };

//面向对象的思想
//在函数的形参中传入按钮对象和div对象和要设置的样式对象
 function ChangeStyle(btnObj, dvObj, json) {
    this.btnObj = btnObj;================>this指代当前实例化的对象`
    this.dvObj = dvObj;
    this.json = json;
  }
//在构造函数的原型中添加init方法
  ChangeStyle.prototype.init = function () {
    //点击按钮,改变div多个样式属性值
    var that = this;   //======that/this指代 的是实例化的对象
    this.btnObj.onclick = function () {//按钮
      for (var key in that.json) {
        that.dvObj.style[key] = that.json[key];
      }
    };
  };
```

## 原型中的方法可以互相调用

```js
function Animal(name,age) {
  this.name=name;
  this.age=age;
}
//原型中添加方法
Animal.prototype.eat=function () {
  console.log("动物吃东西");
  this.play();
};
Animal.prototype.play=function () {
  console.log("玩球");
  this.sleep();
};
Animal.prototype.sleep=function () {
  console.log("睡觉了");
};

var dog=new Animal("小苏",20);
dog.eat();
```

## 实例化对象使用的属性和方法规则

```js
/*
实例化对象在调用属性和方法时,首先在自己的实例对象中查找,自己有则使用自己的,当自己没有时,原型对象中有,则使用原型对象的,当自己和原型对象中都没有的时候则户报错
```

## 为内置对象添加原型方法

为内置对象添加原型方法则相当于在修改内置对象的方法,或为内置对象添加方法

```js
String.prototype.myReverse=function () {
  for(var i=this.length-1;i>=0;i--){
    console.log(this[i]);
  }
};
var str="abcdefg";
str.myReverse();
```

## 把局部变量变成全局变量

在自调用函数中,传入window,js是一门动态类型的语言没有这个属性的时候,点了就有这个属性了,把局部变量(属性,对象),暴露给window,传给window就可以变成全局变量

```js
(function (window) {====?形参
     var num=10;//局部变量
     //js是一门动态类型的语言,对象没有属性,点了就有了
     win.num=num;
   })(window);====>实参
   console.log(num);

	//window.num 则window就有这个属性了并且把10赋给了num这个属性,在外面访问num实际上是window.num 但是window可以省略

```

### 案例 

通过自调用函数产生一个随机数对象,在自调用函数外面,调用该随机数对象方法产生随机数

```js
(function (window) {
      //产生随机数的构造函数
      function Random() {
      }
      //在原型对象中添加方法
      Random.prototype.getRandom = function (min,max) {
        return Math.floor(Math.random()*(max-min)+min);
      };
      //把Random对象暴露给顶级对象window--->外部可以直接使用这个对象
      window.Random=Random;
    })(window);
    //实例化随机数对象
    var rm=new Random();
    //调用方法产生随机数

```

随机产生小方块

```js
<div class="map"></div> //=================>地图 (需要脱标)

//产生随机数对象的
  (function (window) {
    function Random() {
    }
    Random.prototype.getRandom=function (min,max) {
      return Math.floor(Math.random()*(max-min)+min);
    };
    //把局部对象暴露给window顶级对象,就成了全局的对象
    window.Random=new Random();===============>Random此时是全局变量
  })(window);//自调用构造函数的方式,分号一定要加上

	//产生小方块对象
  (function (window) {
    //console.log(Random.getRandom(0,5));
    //选择器的方式来获取元素对象
    var map=document.querySelector(".map");

    //食物的构造函数
    function Food(width,height,color) {
      this.width=width||20;//默认的小方块的宽
      this.height=height||20;//默认的小方块的高
      //横坐标,纵坐标
      this.x=0;//横坐标随机产生的
      this.y=0;//纵坐标随机产生的
      this.color=color;//小方块的背景颜色
      this.element=document.createElement("div");//小方块的元素
    }
      
    //初始化小方块的显示的效果及位置---显示地图上
    Food.prototype.init=function (map) {
      //设置小方块的样式
      var div=this.element;
      div.style.position="absolute";//脱离文档流
      div.style.width=this.width+"px";
      div.style.height=this.height+"px";
      div.style.backgroundColor=this.color;
      //把小方块加到map地图中
      map.appendChild(div);
      this.render(map);
    };
      
    //产生随机位置
    Food.prototype.render=function (map) {
      //随机产生横纵坐标
      var x=Random.getRandom(0,map.offsetWidth/this.width)*this.width;
      var y=Random.getRandom(0,map.offsetHeight/this.height)*this.height;
      this.x=x;
      this.y=y;
      var div=this.element;
      div.style.left=this.x+"px";
      div.style.top=this.y+"px";
    };
      
      //实例化对象
    var fd=new Food(20,20,"green");
    fd.init(map);
    console.log(fd.x+"===="+fd.y);
```



# JavaScript 高级 (第二天)



## 贪吃蛇案例

__思路:__

```css
//模拟贪吃蛇游戏,做的项目
/*
*
* 地图: 宽，高，背景颜色，因为小蛇和食物都是相对于地图显示的,这里小蛇和食物都是地图的子元素,随机位置显示,脱离文档流的,地图也需要脱离文档流--css需要设置:宽,高,背景颜色,脱标
*
* 食物---div元素
* elements--->存储div的数组(将来删除的食物div时候,先从map中删除div,再从数组中移除div)
* 食物:宽,高,背景颜色,横坐标,纵坐标
* 一个食物就是一个对象,这个对象有相应的属性,这个对象需要在地图上显示
* 最终要创建食物的对象,先 有构造函数,并且把相应的值作为参数传入到构造函数中
* 食物要想显示在地图上,食物的初始化就是一个行为
* 1.食物的构造函数--->创建食物对象
* 2.食物的显示的方法-->通过对象调用方法,显示食物,设置相应的样式
* 2.1.1 因为食物要被小蛇吃掉,吃掉后应该再次出现食物,原来的食物就删除了
* 2.1.2 每一次初始化食物的时候先删除原来的食物,然后重新的初始化食物
* 2.1.3 通过一个私有的函数(外面不能调用的函数)删除地图上的食物,同时最开始的时候食物也相应的保存到一个数组中,再从这个数组中把食物删除
* 最后的时候,把食物的构造函数给window下的属性,这样做,外部就可以直接使用这个食物的构造函数了
*
* 小蛇
* 小蛇就是一个对象
* 属性: 每个身体都有宽，高，方向
* 属性:身体分三个部分,每个部分都是一个对象,每个部分都有横纵坐标,背景颜色
* 小蛇要想显示在地图上,先删除之前的小蛇,然后再初始化小蛇(小蛇要移动)--方法
*
* 小蛇要移动---方法
* 思路:把小蛇的头的坐标给小蛇第一部分的身体,第一部分的身体的坐标给下一个部分身体
* 小蛇的头,需要单独的设置:方向
*
```


**能够输出对象的结构**

**console.dir(对象)**



# JavaScript 高级 第二天



## 原型

### 原型的作用和目的

一 数据共享===========>节省内存空间

二  继承===============>节省内存空间

### 原型及原型链

只要是函数都有prototype原型    只要是对象都有`__proto__  `原型 ,   对象的`__proto__`原型指向构造函数的原型对象prototype

构造函数既是函数又是对象 ,所以构造函数中有prototype 又有 __ proto __ , 构造函数作为对象时,它的构造函数则是大写的Function, Function中有__protoype__,但是没有__ proto __原型

```css
/*
构造函数能够创建实例对象,但实例对象和构造函数并无直接的关系
构造函数中prototype指向原型对象,原型对象中的constructor又指向自己的构造函数
实例对象的__ proto__指向构造函数的原型对象
构造函数中的prototype 和 实例对象中的 __ proto__ 的指向是相同 都是构造函数的原型对象	
```

## 原型链

### 什么是原型链

对象有`__proto__`指向了原型对象, 原型对象也是对象, 也有`__proto__` 指向了原型对象的原型对象, 这样形成的链式关系就是原型链

原型链是一种关系: **实例对象和原型对象之间的一种关系**是通过 __ proto__(原型)进行联系的

![](images\原型及原型链.png)



### 原型链的最终的指向

任何对象原型对象的最终的指向都指向`Object.prototype`

```js
Persion.protype.__proto__ === Object.project
Object.project.__proto__ === null
```



![](images\原型最终的指向.png)

```js
function Person() {

}
Person.prototype.eat=function () {
  console.log("吃东西");
};

var per=new Person();
/*
实例对象的 per.__ proto__ 指向 构造函数 Person.prototype
构造函数中的prototype也是一个对象,那么 Person.prototype.__ proto__ 指向的则是Object.prototype
object.prototype也是对象  object.prototype.__ proto__的指向为null
所以说原型的最终指向都是object.prototype

console.log(per.__proto__==Person.prototype);
console.log(per.__proto__.__proto__==Person.prototype.__proto__);
console.log(Person.prototype.__proto__==Object.prototype);
console.log(Object.prototype.__proto__);
```



### 内置对象的原型链

内置对象都是`Function`的实例对象

Array , Date 内置对象

**找爸爸**

```js
Array.prototype ==> Object.prototype ==> null
Date.prototype ==> Object.prototype ==> null
```

Math

Math不是一个构造函数 , 本身就是一个实例对象, 不能new

```js
Math.__proto__ ==> object.prototype ==>  object.prototype ==> null
```



### 属性查找原则

> 记忆技巧: 自己有则找自己的 ,  自己没有找爸爸的

- 实例对象`.属性` , 首先会在自己身上找是否有**该属性**

- 自己身上没有, 就会去构造函数的原型对象身上找, 如果有就返回属性值
- 如果原型对象上也没有, 就会原型链上找, 一直找到`Object.prototype`, 如果没有就返回`undefined`

```js
function Persion(name, gender) {
    this.name = name,
    this.gender = gender
}

Persion.prototype.gender = 'male'
var p = new Persion()
#自己身上有, 但是没有传参
console.log(p.name) // undefined
console.log(p.gender) // undefined
```



### 属性设置原则

> 记忆技巧: 有就覆盖, 没有就添加

- 对于自己身上有的属性 , 在设置的时候, 会改变自己身上的属性值, 不会改变原型对象身上的属性值
- 对于自己身上没有的属性, 在`obj.属性`的时候, 会在自身添加一个属性并赋值 **(JS是一门动态类型的语言)**
  - 不会影响原型对象身上的属性



### 原型指向改变如何添加方法

指向改变,添加属性和方法,可以在指向改变后,添加属性和方法

```js
//改变了原型对象的指向
//    Student.prototype=new Person(10);
//    //学生的原型中添加方法----后在原型中添加方法
//    Student.prototype.sayHi=function () {
//      console.log("您好哦");
//    };
//    var stu=new Student("男");
//    stu.eat();
//    stu.sayHi();
```

### 原型的指向可以改变

```json
/*
实例对象中的原型指向的是该对象的构造函数中的prototype , 当构造函数中的prototype的指向发生改变,实例对象中的 __ proto__的指向也会发生改变

实例对象和原型对象之间的关系就是通过__ proto__原型联系起来的,这个关系就是原型链


//人的构造函数
    function Person(age) {
      this.age=10;
    }
    //人的原型对象方法
    Person.prototype.eat=function () {
      console.log("人的吃");
    };
    //学生的构造函数
    function Student() {

    }
    Student.prototype.sayHi=function () {
      console.log("嗨,小苏你好帅哦");
    };
    //学生的原型,指向了一个人的实例对象=======>学生的__ proto__指向了实例对象 new Person();
    new Person()是一个实例对象,指向Person.prototype
    Student.prototype=new Person(10);
    var stu=new Student();
    stu.eat();
    stu.sayHi();
```

![](images\原型链指向改变.png)



![](images\原型链的图解.png)



### 实例对象和原型对象属性重名问题

两者不冲突 , 实例对象访问这个属性,应该先从实例对象中找,找到了就直接用，找不到就去指向的原型对象中找,找到了就使用 ,    找不到就报错

```js
function Person(age,sex) {
  this.age=age;
  this.sex=sex;
}
Person.prototype.sex="女";
var per=new Person(10,"男");
console.log(per.sex);=============>男

/*通过实例对象能否改变原型对象中的属性值?不能
就想改变原型对象中属性的值,怎么办?直接通过原型对象.属性=值;可以改变
```



### 神奇的原型链

```js
var divObj=document.getElementById("dv");
console.dir(divObj);

//divObj.__proto__---->HTMLDivElement.prototype的__proto__
// --->HTMLElement.prototype的__proto__
// --->Element.prototype的__proto__
// ---->Node.prototype的__proto__
// ---->EventTarget.prototype的__proto__
// ---->Object.prototype没有__proto__,所以,Object.prototype中的__proto__是null
```



### Object.prototype原型对象上的常用成员

任何原型对象,沿着原型链总会找到`Object.prototype` 来使用这个原型对象上的成员

#### hasOwnProperty()

> 判断这个属性是不是对象自身的

**语法:**

```js
对象.hasOwnProperty(属性)
```

**作用**

判断是否是自己的属性, 而不是原型链上的方法 , 有则返回`true` 无则返回`false

 ```js
function Persion(name) {
    this.name = name
}
var p = new Persion('lw')
console.log(p.hasOwnProperty('name')) //true
console.log(p.hasOwnProperty('toString')) //false
console.log(p.hasOwnProperty('hasOwnProperty')) //false
 ```



**应用场景**

```js
function Persion(name) {
    this.name = name
}
Object.prototype.legs = '腿'
var p = new Persion('lw')
for(var key in p) {
    console.log(key)
}
//此时, legs 会被遍历到
```

在`for in` 遍历对象的时候, 会把对象自身的属性, 及原型链上的属性也会遍历

**但是**  对于Object自己的属性, **灰蓝色属性** , 不会被遍历





## 函数进阶

### 函数的角色

```js
//函数的角色:
//函数的声明
function f1() {
  console.log("我是函数");
}
f1();
//函数表达式
var ff=function () {
  console.log("我也是一个函数");
};
ff();
```

### 创建函数的三种方式

#### 函数声明和函数表达式

> 使用时没有什么区别

**区别**

> 函数声明 : 可以先调用 , 在声明
>
> 函数表达式 : 只能先声明, 在调用  ===> 由于预解析的原因, 声明提前, 赋值不会提升

```js
//函数声明如果放在if-else的语句中,在IE8的浏览器中会出现问题
if(true){
	function () {
    console.log("哈哈,我又变帅了");
  };
}else{
  	function () {
    console.log("小苏好猥琐");
  };
}

//在谷歌和火狐中输出的是 true中的函数结果
//而在IE8中输出的是else中的结果=========后面的函数层叠掉前面的函数

var ff;
    if(true){
      ff=function () {
        console.log("哈哈,我又变帅了");
      };
    }else{
      ff=function () {
        console.log("小苏好猥琐");
      };
    }
    ff();===============>IE 8 和谷歌输出相同
    
    //以后宁愿用函数表达式,都不用函数声明
```

#### Function=>创建函数=> JS一等公民

函数也是对象, 任何函数都是大写`Function`创建

函数(对象)也是构造函数创建出来的, 构造函数`Function`

**Function**

是JS中**唯一的**原型对象`prototype` 是一个函数  (当然函数也是对象)

**语法:**

```js
var newFn = new Function(arg1, arg2, ..., fnbody)
```

**参数**

- 参数类型都是字符串, 参数可以是若干个
- 最后一个参数`fnbody` 是新函数的函数体
- 除了最后一个参数, 其他参数都是新函数的**形参**

```js
var fn3 = new Function('n1', 'n2', 'alert(n1+n2)')

//相当于
var fn3 = function (n1, n2) {
    alert(n1+n2)
}
```

 ```js
浏览器控制台中的`anonymous` 就是匿名函数的意思
function anonymous() {
}
 ```



### 函数的原型链

函数也是对象, 那么函数设计谁生下来的?

函数都是`new Function` 出来的 

```js
Persion ==> Function.prototype ==> Object.prototype ==> null
```



![](images\函数的原型链.png)





### 严格模式

```js
//严格模式:
//在严格模式下,方法都需要对象.  普通函数是个方法需要 window.f1(); 否则就会出错
"use strict";//严格模式
function f1() {
  console.log(this);//window
}
f1();
```

### 函数的不同调用方式

**构造函数也是函数 和普通函数没什么区别,不过构造函数用来创建对象,所有用大写来区别普通函数 , 通过new 来创建对象**

```js
//普通函数
function f1() {
  console.log("文能提笔控萝莉");
}
f1();
```

```js
//构造函数---通过new 来调用,创建对象
function F1() {
  console.log("我是构造函数,我骄傲");
}
var f=new F1();
```

### 函数也是对象

函数是对象,但是对象不一样是函数

```js
 console.dir(Math);//中有__proto__,但是没有prorotype
```

函数中有prototype,但函数作为对象也有__ proto__ 

```js
//   如果一个东西里面有prototype，又有__proto__,说明是函数,也是对象
```

函数既然是对象,那么就有__ proto__ ,那么函数的 构造函数时 Function

所有的函数都是 Function 创建的实例对象

```js
 var f1=new Function("num1","num2","return num1+num2");
//    console.log(f1(10,20));==========>30
//    console.log(f1.__proto__==Function.prototype);
```

### 数组的函数调用

数组可以存储任何数据类型, 包括字符串类型,数字类型, 对象  ,  和 函数, 函数也是一种数据类型

```js
var arr=[
    function () {
      console.log("十一假期快乐");
    }
];
//回调函数:函数作为参数使用
    arr.forEach(function (ele) {
      ele();
    });
```



# 完整原型链

- 任何函数的原型链上都有`Function.prototype`

- 任何对象上的原型链上都有`Object.prototype`

- 函数也是函数, 也是对象
  - 既有`prototype`属性
  - 也有`__proto__`  属性
- 函数在JS中是**一等公民**
  - 大`Function` 是自己生自己
  - 大`Function`  的原型对象是一个函数
  - `typeof`  判断简单的数据类型
    - 对于复杂数据类型, `typeof` 都返回 字符串的`"object"`
      - `typeof 函数`  检测函数, 返回的结果 是字符串`"function"`



![](images\完整原型链.png)





### 补充 `instanceof`

- 判断构造函数的`prototype`属性是否在**对象的原型链**上, 如果在则返回`true` 否则返回`false`

**语法**

```js
对象 instanceof 构造函数
```

**作用**

判断对象是不是这个构造函数的实例

- 返回值 : `true or false`

```js
console.log( [] instanceof Array) //true
console.log( [] instanceof Object ) //true
```

### 面试题

```js
#前面是对象, 后面是构造函数
console.log(Function instanceof Function) //true
console.log(Function instanceof Object)   //true
console.log(Object instanceof Function)   //true
console.log(Object instanceof Object)     //true
```









# JavaScript 高级 第三天



## bind方法

apply和call是在调用的时候,改变this的指向,调用别人的方法,而bind是复制一份,参数可以在复制的时候传进去,也可以在复制之后传进去

复制一份的时候 , null表示默认还是window,

当使用bind方法后, 把别人的方法复制了一份,并且有返回值 , 返回值是复制后的这个方法或函数

```js
使用的语法:
/*
* 函数名字.bind(对象,参数1,参数2,...);---->返回值是复制之后的这个函数
* 方法名字.bind(对象,参数1,参数2,...);---->返回值是复制之后的这个方法
```

```js
function Person(age) {
      this.age=age;
    }
    Person.prototype.play=function () {
      console.log(this+"====>"+this.age);
    };

    function Student(age) {
      this.age=age;
    }
    var per=new Person(10);
    var stu=new Student(20);
    //复制了一份,  stu这个对象调用了play这个方法,并且this为stu这个实例对象
    var ff=per.play.bind(stu);
    ff();=========>[object Object]====>20
```

### bind方法的使用

```js
//通过对象,调用方法,产生随机数

function ShowRandom() {
  //1-10的随机数
  this.number=parseInt(Math.random()*10+1);
}
//添加原型方法
ShowRandom.prototype.show1=function () {
  //改变了定时器中的this的指向了,本来应该是window,现在是实例对象了
  window.setInterval(this.show2.bind(this),1000);
};
//添加原型方法
ShowRandom.prototype.show2=function () {
  //显示随机数--
  console.log(this.number);
};
//实例对象
var sr=new ShowRandom();
//调用方法,输出随机数字
//调用这个方法一次,可以不停的产生随机数字
sr.show1();
```



## 函数中的成员

```js
//函数中有一个name属性----->函数的名字,name属性是只读的,不能修改
//函数中有一个arguments属性--->实参的个数
//函数中有一个length属性---->函数定义的时候形参的个数
//函数中有一个caller属性---->调用(f1函数在f2函数中调用的,所以,此时调用者就是f2)
function f1(x,y) {
  console.log(f1.name);
  console.log(f1.arguments.length);
  console.log(f1.length);
  console.log(f1.caller);//调用者=====>f2
}

function f2() {
      console.log("f2函数的代码");
      f1(1,2);
    }
    f2();
```





## 高阶函数



### 函数作为参数使用

```js
//fn是参数,最后作为函数使用了,函数是可以作为参数使用
//可以传入命名函数也可以是匿名函数
//传入命名函数
function f1(fn) {
  console.log("f1的函数");
  fn();//此时fn当成是一个函数来使用的
}
function f2() {
     console.log("f2的函数");
}
 f1(f2);//======f1的函数  f2的函数
========================================================================
//传入匿名函数
f1(function () {
     console.log("我是匿名函数");
   });
```

案例

sort方法不稳定,需要加入一段代码

```js
var arr = [1, 100, 20, 200, 40, 50, 120, 10];
//排序---函数作为参数使用,匿名函数作为sort方法的参数使用,那么此时的匿名函数中有两个参数,
arr.sort(function (obj1,obj2) {
  if(obj1>obj2){
    return -1;//===================return 1; 则从小到大排序
  }else if(obj1==obj2){
    return 0;
  }else{
    return 1;
  }
});
console.log(arr);//=====[200, 120, 100, 50, 40, 20, 10, 1]


//排序字母
var arr1=["acdef","abcd","bcedf","bced"];
    arr1.sort(function (a,b) {
      if(a>b){
        return 1;
      }else if(a==b){
        return 0;
      }else{
        return -1;
      }
    });
    console.log(arr1);//=====["abcd", "acdef", "bced", "bcedf"]
```



### 函数作为返回值使用

```js
 function f1() {
     console.log("f1函数开始");
     return function () {    //函数作为返回值
       console.log("我是函数,但是此时是作为返回值使用的");
     }

   }
//
   var ff=f1();
   ff();
```

案例

```js
//判断这个对象和传入的类型是不是同一个类型
//获取某个对象的类型是不是你传入的类型
    //[10,20,30] 是不是"[object Array]"
    //type---是变量----是参数----"[object Array]"
    //obj---是变量-----是参数----[10,20,30];
function getFunc(type) {
  return function (obj) {
    return Object.prototype.toString.call(obj) === type;
  }
}

var ff = getFunc("[object Array]");//=======返回值是个函数 所以ff也是函数
var result = ff([10, 20, 30]);
console.log(result);

var ff1 = getFunc("[object Object]");
var dt = new Date();
var result1 = ff1(dt);
console.log(result1);
```

```js
//排序,每个文件都有名字，大小,时间,都可以按照某个属性的值进行排序
//三部电影,电影有名字,大小,上映时间
    function File(name, size, time) {
      this.name = name;//电影名字
      this.size = size;//电影大小
      this.time = time;//电影的上映时间
    }
    var f1 = new File("jack.avi", "400M", "1997-12-12");
    var f2 = new File("tom.avi", "200M", "2017-12-12");
    var f3 = new File("xiaosu.avi", "800M", "2010-12-12");
    var arr = [f1, f2, f3];

    function fn(attr) {
      //函数作为返回值
      return function getSort(obj1, obj2) {
        if (obj1[attr] > obj2[attr]) {
          return 1;
        } else if (obj1[attr] == obj2[attr]) {
          return 0;
        } else {
          return -1;
        }
      }
    }

    var ff = fn("name");

    //函数作为参数
    arr.sort(ff);
    for (var i = 0; i < arr.length; i++) {
      console.log(arr[i].name + "====>" + arr[i].size + "===>" + arr[i].time);
    }
```



### 判断对象是什么数据类型三种方式

```js
var num=10;
console.log(typeof num);//获取num这个变量的数据类型
var obj={};//对象

//判断这个对象是不是某个类型的
console.log(obj instanceof Object);

//获取某个对象的数据类型的样子
Object.prototype.toString.call(对象);//此时得到的就是这个对象的类型的样子
```



## 预解析和作用域

预解析: 就是在浏览器执行代码之前,把变量的声明和函数的声明提前到该作用域上面

作用域: 就是变量的使用范围  (局部变量和全局变量)

- **函数在定义好的时候, 作用域就已经定下来了, 和函数在哪里调用没有关系**



### ES6新增块级作用域

### 什么是块级作用域

有`{}`形成的区域,就叫做块级作用域,

使用`let` 新增块级作用域



### 作用域链

#### 什么是函数的作用域链

函数可以形成作用域, 把函数嵌套在另一个函数中, 层层嵌套,从里到外直到全局作用域, 形成的一条链式结构 就是作用域链

> 对于每个函数的作用域链, 都是从自己本身出发, 一直到全局作用域 

作用域链: 就是从里到外层层搜索, 搜索到了,就直接使用,一直搜索在0级作用域

#### 变量搜索规则(找声明)

> 沿着作用域链,从里到外直到全局作用域

先在当前函数作用域内查找是否**声明了该变量**, 沿着作用链从里往外查找, 如果找到全局作用域还没有, 就报错 

```js
var num=10; //作用域链 级别:0
function f1() {
  var num2=20;
  function f2() {
    var num3=30;
    console.log(num);
  }
  f2();//====30
}
f1();
```



## 函数中this指向问题

**普通函数this的指向只有在函数调用的时候才能被确定**

- 函数都有自己的`this` 指向谁, 取决于,何种调用模式



**`this` 问题如何分析**

- **看this是哪个函数的**
- **这个函数是何种调用模式**



### 函数的四种调用模式

#### 1.函数调用模式

`函数名()`

这种模式中`fn()`的`this`指向`window`

#### 2.构造函数调用模式

`this`  指向实例对象

```js
function Persion() {
    console.log(this) //实例对象
}
var p = new Persion()

```

#### 3.方法名调用模式

`对象.方法名()`  这种调用方式, `this`  谁调用this指向谁

> 中括号语法或者点语法都属于方法调用模式

**也就是说明这个方法(函数)调用的过程是对象参与了, this就指向调用对象**

```js
var obj = {
    fn: functon() {
    	console.log(this)// 指向调用的对象obj
	}
}
obj.fn() //this指向obj
```

```js
function fn() {
    console.log(this)
}
//fn被arr这个数组对象调用了
var arr = [fn, 20, 30]
arr[0]()      `this指向arr`
```



#### 4.方法借用模式

又叫上下文调用模式

**主要用来修改`this`的指向**

##### 三个方法`call`  `apply`  `bind`

`call()`可以借用其他对象的方法

- 对于自己没有的方法, 可以使用`借用对象.借用方法.call(对象)`

```js
对象.要借用的方法.call(借用对象)
```



```js
 函数调用模式的this==============>window===========页面中所有的属性和方法都是window的

 方法调用模式中的this指的的是============>当前的调用对象
 
 构造函数中的this指的是================>实例对象 

 定时器中的this指的是==================>window
 
 原型对象中的this指的是=================>实例对象
```

#### 补充`arguments`

本身是个伪数组, 函数的实参列表, 存储了函数调用时, 传的所有实参



#### `this`相关面试题

```js
#面试题1
var length = 10

    function fn() {
        console.log(this.length)
    }
    var obj = {
        length: 5,
        method: function(fn) {
            // 函数调用模式
            fn(); // 10

            // arguments  是函数内的实参列表，伪数组
            // arguments ==> [fn, 10, 5]
            // console.log(arguments);

            // 方法调用模式
            //  fn是被arguments调用的，fn内的this指向了arguments
            arguments[0]();  // 3
        }
    }
    // 方法调用模式
    obj.method(fn, 10, 5);

#面试题2
    var length = 10;
    var age = 18;

    function fn() {
        console.log(this.length);
    }
    var arr = [fn, "222"];
    // 函数调用模式
    fn(); //10
    // 方法调用模式
    arr[0]()  //2

#面试题3
    var age = 38;
    var obj = {
        age: 18,
        getAge: function() {

            // getAge 方法内的this指向了obj对象
            console.log(this.age); // 18

            function foo() {
                // 只要是个function 都会有自己的this
                // 函数内的this指向了谁，取决于函数的调用模式
                console.log(this.age); // 38
            }
            // 函数调用模式 this指向window
            foo(); //38
        }
    }
    // 方法调用模式
    obj.getAge(); // 18 38 
    obj["getAge"](); //18 38

#面试题4
   var age = 38; // 全局变量， 是window对象的属性  window.age = 38
    var obj = {
        age: 18,  // obj属性
        getAge: function() {
            console.log(this.age);
        }
    }

    var f = obj.getAge; // 把obj对象的getAge方法赋值给了变量f
    // 函数调用模式
    f(); // 38
```







## `call()`  `apply()` `bind()	`



### `call()`

#### **参数**

`call(newthis, [arg1, arg2, .....])`

- 参数1 : 可以修改函数的`this`的指向, **借用的对象**
- 其他参数: 都会作为函数调用的实参

#### 借用套路

- 找到要借的方法
- `.call(要借的对象)`

#### 作用

- 可以用来调用函数

```js
fn() === fn.call()
```

- 函数内的`this` 指向为 `call`  的第一个参数
  - `call`的**第一个参数**可以用来修改函数内的`this`指向
- 其他参数作为函数的实参

```js
function fn(n1, n2) {
    console.log(this)
    console.log(n1 + n2) //100 200则作为函数的实参
}
fn.call({name:'lw'}, 100, 200)  // this则指向{name: 'lw'}
```



#### 伪数组借用数组的方法

##### 什么是伪数组

伪数组也是一个对象, 有数字下标, 有`length` , 可以遍历

伪数组不能使用数组的方法, 但是可以使用`call`借用数组的方法

##### 常见的伪数组

- `getElementsByTagName()`
- `getElementsByClassName`
- `getElementsByName`
- `querySelectorAll()`
- `auguments`
- `jq对象`

```js
var obj = {
    0: '大飞哥',
    1: '棠哥',
    2: '罗大爷',
    length: 3,
}

//伪数组不能使用数组的方法
// obj.push(1)  不能

//需求添加一个 3: '皮皮虾',
obj[3] = '皮皮虾'
obj.leght++

//借用方法, length自动加
Array.prototype.push.call(obj, '吴大骚', '骚亮', '浩哥');
//等价于
[].push.call(obj, '吴大骚', '骚亮', '浩哥')
```



#### 无分号写法的注意

一行的开头以`[` **`** 和 `(`  开头需要加分号	

### `apply()`

> `apply()`方法和`call()`作用一样

**和`call()`的区别**

把实参列表变成一个数组

#### **参数**

`call(thisArg, 实参列表)`中的除了第一个参数,其他参数就是一个实参列表

> apply() 给函数传的实参列表需要放到一个数组或者伪数组中

`apply(newThis[,Array[arg1, arg2, ...] ] )`

#### **作用**

- 调用函数
- 修改this的指向
- 其他参数作为函数的实参

```js
function sum(n1, n2) {
    console.log(this)
    coonsole.log(n1 + n2)
}
sum.call({name: 'lw'}, 10, 20) // {name: 'lw'}  30
sum.apply({name: 'lw'}, [10, 20]) // {name: 'lw'}  30
```

#### 平铺性

将`apply()`  第二个参数的每一项取出来作为函数的实参



### `call()`和 `apply()`  使用场景

- 当函数的参数, 比较少的时候, 使用`call()` 较好
- 当函数的参数已经存在于数组或伪数组中, 使用`apply`  较好

```js
var arr = [18, 34, 43, 32, 233]

#apply()更合适
Math.max.apply(arr, arr)
Math.max.call(arr, 18, 34, 43, 32, 233)
```



### `bind()`

在`Vue`和 `React` 使用较多

#### 语法

```js
函数.bind(thisArg)
```

#### 作用

- **创建并返回新函数, 不会调用函数**
- **`bind`  的this固定指向第一个参数**
- 新函数和原来的函数一模一样(把函数克隆了一份, 并返回了)

- 但新函数的`this`  指向就被固定了, 而不是在函数调用时, 指向`window` , 而是固定指向`bind` 的第一个参数

#### this指向固定

- 无论函数是何种调用模式, 在bind创建的时候, `this`指向就已经固定

```js
var fn1 = function () {
    console.log(this)
    console.log(123)
}
var fn2 = fn1.bind([10, 20, 30])
fn2() // this => [10, 20, 30] 而不是window
```

#### bind的使用

```js
var obj = {
    name: '骚亮',
    car: '法拉利',
    sayHi: function () {
       // console.log('wo'+this.name+'有'+this.car)
        setInterval(function () {
         console.log('wo'+this.name+'有'+this.car)
    	#此时定时器中的function还没调用, this指向还未固定, bind(this)固定this指向obj    
    	}.bind(this), 1000)
    }
    
}
obj.sayHi()
```



## 箭头函数中的`this`指向

- 由于箭头函数不绑定this， 它会捕获其所在（即定义的位置）上下文的this值， 作为自己的this值

- 函数体内的`this`对象，就是定义时所在的对象，而不是使用时所在的对象。
- 箭头函数中的this是在定义函数的时候绑定，而不是在执行函数的时候绑定。

### 箭头函数作为一个方法

作为方法的箭头函数this指向全局window对象，而普通函数则指向调用它的对象

```js
var obj = {
  i: 10,
  b: () => console.log(this.i, this),
  c: function() {
    console.log( this.i, this)
  }
}

window.obj.b();  // undefined window{...}
obj.c();  // 10 Object {...}
```





## 递归

### 什么是递归

递归就是在函数中,调用自己,此时就形成了递归,如果没有递归条件就会形成死循环,所以递归必须要有执行条件

```js
function f1() {
  console.log("从前有个山,山里有个庙,庙里有个和尚给小和尚讲故事:");
   f1();
}
f1();
```



### 递归函数使用套路

- 找规律

- 把未知的问题转化为已知问题
- 结束递归的条件

**计算1-100的和**

```js
function sum(n) {
    if (n === 1) {
    	return 1 //return后面的代码不在执行, 不在递归
    }
    return sum(n-1) + n   
}
sum(100) //5050
```

### 执行过程

先根据条件,不停的一次一次的进入函数中,当满足条件时,在一层一层的往外出

> 层层递进, 层层回归

```js
//函数的声明
function getSum(x) {
  if(x==1){
    return 1;
  }
  return x+getSum(x-1);
}
//函数的调用
console.log(getSum(5));
```

```js
/执行过程:
* 代码执行getSum(5)--->进入函数,此时的x是5,执行的是5+getSum(4),此时代码等待
* 此时5+getSum(4),代码先不进行计算,先执行getSum(4),进入函数,执行的是4+getSum(3),等待, 先执行的是getSum(3),进入函数,执行3+getSum(2),等待,先执行getSum(2),进入函数,执行 2+getSum(1);等待, 先执行getSum(1),执行的是x==1的判断,return 1,所以,
* 此时getSum(1)的结果是1,开始向外走出去
* 2+getSum(1) 此时的结果是:2+1
* 执行:
* getSum(2)---->2+1
* 3+getSum(2) 此时的结果是3+2+1
* 4+getSum(3) 此时的结果是4+3+2+1
* 5+getSum(4) 此时的结果是5+4+3+2+1
```



### 递归问题优化

**计算斐波那契数列存在大量重复计算**

#### 解决方案

缓存: 在JS中用`[]` 或 `{}` 表示缓存这个容器

#### 使用缓存

- 定义一个数组或者对象表示缓存
- 先看缓存中是否有对应需要的数据, 如果有就直接取出来使用
- 如果没有, 就需要去计算结果, 而且把计算好的结果存储到缓存容器中, 方便下次使用

```js
//定义一个缓存容器
var cache = {}

function getFib(x) {
  if(x==1||x==2){
    return 1
  }
   //先看缓存中有没有想要的数据 
   if (cache[n]) {
        return cache[n]
    }else {
   //缓存中没有数据
       //计算结果
        var ret = getFib(n-1) + getFib(n-2)
       //存入缓存
        cache[n] = ret
       // 返回数据
        return ret
    }
    
 // return getFib(x-1)+getFib(x-2);
}
```



### 递归案例

求N个数字的和

```js
function getSum(x) {
  if(x==1){
    return 1;
  }
  return x+getSum(x-1);
}
//函数的调用
console.log(getSum(5));===15
```

求数字各个数字的和

```js
function getEverySum(x) {
   if(x<10){
     return x;
   }
   //获取的是这个数字的个位数
   return x%10+getEverySum(parseInt(x/10));
 }
console.log(getEverySum(136));//10
```

**斐波那契数列**

```js
规律:
fib(40) => fib(39) + fib(38)
fib(39) => fib(38) + fib(37) ...

function getFib(x) {
  if(x==1||x==2){
    return 1
  }
  return getFib(x-1)+getFib(x-2);
}
console.log(getFib(12));
```



## 闭包(closure)

三个特性: 

1. 函数嵌套函数
2. 函数内部可以引用函数外部的参数和变量
3. 参数和变量不会被垃圾回收机制回收

### 引入

需求: 

- 拿到函数内部的`num` 值

```js
function fn() {
    var num = 10
    return num
}
var ret = fn()
console.log(ret) //10
```

- 修改函数内部`num`的值
- 下面案例就形成的闭包

> 从外部无法修改函数内的值
>
> 打进去一个卧底, 再把卧底返回出去

```js
function fn(n) {
    var num = 10
    
    #卧底函数, 能够修改num的值
  	function inner (n) {
       num = n 
        console.log(num)
    }
   //把具有修改功能的函数返回出去 
    return inner
}
 //把inner函数返回出去, 
var ret = fn()
ret(100) // log=> 100
```



### 闭包的概念

> 能够保护数据的安全

是函数和声明该函数的词法环境的组合 (MDN)

- 函数=> 内部的`inner`函数
- 声明该函数 => 外部`fn`函数
- 词法环境 =>  作用域链
- 组合 => 综合环境, 是一个整体

内部函数和外部函数嵌套形成的一个综合环境, 作用域链访问的关系

- 嵌套关系
- 内部函数访问外部函数的变量就形成了一个闭包

### 形成的条件

> 函数嵌套且访问外部函数的局部变量

至少是两个函数嵌套, 且存在内部函数访问外部函数局部变量形成的一个综合环境	

**chrome中source调试**

`Scope`  => 作用域

### 闭包的基本模型

```js
function outer() {
    var num = 0 //outer的局部变量
    function inner() {
        //只要有访问关系即可
        //num++
        console.log(num)
    }
    //通常把inner内部函数返回出去, 外部可以拿到inner函数进行操作, 但不是闭包的必备条件 
    return inner
}
```



### 使用闭包解决斐波那契缓存

- 使缓存`cache`  和 `getFib()`  形成一个闭包
- 使`cache` 变成一个局部变量, 保护`cache`的安全

```js
function outer() {
    //定义一个缓存容器
	var cache = {}

	return function getFib(x) {
  		if(x==1||x==2){
    	return 1
  		}
  		 //先看缓存中有没有想要的数据 
   		if (cache[n]) return cache[n]
        
         #三行代码优化为一行, return 的是 等号的右边
        return cache[n] = fib(n-1) + fib(n-2)
       		
  	 	/*//缓存中没有数据
       //计算结果
       // var ret = fib(n-1) + fib(n-2)
       //存入缓存
        cache[n] = ret
       // 返回数据
        return ret */
        
       
        
 	// return getFib(x-1)+getFib(x-2);
	}
}

//
var fb = outer()
fb(100)
```



#### 补充:赋值表达式的返回值

- 在赋值表达式中, 是有返回值的
- 在函数`return`  一个表达式的时候, 返回的是等号右边的值

- 返回值是等号右边的值

### 闭包的作用

- 保护数据安全
  - 让全局变量变成函数的局部变量, 外部则就无法修改

- 持久化维持数据
  - 缓存数据,延长作用域链

### 闭包的优缺点

**优点 :也是缓存数据,延长作用域链     缺点 : 也是缓存数据,延长作用域链**



**函数调用也会开辟空间存储**

#### 全局作用域下的函数调用

全局声明的变量及函数, 在函数调用时, 会开辟一个内存空间,只有在关闭页面或浏览器的时候, 函数的调用占用的内存才会被销毁

缺点: 数据不安全

#### 局部作用域下的函数调用

优点: 数据安全

**普通函数调用时**

当函数调用时, 函数就会开辟内存空间,  存储函数内部的变量

函数调用结束, 开辟的内存空间会被销毁掉

**闭包函数调用时**

闭包的函数调用时, 闭包占用的内存空间不会被释放



### 闭包存在的问题

由于闭包能够持久化数据, 就会导致内存泄漏

- 内存泄漏
  - 有一块内存空间被占用, 而且无法释放, 其他对象也无法使用这块内存空间

#### 内存管理

内存生命周期

- 分配内存 (JS自动分配)
- 使用内存(读写操作)
- 释放内存( js自动释放)

**内存泄漏和内存溢出**

内存泄漏: 一个对象 /函数 之类不用了, 没有被释放

内存溢出: 内存满了, 不够用了(一般只有死循环会导致内存溢出)



#### JS中的垃圾回收机制

https://developer.mozilla.org/zh-	CN/docs/Web/JavaScript/Memory_Management

> 在前端浏览器中, 垃圾回收机制关注不多, 因为浏览器会自动回收, 而且电脑的硬盘内存大
>
> 一般在移动端和后端关注较多, 因为在移动端手机的内存小, 而且不会自动释放, 会导致用久了会卡
>
> 后端数据量大所以需要垃圾回收

##### **引用计数算法(被淘汰)**

看对象引用次数, 对象引用次数是0(零引用对象), 那么该对象就是垃圾

```js
定义好了的变量, 就引用了一次对象, 对象的引用次数就是1 (那么这个对象就不是垃圾, 占用的内存不会被释放)
var o = {
    name: 'lw'
}
对象引用次数为2
var o2 = o

不在引用对象, 对象引用次数为1
var o = 1

o2不在引用对象, 对象引用计数为0, 变为一个垃圾
o2 = null
```

**存在问题**

- 循环引用

```js
function fn() {
    var obj1 = {}
    var obj2 = {}
    
    //obj1中有obj2, obj2中有obj1
    obj1.a = obj2
    obj2.b = obj1
}

// fn调用完毕后, 对象占用的内存应该被释放掉, 但是引用计数算法看来这两个对象引用次数不是0, 不会释放
fn() 
fn() 
fn() 
fn()  // 调用都, 函数中的obj1, obj2都无法释放, 就造成了内存泄漏
```



##### 标记清除算法(升级)

这个算法把对象是否不在需要简化为**对象是否可获得**

主要看对象是否可以从`window`获取, 获取不到的对象则视为垃圾

- 能够解决循环引用问题

```js
//window.o3则可以找到o3则不视为垃圾
var o3 = {
    name: 'lw'
}

改变指向, 则对象视为垃圾
o3 = null
```



### 闭包占用内存不会被释放

从引用标记算法

有变量引用闭包中的那个函数, 那个函数就不会被视为垃圾

从标记清除算法角度

从`window`上能够找到闭包中的函数的返回值得那个变量,变量指向闭包中的函数



### 解决闭包内存泄漏问题

当闭包的功能不在需要使用时, 需要手动的释放内存

- 当内存中闭包的函数没有变量指向他的时候, 就会被当然垃圾回收
-  result 在window 身上, 不会回收, fn 用到 count , 导致outer不会被释放, 导致整个 outer 函数占用的内存也不会被释放

```js
// 这和只是定义一个闭包环境
function outer(){
  var count = 0;

  function fn(){
    count++;
    console.log("执行次数"+count);
  }
  return fn;
}

// 使用闭包
var result = outer()();   // result 在window 身上, 不会回收, fn 用到 count , 导致outer不会被释放
// result();

result = null;//当函数fn没有被变量引用了，那么函数fn就会被回收，函数fn一旦被回收，那么outer调用形成的作用域也就得到了释放。
```



### 闭包的经典面试题

点击按钮打印按钮的下标(闭包来实现)

- 每一次循环, 都会调用`outer()` , 并且在内存中开辟了空间存储, 循环多少次就会开辟多少空间 , 每一空间都有自己的`j=i` , 并且点击事件都打印了对象的`j`的值

```html
<button>按钮</button>
<button>按钮</button>
<button>按钮</button>
<button>按钮</button>
<button>按钮</button>
<button>按钮</button>

<script>
   var btns = document.querySelectorAll('button')
   for (var i = 0; i < btns.length; i++) {
     
      /* function outer(j) {
           // i = 0, j=0
           //空间中注册了一个事件 j= 0, 并且给对应的btn注册了点击事件
           btns[j].onclick = function () {
               console.log(j)
           }
       }
       outer(i)  //每一次调用,就开辟了一个空间 
       */
       
       
        #优化: 自调用函数
   		 (function outer(j) {
           // i = 0, j=0
           //空间中注册了一个事件 j= 0, 并且给对应的btn注册了点击事件
           btns[j].onclick = function () {
               console.log(j)
           }
      	 })(i)
   }
    
    
   
</script>
```



### 闭包案例

给美女点赞案例

```js
 <li><img src="images/ly.jpg" alt=""><br/><input type="button" value="赞(1)"></li>
//获取所有的按钮
//根据标签名字获取元素
function my$(tagName) {
  return document.getElementsByTagName(tagName);
}
//闭包缓存数据
function getValue() {
  var value=2;
  return function () {
    //每一次点击的时候,都应该改变当前点击按钮的value值
    this.value="赞("+(value++)+")";
  }
}
//获取所有的按钮
var btnObjs=my$("input");
//循环遍历每个按钮,注册点击事件
for(var i=0;i<btnObjs.length;i++){
  //注册事件
  btnObjs[i].onclick=getValue();
}
```



## 沙箱

### 什么是沙箱

沙箱就是一个环境,黑盒, 在一个虚拟的环境中模拟真实世界,结果和真实世界一样,但不影响真实世界

### JS中的沙箱

自调用函数就是一个沙箱,沙箱中的变量和方法,函数,和外面的其他变量和方法不冲突

> 把代码放在一个自调用函数里面即可

```js
var num=10;
console.log(num);===10

//沙箱---小环境
(function () {
  var num=20;
  console.log(num);===20
})();

//沙箱---小环境
(function () {
  var num=30;
  console.log(num);===30
}());
```







# JavaScript 高级 第六天



## 正则表达式 Regular Expression

### 什么是正则表达式

也叫规则表达式,按照一定规则组成的表达式, 表达式的作用主要用来匹配字符串的

### 创建正则表达式的方式

通过构造函数创建正则表达式对象

```js
//对象创建完毕---
 var reg=new RegExp(/\d{5}/);
//字符串
 var str="我的电话是10086";
//调用方法验证字符串是否匹配
 var flag=reg.test(str);
 console.log(flag);
```

字面量的方法创建正则表达式对象

```js
var reg=/\d{1,5}/;
var flag=reg.test("小苏的幸运数字:888");
console.log(flag);
```

正则的测试 : `text()`

语法: 

```js
reg.text(string)
```



### 正则表达式的组成

- 普通字符串 : 没有特殊意义, 写啥匹配啥

- 主要由元字符和限定符组成

### 正则优先级

- `|`  或, 优先级最低
- `()`  分组, 优先级最高

### 元字符

> 有一个满足即可

- `\d`  匹配数字 0-9
- `\D`  匹配一个非数字
- `\w`  字母数字下划线
- `\W`  给字母数字下划线的特殊字符
- `\s`  不可见的空白符
- `\S`  非空白符
- 汉字 -> `/[\u4e00-\u9fa5]/`

```js
#有一个满足即可
console.log(/\d/.test('123')) //true

console.log(/\D/.test('a1bc')) //true
```



### 字符类元字符

`[]` 表示一个字符,可以在`[]` , 可以写范围, 表示范围中的一个

- 自带或者的含义
- `[ a-z ]` 表示一个范围
- `[^]` 表示非

```js
console.log( /[abc]/.test('afg'))// true

//匹配a-z任意一个
/[a-z]/  [a-z] 表示的是:所有的小写的字母中的任意的一个
```



```js
	`.`  表示的是:除了\n以外的任意的一个字符 
    console.log(/./.text('/n'))  false
*
* `[]` 表示的是:范围,  [0-9] 表示的是0到9之间的任意的一个数字,  "789" [0-9]
* `[1-7]` 表示的是1到7之间的任意的一个数字
* [a-z] 表示的是:所有的小写的字母中的任意的一个
* [A-Z] 表示的是:所有的大写的字母中的任意的一个
* [a-zA-Z] 表示的是:所有的字母的任意的一个
* [0-9a-zA-Z] 表示的是: 所有的数字或者是字母中的一个
* [] 另一个函数: 把正则表达式中元字符的意义干掉    [.] 就是一个.
* | 或者     [0-9]|[a-z] 表示的是要么是一个数字,要么是一个小写的字母
* () 分组 提升优先级   [0-9]|([a-z])|[A-Z]
* ([0-9])([1-5])([a-z]) 三组, 从最左边开始计算
```



### 边界类元字符

**以什么开始** : `^`

**以什么结束** : `$`

^ 和 $ 一起使用 精确匹配, 常用于表达校验



### 量词类元字符

量词是就近修饰

`*  +   ?  {}`

`*`  : 表示次数大于等于 0  , `{0,}`

`+` :   大于等于 1 `{1,}`

`?`  :  `0 | 1`  = `{0, 1}`

`{}`   : 就近修饰

```js
{m} 次数为m次
{m,} 大于等于m次
{m,n} m到n之间, 包含m,n
```

```js
/^a*$/.test('') //true
/^a*$/.test('aaa') //true
/^a*$/.test('abc') //false


/^a+$/.test('') //false
/^a+$/.test('aaa') //true
/^a+$/.test('abc') //false
```



### 总结元字符

限定符也叫属于元字符,是元字符下面的一个范围

`^`  表示非, 或者以什么开始

```js
*   表示的是:前面的表达式出现了0次到多次

+  表示的是:前面的表达式出现了1次到多次

 ?  表示的是:前面的表达式出现了0次到1次,最少是0次,最多1次 ,另一个含义:阻止贪婪模式
 
 {} 更加的明确前面的表达式出现的次数 
 {0,} 表示的是前面的表达式出现了0次到多次,和 *一样的
  {1,} 表示的是前面的表达式出现了1次到多次,和 +一样的
 {0,1} 表示的是前面的表达式出现了0次到1次,和 ?一样的
 {5,10} 表示的是前面的表达式出现了5次到10次
 {4} 前面的表达式出现了4次
 {,10} 错误的========不能这么写
 
 ^ 表示的是以什么开始,或者是取非(取反) ^[0-9] 以数字开头
 ^[a-z] 以小写字母开始
 [^0-9] 取反,非数字
 
 $ 表示的是以什么结束   [0-9][a-z]$  必须以小写字母结束
 ^[0-9][a-z]$   相当于是严格模式  必须是以数字开始,以字母结束
 
   \d 数字中的任意一个,
   \D 非数字中的一个
   \s 空白符中的一个(不可见字符)
   \S 非空白符
   \w 非特殊符号
   \W 特殊符号
   \b 单词的边界
```







### 正则表达式案例

#### 邮箱的正则表达式

```js
[0-9a-zA-Z_.-]+[@][0-9a-zA-Z_.-]+([.][a-zA-Z]+){1,2}
```

#### 验证密码强度

```js
//获取文本框注册键盘抬起事件
  my$("pwd").onkeyup=function () {
    //每次键盘抬起都要获取文本框中的内容,验证文本框中有什么东西,得到一个级别,然后下面的div显示对应的颜色
    //如果密码的长度是小于6的,没有必要判断
//    if(this.value.length>=6){
//     var lvl= getLvl(this.value);
//      my$("strengthLevel").className="strengthLv"+lvl;
//    }else{
//      my$("strengthLevel").className="strengthLv0";
//    }
    my$("strengthLevel").className="strengthLv"+(this.value.length>=6?getLvl(this.value) :0);
  };

/给我密码,我返回对应的级别
  function getLvl(pwd) {
    var lvl=0;//默认是0级
    //密码中是否有数字,或者是字母,或者是特殊符号
    if(/[0-9]/.test(pwd)){
      lvl++;
    }
    //判断密码中有没有字母
    if(/[a-zA-Z]/.test(pwd)){
      lvl++;
    }
    //判断密码中有没有特殊符号
    if(/[^0-9a-zA-Z_]/.test(pwd)){
      lvl++;
    }
    return lvl;//最小的值是1,最大值是3
  }

```



#### 验证表单是否符合要求

```js
<div class="container" id="dv">
  <label for="qq">Q Q</label><input type="text" id="qq"><span></span><br/>
  <label>手机</label><input type="text" id="phone"><span></span><br/>
  <label>邮箱</label><input type="text" id="e-mail"><span></span><br/>
  <label>座机</label><input type="text" id="telephone"><span></span><br/>
  <label>姓名</label><input type="text" id="fullName"><span></span><br/>
</div>

//qq的
  checkInput(my$("qq"),/^\d{5,11}$/);
  //手机
  checkInput(my$("phone"),/^\d{11}$/);
  //邮箱
  checkInput(my$("e-mail"),/^[0-9a-zA-Z_.-]+[@][0-9a-zA-Z_.-]+([.][a-zA-Z]+){1,2}$/);
  //座机号码
  checkInput(my$("telephone"),/^\d{3,4}[-]\d{7,8}$/);
  //中文名字
  checkInput(my$("fullName"),/^[\u4e00-\u9fa5]{2,6}$/);

//给我文本框,给我这个文本框相应的正则表达式,我把结果显示出来
  //通过正则表达式验证当前的文本框是否匹配并显示结果
  function checkInput(input,reg) {
    //文本框注册失去焦点的事件
    input.onblur=function () {
      if(reg.test(this.value)){
        this.nextElementSibling.innerText="正确了";
        this.nextElementSibling.style.color="green";
      }else{
        this.nextElementSibling.innerText="让你得瑟,错了吧";
        this.nextElementSibling.style.color="red";
      }
    };
  }
```



### 正则替换

正则表达式中: `//g` 表示`global`的是全局模式匹配
正则表达式中: `//i` 表示`ignore`的是忽略大小写



. match 把符合要求的字符串显示出来,并返回一个数组

```js
var str="中国移动:10086,中国联通:10010,中国电信:10000";
//把里面所有的数字全部显示出来
var array=str.match(/\d{5}/g);
console.log(array);========= ["10086", "10010", "10000"]
```

. replace  替换 字符串中的内容

```js
var str="小苏好帅哦,真的是太帅了,帅,就是真帅";
str=str.replace(/帅/g,"猥琐");
console.log(str);
```

.trim   把字符串两边的空白字符删除

```js
var str="  哦买噶的    ,太幸福了  ";
str=str.trim();
console.log("==="+str+"===");
```



## 继承

### 面向对象的特性

封装 

```js
/封装:就是包装
* 一个值存储在一个变量中--封装
* 一坨重复代码放在一个函数中--封装
* 一系列的属性放在一个对象中--封装
* 一些功能类似的函数(方法)放在一个对象中--封装
* 好多相类似的对象放在一个js文件中---封装
```

继承

```js
/继承: 首先继承是一种关系,类(class)与类之间的关系,JS中没有类,但是可以通过构造函数模拟类,然后通过原型来实现继承
*/继承也是为了数据共享,js中的继承也是为了实现数据共享
```

多态

```js
/多态:一个对象有不同的行为,或者是同一个行为针对不同的对象,产生不同的结果,要想有多态,就要先有继承,js中可以模拟多态,但是不会去使用,也不会模拟,
*
```



### 实现继承的方式

#### 原型链继承

在构造函数创建出来的实例对象, 能够使用(**继承**)构造函数原型对象中的方法和属性, 就实现了继承

**原型替换**

改变了原型对象的指向, 指向一个新对象

```js
function Person() {
    
}
Person.prototype = {
    constructor : Person, #需要手动添加
}

var p = new Person()

// p -> Person.prototype -> Object.prototype -> null
console.log(p.constructor) // Object
```



**JS中如何继承**

JS中没有类,但是可以通过构造函数模拟类,然后通过__原型__来实现继承

```js
function Person(name,age,sex) {
  this.name=name;
  this.sex=sex;
  this.age=age;
}
function Student(score) {
      this.score=score;
}
//改变学生的原型的指向即可==========>学生和人已经发生关系
//让学生的原型==========>指向Person的实例化对象,实例化对象中有都构造函数的属性,并且能够指向构造函数的原型对象
    Student.prototype=new Person("小明",10,"男");
```

缺点:

__每一个继承的对象的属性都是相同,不能修改__



#### 借用构造函数

优点:

__能够解决通过继承的实例化对象属性相同问题,并且能够分别添加不同的属性__

```js
//借用构造函数:构造函数名字.call(当前对象,属性,属性,属性....);
//解决了属性继承,并且值不重复的问题

```

缺陷:  父级类别中的方法不能继承

```js
function Person(name, age, sex, weight) {
  this.name = name;
  this.age = age;
  this.sex = sex;
  this.weight = weight;
}
Person.prototype.sayHi = function () {
  console.log("您好");
};
function Student(name,age,sex,weight,score) {
  //借用构造函数
  Person.call(this,name,age,sex,weight);
  this.score = score;
}
var stu1 = new Student("小明",10,"男","10kg","100");
console.log(stu1.name, stu1.age, stu1.sex, stu1.weight, stu1.score);
//stu1.sayHi();===================>会报错
var stu2 = new Student("小红",20,"女","20kg","120");
console.log(stu2.name, stu2.age, stu2.sex, stu2.weight, stu2.score);
```

#### 组合继承

原型继承+借用构造函数

- 把想要的方法的原型对象, 添加到实例对象的原型链上
- 原型链继承 => 原型替换
  - `Student.prototype = new Person()` 
  - `stu -> Student.prototype(new Person()) -> Person.prototype -> Object.prototype -> null`  
- 借用构造函数继承 => 属性

既能够继承父类构造函数的方法,而且每个对象的属性能赋不同的值;

属性和方法都被继承了

```js
function Person(name,age,sex) {
  this.name=name;
  this.age=age;
  this.sex=sex;
}
Person.prototype.sayHi=function () {
  console.log("阿涅哈斯诶呦");
};
function Student(name,age,sex,score) {
  //借用构造函数:属性值重复的问题
  Person.call(this,name,age,sex);
  this.score=score;
}

//原型链继承----继承
//在添加原型方法时, 就会覆盖或修改Person.prototype的成员方法
//Student.prototype = Person.prototype

//优化------------------------------> 指向Person的实例对象
Student.prototype=new Person();//不传值
Student.prototype.eat=function () {
  console.log("吃东西");
};
var stu=new Student("小黑",20,"男","100分");
console.log(stu.name,stu.age,stu.sex,stu.score);
stu.sayHi();
stu.eat();
var stu2=new Student("小黑黑",200,"男人","1010分");
console.log(stu2.name,stu2.age,stu2.sex,stu2.score);
stu2.sayHi();
stu2.eat();
```

#### 拷贝继承

第一种方式: 将改变地址只指向

```js
 //拷贝继承；把一个对象中的属性或者方法直接复制到另一个对象中

var obj1={
  name:"小糊涂",
  age:20,
  sleep:function () {
   console.log("睡觉了");
  }
};

//改变了地址的指向
var obj2=obj1;
console.log(obj2.name,obj2.age);
obj2.sleep();
```

第二种方式: 把属性和方法完全复制一份

```js
function Person() {
}
Person.prototype.age=10;
Person.prototype.sex="男";
Person.prototype.height=100;
Person.prototype.play=function () {
  console.log("玩的好开心");
};
var obj2={};
//Person的构造中有原型prototype,prototype就是一个对象,那么里面,age,sex,height,play都是该对象中的属性或者方法
//在堆中重新开辟一个空间,把Person的原型复制一个给obj2;
for(var key in Person.prototype){
  obj2[key]=Person.prototype[key];
}
console.dir(obj2);
obj2.play();
```

### 总结继承

```js
//继承:
/*
* 原型作用: 数据共享 ，目的是:为了节省内存空间,
* 原型作用: 继承  目的是:为了节省内存空间
*
* 原型继承:改变原型的指向
* 借用构造函数继承:主要解决属性的问题
* 组合继承:原型继承+借用构造函数继承
* 既能解决属性问题,又能解决方法问题
* 拷贝继承:就是把对象中需要共享的属性或者方法,直接遍历的方式复制到另一个对象中
```



### 逆推看继承

```js
function F1(age) {
  this.age = age;
}
function F2(age) {
  this.age = age;
}
F2.prototype = new F1(10);
function F3(age) {
  this.age = age;
}
F3.prototype = new F2(20);

var f3 = new F3(30);
console.log(f3.age);// 30
```

![](images\逆推继承看原型.png)







## JQuery源码分析

### 我对`jQuery`的源码的分析

首先为了,防止全局变量污染问题, jQuery就是一个自调用函数, 同时保证我们能够使用它的`API`, jquery把`$ ` 或者`jQuery` 这个两个变量挂载到`window`身上, 我在在外部就能够通能过这个`$` 使用jquery的方法



其次, 我们通过这个`$` 获取元素的时候, 实际上这个`$(selector)` 就是一个实例对象, 它的`__proto__`指向构造函数`init`的`prototype`, `init`构造函数在`jQuery.prototype`上, 在jquery中通过`init`这个构造函数能够获取元素, 为了我们省去这个`new` , 就使用了`jQuery` 这个工厂函数替我们去`new`这件事情, 通过把`new`得到的实例对象返回

也就是说我们`$`的时候, 就像于调用了工厂函数, 工厂函数去给我们`new` 了一个`jquery.prototype.init`构造函数的实例对象并返回



同时,为了保证实例对象能够使用`jQuery.prototype`身上的方式方法, 我们改变了`init`这个构造函数的原型对象的指向, 重新指向了`jQuery.prototype` , 这样我们就能够使用`$`身上的方法了

 



### 整体架构

自调用函数

传参`window` :  把`JQuery` 这个变量(函数) 暴露出去

- 在自调用函数中, 外部想要使用需要暴露给`window`
- 不传`window` 也可以暴露, 但是传了以后, `window` 就是自调用函数的形参, 在自调用函数内部即可找到
  - 只需要找一次, 减少对`window`的搜索过程
  - 在自调用函数中`window` 是形参, 变量名可以修改,利于代码压缩

传参`undefined`  :  undefined 是一种数据类型 , 值是自己本身

- IE678中`undefined` 数据类型的值可以修改, 其他浏览中不能修改`undefined` 的值
- 自调用函数中`undefined` 中不受外界`undefined`影响

```js
(function(window, undefined) {
    var jQuery = function () {
        console.log('jQuery is Ok')
    }
    //给window添加jQuery这个属性, 暴露给window
    window.jQuery =  window.$ = jQuery
})(window)

//外部可以调用
jQuery()
```



### jQuery获取元素

- `jQuery` 相当于一个构造函数 我们使用的`$('div)` 相当于`JQuery`的实例对象

```js
		(function (window, undefined) {
			
			var jQuery = function (selector) {

				var ele = document.querySelectorAll(selector)
				Array.prototype.forEach.call(ele,(item, i) =>{
					this[i] = ele[i]
				})

				// for (var i = 0; i < ele.length; i++) {
				// 		this[i] = ele[i]
				// 	}	
				this.length = ele.length
			}

			window.$ = window.jQuery = jQuery
		})(window)

		console.log(new $('div'))
```



### 原型添加方法

把方法添加到`jquery.prototype`上面

```js
jQuery.fn = jQuery.prototype = {
                constructor: jQuery,
                css: function () {
                    console.log("css is ");
                },
                show: function () {
                    console.log("show is ok");
                },
                // ...
            }
```



### 省去`new`

`jQuery ` 实际上是一个工厂函数, 作用就是用来`new jQuery.fn.init()`  在把这个对象返回, 只要调用`$ or jQuery` 就能够的到一个jq对象

 ```js
(function (window, undefined) {
            // jQuery 函数暂且理解成是 jq中的构造函数
            var jQuery = function (selector) {
                // 根据selector参数获取到元素
                var el = document.querySelectorAll(selector);
                // 把el中的每一项添加到jq实例对象（this）上
                [].push.apply(this, el);
              }
              
            // 给jq原型添加方法  ==> 原型替换
            // jQuery.fn 是 jQuery.prototype的简写形式
            jQuery.fn = jQuery.prototype = {
              constructor: jQuery,
              css: function () {
                console.log("css is ");
              },
              show: function () {
                console.log("show is ok");
              },
                // ...
              }

              window.jQuery = window.$ = jQuery;
            })(window)
            
            var $divs = new $("div");
            console.log($divs);
 ```





## 浅拷贝

### 什么是浅拷贝

直接的说,就是把对象a的属性和方法的地址给了对象b,他们的指向相同

```js
var obj1={
  age:10,
  sex:"男",
  car:["奔驰","宝马","特斯拉","奥拓"]
};
//另一个对象
var obj2={};

//写一个函数,作用:把一个对象的属性复制到另一个对象中,浅拷贝
//把a对象中的所有的属性复制到对象b中
function extend(a,b) {
  for(var key in a){
    b[key]=a[key];=====>把a的属性的地址给了b,并没有在堆中从新开辟空间
  }
}
extend(obj1,obj2);
```



## 深拷贝

### 什么是深拷贝

把a对象中的属性和方法,复制,在内存空间中重新开辟一个地址空间,这个对象用来存储复制的属性和方法,在把这个对象的地址给对象b ,b 就有了 a的属性和方法

```js
var obj1={
  age:10,
  sex:"男",
  car:["奔驰","宝马","特斯拉","奥拓"],
  dog:{
    name:"大黄",
    age:5,
    color:"黑白色"
  }
};

 var obj2={};//空对象
    //通过函数实现,把对象a中的所有的数据深拷贝到对象b中
    function extend(a,b) {
      for(var key in a){
        //先获取a对象中每个属性的值
        var item=a[key];
        //判断这个属性的值是不是数组
        if(item instanceof Array){
          //如果是数组,那么在b对象中添加一个新的属性,并且这个属性值也是数组
          b[key]=[];
          //调用这个方法，把a对象中这个数组的属性值一个一个的复制到b对象的这个数组属性中
          extend(item,b[key]);
        }else if(item instanceof Object){//判断这个值是不是对象类型的
     //如果是对象类型的,那么在b对象中添加一个属性,是一个空对象
          b[key]={};
          //再次调用这个函数,把a对象中的属性对象的值一个一个的复制到b对象的这个属性对象中
          extend(item,b[key]);
        }else{
          //如果值是普通的数据,直接复制到b对象的这个属性中
          b[key]=item;
        }
      }
    }

 extend(obj1,obj2);
```



## 遍历DOM树

递归的思想

```js
//获取页面中的根节点--根标签
var root=document.documentElement;//html
//函数遍历DOM树
//根据根节点,调用fn的函数,显示的是根节点的名字
function forDOM(root1) {
  //调用f1,显示的是节点的名字
 // f1(root1);
  //获取根节点中所有的子节点
  var children=root1.children;
  //调用遍历所有子节点的函数
  forChildren(children);
}
//给我所有的子节点,我把这个子节点中的所有的子节点显示出来
function forChildren(children) {
  //遍历所有的子节点
  for(var i=0;i<children.length;i++){
    //每个子节点
    var child=children[i];
    //显示每个子节点的名字
    f1(child);
    //判断child下面有没有子节点,如果还有子节点,那么就继续的遍历
    child.children&&forDOM(child);
  }
}
//函数调用,传入根节点
forDOM(root);
function f1(node) {
  console.log("节点的名字:"+node.nodeName);
}
```





## 数组和伪数组

### 数组和伪数组的区别

真数组的长度是可以改变

伪数组的长度是不可以改变的

真数组可以使用数组中的方法

伪数组不能够使用数组中的方法



注意 : argument  是一个伪数组,但是它的长度可以根据函数传入的参数的个数改变而改变

```js
function f1() {
  var sum=0;
  for(var i=0;i<arguments.length;i++){
    sum+=arguments[i];
  }
  console.log(sum);
}
//arguments得到的是实参的个数及实参的每个值

f1(10,20,30,40);
```





## 箭头函数

### 和普通函数的区别

- **this 的改变**

  - 箭头函数this为父作用域的this，不是调用时的this 
  - 箭头函数的this永远指向其父作用域，任何方法都改变不了，包括call，apply，bind。 普通函数的this指向调用它的那个对象。 

  ```js
  
      let person = {
        name: 'jike',
        init: function () {
          //为body添加一个点击事件，看看这个点击后的this属性有什么不同
          document.body.onclick = () => {
            alert(this.name); //this就是 person 
            console.log(this)  //  {name: "jike", init: ƒ}              
          }
        }
      }
      person.init();
  ```

  ```js
  let person = {
      name:'jike',
      init:()=>{
          //为body添加一个点击事件，看看这个点击后的this属性有什么不同
          document.body.onclick = ()=>{
              alert(this.name);//?? this===window
              console.log(this)// window
          }
      }
  }
  person.init();
  ```

  

- **不能当构造函数 , 不能使用 new**

  - 由于this必须是对象实例，而箭头函数是没有实例的，此处的this指向别处，不能产生person实例，自相矛盾。 

  ```js
  //构造函数如下：
  function Person(p){
      this.name = p.name;
  }
  //如果用箭头函数作为构造函数，则如下
  var Person = (p) => {
      this.name = p.name;
  }
  ```

  

- **没有prototype**

  ```js
  var a = ()=>{
    return 1;
  }
  
  function b(){
    return 2;
  }
  
  console.log(a.prototype);  // undefined
  console.log(b.prototype);   // {constructor: ƒ}
  ```

  

-  **箭头函数没有arguments，caller，callee**

  > 箭头函数本身没有arguments，如果箭头函数在一个function内部，它会将外部函数的arguments拿过来使用。 箭头函数中要想接收不定参数，应该使用rest参数...解决。 

```js
let B = (b)=>{
  console.log(arguments);
}
B(2,92,32,32);   // Uncaught ReferenceError: arguments is not defined

let C = (...c) => {
  console.log(c);
}
C(3,82,32,11323);  // [3, 82, 32, 11323]
```



- **箭头函数通过call和apply调用，不会改变this指向，只会传入参数** 

```js
let obj2 = {
    a: 10,
    b: function(n) {
        let f = (n) => n + this.a;
        return f(n);
    },
    c: function(n) {
        let f = (n) => n + this.a;
        let m = {
            a: 20
        };
        return f.call(m,n);
    }
};
console.log(obj2.b(1));  // 11
console.log(obj2.c(1)); //  11
```

### 基本写法

```js
//无函数名,无参数
() => {}
//无函数名,有参数
(num) => {}
//有函数名,有参数
函数名 (参数) => {}
```

- 如果只有一个参数，还可以省略前面的小括号 

```js
const fun = number => {
    return number * 2
}
```

-  如果只有一条执行语句，甚至可以省略后面的大括号，而且可以也不能写 return 

```js
const fun = number => number * 2 
```

- 也可以写成立即执行函数 

```js
const fun = (() => 3 * 2)()  // 6
```









​	