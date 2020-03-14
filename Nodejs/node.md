# node.js 第一天

## 历史

node的作者 : `ryan dahl` 	node之父

## 为什么要学习nodejs

为什么要学习服务端的开发？

1. 通过学习Node.js开发理解**服务器开发**、**Web请求和响应过程**、 **了解服务器端如何与客户端配合**
2. 作为前端开发工程师（FE）需要具备一定的服务端开发能力
3. 全栈工程师的必经之路

服务器端开发语言有很多，为什么要选择nodejs

1. 降低编程语言切换的成本(nodejs实质上用的还是javascript)
2. NodeJS是前端项目的基础设施，前端项目中用到的大量工具 (大前端)
3. nodejs在处理高并发上有得天独厚的优势
4. **对于前端工程师，面试时对于nodejs有一定的要求**

- [web前端10-20k](https://www.zhipin.com/job_detail/d35a590c832162ed1XB42Ny-Flo~.html?ka=search_list_7)
- [web前端15-30k](https://www.zhipin.com/job_detail/fa90a3f6c28712da1XF-2dm5FVc~.html?ka=search_list_15)



## 什么是nodejs

nodejs是一个基于chrome V8引擎的JavaScript的运行环境, 因为node中也有一个chrome V8引擎的JS解析器

浏览器也是一个JavaScript的运行环境



## node和浏览器的区别

**浏览器是做前端开发**

- 能够操作DOM和BOM

**node做服务端开发**

- 不能操作BOM和DOM

- 监听请求, 处理响应
- 操作数据库



## node可以干什么

### 服务端开发

### 命令行工具

比如npm,webpack,gulp,less,sass等 vue-cli

### 开发桌面应用程序

借助 node-webkit、electron 等框架实现



## 安装node环境

### 下载地址

http://nodejs.org官网就可已下载

查看当前node的版本  在命令行输入`node  -v`   或者`node --version`

对于安装过的，直接安装最新版会直接覆盖老版本

### 环境变量

`在cmd中  cls可以清屏`

在Git中`clear`可以清屏

## nodejs

node是模块化的, node中有很多功能, 划分成各个模块

### EcmaScript

- 没有BOM和DOM

### 核心模块

- node为js提供了很多服务器级别的api ,这些api 绝大多数都被包装在到了一个具名的核心模块中，例如文件操作模块`fs`模块，http服务构建模块`http`模块，`path`路径操作模块，`os`操作系统信息模块........

- 只要提到这个模块是核心模块，就要想到

  ```js
  var fs = require('fs')
  ```

在node.js官网的docs中看提供的 `API`

**`fs`模块 常见 API**

读取目录 fs . readdir （）

 创建目录 fs . mkdir (  )

删除文件 fs . unlink （）



**`http`网络服务构建模块**



**os核心模块   操作操作系统的**

os . cpus()   获取当前机器的CPU 信息 

os . totalmem ( )  获取当前机器的内存



**path 模块  操作路径的**

path . extname()   输出扩展名



### 第三方模块

凡是第三方模块都必须通过`npm` 来下载

使用的时候通过require( ' 包名' )的方式进行加载才可以使用

> 不存在任何一个第三方模块和核心模块的名字一致

### 用户自定义模块



## global全局模块

**在node中除了global不需要引入其他模块都需要require引入,global中的属性和方法, 在任何地方都可以使用**

### global中的属性和方法

setInterval()

console

export

**`__dirname`   和  `__filename`**

在每一个模块中,除了`require` ,`exports` 等模块相关的API之外,还有两个特殊的成员

- `__dirname`  : 可以**动态**来获取当前文件模块所属**目录**的绝对路径===> 目录(不包含文件名)
- `__filename` : 可以**动态**来获取当前文件的绝对路径=============>路径(包含文件名)

## node中的作用域

在node中没有全局作用域，只有模块作用域

模块作用域就是文件作用域，超出这个文件的都没有用，在a文件中加载b文件，在b中，也无法使用a中的变量和方法;  b不会影响到a ，a也不会影响到b

外部访问不到内部，内部也访问不到外部---》就是模块作用域----->只能在当前文件使用



模块与模块之间`默认`是封闭的，不能访问之间的成员方法或变量，只能加载里面的代码

好处：可以完全避免变量命名冲突污染问题，但是模块之间需要通信，每个模块都提供了一个`exports`接口对象，可以把需要通信的方法挂载到接口对象`exports`里，谁`require`就能得到接口对象，就能会获取到接口对象中的成员方法





## require （）方法

### require加载规则

- 优先从缓存中加载
- 在main.js中加载 a.js 时加载过 b.js  在加载b.js时,就不会重复加载 b.js 
- 但是 main.js 加载b.js 会拿到b.js 的接口对象 不会重复加载
- 避免重复加载.提高加载效率

![](images\require加载规则.png)

### require模块标识符

- 如果是非路径形式的模块标识
  - 会被当成核心模块或者第三方模块
- 路径形式的模块
  - `./  ` 和` ../ `相对路径 , 文件的后后缀名可以省略
  - `/xxx `  代表盘符的,  磁盘根目录的绝对路径 , 几乎不用

### 加载模块(require)

require （）是个方法，它的作用是用来`加载模块`，在Node中，模块有三种，核心模块，用户自定义模块，第三方模块 （只能加载另一个模块的代码，不能访问另一个模块里的成员方法）

用户自己编写的文件模块，相对路径必须加 `./` , `./`省略就会报错

在node中只能执行一个文件，为了能够执行多个文件，可以在一个文件中加载其他文件 

```js
在a中 加载 b文件  在执行a文件中，只要碰到require就会执行require中的代码

require(./b.js)  //=== 后缀名可以省略（.js）
```

加载文件的执行顺序

![](images\require.png)







## fs 文件操作模块

###异步API

所有的文件操作`API`都是异步的

### fs.readFile()读取文件 

在浏览器中的js中，没有文件操作能力，但是在node中的JavaScript有文件操作能力

在node中想要操作文件，需要引入fs这个核心模块，fs这个模块提供了所有文件操作的API

**语法**

`fs.readFile(path[, options], callback)`

**当读取失败(文件不存在时)**

- data就为`undefined`

- error就是错误对象

**当读取成功时:** 

- data就是一个Buffer(二进制)对象, 表现形式为十六进制
- data.toString()转成字符串
- 设置`fs.readFile('01.js', 'utf8', callback)`, 第二个参数, 设置编码格式

 总之 ： **成功 ：error就是 null   data就是读取的数据**
 			  **失败：error就是错误对象  data就是null**

**注意点**

- **path参数的使用相对路径, 是相对运行node代码的路径**
- 使用fs,进行读取操作都会结合`path.join(__dirname, './data.txt')`
- `app.use('/public/', express.static(path.join(__dirname,'./public/')))`

```js
var fs = require('fs');  //================加载模块
fs.readFile ('文件'，[参数2] , callback);

readFile（）有两个参数：
第一个参数：文件路径

第二个参数 : 'utf8' 把获取的数据转换成utf8我们能认识的编码格式

第三个param ： 回调函数  
回调函数有两个参数 ： error  data
error ：如果读取失败 , error就是错误对象
		如果成功，error就是null
data： 如果读取成功，data就是读取的数据
		如果读取失败，error就是错误对象
        
 总之 ： 成功 ：error就是 null   data就是读取的数据
 		失败：error就是错误对象  data就是null
        
  输出的文件都是十六进制，想要查看使用 data.toString（）方法或者 String（data）
        
var fs = require('fs');

fs.readFile('./data/01.txt',function (error,data) {	
	if (error) {//============================添加读取失败提示
		console.log('读取文件失败')
		return ;
	} 
	console.log(data.toString());
});
```





### fs.writeFile()写文件

**语法**

`fs.writeFile(file, data[, options], callback)`

- param1 : 路径
- param2: 写入的内容
- param3 :  可选, 编码
- parm4:  callback 写入结果 

特点: 

- *会覆盖原有内容*
- 当文件名不存在时, 会创建这个文件, 执行写入操作

```js
fs.writeFile ();
参数1 ：要写入文件路径
参数2:  要写入的文件内容
参数3：  回调函数  function(error) 有一个形参
	写入成功： error : null
	写入失败： error：就是错误对象
    
var  fs = require('fs')

fs.writeFile('./data/name.txt', '大家好，我是nodejs',function (error) {
	if (error) {    //=======================添加写入结果
		console.log('文件写入失败');
    }else {
        console.log('文件写入成功');
    }
})

```



### fs.appendFile()追加内容

**语法**

`fs.appendFile(path, data[, options], callback)`

```js
path: 路径, 
data: 追加内容,
[option]: 编码
callback: 处理结果

const fs = require('fs')
fs.appendFile('./data.txt', '\n你是个好人', error=> {
    if (error) {
        console.log('追加失败)
    }
     console.log('写入成功')               
})
```

### fs.rename()重命名

**语法**

`fs.rename(oldname, newname, error => {})`



### 其他API

| 方法名                                  | 描述                   |
| --------------------------------------- | ---------------------- |
| `fs.readFile(path, callback)`           | 读取文件内容（异步）   |
| `fs.readFileSync(path)`                 | 读取文件内容（同步）   |
| `fs.writeFile(path, data, callback)`    | 写入文件内容（异步）   |
| `fs.writeFileSync(path, data)`          | 写入文件内容（同步）   |
| `fs.appendFile(path, data, callback)`   | 追加文件内容（异步）   |
| `fs.appendFileSync(path, data)`         | 追加文件内容（同步）   |
| `fs.rename(oldPath, newPath, callback)` | 重命名文件（异步）     |
| `fs.renameSync(oldPath, newPath)`       | 重命名文件（同步）     |
| `fs.unlink(path, callback)`             | 删除文件（异步）       |
| `fs.unlinkSync(path)`                   | 删除文件（同步）       |
| `fs.mkdir(path, mode, callback)`        | 创建文件夹（异步）     |
| `fs.mkdirSync(path, mode)`              | 创建文件夹（同步）     |
| `fs.rmdir(path, callback)`              | 删除文件夹（异步）     |
| `fs.rmdirSync(path)`                    | 删除文件夹（同步）     |
| `fs.readdir(path, option, callback)`    | 读取文件夹内容（异步） |
| `fs.readdirSync(path, option)`          | 读取文件夹内容（同步） |
| `fs.stat(path, callback)`               | 查看文件状态（异步）   |
| `fs.statSync(path)`                     | 查看文件状态（同步）   |







##  path操作路径模块

路径存在兼容问题, window路径以`\` 表示路径分隔符, 其他操作系统已`/` 表示路径分隔符

### path.join()

 `path.join()` 方法使用平台特定的分隔符作为定界符将所有给定的 `path` 片段连接在一起，然后规范化生成的路径。 

**语法**

**path.join([...paths])**

```js
const path = require('path')

path.join(__dirname, './aa')
```

**优化读文件的路径**

- 能够解决手动拼路径的错误
- 能够解决系统兼容性错误

```js
const fs = require('fs')
const path = require('path')

fs.readFile(path.join(__dirname, 'data.txt'), 'utf8', (err, data) => {
    if (err) {
        console.log('读取失败')
    }
})
```





### path模块的常用方法

> 关于路径，在linux系统中，路径分隔符使用的是`/`，但是在windows系统中，路径使用的`\`

在我们拼写路径的时候会带来很多的麻烦，经常会出现windows下写的代码，在linux操作系统下执行不了，path模块就是为了解决这个问题而存在的。

常用方法：

```javascript
path.join();//拼接路径

//windows系统下
> path.join("abc","def","gg", "index.html")
"abc\def\gg\a.html"

//linux系统下
> path.join("abc","def","gg", "index.html")
'abc/def/gg/index.html'

path.basename(path[, ext])	返回文件的最后一部分
path.dirname(path)	返回路径的目录名
path.extname(path)	获取路径的扩展名

var path = require("path");
var temp = "abc\\def\\gg\\a.html";
console.log(path.basename(temp));//a.html
console.log(path.dirname(temp));//abc\def\gg
console.log(path.extname(temp));//.html
```

【优化读写文件的代码】

### path模块其他api（了解）

| 方法名                       | 描述                                 |
| ---------------------------- | ------------------------------------ |
| `path.basename(path[, ext])` | 返回文件的最后一部分                 |
| `path.dirname(path)`         | 返回路径的目录名                     |
| `path.extname(path)`         | 获取路径的扩展名                     |
| `path.isAbsolute(path)`      | 判断目录是否是绝对路径               |
| `path.join([...paths])`      | 将所有的path片段拼接成一个规范的路径 |
| `path.normalize(path)`       | 规范化路径                           |
| `path.parse(path)`           | 将一个路径解析成一个path对象         |
| `path.format(pathObj)`       | 讲一个path对象解析成一个规范的路径   |



## http模块

用来搭建服务器, 处理http请求和响应



### 构建web服务器

在node很容易就能创建一个web服务器

cmd中关闭当前服务器   `ctrl + C`  

在node中想要使用模块就必须加载（require）

**代码一旦修改, 服务器就需要重启**

**创建服务器四步**

- 1- 引入HTTP核心模块 
- 2 - http.createServer() 创建一个服务器
- 3- 绑定监听事件
- 4- 设置端口, 打开服务器

**在处理请求的过程**

- 获取请求报文
- 设置响应报文内容

```js
// 1====加载HTTP核心模块 
const http = require('http')  
 
 // 2===  createServer（）方法返回一个服务器
 const server = http.createServer() //=========创建服务器
 
 //3====当收到客服端发送的请求了，就自动触发request请求，然后执行第二个参数，处理回调函数

 //request : 请求对象  可以用来获取客服端的一些请求信息
 //request.url  能拿到浏览器地址栏端口号后面的路径
 
  //response ：响应对象  用来给客户端发送响应消息
 //respons.write（）可以给客服端发送响应数据，write可以使用多次，但是醉倒一定要用end来结束响应	否则客户端会一直等待
 
 //3 - 给服务器绑定一个监听事件
server.on('request', function(request ， response) { 
	console.log('收到客户端的请求了' +request.url)
    
     response.write('hello')
	 response.write('end')
	 response.end()// end（）支持两种数据格式：二进制和字符串，二进制可以通过toString（）转化为字符串
});


// 4- 设置端口, 打开服务器
server.listen(3000, function () {
    console.log('the server is running...')
})

```

![](images\http.png)

```js
//4=====绑定端口号 启动服务器  此时已经创建的HTTP服务器，能收到请求，但是没有处理能力
server.listen(3000,function () {
	console.log('服务器启动啦，可以通过http://127.0.0.1：3000 来访问啦');
})

//在浏览器器中输入 http://127.0.0.1:3000/  黑窗口中就可以收到客服端的请求
//此时，服务器只能接受请求，不能处理请求，客服端会一直处于等待装填中



```

通过上面的代码，就可以创建一个服务器，并且能够响应给客服端，但是不管是什么请求，服务器只能返回hello end 功能还很弱

```js
response.write('hello')
response.write('end')

//=============由于每次都需要end一下所以：在结束的时候发送数据
response.end（'hello world'）
```



#### req请求报文

- 获取请求方式
  - `req.method`  GET 或 POST
- 获取请求地址
  - `req.url` 不包含协议和域名
- 获取请求头
  - `req.header` 获取的是一个对象

#### res响应报文

在服务器中设置`res` 响应对象

- 状态行
  - 状态码 `res.statusCode = 200`
  - 状态文本 `res.statusMessage = 'not found'`  不支持中文, 不推荐设置

- 响应头
  - `res.setHeader('content-type', 'text/html; charset=utf-8')`
  - `res.setHeader('aa', 'bb')`

- 响应体
  - `res.write('res is ok')` 可以写多个

### 根据不同的url响应不同的数据

`req.url`获取的是端口号之后的那一部分的路径

也就是说所有的url 都是以 `/ `开头的，不加` /` 浏览器会自动加 

end（）只能是二进制或者字符串

```js
var http = require('http')

var server = http.createServer()

server.on('request',function (req,res) {
	
	console.log('收到客户端请求了' + req.url)

	var url = req.url
	
    //根据不同的地址，输出不同的内容
	if (url === '/') {
		res.end('index.html')
	}else if(url === '/login') {
		res.end('login.html ')
	}else {
		res.end('404 not found')
	}
})

server.listen(80, function () {
	console.log('服务器启动了，可以来访问啦')
} )
```



### 汉字乱码问题（Content-Type）

text/plain  浏览器就会以普通文本解析响应

text/html  浏览器就会以html解析响应

并且要声明以什么编码格式解析： Content-Type

对于文本类型的数据，最好都加上编码，目的是为了防止中文解析乱码问题

```js
  // 在服务端默认发送的数据，其实是 utf8 编码的内容

  // 但是浏览器不知道你是 utf8 编码的内容

  // 浏览器在不知道服务器响应内容的编码的情况下会按照当前操作系统的默认编码去解析

  // 中文操作系统默认是 gbk

  // 解决方法就是正确的告诉浏览器我给你发送的内容是什么编码的

  // 在 http 协议中，Content-Type 就是用来告知对方我给你发送的数据内容是什么类型

  // res.setHeader('Content-Type', 'text/plain; charset=utf-8')

  // res.end('hello 世界')

```

不同的资源对应的 Content-Type 是不一样，具体参照：http://tool.oschina.net/commons

.jpg 的文件类型时 `image/jpeg`

### 字符编码（charset）

一般只对字符数据指定字符编码，对于图片，我们就不需要指定字符编码，只需要指定响应内容类型为image/jpeg就可

### 完整服务器搭建

http模块和 fs文件操作模块搭配，就可以访问其他路径的文件

对于服务器而言响应就把把一段字符串响应给客服端，服务器要说明响应内容的类型（Content-Type），浏览器会根据内容的类型进行解析，如果`text/html` 就会按照HTML就行解析

```js
var http = require('http')
var fs = require('fs')

var server = http.createServer()

server.on('request', function(req, res) {
    var url = req.url

    if (url === '/') {
        fs.readFile('./resource/index.html', function(err, data) {
            if (err) {
                res.setHeader('content-Type', 'text/plain; charset=utf-8')
                res.end('读取文件失败，稍后请重试')
            } else {
                res.setHeader('Content-Type', 'text/html; charset=utf-8')
                res.end(data)
            }
        })
    } else if (url === '/bady') {
        fs.readFile('./resource/ab2.jpg', function(err, data) {
            if (err) {
                res.setHeader('content-Type', 'text/plain; charset=utf-8')
                res.end('读取文件失败，稍后请重试')
            } else {
                res.setHeader('Content-Type', 'image/jpeg;')
                res.end(data)
            }
        })

    }

})

server.listen(3000, function(error, data) {
    console.log('server  is  running ....')


})
```





## ip地址和端口号

ip地址用来定位计算机，端口号定位具体的应用程序（所有联网的通信软件都必须有端口号），必须有相应的端口号，才能识别不同的应用程序

客户端通过ip地址定位服务器的计算机，通过端口号定位服务器的服务程序，而且服务器在回响应的时候，也需要

端口号给客户端发送响应, 但是服务端api已经高度封装了，服务端发响应会自动获取客户端的ip和端口号，不需要

手动获取，但是客户端访问服务器必须需要ip和端口号，但是浏览器会帮我们获取一个空闲的端口号，访问服务器

获取客户端的端口号有一个 API ： . socket. removePort（端口号）     .socket.remoteAddress（ip地址）

```js
// ip 地址用来定位计算机
// 端口号用来定位具体的应用程序
// 所有需要联网通信的应用程序都会占用一个端口号

var http = require('http')

var server = http.createServer()

// 2. 监听 request 请求事件，设置请求处理函数
server.on('request', function (req, res) {
  console.log('收到请求了，请求路径是：' + req.url)
  console.log('请求我的客户端的地址是：', req.socket.remoteAddress, req.socket.remotePort)

  res.end('hello nodejs')
})

server.listen(5000, function () {
  console.log('服务器启动成功，可以访问了。。。')
})
```



端口号有一定的范围 ：0 - 65536 之间

在计算机中有一些默认的端口号，最好不要去使用  例如 ： HTTP ：80

在开发过过程中，最好不要使用，使用一些没有含义的端口号 ：3000,5000,8000等

网站上线了，在使用默认的 80 端口





# node.js第二天



## 代码风格

- [JavaScript Standard style](https://standardjs.com/)
- Airbnb javaScript Style   

### 代码结束分号省略

要注意三种情况：一行代码以 ？ 开头

- （

- [
- `  **反引号ES6 新增：模板字符串  包裹字符串，支持换行和 变量的拼接**

以这三种开头的时候，需要在前面补个分号`;`，避免语法错误 而且用 `~`  `！`  `&`  也可以 但是不推荐 



## 第三方MIME模块

后台服务器在给前端返回资源时, 需要明确告诉前端返回的资源类型, 以保证浏览器的正常解析

如果后台没有告诉前端浏览器资源的类型, 浏览器只能靠猜测, 但是不准确

后台设置`MIME` : 设置`content-type`

**解决`content-type`类型**

**安装**

```shell
$ npm i mime
```

**使用**

- **`mime.getType(url地址)` :能够智能获取`content-type`**
- `mime.getExtension()`  根据mime类型, 获取后缀名

```js
const mime = require('mime')

//能获取参数url的文档类型, 并返回文档类型
mime.getType(url地址)
```



## moment第三方模块

 一个轻量级的JavaScript日期库，用于解析，验证，操作和格式化日期。 



## Apache的不同路径响应

```js
var fs = require('fs')

var http = require('http')

var server = http.createServer()

//获取网站的根目录
var wwwDir = 'E:/node/day02'

server.on('request', function(req, res) {

    var url = req.url

    //当不时 '/' 是就访问网站主页
    var filePath = '/index.html'

    //判断访问的路径 ,如果是 / 就不会进入if判断
    if (url !== '/') {
    		//把地址栏的/后面的路径获取给变量filePath 
        filePath = url
    }
        //把跟目录和地址后的路径进行拼接，响应给客户端
        fs.readFile(wwwDir + filePath, function(err, data) {

            if (err) {
                return res.end('404 Not Found')
            }

            res.end(data)
        })

    } 

})

server.listen(3000, function(err, data) {
    console.log('server running....');
})
```



## Apache的目录效果



### 读取目录（fs . readdir）

```js
//这个 API 能够动态的获取目录

 fs.readdir(wwwDir, function (err, files) {
      if (err) {
        return res.end('Can not find www dir.')
      }
     console.log(files)  //输出是一个一个目录数组
 })    
```



### 显示目录

- 读取根目录中的文件名和目录名 （fs . readdir）
- 如何将得到的文件名和目录名替换到 template.html 中
  + 在 template.html 中需要替换的位置预留一个特殊的标记（^ _ ^）（就像以前使用模板引擎的标记一样）
  + 根据 files 生成需要的 HTML 内容
-  生成需要替换的内容
-   替换标记   并且发送解析替换过后的响应数据

```js
var fs = require('fs')

var http = require('http')

var server = http.createServer()

server.on('request', function(req, res) {

    fs.readFile('./template.html', function(err, data) {

        if (err) {
            return res.end('404 not found')
        }

        //动态的读取目录
        fs.readdir('E:/node/day02', function(err, files) {
            if (err) {
                return res.end('404 not files')
            }

            var content = ''
            
            //遍历，目录数组中每一项，根据目录中的个数动态的生成每一行
            files.forEach(function(item) {
                content += `
			   <tr>
            		<td data-value="apple/"><a class="icon dir" href="/D:/Movie/www/apple/">
            		${item}/</a></td>
            		<td class="detailsColumn" data-value="0"></td>
            		<td class="detailsColumn" data-value="1509589967">2017/11/2 上午								10:32:47</td>
          		</tr>
        		 `
            })

            //字符串的替换
            data = data.toString()
            data = data.replace('^_^' , content) 

            //发送响应
            res.end(data)
        })
    })
})

server.listen(3000, function(err, data) {
    console.log('Server is running......')
```



## 在node中使用模板引擎



### 安装(art-template)

在对应目录执行，就会下载到对应的目录下`npm install art-template  --save` 

模板引擎不关心内容格式，只关心自己认识的标记语法，在模板中的内容都被当做字符串输出

### 引包

在html中用script就可以把模板引擎引入，在node不同通过这种方式引入

在node中，使用require加载art-template，只需要require就可以了:`var art= require（'art-template'）`

require中的参数就是art-template下载的名字

`render（）`是模板引擎提供的一个`API`能够渲染，解析替换，通过模板引擎把页面中的一些标记替换

render (替换字符串 ， {解析替换对象})

```js
var template = require('art-template') //加载模板引擎

var fs = require('fs')

var http = require('http')

var server = http.createServer()

server.on('request', function(req, res) {

		var url = req.url 

		console.log('客户端发请求了' +url)

    fs.readFile('./04-temp.html', function(err, data) {
        if (err) {
            return res.end('404 not found')
        }

        //render（）只能接受字符串，readfile读取的是二进制，需要toString一下
        var ret = template.render(data.toString(), {

            name: 'Jack',
            age: 18,
            province: '北京市',
            hobbies: [
                '写代码',
                '唱歌',
                '打游戏'
            ],
            title: '个人信息'

        })

        res.end(ret)//响应给客户端
    })

})

server.listen(3000, function(err, data) {
    console.log('server is running')

})
```



### 模板引擎的语法

`{{}}`括号中间放标记的变量

```css
//需要先引入
<script src="node_modules/art-template/lib/template-web.js"></script>
//打标记
<script type="text/template" id="tpl">
<!DOCTYPE html>
    <html lang="en">
    <head>
      <meta charset="UTF-8">
	  <title>{{title}}</title>
    </head>
    <body>
      <p>大家好，我叫：{{ name }}</p>
      <p>我今年 {{ age }} 岁了</p>
      <h1>我来自 {{ province }}</h1>
      <p>我喜欢：{{each hobbies}} {{ $value }} {{/each}}</p>
    </body>
    </html>
```



## 服务端渲染和客户端渲染

服务端渲染：查看网页源代码，可以搜索到的，就是服务端渲染的 （京东商品页面）

客户端渲染：在网页源代码中看不到，是客户端通过ajax请求，动态追加的渲染的，（京东商品评论）

**区别：**

服务端渲染不利于SEO搜索引擎优化，搜索时，搜不到，无法被爬虫抓取

客户端渲染可以背爬虫抓取到，，可以搜索到

好的网站两者结合，保证SEO，爬虫能搜索

到，也能保证用户体验，商品评论用客户端渲染，商品在服务端渲染

考虑SEO在服务端渲染，不考虑SEO用客服端渲染

### 创建服务器简写

```js
var http = require('http')
var fs = require('fs')
http
  .createServer(function (req, res) { 
})
 .listen(3000,function () {
    
})
```



## 网站静态资源

浏览器收到 HTML 响应内容之后，就要开始从上到下依次解析，当在解析的过程中，如果发现：
      link
      script
      img
      iframe
      video
      audio
等带有 src 或者 href（link） 属性标签（具有外链的资源）的时候，浏览器会自动对这些资源发起新的请求。

> 对于一些客服端请求的静态资源,最好都放在一个`public`文件夹里



## node中的console (REPL)

> 作用 类似浏览器中的console控制台,能够测试node中的一些API
>
> 在任意路径 输入 node 回车即可
>
> 在node环境中, 任意核心模块中的 API 不需要 require 就可以使用测试
>
> 退出node环境 : ctrl + C  , C (两次C) 退出





## url 模块

url 是一个 node提供的模块, 中有相应的`API`可以操作路径, 其中就有一个 parse() 方法能够 把路径以对象的方式

输出,并且能够得到我们想要的路径 , 其中的pathName属性就可以拿到表单提交的地址

> 使用 url.parse 方法将路径解析为一个方便操作的对象，第二个参数为 true 表示直接将查询字符串转为一个对象（通过 query 属性来访问）
>
> pathName   单独获取不包含查询字符串的路径部分（该路径不包含 ? 之后的内容）

```js
var url = require('url')

//参数 true 能够把 /pinglun 后面表单提交的数据变成一个对象  
//就是 query属性的值变成一个对象


var obj = url.parse('/pinglun?name=的撒的撒&message=的撒的撒的撒', true)

console.log(obj)
console.log(obj.query)
```



![](images\url_parse.png)



## 留言版项目

> 注意点: 在服务端的响应给客户端页面里, 里面的静态资源的路径使用url路径 / 
>
> 服务器会开放一个 /public/ 目录,供客户端浏览器访问服务器的静态资源,所有在响应的页面中的静态资源路径都写成  /public/ xxx
>
> / 就是url根路径的意思,浏览器在请求静态资源的时候,会把 http: // 127 . 0 . 0 .1 拼上 url路径 



客户端重定向 :  当提交 评论后, 浏览器根据看到状态码为 `302`  会根据 `location`的路径`/`向服务器发起请求,相当

于刷新页面,重新加载,在这个过程中,表单饿数据已经追加到服务器的 模板引擎渲染数据的数组中

**思路**

```js
// 1. / index.html
// 2. 开放 public 目录中的静态资源
//    当请求 /public/xxx 的时候，读取响应 public 目录中的具体资源
// 3. /post post.html
// 4. /pinglun  
	//在点击发表时,表单会把内容提交到 action的路径文件中 
//    4.1 接收表单提交数据
//    4.2 存储表单提交的数据
//    4.3 让表单重定向到  location /  状态码 302  
//        statusCode
//        setHeader
```

**代码**

```js
var fs = require('fs')
var http = require('http')

//使用 url 模块
var url = require('url')

//加载模板引擎
var template = require('art-template')

//渲染到客户端的数据
var comment = [
  {
    name: '张三',
    message: '今天天气不错！',
    dateTime: '2015-10-16'
  },
  {
    name: '李四',
    message: '今天天气不错！',
    dateTime: '2015-10-16'
  },
  {
    name: '张三3',
    message: '今天天气不错！',
    dateTime: '2015-10-16'
  },
  {
    name: '张三4',
    message: '今天天气不错！',
    dateTime: '2015-10-16'
  },
  {
    name: '张三5',
    message: '今天天气不错！',
    dateTime: '2015-10-16'
  }
]

http
.createServer(function (req , res) {
	
	//把客服端url的数据给一个变量对象
	var urlObj = url.parse(req.url , true)

	//用pathName获取 搜索前面的路径
	var  pathname = pathObj.pathname


	//主页使用模板引擎对数据进行渲染
	if (pathname === '/') {
		fs.readFile('./views/index.html', function (err , data) {
			if (err) {
				return res.end('404 is not found')
			}

			//使用模板引擎进行渲染
			var htmlStr = template.render(data.toString() , {
				conments : comment
			})

			res.end(htmlStr)
		})
	}

	//浏览静态资源请求静态资源的处理
	else if (pathname.indexOf('/public/') === 0) {
		fs.readFile('.'+ pathname , function (err , data) {
			if (err) {
				return res.end('404 is not found')
			}

			res.end(data)
		})
	}

	//评论页
	 else if ( pathname === '/post') {
		fs.readFile('./views/post.html', function (err, data) {
			if (err) {
				return res.end('404 not found....')
			}
			res.end(data)
		})
	}


	//表单提交处理
	else if ( pathname === '/pinglun'){
		
		//res.end(JSON.stringify(pathObj.query))

		//获取表单提交的内容
		var common = urlObj.query
		//把评论内容追加到数组中
		common.dataTime = '2019-8-22 19:44'
		comment.unshift(common)

		//设置客户端重定向,让状态吗为302
		res.statusCode = 302
		//浏览器看到状态码为302 就直接去看location  / 代表根路径
		res.setHeader('Location' , '/')
		res.end()
	  
	}
	//客户访问不存在页面的返回404页面
	else {
		fs.readFile('./views/404.html', function (err, data) {
			res.end(data)
		})
	}

})
.listen(3000 , function () {
	console.log('the server is running')
})
```





# node 第三天



## 前端好的书籍

 《JavaScript 高级编程》第3版

《JavaScript 语言精粹》

## npm

全称 : node package manager   node的包管理工具

第一层含义: 也是一个网站 里面存放了很多第三方包[npm官网](http://www.npmjs.com)

第二层含义 : 是一个命令行工具,只要安装了`node`,就安装了 `npm`

```js
npm --version  //查看npm版本
npm install  --global  npm //升级npm   
```

### 常用命令

博客 : [npm常用命令](http://www.cnblogs.com/PeunZhang/p/5553574.html)

- `npm init  ` 
  - 下载包描诉文件`package.json`  项目初始化
  - `npm init -y  `可以跳过向导 , 快速生成
- `npm install ` 
  - 一次性把depandencies中的依赖项全部下载
  - npm  i 
- `npm install  + 包名`
  - npm  i  单纯的下载
- `npm install  --save + 包名`   
  -  下载并且保存文件依赖项 ( package中的depandencies选项 ) 
  - `npm i -S + 包名`
- `npm  uninstall  + 包名`
  - 只删除,如果有依赖依然会保存
  - `npm  un`
- `npm  uninstall  --save`
  - 删除包的同时也会删除依赖信息
  - `npm  un  -S`
- `npm help  `
  - 查看使用帮助
- `npm + 命令  --help`
  - 查看当前命令的使用帮助
  - aliases: i, isntall, add   别名
  - common options: --save-prod  /  --save-dev  /  --save-optional  / --save-exact  /  --no-save
- `mkdir + 文件夹名`  :  创建文件夹
- `rmdir + 文件名` :    删除文件夹 

**npm升级自己**

```shell
 $ npm install npm -g 
```

**清空npm缓存**

```shell
#由于网速问题, 下载的包不完整, 又删不掉
$ npm cache clean -f
```



### 解决npm被墙问题

npm 存储包文件的服务器在国外, 有时候会被墙, 速度很慢 , 怎么解决这个问题

淘宝开发人员在国内做了一个npm备份   [npm镜像国内版](http://npm.taobao.org/)

安装淘宝的 : `cnpm`

```powershell
#在任意目录执行都可以  --global 表示全局   npm依旧可以继续使用
npm  install  --global  cnpm
```

接下载你安装包的时候把之前的`npm` 替换成 `cnpm`

```shell
# 这里走国外的npm 服务器
npm  install  jquery

#cnpm 会走国内的淘宝服务器
cnpm  install  jquery
```

不安装`cnpm` 又想通过 淘宝的服务器下载文件 可以使用这种方法

```shell
npm install jquery --registry=https://registry.npm.taobao.org
```

但是每一次手动输入很麻烦,我们可以把这条命令加入到配置中

```shell
#只要配置之后,以后的npm install 都会默认通过淘宝的服务器来下载
npm config set registry https://registry.npm.taobao.org

# 查看npm配置信息
npm config list
```



### 安装文件

- `npm install   jquery `(文件名)
- `npm install(i)  art-template@1.12.0`    指定安装版本
- `npm install  art-template  jquery bootstrap`  安装多个包

### package.json(包描述文件)

**存放在项目的根目录下**

- `npm install jquery --save`   中加上 `--save` 能够在`package.json`生成第三方包的依赖信息建议安装第三方包的时候都加上 `--save` , 第二个作用, 在第三方包 `node_modules` 丢失时, 直接 `npm install`  会根据`package.json`的依赖信息把丢失的包安装回来

```js
"dependencies": {
    "bootstrap": "^4.3.1", // 包的依赖
    "jquery": "^3.4.1"     //依赖
  }
```

- 建议在每个项目的目录下都有一个`package.json` 包描述文件.就像产品的说明书一样
- 在项目目录 下: 输入 `npm init`  会自动产生`package.json`  产生一个向导,配置package的参数 

```js
package name: (npm-install)      // 确定生成的包名路径 可修改
version: (1.0.0) 0.0.1		     //版本信息 , x.y.z; 如果只是修改BUG修改Z位, 添加新功能, 向下兼容,修改y位, 有重大更新, 不向下兼容修改X位
description: 这是一个测试文件      //描诉
entry point: (index.js) main.js  //入口文件
test command:					
git repository:					//github的资源库地址
keywords:						
author: 刘自成
```



###  package.json和 package-lock.json

**` package-lock.json` 用来锁住包问的版本和来源**

> npm 5以前没有 package-lock.json
>
> npm 5 以后才加入这个软件
>
> package-lock 可以保存依赖信息 , 锁住包的版本

- 在安装包的时候, npm都会生成或者更新 `package-lock`这个文件
- `npm 5` 以后的版本会自动保存依赖项 , 不需要加`--save`
- 当安装包的时候, 会自动创建或者更新
- 当我们下载一个第三方包的时候, 会把依赖包也下载下来, 所以 `package-lock`就保存了, `node_modules`中 所有包的依赖信息 ( 包括版本 , 下载地址 )
  - 当我们某些第三方包丢失的时候, **重新下载会比之前下载的速度快**
- 从文件来看, 有一个`lock`称之为锁
  - **lock 用来锁住版本和来源, 保证下载的包和原来的包一模一样**
  - **重新下载就会下载最新版而不是 原来的版本**
  - `package-lock` 可以用来锁定版本号 , 防止自动升级



### npm的本地安装和全局安装

**本地安装**

项目中要用到某个包, 使用本地安装 npm i  包

**全局安装**

能够得到一个命令行工具, 可以使用一些命令 `npm i bao -g`



## nrm

### 什么是nrm

提供了一些最常用的NPM包镜像地址，能够让我们快速的切换安装包时候的服务器地址；**不是一个装包工具**

什么是镜像：原来包刚一开始是只存在于国外的NPM服务器，但是由于网络原因，经常访问不到，这时候，我们可以在国内，创建一个和官网完全一样的NPM服务器，只不过，数据都是从人家那里拿过来的，除此之外，使用方式完全一样

> 注意： nrm 只是单纯的提供了几个常用的 下载包的 URL地址，并能够让我们在 这几个 地址之间，很方便的进行切换，但是，我们每次装包的时候，使用的装包工具，都是  npm

### 安装nrm

```shell
$ npm i -g nrm
```

### 切换npm下载地址

```shell
$ nrm use taobao(npm/ cnpm/ ...)
```

### 查看镜像切换地址

```shell
$ nrm ls
```



## 请求状态码(status)	

- 永久重定向 301

  > 浏览器会记住 location 的路径, 访问 a 网站 加载 b 网站, 下次访问的时候,直接访问B网站 , 从缓存中拿数据访问重定向的地址 , 不会在走 a网站了

- 临时重定向 302

  > 浏览器不会记住 临时记住b网站, 能走通就走,走不通时,还会去a去问一下  下次访问 a网站 还会 先访问 a 在去 b





## url模块

node中提供了一个核心模块获取地址栏的url信息

### url.parse()

将url各个部分分割, 能够提供我们想要的数据, 默认是不会解析查询字符串,`query` 中是地址栏? 后面的部分

**url.parse(请求地址[, parseQueryString[, slashesDenoteHost]])**

- 请求地址 : The URL string to parse.
- 布尔类型,:  是否解析`query` 查询字符串, 传`true` 能够将url中的`query` 解析成一个对象,url模块会调用`queryString` 模块去解析`query`  , 默认值`false` 不解析为对象
- 布尔类型 :   If `true`, the first token after the literal string `//` and preceding the next `/` will be interpreted as the `host`. For instance, given `//foo/bar`, the result would be `{host: 'foo', pathname: '/bar'}` rather than `{pathname: '//foo/bar'}`. **Default:** `false`.



## querystring模块

解析查询字符串的模块

使用场景: 已经能得到地址栏的查询字符串, 就可以直接使用这个模块去解析查询字符串

**querystring.parse(str[, sep[, eq[, options]]])**

- `str`<string> : 要解析的 URL 查询字符串。
- `sep`<string> 用于在查询字符串中分隔键值对的子字符串。**默认值:** `'&'`。
- `eq` <string> 用于在查询字符串中分隔键和值的子字符串。**默认值:** `'='`。
- `options` <object>
  - `decodeURIComponent` <function>解码查询字符串中的百分比编码字符时使用的函数。**默认值:** `querystring.unescape()`。
  - `maxKeys` <number>指定要解析的键的最大数量。指定 `0` 可移除键的计数限制。**默认值:** `1000`。

`querystring.parse()` 方法将 URL 查询字符串 `str` 解析为键值对的集合。



## [moment格式化时间模块]( http://momentjs.cn/  )

### 安装

```shell
$ npm i moment
```

### 使用

[显示时间](http://momentjs.cn/docs/#/displaying/ )

`moment()` 可以不传时间, 默认使用系统的当前时间

```js
#年: YYYY  月: MM  日: DD   时:HH   分:mm   秒: ss 
const moment = require('moment')
moment(时间).format(格式)

let date = new Date()
moment(date).format('YYYY年MM日DD日   HH:mm:ss')
//moment().format('YYYY年MM日DD日   HH:mm:ss') 和上面一样
```





## 在服务端页面重定向

服务器无法直接控制浏览器页面跳转, 但是可以通过设置响应报文, 告诉浏览器跳转到相应的页面

### 设置响应报文

```js
//重定向必须设置状态码
res.statusCode = 302

//在响应头中设置跳转地址
res.setHeader('location', '/')

res.end()
```



## JSON.stringify()带格式转换

在转换json数据时, 默认是不带格式的

```
JSON.stringify(value[, replacer [, space]])
```

**参数说明**

`value`

> 将要序列化成 一个JSON 字符串的值。

`replacer` 可选

> 如果该参数是一个函数，则在序列化过程中，被序列化的值的每个属性都会经过该函数的转换和处理；如果该参数是一个数组，则只有包含在这个数组中的属性名才会被序列化到最终的 JSON 字符串中；如果该参数为null或者未提供，则对象所有的属性都会被序列化；关于该参数更详细的解释和示例，请参考[使用原生的 JSON 对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Using_native_JSON#The_replacer_parameter)一文。

`space` 可选

> 指定缩进用的空白字符串，用于美化输出（pretty-print）；如果参数是个数字，它代表有多少的空格；上限为10。该值若小于1，则意味着没有空格；如果该参数为字符串(字符串的前十个字母)，该字符串将被作为空格；如果该参数没有提供（或者为null）将没有空格。



## 后端的获取数据GET 和 POST

**通过 `req.method` 能够知道前端提交表单的提交方式**	

### GET

```js
const url = require('url')

//在地址栏中获取表单提交的查询字符串
let getData = url.parse(req.url, true).query
```



### POST

前端 : post方式传输数据可能很大, 在传输给后台时, 会分段传输给后台

后台: 需要持续接收前端传递的片段, 进行拼接, 所有的数据传递完成后, 才能使用数据

借助`querystring` 模块可以直接获取post方式传过来的查询字符串

```js
const queryString = require('querystring')

 	//1.通过判断url路径和请求方式来判断是否是表单提交
    if (req.url === '/heroAdd' && req.method === 'POST') {
        /**服务端接收post请求参数的流程
         * （1）给req请求注册接收数据data事件（该方法会执行多次，需要我们手动累加二进制数据）
         *      * 如果表单数据量越多，则发送的次数越多，如果比较少，可能一次就发过来了
         *      * 所以接收表单数据的时候，需要通过监听 req 对象的 data 事件来取数据
         *      * 也就是说，每当收到一段表单提交过来的数据，req 的 data 事件就会被触发一次，同时通过回				   调函数可以拿到该 段 的数据
         * （2）给req请求注册完成接收数据end事件（所有数据接收完成会执行一次该方法）
         */
        
        
        //创建空字符叠加数据片段
        let data = '';

        //2.注册data事件接收数据（每当收到一段表单提交的数据，该方法会执行一次）
        req.on('data', function (chunk) {
            // chunk 传输的数据片段 , 默认是一个二进制数据，和 data 拼接会自动 toString
            data += chunk;
        });

        // 3.当接收表单提交的数据完毕之后，就可以进一步处理了
        //注册end事件，所有数据接收完成会执行一次该方法
        req.on('end', function () {

            //（1）.对url进行解码（url会对中文进行编码）
            data = decodeURI(data);
            console.log(data);

            /**post请求参数不能使用url模块解析，因为他不是一个url，而是一个请求体对象 */

            //（2）.使用querystring对url进行反序列化（解析url将&和=拆分成键值对），得到一个对象
            //querystring是nodejs内置的一个专用于处理url的模块，API只有四个，详情见nodejs官方文档
            let dataObject = querystring.parse(data);
            console.log(dataObject);
        });
    }

```



## 黑马留言

```js
const fs = require('fs')
const http = require('http')
const path = require('path')
const url = require('url')
const template = require('art-template')
const mime = require('mime')
const moment = require('moment')
const queryString = require('querystring')



http
  .createServer((req, res) => {
    let urlPath = req.url
    //主页
    if (urlPath === '/' || urlPath.startsWith('/index')) {
      readData(data => {
        data.list.sort((a, b) => b.id - a.id) 
        let str = template(path.join(__dirname, '/pages/index.html'), data)
        res.end(str)
      })

	//添加页面
    } else if (urlPath.startsWith('/add')) {
      fs.readFile(path.join(__dirname, '/pages/add.html'), (err, data) => {
        if (err) return console.log(err)

        res.end(data)
      })
	
     //post方式提交表单
    } else if (urlPath.startsWith('/submit') && req.method === 'POST') {
      let data = ''
      req.on('data', chunk => data += chunk)
      req.on('end', () => {
        data = decodeURI(data)
        data = queryString.parse(data)

        data.id = Date.now()
        data.created = moment().format('YYYY-MM-DD HH:mm:ss')

        readData(dataData => {
          dataData.list.push(data)

          writeData(dataData, () => redirect(res))
        })
      })
     //删除评论   
    } else if (urlPath.startsWith('/delete')) {
      let id = url.parse(urlPath, true).id
      readData(data => {
        data.list.splice(data.list.findIndex( v => v.id === id), 1)
        writeData(data, () => redirect(res))
      })
     //静态资源开放   
    } else if (urlPath.startsWith('/assets/')) {
      fs.readFile(path.join(__dirname, urlPath), (err, data) => {
        if (err) return console.log(err)

        res.setHeader('content-type', mime.getType(urlPath))
        res.end(data)
      })
        //404
    } else {
      res.end('404 not found')
    }
  })
  .listen(3000, () => {
    console.log('The server is running...')
  })

//读取数据
function readData(fn) {
  fs.readFile(path.join(__dirname, './data/data.json'), (err, data) => {
    if (err) return console.log(err)

    data = JSON.parse(data)
    fn && fn(data)
  })
}
//写入数据
function writeData(data, fn) {
  data = JSON.stringify(data, null, 2)
  fs.writeFile(path.join(__dirname, '/data/data.json'), data, err => {
    if (err) return console.log(err)

    fn && fn()
  })
}
//重定向
function redirect(res) {
  res.statusCode = 302
  res.setHeader('location', '/')
  res.end()
}
```





# nodejs第四天

## 路径问题

### 模块标识中的`/`和 文件操作路径`/`

- 文件操作中的相对路径`./`可以省略 

```js
fs.readFile('data/a.txt', function (err, data) {
  if (err) {
    return console.log('读取失败')
  }
  console.log(data.toString())
})
```

-  在模块加载中，相对路径中的 `./ `不能省略, 文件后缀可以省略

```js
//Error: Cannot find module 'data/foo.js'
require('data/foo.js')
```



### 文件操作`./`和`/`

- `./`表示相对路径
-  `/`表示磁盘根目录 ,当前在 C盘就在磁盘中找

在文件操作的过程中 : 

- 相对路径要不省略 `./` 要不就把 `./`加上 ,不能把`.`省略
- `/`表示 磁盘根目录

模块中的 `./` 和 `/`

- `/`  表示的就是磁盘根目录
- `./`  表示相对路径



## node的模块系统

相关书籍

[深入浅出Node.js(三) -朴灵 - 深入Node.js的模块机制](http://www.infoq.com/cn)

博客 : [Node.js模块机制](http://www.infoq.com/cn/articles/node-module-mechanism)

### 什么是模块化

在nodejs中每一文件就是一个模块, 每个文件都有自己的作用域,**当前模块的数据(变量和方法), 其他模块无法使用**

- 文件作用域
  - 文件与文件之间是封闭的,只能加载,不能访问成员
- 通信规则
  - 加载 require
  - 导出

###node中的模块分类

- **核心模块**
  + 文件操作模块 fs
  + http 创建服务器模块
  + url 路径操作模块
  + path 路径处理模块
  + os 操作系统信息模块
- **第三方模块**
  + art-template
  + mime
  + moment
  + Express
- **自定义模块**
  - 自己创建的JS文件
  - **需要路径标识**  `require('./a')`

### [CommonJs模块规范](https://javascript.ruanyifeng.com/nodejs/module.html )

在node中的JavaScript有个很重要的概念: 模块系统

- 模块作用域
- 使用require加载模块
- 使用exports接口对象来导出模块中的成员

### 核心模块

 核心模块文件已经被编译到了二进制文件中了，我们只需要按照名字来加载就可以了

```js
require('fs')

require('http')
```

### 第三方模块

凡是第三方模块都必须通过`npm` 来下载

使用的时候通过require( ' 包名' )的方式进行加载才可以使用

> 不存在任何一个第三方模块和核心模块的名字一致

**查找规则** : 首先在核心模块中查找, 找不到在node_modules中查找



### require查找规则

**首先会判断模块是不是路径**, **如果是路径, 就是自定以模块, 就会以路径去找**

**如果不是路径**, **会先当核心模块查找, 在当第三方模块查找**

**如果是核心模块, 直接去node安装包中的`node_modules` 中查找**

**既不是核心模块、也不是路径形式的模块, 则代表第三方模块查找**

- 先找到当前文件所处同级目录中的 node_modules 目录
- node_modules/art-template
- node_modules/art-template/package.json 文件
- node_modules/art-template/package.json 文件中的 main 属性
- main 属性中就记录了 art-template 的入口模块( 要加载的文件)
- 然后加载使用这个第三方包
- 实际上最终加载的还是文件

**当前文件下没有package.json这个文件或者mian属性是错的**

```js
#    如果 package.json 文件不存在或者 main 指定的入口模块是也没有
//    则 node 会自动找该目录(类似 mime包文件夹下)下的 index.js index.node , index.json
//    也就是说 index.js 会作为一个默认备选项
//    

#    如果以上所有任何一个条件都不成立，则会进入上一级目录中的 node_modules 目录查找
//    如果上一级还没有，则继续往上上一级查找
//    。。。
#    如果直到当前磁盘根目录还找不到，最后报错：
//      can not find module xxx
```

注意：我们一个项目有且只有一个 node_modules，放在项目根目录中，这样的话项目中所有的子目录中的代码都可以加载到第三方包
不会出现有多个 node_modules



### 模块的导入和导出

每一个模块都有自己的独立作用域, 模块中的成员和方法, 其他模块都无法使用, 需要模块自己导出, 其他模块导入才能使用

在node中每个js文件都有`module` 对象表示当前模块自身, module 有个一个exports 属性, 可以向外暴露属性

#### module.exports

能够导出模块的成员和方法, 导出的时候, 需要定义变量接收, 才是使用导出的属性和方法, `module.exports` 默认是个空对象

```js
module.exports = {
    show(){
      console.log('哈哈哈')  
    },
}
```

#### require

导入模块, 返回值, 是模块的暴露出去的数据





### 导出成员 （exports）

- node中是模块作用域 , 默认文件中的成员只在当前文件模块有效,其他模块只能加载不能访问其中的成员
- 对于希望被访问的成员可以挂载在`exports`接口对象中

每个文件模块中都提供了一个对象：`exports`: 接口对象

默认是一个空对象 是require的返回值

可以把所有需要被外部访问的成员挂载到exports这个空对象中

**导出多个成员**

> exports .  或者 module. exports = {  }

```js	
//在 b.js中
var foo = 'hahha'
exports.foo= 'heihiehie'
exports.add = function(x, y) {
    return x + y
}

//在 a.js中
var ret = require('./b') //接受require返回的值

console.log(ret) //  ==== { foo: 'heihiehie' }
console.log(ret.add(10 ,20));//========30

```

**导出单个成员 ( 必须是 module . exports )** 

> **返回值就是一个 数组 / 字符串 / 函数 /  对象**

```js
function add(x, y) {
  return x + y
}

//此时,在导出的exports就是一个函数而非是一个空的接口对象
module.exports = add
```

- 多个 module . exports 导出会覆盖前面的

```js
module.exports = 'hello'

module.exports = function (x, y) {
  return x + y
}    //  只会导出函数, 不会导出字符串
```

- 导出多个成员 module . exports =  {   }

```js
module.exports = {
  add: function () {
    return x + y
  },
  str: 'hello'
}
```



### module

在node中每个模块内部默认都有一个返回的module对象 , module对象中都有一个exports对象

```js
var module = {
  exports: {
  }
}
```

node为了简化操作,防止点的太多了,加了一个变量 使 `exports = module.exports`

```js
 var exports = module. exports
 
 //所有exports 和 module.exports 都是都一个对象
```



### exports 和 module.exports (面试能说清楚 NB)

- 为什么导出单个文件使用 module .exports 而不能使用 exports   
- 复杂类型 , 变量中存的是地址, 指向的是内存中的某块代码

> 在代码的结尾有  exports = module . exports
>
> 当exports = 新的值   时,这时候就改变了exports的地址指向 , 由原来的指向 module. exports 指向了新的对象, 但是 require返回的是 module . exports 中的内容
>
> 所以 exports = 新值  并不能改变 module . exports 中值

- 一但 exports 重新赋值 , 就和 module . exports没关系了 , 就不能用 exports 挂载成员了
- 给 module. exports 重新赋值 require返回的值也就改变了
- module.exports  和 exports 指向内存中同一个空对象, 一旦其中一个改变指向, 导入时就会以`module.exports` 导出的数据为准 

```js
exports.foo = 'bar'
// 这样使用, 两者没有区别, 都相当于给同一个对象添加属性或者方法
module.exports.a = 123


console.log(exports)  // {a:123， foo: 'bar' }  
console.log(module.exports)  //{a:123， foo: 'bar' } 

//如果导出一个对象, 此时 exports 和 module.exports 已经没关系了
exports = {
  a: 456
}

console.log(exports)  // {a:456 } 
console.log(module.exports)  // { foo: 'bar' , a:123 }
//也就是说， 我们在require的时候得到的时{ foo: 'bar' , a:123 } 而不是  {a:456 }

// 如果想要继续使用exports, 需要重新建立了和 module.exports 之间的引用关系了
exports = module.exports  //把地址给 exports

exports.a = 789

console.log(exports)  // { foo: 'bar' , a:789 }
console.log(module.exports)  // { foo: 'bar' , a:789 }

// 当module.exports 重新赋值时
module.exports = function () {
  console.log('hello')
}

//到我们在require时， 得到的时一个函数， 而不是这个对象 { foo: 'bar' , a:789 }
console.log(module.exports) //就是一个函数
console.log(exports)  // { foo: 'bar' , a:789 }
```



## 模块化开发

将代码按照功能, 分割成单个的模块, 每个模块的功能单一, 处理单一功能

优点: 代码结构清晰, 后期方便维护



## Express

原生的http在某些方面表现不足以应对我们的开发需求 ,  所以我们需要框架来提高我们的开发效率, 让我门的代码更高度统一

`koajs` 也是node开发框架 , 作者也是 `tj`

在 Node中有很多Web开发框架, 这里我们学习`Express`   网站 [express官网](https://www.expressjs.com)   author : `tj`

```shell
$ npm install express --save
```

[bootstrap官网](https://www.bootcss.com/ )

###文档官网的学习指南

> getting started   ===> cook  book   怎么使用 
>
> guide     指南



### express的基本使用

- 可以很容易的对访问路径的设置
  - API`use` 专门用来设置开放资源
- 可以很容易的设置开放的资源目录
  - `get`  专门用来设置网站访问路径
- `res.send()` 能够自动设置响应头

```js
//0 安装

// 1 引包
var express = require('express')

//2 创建server应用程序, 相当于 createServer
var app = express()

//公开静态资源API(  use )  
app.use('/public/' , express.static('./public/'))
app.use('/static/' , express.static('./static/'))

//处理get请求
app.get('/' , function (req , res) {
		res.send('hello express')
})

app.get('/post' , function (req , res) {
		res.send('这是一个post请求')
})

//设置端口
app.listen(3000 , function () {
	console.log('the server is running at 3000')
})
```



### nodemon代码修改后自动重启

需要使用第三方命令工具 : `nodemon` 解决频繁重启服务器问题

安装命令 : 

```shell
#在任意目录执行该命令都可以
#通过 --global 安装的包可以在任意目录执行
npm  install --global nodemon
```

安装完毕后,使用

```js
node app.js

//使用nodemon  
nodemon app.js 
```

只要通过`nodemon app.js`  启动的服务 , 则它就会自动监视文件的变化,自动重启服务器



### Express中的路由

#### 第一种app.method

**精确匹配,以指定的url地址开头结尾,必须是一模一样的地址才可以**

```js
//路由表
app
  .get('/login', 函数)
  .get('/dsadsa', 函数)
  .post('/d/sadsa', 函数)
  .get('dsadsa', 函数)
```

#### 第二种 app.use

**模糊匹配, 以任意的请求方式(不区分get, post), 匹配指定的url开头的请求**

`app.use('匹配地址', (req, res) => {})`

```js
app.use('/index', (req, res) => {
    # 匹配地址, 会作为匹配项, 不会作为url地址输出
    console.log('req.url', req.url)
    console.log('req.method' req.method)
})
```







### 开放静态服务(静态资源托管)

```js
app.use ('/public' , express.static('./public/'))
```

- 第一个参数 : 当以 `/public` 访问的时候 , 就去 `./public/` 中找相应的资源, 整个 public 就开放了
- 第二个参数 : 要开放的文件目录
- 支持别名 ( 不常用)

```js
app.use (express.static('./public/'))
```

当第一个参数省略的时候 `app.use (express.static('./public/'))`

- 就是把这个文件中的内容开放了, 访问直接用文件名即可**(就像放在网站根目录)**
- 在访问是直接把`public`省略,访问其中的文件, 加上`public`反而不行



### req拓展

#### req.query 

express提供了一个`API`  `req.query` 可以获取请求参数

```js
var content = req.query
```

#### req.body

需要通过第三方包,`body-parser`  获取post的请求体参数

```js
var body = req.body
```

 

### res拓展

`res.status(200)` 相当于 res.statusCode = 200

`res.set(k, v) ` 相当于 res.setHeader(k, v)

`res.send() `相当于 res.end()

`res.sendFile() `读取文件并返回

`res.redirect() `重定向

- `res.redirect([status,] path)`

```js
res.sendFile(path.join(__dirname, 'index.html'))

res.redirect('/')
```



## Express解析表单post请求

express没有提供能够直接获取post请求体的`api` , 需要借助第三方插件来获取

在express官网导航栏中 `Resources`  选项中的 `middleware`

#### 安装第三方包 body-parser

```shell
npm install --save body-parser
```

#### 配置

> 只要配置了, 则就会在`req`  请求对象上就会多一个属性 : `body` 就可以直接通过 `req.body` 就可以获取表单请求体数据了
>
> 一定要在路由挂载之前配置

```js
var express = require('express')
//引包
var bodyParser = require('body-parser')

var app = express()

//配置body-parser
// parse application/x-www-form-urlencoded
app.use(bodyParser.urlencoded({ extended: false }))
// parse application/json
app.use(bodyParser.json())

```

#### 使用

```js
	var content = req.body
	content.dateTime = '2099-99-99'
	comment.unshift(content)

	res.redirect('/')
```



## Express中get和post获取参数

### GET 

express提供了一个`API`  `req.query` 可以获取请求参数

```js
var content = req.query
```

### POST

需要通过第三方包,`body-parser`  获取post的请求体参数

```js
var body = req.body
```



### 在Express配置使用art-template模板引擎

[art-template 在 github仓库连接](https://github.com/aui/art-template)

[art-template官方文档](https://aui.github.io/art-template)

#### 安装

```shell
npm install --save art-template
npm install --save express-art-template
```

#### 配置

```js
app.engine('html' , require('express-art-template')) //配置模板引擎
app.set('views' , 'pages') //配置查找的目录
```

- 配置模板引擎必不可少
- 第一个参数 `html`  是加载渲染的模板文件类型 , 默认是 `art`

**默认会去`views文件夹` 中找 相应的文件**

但是可以修改 : 

- 第一个参数,只能是 `views`  , 意思是 基于哪个目录去找

```js
app.set('views' , render函数的路径)
```

#### 使用

```js
app.get('/' , function (req , res) {
    //默认会从views中找相应的文件index.html
	res.render('index.html' , { conments : comment	})
})
```

```js
var express = require('express')
var app = express()

//公开今天资源
app.use('/public/' , express.static('./public/'))


//配置express-art-template模板引擎
//express-art-template专门用来把art-template整合到express , 但是art-template也要安装
//express-art-template依赖了art-template
//第一个参数 art 是文件后缀,可以修改
app.engine('html' , require('express-art-template'))

//默认express中不能使用render方法,但是express如果配置art-template,就可以使用了
// res.render('html模板名' , {模板数据})
//第一个参数不能写路径,默认会去项目中的views目录查找该模板文件
//也就是说express有一个约定 : 开发人员会把所有的视图文件放在views 目录中

app.get('/' , function (req , res) {
	res.render('index.html' , {
		conments : comment
	})
})

app.listen(3000 , function () {
	console.log('I am running.....');
})
```



#### express重定向API(redirect)

> 会自动使用 res.end()

```js
	res.redirect('/')	

	//等价于
	res.statusCode = '302'
	res.setHeader('location' , '/)
```



## 外置路由

### 为什么使用

在`app.js` 中使用外置路由, 不一定要将路由绑定到app身上, 那样必须把app传给路由模块

也可以使用express提供的外置路由对象, 主动暴露给app.js

### 使用步骤

1. 创建外置路由对象
2. 给外置路由对象绑定路由
3. 向外暴露路由对象

4. 在`app.js` 中引入并使用路由中间件

```js
const express = require('express')

//创建外置路由对象
let router = express.Router()

//书写路由
router.get()
router.post()

//向外暴露路由
module.exports = router


//在app.js中
const router = require('./router')

app.use(router)
```





 

## 学生管理系统demo (CRUD)

### 下载所需第三方包

```shell
npm init -y
npm i -S express express-art-template 
npm i -S bootstrap@3.3.7
```

### 引包

```js
var fs = require('fs')
var express = require('express')
var app = express()
```

### 配置express的art-template

```js
//配置,模板引擎
app.engine('html' , require('express-art-template'))
//指定模板目录
app.set('views', 'pages')
```

### 开放静态资源

```js
app.use('/public/' , express.static('./public/'))
app.use('/node_modules/' , express.static('./node_modules/'))
```

### 设置相关文件目录

```shell
mkdir crud
mkdir public
mkdir views
```

### 处理JSON数据转换字符串和对象

```js
//都把字符串转换为对象
JSON.parse()

//把对象转换成字符串
JSON.stringify()
```

### 页面初始化

```js
var fs = require('fs')
var express = require('express')
var app = express()


app.engine('html' , require('express-art-template'))

//开放资源
app.use('/public/' , express.static('./public/'))
app.use('/node_modules/' , express.static('./node_modules/'))


app.get('/' , function (req , res) {
	fs.readFile('db.json','utf8', function (err , data) {
		if (err) {
			return res.status(500).send('Server error')
		}
		var stu = JSON.parse(data).student
		res.render('index.html', {
			student:stu,
		
			firct:['苹果' ,'香蕉' , '鸭梨' , '橘子']
		})
	})
	
})

app.listen(3000 , function () {
	console.log('the server is running')
})
```



### 路由设计

| 请求方法 | 请求路径         | get 参数 | post 参数                      | 备注             |
| -------- | ---------------- | -------- | ------------------------------ | ---------------- |
| GET      | /studens         |          |                                | 渲染首页         |
| GET      | /students/new    |          |                                | 渲染添加学生页面 |
| POST     | /studens/new     |          | name、age、gender、hobbies     | 处理添加学生请求 |
| GET      | /students/edit   | id       |                                | 渲染编辑页面     |
| POST     | /studens/edit    |          | id、name、age、gender、hobbies | 处理编辑请求     |
| GET      | /students/delete | id       |                                | 处理删除请求     |

### 路由分离

在入口文件 `app.js` 把路由分离出去, 成单独的`js`文件, 在入口函数中引入 `var router = require('./router')`

并且把 路由容器挂载到 `App.js`服务中 `app.use(router)`



### 模块职责单一性

### 划分模块的目的

模块职责单一 , 增强项目代码的可维护性 , 和代码的可读性

### 入口模块职责

- 创建服务
- 做一些服务相关的配置
  - 模板引擎
  - bady-parser 解析表单 post请求体
  - 提供静态资源
- 挂载路由
- 设置监听端口,启动服务

### 路由模块职责

- 处理路由
- 根据不同请求方法+请求路径设置具体的请求处理函数

**在`Express`专门提供了专门包装路由的`API`**

**在路由文件 `router.js`导出路由容易的步骤 :** 

- 引入`var express = require('express)`
- 创建一个路由容器 

```js
var router = express.Router()
```

- 把路由都挂载到路由容器中

```js
router.get('/students' , function () {})
router.get('/students/new' , function () {})
```

- 导出路由容器

```js
modules.exports = router
```

- 在入口文件中引入路由文件`router.js`
- 把路由容器挂载到`app`服务中

```js
app.use(router)
```



### 路由模块代码

```js
var express = require('express')
var fs = require('fs')

// 1 创建一个路由容器
var router = express.Router()

// 2 把请求路径都挂载到路由容器中
router.get('/' , function (req, res) {
})

router.get('/students' , function (req , res) {
	res.render('index.html' ,{
		firct:['苹果' , '橘子' , '鸭梨']
	})
})

router.get('/students/new' , function (req , res) {
	res.render('new.html')
})

router.post('/students/new' , function (req , res) {	
	console.log(req.body)
})

router.get('/students/edit' , function (req , res) {	
})

router.post('/students/edit' , function (req , res) {	
})

router.get('/students/delete' , function (req , res) {	
})

// 3 把路由容器挂载到接口对象中
module.exports = router

```



### 异步操作API如何获取内部的数据

> 如果想要获取异步操作中的数据 , 返回值得方法行不通,  因为异步操作, return会先执行,不会等待异步操作完成, 想要获取异步操作的数据, 就必须通过回调函数

- 必须通过回调函数获取结果或者数据

![](images\获取异步API操作结果.png)



### 设计操作数据的API

封装增删改查的API文件 `student.js`

```js
/**
 * student.js
 * 数据操作文件模块
 * 职责：操作文件中的数据，只处理数据，不关心业务
 *
 * 这里才是我们学习 Node 的精华部分：奥义之所在
 * 封装异步 API
 */

var fs = require('fs')

var dbPath = './db.json'

/**
 * 获取学生列表
 * @param  {Function} callback 回调函数
 */
exports.find = function (callback) {
  fs.readFile(dbPath, 'utf8', function (err, data) {
    if (err) {
      return callback(err)
    }
    callback(null, JSON.parse(data).students)
  })
}

/**
 * 根据 id 获取学生信息对象
 * @param  {Number}   id       学生 id
 * @param  {Function} callback 回调函数
 */
exports.findById = function (id, callback) {
  fs.readFile(dbPath, 'utf8', function (err, data) {
    if (err) {
      return callback(err)
    }
    var students = JSON.parse(data).students
    var ret = students.find(function (item) {
      return item.id === parseInt(id)
    })
    callback(null, ret)
  })
}

/**
 * 添加保存学生
 * @param  {Object}   student  学生对象
 * @param  {Function} callback 回调函数
 */
exports.save = function (student, callback) {
  fs.readFile(dbPath, 'utf8', function (err, data) {
    if (err) {
      return callback(err)
    }
    var students = JSON.parse(data).students

    // 添加 id ，唯一不重复
    student.id = students[students.length - 1].id + 1

    // 把用户传递的对象保存到数组中
    students.push(student)

    // 把对象数据转换为字符串
    var fileData = JSON.stringify({
      students: students
    })

    // 把字符串保存到文件中
    fs.writeFile(dbPath, fileData, function (err) {
      if (err) {
        // 错误就是把错误对象传递给它
        return callback(err)
      }
      // 成功就没错，所以错误对象是 null
      callback(null)
    })
  })
}

/**
 * 更新学生
 */
exports.updateById = function (student, callback) {
  fs.readFile(dbPath, 'utf8', function (err, data) {
    if (err) {
      return callback(err)
    }
    var students = JSON.parse(data).students

    // 注意：这里记得把 id 统一转换为数字类型
    student.id = parseInt(student.id)

    // 你要修改谁，就需要把谁找出来
    // EcmaScript 6 中的一个数组方法：find
    // 需要接收一个函数作为参数
    // 当某个遍历项符合 item.id === student.id 条件的时候，find 会终止遍历，同时返回遍历项
    var stu = students.find(function (item) {
      return item.id === student.id
    })

    // 这种方式你就写死了，有 100 个难道就写 100 次吗？
    // stu.name = student.name
    // stu.age = student.age

    // 遍历拷贝对象
    for (var key in student) {
      stu[key] = student[key]
    }

    // 把对象数据转换为字符串
    var fileData = JSON.stringify({
      students: students
    })

    // 把字符串保存到文件中
    fs.writeFile(dbPath, fileData, function (err) {
      if (err) {
        // 错误就是把错误对象传递给它
        return callback(err)
      }
      // 成功就没错，所以错误对象是 null
      callback(null)
    })
  })
}

/**
 * 删除学生
 */
exports.deleteById = function (id, callback) {
  fs.readFile(dbPath, 'utf8', function (err, data) {
    if (err) {
      return callback(err)
    }
    var students = JSON.parse(data).students

    // findIndex 方法专门用来根据条件查找元素的下标
    var deleteId = students.findIndex(function (item) {
      return item.id === parseInt(id)
    })

    // 根据下标从数组中删除对应的学生对象
    students.splice(deleteId, 1)

    // 把对象数据转换为字符串
    var fileData = JSON.stringify({
      students: students
    })

    // 把字符串保存到文件中
    fs.writeFile(dbPath, fileData, function (err) {
      if (err) {
        // 错误就是把错误对象传递给它
        return callback(err)
      }
      // 成功就没错，所以错误对象是 null
      callback(null)
    })
  })
}

```



### 代码编写步骤

- 处理模板
- 配置静态资源
- 配置模板引擎
- 简单路由 : /students 渲染静态页面 
- 路由设计
- 提取路由模块
- 一些业务操作的需要处理的文件数据 , 封装student.js
- 可以先写好所有的操作的结构
  - 查询所有学生列表的`API`find
  - findById
  - save
  - updateById
  - deleteById
- 实现具体的功能
  - 通过路由	收到请求
  - 接受请求中的数据(get , post)
    - req.query
    - req.body
  - 调用数据操作的API处理数据
  - 根据造作结果发送响应给客户端
- 业务功能顺序
  - 列表
  - 添加
  - 编辑
  - 删除





# node 第五天



## 异步API

### 异步编程

JS中的的一步步API:

- 定时器
- 事件绑定
- ajax异步模式
- node中的文件操作(readFile,writeFile)

获取一个异步操作中的数据, 必须使用回调函数才能获取

```js
    function fn(x, y,callback) {
      setTimeout(function () {
        var data = x + y
        callback(data)
      }, 1000)

    }
    
    fn(10, 20, function (dt) {
      console.log(dt)
    })
```



## JavaScript中的模块化

Node中的模块化 `CommonJS`

- 浏览器中的模块化
  - AMD   require.js
  - CMD   sea.js
- ECMAScript 6 中增加了模块化支持 , 但是默认不支持, 需要特殊处理



## mongoDB

###关系型数据库和非关系型数据库

[Nosql菜鸟文档](https://www.runoob.com/mongodb/nosql.html ) : MongoDB 资料文档

表就是关系

或者说表语表之间存在关系

- 所有的关系型数据库都需要通过`sql`语言操作
- 所有关系型数据库咋操作之前都需要设计表结构
- 而且数据表还支持约束(保证数据的完整性)
  - 唯一的
  - 主键
  - 默认值
  - 非空
- 非关系型数据库非常灵活
- 有的非关系型型数据库就是存key-value
- 但是MongoDB长得最像关系型数据库的非关系型数据库
  - 数据库=====>数据库
  - 数据表 =====> 集合(  数组 )
  - 表记录====>( 文档对象 )
- **MongoDB不需要设计表结构**
- 也就是说没有结构一说

### MongoDB下载

[下载网站](https://www.mongodb.com/download-center/community )

- 需要配置环境变量

> 在 shell 中输入 services.msc 进入window的服务

### window中MongoDB的安装

在window中配置服务 [跟着网站指南走](https://www.runoob.com/mongodb/mongodb-window-install.html )

### 启动

mongodb 默认使用执行 mongod 命令默认下盘符根目录  /data/db  作为自己的数据存储目录

如果没有data目录 , 会启动不成功

所以在启动之前手动创建一个 data目录

```shell
$ mongod
```

如果想要修改默认的数据存储目录 :

```shell
$ mongod --dbpath=数据存储目录路径
```

### 停止服务

```shell
$  在开启服务的cmd  ctrl + C 
```



### 连接和退出数据库

连接 ====> 在新的cmd窗口执行命令

```shell
$ mongo  #默认连接本机的 mongodb 服务
```

退出 : 退出连接状态

```shell
$ exit
```



## 基本命令	

- `show dbs`  : 查看显示所有数据库
- `db` 
  - 查看当前操作的数据库
  - 默认会连接到`test`
- `use 数据库名称`
  -   切换到指定的数据库  , 如果没有会新建数据库
- 插入数据



## 在Node中如何操作MongoDB数据

### 官方提供的 `mongodb`包

[mongodb在github的原码](https://github.com/mongodb/node-mongodb-native  )  (官方提供: 开发一般不用)

### 使用第三方mongoose来操作数据库

第三方包 :基于`MongoDB`的mongodb进行了再一次封装

[第三方包的官网](https://mongoosejs.com/ )

### 使用指南 

- 新建一个文件 , 设置初始化package.json

```shell
$ npm init -y
```

- 下载`mongoose` 第三方包

```shell
$ npm i -S mongoose
```

- 新建文件 `demo.js`

```js
var mongoose = require('mongoose');

// 连接 MongoDB 数据库
mongoose.connect('mongodb://localhost/test', { useMongoClient: true });

mongoose.Promise = global.Promise;

// 创建一个模型
// 就是在设计数据库
// MongoDB 是动态的，非常灵活，只需要在代码中设计你的数据库就可以了
// mongoose 这个包就可以让你的设计编写过程变的非常的简单
var Cat = mongoose.model('Cat', { name: String });

// 实例化一个 Cat
  var kitty = new Cat({ name: '喵喵' + i });

  // 持久化保存 kitty 实例
  kitty.save(function (err) {
    if (err) {
      console.log(err);
    } else {
      console.log('meow');
    }
  });
```



## MongoDB概念理解

- 数据库
  - 一个mongodb数据库下面还可以有多个数据库
- 集合
  - 集合就是每个数据库中的每个数组(表)
- 文档
  - 每个集合中存储的必须是对象(表记录), 一个集合中可以存储多个记录

> mongodb就是最外层最大的对象 , 里面有多个数据库, 每一数据库中都存储中很多的集合(数组) , 集合中存储着许多的记录, 一个记录就是一条数据



```js
{================//mongodb数据库
    qq:{ =====================//mongodb中的一个数据库
        user:[=============================//qq数据库中的一个集合
            {name:"张三",age:17}=======================//user集合中的一条记录
            {name:"张三",age:17}
            {name:"张三",age:17}
        ],
         product:[ // ===================集合
               
            ]    
    },
    taobao :{
        
    }
    
    
}
```



## mongoose使用

第三方包 :基于`MongoDB`的mongodb进行了再一次封装

[第三方包的官网](https://mongoosejs.com/ )

- 1 引包

```js
var mongoose = require('mongoose')
```

- 2 连接数据库

```js
mongoose.connect('mongodb://localhost/itcast',{useNewUrlParser: true})
//{ useMongoClient: true }
```

- 3 创建一个 `schema` 架构

```js
var Schema = mongoose.Schema
```

- 4 设计集合结构 ( 表结构 )

```js
var userSchema = new Schema({
  username: {
    type: String,
    required: true // 必须有
  },
  password: {
    type: String,
    required: true
  },
  email: {
    type: String
  }
})
```

- 5 将文档结构发布为模型

> mongoose.model  方法就是用来将一个架构发布为 model
>
> 参数 1: 	    传入一个大写名词单数字符串用来表示你的数据库名称
>                    mongoose 会自动将大写名词的字符串生成 小写复数 的集合名称
>                    例如这里的 User 最终会变为 users 集合名称
>
> 参数 2 :    架构  useSchema
>
> 返回值 :  模型构造函数

```js
var User = mongoose.model('User', userSchema)
```

当我们有了模型构造函数 , 就可以对  `users`  集合中的数据进行为所欲为的操作了



### 增加数据

```js
 var admin = new User({
   username: 'zs',
   password: '123456',
   email: 'admin@admin.com'
 })

admin.save(function (err, ret) {
  if (err) {
    console.log('保存失败')
  } else {
    console.log('保存成功')
    console.log(ret)
  }
})
```



### 查询

查询所有 :  `User.find()`  ======> 返回一个数组

```js
User.find(function (err, ret) {
  if (err) {
    console.log('查询失败')
  } else {
    console.log(ret)
  }
})
```

按照条件查询所有 : ==========> 返回的是一个数组(集合 )

```js
User.find({
  username: 'zs'
}, function (err, ret) {
  if (err) {
    console.log('查询失败')
  } else {
    console.log(ret)
  }
})
```



查询单个 `findOne ()`   ======> 返回一个对象

```js
User.findOne({
  username: 'zs'
}, function (err, ret) {
  if (err) {
    console.log('查询失败')
  } else {
    console.log(ret)
  }
})
```

通过Id查询 `findById`

```js
	var id = req.query.id.replace(/"/g,'')
	Student.findById(id,function (err, student) {
		if (err) {
			return res.status(500).send('server err')
		}
		res.render('edit.html', {
			student:student
		})
	})
```



### 删除数据

- 根据条件删除所有

```js
User.remove({
  username: 'zs'
}, function (err, ret) {
  if (err) {
    console.log('删除失败')
  } else {
    console.log('删除成功')
    console.log(ret)
  }
})
```

- 根据条件删除一个

```js
Model.findOneAndRemove(条件 , [option] , [callback])
```

- 根据id 删除一个

```js
Model.findByIdAndRemove(条件, [option] , [callback])
```

### 更新数据

- 根据条件更新所有 

```js
Model.update(条件 , doc , [options] , [callback])
```

- 根据指定条件更新一个

```js
Model.findOneAndUpdate([options] , [update] , [options] , [callback])
```

- 根据ID 更新一个 ,

Model.findByIdAndUpdate()

> 参数一 : id值
>
> 参数二 : 修改的属性
>
> 参数三 :  回调函数

```js
User.findByIdAndUpdate('5d67c1c30fa96e3964a5cc94',{username:'哈哈'},function (err, ret) {
	if (err) {
		console.log('删除失败');
	}else {
		console.log('删除成功');
	}
})
```





## MySQL

### MySQL安装

- 1 官网下载 [mysql下载](https://dev.mysql.com/downloads/mysql/ )
- 2 解压到纯英文路径
  - 解压目录添加 my.ini （可选） 
  - 参考： http://www.cnblogs.com/Ray-xujianguo/p/3322455.html
  -  https://gist.github.com/hanjong/1205199
  -  https://dev.mysql.com/doc/refman/5.5/en/mysqld-option-tables.html 

```shell
[mysql]
# MySQL 安装目录
basedir=C:/Develop/mysql
# 数据文件所在目录
datadir=C:/Develop/mysql/data
```



- 3 以管理员身份运行 CMD 执行以下命令，安装一个 MySQL 服务 

```shell
# 定位到安装目录下的 bin 文件夹
$ cd <MySQL安装目录>/bin
# 初始化数据所需文件以及获取一个临时的访问密码  初始化的最后会给一个零时密码, 要保存住
$ mysqld ‐‐initialize ‐‐user=mysql ‐‐console
# 将 MySQL 安装为服务 可以指定服务名称
$ mysqld ‐‐install MySQL

```



- 4 登入 MySQL 服务器，重置密码 

```shell
# 先通过用户名密码进入 MySQL 操作环境
$ mysql ‐u root ‐p
Enter password: # 输入临时密码 =================>初始化时的密码
# 设置数据库访问密码，一定要加分号
mysql> set password for root@localhost = password('123456');
```



- 5 退出数据库

```shell
$ exit
```

- 6 登录数据库

```shell
$ mysql ‐u root ‐p
Enter password: 输入设置的密码
```



### MySQL命令行工具

- 通过命令行运行解压目录下 bin 目录中的 mysql.exe ： 

```shell
# 定位到 bin 目录
$ cd <解压目录>/bin
# 运行 mysql，‐u 指定数据库用户名，‐p 指定密码
$ mysql ‐u root ‐p wanglei
# 一般不建议在命令中填写密码，因为这样会暴露你的密码，一般只加一个 ‐p 但是不给值
$ mysql ‐u root ‐p
Enter password: # 这时会要求你输入密码
```

- 进入 MySQL 客户端的 REPL 环境过后，可以通过标准的 SQL 语句操作数据库。 

> 常见操作指令

```shell
$ mysql> show databases; ‐‐# 显示全部数据库
$ mysql> create database <db‐name>; ‐‐ # 创建一个指定名称的数据库
$ mysql> use <db‐name>; ‐‐#  使用一个数据库，相当于进入指定的数据库
$ mysql> show tables; ‐‐#  显示当前数据库中有哪些表
$ mysql> create table <table‐name> (id int, name varchar(20), age int); ‐‐ # 创建一个指定名称的数据表，并添加 3 个列

$ mysql> desc <table‐name>; ‐‐ # 查看指定表结构
$ mysql> source ./path/to/sql‐file.sql ‐‐ # 执行本地 SQL 文件中的 SQL 语句
$ mysql> drop table <table‐name>; ‐‐ # 删除一个指定名称的数据表
$ mysql> drop database <db‐name>; ‐‐ # 删除一个指定名称的数据库
$ mysql> exit|quit; ‐‐ # 退出数据库终端
```



### 可视化工具

> 如果需要复杂的操作，推荐 Navicat Premium 

> 下载地址：http://www.navicat.com.cn/download/navicat-premium 
>
> 这是一个付费软件，可以免费试用 14 天 



### 数据库的分类

#### 关系型数据库

以表格的实行存储数据

- mysql
- SQLserver

#### 非关系型数据库

以键值对的形式存储数据, 执行速率高

- mongodb
- redis
- BigTable



### 数据库中的术语

- 数据库 database
- 表table: 一个表对应一类数据, 比如学生表, 用户表
- 行`rows` : 一行信息, 又叫一条记录
- 列`columns` : 一列, 又叫一个字段



### 数据库增删改查

注释: `__ 注释内容 `

#### 查询

``` mysql
select * from stu

select 字段列表  from 表名 where 条件 
```

#### 添加

```mysql
# insert into 表名  (k1, k2, k3) values (v1, v2, v3)
insert into stu (name, age, sex) values('张三', 18, 'm')
# 简写 -- 必须和键一一对应, 才能省略
insert into stu  values(null, 'zs', 19, 'f')
```

#### 删除

```mysql
delete from 表名 where 条件

delete from stu where id = 8 # 根据条件删除
delete from stu  #全部删除
```

#### 修改

```mysql
update 表名 set k = v, k = v where 条件

update stu set name = '飞飞' ,  sex = 'f' where id = 8
```



#### mysql拓展

```mysql
相等和赋值 : = 
与: and
或: or
非: !

in语法:
select * from stu where id = 1, id = 3, id = 5 ...
#等价与
select * from stu where id in (1, 3, 5)

#模糊查询
like 语法
#查找所有姓小的人
select * from stu where name like '小%'
#查找包含大的人
select * from stu where name like '%大%'

#数据排序
order by 字段
#按age排序 , 默认是升序  desc: 降序
select * from stu order by age
select * from stu order by age desc
```





 

## Node操作MySQL数据库

### 安装

在npm官网直接所有`mysql`  针对于js操作的

```shell
#初始化
$ npm init -y
#安装
$ npm install --save  mysql
```

```shell
$ npm install mysqljs/mysql
```



### 引包和使用

```js
//引包
var mysql = require('mysql');

// 1. 创建连接
var connection = mysql.createConnection({
  host: 'localhost',
  user: 'root',
  password: 'root',
  database: 'users' // 对不起，我一不小心把数据库名字和表名起成一样的，你知道就行
});

// 2. 连接数据库 打开冰箱门
connection.connect();

// 3. 执行数据操作 把大象放到冰箱
connection.query('SELECT * FROM `users`', function (error, results, fields) {
  if (error) throw error;
  console.log('The solution is: ', results);
});

// connection.query('INSERT INTO users VALUES(NULL, "admin", "123456")', function (error, results, fields) {
//   if (error) throw error;
//   console.log('The solution is: ', results);
// });

// 4. 关闭连接 关闭冰箱门
connection.end();
```



## node 操作mysql数据库

### 下载库

能够操作mysql的第三方库, 去npm官网找mysql模块, 查询使用的api

```shell
$ npm i mysql
```

### 引入

```js
const mysql = require('mysql')
```



### 使用步骤

1. 准备账号信息

2. 创建数据库的连接

```js
const connection = mysql.createConnection({
  // 对象中放账号信息  
  host     : 'localhost',
  user     : 'root',
  password : 'root',
  database : 'my_db' //数据库的名字
});
```

3. 连接数据库

```js
connection.connect();
```

4. 操作数据库数据 `query`方法
   - 参数1: mysql语句
   - 操作的数据
   - 处理结果

删除

```js
let id = 4
//connection.query(`delete from stu where  id = ${id}`, null, (err, data) => {
//简写
connection.query('delete from stu where  id = ?', id, (err, data) => {    
    if (err) return console.log(err)
    console.log('删除成功')
})
```

查找

- 返回一个数组, 没有查找到,就返回空数组

```js
// ? 号后面是查找的数据, 数据不止一个,用数组表示
connection.query('select * from stu where age> ? and age < ?', [ 20, 100], (err, data) => {
    if (err) return console.log(err)
    console.log('data: ' , data)
})
```

添加

```js
let name = '张三'
let age = 18
let sex = 'f'
connection.query('insert into stu (name, age, sex) values(?, ?, ?)', [name, age, sex], (err, data) => {
    
})

//简写
connection.query('insert into stu set ?', {name: '翠花', age: 18, sex:'f'}, (err, data) => {
   if (err) return console.log(err)
    console.log('data' ,data)
})
```

修改

```js
connection.query('update stu set name = ?, age = ?, where id = ? ', ['翠花', 18, 10], (err, data) => {
    if (err) return throw err
    
})

//简写
connection.query('update stu set ? where id = ?', [{name: '马冬梅', sex: 'f'}, 10])
```





5. 断开和数据库的连接

```js
connection.end();
```



## 封装操作数据库

```js

//引入
const mysql = require('mysql')

//准备账号信息
const obj = {
  // 对象中放账号信息  
  host     : 'localhost',
  user     : 'root',
  password : 'root',
  database : 'my_db' //数据库的名字
}

//
const connect =  mysql.createConnection(obj)
```





## 登录状态保持(登录拦截)

在用户访问所有的页面时, 都需要判断用户是否登录过, 只有登录才能访问

### http协议是无记忆, 无状态的

早期浏览器只提供浏览功能, 访问者是谁不重要, 所以不需要cookie和session来记录用户的登录信息



### express-session

下载, 引包

```shell
$ npm i express-session
const session = require('express-session')
```

配置

```js
app.use(session({
    //传递加密字符串: 用户传递加密标识
    secrect: 'itcast ' ,
    name: 'session-user' //指定session的name值	
}))
```



**登录拦截使用**

- 在登录成功时, 加标记`req.session.isLogin = true`
- 在每一次请求时, 在路由中间件前面加一个中间件, 判断是否有`req.session.isLogin` 属性, 有则`next()` 
- 无则, 强行跳转到登录页

```js
  db('select * from user where username = ? and password = ?', [username, password], (data)=> {
    //说明匹配
    if (data.length > 0) {
      //记录session
      req.session.isLogin = true
      //跳转主页
      res.redirect('/')
    } else {
      //跳转
      res.redirect('/login')
    }
  })
```









## Promise

### 回调地狱( callback hell )

异步读取文件的顺序取决于文件的大小, 无法保证顺序

通过回调嵌套的方式能够保证执行顺序

```js
var fs = require('fs')

fs.readFile('./data/a.txt', 'utf8', function (err, data) {
  if (err) {
    // return console.log('读取失败')
    // 抛出异常
    //    1. 阻止程序的执行
    //    2. 把错误消息打印到控制台
    throw err
  }
  console.log(data)
  fs.readFile('./data/b.txt', 'utf8', function (err, data) {
    if (err) {
      // return console.log('读取失败')
      // 抛出异常
      //    1. 阻止程序的执行
      //    2. 把错误消息打印到控制台
      throw err
    }
    console.log(data)
    fs.readFile('./data/c.txt', 'utf8', function (err, data) {
      if (err) {
        // return console.log('读取失败')
        // 抛出异常
        //    1. 阻止程序的执行
        //    2. 把错误消息打印到控制台
        throw err
      }
      console.log(data)
    })
  })
})

```



### Promise语法

在EcmaScript 6 中新增了一个`API`  **promise构造函数** , 是一个:  存放一个异步任务的一个容器

promise : 意思是 承诺,保证的意思

![](images\promise.png)

#### 使用场景

promise 本身不是异步的 , 但是内部往往都是封装异步任务

能够解决回调嵌套问题

```js
var fs = require('fs')

//Promise一旦创建就会立即执行里面的代码
var p1 = new Promise(function (resolve, reject) {
  fs.readFile('./data/a.txt', 'utf8', function (err, data) {
    if (err) {
      //如果失败了, 就把Pending的状态改为 reject  
      reject(err)
    } else {
        //如果成功了,就把pending的状态改为 reslove
      resolve(data)
    }
  })
})

//p1就是那个承诺
//then 就是 当 p1成功, 然后(then) 执行相应的操作
//then方法接受两个函数参数 , 分别是resolve 和 reject
p1
  .then(function (data) {
    console.log(data)
    // 当 p1 读取成功的时候
    // 真正有用的是：我们可以 return 一个 Promise 对象
    // 当 return 一个 Promise 对象的时候，后续的 then 中的 方法的第一个参数会作为 p2 的 resolve
    // 
    return p2
  }, function (err) {
    console.log('读取文件失败了', err)
  })
  .then(function (data) {
    console.log(data)
    return p3
  })
  .then(function (data) {
    console.log(data)
    console.log('end')
  })



var p2 = new Promise(function (resolve, reject) {
  fs.readFile('./data/b.txt', 'utf8', function (err, data) {
    if (err) {
      reject(err)
    } else {
      resolve(data)
    }
  })
})

var p3 = new Promise(function (resolve, reject) {
  fs.readFile('./data/c.txt', 'utf8', function (err, data) {
    if (err) {
      reject(err)
    } else {
      resolve(data)
    }
  })
})
```



**then方法**

![](images\then.png)



### 封装promise

```js
var fs = require('fs')

function pReadFile(filePath) {
  return new Promise(function (resolve, reject) {
    fs.readFile(filePath, 'utf8', function (err, data) {
      if (err) {
        reject(err)
      } else {
        resolve(data)
      }
    })
  })
}

pReadFile('./data/a.txt')
  .then(function (data) {
    console.log(data)
    return pReadFile('./data/b.txt')
  })
  .then(function (data) {
    console.log(data)
    return pReadFile('./data/c.txt')
  })
  .then(function (data) {
    console.log(data)
  })

```



### 关于promise的使用

阮一峰关于es6的讲解 : [ECMAScript 6 入门](http://es6.ruanyifeng.com/ )

> promise章节的讲解 [promise](http://es6.ruanyifeng.com/#docs/promise )





# nodejs 第六天



## path核心模块

专门用来操作路径的核心模块

path模块查阅文档 [nodeJs官网path模块](https://nodejs.org/dist/latest-v12.x/docs/api/path.html )

**path.basename( path, [ext] )**

> 获取一个给定文件路径的文件名部分
>
> 参数一 : 文件路径
>
> \[ 参数二 ]: 文件后缀名, 把文件后缀名截取, 输出文件名,不包含后缀名 

**path.dirname(  path )**

> 获取给定文件路径的目录部分 , 不包括文件

**path.extname( path )**

> 获取文件路径的文件后缀名 

**path.isAbsolute(path)**

> 判断一个路径是不是解决路径
>
> 返回布尔类型

**path.parse(path)**  最强大

> 会一个路径解析成一个对象, 是上面方法的一个总结
>
> 返回一个对象 
>
> path :   ' c:/a/b/index.html '
>
> {	
>
> ​	root : ' c:/ '       	根路径
>
> ​	dir : 'c:/a/b/'		目录
>
> ​	base : 'index.html' 包含后缀名的文件名 	
>
> ​	ext: '.html'  		  文件后缀名
>
> ​	name : 'index'  	   不包含后缀名的文件名
>
> }

**path.join([....paths])**

> 能够将多个路径拼接成一个路径, 在window会自动加 `\ ` 
>
> 解决手动拼接路径失误的问题, 能够根据操作系统,自动添加转义符 `\`

**window系统的路径:  以`\` 分割, 在js中 `\` 是转义符** 

**Linux , max os  系统的 路径是`/`  正斜杠 表示**



## node中的其他成员

**`__dirname`   和  `__filename`**

在每一个模块中,除了`require` ,`exports` 等模块相关的API之外,还有两个特殊的成员

- `__dirname`  : 可以**动态**来获取当前文件模块所属**目录**的绝对路径===> 目录(不包含文件名)
- `__filename` : 可以**动态**来获取当前文件的绝对路径=============>路径(包含文件名)

在node中, 文件操作的相对路径是不可靠的, 是相对于执行当前node命令的所处的终端的路径

为了解决这个问题, 只需要把相对路径变为绝对路径:

​	就需要使用	`	__dirname` 或者`__filename` 解决这个问题

在拼接过程中,为了避免手动拼接失误,通常个`path.join()` 辅助拼接



### 模块的相对路径和文件操作中的相对路径

模块中的路径标识就是相对于当前文件,不受执行node命令的路径影响

文件操作中的相对路径受node命令执行的路径的影响



## 知名模板引擎

- `ejs`
- `jade(pug)`
- `handlebars`
- `nunjucks`



## 密码加密第三方包

blueimp [md5加密](https://github.com/blueimp/JavaScript-MD5 )

下载

```shell
$ npm i blueipm-md5
```

引包

```js
var md5 = require('blueimp-md5')
```



## 服务端重定向对异步请求无效

服务端重定向对于异步请求无效, 只针对于同步请求才有效 

需要重定向, 在客服端自己



## express中的json()

在 res.send给客服端回复请求的时候, 往往想发送一个json格式的数据, express就提供了一个API能够返回一个json数据, 客户端就可以拿到这个json数据,



## 在express配置使用session

session默认是内存存储的,服务器一旦重启, 数据就会丢失, 真正的成产环境, 会把session持久化存储

express没有session, 可以引用第三方包

```shell
$ npm i express-session
```

引包

```js
var session = require('express-session')
```

配置session

```js
//该插件会默认为req请求对象添加一个成员:req.session 也就一个对象
app.use(session({
  // 配置加密字符串，它会在原有加密基础之上和这个字符串拼起来去加密
  // 目的是为了增加安全性，防止客户端恶意伪造
  secret: 'itcast',
  resave: false,
  saveUninitialized: false // 无论你是否使用 Session ，我都默认直接给你分配一把钥匙
}))
```

使用

```js
//添加数据
req.session.user = 'bar'

//获取数据
req.session.user
```

销毁session

```js
#不严谨的写法, session的成员没销毁
req.session = null

#严谨的写法
delete req.session.xxx
```





# Node第七天



### 什么是中间件

**本质就是请求处理方法 , 本质就是一个函数**

在我们引入第三方插件的时候 , 请求对象`req`  就多了相应的成员方法

`body-parser`  `express-session`  `md5` 等等



### 中间件 (middleware) 

当在主程序`app.js`  加载 `body-parser`  `express-session`  等中间件插件时, 在下面挂载路由, 在解析路由的时候, `req.body`  `req.session`  就存在了, 才能够使用

**说白了, 可以给req, res 拓展功能**



当请求进来，会从第一个中间件开始进行匹配  , 如果匹配，则进来如果请求进入中间件之后，没有调用 next 则代码会停在当前中间件 , 如 果调用了 next 则继续向后找到第一个匹配的中间件



### 应用程序级别中间件

#### 不关心请求路径的中间件

**万能匹配**

>  不关心请求路径和请求方法的中间件
>
>  也就是说任何请求都会进入这个中间件

- 中间件本身是一个方法，该方法接收三个参数：
  + Request 请求对象
  + Response 响应对象
  +  next     下一个中间件

> 如果不匹配，则继续判断匹配下一个中间件

```js
app.use(function (req, res, next) {
  console.log('1')
  # 此处有两个选择, 要不next(), 传给下一个中间件, 要不res.send() 终止响应	  
  next()
})
```



#### 关心请求路径的中间件

**路径匹配**  **不严格匹配, 以他开头即可**

当有不关心路径的中间件, 必须使用`next()` 释放出控制权 , 才会进入下一个中间件, 

关心路径的中间件, 根据匹配条件, 进入匹配项 , 进入中间件之后, 如果没有 `next()` 释放控制权 , 后面的中间件依旧无法加载



```js
app.use('/a', function (req, res, next) {
  console.log('a')
  next()
})
```



### 路由级别中间件

**严格匹配的中间件**

`app.get`  `app.post` 等必须是 `/a` 或者 `/` 才能匹配



当调用 next 的时候，如果传递了参数，则直接往后找到带有 四个参数的应用程序级别中间件

