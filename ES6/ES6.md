# EcmaScript 6

## 介绍

> ECMAScript 6.0（以下简称 ES6）是 JavaScript 语言的下一代标准，已经在 2015 年 6 月正式发布了。它的目标，是使得 JavaScript 语言可以用来编写复杂的大型应用程序，成为企业级开发语言。

我们从node开始，会大量用到ES6中的一些新语法，因此在学习node之前需要先学习一下es6中提供的新语法

## ECMAScript与Javascript的关系

ECMAScript，简称ES，是由Ecma国际（欧洲计算机制造商协会,英文名称是European Computer Manufacturers Association）按照标准制定的一种脚本语言规范。

JavaScript是按ECMAScript规范实现的一种脚本语言，JavaScript除了实现了ECMAScript规范，还提供了BOM和DOM的操作。

## ECMAScript版本历史

+ ES1.0, 1997年06月发布
+ ES2.0, 1997年06月发布
+ ES3.0, 1999年12月发布

+ ES4.0,  由于关于语言的复杂性出现了分歧。放弃发布
+ ES5.0, 2009年12月发布， 增加了严格模式，增加了少量语法，为ES6铺路
+ ES6.0, 2015年6月发布，增加了大量的新概念和语法特性
  + **第六版的名字， 可以叫做ECMAScript6.0(ES), 也可以叫做ECMAScript 2015（ES2015）**
  + ECMA组织决定以后每年6月份都会发布一版新的语法标准，比如ES7(ECMAScript 2016) 
  + **通过我们说的ES6泛指ES5之后的下一代标准，涵盖了ES6, ES7, ES8....**  




## ES5 数组新方法

### forEach()

能够遍历数组, 功能等同于for循环, 没有返回值, 只能操作数组中的每一项

**语法**

`forEach(callback(item, i, arr){})` 

接收一个回调函数, 参数除了item, 都是可选

- item : 数组中的每一项
- i : 每一项的下标
- arr : 数组本身



### map()

能够遍历数组中每一项, 并且能够返回一个新数组, 

把回调函数处理过的每一项自动加入新数组中, 能够用于收集函数处理过后的数据

**语法**

`map(callback(item, i, arr) {})`

**参数都是可选的, 参数同forEach()一样**



### filter()

筛选 , 会返回一个新数组, 数组中存放的是满足条件的元素

**语法**

`filter(callback(item, i, arr){})`

**参数同forEach一样**



### some()

判断数组中书否有元素满足条件, 只要有一个就算, **返回布尔类型** => 有一个就算

**语法**

`some(callback(item, i, arr) {})`

```js
let arr = [11, 22, 33, 44]

let flag= arr.some(v => v > 50)
console.log(flag) //false
```



### every()

判断数组中每一个元素都满足条件, 全部都满足才可, **返回布尔类型** => 全部才算

`every(callback(item, i, arr) {})`

```js
let arr = [11, 22, 33, 44]
    
let flag = arr.every(v => v > 30)
console.log(flag) //false
```



### sort()

操作原数组, 没有返回值

```js
arr.sort((a, b) => a-b) //升序
arr.sort((a, b) => b-a) //降序
```





## ES6 新增数组方法

### find()

查找数组中**第一个符合的元素,  只找第一个** ,**filter()是查找数组所有符合条件的元素, 把符合条件的第一个元素返回**

`find(callback(item, i, arr){})`

### findIndex()

查找数组中第一个符合添加条件的索引值



**区别**

find()找符合条件的第一个元素

findIndex()找符合条件的第一个元素的索引值 



## 综合大练习

给定一个数组

```js
let list = [
  // wu: 武力    zhi:智力
  { id: 1, name: '张飞', wu: 97, zhi: 10 },
  { id: 2, name: '诸葛亮', wu: 55, zhi: 99 },
  { id: 3, name: '赵云', wu: 97, zhi: 66 },
  { id: 4, name: '周瑜', wu: 80, zhi: 98 },
  { id: 5, name: '吕布', wu: 100, zhi: 8 },
  { id: 6, name: '司马懿', wu: 30, zhi: 98 }
]
```

+ 得到一个新数组，只保留英雄的名字， `['张飞', '诸葛亮', '赵云', '周瑜', '吕布', '司马懿']`
+ 得到一个新数组，新数组中只保留武力值超过90的英雄
+ 删除数组中名字为周瑜的英雄    list.splice(从哪删，删几个)
+ 判断数组中所有英雄的武力是否都超过60， 最终打印结果： `全是猛将`  `还有弱鸡`     使用两种方式实现
+ 找到数组中id为2的英雄，求他的武力+智力的综合

```js
  //1 - 得到一个新数组，只保留英雄的名字， ['张飞', '诸葛亮', '赵云', '周瑜', '吕布', '司马懿']
    let newArr = list.map(v => v.name)
    console.log(newArr)

  //2-  得到一个新数组，新数组中只保留武力值超过90的英雄
  //筛选
    let arr1 = list.filter(v => v.wu > 90)
    console.log(arr1)

    let temp = list.filter( (v) => {
      return v.wu > 90
    })

    temp = temp.map( v => v.wu)
    console.log(temp)

    //3 - 删除数组中名字为周瑜的英雄    list.splice(从哪删，删几个)
    list.splice(list.findIndex(v => v.name === '周瑜'), 1)  
    console.log(list)


    //4 - 判断数组中所有英雄的武力是否都超过60， 最终打印结果： 全是猛将  还有弱鸡     使用两种方式实现
    if (list.every(v => v.wu > 60)) {
      console.log('全是猛将')
    } else {
      console.log('全是弱鸡')
    }

    if (list.some(v => v.wu < 60)) {
      console.log('全是弱鸡')
    } else {
      console.log('全是猛将')
    }

  // 5- 找到数组中id为2的英雄，求他的武力+智力的综合
    var obj = list.find(v => v.id === 2)
    console.log(obj.wu + obj.zhi)
```







## ES6 定义变量

### var

**var的特点**

作用域: 全局作用域, 函数作用域

预解析: 变量和函数声明会提升 ----------------------> 很恶心

**var的缺点**

全局变量污染, 预解析



### let

**let的特点**

变量不能提升 -> **不存在预解析,** **必须先定义,后使用**

变量不能重名 -> **重名不存在覆盖问题, 定义过后, 不能再次定义**

**块级作用域**

**块 :  { }内就形成了一个块级作用域**



### const

**定义常量, 在程序运行过程中,不能再修改, 所以在定义的时候必须赋值, 否则就无法在赋值** 

var 和 let 是变量, 在程序运行过程中能够被修改

**特点**

变量不能提升 -> **不存在预解析,** **必须先定义,后使用**

变量不能重名 -> **重名不存在覆盖问题, 定义过后, 不能再次定义**

块级作用域     ->  **块 :  { }内就形成了一个块级作用域**



### 三者使用场景

定义变量 : let

定义常量 : const

不推荐使用--------------------> var  





## ES6 解构赋值

解构赋值: 分解结构, 进行赋值, 解构复杂数据类型的数据

### 解构对象

**解构时,必须同名**

```js
let obj = {
    name: '涛涛',
    age: 18,
    sex: '男'
}
//let name = obj.name
//let age = obj.age
	
//解构语法
let {usernanme, age} = obj
console.log(name, age) //涛涛, 18
console.log(username, age) //undefinded 18
```



**可以起别名**

```js
let {username:name, age}
console.log(username, age) //涛涛 18
```



**没有的属性,设置默认值**

sex = '女'  只是一个默认值, 在解构失败时, 才有用

```js
//sex = '女' 只是一个默认值, 在解构失败时, 才有用
let {name, age, sex='女'}
console.log(name, age, sex) //涛涛 18 男
```



### 解构数组

使用`let [] = array`

```js
let arr = [11, 22, 33]
let [a, b, c] = arr
console.log(a, b, c) // 11 22 33
```



**设置默认值**

解构失败时, 使用默认值

```js
let arr = [11, 22, 33]
let [a, b, c, d=55] = arr
console.log(a, b, c, d) // 11 22 33 55
```



**解构部分元素**

使用`,` 占位

```js
let arr1 = [11, 22, 33, 44] 
let [a, , , b] = arr1
console.log(a, b) //11 44
```



### 函数参数的解构

在实参给形参传值的时候, 发生了解构

`let  {url, type, data} = { url: 'o1.php',    type: 'json',  data: 111}`

```js
//function ajax(obj) {
 //   let {url, type, data} = obj
 //   console.log(url, type, data)
//}

function ajax({url, type, data}) {
    let {url, type, data} = obj
    console.log(url, type, data)
}
ajax({
    url: 'o1.php',
    type: 'json',
    data: 111
})
```



## ES6 模板字符串 template String

原始字符串 : `''` 或者 `""`

模板字符串:  反引号

**特点**

1. 支持换行
2. 可以插值 `${}`



## ES6新增字符串方法

### startsWith()

判断字符串是否以已指定的字符串开头

### endsWith()

判断字符串是否以已指定的字符串结尾

### includes()

判断字符串是否包含指定的字符串

```js
let str = 'aabbccddeeff'
console.log(str.startsWith('aa')) //true
console.log(str.startsWith('ff')) //false

console.log(str.endsWith('aa')) //false
console.log(str.endsWith('ff')) //true

console.log(str.includes('aa')) //true
console.log(str.includes('ff')) //true
```



### 字符串补全`padStart()`和 `padEnd()`

- **padStart**：返回新的字符串，表示用参数字符串从头部（左侧）补全原字符串。
- **padEnd**：返回新的字符串，表示用参数字符串从尾部（右侧）补全原字符串。

**语法**

```js
padStart(maxLength, fillString)
padEnd(maxLength, fillString)
```

**参数**

以上两个方法接受两个参数，第一个参数是指定生成的字符串的最小长度，第二个参数是用来补全的字符串。如果没有指定第二个参数，默认用空格填充。

- 如果指定的长度小于或者等于原字符串的长度，则返回原字符串:
- 如果原字符串加上补全字符串长度大于指定长度，则截去超出位数的补全字符串:

```js
console.log("h".padStart(5,"o"));  // "ooooh"
console.log("h".padEnd(5,"o"));    // "hoooo"
console.log("h".padStart(5));      // "    h"
```







## ES6 对象简写

变量名和属性名相同可以省略一个

对象中的方法可以省略 `: function`

```js
let name = '海亮'
let age = 18

let obj = {
    name,
    age,
    sex: '女',
    sayHi(){
        console.log('哈哈')
    }
} 
```



## 对象(数组) 展开

### 展开运算符 `...`

一般用于可遍历的数据

### 展开数组

```js
let arr1 = [1, 2, 3]
let arr2 = ['a', 'b', 'c']
let arr3 = [1, ...arr2, 2, ...arr2, 3]

```

### 展开对象

```js
    const obj1 = {
      name: '张三',
      age: 18
    }  
    const obj2 = {
      money: '一个亿',
      sayHi () {
        console.log('我会撩妹')
      }
    }
    const obj3 = {
      ...obj1,
      ...obj2,
    }    
    console.log(obj3.sayHi())
```





## 箭头函数

### 语法

**箭头函数就是函数表达式**

```js
let fn1 = (n1, n2) => {
    console.log(n1 +n2)
}
fn1(10, 20)
```



### 箭头函数的简写

**箭头函数只有一个参数, 可以省略小括号**

```js
var fn = parm1 => {
    //函数体
}
```

**函数体只有一行, 可省略花括号 `{} `和 `return`**

```js
let fn = parm1 => n1 + n2

//等价于
let fn = (parm1) => {
    return n1 + n2
}
```



### 箭头函数中this指向问题

箭头函数中没有自己的this, 在箭头函数中使用外部函数的this

箭头函数的this不取决于函数的调用模式, 只在定义时所在的外部函数的this

箭头函数没有this, 所以无法作为构造函数





## 函数的默认参数

在函数的形参中传入默认值

```js
function fn(a = 0, b = 0) {
    console.log(a, b)
}

fn() //0
fn(1) //1
fn(1,2) // 3
fn(1,2,3) // 3
```



## Set数据类型

>  let arr = [1, 2, 3, 4, 2, 3, 5 ]  如何去重？    

```js
// 答案：
arr = [...new Set(arr)];
```

>  *Set* 对象允许你存储任何类型的唯一值,无论是原始值或者是对象引用 ,　ES6提供了新的数据类型Set**，**Set对象不是数组， 可以用来保存对象或者基本类型， 所有保存的值都是唯一的 

```js
let set = new Set();
set.add(1)  // {1}
set.add(2)  // {1, 2}
set.add(1)  // {1, 2}
//或者 
let set = new Set([1,2,3,4,4,4,4,4]);
console.log(set) // Set(4)  {1, 2, 3, 4} -->对象
console.log([...set]); //输出：[ 1, 2, 3, 4 ]  --> 数组
```



**数组去重**

```js
    let list = [1, 3, 4, 5, 2, 3, 3]
    
    //... 展开符
    list = [...new Set(list)]
    console.log(list)
```



# Es6 中Promise

为了解决异步操作, 造成的回调地狱的问题

## promise本质

1. 它出现的本质就是解决回调地狱的问题, 实现串联式代码, 一定程度上并不能减少代码量

2. promise是一个构造函数, new之后能够得到一个promise实例

3. **promise的原型对象`prototype`上有`then`方法, 所以promise的实例都有`then` 方法**
4. Promise表示一个异步操作, 我们new出来的实例, 这个实例就表示一个具体的异步操作
5. 既然Promise创建的实例是一个异步操作, 那么这个异步操作的结果只有两种状态
   - 状态1: 异步执行失败了, 在内部调用resolve 把结果返回给调用者
   - 状态2: 异步执行成功了, 在内部调用reject 把结果返回给调用者
   - 由于Promise的实例, 是一个异步操作, 所以内部拿到操作的结果后, 无法使用`return` 把操作的结果返回给调用者, 这个时候只能使用回调函数, 把成功 或者 失败 的结果, 返回给调用者
6. 我们可以在 new 出来的Promise 实例上调用 .then 方法, 预先 为这个Promise异步操作, 指定成功的 ( **resolve**  ) 的回调 和 失败的回调 **reject**

reject() 和 resolve()

本质上都是promise身上的两个函数

reject:失败之后的回调

resolve: 成功之后的回调



## 形式上的和具体的Promise 异步操作

形式上的Promise 异步操作

```js
//这只是new 出来一个异步操作, 但是我们不知道具体是什么异步操作
let promise = new Promise()
```

具体的Promise异步操作

```js
//在function内部写具体的异步操作, 我们就知道这个promise实例具体是什么异步操作
let promise = new Promise(function () {
    fs.readFile()
})
```

**每当new 一个Promise 实例的时候, 就会立即调用unction内部的异步代码**

**也就是说new除了能够得到一个 Promise实例, 还会立即调用我们传递给 构造函数Promise 那个函数**



## Promise执行过程分析

1. 程序走到`getFile`  内存中有了这么一个方法, 但是没有调用
2. 调用`getFile` 进入函数内部执行函数体
3. 得到一个`Promise` 实例, 并直接把 实例返回出去
4. 定义变量接收`Promise` 实例, 调用`.then` 方法
5. 执行读文件异步操作, 此时已经有了`resolve` 和 `reject` 函数

```js

const fs = require('fs')
const path = require('path')

//封装一个 promsie读文件的异步操作
//执行过程 
// 1-1定义一个function
function getFile(fpath) {
  // 1-3 new Promise, 得到了一个实例
  // resolove和 reject 是形参, 实参从 promise实例的.then上传实参
  let promise = new Promise((resolve, reject)=>{
    //1-6 当执行到异步操作的时候, 已经有了resolve 和 reject这两个function
    fs.readFile(path.join(__dirname, fpath), 'utf8', (err, data) => {
      if (err) return reject(err)
      resolve(data)
    })
  })

  // 1-4  读文件的操作时异步, 就直接把Promise实例 return出去了
  return promise  //把promise实例返回出去
} 

// 1-2 执行函数
let pro = getFile('./files/2.txt')
// 1-5 执行实例的.then 方法
pro.then((data)=>{
  //成功的回调
  console.log(data)
}, (err)=>{
  //失败的回调
  console.log(err)
})
```



**上述代码优化**

```js
//代码优化
function getFile(fpath) {
  return new Promise((resolve, reject) => {
    //1-6 当执行到异步操作的时候, 已经有了resolve 和 reject这两个function
    fs.readFile(path.join(__dirname, fpath), 'utf8', (err, data) => {
      if (err) return reject(err)
      resolve(data)
    })
  })
}

// 1-2 执行函数
getFile('./files/2.txt')
  // 1-5 执行实例的.then 方法
  .then((data) => {
    //成功的回调
    console.log(data)
  }, (err) => {
    //失败的回调
    console.log(err)
  })
```



## Promise解决回调地狱

**promise实例的.then方法, 可以只传成功(resolve)的回调, 省略失败(reject)的回调**

**在上一个 `.then` 中返回一个新的 `promise` 实例, 可以继续下一个`.then` 处理异步操作成功的回调**

```js
const fs = require('fs')

//封装一个promise方法
function getFile(fpath) {
  return new Promise((resolve, reject)=>{
    fs.readFile(fpath, 'utf8', (err, data) => {
      if (err) return reject(err)

      resolve(data)
    })
  })
}

getFile('./files/1.txt')
  .then(data=>{
    console.log(data)
    # 在每一次成功的回调中, 都return 一个promise实例, 就可以链式的.then下去
    return getFile('./files/2.txt')
  })
  .then(data => {
    console.log(data)
    return getFile('./files/3.txt')
  })
  .then(data => {
    console.log(data)
  })
```

## Promise捕获异常的方式

### 应用需求一

当我们前面的Promise执行失败了, 也不要影响后续的Promise实例的`.then` 的执行

**解决方式**

给每一个`.then` 指定失败的回调

```js
getFile('./files/11.txt')
  .then(data=>{
    console.log(data)
    # 在每一次成功的回调中, 都return 一个promise实例, 就可以链式的.then下去
    return getFile('./files/2.txt')
  }, err => {
      console.log('这是失败的结果'+err.message)
      return getFile('./files/2.txt')  # 在失败的回调中, 继续return一个新的Promise实例
  })
  .then(data => {
    console.log(data)
    return getFile('./files/3.txt')
  })
  .then(data => {
    console.log(data)
  })
```

### 应用需求二

当前面的Promise执行失败, 后面的promsie就不要再继续执行了, 后面的Promise执行依赖于前面的promsie的执行, 一旦前面的报错, 后面的就不在执行

**注意: 如果不加失败的回调, 程序是会终止, 但是不会捕获**

**解决方式**

catch方法的作用: 	

当前面任何一个`.then` 执行失败了 , 会立即终止后续所有Promise的执行, 立即进入 `.catch` 中 进行错误的捕获和处理, catch处理过的失败, 不是报错, 是捕获抛出错误

使用方法: 在所有`.then` 后面 `.catch`

```js
getFile('./files/1.txt')
  .then(data=>{
    console.log(data)
    return getFile('./files/22.txt')
  })
  .then(data => {
    console.log(data)
    return getFile('./files/3.txt')
  })
  .then(data => {
    console.log(data)
  })
  # 在所有.then的后面 .catch进行错误的捕获和处理
  .catch(err => {
    console.log('这是catch的处理'+ err.mssage)
  })

```

**和不加失败的回调(reject) 的区别**

1. `.catch`处理的异常, **程序不会报错**, 捕获异常并处理异常
2. 不加失败的回调, 一旦出错, 也会终止所有Promsie的执行, **但是程序会报错**





## `.all` 和 `.race` 方法拓展了解

promise.all([p1, p2, p3, ....], () => {})

- params: 数组, 与promise实例组成

Promise.all() 必须所有数组里面所有的promise执行完毕后, 才成功, 虽然数组中的所有promise都是异步, 但是必须等待所有都成功, all() 才执行完毕

> 全部成功才执行完毕



promise.race([p1, p2, p3, ....], () => {})

Promise.race 只要数组中的promise只要成功一个, 整个race就执行了

> 一个成功就执行完毕

## jQuery中$.ajax使用Promise方式

就是将success抽离出去, 用`.then` 代替

```js
    $(function () {
      $('button').click(function () {
        $.ajax({
          url: './data.json',
          type: 'get',
        })
        .then(data => {
          console.log(data)
        })
      })
    })
```





# node的导出导出和 ES6的导入导出的关系

node中的 require 导入 和 exports 、 module.exports 导出

ES6 中的 import导入 和 export , export default 导出

## node中的导入导出

 `Node`里面的模块系统遵循的是`CommonJS`规范。 

 `CommonJS`定义的模块分为: 模块标识(`module`)、模块定义(`exports`) 、模块引用(`require`) 

### exports 和 module.exports

 在一个node执行一个文件时，会给这个文件内生成一个 `exports`和`module`对象 , exports 是module的一个属性

在文件的结尾都会添加这么一行

```js
exports = module.exports = {};
```

也就是说: 为了我们操作导出的这个对象, 让exports引用了`module.exports`的地址

![](image/exports和module.exports.png)

二者都指向内存中同一个对象, 无论是`exports` 和 `module.exports` 谁发生改变, 最终导出的还是module.exports

 所以呢，为了避免糊涂，尽量都用 `module.exports` 导出，然后用`require`导入。 



## ES6中导入和导出

### import导入

导入规则和node中的require 一样

默认的导入

1. `import './a.js'`  使用于模块没有导出, 只是加载模块的代码

精确的导入

2. `import { 变量名 } from './a.js'`  适用于模块有导出

### export 和 export default

这两个都能够导出常量, 函数, 文件, 模块等

1. 在一个文件或者模块中, export 和 import 可以有多个, export default 只能有一个
2. `export`   导出的成员, 在导入时, 必须严格按照导出的名称, 在 `{  }` 中按需接收
3. `  export default`向外暴露的成员, 可以`import`接收时可以定义任意变量接收 

```js
'use strict'
//导出变量
export const a = '100';  

 //导出方法
export const dogSay = function(){ 
    console.log('wang wang');
}

 //导出方法第二种
function catSay(){
   console.log('miao miao'); 
}
export { catSay };

//export default导出
const m = 100;
export default m; 
//export defult const m = 100;// 这里不能写这种格式。
```





# 节流和防抖

### 防抖 (输入框)

利用定时器, 连续触发函数时, 每一次触发都会把上一次的定时器清掉, 触发触发最后一次定时器的函数



### 节流 (按钮多次点击)

利用了节流阀的功能, 当我们触发函数时, 这一次的函数没有完成, 就不会触发下一次的函数





# var a= b = 3 和 var a =3, b=3

 var a = b = 3; 实际是以下声明的简写 

> 即连续赋值是**从右至左永远只取等号右边的表达式结果赋值到等号左侧** 

```js
b = 3; # 隐式全局
var a = b;
```

var a = 3, b = 3 实际等于

```js
var a = 3;
var b = 3
```



# 数组去重

## ES6 Set对象

```js
// 数组去重
function unique(arr) {
  return Array.from(new Set(arr))
}

console.log(unique([1, 2, 3, 3, 2, 1]))
```

lodash库去重

`_.uniq(array)` :  创建一个去重后的`array`数组副本。使用了 [`SameValueZero`](http://ecma-international.org/ecma-262/6.0/#sec-samevaluezero) 做等值比较。只有第一次出现的元素才会被保留。 

```js
_.uniq([2, 1, 2]);
// => [2, 1]
```



`filter` 去重

```js
function unique(arr) {
  return arr.filter(function(item, index, arr) {
    //当前元素，在原始数组中的第一个索引==当前索引值，否则返回当前元素
    return arr.indexOf(item, 0) === index
  })
}
var arr = [1, 1, 0, 0, 'a', 'a', {}, {}]
console.log(unique(arr))
```





# promise原理

```js
function Promise(executor) {
    var self = this
    self.status = 'pending' // Promise当前的状态
    self.data = undefined  // Promise的值
    self.onResolvedCallback = [] // Promise resolve时的回调函数集

    function resolve(value) {
        if (self.status === 'pending') {
            self.status = 'resolved'
            self.data = value
            for(var i = 0; i < self.onResolvedCallback.length; i++) {
                self.onResolvedCallback[i](value)
            }
        }
    }

    // 执行new Promise()时，传入的function。等于说每次新建new Promise实例，总会执行传入的函数
    executor(resolve, reject)
}

Promise.prototype.then = function(onResolved, onRejected) {
    var self = this // self = this = primise1
    // 重要，根据Promise A+标准，then方法总是返回一个新的promise2 = new Promise()，这点非常重要
    var promise2

    // 状态处理，主流程大部分走pending
    if (self.status === 'pending') {
      return promise2 = new Promise(function(resolve, reject) {
        // 包装的resolvedCallback。resolvedCallback调用时间：promise1调用resolve
        var resolvedCallback = function(value) {
            var x = onResolved(self.data)
            resolve(x) // 重要。这是promise2的resolve，触发链式调用
        }

        // 如果当前的Promise还处于pending状态，我们并不能确定调用onResolved还是onRejected，只能等到Promise的状态确定后，才能确实如何处理.
        // 重要：第一个then()回调，放进promise1.callbacks，第二个then()，放进promise2.callback。
        self.onResolvedCallback.push(resolvedCallback)
      })
    }
  }

module.exports = Promise
```



# 移动端 1px 变粗



# 伪数组转真数组


# 装饰器

装饰器就是一个函数

在*类*或者*类属性方法*前面写上 `@函数名` 就相当于调用这个函数

它可以给类 或者 属性方法 加上一些其他的东西(属性或方法或数据之类), 就和react中高阶组件一样, 高阶组件是一个函数, 可以通过装饰器写法使用
