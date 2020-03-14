# JavaScript第一天

## 变量

### 变量的用作

用来操作数据的,可以用来在计算机内存中存储

### 变量的声明

var   num ;   	声明变量不赋值

**多个变量名声明**

```js
var  a , b , c 相当于
   var a
   var b
   var c
   
====================================================
var a = b = c = 1  相当于
var a = 1
b = 1
c = 1
=====================================================
var a = 1 ,
    b = 1, 
    c = 1相当于

var a = 1,
var b = 1,
var c = 1
```



### 变量初始化

给声明的变量进行赋值,

var 	num	= 	10;

### 变量的命名注意问题

变量的命名应该遵守驼峰命名法 

变量的开头不能是数字开头,可以是字母,$,下划线

### var  let 和const 区别

>  在JavaScript中没有块级作用域 , 只有全局作用域和局部作用域 
>
> 在ES6中, 给我们带来了块级作用域 , 使用let 声明的变量只在块级作用域中有效 , 并且约束了 let的提升(不能预解析) ,必须先声明在使用

- **var 存在变量提升,存在预解析 而 let 和const 不存在**

```js
console.log(a); // undefined  ===>  a已声明还没赋值，默认得到undefined值
var a = 100;
console.log(b); // 报错：b is not defined  ===> 找不到b这个变量
let b = 10;
console.log(c); // 报错：c is not defined  ===> 找不到c这个变量
const c = 10;
```

- **var声明的变量会挂载在window上，而let和const声明的变量不会**

  > 我们在全局范围内使用var声明一个变量时，这个变量会自动成为全局对象的属性(在浏览器和Node.js环境下，这个全局对象分别是window和global)，但let是独立存在的变量 

```js
var a = 100;
console.log(a,window.a);    // 100 100

let b = 10;
console.log(b,window.b);    // 10 undefined

const c = 1;
console.log(c,window.c);    // 1 undefined
```

- **let和const声明形成块作用域**

```js
if(1){
    var a = 100;
    let b = 10;
}

console.log(a); // 100
console.log(b)  // 报错：b is not defined  ===> 找不到b这个变量

if(1){

    var a = 100;
        
    const c = 1;
}
 console.log(a); // 100
 console.log(c)  // 报错：c is not defined  ===> 找不到c这个变量
```

- **同一作用域下let和const不能声明同名变量，而var可以**

  > 使用var可以重复声明变量，但let不允许在相同作用域内重复声明同一个变量 

```js
var a = 100;
console.log(a); // 100

var a = 10;
console.log(a); // 10
let a = 100;
let a = 10;

//  控制台报错：Identifier 'a' has already been declared  ===> 标识符a已经被声明了。
```

- **暂存死区**

  > 只要在块内存在let命令，那么这个变量就绑定到了当前块作用域，不再受外部变量的影响，下面代码将会引发一个错误： 
  >
  > ES6规定如果块内存在let命令，那么这个块就会成为一个封闭的作用域，并要求let变量先声明才能使用，如果在声明之前就开始使用，它并不会引用外部的变量。 

```js
    var a = 100;

    if(1){
        a = 10; //不能使用
        //在当前块作用域中存在a使用let/const声明的情况下，给a赋值10时，只会在当前作用域找变量a，
        // 而这时，还未到声明时候，所以控制台Error:a is not defined
        let a = 1;
    }

```

- **const**

  > 以上let所介绍的规则均适用于const命令，不同的是，**const声明的变量不能重新赋值**，也是由于这个规则，**const变量声明时必须初始化**，不能留到以后赋值，所以下面的代码是不合法的 

```js
/*
* 　　1、一旦声明必须赋值,不能使用null占位。
*
* 　　2、声明后不能再修改
*
* 　　3、如果声明的是复合类型数据，可以修改其属性
*
* */

const a = 100; 

a = 5;   // Uncaught TypeError: Assignment to constant variable

const b; // Uncaught SyntaxError: Missing initializer in const declaration

const list = [];
list[0] = 10;
console.log(list);　　// [10]

const obj = {a:100};
obj.name = 'apple';
obj.a = 10000;
console.log(obj);　　// {a:10000,name:'apple'}
```



## 变量交换

使用第三方变量进行交换:

```js
	  var num1=10;
       var num2=20;
      //把num1这个变量的值取出来放在temp变量中
       var temp=num1;
      //把num2这个变量的值取出来放在num1变量中
       num1=num2;
      //把temp变量的值取出来放在num2变量中
       num2=temp;
       console.log(num1);//20
       console.log(num2);//10
```

用于数字交换

```
       var num1 = 10;
       var num2 = 20;
       //把num1的变量中的值和num2变量中的值,取出来相加,重新赋值给num1这个变量
       num1 = num1 + num2;//30
       //num1变量的值和num2变量的值取出来,相减的结果重新赋值给num2
       num2 = num1 - num2;//10
       //num1变量的值和num2变量的值取出来,相减的结果重新赋值给num1
       num1 = num1 - num2;//20
       console.log(num1, num2);
```

## 代码注释

多行注释    /**/

单行注释    //

## 数据类型

可以使用  typeof   获取数据类型

用法：

```
 typeof 变量名
 typeof(变量名)
 	var num = 10;
    var str = "小白";
    var flag = true;
    var nll = null;
    var undef;
    var obj = new Object();
    //是使用typeof 获取变量的类型
    console.log(typeof num);//number
    console.log(typeof str);//string
    console.log(typeof flag);//boolean
    console.log(String(nll));//是null
    console.log(typeof nll);//不是null
    console.log(typeof undef);//undefined
    console.log(typeof obj);//object
    console.log(typeof(num));
```

## 数字类型

数字类型：整数和小数

```
数字类型有范围: 最小值和最大值
//    console.log(Number.MAX_VALUE);//数字的最大值
//    console.log(Number.MIN_VALUE);//数字的最小值
```

 注意事项：

```
不要用小数去验证小数
var x=0.1;
//    var y=0.2;
//    var sum=x+y;
//    console.log(sum==0.3);
```

NaN ：不是一个数据 ，但是它是一个数字类型 

它不等于任何值，包括他自己

```js
不要用NaN验证是不是NaN

//    var num;
//    console.log(num+10==NaN);
//    console.log("您好"=="我好");

  如何验证这个结果是不是NaN,应该使用isNaN()
isNaN（）  是不是不是一个数字  
不是一个数字的时候取值为true  是一个数字的时候取值为false
```

## 字符串类型

字符串可以使用单引号也可使用双引号

JS中的转义字符

![](E:\JS学习\01 day\js最新发放资料\html和js转义符\js中转义符.png)

## 布尔类型（Boolean）

取值：两个 true 和 false



## 类型转换（parseInt  toSring()  ）

### 其他类型转数字类型（5种）：

1 、parseInt（“ ”）； 转整数

2 、parseFloat（“ ”）；转小数

3 、 Number（“ ”）；转数字  （严格）

4 、在前面加+（正号）

```js
var num1='123';
console.log (+num)// 数字123
```

5、 -  /   * 运算符 

### 其他类型转字符串型 （3种）

变量如果有意义调用toString()方法 ，变量如果无意义使用String（）进行转换

1、toString()

```js
语法：值 . toString()
var num=10;
//    console.log(num.toString());//字符串类型
```

2、String ()

```
var num1=20;
//    console.log(String(num1));
```

3、拼接字符串===》结果就是字符串

```
//拼接空串
var num1=20;
//    console.log(num1 + '');
```



### 其他类型转布尔类型（2种）

 一、  很过数据类型转布尔类型都是true

转换成flase的数据只有6个

0   、' '  、flase  、 undefined 、null 、NaN  转布尔类型都是false

```js
	console.log(Boolean(1));//true
//    console.log(Boolean(0));//false
//    console.log(Boolean(11));//true
//    console.log(Boolean(-10));//true
//    console.log(Boolean("哈哈"));//true
//    console.log(Boolean(""));//false
//    console.log(Boolean(null));//false
//    console.log(Boolean(undefined));//false
```



二 、 ！！（飞飞）  转布尔类型



```js
"0" == false  // ? true or false
//result===> true

因为他们在比较的时候，并不是把结果转换成布尔类型比较，而是转换成数字类型进行比较 ，"0"==> 0  false
0 == 0 ; //true`
```



## 操作符

### 算数运算符

算数运算符  +  -  *  /

算数运算符表达式：由算术运算符连接起来的式子

一元运算符 ：++  ——

二元运算符：+  — *  /

三元运算符  : a>b? a:b

复合运算符 ：+=    *=    —=      /=     %=

复合运算表达式：用复合运算符连接起来的式子



### 关系运算符

关系运算符：>  <   ==（不严格）  ===（严格）   != （不严格）  !===(严格)

关系运算符表达式：关系运算符连接的式子

关系运算符的结果是布尔类型



### 逻辑运算符

逻辑运算符 ：&&   逻辑与 （并且）  || 逻辑或 （或者）  ！逻辑非  （逻辑非  ---取反）

&&  有一个结果为false 则整体结果为false

|| 有一个结果为true 则整体结果为 true

! true   结果为 false

```javascript
			false ||  true  &&  true && true 
var result = (4 >= 6 || '人' != '狗' && !(12 * 2 == 144) && true);
//    console.log(result);
//结果为true 
```



**&& 和 ||的逻辑**

当 &&两遍不是 布尔类型, 返回的是两遍的值

> 复杂数据类型转成布尔类型是 `true`

```js
console.log( 1 && 2 ) // 2
console.log( 1 && [] ) // []
```

&&短路

> 如果第一个符合条件, 后面的就不看了, 返回第一个值

> 当第一个转成布尔类型不符合条件(false), 会看第二个, 并且返回第二个

`0` 转布尔类型时`false`

```js
console.log( 0 && [] ) // 0

#回调函数的应用场景

fn && fn()
当fn不存在时, 就不会再看 fn() , 只有当fn转布尔为 true 时, 才会看 fn(), 并且返回fn()
```



**|| 短路逻辑**

当第一个符合条件 , 就不会再看第二个条件, 并且返回第一个条件

第一个不符合条件, 再看第二个条件, 返回第二个条件

```js
1 || 2  // 1
0 || 2  // 2

# if条件中的 || 应用
if (i=1 || i=2 )
当i=1不存在是,才会看第二个
```



# JavaScript第二天

## 一元运算符

++  和 - -都输一元运算符

但是++  和  --  放在不同位置,结果就不同

```
i++  	++i
不参与运算时,结果相同
当参与运算时,i++ 是先参与运算,运算结束后再自身加一
++i 是先自身+1 在参与运算
```

## 流程控制

分为三种结构

1 顺序结构 : 代码从上到下执行

2 分支结构 : if语句  if -else if -  else 语句 和 switch-case 语句,三元表达式

3 循环结构 : while 循环    do-while 循环    for循环

### 分支语句

#### if 语句

```
if语句:主要是判断
* 语法:
* if(表达式){
*   代码块
* }
先判断表达式中的结构是true还是false 结果为true则执行代码块 	结果为false 则不执行
```

#### if-else 语句

```
语法:
if (表达式1) {
    代码块1
} else {
    代码块2
}
只执行一次,如果表达式1结果为true 则执行代码块1  否则执行代码块2
```

#### if-else if-else	语句

```js
语法:
if (表达式1) {
    代码块1
}else if (表达式2) {
      代码块2
}else if (表达式3) {
      代码块3
}else {
      代码块4
}
结果也执行一次
//练习:判断一个年份是不是闰年
    //定义变量存储一个年份
    var year = 2017;
    if (year % 4 == 0 && year % 100 != 0 || year % 400 == 0) {
      console.log("闰年");
    } else {
      console.log("平年");
    }
```

#### 三元表达式

```js
运算符号:  var 变量 =  表达式1 ?  表达式2 : 表达式3 ;
如果表达式1的结果为true 则 把表达式2的值赋给变量  
如果表达式1的结果为false 则 把表达式3的值赋费变量

//两个数字中的最大值
    var x = 10;
    var y = 20;
    var result1 = x > y ? x : y;
    console.log(result1);
```

#### switch-case 语句

多分支语句  ；case中的比较时全等比较

```js
语法:
* switch(表达式){
*  case 值1:代码1;break;
*  case 值2:代码2;break;
*  case 值3:代码3;break;
*  case 值4:代码4;break;
*  ...多个case
*  default:代码5;
*
* }
注意问题 :
default 是可以省略的 default后面的break也是可以省略的
switch-case 语句中的case后面的值进行比较时使用的是严格的模式 (===) 变量类型和值都相等时才相等
 
 
 var num = "10";//字符串
//    console.log("10"===10);//false
//    switch (num) {
//      case 10:
//        console.log("数字的10");
//        break;
//      case "10":
//        console.log("字符串的10");
//        break;
//    }
执行过程:
case的值和表达式中的值进行比较,当相等时,则执行代码 ,遇到break 直接跳出循环 后面的代码都不执行

代码优化问题:
当case 后面的代码多个相等时,可以省略只写一个
例如:
var month=parseInt(prompt("请输入月份"));
//    switch (month){
//      case 1:
//      case 3:
//      case 5:
//      case 7:
//      case 8:
//      case 10:
//      case 12:console.log("31天");break;
//      case 4:
//      case 6:
//      case 9:
//      case 11:console.log("30天");break;
//      case 2:console.log("28天");break;
//    }
```

#### 总结分支语句

if 语句 : 只有一个分支

if-else : 有两个分支 但只执行一个分支

if-else if 语句 有多个分支但是也只执行一个分支

switch - case : 有多个分支 最终也只会执行一个语句

三元表达式: 有两个分支 但也只执行一个分支

**if -else if 语句 和switch-case  使用**

当多分支语句,是针对范围的时候,可以使用if-else if语句  if()可以判断一定的范围

当多分支语句,是针对具体值得时候,可以使用switch -case 语句



### 循环语句

#### while循环

```js
语法:
  var i=0;  //计算器
  while (条件) {
      循环体;
      i++;
  }
  执行过程,先判断条件是否成立,结果为true则执行循环体,否则不执行
  优点: 不需要知道循环的次数,只需要循环条件就可以执行
  例子:
  var sum=0;//存储最终的和
    var i=1;//计数器
    while(i<=100){
      //sum=sum+i;//不停的计算数字的和
      sum+=i;
      i++;
    }
    console.log("和为:"+sum);
```

#### do-while 循环

```
语法:
do {
    循环体;
    i++
}while (循环条件);
至少会执行一次,然后判断循环条件,结果为true,则继续执行循环体,否则跳出循环体
```



#### 总结while语句和do-while语句

while: 先判断条件是否成立在执行循环体

do-while : 先执行一次循环体,在判断条件是否成立  至少执行一次循环体



#### for循环

```javascript
语法:
 	for ( 表达式1; 表达式2; 表达式3) {
        循环体;
 	}
 执行过程:
 先执行表达式1,然后判断表达式2是否成立,如果不成立则直接跳出循环
 如果表达式2成立,则执行循环体,一直如此,知道表达式2不成立跳出循环
 例子:
  //控制行数的---正方形的
    for (var i = 0; i <= 5; i++) {
      //控制每一行有几个星星
      for (var j = 0; j <= 5; j++) {
        document.write("★");
      }
      document.write("<br/>");
    }
    //乘法口诀表
   document.write("<table border='1' cellpadding='0' cellspacing='0'>");
	for (var i = 1; i <= 9; i++) {
		document.write("<tr>");
		for (var j = 1; j <=i ; j++) {
			document.write("<td>");
			document.write(j+"*"+i+"="+i*j);
			document.write("</td>");
		}
		document.write("</tr>");
	}
	document.write("</table>");
	    
```

## 代码调试( Chrome中调试)

在F12开发者工具中sources选项中双击文件→点击行数可以设置断点→右侧进行调试

![](E:\JS基础\02 day\1.png)

右侧向上箭头可以对断点进行单步调试

watch 中可以查看具体各个元素的值

**右侧的几个按钮**

> 第一个按钮 :  结束当前的断点,进入下一个断点
>
> 第二个按钮  : 在普通的代码中,就向下执行一步, 如果遇到函数的调用,会瞬间把函数执行完
>
> 第三个按钮 :  往下执行一步 , 进入函数,  一步一步的执行 
>
> 第四个按钮 : 让函数的代码 ,  瞬间执行完



# JavaScript第三天



## 循环中的关键字使用

### break关键字

在循环体中,放=当遇到break关键字则立即跳出当前循环,不在执行循环体

### continue关键字

当在循环体中遇到continue关键字,会跳出本次循环,继续下一轮的循环,会继续执行循环体

## 数组(Array)

数组的作用:一次性储存多个数据

### 数组的定义方法(2种)

1 通过构造函数创建数组

```
var 数组名=new Array();
当Array()中为空时,则为一个空数组
当Array(5)中一个数字是,则代表的是数组的长度
当Array(1,2,3,5,6)是多组数据时,则代表数组存储的是一组数据,数组就有了长度(length)

当Array(5)数组定义了长度,没有数据,则默认为undefined
```

2 字面量的方式创建数组(常用)

```js
var 数组名=[];

var array=[] 则为一个空数组,长度为0
var array=[5] 则代表数组的长度为1,值为5
array=[1,2,3,4] 则代码数组有数据

数组的索引:也叫下标,从0开始,代表数组中每个元素的位置;
如何设置数组中某个位置的值:
arr [下标]=值;
arr[3]=10;
```



### 数组的注意问题

1  数组中存储的每个数据的数据类型可以不同;

```
var arr=[10,"哈哈",true,null,undefined,new Object()];
```

2  数组的长度是可以改变的,可以通过索引的方式设置数组中的值

```
var arr=[];
//通过索引来设置数组中的元素的值
arr[0]=10;
arr[1]=20;
console.log(arr.length);
```

3 获取数组中的值,通过索引的方式

### for循环遍历数组

```
var arr=[10,20,30,40,50,60,70,80,90,100];
//小于的是数组的长度--个数
    for(var i=0;i<arr.length;i++){
      console.log(arr[i]);
    }
```

#### 求数组中所有元素的和

```
var arr1 = [10, 20, 30, 40, 50];
var sum = 0;
for (var i = 0; i < arr1.length; i++) {
  sum += arr1[i];
}
```

#### 求数组中所有元素的最小值

```
//案例4:求数组中所有元素的最小值
var arr4 = [100, 10, 20, 30, 40, 50];
var min = arr4[0];//假设min里存储的就是最小值
for (var i = 0; i < arr4.length; i++) {
  if (min > arr4[i]) {
    min = arr4[i];
  }
}
```

#### 倒序遍历数组

```
for (var i = arr5.length - 1; i >= 0; i--) {
   console.log(arr5[i]);
}
```

#### 冒泡排序(重点)

```js
//冒泡排序:把所有的数据按照一定的顺序进行排列(从小到大,从大到下)
var arr = [10, 0, 100, 20, 60, 30];
var count = 0;
//循环控制比较的轮数
for (var i = 0; i < arr.length - 1; i++) {
  //控制每一轮的比较的次数
  for (var j = 0; j < arr.length - 1 - i; j++) {
      count ++;
    if (arr[j] < arr[j + 1]) {=========/降序
      var temp = arr[j];
      arr[j] = arr[j + 1];
      arr[j + 1] = temp;
    }
  }
}
console.log(arr);
console.log(count) //21次 
```

####冒泡排序的高级版

优化点：以下特殊情况

- 如果数组本身排好序的，那么不需要排很多次
- 如果数组第一趟下来就排好了，后面的不需要排了

假设成立法：假设这一趟已经排好了（那么一趟下来不会交换），设置变量flag=true，当交换的时候设置flag=false。

- 如果真的排好了，一趟下来flag还是true，此时结束循环break
- 如果还没排好，一趟下来flag会改成false，此时不执行break

```js
//冒泡排序:把所有的数据按照一定的顺序进行排列(从小到大,从大到下)  
var arr = [10, 0, 100, 20, 60, 30];
//循环控制比较的轮数
for (var i = 0; i < arr.length - 1; i++) {
  //控制每一轮的比较的次数
  var flag = true;// 假设这一趟已经排好的，true
  
    for (var j = 0; j < arr.length - 1 - i; j++) {
    	if (arr[j] > arr[j + 1]) {  ======/ 升序
      	var temp = arr[j];
      	arr[j] = arr[j + 1];
      	arr[j + 1] = temp;
        flag = false; //只要交换位置，表示这一趟还没排好，下一次继续
    	}
  	}
   	if(flag) {
        break;// 如果flag在这一趟下来没有改变，还是true，说明已经排好，此时结束循环
    }
}
console.log(arr);
```



## 函数(function)

### 函数的作用

将一些重复的代码进行封装,在使用时直接调用即可

### 函数的格式

```
//声明函数
function 方法名() {//函数定义
  代码块
}
//调用函数
方法名();
```

### 形参和实参

形参:函数在定义时,方法名小括号里的变量就是形参

实参:在调用的时候,小括号里,传入的值就是实参,实参可以是变量也可以值

**传参问题**

> 实参传多了: 多出来的会被忽略
>
> 传少了 : 没传的参数时 undefined

### 函数的返回值(return)

```
函数的返回值:在函数内部有return关键字,并且在关键字后面有内容,这个内容被返回了
```

当函数调用时,可以定义一个变量对返回值进行接收,用户拿到这个返回值可以在进一步操作

注意事项:

如果一个函数没有返回值,当定义变量接收时,就是undefined

变量声明没有赋值,结果也是undefined

```
function f1(x,y) {
  var sum= x+y;
}
var result=f1(10,20)
console.log(result);//undefined
```

函数中没有明确返回值则函数没有返回值

函数中有返回值,则return下面的代码则不会执行



# JavaScript第四天

### 函数案例练习

```
// 求3个数中的最大值
function getThreeMax(x, y, z) {
  return x > y ? (x > z ? x : z) : (y > z ? y : z);
}
console.log(getThreeMax(10,2,24));
```



```js
// 判断一个数是否是素数(质数),只能被1和自身整除，质数是从2开始
//用这个数字和这个数字前面的所有的数字整除一次(没有1的,没有自身的)
function isPrimeNumber(num) {
  for(var i=2;i<num;i++){
    if(num%i==0){
      //说明有一个数字整除了,就没有必要向后继续整除了,此时就已经验证出不是质数
      return false;
    }
  }
  return true;
}
console.log(isPrimeNumber(8)?"是质数":"不是质数");
```



```js
//求一组数字中的最大值
function getArrayMax(array) {
  //定义变量假设这个变量中存储的是最大值
  var max = array[0];
  for (var i = 0; i < array.length; i++) {
    if (max < array[i]) {
      max = array[i];
    }
  }
  return max;
}
//    var arr=[10,20,30,40,50];
//    var max=getArrayMax(arr);
//    console.log(max);
var max = getArrayMax([10, 20, 30, 40, 50]);//可以直接把数组传到函数中的
console.log(max);
```



```js
//求一组数字的和
function getArraySum(array) {
  var sum = 0;
  for (var i = 0; i < array.length; i++) {
    sum += array[i];
  }
  return sum;
}
console.log(getArraySum([1, 2, 3, 4, 5, 6]));
```



```js
//求一个数组中的最大值和最小值还有和
/**
 *  给我一个数组,我返回一个数组(最大值,最小值,和)
 * @param array参数是一个数组
 * @returns {*[]}返回值是一个数组,第一个元素值是最大值,第二个元素值是最小值,第三个元素值是和
 */
function getArrayMaxAndMinAndSum(array) {
  var min = array[0];//最小值
  var max = array[0];//最大值
  var sum = 0;//和
  for (var i = 0; i < array.length; i++) {
    sum += array[i];//和
    //最大值
    if (max < array[i]) {
      max = array[i];
    }// end if
    //最小值
    if (min > array[i]) {
      min = array[i];
    }// end if
  }// end for
  var arr = [max, min, sum];
  return arr;
}
//测试
var resultArray = getArrayMaxAndMinAndSum([1, 2, 3, 4, 5, 6, 7]);
console.log("最大值:" + resultArray[0]);//7
console.log("最小值:" + resultArray[1]);//1
console.log("和:" + resultArray[2]);//28

//通过函数实现数组反转
function reverseArray(arr) {
  for (var i = 0; i < arr.length / 2; i++) {
    var temp = arr[i];
    arr[i] = arr[arr.length - 1 - i];
    arr[arr.length - 1 - i] = temp;
  }
  return arr;
}
console.log(reverseArray([1, 2, 3, 4, 5]));
```

```
//求一个数字的阶乘
function getJieCheng(num) {
  var result = 1;
  for (var i = 1; i <= num; i++) {
    result *= i;
  }
  return result;
}
console.log(getJieCheng(5));//1*2*3*4*5
```



```
//求一个数字的阶乘和  5  5的阶乘+4的阶乘+3的阶乘+2的阶乘+1的阶乘
function getJieChengSum(num) {//5
  var sum=0;//和
  for(var i=1;i<=num;i++){
    sum+=getJieCheng(i);
  }
  return sum;
}
console.log(getJieChengSum(5));
//1 +2+ 6+ 24+120
```

**斐波那契数列**

```js
/求斐波那契数列,12---144
//1 1 2 3 5 8 13 21 34 55 89 144
function getFib(num) {
  var num1=1;
  var num2=1;
  var sum=0;
  for(var i=3;i<=num;i++){
    sum=num1+num2;
    num1=num2;
    num2=sum;
  }
  return sum;
}
console.log(getFib(12));
```

输入一个年月日判断是一年的第多少天

```js
//输入,年月日,获取这个日期是这一年的第多少天
//判断这个年份是不是闰年
function isLeapYear(year) {
  return year%4==0&&year%100!=0||year%400==0;
}
//年---月---日:2017年4月28日
function getDays(year, month, day) {
  //定义变量存储对应的天数
  var days = day;
  //如果用户输入的是一月份,没必要向后算天数,直接返回天数
  if (month == 1) {
    return days;
  }
  //代码执行到这里-----说明用户输入的不是1月份
  //用户输入的是7月份23日----1，2，3  +23
  //定义一个数组,存储每个月份的天数
  var months = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];
  //小于的是输入的月份-1
  for (var i = 0; i < month - 1; i++) {
    days += months[i];
  }
  //需要判断这个年份是不是闰年
  if(isLeapYear(year)&&month>2){
    days++;
  }
  return days;
}
 console.log(getDays(2000,3,2));
```



### arguments对象（伪数组）

arguments是一个伪数组，能够动态的根据数组中值得变化而变化

出现背景：需要计算1-n的和时，不知道数组的长度，就无法通过循环进行计算

​		定义一个函数，不确定用户传了几个值，或者说不知道用户传了几个参数，此时我门就可以使用arguments获取数组的

例子：计算N个数的和

```
function f1() {
  //arguments----->数组使用------伪数组---
  var sum=0;
  for(var i=0;i<arguments.length;i++){
    sum+=arguments[i];
  }
  return sum;
}
console.log(f1(10,20,30));
```



### 函数的命名方式

命名函数：函数有名字，可以直接调用

```
 function f1() {
      console.log("哈哈,我又变帅了");
    }
```

匿名函数： 函数没有函数名

如果想要调用函数，就必须给函数设置一个变量名进行接收，此时就形成了函数表达式

```
var 变量=匿名函数;
* 例子:
* var f1=function (){
*
* };
```

函数自调用：声明与调用同时进行

```
(function(){console.log("阿涅哈斯诶呦");})();
(function(){console.log("嘎嘎")})();
```

函数也是一种数据类型



### 函数作为参数使用（不易理解）

函数可以作为参数使用，如果这个函数作为参数使用，那么我们说这个参数（函数）可以叫回调函数

只要看到一个函数作为参数使用，都可以称为回调函数

```
function sayHi(fn) {
  console.log("您好啊");
  fn();//fn此时应该是一个函数
}
function suSay() {
  console.log("我猥琐,我邪恶,我龌龊,小苏说");
}

sayHi(suSay); 调用函数时，先进入sayHi中，这是就输出了（“您好啊”），继续向下执行时，到fn();fn()就说明此时fn就是一个函数，  fn();就等于suSay函数执行了 function suSay() {
  								console.log("我猥琐,我邪恶,我龌龊,小苏说");
								}
```



### 函数作为返回值使用

```
function f1() {
  console.log("f1函数调用了");
  return function () {
    console.log("这是一个函数");
  };
}
var ff=f1();//调用
    //ff就是一个函数了
    ff();
```



### 全局变量和局部变量

- 全局变量：用var 声明的变量，全局变量可以在页面的任何位置生效
- 局部变量： 在函数内部声明的变量，只在函数内部起作用

>  除了在函数中声明的变量，其他地方都是全局变量

- 隐式全局变量：声明变量没有用var
  - 在函数内部没有声明的变量 , 如果有嵌套 , 会逐层向外找, 如果最外层`funcition`  也没有声明 , 才会创建一个隐式全局变量
- 全局变量是不能被删除的，但是隐式全局变量可以被删除



### 作用域

- 全局作用域：全局变量的使用范围

- 局部作用域：局部变量的使用范围  函数内部就是一个局部作用域

  > 再函数内部声明的变量, 函数外部无法访问

### 作用域链

> 函数嵌套的时候，当里面的函数需要使用某个变量的时候，会先向自己的函数中查找，当自己没有时，会向上一级函数查找，这样的过程就是作用域链

```js
var num=10;
function f1() {
  var num=20;
  function f2() {
    var num=30;
    function f3() {
      var num=50;
      console.log(num);
    }
    f3();
  }
  f2();
}
f1();
```



### 预解析

代码在执行的过程中，会先进行预解析，预解析会将变量的声明和函数的声明提前，**但不会将变量的赋值提前**

> **同时声明了同名的变量和函数 , 在预解析的时候,函数优先, 函数会把变量覆盖**  ===> 尽量避免同名

**预解析只会在当前的script的模块中**

```js
var a = 1;
function a() {}
console.log(a) //  1
```



### 匿名函数的自调用 ( 沙箱 )

两种方式

```js
//方式一 
(function () { 
        console.log('哈哈哈')
  })()

//方式二   分号省略写法时, 遇到 (   [  `   前面要加 ;
  ;(function () { 
         console.log('嘿嘿嘿')
    }())
```



**预解析案例** : 只提升声明 

```js
//变量声明和函数声明提前之后,函数被把变量覆盖 , 然后执行代码, 遇到 var a = 11 , 此时的 a 就由一个函数变成了一个数字11 , 所以 第一次输出是 11 , 第二次输出会报错, 因为 a 不是一个函数 不能调用 

var a = 11 

    console.log(a)  //11

    function a () {
      console.log('嘿嘿嘿')
    }

    a() //  报错
```



```js
    console.log(a) //函数体

    function a () { 
      console.log( '嘿嘿' )
     }

     var a = 1 
     console.log(a) //1
  
```



**函数内部的预解析**

```js
//1、 每个作用域中都有预解析——》函数内部也会预解析
var num = 10;
fn1(); //undefined   函数内部把num 声明提前了,但是没有赋值
function fn1() {
  console.log(num);
  var num = 20;
}
```



**预解析案例**

```js
函数调用的时候,把会函数的声明提升到作用域的上面
//    f1();//调用
//    var num=20;//这个变量的声明会提升到变量使用之前
//    function f1() {
//      console.log(num);
//      //var num=10;
//    }
```

预解析之后：

```js
函数调用的时候,把会函数的声明提升到作用域的上面
//    
//    var num=20;//这个变量的声明会提升到变量使用之前
//    function f1() {
		var num；
//      console.log(num);//undefined
//      //var num=10;
//    }
	f1();//调用
```



预解析分段问题：

>  不同script标签中，函数重名时，不会相互影响



# JavaScript第五天

## JS是一门什么样的语言

```js
js是一门什么样的语言?
* 是一门解释性的语言
* 是一门脚本语言
* 是一门弱类型语言,声明变量都用var
* 是一门基于对象的语言
* 是一门动态类型的语言:
* 1. 代码(变量)只有执行到这个位置的时候,才知道这个变量中到底存储的是什么,如果是对象,就有对象的属性和方法,如果是变量就是变量的作用
* 2. 对象没有什么,只要点了,通过点语法,那么就可以为对象添加属性或者方法
```

## 什么是对象

```
编程思想:把一些生活中做事的经验融入到程序中

面向过程:凡事都要亲力亲为,每件事的具体过程都要知道,注重的是过程

面向对象:根据需求找对象,所有的事都用对象来做,注重的是结果

JS是一门基于对象的语言
```

## 创建对象的三种方式

### 调用系统的构造函数创建对象

```
var 变量名= new Object(); // Object 是系统的一种构造函数
```

```js
var obj=new Object();//实例化对象
obj.name="小明";//添加对象的属性.并赋值
obj.play=function () {
    console.log();
}
对象不需要return 对象会自动产生返回值
obj.play();//方法的调用
```

如何获取该变量(对象)属于什么类型

**变量    instanceof   类型名字------->>>>布尔类型  true就是这种类型 false不是这种类型**

**typeof  输出 一个对象的数据类型**

### 工厂模式创建对象

将创建对象的函数封装进一个函数中,调用这个函数即可对创建对象,不过还是使用的是系统的构造函数

```js
//工厂模式创建对象
function createObject(name,age) {
  var obj = new Object();//创建对象
  //添加属性
  obj.name = name;
  obj.age = age;
  //添加方法
  obj.sayHi = function () {
    console.log("阿涅哈斯诶呦,我叫:" + this.name + "我今年:" + this.age);
  };
  return obj;
}
//创建人的对象
var per1 = createObject("小芳",20);
per1.sayHi();
//创建一个人的对象
var per2 = createObject("小红",30);
per2.sayHi();
```



### 自定义构造函数创建对象

不使用系统的构造函数创建对象,我们自己写一个构造函数创建对象

函数和构造函数的区别:

> 函数的函数名开头是小写字母,构造函数的函数名开头是大写(实际并没有太大区别)

```js
//构造一个Person的函数
function Person(name,age) {
  this.name=name;
  this.age=age;
  this.sayHi=function () {
    console.log("我叫:"+this.name+",年龄是:"+this.age);
  };
}

//创建对象 并赋值
var per1=new Person("小明",20);
per1.sayHi();
```



### 字面量的方式创建对象

```js
var obj={};
obj.name="小明";
obj.sex="3岁";
obj.sayHi=function () {
    consolie.log("哈哈,我又变帅啦");
};
obj.sayHi();
```

设置和获取属性的另一种写法:

```js
obj.sayHi();
obj["sayHi"]();

将点后面的属性或者方法变成[""]的方式 		注意[]中要加""
```



## 自定义构造函数实例对象时,系统做的几件事(new)

**`new`**的作用 : 创建对象

> 1 在内存中开辟一盒空间,存储创建的新对象, 并且空对象有对应的类型

> 2 把this设置为当前的对象=========================>指向实例对象

> 3 执行构造函数中的代码 , 设置对象的属性和方法=======> 实例化对象

> 4 把 this这个对象返回============================>返回实例对象



`new`  一个对象时,不需要构造函数中的创建的对象`return` , `new` 会自动把这个对象返回

但是如果是执行普通的返回 , 需要对输出结果进行操作, 必须 `return`

## 点语法和中括号语法

### 点语法

- 取值：对象名.属性名
- 赋值：对象名.属性名 = 值
- 对象没有某个属性, `对象.`了,就有了这个属性 ,但是只是创建了这个属性, 没有赋值 ,返回 undefined

```js
var obj= {
    name : 'zs',
    age : 18,
    color : 'red'
}
console.log(obj[str]) // undefined
```



### 中括号语法(关联数组语法)

> 把对象当做数组进行操作
>
> 在js中 `.` === ` [''] `

```js
对象名[ '属性名' ]
```

- **`[]`中可以写一个变量**

```js
var obj= {
    name : 'zs',
    age : 18,
    color : 'red'
}

var str = 'name',
console.log(obj[str]) //zs
```

### 应用场景

```js
 var obj = {}

      for (let i = 1; i <= 10; i++) {
        obj[`n${i}`] = i       
      }
      console.log(obj) //{n1: 1, n2: 2, n3: 3, n4: 4, n5: 5, …}

//法二
    var obj = {}
      for (let i = 1; i <= 10; i++) {
        var str = 'n'+i   
        obj[str] = i   
      }
      console.log(obj)
```



## JSON格式的数据

都是成双成对了,通过键值对的方式

```
var json = {
  "name": "小明",
  "age": "10",
  "sex": "男"
};
```

## 遍历对象

不能通过for循环遍历对象,因为对象是无序的

所以只能用for-in遍历对象

```js
var json = {
  "name": "小明",
  "age": "10",
  "sex": "男"
};   //key="属性值"  声明一个变量存储对象中的属性名;
 for (var key in json) {
      console.log(key + "===========" + json[key]);
    }								==json["name"]);
    								==json["age"]);
                                       ==json["sex"]);
```



## 数据类型(简单类型和复杂类型)

原始数据类型---(number,string ,boolean, null, undefined,object)

### 简单类型(值类型)

>  **number , string , boolean , undefined , null**
>
> 简单类型作为函数的参数,传递的是值 ,值存在栈上 

```
原始数据类型: number,string,boolean,undefined, null,object
//基本类型(简单类型),值类型: number,string,boolean , null ,undefined
//复杂类型(引用类型):object , array , function
//空类型:undefined,null
```

### 复杂类型(引用类型) 

> **复杂类型(引用类型):object , array , function**

**复杂类型传递的地址(栈)===>>地址指向堆中的对象**

```js
var obj={
  name:"小明"
};
function f2(obj2) {
  obj2.name="小红";
}
console.log(obj.name);//小明
f2(obj);
console.log(obj.name);//小红
```

识别传递的值是什么

```js
function Person(name,age,salary) {
  this.name = name;
  this.age = age;
  this.salary = salary;
}
function f1(person) {
  person.name = "ls";
  person = new Person("aa",18,10);
}

var p = new Person("zs",18,1000);
console.log(p.name);//zs
f1(p);
console.log(p.name);//ls
```



## 内置对象

内置对象就是系统自带的对象

JS的三种对象:

- 1   内置对象   Math  Date  String Array  Object
- 2   自定义对象
- 3  浏览器对象

```
//如何验证变量是不是对象
//    console.log(Array instanceof Object);
//    var obj={};
//    console.log(obj instanceof Object);
```



### Math 对象

Math是一个对象,但不是一个函数,MAth下的属性和方法都是静态的

Math.PI  ------π

Math.E------->e

Math.abs(值)----->绝对值

Math.ceil(值)--->向上取整 , 取大的那个数( -1.9→ -1 )

Math.floor(值)---->向下取整  取小的那个数 (  -1.2 → -2 )

Math.round(值)---->四舍五入取整 

Math.max();--->获取一组数中的最大值

Math.min()----->获取一组数中的最小值

Math.pow(2,4)----->去一个数的多少从方--->  `2的四次方`

Math.aqrt(16)----->开方

**Math.random()---->获取一个随机数 取值0到1, 不包括1 ` [ 0 , 1 )`**

```
//0-4  没有5
console.log(parseInt(Math.random()*5)+1);  //从1-4获取随机数
console.log(parseInt(Math.random()*100)+1);//从1到99获取随机数
```



# JavaScript第六天



## Math对象的案例

 Math.random()随机数案例

随机产生一个十六进制的颜色值

```js
function getColor() {
      var str = "#";
      //一个十六进制的值的数组
      var arr = ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9", "a", "b", "c", "d", "e", 		"f"];
      for (var i = 0; i < 6; i++) {
        //产生的每个随机数都是一个索引,根据索引找到数组中对应的值,拼接到一起
        var num = parseInt(Math.random() * 16);//定义一个变量存储数组的索引值
        str += arr[num]; 	//将遍历的每个字母拼接在一起
      }
      return str;//返回一个十六进制的颜色字符串
    }
    console.log(getColor());
```



## Date对象

### 用法

var dt=new Date();  //实例化一个时间对象dt

console.log(dt);	//输出系统的当前时间

> 也可以自己传入时间 , 指定日期对象的的时间

```js
 var dt=new Date("2017-08-12 00:00:00");
    //传入的时间
    console.log(dt);
```

### Date对象下的方法

> dt . toDateString 	()	//获取日期
>
> dt . toLocaleDateString ()  	//日期

> dt.toLocaleString()          //日期和时间

> dt . toTimeString () 		//时间
>
> dt . toLocaleTimeString ()    //时间

> dt . getFullYear();		//年
>
> dt . getMonth ()+1	//月   从0开始
>
> dt . getDate ()		//日
>
> dt . getHours ()		//时
>
> dt . getMinutes ()		//分
>
> dt . getSeconds ()  	//秒
>
> dt . valueOf ()		//毫秒
>
> dt . getDay ()			//星期 从0开始



### 格式化时间

```js
/**
 * 获取指定格式的时间
 * @param dt 日期的对象
 * @returns {string} 返回的是字符串的日期时间
 */
function getDate(dt) {
    //获取年
    var year = dt.getFullYear();
    //获取月
    var month = dt.getMonth() + 1;
    //获取日
    var day = dt.getDate();
    //获取小时
    var hour = dt.getHours();
    //获取分钟
    var minute = dt.getMinutes();
    //获取秒
    var second = dt.getSeconds();
    month = month < 10 ? "0" + month : month;
    day = day < 10 ? "0" + day : day;
    hour = hour < 10 ? "0" + hour : hour;
    minute = minute < 10 ? "0" + minute : minute;
    second = second < 10 ? "0" + second : second;
    return year + "年" + month + "月" + day + "日 " + hour + ":" + minute + ":" + second;
}

	var dt= new Date();
	console.log(getDate(dt));
```



### 时间戳

> 数字格式的事件, 获取的是毫秒 , 从1970年到现在所过去的毫秒数

```js
var now = new Date()
console.log(+now) //打印时间戳 , 把字符串转成数字类型
//或者
console.log( Number(now) ) 
```

**应用**

计算代码的执行时间 = 代码结束的时间戳 - 代码开始的时间戳

对于一个需求多种代码方案,可以通过代码时间戳验证代码的优良性

**倒计时**

```js
  var end = new Date('2019-8-26 12:30:00') //结束时间

    setInterval(function () {
      var now = new Date() //当前时间

      var time = end - now //获取时间戳

      time = time / 1000 //转化为 秒

      //时
      var hour = parseInt(time / 3600)
      //分钟
      var minute = parseInt(time / 60) % 60
      //秒
      var second = parseInt(time % 60)
      console.log('倒计时 : ' + hour + '时' + minute + '分' + second + '秒')
    }, 1000)
```





## Array对象

###伪数组转数组

```js
//使用系统的API
[].splice().call(传入转换的对象)
//转换语法
[].arr().call()
```

```js
Array.prototype.arr = function () {

  var star = 0
  var end = this.length  //如果是对象,需要.length属性
  if (arguments === 1 ) {
     star = arguments[0] 
  } else if ( arguments === 2 ) {
    star = arguments[0]
    end = arguments[1]
  } 
  var temp = []
  for (let i = 0; i < this.length; i++) {
    temp.push(this[i])
  }

  return temp //返回一个真数组
}

var obj = {
    0 : 'abc',
    1 : 'wed',
    2 : 'dsf',
    length : 3 //  必须有 .length
}

[].arr.call(obj) // 就可以变成数组了
```



### Array下的一些重要方法

`.push `(值)--->追加数据的,把值追加到数组食物最后, 追加一个(**多个**)元素中,返回值是追加数据之后的数组长度

```js
// 可以添加多项
arr.push('皮皮虾' , '貂蝉')
```

`.pop()`----->删除数组中的最后一个元素,返回值是删除的的那个值

`.shift()`----->删除数组中的第一个元素,返回值也是删除的那个值

`.unshift()`---->在数组中的开头,插入一个(**多个**)新元素,返回值插入后的长度

记忆技巧 : 长的添加 , 短的删除 , `s`  前  `p` 后 

```js
var arr=[10,20,30,40,50];
var result=arr.unshift(100);
console.log(result);
结果=====>  (6) [100, 10, 20, 30, 40, 50]
```

`.forEach(函数)`:遍历数组---相当于for循环

```javascript
var arr = [10, 20, 30, 40];
arr.forEach(function (ele,index) {
  console.log(ele+'======'+index);
});  结果====>
10======0
20======1
30======2
40======3
```

`.find(函数)`  : 作用能够隐式遍历数据 ,相当于 `forEach()` 方法 , 函数中需要传入一个值 , 代表需要遍历的数组中的每一项数据 , 而且需要一个返回值 , 返回符合条件的 数组中的那一项

```js
//ES6的方法
var arr = [{name:'张三',age:18},
          	{name:'李四',age:20}
          ]
var data = arr.find(function (item) {
    return item.age === 18
})
console.log(data) //{name: "张三", age: 18}
```

`.findIndex(函数) `: find 函数符合条件的元素 , 这个方法返回符合条件的**下标** , 用法和`find` 一样 

`.isArray(对象)`:判断这个对象是不是数组

`.concat(数组1,数组2,.....)`:用来拼接数组,组合成一个新数组 , 返回值是把新数组返回

`.every(函数)`:  返回值是布尔类型,函数作为参数使用,函数中有三个参数,第一个参数是元素的值，第二个参数是索引值,第三个参数是原来的数组(没用)       如果这个数组中的每个元素的值都符合条件,最后才返回的是true

**方法测试一个数组内的所有元素是否都能通过某个指定函数的测试。它返回一个布尔值。** 

```js
function isBelowThreshold(currentValue) {
  return currentValue < 40;
}

var array1 = [1, 30, 39, 29, 10, 13];

console.log(array1.every(isBelowThreshold));
// expected output: true
```



可以用来筛选

`.filter(函数)`: 返回数组中每个元素都符合条件的元素,组成一个新的数组**=======>筛选数组**

```js
var arr=[10,20,30,40,50,60,70,80];
var newArr=arr.filter(function (ele) {//ele---每个元素
  return ele>40;
});
console.log(newArr);//    [50, 60, 70, 80]
```

`.indexOf`(要找的元素 , 从某个位置开始的索引):**返回的是第一次出现的索引值 **, 没有则为-1===>查找元素的,并到那会索引

```js
var arr=[10,20,30,40];
var index=arr.indexOf(30);
console.log(index);//结果===> 2
```

`lastIndexOf(要查找的元素)`  : 从数组中的最后面开始查找 , 但**返回的是最后一次的索引** , 没有的数据返回 `-1` 



`.join("字符串")`:返回的是一个字符串=====>**添加元素,返回一个字符串**

> 把数组变成一个字符串

```js
var arr=["小白","小黑","小红","小芳","小绿","小苏"];
var str=arr.join("|");
console.log(str);
结果====>  小白|小黑|小红|小芳|小绿|小苏
```

`.map(函数)`;--->数组中的每个元素都要执行这个函数,把执行后的结果重新的全部的放在一个新的数组中

```javascript
var numbers = [1, 4, 9];
var roots = numbers.map(Math.sqrt);
console.log(roots);
结果===>  (3) [1, 2, 3]
```

`.reverse()`----->**反转数组**

`.sort()`----->排序的,可能不稳定,如果不稳定,请写MDN中的那个固定的代码**========>** **排序**

```js
var arr=[1,40,20,10,100];

//return a-b ====> 升序
// return b-a ====>降序
arr.sort(function (a,b) {
 	return a-b //升序
    return b-a //降序
});

//写法二
//a---arr[j]
//b---arr[j+1]
arr.sort(function (a,b) {
  if(a>b){
    return 1; //返回值大于0 会交换位置
  }else if(a==b){
    return 0;
  }else{
    return -1;
  }
});
console.log(arr);
```

**高级用法**

sort : 还可以用来排序, 字符串,数组中对象的属性等等



`.slice(开始的索引,结束的索引)`把截取的数组的值放在一个新的数组中,但是不包含**结束的索引**对应的元素值

通过索引截取数组,**返回新的数组** **===========>截取数组 ( 有始无终 )**   

> 不传参数, 表示从头截到尾

```js
//可以传一个参数, 可以传两个参数
var arr=[10,20,30,40,50,60,70,80,90,100];
var newArr= arr.slice(3,7);
console.log(newArr);
 结果为====>[40, 50, 60, 70]
```

`.splice(开始的索引,要删除的个数,添加数1 , 添加的数2) `在数组中的任意位置, 进行添加(可以多个), 删除 , 替换元素**============>** **在原数组中添加 , 删除 , 替换**   

```js
var myFish = ['angel', 'clown', 'mandarin', 'sturgeon'];

//添加 
myFish.splice(2, 0, '哈哈哈'); // 把'drum'插到索引为2的位置
 结果===> ["angel", "clown", "哈哈哈", "mandarin", "sturgeon"]
 
//删除 ===上面添加一个元素, 下面删除新加的元素
 myFish.splice(2, 1); // 从索引为2的位置删除一项（也就是'drum'这一项）
 console.log(myFish); // ['angel', 'clown', 'mandarin', 'sturgeon']

//替换  , 先删除在添加
myFish.splice(2, 1 ,'皮皮虾');
console.log(myFish) //(4) ["angel", "clown", "皮皮虾", "sturgeon"]
```



### 补充 : 常用重要方法

`includes ()` : 传一个数组中的元素, 判断数组数组是否包含这个元素 , 返回布尔值 `true`或者`false`和 				      `indexOf()`作用相同

`reduce()` : 对数组中的每一个执行一次, 我传入的函数的操作	, 将结果汇总为返回值返回

```js
//能够接受四个参数
//Accumulator (acc) (累计器)
//Current Value (cur) (当前值)
//Current Index (idx) (当前索引)
//Source Array (src) (源数组)

var arr = [1, 2, 3, 4, 5]
    var sum = arr.reduce(function(prev, curr) {
        return prev + curr
    })
    console.log(sum)//15
```

 **. some ( ) **   方法测试是否至少有一个元素可以通过被提供的函数方法。该方法返回一个Boolean类型的值。 

 ```js
var array = [1, 2, 3, 4, 5];

var even = function(element) {
  // checks whether an element is even
  return element % 2 === 0;
};

console.log(array.some(even));
// expected output: true
 ```





### 清空数组

- 方式一

```js
arr = [];
```

- 方式二

```js
arr.length = 0
```

- 方式三

```js
arr.splice(0,arr.length)
```



## 基本包装类型

- 简单数据类型本身是没有属性和方法
- 复杂数据类型才有属性和方法

### 基本包装类型

> 针对于 `number` `string` `boolean` 都有对应的基本包装类型, 把简单数据类型,包装成复杂数据类型, 此时就有了自己的属性和方法

```js
//当我们给简单数据类型使用属性和方法, 浏览器就给简单数据类型包装成复杂数据类型
//浏览底层做的事情
var num = new Number()
var str = new String()
var flag = new Boolean()
//属性调用完之后,浏览器会恢复成简单数据类型
```



## Number对象下方法

`toString()` 将数字类型转换为字符串类型

`toFixed(保留的位数)`  设数字保留的位数 , 输出的是字符串,

## Boolean对象下的方法

`toString()` 将boolean的结果转换为字符串



## String对象



String是一个对象,字符串可以看成是一个数组,可以通过for循环进行遍历,每个字符都有自己的索引



### 拼接字符串

方式一 ：

```js
 '我是第'+i+' 个'  //===== '+变量+'
```

方式二 ： 在 ECma 6中加入了  反引号``

```js
` 我是第 ${i} 个 `   //而且支持换行
```

   

### 字符串的特性

```js
不可变性:字符串的值是不可改变,但不是是说字符串的值可以通过重新赋值,改变字符串的值
var str="小苏好猥琐";
str="小苏好邪恶了";//重新赋值
此时相当于在堆中重开开辟一个空间存储Str的值,栈中存储的是Str的地址,重新赋值改变了栈中Str地址的指向,但是Str之前地址中的字符串的值并没有改变

var str="hello";
    str[1]="W";
    console.log(str);  //hello


//可遍历
for (let i=0; i < str.length; i++) {
    console.log(str[i])
}
```

### string和String的区别

string 是字符串类型--------->基本类型

String是字符串类型---------->引用类型



### String下的方法(重点)

> 字符串是基本包装类型,字符串调用方法时, 就会被浏览器, 进行包装
>
> var str = new String()
>
> 此时的 str 就变成了一个**类似数组的对象**, 可以通过索引,访问字符串中每一个字母 

.length --------字符串的长度

**.charAt** (索引), 返回值是指定索引位置的字符串(单指的是索引位置的字符串),超出索引,结果是空字符串

**就是查找字符串并通过索引返回查找的字符串**

```javascript
var str="whatareyounoshalei";
var result=str.charAt(3);
console.log(result);//结果返回一个---> t
```

`.concat(字符串1,字符串2,.....)`: 字符串的拼接,**返回的是拼接后的字符串======>拼接字符串**

```javascript
 var str="小苏";
 console.log(str.concat("喜欢","凤姐","这是","真的"));
 //结果为--->小苏喜欢凤姐这是真的
```



**.indexOf(要找的字符串 , 从某个位置开始的索引)  返回的是要找的字符串的索引值, 没有找到则返回-1**

```javascript
var str="小苏真的好猥好琐啊";
var index=str.indexOf("好",5);
console.log(index);// 结果为 ---> 6
```

`.lastIndexOf(要找的字符串)`: 默认从后往前找 ,但是索引值依旧从前往后, 没找到则返回-1

**从后面查找,返回查找的索引**

```javascript
var str="helo amen";
var index=str.lastIndexOf("Y");
console.log(index);//结果为--->-1
```



`.replace("原来的字符串", "新的字符串") ` :  把替换后的字符串返回========>  **用来替换字符串的**

> 通过正则可以进行全局替换

> 只能替换第一个
>
> 可以使用 正则 str.replace( /需要替换的字符串/g , '替换的字符串' )

```js
var str="小苏好帅哦,真的好勇敢哦";
str=str.replace("帅","猥琐");
console.log(str);
结果----> 小苏好猥琐哦,真的好勇敢哦

```



`.slice(开始的索引 , 结束的索引)` : 从开始的索引位置开始提取, 到结束索引的位置 ,但不包括结束的索引,并返回提取后的字符串===================**截取字符串(有始无终)**

```js
var str = "如果有一天我邪恶了,请记住,我曾纯洁过";
//从索引5的位置开始提取,到索引为10的前一个结束,没有10，并返回这个提取后的字符串
str = str.slice(5, 10);
console.log(str);
结果为====> 我邪恶了,

```

`.substring(开始位置的索引 , 结束位置的索引)` : 返回截取后的字符串,不包括结束索引的字符串 **===截取字符串(有始无终)**

```js
var str="哈哈,小苏真的是好帅哦";
str=str.substring(5,9);
console.log(str);  
结果===> 真的是好


```

`.substr(开始位置 , 个数)`:返回的是截取后的新字符串 **======截取字符串** 

```js
var str="哈哈,小苏真的是好帅哦";
str=str.substr(5,5);
console.log(str);
结果===> 真的是好帅

```



```js
.toLocaleLowerCase();  转小写
.toLowerCase()      转小写
.toLocaleUpperCase()  转大写
.toUpperCase();    转大写
```



`.split( "要干掉的字符串" , 切割后留下的个数)` : **分割字符串的,返回成一个数组**

> 把字符串变成数组
>
> 数组的join() 把数组变成一个字符串

```js
var str="乔峰|慕容|凤姐|梅超风|小苏|大蛇丸";
var arr=str.split("|");
console.log(arr);
结果:["乔峰", "慕容", "凤姐", "梅超风", "小苏", "大蛇丸"]

```

`.trim()`;   干掉字符串两端的空格, 返回去掉空格之后的字符串

`.startsWith ('  查找的字符串 ')`  ====> 是不是以某个字符串开头

> 值: true 或  false



`.endswith (  ' 字符串 ' ) ` =======> 是不是什么结束

> 值: true  false



### 字符串案例

//案例2:找到这个字符串中所有的 o 出现的位置

```js
var str2 = "hello wod odd ott fbo nhyo";
var index = 0;//开始的位置
var key = "o";//要找的字符串
while ((index = str2.indexOf(key, index)) != -1) {//如果是-1情况,说明找完了
  console.log(index);
  index + = key.length;
}
	var index=str2.indexOf("o",0);
	console.log(index);

```

案例1

```javascript
//案例1:
var str = "我爱最帅的杨哥,太帅了";
//console.log("杨哥");
var key = "杨哥";
//先获取要截取的字符串的索引的位置
var index = str.indexOf(key);
//从指定的位置开始截取,截取两个即可
str = str.substr(index, 2);
console.log(str);
```

//案例3:找到这个字符串中每个字符串出现了多少次

```javascript
var str3 = "whatOareYyouYnoYshaHleiHoHmyHgod";
//第一步:把所有的字母全部变成小写
str3 = str3.toLocaleLowerCase();
//第二步:创建一个空对象,目的:把字母作为键,次数作为值
var obj = {};
//第三步,遍历字符串,获取每个字母
for (var i = 0; i < str3.length; i++) {
  //判断obj这个对象中有没有这个字母(字母---键)
  var key = str3[i];//每个字母
  if (obj[key]) {//判断obj中有没有这个键
    //对象中有这个字母了
    obj[key]++;
  } else {
    //对象中没有这个字母,那就把字母加到对象中,并且给这个字母一个出现的次数,默认1次
    obj[key] = 1;
  }
}
//遍历对象,显示每个字母的次数
    for(var key in obj){
      console.log(key+"这个字母出现了"+obj[key]+"次");
    }
```





# JS基础补充

## == 和 ===

1. NaN 不等于任何值, NaN 也不等于 NaN



2. null 不等于任何值,  除了 null 和 undefined  ,  null == null  ,  null == undefined



3. undefined 不等于 任何值, 除了 null 和 undefined



4. 如果有布尔值 或者 数字, 都转数字比较 , true 转数字是 1 . false  转数字会变 0 



5. 如果有字符串, 两边都变字符串

   - 字符串和对象比较, 会转字符串比较, 对象自动掉`toString `

   - `{}.toString() == [object Object] // true`

      

6. 复杂类型比地址



## 基础书籍推荐

javascript 高级程序设计

javascript 权威指南

你不知道的 javascript (上中下)

javascript 精粹

