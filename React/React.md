# React 第一天

## React简介

+ React 起源于 Facebook 的内部项目，因为该公司对市场上所有 JavaScript MVC 框架，都不满意，就决定自己写一套，用来架设 Instagram（照片交友） 的网站。做出来以后，发现这套东西很好用，**就在2013年5月开源了**。
+ Angular1 2009 年  谷歌    MVC  不支持 组件化开发
+ 由于 React 的**设计思想极其独特**，属于革命性创新，性能出众，代码逻辑却非常简单。所以，越来越多的人开始关注和使用，认为它可能是将来 Web 开发的主流工具。
+ 清楚两个概念：
  + library（库）：小而巧的库，只提供了特定的API；优点就是 船小好掉头，可以很方便的从一个库切换到另外的库；但是代码几乎不会改变；
  + Framework（框架）：大而全的是框架；框架提供了一整套的解决方案；所以，如果在项目中间，想切换到另外的框架，是比较困难的；



## React的特点

- 声明式
  - React负责渲染UI, 并在数据变化的时候, 更新UI
- 基于组件
- 学习一次,随处使用
  - 使用React可以开发web应用
  - 使用react可以开发移动端混合应用(react-native)
  - 使用React可以开发VR (虚拟现实) 应用(react 360)

## React与vue的对比

### 组件化方面

1. **什么是模块化：**是从**代码**的角度来进行分析的；把一些可复用的代码，抽离为单个的模块；便于项目的维护和开发；
2. **什么是组件化：** 是从 **UI 界面**的角度 来进行分析的；把一些可服用的UI元素，抽离为单独的组件；便于项目的维护和开发；
3. **组件化的好处：**随着项目规模的增大，手里的组件越来越多；很方便就能把现有的组件，拼接为一个完整的页面；
4. **Vue是如何实现组件化的：** 通过 `.vue` 文件，来创建对应的组件；
   + template  结构
   + script        行为
   + style           样式


5. **React如何实现组件化**：大家注意，React中有组件化的概念，但是，并没有像vue这样的组件模板文件；React中，一切都是以JS来表现的；因此要学习React，JS要合格；ES6 和 ES7 （async  和 await） 要会用；

### 开发团队方面

+ React是由FaceBook前端官方团队进行维护和更新的；因此，React的维护开发团队，技术实力比较雄厚；
+ Vue：第一版，主要是有作者 尤雨溪 专门进行维护的，当 Vue更新到 2.x 版本后，也有了一个以 尤雨溪 为主导的开源小团队，进行相关的开发和维护

### 社区方面

+ 在社区方面，React由于诞生的较早，所以社区比较强大，一些常见的问题、坑、最优解决方案，文档、博客在社区中都是可以很方便就能找到的；
+ Vue是近两年才火起来的，所以，它的社区相对于React来说，要小一些，可能有的一些坑，没人踩过；

### 移动APP开发体验方面

+ Vue，结合 Weex 这门技术，提供了 迁移到 移动端App开发的体验（Weex，目前只是一个 小的玩具， 并没有很成功的 大案例；）
+ React，结合 ReactNative，也提供了无缝迁移到 移动App的开发体验（RN用的最多，也是最火最流行的）；



> 精辟总结:  vue 的生态更官方化, react的生态更社区化



## React 的使用

### react普通html使用

1. 安装

- react: 核心包, 创建react元素, 创建react组件
- react-dom: 渲染react元素/react组件

```shell
yarn add react react-dom
```

2. 引入

```html
// 会暴露两个全局变量 React , ReactDOM
<script src="./node_modules/react/umd/react.development.js"></script>
<script src="./node_modules/react-dom/umd/react-dom.development.js"></script>
```

3. 创建react元素
   - 参数1:  元素名称/标签名
   - 参数2:  元素的属性 `{}`, 无属性给`null`
   - 参数3:   文本子节点或者 dom子节点

```js

// react 创建元素
let el = React.createElement(
    'div', 
    {
    titel: '嘻嘻'
    },
    'hello React'
)
```

4. 渲染

```js
<div id="app"></div>

// ReactDOM 渲染react元素
渲染
参数1: 要渲染的内容 react元素 / react组件
参数2: 容器
ReactDOM.render(el, document.getElementById('app'))
```



### 模块化基本使用

1. 运行 `cnpm i react react-dom -S` 安装包

   + react： 专门用于创建组件和虚拟DOM的，同时组件的生命周期都在这个包中
   + react-dom： 专门进行DOM操作的，最主要的应用场景，就是`ReactDOM.render()`

2. 在`index.html`页面中，创建容器：

   ```html
   <!-- 容器，将来，使用 React 创建的虚拟DOM元素，都会被渲染到这个指定的容器中 -->
   <div id="app"></div>
   ```

3. 导入 包：**定义的接收变量必须这么写**

   ```js
   //创建组件, 虚拟DOM元素, 生命周期
   import React from 'react'
   //那创建的虚拟DOM, 组件放到页面上展示
   import ReactDOM from 'react-dom'
   ```

4. 创建虚拟DOM元素：

   ```jsx
   // 这是 创建虚拟DOM元素的 API    <h1 title="啊，五环" id="myh1">你比四环多一环</h1>
   //  第一个参数： 字符串类型的参数，表示要创建的标签的名称
   //  第二个参数：对象类型的参数， 表示 创建的元素的属性节点
   //  第三个参数： 文本子节点或者 dom子节点
   //  参数 n   :  其他子节点 	
   const myh1 = React.createElement('h1', { title: '啊，五环', id: 'myh1' }, '你比四环多一环')
   ```


5. 渲染：

   ```js
   // 3. 渲染虚拟DOM元素
   // 参数1： 表示要渲染的虚拟DOM对象
   // 参数2： 指定容器,注意：这里不能直接放 容器元素的Id字符串，需要放一个容器的DOM对象
   ReactDOM.render(myh1, document.getElementById('app'))
   ```









## React的使用

### 基本使用

1. 运行 `cnpm i react react-dom -S` 安装包

   + react： 专门用于创建组件和虚拟DOM的，同时组件的生命周期都在这个包中
   + react-dom： 专门进行DOM操作的，最主要的应用场景，就是`ReactDOM.render()`

2. 在`index.html`页面中，创建容器：

   ```html
   <!-- 容器，将来，使用 React 创建的虚拟DOM元素，都会被渲染到这个指定的容器中 -->
   <div id="app"></div>
   ```

3. 导入 包：**定义的接收变量必须这么写**

   ```js
   //创建组件, 虚拟DOM元素, 生命周期
   import React from 'react'
   //那创建的虚拟DOM, 组件放到页面上展示
   import ReactDOM from 'react-dom'
   ```

4. 创建虚拟DOM元素：

   ```jsx
   // 这是 创建虚拟DOM元素的 API    <h1 title="啊，五环" id="myh1">你比四环多一环</h1>
   //  第一个参数： 字符串类型的参数，表示要创建的标签的名称
   //  第二个参数：对象类型的参数， 表示 创建的元素的属性节点
   //  第三个参数： 文本子节点或者 dom子节点
   //  参数 n   :  其他子节点 	
   const myh1 = React.createElement('h1', { title: '啊，五环', id: 'myh1' }, '你比四环多一环')
   ```


5. 渲染：

   ```js
   // 3. 渲染虚拟DOM元素
   // 参数1： 表示要渲染的虚拟DOM对象
   // 参数2： 指定容器,注意：这里不能直接放 容器元素的Id字符串，需要放一个容器的DOM对象
   ReactDOM.render(myh1, document.getElementById('app'))
   ```




### 在js中实现DOM元素嵌套

```js
//创建组件, 虚拟DOM元素, 生命周期
import React from 'react'
//那创建的虚拟DOM, 组件放到页面上展示
import ReactDOM from 'react-dom'

//2-创建虚拟DOM
const h1 = React.createElement('h1', {titel: '这是我的第一个react虚拟DOM'}, '这是一个h1')

// 从第三个参数开始, 都算做div的子节点, 包含文本节点
const div = React.createElement('div', null, '这是一个父盒子',h1)

//3-渲染到页面中
ReactDOM.render(div, document.querySelector('#app'))
```



## webpack 4.X

webpack是基于node构建的, 支持所有的 Node API 和语法

1. 运行`yarn init -y` 初始化项目
2. 在项目根目录下创建`src` 源代码目录和 `dist` 产品目录
3. 在`src` 下新建一个`index.html` 和 `index.js` 入口文件
4. `yarn add webpack webpack-cli -D`

5. **注意:** 在webpack 4.x中 有一个很大的特性, 就是约定大于配置, 约定  默认的打包入口文件路径是 src -> index.js
   - 目的就是尽量减少配置文件的体积
   - 打包入口文件时`index.js` 
   - 打包的输出文件时`dist/main.js`
   - 新增`mode` 配置选项必须配置:`production 和 development`



### module.exports 和 export default

都是向外导出模块的API , 但是在webpack.config.js配置文件中不支持`export default {}` 

- `export default {}` 是ES6 的新语法 , node都不支持

> *chrome支持的ES6+新特性, node就支持, 因为node用的是chrome的V8引擎*
>
> chrome 不支持 export default



## webpack-dev-server

每一次修改代码都需要重新打包, webpack-dev-server能够自动打包, 并在项目的根目录的内存中生成一个`main.js` , 把main.js托管到内存中

一些常见配置:

- --open 自动打开浏览器

- --open firefox 指定打开的浏览器

- --port 3000 指定端口

- --hot 热更新

- --progress 打包进度

- --compress 在走网络的时候进行压缩

- --host 能够指定域名

  

## html-webpack-plugin

html-webpack-plugin 能够在网站根目录中根据提供的模板自动生成一个`index.html` 并且自动引入`main.js`

会将生成的`index.html` 在内存中生成并在内存中托管到内存中

***在内存中生成index.html并托管到网站根目录, 自动引入打包好的main.js***

**配置**

```js
const htmlWebpackPlugin = require('html-webpack-plugin')
const path = require('path')

const htmlWebpack = new htmlWebpackPlugin({
  template: path.resolve(__dirname, 'src/index.html'),
  filename: 'index.html'
})

module.exports = {
  mode: 'production',
  plugins:[ 
    htmlWebpack
  ]
}
```



## React 脚手架

### 安装脚手架

1. 使用`npm`

``` js
第一种 使用npm 全局安装
$ npm i create-react-app -g

查看版本号
$ create-react-app -V

初始化项目
$ create-react-app react-demo 
```

2. npx  `官网推荐`

`npx` 一条命令, 实现了两个动作, 安装脚手架 + 初始化项目

能够保证全局只有一个 脚手架

```js
$ npx create-react-app 项目名
```

### 创建一个项目

```js
npx create-react-app react-demo
```

### 运行项目

```js
yarn start
```



### 项目目录

- `src/`
  - `index.js` 入口文件
- `public/`
  - `index.html` 入口页面, 项目启动首先访问`index.html` 入口页面中去引入`index.js` 入口文件



## JSX语法

### 配置jsx语法babel

+ 安装 `babel` 插件

  - 运行`cnpm i babel-core babel-loader babel-plugin-transform-runtime -D`
  - 运行`cnpm i babel-preset-env babel-preset-stage-0 -D`

+ 安装能够识别转换jsx语法的包 `babel-preset-react` 

  + 运行`cnpm i babel-preset-react -D`

+ 添加 `.babelrc` 配置文件

  ```json
  {
    "presets": ["env", "stage-0", "react"],
    "plugins": ["transform-runtime"]
  }
  ```

+ 添加babel-loader配置项：

  ```js
  module: { //要打包的第三方模块
      rules: [
        { test: /\.js|jsx$/, use: 'babel-loader', exclude: /node_modules/ }
      ]
  }
  ```

  

#### babel 6 的配置方法

安装loader

```js
yarn add babel-core babel-loader@7 babel-plugin-transform-runtime -D
yarn add babel-preset-env babel-preset-stage-0 -D
yarn add babel-preset-react -D
```

添加 `.babelrc` 配置文件

```json
{
  "presets": ["env", "stage-0", "react"],
  "plugins": ["transform-runtime"]
}
```

添加babel-loader配置项：

```js
module: { //要打包的第三方模块
    rules: [
      { test: /\.js|jsx$/, use: 'babel-loader', exclude: /node_modules/ }
    ]
}
```



#### babel 7 配置方法

安装loader   ------------> 不可行

```shell
#babel 插件
$ yarn add @babel/core babel-loader @babel/plugin-transform-runtime -D
$ yarn add @babel/preset-env @babel/preset-stage-0 -D	

#语法插件
$ yarn add @babel/preset-react -D

#执行命令
$ cnpm i @babel/plugin-proposal-class-properties -D
$ cnpm i @babel/runtime -D
```

添加 `.babelrc` 配置文件

```json
{
  "presets": ["@babel/preset-env","@babel/preset-react", "@babel/preset-stage-0"],
  "plugins": ["@babel/plugin-transform-runtime","@babel/plugin-proposal-class-properties"]	
}
```

添加babel-loader配置项：

```js
module: { //要打包的第三方模块
    rules: [
      { test: /\.js|jsx$/, use: 'babel-loader', exclude: /node_modules/ }
    ]
}
```



### 什么是jsx语法

是一个javascript 的一个语法扩展

> 就是符合 xml 规范 的 js 语法;  ( 语法格式相对来说,要比html严谨的多 )

对于构造UI结构来说, html是最为合适不过的标记语言了

但是在JS文件中不能写 html 语言  ,  但是可以使用 babel 来转换 这些 JS 中的 html 标签

> 作用: 可以在js中写 html

**jsx语法的本质: 在运行的时候, 最终还是被babel转换成了 React.createElement 形式生成的, 语法糖**



### jsx语法

- jsx 只允许一个跟标签和`vue` 中的 `template` 一样 , 也可以使用空标签`<></>`包裹
- jsx 里面的代码结构比较复杂的时候, 推荐使用在外面`()`包裹起来, 把内容当成一个整体 



### jsx中嵌入表达式

- 当我们在jsx控制的区域内, 使用js变量,或者表达式, 则需要写在`{  }` 中, 类似vue中的插值表达式`{{  }}`
- `{}` 插值中可以放(表达式)
  - 运算
  - 三元表达式
  - 函数调用
- `{}` 不可以放语句
  - if 语句 for 语句 等等
- 语句和 表达式的区别
  - 表达式都有返回值, 语句没有返回值

```jsx
let a = 10
const div = <div>这是一个div { a + 2 } </div>
```



- 在vue 中标签的属性赋值需要使用`v-bind`不能使用`{{}}` , 在react 可以在属性中使用插值表达式`{}`

```js
const h1 = <h1 title={ title }>哈哈哈 </h1>
```





- jsx中使用 布尔值, 字符串变量, 数组

```js
import React from 'react'
import ReactDOM from 'react-dom'

//把数组里的字符串变成一个h3标签放入到页面中
const nameArr = ['小傻子', '大傻子', '皮皮虾']

const nameObj = {
  name: '小傻子',
  age: 18
}
const flag = true

const arr = [
  <div>这一个数组</div>,
  <div>这一个数组</div>
]

const div = <div>
  {/* 渲染一个布尔值 */}
  { flag ? 'true' : 'false' }

  {/* 渲染数组每一项 */}
  { nameArr.map(item => <h3>{ item }</h3>) }
  <hr />
  {/* { nameArr } */}
  <h1  title={nameObj.age}>{ nameObj.name } </h1>

  <hr />
  { arr }

</div>

ReactDOM.render(div, document.querySelector('#app'))
```



### jsx中的注释

```jsx
{/*  这是jsx的注释 */}
{
  //这样写注释也可以
}
```



### jsx中为元素添加class , for

在jsx环境中为元素添加class但是不能使用 class , 需要使用`className` 代替`class`

> *因为class是js的关键字*
>
> label 标签的 for 应该用htmlFor 代替



### jsx中的label的for属性

`for` 也是js中的关键字, 所以在jsx中也不能使用, 需要用`htmlFor` 替代

### jsx创建DOM

在jsx创建DOM的时候,所有的节点 必须有唯一的根元素包裹, 类似vue中的`template`

```jsx
  <p className="jsx">这是jsx中的元素</p>
  <label htmlFor="#label">这是jsx中的label</label>
```





## 虚拟DOM

### 真实DOM的解析流程

#### **DOM数据来源?**

>  也就是我们在浏览器地址栏输入域名点击回车, 都发生了什么事?

![](E:/Vue/image/敲回车做的事情.png)

1. 浏览器会解析域名, 会先从本地的host文件中查看有没有域名对应的IP 地址, 有则对这个IP发起http请求

没有则向DNS服务器发送请求, 获得域名对应的IP地址, 对这个IP发起http请求

2. 服务器收到请求, 会这个处理请求, 把响应结果给客户端浏览器
3. 浏览器拿到响应, 进行处理



#### **浏览器的渲染过程**

我们能够得到服务器响应的一个html页面的字符串, 前后端交互的本质也就是字符串交互, 客户端发请求, 后台服务器响应

当然ajax请求, 前端能够得到json数据格式, 但是这些数据最终还是要渲染到html页面上, 也就是说我们第一次请求请求一个网站, 服务器必定会响应一个html字符串

浏览器拿到html页面的字符串, 进行解析, 遇到 link, a, script等会发起二次请求

浏览器为了效率不会等待服务器的响应会继续向下解析

![](image/真实DOM树.png)

当css等文件回来之后, 会在内存中同步解析css代码, 会形成一个 style rules => css tree

解析 html 会得到一个 DOM tree

浏览器最终会把`css tree `和 `DOM tree` 关联起来形成一个 `render tree` , 然后绘制到页面上



#### JS操作真实DOM的代价

用原生的JS或者`jquery`操作DOM代价较大, 举个栗子, 我们在电商全端的时候, 做过最多的一件事就是发送ajax, 拿到数据把数据重新渲染到页面上

带来的问题?

可能我们的一个操作, 只是改变了这个结构中很少的一部分, 对于大部分结构都是未改变的, 但是浏览器会把之前的内容全部干掉, 重新渲染DOM结构, 系统开销很大



**这个时候虚拟DOM应景而生**

### 虚拟DOM

在vue中和react中都提到了虚拟DOM, 只是在vue中我们很少关注虚拟DOM, 虚拟DOM是随着react的诞生而诞生

但是了解了虚拟DOM的原理,能够帮助我们很好的了解MVVM框架实现一些功能的底层原理



 虚拟DOM就是为了**解决浏览器性能问题**而被设计出来的 , 比如,  若一次操作中有10次更新DOM的动作，虚拟DOM不会立即操作DOM ,  而是将这10次更新的diff内容保存到本地一个JS对象中，最终将这个JS对象一次性attch到DOM树上，再进行后续操作，避免大量无谓的计算量 

**那么这就能解释为什么vue中 DOM的更新是异步的了** 避免了我们我们短时间内操作多次DOM, 带来的性能消耗



#### 什么是虚拟DOM

**我的理解: 虚拟DOM就是我们程序员用JS的对象模拟页面中的真实DOM结构和DOM嵌套**

![](image/虚拟DOM对比真实DOM.png)



**带来的好处: 按需更新**

当我们操作DOM时,可以全部映射到虚拟DOM上, 我们能够手动的模拟新旧两颗DOM树, 进行diff对比, 实现高效更新



#### 虚拟DOM的本质和目的

本质: 用JS对象, 来模拟真实DOM元素的嵌套关系

目的:  实现页面元素的高效更新

> jsx => 虚拟DOM => 真实DOM

jsx数据发生变化之后

> 产生新虚拟DOM树 => 新旧DOM树diff对比  => 找到差异的



## Diff算法

> diff => different 差异, 不同

React中的两种假定

- 两个不同类型的元素, 会产生不同虚拟DOM树

### tree diff

两个新旧DOM树,  逐层对比的过程就是`tree diff`,  当整颗DOM逐层对比完毕, 则需要按需更新的元素, 必然能够找到

### component diff

在进行Tree Diff 的时候, 每一层中, 都有不同的组件, (头部组件, 轮播图组件等等) 组件级别的对比, 叫做**Component Diff**

- 如果对比前后, 组价类型相同, 则暂时认为次组件不需要被更新
- 如果对比前后, 组件类型不同, 则需要移除旧组件, 并追加到页面上

### element diff

在进行组件对比的时候, 如果两个组件类型相同, 则需要进行元素级别的对比

![](image/diff.png)

## 三大框架的更新机制: 面试题

angular

- 脏检查机制
- vue 模仿angular , 双向数据绑定, 指令

react

- 虚拟DOM更新机制

- jsx => 虚拟DOM => 真实DOM
- 数据发生变化 => 产生新虚拟DOM树 => 通过diff 比对 新旧虚拟DOM => 修改差异的地方 

Vue

- 细粒度更新 : 一个数据对应一个`Watcher`
  - data( name )数据 => observer( defineReactive  数据响应式 ( defineProperty 数据劫持 ) ) => data数据 具有`getter setter`
  - 当数据`name`被使用的时候 => getter =>  Watcher(name) 把数据记录到  => Dep 依赖` []`
  - 当数据`name`被修改的时候 => setter  => 遍历Dep => 找到对应的Watcher => 通知外界 => 让外界更新页面
- 中等粒度更新: 一个组件对应一个`Watcher`
  - `name` 数据发生变化 => Watcher => 组件 => 虚拟DOM
    - 一个组件 对应一个 Watcher 对应一个 虚拟DOM树
  - vue中的`template`  => render => 虚拟DOM







# React 第二天

## React中创建函数组件

### 函数组件

一个构造函数就是一个组件, 但是组件必须有return , 如果组件内容为空`return null`

1. **创建组件, 一个构造函数就是一个组件(组件首字母必须大写)**
2. **以标签形式引入组件, 并且可以传值, 在构造函数中接收, 标签可以是单标签可以是双标签**
- 配合`ES6` 中的展开运算符传参
   - `props` 是只读的, 不管是简单数据类型, 还是复杂数据类型, 都不允许修改
- 在vue中 对于复杂数据类型的props能够修改
3. 函数组价内部一定要有`return` 返回值

   - 如果没有渲染内容: `return null`
   - 有内容`return JSX模板`
4. JSX的注意点:
   - 只能有一个根节点
   - 如果结构复杂, 外面用`()` 包起来

**组件传参**

- 传值可以在组件标签上直接传参 `name={传递的参数}`
- 在函数组件上, 直接通过`props` 接收外界传来的参数  

```jsx
import React from 'react'
import ReactDOM from 'react-dom'

const dog = {
  name: '小黑',
  age: 3,
  gender: '雌'
}

// 1.创建一个Hello组件
//外界传的值, 需要在构造函数中接收, 接收之后就可以直接使用  注意组件名必须大写
function Hello(props) {
  #组件的props是只读的  
  return <div>这是Hello组件 --- {props.name} --- {props.age} --- {props.gender} </div>
}

ReactDOM.render(<div>
  {/*  2.像在vue中一样, 以标签形式引入组件  并且可以给组件传值 */}
  <Hello name={dog.name} age={dog.age} gender={dog.gender}></Hello>
        
  {/* 使用ES6 的展开运算符 */}      
   <Hello {...dog}></Hello>     
</div>, document.querySelector('#app'))
```



### 抽离到jsx文件创建组件

把 组件抽离为一个单独的`.jsx`文件

> **确保, webpack能够解析jsx的文件, webpack.config.js必须配置 rules**

1. 将组件抽离到`jsx`文件中

```jsx
import React from 'react'

//创建并导出一个Hello组件
export default function Hello(props) {

  // props.name = '大黄'
  return <div>这是Hello组件 --- {props.name} --- {props.age} --- {props.gender} </div>
}
```

2. 在`index.js` 入口文件中 导入组件`import`

```js
import React from 'react'
import ReactDOM from 'react-dom'

const dog = {
  name: '小黑',
  age: 3,
  gender: '雌'
}

//导入组件==================================================导入组件
//并且后缀名在没有配置的情况下是不能省略的
import Hello from './components/index.jsx'

ReactDOM.render(<div>
  {/* <Hello name={dog.name} age={dog.age} gender={dog.gender}></Hello> */}
  <Hello {...dog}></Hello>

</div>, document.querySelector('#app'))
```



## 导入时省略.jsx文件的后缀名

在`webpack.config.js`中配置 `resolve: { extensions: [] }` 

> 我们在react项目中可以配置.jsx, 在vue中则可以配置.vue省略后缀名
>
> 我们配置的`webpack.config.js` 能够覆盖脚手架默认的配置

```js
//和 mode, plugins, entry 平级的属性
resolve: {
    //表示这几个文件的后缀名可以省略, 会自动补全后缀, 顺序是从前到后
    extensions: ['.js', '.jsx', '.json'] 
}
```



## 使用`@` 代替 `src` 这一层路径

有时候我们引入组件还可以使用 `@` 开头

可以使用`alias` 是一个对象, 别名的意思

```js
#引入组件的时候, 以@开头
import Hello from '@/components/index'

#在webpack.config.js中的配置
  resolve: {
    extensions: ['.js', '.jsx', '.json'],
    alias: {
      "@": path.join(__dirname, './src')
    }
  }
```



## class类创建组件

ES6 中class 是实现类的一种方法, `class` 本身是一个语法糖

### 类的基本使用

1. `class` 定义的类和 构造函数一样, 可以`new`  一个对象
2. `constructor` 属性能够定义实例属性, `new` 的时候会优先执行`constructor` 的代码, **每一个必须有构造器**
3. `static` 是静态属性, 类作为对象, 也可以有自己的属性

```js
class Animal {
  //如果不写constructor, 默认就是一个  constructor () { }
  //每当new的时候, 会优先执行构造器中的代码, 能够接受实参
  constructor(name, age) { //相当普通的构造函数  constructor中的属性就是实例属性
    //this.name, this.age 也叫做实例属性, new之后, 实例对象自己身上就有
    this.name = name 
    this.age = age
  }

  // 静态属性: 通过构造函数直接访问的属性, 构造函数也是对象, 也可有自己的属性
  static info = '这是Animal的静态属性' 
}

let a1 = new Animal('大黄', 3)
console.log(a1) 
console.log(Animal.info)

```



### 类添加实例方法

也就是给类(构造函数) 原型上添加方法, 实例对象能够直接 `.` 出来的方法, 也叫做实例方法

作用和 在构造函数的`Animal.prototype.eat = function () {}` 做作用相同

两种方式都能够给实例添加方法, **一个是直接添加到实例对象身上, 一个添加到实例对象的构造函数的原型上**

```js
class Animal {
  constructor(name, age) { //相当普通的构造函数  constructor中的属性就是实例属性
    this.name = name 
    this.age = age
    //这是相当于直接给实例添加实例方法---------------
    this.show = function () {
      console.log('直接添加在实例对象身上')
    }
  }
    
  //这是相当于给实例的构造函数的原型添加方法-----------------------
  show () {
    console.log('添加在构造函数原型上')
  }  
    
  // 属性初始化语法, 其实就行相当于把实例方法从`constructor`中抽离出来了, 还是直接添加到实例上  
  show = () => {
    console.log('还是直接添加到实例对象身上的')  
  }  

  // 静态属性: 通过构造函数直接访问的属性, 构造函数也是对象, 也可有自己的属性
  static info = '这是Animal的静态属性'
  
}
```



### 类添加静态方法

在方法前面添加`static` 关键字, 定义的方法就是静态方法, 实例对象无法访问

```js
// 这是类的静态方法 和实例方法平级
static show() {
    console.log('这是Animal的静态方法')
}
```

> 注意点1 : 在class 的` {  }` 内部只能写 构造器, 实例属性, 实例方法 和静态属性, 静态方法
>
> 注意点2 : class 只是在语法层面帮我们做一层优化, 内部还是使用 原来的构造函数 , 它只是一个`语法糖`



## class 实现继承

### 实现继承的基本方式

```js
class Person {
  constructor(name, age) {
    this.name = name
    this.age = age 
  }
}

//通过extends 关键字, 就可以实现继承, 能够继承Person
class Mail extends Person { }

class Femail extends Person { }

let boy = new Mail('大傻子', 18)
let gils = new Femail('小傻子', 18)
console.log(boy)
console.log(gils)
```



### 继承父类的实例方法

构造函数能够继承父类构造函数,  在 `new` 的时候 实例对象能够访问

```js
class Person {
  constructor(name, age) {
    this.name = name
    this.age = age
  }

  //这是相当于给实例的构造函数的原型添加方法----------实例对象能够访问
  show() {
    console.log('这是外部的实例方法')
  }
}

//通过extends 关键字, 就可以实现继承, 能够继承Person
class Mail extends Person { }

class Femail extends Person { }

let boy = new Mail('大傻子', 18)
let gils = new Femail('小傻子', 18)
console.log(boy)
console.log(gils)

```



`extends` 

`extends` 在我们不写`constructor () {}` 时, 底层会帮我们调用`constructor()` 并改变this指向 



### `super()` 函数

1. 为什么要在子类的构造器`constructor` 中调用`super()` 

因为 如果一个子类通过 `extends` 继承了父类, 那么在子类的`constructor` 中必须优先调用 `super()`  这是约定

如果我们不写constructor , 不加私有属性, 则extends 默认调用`super()` 

2. `super` 是什么

`super` 是一个函数, 而且 它是父类的 构造器,   调用`super()` 就相当于父类的`constructor()` , 它就是父类构造器的一个引用

也就是说在调用的`super(name, age)` 的时候, 父类`constructor(name, age)` 的形参在调用形参的时候, 也需要定义 

3. 为什么掉用`super()` 不传实参,  new 出来的实例对象属性都是`undefined` 

`super(name, age)`相当于调用父类的` constructor `把实参传递父类构造器, 不传实参, 实例对象的值就是`undefined`

```js
class Person {
  constructor(name, age) {
    this.name = name
    this.age = age
  }

  //这是相当于给实例的构造函数的原型添加方法
  show() {
    console.log('这是外部的实例方法')
  }
}

//通过extends 关键字, 就可以实现继承, 能够继承Person
class Mail extends Person { 
  constructor(name, age) {
    super(name, age)
  }
}

class Femail extends Person {
  //在new的时候, 传递的参数第一次出现在constructor中
  constructor(name, age) {  // name,age --> 形参
    super(name, age) //  name,age --> 实参 相当于调用父类的 constructor  把实参传递父类构造器
  }
}

let boy = new Mail('大傻子', 18)
let gils = new Femail('小傻子', 18)
console.log(boy)
console.log(gils)
boy.show()
gils.show()
```



> 在 `extends` 继承 父类, 不写 `constructor` 会默认 调用`super()` , 并且把参数传给父类



### 定义子类独有实例属性

> 子类独有的实例属性, 必须在`super()` 后面写, 不然就会报错

```js
class Femail extends Person {
  //在new的时候, 传递的参数第一次出现在constructor中
  constructor(name, age, mei) {
    super(name, age) // 相当于调用父类的 constructor  把实参传递父类构造器
    # 必须在super()之后写
    this.mei = mei
  }
}
```



## class创建组件

### 基本的组件结构

1. 如果是抽离出来的组件需要`export default`导出
2. `render(){}` 方法的作用是: 渲染当前组件**对应的虚拟DOM元素**, 且 必须有 `return`  
3. 在根组件的`jsx` 环境内部, 直接以标签形式使用组件

```js
import React from 'react'
export default  class Liu extends React.Component {
  render() {
    return <div>这一个class创建的组件</div>
  }
}
```



### class组件传值

> **通过class创建的组件, 在组件标签传递的值 , 在组件内部可以直接通过 `this.props.属性`, 直接使用** 

- 组件中的`this` 指向当前组件的实例对象

```js
import React from 'react'
import ReactDOM from 'react-dom'
class Liu extends React.Component {
  render() {
    // 内部的this也指向组件实例对象  
    return <div>这一个class创建的组件 -- {this.props.name} --- {this.props.age}</div>
  }
}

ReactDOM.render(<div>
  <Hello {...obj}></Hello>
{/* 在jsx中使用的组件标签, 就是组件的实例对象 */}
  <Liu {...obj}></Liu>
</div>, document.querySelector('#app'))
```

> *引入的组件 `<Liu></Liu>` ,  就是组件的实例对象*
>
> 不论是`class`  还是 普通 构造函数 创建的组件 的 props 都是 `只读的`



**另一种不常用的方式**

也可以在`constructor (props) {}` 中接收组件传递的值

```js
class Liu extends React.Component {
    constructor (props) {
        super(props)
        console.log(props)
    }
}
```





### class 创建组件 和 构造函数创建组件区别

1. 使用`class` 创建的组件有生命周期函数和自己的私有数据,  但使用`function` 创建的组件没有生命周期钩子, 没有自己的私有数据, 只有`props`
2. 使用`class` 创建 的组件传递的参数直接通过`this.props.属性` 使用, `function` 创建的组件需要接收
3. 用构造函数`function` 创建的组件叫做:  `无状态组件/ 木偶组件`, 状态(state)即数据, 无法有自己私有数据
4. 用`class` 创建的组件叫做: `有状态组件/ 智能组件` , 有`state`, 可以有自己私有数据

> 有状态和无状态之间的**本质区别**: 有无 `state` 属性 和 生命周期函数
>
> 无状态组件以后用的不多

```js
# class创建组件
 class Liu extends React.Component {
  render() {  //传递的采纳数不需要接收, 直接通过 this.props.属性 使用
    console.log(this)
    return <div>这一个class创建的组件 -- {this.props.name} --- {this.props.age}</div>
  }
}

#使用构造函数创建组件
function Hello(props) {   // 传递的参数需要接收
  return <div>这是一个分离出去的react组件 --- {props.name} --- {props.age} --- {props.gender}</div>
}

#在引入组件 和 传参时, 都相同
ReactDOM.render(<div>
  <Hello {...obj}></Hello>
  {/* 在jsx中使用的组件标签, 就是组件的实例对象 */}
  <Liu {...obj}></Liu>
</div>, document.querySelector('#app'))
```



## this.state

> 只有调用`super()` 之后, `this` 才能使用

`this.state = {}`  在 组件中的`constructor` 中`super()` 后面定义, 它就相当于 `vue` 中的 `data () { return {} }`

### state 第一种写法

`this.state` **中的数据是可读可写的**

```js
class Liu extends React.Component {
  constructor() {
    super()
    this.state = {
      msg: '这是Liu组件的私有数据!'
    }
  }
  render() {
    // console.log(this)
    this.state.msg = 'state中的数据是可以修改的'
    return <div>
    这一个class创建的组件 -- {this.props.name} --- {this.props.age}
    <h3>{this.state.msg}</h3>
    </div>
  }
}
```



### state 第二种写法 (推荐)

也叫: 属性初始化语法

不需要在`constructor` 中书写, 提取到外面写, 其实本质都是一样的

```js
class Liu extends React.Component {
  state = {
      msg: '这是Liu组件的私有数据!'
  }
  render() {
    // console.log(this)
    this.state.msg = 'state中的数据是可以修改的'
    return <div>
    这一个class创建的组件 -- {this.props.name} --- {this.props.age}
    <h3>{this.state.msg}</h3>
    </div>
  }
}
```





## this.setState

- 修改`state` 中的数据
- 重新调用`render()` 更新页面

在`react` 中 为 `state `中的属性重新赋值, 不要直接通过 `this.state.*** = 新值`

如果直接修改 `state` 中的值,页面不会响应式更新, 但是`state` 的值确实能够修改, 应该使用`this.setState({})`

```js
export default class EventBind extends Component {
  constructor () {
    super()
    this.state = {
      msg: '这是msg数据'
    }
  }  
  render () {
    return <div>
      这是EventBind组件
      <hr/>
      <button onClick={ () => this.show('123 🐷') }>这是一个点击事件</button>
      <h3>{this.state.msg}</h3>
    </div>
  }
  //点击事件的处理函数
  show =  (arg) => {
    // console.log('哈哈哈哈' + arg)
    this.setState({
      msg: '响应式修改了msg的值'
    })
  }
}
```

> 在`setState()` 中 只会把 提供的 state 状态值更新,  而不会覆盖掉没有修改的 state 值
>
> **`setState()`  这个方法是 异步的**
>
> `setState` 会重新调用`render` , 就存在性能优化问题, render中存在我们组件的所有结构

注意 :  

`this.setState( {} , callback )`

- `callback` : 由于这个api 是 异步的, 如果想拿到最新的 值, 可以在 回调函数中 拿





## 函数组件和类组件使用场景

1. 看需不需要`state` 和 生命周期
2. 类组件比较强大, 有state 和 生命周期, 但是缺点渲染速度慢
3. 函数组件没有`state` 和 `生命周期` 渲染数据快



## 组件中`props` 和 `state`区别

- `props` 中的 数据是外界传递的
- `state/data` 是组件私有的数据, 一般通过`ajax` 获取来的数据
- `props` 中的数据是只读的,  `state` 中的数据是可读可写的





## React 中 事件处理

### 基本使用

在`react`  有一套自己事件绑定机制,  事件名都必须遵守驼峰命名规则

```js
/**
	js: onclick	
	vue: @click    v-on
	react: onClick  驼峰
*/
```

**用的最多的事件绑定形式为：**

属性初始化语法 => 箭头函数 =>能够避免`this` 问题

> `React `默认是没有帮我们处理, class中函数的this问题, 我们需要借助`箭头函数` 或者 `bind` 

```js
import React, { Component } from 'react'
import ReactDOM from 'react-dom'

class Person extends Component {
  render () {
    return (
      <div>
        <button onClick={ () => this.fn('哈哈') }>哈哈哈</button>
      </div>
    )
  }

  fn = arg => {
    console.log(this, arg)
  }
}

ReactDOM.render(<Person />, document.querySelector('#app'))
```

在React中，如果想要修改 state 中的数据，推荐使用 `this.setState({ })`



### 事件处理函数中的this

- 在class 中的事件处理函数中没有`this` , `this` 是`undefined`

```jsx
class Child extends React.Component {
    state = {
       name: '张三' 
    }
	render () {
        return <div>
            	<button onClick={this.fn}>修改state的值</button>
            </div>
    }
	fn () {
        console.log(this) // undefined
        this.setState({
            name: '李四' // 报错
        })
    }
}
```



### `bind`解决`this` 问题

作用: 改变`this`指向, 创建新函数并返回

写法一: 

- 使用`bind` 绑定`this` , 返回一个新函数, 在点击的时候, 触发函数

**传参**: `this.fn.bind(this, 参数1, 参数2)`

**获取事件对象**: 

- 在不传参的情况下, 默认的形参就是事件对象, 可以**直接获取使用事件对象**
- 最后一个形参就是事件对象`this.fn.bind(param1, param2, ...., e)`

```jsx
class Child extends React.Component {
	render () {
        return <div>
            	{/* 使用bind 绑定this */}
            	<button onClick={this.fn.bind(this)}>修改state的值</button>
            </div>
    }
	fn () {
        console.log(this) // 当前组件对象
        this.setState({
            name: '李四' 
        })
    }
}
```

写法二: (不常用) 

```jsx
class Child extends React.Component {
    constructor () {
        super()
        this.fn = this.fn.bind(this)
    }
	render () {
        return <div>
            	{/* 使用bind 绑定this */}
            	<button onClick={this.fn}>修改state的值</button>
            </div>
    }
	fn () {
        console.log(this) 
        this.setState({
            name: '李四'
        })
    }
}
```



### 属性初始化语法 (优先)

**传参**: 属性初始化语法**不能传参**, 传参就直接调用了

**获取事件对象**: 由于不能传参, 所以默认的形参就是事件对象`e`

```jsx
class Child extends React.Component {
    constructor () {
        super()
        this.fn = this.fn.bind(this)
    }
	render () {
        return <div>
            	<button onClick={ this.fn }>修改state的值</button>
            </div>
    }
	fn = () => {
        console.log(this) 
        this.setState({
            name: '李四'
        })
    }
}
```



### 箭头函数处理this

传参: 直接传参, 接收, 使用即可

获取事件对象: 

- 由于箭头函数中的函数体是`函数调用`, **不传参就没有函数就没有形参**

```jsx
class Child extends React.Component {
    constructor () {
        super()
        this.fn = this.fn.bind(this)
    }
	render () {
        return <div>
            	<button onClick={ (e) => this.fn(e) }>修改state的值</button>
            </div>
    }
	fn (e) {
        console.log(e)
        this.setState({
            name: '李四'
        })
    }
}
```



### 箭头函数 + 属性初始化语法

- 想传参就直接传参, 想获取事件对象, 就直接获取

```jsx
class Child extends React.Component {
    constructor () {
        super()
        this.fn = this.fn.bind(this)
    }
	render () {
        return <div>
            	<button onClick={ (e) => this.fn(123) }>修改state的值</button>
            </div>
    }
	fn =  (num, e) => {
        console.log(num, e)
        this.setState({
            name: '李四'
        })
    }
}
```



# React 第三天



## 条件渲染

#### 1. if / else

```js
state = {
    isLoading: true
} 
render () {
    if (this.state.isLoading) { // 正在加载中
      return <h1>Loading...</h1>
    }
    return <div>这就是我们想要的内容</div>
  }
// 钩子函数 五秒钟之后 修改状态值
  componentDidMount () { 
    setTimeout(() => {
      this.setState({
        isLoading : false
      })
    }, 3000);
  }
```

#### 2. 三元表达式

```js
 return this.state.isLoading ? (<h1>Loading...</h1>) : (<div>这就是我们想要的内容</div>)
```

#### 3. 逻辑运算符

一般用来判断数组是否为空, 不为空则渲染数组`{ list && list.map() }`

```js
 return this.state.isLoading && (<h1>Loading...</h1>) 
```



## 列表渲染

#### 遍历简单数组

使用数组的`map()` 方法遍历数组

```js
// 准备数据
state = {
  list :['小苹果','大香蕉','黄橙子']
}

return (
    <ul>
    {
        this.state.list.map(item => { 
       		return <li>{ item }</li>
     	}) 
	}
	</ul>
)
```



#### 遍历对象数组

> 如果不指定`key` 浏览器会报错, 这里的`key` 和 vue 中一样

```js
// 准备数据
state = {
    list2: [{ id: 1, name: '春' }, { id: 2, name: '飞' }, { id: 3, name: '莲' }]
}
// 遍历
 return (
      <ul>
        {this.state.list2.map(item => { 
          return <li key={item.id}>{ item.name }</li>
        }) }
      </ul>
    )
```

#### 提取到函数

```jsx
// render 钩子函数
render () {
  return (<ul>
        { this.renderLi()  }
       </ul>)
 }
  
// 提取到的一个函数
renderLi () { 
   # 必须要有返回值 把 map得到的数组return 出去
  return this.state.list2.map(item => { 
      # 这个return 是 map 函数的return
     return <li key={item.id}>{ item.name }</li>
    }) 
}
```



## React中的key

react中的key 和 vue中的key完全一样, 唯一区别就是绑定key的方式不一样, key要绑定给我们遍历的元素

```js
#为遍历的元素绑定key值
nameArr.map(item => <h3 key={item}>{ item }</h3>) }
```

没有key在浏览器控制台会报警告

```html
Warning: Each child in a list should have a unique "key" prop
```







## `style` 行内样式

在jsx中书写style的格式为 `<h1 style={ {color: 'red'} }></h1>`

> 双花括号, 外面的花括号表示我们要写js代码了 
>
> 里面的花括号是一个样式对象,  是一个JS对象, 要符合JS的规范

```jsx
import React from 'react'

//第一层封装
const cmtItem = {
  border: '1px dashed #ccc', 
  boxShadow: '0 0 7px #ccc', 
  margin: '20px auto',
  padding: '10px 10px',
  boxSizing: 'border-box',
  width: '500px'
}

//第二层封装
const styles = {
  cmtItem: {
    border: '1px dashed #ccc', 
    boxShadow: '0 0 7px #ccc', 
    margin: '20px auto',
    padding: '10px 10px',
    boxSizing: 'border-box',
    width: '500px'
  },
  cmtTitle: {
    fontSize: '14px'
  }
}

export default class CmtItem extends React.Component {
  render () {
    return <div style={styles.cmtItem}>
      <h3 style={styles.cmtTitle}>评论人: {this.props.user}</h3>
      <p >评论内容: {this.props.content}</p>
    </div>
  }
}
```

> **也可以把css样式对象 ,抽离为一个 js 文件,成为一个样式表模块**



## 使用css样式文件

webpack的css-loader 配置

在组件中可以引入css样式文件, 使用样式文件提供的类名, 去美化DOM元素

1. 创建对应的`.css` 样式文件, 书写样式
2. 下载处理css的`loader`, 并且在webpack配置loader
3. 在组建中`import` 引用样式文件, 给虚拟DOM 添加类名
   - css样式文件, 没有作用域, 直接导入的css样式文件, 默认是在全局, 整个项目都能生效

```js
//webpack的配置
 {test:/\.scss/, use: ['style-loader', 'css-loader', 'sass-loader']}
 {test:/\.less/, use: ['style-loader', 'css-loader', 'less-loader']}
```



css 文件使用

1. import css 文件
2. 给jsx元素添加样式类名即可

```js
//2. 引入
import './index.css'

//3. 添加类
 <p className='red' >哈哈</p>
```



#### css模块化

css文件没有文件作用域的概念, 引入的css样式文件, 在整个项目都能生效, 就导致了, 样式可能冲突的问题

在`vue` 也有样式冲突, 但是在vue 中 提供了`scoped`  指令能够解决样式全局污染问题, 但是在`react` 没有指令的概念

但是可以配置`css-loader` 是css具有模块化的概念

```js
# 这是webpack 4.x 配置, 中文网是还未及时更新
//给css-loader 配置模块化, loader也可以为一个对象
      { 
        test:/\.css/, 
        use: [
          'style-loader',
          {
            loader: 'css-loader',
            options: {
              modules: {
                mode: 'local',
                localIdentName: '[path][name]__[local]--[hash:base64:5]',
                // context: path.resolve(__dirname, 'src'),
                // hashPrefix: 'my-custom-hash',
              }
            }
          }
        ]
      }
```

> 但是css模块化 只针对 类选择器 和 id 选择器 生效
>
> 对于标签选择器不会模块化, 依旧存在全局问题



#### 自定义模块化类名

1. 启用 css-modules

   1. 修改 `webpack.config.js`这个配置文件，为 `css-loader` 添加参数：

      ```js
      { test: /\.css$/, use: ['style-loader', 'css-loader?modules'] } // 为 .css 后缀名的样式表  启用 CSS 模块化
      ```

   2. 在需要的组件中，`import`导入样式表，并接收模块化的 CSS 样式对象：

      ```js
      import cssObj from '../css/CmtList.css' 
      ```

   3. 在需要的HTML标签上，使用`className`指定模块化的样式：

      ```jsx
      <h1 className={cssObj.title}>评论列表组件</h1>
      ```

2. 使用`localIdentName`自定义生成的类名格式，可选的参数有：

   - [path]  表示样式表 `相对于项目根目录` 所在路径
   - [name]  表示 样式表文件名称
   - [local]  表示样式的类名定义名称
   - [hash:length]  表示32位的hash值
   - 例子：

   ```js
     { 
           test:/\.css/, 
           use: [
             'style-loader',
             {
               loader: 'css-loader',
               options: {
                 modules: {
                   mode: 'local',
                   localIdentName: '[path][name]__[local]--[hash:base64:5]',
                   // context: path.resolve(__dirname, 'src'),
                   // hashPrefix: 'my-custom-hash',
                 }
               }
             }
           ]
         }
   ```

   

3. 使用 `:local()` 和 `:global()`

   - `:local()`包裹的类名，是被模块化的类名，只能通过`className={cssObj.类名}`来使用

     同时，`:local`默认可以不写，这样，默认在样式表中定义的类名，都是被模块化的类名；

   - `:global()`包裹的类名，是全局生效的，不会被 `css-modules` 控制，定义的类名是什么，就是使用定义的类名`className="类名"`

4. 注意：只有`.title`这样的类样式选择器，才会被模块化控制，类似于`body`这样的标签选择器，不会被模块化控制



**模块化类名的使用**

```jsx
//如果想要添加多个类名, 可以结合数组 和 数组的 join方法
<h1 className={[cssobj.title, cssobj.title2, 'title3'].join(' ')}>这是一个评论父组件</h1>
```



**在模块化中定义一个全局的类名**

使用`:global(.className)` 能够将这个类选择器变成全局的类名

```css
:global(.title3) {
    font-style: italic;
}
```

使用`:local(.className)` 能够将这个类名变成一个局部的类名



## 第三方样式表

**为了在react中使用样式表, 我们把css文件开启了模块化, 但是对于第三方的UI框架, 我们并不想启用模块化, 而是直接使用它提供的类名**

所以我们约定: 自己样式表以`.scss` 或者 `.less` 启用模块化, 对于 `.css` 文件不启用模块化 	

> 所以在配置`css loader` 的时候, 第三方的css 文件 不配置模块化
>
> 我们自己使用`.scss ` `.less` 文件配置模块化

使用: 

```js
//导入时, 直接导入, node_modules z这层目录可以省略 
import 'bootstrap/dist/css/bootstrap.css'

<button className="btn btn-success">这是一个bootstra</button>
```

### css loader 配置 

```js
   {  // js loader
        test: /\.js|jsx$/,
        use: 'babel-loader',
        exclude: /node_modules/
      },	
	{  // scss loader
        test:/\.scss/, 
        use: [
          'style-loader',
          {
            loader: 'css-loader',
            options: {
              modules: {
                mode: 'local',
                localIdentName: '[path][name]__[local]--[hash:5]',
                context: path.resolve(__dirname, 'src'),
                hashPrefix: 'my-custom-hash',
              }
            }
          },
          'sass-loader'
        ]
      },
      {  //css loader
        test:/\.css/, 
        use: [
          'style-loader',
          'css-loader',
        ]
      },
      {  //less loader
        test:/\.less/, 
        use: [
          'style-loader',
          {
            loader: 'css-loader',
            options: {
              modules: {
                mode: 'local',
                localIdentName: '[path][name]__[local]--[hash:5]',
                context: path.resolve(__dirname, 'src'),
                hashPrefix: 'my-custom-hash',
              }
            }
          },
          'less-loader'
        ]
      },
      { test: /\.ttf|woff|woff2|eot|svg$/, use: 'url-loader'}
```



## 受控组件

#### 什么是受控组件

对于表单元素我们加`value` 属性之后, 就变成一个受控组件, 在没有`onChange` 处理函数, 这个表单元素, 无法输入变成了一个受控组件 => **简而言之, 给表单元素加`value` 之后就变成受控组件了**

- `value` 就是从 `M -> V` 的过程
- `onChange` 就是`V -> M` 的 过程 从而实现数据双向绑定

```jsx
render () {
    return (
        # 在没有onChange 的情况下, 这个表单无法交互
    	<input value={this.state.msg} onChange={ e => this.txtChange(e)}>	
    )
}
```

#### 其他受控组件

```jsx
// 文本输入框
<input onChange={this.handleInput} value={username} type="text" />  <br />
// 文本域
<textarea onChange={this.handleTextarea} value={content} cols="30" rows="10"></textarea>
// 下拉框
<select value={city} onChange={this.handleSelect}>
    <option value="sh">上海</option>
    <option value="hz">杭州</option>
    <option value="bj">北京</option>
</select>
```



#### 优化`onChange`处理函数

由于`onChange` 处理函数的代码都基本差不多, 写了很多重复的处理函数, 如果一个页面有很多表单元素, 则会出现很多处理函数

**优化方式一**

绑定一个`handler` 受控组件处理函数, 则多个受控组件共用一个处理函数

表单元素需要定义`name` 属性

```js
handler = e => {
    this.setState({
        [e.target.name]: e.target.value
    })
}
```

> 注意点: 在对象中,如果key使用变量, 则需要加`[]` 包裹 



**优化方式二**

- 把要修改的`key / value` 传值

```jsx
// 文本输入框
<input  onChange={(e) => this.getValues('username', e.target.value)} value={username} type="text" />  <br />
// 文本域
<textarea onChange={(e) => this.getValues('content', e.target.value)} value={content} cols="30" rows="10"></textarea>
// 下拉框
<select value={city} onChange={ (e) => this.getValues('city', e.target.value) }>
    <option value="shanghai">上海</option>
    <option value="hangzhou">杭州</option>
    <option value="beijing">北京</option>
</select>
```

`onChange` 处理

```jsx
 getValues = (name, value) => { 
    this.setState({
      [name] : value
    })
  }
```





## 评论案例-结合受控组件





## 非受控组件

#### 什么是非受控组件

如果想要给表单元素添加默认`value` , 而且不想把表单组件变成`受控组件` 可以使用`defaultValue={}` , 表单元素依旧保持交互性

```jsx
<input type="text" defaultValue={this.state.name} />
```

**表单元素(组件) 默认就是非受控组件**

#### 如何拿到非受控组件的值

1. 创建`ref` 引用

```js
constructor(){
  super()
	// 方式1
  this.iptRef = React.createRef()
}
// 和 state 一样
// 方式2: 属性初始化语法
iptRef = React.createRef()

<input ref={ this.iptRef } />
```

2. 通过`ref` 把非受控组件绑定起来

```jsx
render () {
    return (
        <div>
            <input ref={ this.iptRef } />
            <button onClick={this.click}></button>
        </div>
    )
} 

```

3. 通过DOM操作获取数据

```jsx
// 可以通过尝试点击按钮
click = () => {
    console.log(this.iptRef.current.value)
}
```





## React中表单双向数据绑定

### 单向数据流

- 如果我们给表单元素, 绑定`state` 的 状态值,  一旦`state `状态值变化, 将会同步到页面中
- 这个表单将会变成一个只读的表单元素 , 只能实现单向数据流动
- 需要给表单元素绑定一个`onChange` 事件

### 双向数据绑定

React  无法实现像 vue 中的 `v-model` 双向数据绑定

在react 中, 需要我们手动监听文本框的`onChange` 事件, 在 `onChange` 事件中拿到最新的值,  调用 `this.setState()` 把最新的值同步到 `state` 



#### 事件对象e

只有拿到最新的数据, 才能够给state 同步数据, 实现双向数据绑定

方式一:  ` 使用 事件参数e.target.value ` 结合 `setState()`

```jsx
# 1- 定义onChange 事件
<input type="text" value={this.state.msg} onChange={ (e) => this.txtChange(e) }/>
 
txtChange = (e) => {
    // console.log(e.target.value)
    # 拿到最新的值, 调用 setState 同步到 state 中
    this.setState({
      msg: e.target.value
    })
  }
```



#### this.refs 实现双向数据绑定

和vue 中 的`vm.$refs.引用名` 作用一样, 通过在 元素身上定义 `ref="引用名"` 

通过`this.refs.引用名` 就可以访问到这个元素

1. 给 表单元素绑定`onChange` 事件
2. 通过`e.target.value` 或者 `this.refs.引用名` 拿到最新的值
3. 调用`this.setState()` 把数据同步到`state` 中

```js
# 1- 定义onChange 事件
<input type="text" value={this.state.msg} onChange={ (e) => this.txtChange(e) } ref="txt"/>

 txtChange = () => {
    // console.log(this.refs.txt.value)
    # 3-拿到最新的值, 调用 setState 同步到 state 中
    this.setState({
     //	2- 拿到最新的值
      msg: this.refs.value
    })  
  }
```



**ref 的另一种用法**

- `React.createRef()` 能够创建一个ref 引用对象, 并且可以附属到`react` 元素上, `对象的 current ` 属性就是当前的DOM元素
- `this.inputRef.current` 自定以的引用对象,能够得到附属在DOM元素

```js
class Person extends Component {
  state = {
    msg: '嘻嘻嘻 '
  }
  render () {
    return (
      <div>
        <button>{ this.state.msg }</button> 
        <input onChange={ () => this.setText() } value={ this.state.msg } ref={this.inputRef}/>
      </div>
    )
  }
  // createRef 是一个方法, 能够得到一个ref引用对象, 能够附属到 react 元素上
  inputRef = React.createRef()
  setText = e => {
    // this.inputRef 是一个对象, current指向当前的DOM元素
    console.log(this.inputRef.current)
    this.setState({
      msg: this.inputRef.current.value
    })
  }
}

ReactDOM.render(<Person />, document.querySelector('#app'))
```





## 组件通讯

### 父传子

1. 通过属性传值的方式传递给子组件,子组件通过props, 就可以拿到父组件传递过来的值

```js
// 父组件
class Parent extends React.Component {
  // 1. 准备好数据
    state = {
      pName : '父的数据'
    }
    render() {
      return (
        <div>
          <p>哈哈</p>
          //2. 通过属性 将数据传递给子组件
          <Child name={this.state.pName}></Child>
        </div>
      )
    }
}
// 子组件  
// 3. 通过 props 获取数据
const Child = (props) => <div>子组件 { props.name }</div>
```



### 子传父

思路: 父组件中提供了一个方法, 由子组件调用这个方法, 将数据作为参数传递给父组件

步骤 : 

- 1-在父组件中提供一个方法
- 2-将这个方法通过属性传递给子组件
- 3-子组件中通过props 拿到这个方法调用, 并且将数据作为实参传递给父组件传递过来的函数, 父组件就拿到子组件传递过来的实参了

```js
// 父组件
class Parent extends React.Component {
    // 第一步 :父组件准备一个方法
    pFn = (data) => { 
      console.log('调用了',data);
    }
    render() {
      return (
        <div>
          <p>哈哈</p>
          {/* 第二步 : 通过属性将方法产传递给子组件 */}
          <Child cfn={ this.pFn } ></Child>
        </div>
      )
    }
}
// 子组件  
class Child extends React.Component { 
  render () { 
    return (<div>
      <button onClick={this.sendMsg}>点击发送</button>
    </div>)
  }
  sendMsg = () => { 
    // 第三步 : 子组件通过props 拿到这个方法, 并且传参
    this.props.cfn('撩汉子')
  }
}
```





### 非父子传值

react 中没有 vue 中的 bus 来实现非父子的传递

思路: `状态提升`, A 组件把数据传递给 父组件, 父组件把数据传递给 B组件, 当A组件数据改变, 再传递给 父组件, 父组件通过单向数据流, B组件的值也随之改变

总结: 子传父 -> 父传子

## 组件化改造评论列表





# React 第四天

## 组件通讯

> 父传子  
>
> 子传父  
>
> 非父子(状态提升) 
>
> context  
>
> localStorage 
>
> redux

**localStorage 和 redux(vuex) 有什么区别?**

redux 是响应式的 , localStorage 不是响应式的 

### context

`context: 上下文`用来解决跨多层组件传递数据的问题

当多层组件嵌套, 想传递一个数据到最里层的组件 , 可以通过父传子一层一层传递, 也可以使用`context` 传递

#### 使用

`const { Provider, Consumer } = React.createContext()`

- `Provider` 提供组件 传递数据的组件/ 提供数据的组件
- `Consumer` 消费组件, 接收数据的 / 使用数据的组件

步骤: 

1. 创建 上下文  解构出来两个组件`const { Provider, Consumer } = React.createContext()`

2. 通过`Provider` 包裹使用数据的组件
   - `<Provider value={ this.state.name }></Provider>`
3. 通过`<Consumer></Consumer>`  接收数据

```js
<Consumer>
  { data => {
   		return <div style={ { color: data } }></div>
 	} 
   }  
</Consumer>
```

待补充: ....

```jsx
1- 创建一个Context并解构
const { Provider, Consumer } = React.createContext()
class Hello extends Component {
  state = {
    msg: '嘻嘻嘻....',
    color: 'red'
  }
  render() {
    return (
      <div>
        2- 用Provider包裹, 并使用value传值
        <Provider value={this.state}>
          <Hello2></Hello2>
        </Provider>
      </div>
    )
  }
}

function Hello2() {
  return (
    <div>
      <Hello3></Hello3>
    </div>
  )
}

class Hello3 extends React.Component {
  render() {
    return (
        3- 使用Consumer 并使用数据
      <Consumer>
        {(state) => {
          return <div style={{ color: state.color }}>{state.msg}</div>
        }}
      </Consumer>
    )
  }
}
```





## Props深入

### children 组件的子节点

`props`默认是一个空对象

我们在使用组件`<Hello name="zs" age={40}>哈哈哈</Hello>` 时, props 接收的值为

```jsx
{
    name: 'zs',
    age: 40,
    children: '哈哈哈'
}
```

我们给组件传递的子节点, 在`props.children` 获取

可以给组件子节点传递js函数等

```jsx
<Hello name="zs" age={40}>
	{ () => console.log('哈哈哈') }
</Hello>
```



### props 类型校验

 随着你的应用程序不断增长，你可以通过类型检查捕获大量错误。对于某些应用程序来说，你可以使用 [Flow](https://flow.org/) 或 [TypeScript](https://www.typescriptlang.org/) 等 JavaScript 扩展来对整个应用程序做类型检查。但即使你不使用这些扩展，React 也内置了一些类型检查的功能。要在组件的 props 上进行类型检查，你只需配置特定的 `propTypes` 属性 

#### 使用`prop-types` 库

安装

```jsx
yarn add prop-types
```

引入

```js
import PropTypes from 'prop-types'
```

添加校验规则  https://zh-hans.reactjs.org/docs/typechecking-with-proptypes.html 

```js
 class Greeting extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    )
  }
}

Greeting.propTypes = {
  name: PropTypes.string.isRequired,  校验位字符串类型并且是必须要传
  age: PropTypes.number,	数字  
  a: PropTypes.array,		数组
  b: PropTypes.bool,		布尔	
  c: PropTypes.func,		函数
  d: PropTypes.number,		数字
  e: PropTypes.object,		对象
  f: PropTypes.string,		字符串
  g: PropTypes.node  		任意类型 
  h: PropTypes.oneOfType([
    PropTypes.string,
    PropTypes.number,
    PropTypes.instanceOf(Message)
  ])
  children: PropTypes.number       props.children 也可以校验  
}
```



#### 属性默认值

```js
方式1: 指定 props 的默认值：
Hello.defaultProps = {
  children: '嘻嘻嘻'
}

方式二:  在组价内部给组件添加静态属性也可
static defaultProps = {
    children: '嘻嘻嘻'
}
```





## React的生命生命周期

**react 有个约定, 钩子的名字越长越不常用**

### **生命周期的概念**

每一个组件就是一个react实例， 从创建、运行、直到销毁，这个过程中，会发生一系列的事件，这些事件就叫生命周期钩子

生命周期钩子也叫生命周期回调函数 在特定的时机自动调用

就像ajax异步请求, 成功后的回调, 我们并没有调用, 自动调用



### 组件挂载阶段

`1. constructor`

组件创建上来就执行这个钩子函数, 是组件的第一个钩子函数\

触发时机: 页面渲染之前

作用: 初始化数据

`2. render`

只要`state` 发生改变, 就会调用`render()`

触发时机: 初始化数据之后, 就会触发

作用: 渲染虚拟DOM到页面上

`3. componentDidMount`

虚拟DOM已经同步到页面后的会调用这个钩子

使用场景:

-  发送ajax, 把数据保存带state 中
- 可以操作DOM



触发顺序: `constructor -> render -> componentDidMount`

> 一辈子只执行一次



### 组件更新阶段

#### **不常用钩子**

`componentWillReceiveProps`

`shouldComponentUpdate` 

如果return true 则执行更新阶段的钩子, 如果rerun false 则不触发更新, 直接进入运行阶段

` componentWillUpdate` 



#### 常用钩子函数

`1. render`

state 数据发生改变时页面重新渲染

触发条件: 

- `new props`  外界传递的数据改变

- `setState()`  内部私有数据改变

- `forceUpdate()` 强制更新

> 按需， 根据`props` 属性或者 `state` 状态的改变选择性的执行



`2. componentDidUpdate`

已经完成更新, 页面已经是新的





#### componentDidUpdate注意事项

在`componentDidUpdate` 中直接使用`setState` 会造成死循环

原因: setState() 会触发`render() ->componentDidUpdate `  在 componentDidUpdate 又触发了setState 又执行render () 则就进入死循环

解决方案: 有条件的执行, 节流阀思想

比较新的`props.xxx` 属性的值和旧的`prop.xxx` 是否相等, 不相等则进入判断

componentDidUpdate 给我们提供了两个参数

- 参数1:  旧的 `props` 
- 参数2:  旧的`preState`

```js
componentDidUpdate (preProps, preState) {
    if (preProps.name !== this.state.name) {
    	this.setState({
            name: 'ls'
        })    
    }
}
```



#### 组件添加key

在组件身上身上添加唯一标识`key` , 对于复用的组件, 每次都会重新创建新组件, 不会复用组件

在 `好租客项目中` ,筛选功能, 可使用 key 作为复用组件的唯一标识, 解决 state 无法获取的问题



### 卸载阶段

`componentWillUnmount`

触发时机: 在组件将要卸载的时候触发

使用场景: 

- 当子组件销毁后, 子组件里的定时器不会被销毁, 可以在这个钩子函数中器清除定时器
- 移除(window, document) 身上注册的事件

> 一辈子只执行一次

**移除组件(不是钩子函数)**

`ReactDOM.unmountComponentAtNode()`



![](./image/LifeCycle.png)







### 重要的钩子

`render()`: 初始化渲染 或 更新渲染调用

`componentDidMount()` : 开启监听, 发送 ajax请求

`componentWillUnmount()`: 做一些收尾工作, 如: 清理定时器

`componentWillReceviceProps()`: 



# React 第五天

## render-props 和 高阶组件

- 什么情况下 会使用这两种模式 ? **复用**
- 当两个组件或者多个组件有一部分` state `   和  `操作 state 的方法`  相同或者相似的时候, 就可以将这些代码逻辑使用这两种模式来实现复用
- 目的 : **状态逻辑复用**    ==> 通俗点说 :  另一种封装形式
- 要复用的内容为 : 
  - state 
  - 操作 state 的方法
- 注意 
  - 不管是高阶组件还是 render-props 模式, 都要将`状态逻辑`封装在一个组件中 
  - 并且这个组件只提供状态和操作状态的方法逻辑
  - 这个组件不提供要渲染的UI结构,  因为要渲染的内容不确定

- **学习注意 :** 
  - **思想重于代码**



## render-props  组件库思想

**封装组件的思想**

封装的这个组件提供某些特定的方法, 我们引入组件, 能够拿到这个组件方法提供的数据, 我们可以根据这个数据, 去做具体的事情例如我们拿到封装组件提供的鼠标位置, 把这个数据体现在页面上等.

**总结**: 封装的组件有特定的方法, 并提供特定功能的数据, 我们`import` 组件能够得到这些数据, 我们需要通过`props` 去传递方法, 封装组件会调用, 我们在提供方法的时候, 就能够拿到封装组件提供的数据



**组件库使用原理:** 

我们引用人家的组件

- 我们拿到数据做我们想做的操作

```js
<Mouse render={ (data) => {  } } >
```

组件库封装

- 调用我们提供的方法
- 并且把数据也传递出去

```js
render () {
    return this.props.render(this.state)
}
```



**原理**: 其实就是, 以属性传递的形式, 给组件的props传递一个`render` 函数, 在这个函数里, `return` 出组件想要渲染的`React JSX` 元素, 在组件的render钩子渲染时调用`this.props.render` 获取传递过来的JSX元素, 在调用`this.props.render(this.state)` 调用时传递参数给 传递的属性render



**总结使用共同步骤**

- 1.给 Mouse 组件传递 `render 属性`    ( render属性的值 是一个函数 )
- 2.通过 render 函数属性的**参数** 来获取组件内部复用的状态 (比如 : 鼠标位置数据)
- 3 通过render函数属性的**返回值**来指定最终要渲染在 页面中的内容

```js
import React from 'react'
import ReactDOM from 'react-dom'
import Mouse from './Mouse'
import Cat from './cat.png'

ReactDOM.render(
  <Mouse
    # 定义render传递给组件
    render={(data) => {
      return (
      <div>
        <p>水平位置: {data.x}</p>
        <p>垂直方向: {data.y}</p>
        <img src={Cat} alt="" style={{ position: 'absolute', left: data.x - 64, top: data.y - 64 }} />
      </div>
    )}}></Mouse>,
  document.querySelector('#root'))
```

在`Mouse` 组件中调用`render(this.state)` 函数并传递所需要的数据

```jsx
import React from 'react'
export default class Mouse extends React.Component {
  state = {
    x: '',
    y: ''
  }
  render() {
    return this.props.render(this.state)
  }
  componentDidMount() {
    window.addEventListener('mousemove', this.handler)
  }

  handler = e => {
    this.setState({
      x: e.clientX,
      y: e.clientY
    }) 
  }
}
```



#### `props.children`代替 `render`

- 注意 : 不是该模式叫 render-props 模式, 就必须使用render 属性
  - 实际上, 只要有一个属性来告诉组件要渲染什么内容, 其实这就是 render-props 模式了
- **推荐 : 使用 children 代替 render 属性**
- **使用 children 演示位置和猫**

```js
ReactDOM.render(
  <Mouse>
    { (data) => {
      return (
      <div>
        <p>水平位置: {data.x}</p>
        <p>垂直方向: {data.y}</p>
        <img src={Cat} alt="" style={{ position: 'absolute', left: data.x - 64, top: data.y - 64 }} />
      </div>
    ) }}
  </Mouse>,
  document.querySelector('#root'))
```



#### 使用场景

场景1:  `context`

第一步: 定义上下文 context

第二步: 使用`Provider` 包裹

第三步: 使用`Consumer` 包裹, 标签内部给一个箭头函数, return jsx 元素

```js
#  这就是render props 的思想实现的
<Consumer>
  { data => {
   		return <div style={ { color: data } }></div>
 	} 
   }  
</Consumer>
```



场景2: `react-spring` 动画库

也用的是`render props` 的封装思想

```js
yarn add react-spring

import { Spring } from 'react-spring/renderprops'
```

使用: 

```js
ReactDOM.render(
  <Spring from={{ opacity: 0 }} to={{ opacity: 1 }} config={{ duration: 4000 }}>
    {
      data => (
    	<h1 sytle={data}></h1>
      )
	}
  </Spring>,
  document.querySelector('#root'))
```





## 高阶组件 HOC

#### 引入->高阶函数

一个函数 `return` 一个 函数 就叫做高阶函数

同理: 一个函数 `return` 一个组件, 这个组件就叫做高阶组件

```js
这就是一个高阶函数
const func = (x) => {
    return (y) => {
        return x + y
    }
}

func(1)(2) // 3
```

推荐书籍 JS 函数式编程  https://llh911001.gitbooks.io/mostly-adequate-guide-chinese/content/ 

#### 高阶组件介绍

高阶组件: HOC : Higher-Order Component

- **高阶组件 :**  HOC : Higher-Order Component
- 实际上**就是一个函数**,  这个函数能够接受一个**参数组件**, 然后,返回一个**增强后的组件**
- **参数组件** : 就是需要被包装的组件
- **返回的组件** : 增强后的组件, 这个组件中就是通过Props来接收到复用的状态逻辑的

- **思想 : 就是组件在增强的过程中, 传入了一些数据给 组件的 props**

```js
const 增强后的组件 = 高阶组件(被包装组件)
```

>  高阶组件（HOC）是 React 中用于 *  复用组件逻辑  *的一种高级技巧 

**高阶组件约定:** 

- 高阶组件的名称都以`with` 开头
- 高阶组件的参数为一个组件, 约定形参为**首字母大写**
- 高阶组件里创建了一个组件, 并且把这个组件返回出去 
- 高阶组件里面可以提供一个state数据, 和操作state的方法

#### 高阶组件基础使用

在`index.js` 文件中

```js
import React from 'react'
import ReactDOM from 'react-dom'
import App from './App'

ReactDOM.render(<App></App>,document.querySelector('#root'))
```

在`APP.js` 组件中

- 高阶组件传参, 直接在组件中拿不到, 因为经过高阶组件包裹, 则需要高阶组件在传递一次

```js
import React from 'react'
// import withCopyRight from './withCopyRight'
import Another from './Another'
class App extends React.Component {
  render() {
    return (
      <>
        APP
        # 只要使用了高阶组件包裹的进行传值, 则实际传递给了高阶组件, 并且这个组件本身
        <Another name="张三"></Another>
      </>
    )
  }
}
export default App
```



组件`Another.js` 使用高阶组件

- 导出的不是组件本身而是组件包裹在高阶组件里面, 就会附带有高阶组件的内容

```js
import React from 'react'
import withCopyRight from './withCopyRight'
 class Another extends React.Component {
  state = {}
  render () {
    console.log(this.props)
    return (
      <div>
        Another {this.props.name}
      </div>
    )
  }
}
export default withCopyRight(Another)
```



定义高阶组件`withCopyRight.js`

- 在以后的使用中, 会使用别人封装的高阶组件
- 我们会得到一些高阶组件传递过来的属性, 给我们使用

```js
import React from 'react'
const withCopyRight = (YourComponent) => {
  return class withCopyRight extends React.Component {
    render() {
        # 高阶组价拿到了props传递的值
     console.log(this.props)
      return (
        <>
          #  这里需要高阶组件在传递一次, 则组件才能得到传递的props值
          <YourComponent {...this.props}></YourComponent>
          <div>&copy; 2019 &emsp; 传智播客</div>
        </>
      )
    }
  }
}
export default withCopyRight
```



#### 给高阶组件添加displayName 

- **displayName**：用于设置 react-dev-tools （浏览器中的react插件） 中组件的展示名称
- **注意**：该属性仅仅用于设置展示名称，并不会对组件功能产生影响，所以，如果不想再 react-dev-tools 中进行区分，实际上，可以省略该设置。
- 演示 : 效果

```js
// 同时渲染多个高阶组件的时候
ReactDOM.render(<div>
  <HocPosition/>
  <HocCat/>
</div>, document.getElementById('root'))

// 在 react-dev-tools 上面显示的是这样的
<Mouse>...</Mouse>
<Mouse>...</Mouse>
                
// 这样很不容易区分,所有需要添加displayName
```

- 如何 设置 displayName  ?   **在高阶组件中定义**

```js
const withMouse = (WrappedComponent) => {
  class Mouse extends React.Component {
    ... 省略鼠标位置状态 和 操作鼠标位置的方法逻辑
  }

  // 给高阶组件设置名称，将来在 react-dev-tools 工具中，能够区分到底是哪一个高阶组件包装的组件
  function getDisplayName(WrappedComponent) {                          # +
    return WrappedComponent.displayName || WrappedComponent.name 
  }
  Mouse.displayName = getDisplayName(WrappedComponent)                 # +
  // 如果还想体现出来是高阶组价,就加个前缀
  Mouse.displayName = `WithMouse_${getDisplayName(WrappedComponent)}`  # +

  return Mouse
}
- 补充: 
- 先获取被包装组件的 displayName ,如果没有就获取它的名字,如果再没有来个默认的最起码不会报错或者返回undefined
- WrappedComponent.displayName || WrappedComponent.name 
```



#### 给高阶组件传递属性

- 问题 : 如果给 高级组件传属性, 发现会丢失,
- 原因 :  高级组件内部给创建的Mouse组件内没有赋值属性. 即 高阶组件没有往下传递 Props
- 解决办法 : 渲染 WrappedComponent时, 将 state 和 this.props 一起传递给 Mouse组件
- 传递方法

```js
// 如果多加了属性
<HocPosition name='jack'/>

// 高阶组价内部 :
const withMouse = (WrappedComponent) => {
  class Mouse extends React.Component {
    ... 省略鼠标位置状态 和 操作鼠标位置的方法逻辑

    render() { 
      // 之前这里只传递给包装组件 state ,并没有传递props
      return <WrappedComponent {...this.state}  {...this.props}  />    # ++++
    }
  }
  return Mouse
}

// 使用
const Position = props => {
  // 通过 props 就可以获取到传递给高阶组件的属性了
  // ... 省略其他代码
}
```



#### 修饰器是es7 的独立语法

浏览器当前不支持这个语法, 需要配置babel

1. 安装包

```js
yarn add @babel/plugin-proposal-decorators
```

2. 导出webpack配置(git环境需要commit)
   - 能够将node_modules 中的 webpack 配置导出到根目录	和 package.json也会多一些配置

```js
yarn eject // 能够将node_modules 中的 webpack 配置导出到根目录和 package.json也会多一些配置
```

3. 在 package.json 中 添加babel , plugins

```js

```

4. 需要安装`@babel/plugin-transform-react-jsx-self`

```js
yarn add @babel/plugin-transform-react-jsx-self
```



**使用**

修饰器也可以传参

```js
不使用修饰器
const test = (component) => {
    component.isOk = true
}
class Person {}
test(component)
console.log(component.isOk) // true

使用修饰器
const test = (component) => {
    component.isOk = true
}

@test  # 这里可以传参
class Person {}
console.log(component.isOk) // true
```





#### 高阶组件 + 修饰器

包名: `react-app-rewired`

装包

```js
$ yarn add react-app-rewired
```

**使用装饰器写法**

1- 使用`react-app-rewired` 写法

```js
import React from 'react'
import withCopyRight from './withCopyRight'

@withCopyRight
class Another extends React.Component {
  state = {}
  render() {
    // console.log(this.props)
    return <div>Another {this.props.name}</div>
  }
}
export default Another

```

2- 修改package.json 中的 `scripts` 

```js
  "scripts": {
    "start": "react-app-rewired start",
    "build": "react-app-rewired build",
    "test": "react-app-rewired test",
    "eject": "react-scripts eject"
  },
```

3- 创建`config-overrides.js` 文件

```js
# 配置较为麻烦
module.exports = (config) => {
  #  如果没有使用 customize-cra 就需要在这里进行配置
  
  return config
}
```

4- 使用较为简单的`customize-cra` 包配置 -> 依赖``react-app-rewired``

```js
yarn add customize-cra
```

导入配置``config-overrides.js``

- 必须安装依赖包`yarn add @babel/plugin-proposal-decorators`

```js
const { override, addDecoratorsLegacy }  = require('customize-cra')
module.exports = override(
  addDecoratorsLegacy()
)
```



## setState 异步详解

setState() 更新是异步的

#### 为什么是异步的

如果是同步, 当存在多个`setState` 的时候, 就会存在阻塞

#### setState参数

参数1: 要修改的对象

参数2: 异步的回调函数, 这里能拿到setState执行后的结果

```js
console.log(this.state.count)  # 0
# 更新是异步的
this.setState({
    count: this.state.count++
}, () => {
    console.log(this.state.count) # 这里能够到更新后最新的结果 1
})

console.log(this.state.count) # 0
```



#### 多次调用setState问题

- 由于两次setState 都是异步的, 所以两次拿的`count` 都是 0 , 在0 的基础上 +1

```js
 console.log('前', this.state.count) // 0
    // 异步更新
    this.setState({
      count: this.state.count + 1  // 以为是 1
    }, () => {
       console.log(this.state.count)  # 1
    })
    // 异步更新  + 获取 结果
    this.setState(
      {
        count: this.state.count + 1 // 以为是 2
      },
      () => {
        console.log(this.state.count) #  以为是 2 但是结果是 1
      }
    )
// 两次更新 发现结果还都是 1 , 原因是因为 每次获取的this.state.count `都是最开始的 0` ,
// 当执行this.state.count + 1 的时候,一看是异步的都滚一边去, 当回来的时候,都是1
```

解决问题: 获取异步最新的state值

使用场景: 多个setState 出现, 操作`state` 数据时

**函数式参数语法**

- state : 最新的 state
- props: 最新的 props

```js
this.setState((state, props) => {
    return {
        count: state.count + 1
    }
}, () => {
    console.log(this.state.count) 
})
```

基础使用

- 当我们多次操作state 时, react知道我们每次的操作, 会在上次的`setState` 结果出来后, 在此基础上计算
- 所有`setState`的回调都会在所有`setState` 数据修改后才会执行, 也就意味着所有`setState` 的回调函数得到的state是所有setState修改后的结果

```js
  state = {
    msg: 0
  }
  render() {
    return (
      <div>
        <button onClick={this.fn}>点击+1</button>
        <p>{this.state.msg}</p>
      </div>
    )
  }
fn = () => {
	console.log('上面', this.state.msg) # 0
	this.setState(
		(state) => {
			return {
				msg: state.msg + 1
			}
		},
		() => {
			console.log('第一次修改', this.state.msg) # 6
		}
	)

	this.setState(
		(state) => {
			return {
				msg: state.msg + 5
			}
		},
		() => {
			console.log('第二次修改', this.state.msg) # 6
		}
	)
	console.log('下面', this.state.msg) # 0
}

```





## JSX语法的转换过程(了解)

> 演示  : babel中文网试一试 let h1 = <div></div>

- JSX 仅仅是createElement() 方法的语法糖 (简化语法)
- JSX 语法 被 @babel/preset-react  插件编译为 createElement() 方法
- React 元素：是一个对象，用来描述你希望在屏幕上看到的内容
- React 元素 最后 被  `ReactDOM.render(<Child/>,document.getElementById('root'))` 渲染显示到页面

![](./image/jsx.png)



# React 第六天



## 组件更新机制

#### 调用setState

- setState 的两个作用
  - 修改state
  - 重新调用render , 更新组件(UI)
- **过程** : **父组件重新渲染时, 所有的子组件也会重新渲染 -> 有性能问题** 

![](./image/更新机制.png)



## 组件更新性能优化

#### state优化

因为state 发生改变, render 就会重新渲染, 所以 与渲染无关的 数据 就不要放在 state 里

那不放在state里放在哪呢 ?  直接以属性初始化语法, 添加到 组件的身上

在render中没有用到 `age` 如果发生改变也会重新渲染

```js
state = {
    name: '张三',
    age: 80
} 

//
age = 80

render () {
    return <div>{this.state.name}</div>
}

fn = () => {
    this.setState({
        age: this.state.age + 1
    })
}
```





#### shouldComponentUpdate优化

`shouldComponentUpdate() {}` 这个一个生命周期钩子, 在`render` 之前调用

默认不写是`return true`  为 允许更新, 如果`return false` 则不允许更新 , 终止更新

- **组件更新机制** : 父组件更新会引起子组件也被更新
- **问题** : 子组件没有任何变化时, 也会重新渲染
- **如何避免**不必要的重新渲染呢 ? 
- **解决方式** : 使用 钩子函数` shouldComponentUpdate(nextProps, nextState)`
  - nextProps  : 最新的属性
  - nextState : 最新的状态
  - **场景** : 比较更新前后的 state 或者 props 是否相同, 来决定是否 更新组件
- **作用** :  通过返回值 决定该组件是否需要重新渲染, 返回true ,表示重新渲染, false 表示不重新渲染
- **触发时机** : 更新阶段的钩子函数, 组件重新渲染   **前**   执行 
  - 顺序 :  shouldComponentUpdate()   ==> render()  ==>  componentDidMount()
- **演示** : 点击父组件的计算器的数据count

```js
// 演示1 : 子组件里 通过 shouldComponentUpdate()  { return true or false } 
	- true-更新
	- false-不更新

// 演示2 : 获取 父传过来的属性, 奇数更新,偶数不更新,  
  shouldComponentUpdate(nextProps,nextState)
	  - nextProps : 最新的属性
    - nextState : 最新的状态
 - if(nextState.count % 2 == 0) {
        return false    
     }else { 
        return true
     }

// 演示3 : 就一个组件里有number 值, 点击产生随机值, 比较前后生成的随机值是否一致,不一致就更细, 一致就不需要更新
// count : Math.floor(Math.random()*3)
 shouldComponentUpdate(nextProps,nextState) {
     
     //          上一个的值                  最新的值
     console.log(this.state.count === nextState.count)
     
     // 本次的 nextState.number
     // 上一次的 this.state.number
     //  或者 通过 if..else..判断 
     return this.state.count !== nextState.count
 }
```



#### PureComponent 纯组件

功能和`React.Component` 功能一样, 但是它是纯组件, 它内部会对比 `shouldComponentUpdate` , 会自动对比前后props 和 state , 如果值没有变化, 会自动在`shouldComponentUpdate(){}` 中 return false 不调用 render

**作用** : 自动实现了 shouldComponentUpdate() 钩子函数, 不需要再手动对比更新前后的props 或者 state , 来阻止不必要的更新了

**原理** : PureComponent 内部, 会别对比更新前后的props 以及更新前后的state , 只要有一个不同, 就会让组件更新, 只有在两者都相同的情况下, 才会阻止组件更新

```js
import React, {PureComponent} from 'react'
class Hello extends PureComponent {}
```

> 注意: PureComponent 对比的props 和 state  只是浅层比较

像这种state 中 的属性是简单类型, PureComponent 对比是没问题的

但是对于复杂数据类型, 只要地址不发生改变, PureComponent 则认为 state 是没有改变, 时钟不会调用 render

```js
state = {
    count: 0,
    obj: {
        num: 0
    }
}
```

使用新对象让地址改变, 会触发PureComponent 更新

```js
const newObj = {...this.state.obj} // 创建一个新对象

newObj.value = Math.floor(Math.random() * 3)
this.setState({
    obj: newObj
})
```





#### 不可变原则

**不可变原则:  不修改数据, 创建新的**

**对于state 存在复杂数据类型, 要遵循不可变原则**

> 不管是使用Component 还是 PureComponent 都遵循不可变原则
>
> 看到state 对象中有 复杂数据类型, 立刻想到不可变原则

##### 处理对象

**ES5  Object.assign()**

- param1: 目标对象, 后面的参数都会合并到这个新对象里
- param2:  来源对象, 后面的对象都会合并到第一个参数中, 对于前面对象存在属性, 后面的会覆盖前面的

```js
Object.assign({}, this.state.obj, { num: 100 }, ....)
```

**ES6 展开运算符**

```js
this.setState({
    obj: {...this.state.obj, num: 100}
})
```



##### 处理数组

ES5 Array.concat()

concat 会拼接参数组返回一个新数组, 也是一个纯函数

```js
let newArr = this.state.arr.concat(['cc'])
```

ES6 展开运算符

```js
this.setState({
    arr: [...this.state.arr, 'cc']
})
```



## 虚拟DOM的真正价值

- 虚拟 DOM 的真正价值从来都不是性能。
- 真正的价值：虚拟DOM 能够让 React 摆脱浏览器的限制（束缚）。也就是，只要能够运行JS代码的地方，就能够运行 React。
- 跨平台
  - JSX => 虚拟DOM => react-dom  => DOM 元素=> 浏览器 
  - JSX => 虚拟DOM => React-Native => ios和安卓的元素 => 移动混合开发
  - JSX => 虚拟DOM => 工具 => VR





## React-router

#### react-router介绍

- 路由 :  就是一套映射规则, 是url中 `哈希值` 与 `展示视图` 之间的一种对应关系
- 为什么要学习路由 ? 
  - 现代的前端应用大多都是 SPA（单页应用程序），也就是只有一个 HTML 页面的应用程序。
  - 因为它的用户体验更好、对服务器的压力更小，所以更受欢迎。
  - 为了有效的使用单个页面来管理原来多页面的功能，前端路由 应运而生。
- 使用React路由简单来说，就是配置 **路径**   和  **组件**（配对）



 https://github.com/ReactTraining/react-router github仓库地址

react-router 英文官网:  https://reacttraining.com/react-router/web/guides/quick-start 

react-router提供了好几个包, 我们在web开发中使用`react-router-dom` 就可以了, 它也包括了`react-router` 的核心

`React-router`: React-router的核心包

`React-router-dom`:  web 上使用它即可

 [`react-router-native`](https://github.com/ReactTraining/react-router/blob/master/packages/react-router-native) : 在 React-native 上使用

 [`react-router-config`](https://github.com/ReactTraining/react-router/blob/master/packages/react-router-config) : 静态路由的配置



#### react-router-dom使用

> React中的路由都是组件

安装

```js
yarn add react-router-dom
```



`HashRouter/BrowserRouter` : 容器组件, 只有被容器组件包裹, 才可以使用组件, 一个带 # 号 一个不带 # 号

hashRouter是哈希模式, BrowserRouter 是history 模式没有丑陋的# 号



`Link`:  **入口组件** 相当于Vue的`router-link` 默认会渲染成 a 标签, 必须有` to="/home"` 属性指定跳转的url



`Route` : **出口组件(规则 +出口)** , 相当于vue 中的`router-view`, 能渲染APP组件 并且为APP组件`this.props` 注入一些方法history /location/match 等



`NavLink`: 功能和 `Link` 一样, 不过会给当前点击路由添加一个`class="active"` 类名



`Redirect` : 路由重定向`<Redirect to="/home" from="/">` 只有访问`/` 就重定向到`/home` , 要注意的是, 在以前需要`<Switch />` 包裹, 否则就会报错( 现在不会报错了, 已经修复 ), 逻辑类似JS 中的 switch 循环, 只要匹配到一个`case` 就不会在走其他的`case` , 也就意味着`Switch` 内部的路由只能显示一个



在`index.js` 入口文件安装

- `component` : 指定渲染的组件
- `path`: 路由匹配, 分局url 显示的对应的组件, 不加的话, 表示任何url 都匹配

```js
import React from 'react'
import { render } from 'react-dom'

// 路由
import { BrowserRouter as Router, Route } from 'react-router-dom'

import App from './App'
render(
  <Router>
    // 只有访问 / 才会显示App
    <Route component={App} path="/"/>
  </Router>,
  document.querySelector('#root')
)
```



**一个基本的路由跳转实现**

```js
import React from 'react'
import { Route, NavLink as Link, Switch, Redirect } from 'react-router-dom'
// import { BrowserRouter as Router, Switch, Route, Link } from 'react-router-dom'
// 导入组件
import { Home, Article, Users } from './views'
export default class App extends React.Component {
  state = {}
  render() {
    return (
      <div>
        <ul>
          <li><Link to="/home">首页</Link></li>
          <li><Link to="/article">文章</Link></li>
          <li><Link to="users">用户</Link></li>
        </ul>
        <Switch>
          <Route component={Home} path="/home" />
          <Route component={Article} path="/article" />
          <Route component={Users} path="/users" />
          <Redirect to="/home" from="/" />
        </Switch>
      </div>
    )
  }
}
```



#### 路由的执行过程

1. 点击 Link 的时候, 改变入口, url 里的 pathname
2. 一旦改变, 路由就会监听大 pathname的变化
3. 就会找到 `Router` 下的 `Route` , 遍历匹配规则
4. 找到对应的匹配规则, 会继续遍历 `Route` , 匹配所有符合条件`path=""` 也就意味着:一个路径可以匹配多个组件, 
   - 如果想要显示一个, 可以使用`Switch`组件, 匹配到第一个符合条件的后面的就不会匹配

> 在react 中 一个url路径, 可以匹配多个组件, 如果想要匹配一个使用 <Switch>组件





#### 编程式导航

改变入口方式

- 声明式导航
- 编程式导航

在 vue 中 通过`thsi.$router.push()` 编程式导航

在React中 通过`Route` 路由匹配的组件, 在组件内部的`this.props` 就具有`history/location/match` 属性, 正常组件的`this.props ` 则是没有这三个属性的



##### **this.props 中三个重要属性**

`history` : 中的 `push()/go()/goBack()/goForward()/replace()` 方法可以编程式跳转路由



`location` : 记录位置

- pathname: 当前显示的路由url路径
- state: 记录了push(path, state)跳转传递的state参数



`match`: 可以获取参数

- params: 动态路由的参数

```js
<Route path="/detail/:id" component={detail}>
    
 this.props.history.push('/detail/123')
 console.log(this.props.match.params.id) // 123
```





##### history里的重要方法

`history.push(path. state)`

- param1: String类型,  要跳转的url
- param2:  在跳转路由的时候, 可给`location.state`传递参数

```js
this.props.history.push('/two', { name: '聪聪' })
console.log(this.props.location.state) // { name: '聪聪'}
```

`history.replace(path, state)` 直替换掉当前的路由, 不会记录跳转记录,  使用场景: 待支持页面 => 支付成功页面 使用replace 保证不再回到待支付页面

`history.goBack() `: 后退, 直接调用则往前跳转一次, 效果和 go(-1) 一样

`history.goForward()`: 前进, 直接调用, 作用相当于 go(1)

`history.go(1)` : 前进或后退







#### exact 精确匹配

Route默认是模糊匹配, 只要是以`path` 的url 开头就可以匹配, 模糊匹配在嵌套路由中使用

在`<Route exact/>` 则表示完全精确匹配, 对于嵌套路由, 点击子路由, 不在父路由下显示, 则再父路由身上加`exact` 

```js
<Route component={Home} path="/home" />
    
<Route component={Article} path="/article" exact/>
<Route component={ArticleDetail} path="/article/:id"></Route>

<Route component={Users} path="/users" />
<Redirect to="/home" from="/" />
```



#### 嵌套路由

**使用react-router 的 模糊匹配,** 实现嵌套路由

外层有一套路由, 路由里面又有一套路由匹配规则, 只有父路由匹配到了, 才会调用render, 渲染父路由中的子路由Route

所以说react中的嵌套路由, 在他的子路由中的`path="/parent/"`前面必须要带上父路由的路径 => `有爸爸才有儿子`

```js
<Link to="/article/1">文章详情1</Link>
<Link to="/article/2">文章详情2</Link>
<Route component={ArticleDetail} path="/article/:id"></Route>
```



#### 重定向

- **方式1 : render-props**

 ```js
<Route exact path='/'
  render={ () => {
    return <Redirect to='/one' />
	 }
}></Route>
 ```

- **方式2 - children**

```js
<Route exact path='/'>
  <Redirect to='/one' />
</Route>
```

- 方式3

```js
<Redirect to="/home" from="/" exact/>
```



#### 哈希模式和history模式

HashRouter模式

 1. 访问路径 :  http://localhost:8080/#/one 
               			  http://localhost:8080/#/two
 2. 服务器接收到的 (服务器是不会 接收 # 后面的内容的)
 3. 不管访问的路径是什么样的 
     http://localhost:8080  ==> 服务器返回的默认 的就是  index.html
4. 后面的 /one 和 /two 由路由来使用, 根据路由匹配规则找到对应的组件显示
5. 哈希模式 不管是 开发阶段还是发布阶段,都是没有问题的



history模式

1. 访问路径 :  http://localhost:8080/one 
                          http://localhost:8080/two
2. 服务器接收到的 http://localhost:8080/one  和 http://localhost:8080/two
	 		但是，/one 和 /two 这个路径是不需要服务器端做任何处理的。
3.  http://localhost:8080/getNews
    http://localhost:8080/detail 
    它们都是 接口地址  , 后面遇到 类似 /one 和 /two 都会以为是接口 是要返回数据的呢?
3. 所以，应该在服务器端添加一个路由配置，直接返回 SPA 的 index.html 页面就行啦。
5. 类似处理

```js
   app.get('/getNews', (req,res) => {
   // 根据 res 返回 对应的数据
    res.json { .....  }
  })
  app.get('/detail', (req,res) => {
   // 根据 res 返回 对应的数据
    res.json { .....  }
  })

  // 最后 额外再多加一个, 专门用来返回 index.html
  app.use('*', (req,res) => {
    res.sendFile('index.html')
  })

```

总结:

- 开发阶段 : 服务器是本地服务器, webpack脚手架已经处理好了, 
- 发布阶段 : 服务器是公司的服务器, 可能就会报错
- 我们要做的就是`告诉后台`,我们使用的 是 history模式,让他专门处理一下,就可以了
- 如果后台不给处理,或者处理不好, 我们就使用 `哈希模式`





#### 404 匹配

- `/` 的重定向需要`exact` 精确匹配, 除了`/` 和 提供的`path` 都会重定向到`/404`

```js
<Redirect to="/home" from="/" exact/> 
<Redirect to="/404"></Redirect>
<Route component={NotFound} path="/404"/>
```





# React 第七天

## Redux 状态管理

#### 引入 ->纯函数

> 纯函数是这样一种函数，即相同的输入，永远会得到相同的输出，而且没有任何可观察的副作用 

 比如 `slice` 和 `splice`，这两个函数的作用并无二致——但是注意，它们各自的方式却大不同，但不管怎么说作用还是一样的。我们说 `slice` 符合*纯*函数的定义是因为对相同的输入它保证能返回相同的输出。而 `splice` 却会嚼烂调用它的那个数组，然后再吐出来；这就会产生可观察到的副作用，即这个数组永久地改变了 

```js
var xs = [1,2,3,4,5];

// 纯的
xs.slice(0,3);
//=> [1,2,3]

xs.slice(0,3);
//=> [1,2,3]

xs.slice(0,3);
//=> [1,2,3]


// 不纯的
xs.splice(0,3);
//=> [1,2,3]

xs.splice(0,3);
//=> [4,5]

xs.splice(0,3);
//=> []
```





#### redux

redux本身和 react没有关系, 需要手动连接store , 所以我们使用react-redux自动连接store

Redux = Flux +reducer(函数式编程)

## **Redux 三个核心概念**

#### action - 提出想法

- 动作想法, 是用来描述要做的事情
  - 比如 : 计算器案例中的 +1, 点击按钮后 , 计算器的数值就会增加1, 在这个过程中, +1 就是一个action
  - 比如 : 登录功能中, 登录也是 一个 action
  - 比如: 添加任务,删除 任务,切换任务 都是 action
- 注意 : action 仅仅是用来描述要做的什么事情,  但是 , action并不会去完成这个功能
  - 举个例子 : 就想`砖`家 一样,  只是提出 想法, 但是不干活

#### reducer - 实现想法

- 用来实现具体的 action (动作)
- 可以把 reducer 想象成 搬砖的 (干活的人), 是用来完成 `砖家`  提出来的想法的

#### store - 管理者

- 仓库 :  用来 将 action 和 reducer 关联在一起
- 可以把 store 想象成`管理者(老板)`, 负责 将 `砖家` 提出来的想法 告诉 `搬砖的(干活的人)`,  由搬砖的人来完成`砖家` 提出来的想法



## 从代码角度来看三个核心概念

#### action 

- action 实际上就是 一个普通的js对象
- 作用 :  用来描述 要执行的动作 (任务)
- 约定1 : 必须提供 type 属性, 用来表示 任务类型
- 约定2 : type 属性的值(类型), 是一个字符串 应该使用 `大写字母` 表示
  - 如果有多个单词 , 多个单词之间通过 _ (下划线) 来链接
- 约定3 : 可以在 action 中携带体外的数据, 作为完成该功能需要用到的数据

```js
// 计算器案例 : +1  increment
{ type : 'INCREAMENT' }

// 添加任务
{ type : 	'ADD_TODO', text:'学习redux' }

// 删除任务
{ type : 'DELETE_TODO', id:2 }

```

#### reducer

- reducer 实际就是一个普通的js函数
- 作用 : 完成 action 的功能
- 因为要实现 action 中 提出的想法, 所以需要将 **action 传递给 reducer**
- 因为 redux 是用来进行状态管理的, 所以 reducer在完成某个 action 的时候 , 就需要操作状态, 也需要将**state 作为参数传递给 reducer** 
- 因为 reducer 是用来 实现某个具体的 action , 所以 这个返回在完成了某个 action 之后, 需要讲最新的状态返回, 因此需要有返回值, 返回值就是最新的状态
- reducer 的函数 签名 : `(oldState, action) => newState`
- 也就是说 : 状态的变化时在 reducer 中完成的
- 注意 : reducer函数, 一定要返回 状态 , 这样才能保证 redux 一直都有状态
  - 因此, 需要给 switch-case 添加 default , 用来返回默认的state
- 注意 : reducer 是一个纯函数 
  - 1 不要直接修改参数, 也就是不要修改 参数  state,  而是要创建新的state
  - 2 不要再函数里使用 不纯的操作
    - 比如 : Math.random() / new Date() / 发送ajax 请求, / 操作全局变量

```js
// todos 案例：
// 因为 todos 是一个列表，所以，todos的数据应该是一个：数组（ [] ）
// 所以，todos 的默认值应该是一个 数组
// 数组中的每一项都是一个对象，对象的结构：
// text 表示任务名称
// done 表示任务完成状态，是一个布尔值
// { id: 2, text: 任务名称, done: false }

const reducer = (state, action) => {
  switch (action.type) {
      
    case 'ADD_TODO':
      // 添加任务的逻辑代码
      return [...state, { id: id, text: action.text, done: false }]
      
    case 'DELETE_TODO':
      // 删除任务的逻辑代码
      return state.filter(item => item.id !== action.id)

    default:
      return state
  }
}
```

- 纯函数的特点 : 相同的输入 必定得到相同的输出
  - 开始的介绍可预测

```js
// 纯函数：
function fn(a) {
  return 1 + a
}

fn(2) // 3
fn(2) // 3
fn(2) // 3
fn(2) // 3

// 不纯的操作：
function foo(a) {
  return Math.random() + a
}

fn(2) // 2.1231923912983
fn(2) // 2.8909810320912
fn(2) // 2.3213982098401
```



#### store

- store 就是一个对象, 用来将 action 和 reducer 关联在一起
- 注意 : 一个 reducer 应用中只能有一个 store
- store 是通过 redux 中的 createStore来创建的

```js
import { createStore } from 'redux'

// 参数是 reducer
const store = createStore( reducer )

// 执行一个动作：分发动作
store.dispatch( { type: 'ADD_TODO', text: '学习redux' } )
```



## createStore()

createStore能够创建一个store 

- 参数1: reducer
- 参数2: 初始值
- 参数3: 中间件  

```js
const store = createStore(reducer, todos_state)
```



## react-redux

本身`redux `和 `react` 之间没有什么练习, 只能强项导入, 使用`store` ,且无法实现单向数据流的思想, 所以这时候react-redux 就出现了, 它能够把

#### 安装使用

```js
yarn add react-redux
```

#### 使用步骤(购物车案例)

##### 创建store

1. 根目录下创建`store`  -> **需要合并后的reducer**
   - 全局唯一数据源`state`, 使用`createStore` 创建store
   - 在这里引入合并后的`reducer` 

```js
// createStore 是react-redux 用于创建store的方法, 这个
import {createStore} from 'redux'

// 引入合并后的reducer
import rootReducer from './reducers'

// createStore 的第一个参数必须是一个reducer, 如果是多个, 请在reducers目录下先使用combineReducers合并之后在导出 
export default createStore(rootReducer)
```



##### 创建并合并reducer

2. 在`reducers`目录下创建`index.js`并导出合并后的reducer

- 实际中, 可能存在多个`reducer` 我们都可以在`index.js` 中合并之后统一导出
- 在`index.js` 中导入`reducer`通能过`redux` 提供的`combineReducers` 合并所有的`reducer`

```js
// 在实际的项目中, 由于只有单一的store, 但是状态由很多分类, 所以需要划分reducer, 但是createStore的参数只接收一个reducer, 所以, redux聪明的提供了一个用于合并多个render的方法. 注意:不要手动合并
import { combineReducers } from 'redux'

// 引入 cart reducer , 如果有多个, 继续引入
import cart from './cart'

// 导出合并后的reducer
export default combineReducers({
  // 把多个reducer作为combineReducers 的对象参数传入即可, 在外部就可以通过store.getState().cart 来获取到cart reducer 里的state数据 
  cart
})

```



3. 在`reducers`目录下创建reducer `cart.js` -> **在具体的`reducer` 中需要action和 初始state**

- `state` 要给一个初始状态
- 创建的`reducer` 必须是一个纯函数
- 在根据不同的`action` 做不同的处理返回不同的`state`

```js
// 为了避免actionType重复, 所以一般会把actionType放在一个文件统一管理, 也可以避免写错actionType
import actionType from '../actions/actionType'
// 对于购物车来说这是一个初始化状态
const initState = [
  {
    id: 1,
    title: 'Apple',
    price: 888,
    amount: 10
  },
  {
    id: 2,
    title: 'oriange',
    price: 999,
    amount: 10
  }
]

// 创建购物车的 reducer 是一个纯函数, reducer的固定写法是: 
// 两个参数, 第一个参数就是state并有初始值, 第二个是action
export default (state = initState, action) => {

  // 根据不同的action, 做不同的处理, 每一次返回一个新的state, 返回的类型要一样
  switch (action.type) {
    case actionType.CART_AMOUNT_INCREMENT:
      return state.map((item) => {
        console.log('加')
        if (item.id === action.payload.id) {
          item.amount += 1
        }
        return item
      })
    case actionType.CART_AMOUNT_DECREMENT:
    return state.map((item) => {
      console.log('减')
      if (item.id === action.payload.id) {
        item.amount -= 1
      }
      return item
    })

    // 一定要有default, 当actionType不对时, 就不做处理, 返回上一次的state
    default:
      return state
  }
}

```



##### 定义actionCreator

4. 在`src` 目录下创建`action`目录, 创建统一的`actionType.js`

- 为了避免actionType重复, 所以一般会把actionType放在一个文件统一管理, 也可以避免写错actionType

```js
// 为了避免actionType重复, 所以一般会把actionType放在一个文件统一管理, 也可以避免写错actionType
export default {
  CART_AMOUNT_INCREMENT: 'CART_AMOUNT_INCREMENT',
  CART_AMOUNT_DECREMENT: 'CART_AMOUNT_DECREMENT'
}
```



5. 在`action` 目录下创建`cart.js` 对应的actionCreator

- 有两种写法, 实际工作第二种常用
- 这个文件的作用: 给组件的`action`

```js
// 提供actionType
import actionType from './actionType'


// 第一种写法: 这是标准写法, 但是不方便传递动态参数
// export const increment = {
//   type: actionType.CART_AMOUNT_INCREMENT
//   payload: {
//     id
//   }
// }


// 在实际工作中, 常用的一种方式actionCreator, 它是一个方法, 返回一个对象, 这个对象才是真正的action, 能够传递动态参数 
export const increment = (id) => {
  // console.log(id)
  return {
    type: actionType.CART_AMOUNT_INCREMENT,
    payload: {
      id
    }
  }
}

// 导出减的方法
export const decrement = (id) => {
  // console.log(id)
  return {
    type: actionType.CART_AMOUNT_DECREMENT,
    payload: {
      id
    }
  }
}

```



=================== 经历上述步骤, redux 则创建完毕, 可以使用=========================

##### 使用Provider

6. 使用`react-redux` 提供的`Provider` 组件, 传递唯一数据源`store`
   - 需要入口文件`index.js`引入创建的`store`
   - 使用`Provider` 组件包裹, 传递`store`
   - **只要在最外层包裹Provider, 所有后代组件都可以使用Redux.connect连接到store **

```js
import React from 'react'
import { render } from 'react-dom'

// Provider 是 react-redux提供的组件, 类似于context 上下文传递数据
import { Provider } from 'react-redux'

import App from './App'
import store from './store'

// 把store中的数据传递给APP
render(
  // 一般把store 放在应用程序的最顶层, 这个组件必须有store属性, 这个store属性就是我们创建的store
  // 只要在最外层包裹Provider, name所有后代组件都可以使用Redux.connect连接到store 
  <Provider store={store}>
    <App />
  </Provider>,
  document.querySelector('#root')
)

```



##### 在组件中使用改变store

7. 在组件`cartList`中使用redux
   - 使用react-redux提供的`connect` 连接 store
   - 导出`action` 
   - 给组件`props`注入store中的state 和 dispatch 方法

```js
import React from 'react'

// conect方法执行之后是一个高阶组件
import { connect } from 'react-redux'

// 导入 actionCreators
import { increment, decrement } from '../../actions/cart'

class CarList extends React.Component {
  render() {
    // 就多了 dispatch 方法
    console.log('props',this.props)
    // console.log(connect())
    return (
      <div>
        <table>
          <thead>
            <tr>
              <th>ID</th>
              <th>商品名称</th>
              <th>价格</th>
              <th>数量</th>
              <th>操作</th>
            </tr>
          </thead>
          <tbody>
            {this.props.carList.map((item) => (
              <tr key={item.id}>
                <td>{item.id}</td>
                <td>{item.title}</td>
                <td>{item.price}</td>
                <td>
                  <button
                    // onClick={() => {
                    //   // this.props.dispatch(decrement(item.id))
                    //    // mapState 传第二个参数
                    //   this.props.decrement(item.id)
                    // }}

                    // 改写 
                    // onClick={() => this.props.decrement(item.id)}
                    onClick={this.props.decrement.bind(this, item.id)}
                  >
                    -
                  </button>
                  <span>{item.amount}</span>
                  <button
                    onClick={() => {
                      // mapState 不传第二个参数
                      // this.props.dispatch(increment(item.id))
                      // mapState 传第二个参数
                      this.props.increment(item.id)
                    }}
                  >
                    +
                  </button>
                </td>
                <td></td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
    )
  }
}

// 这里的state实际上就是store.getState()的值
const mapStateToProps = (state) => {
  console.log('mapStateToProps', state)
  // 这里return了什么, 在组件里就可以通过this.props获取到
  return {
    carList: state.cart // 则props就有 carList
  }
}
// 不传第二个参数, 自动具有dispatch 方法
// export default connect(mapStateToProps)(CarList)
/* 
  connect 有四个参数, 常用就是前面两个参数
  param1: mapStateToProps: 作用就是从store里把state注入到当前的组件的this.props上 
  param2: mapDispatchToProps: 默认不传是注入dispatch, 可以把action生成的方法注入到当前组件的props上,
  一般第二个参数传递一个对象, 这个对象里就是actionCreateors, 只要传入了actionCreators, 在组件内就可以通过this.props.actionCreator() 调用, 调用之后, 那个actionCreator就会自动帮你把它内部的action dispatch出去
*/
// 传递第二个参数
export default connect(mapStateToProps, { increment, decrement })(CarList)

```





#### 异步action

同步Store流程: actionCreator -> 自动dispatch(action) -> reducer -> store -> view

异步:  actionCreator -> middleWare处理生成新的action -> 手动dispatch(action) -> reducer -> store -> view

借助 middleWare 中间件处理 异步 action => `react-thunk` 中间件实现 异步action

#### react-thunk 

```js
yarn add redux-thunk
```

在`store.js`中redux 中引入 `applyMiddleware`

```js
import { createStore, applyMiddleware } from 'redux'

// 导入合并后的 reducer
import rootReducer from './reducers'

// 导入react-thunk
import Thunk from 'redux-thunk'

export default createStore(rootReducer, applyMiddleware(Thunk))
```



定义异步actionCreator

```js
export const decrementAsync = id => dispatch => {
  setTimeout(() => {
    dispatch(decrement(id))
  }, 2000)
}
```





# React 十二天

## 环境变量和axios优化

### 项目开发的两个环境

- 开发环境 ( development ) : 项目开发期间的环境
  - 给开发人员使用
  - 开发环境 一般就是 由  脚手架 搭建起来的
- 发布环境 ( production ) : 线上环境, 也就是项目完成后, 打包上线的环境
  - 给用户使用
  - `yarn build`打包上线的环境
- 预发布环境 : 测试环境 , 灰度环境(预上线环境) => 测试阶段



## 环境变量

在实际工作中, 可能会有不同的环境下存在不同的接口.....

- 在不同的环境中, 有不同的内容 , 比如 : 接口地址、数据库等
  - 注意 : 接口地址等需要根据环境来作区分的内容,,,,不要写死在项目里,  而应该将其作为配置, 
  - 脚手架中一般都是会提供着这样的 环境变量 的配置,   用来分区不同的环境,  
  - 在 React 脚手架中, 不同的环境有不同的配置文件
- 开发环境的配置文件名称 : ` .env.development `(开发环境读取该配置)
- 生成环境的配置文件名称 : `.env.production` (项目打包上线读取该配置项)
- 在不同环境的配置文件中, 分别配置 环境变量 , 比如 接口: `REACT_APP_URL`
  - 开发环境中配置 : REACT_APP_URL = http://localhost:8080
  - 发布环境中配置 : REACT_APP_URL = http://api.xx.com
- 注意：环境变量的名称相同，值是不同的！！！，将来代码中就可以读取到相同的键，来拿到不同的接口地址了



## 配置环境变量

- ① 在项目根目录创建文件  **.env.development**
- ② 在该文件中添加环境变量  **REACT_APP_URL**   (注意 : 环境变量必须约定以 REACT_APP_开头)
- ③ 设置  REACT_APP_URL 的值 为  : http://localhost:8080

```js
# 为开发环境提供环境变量
REACT_APP_URL=http://localhost:8080    (不是字符串)
```

- ④ 重新启动脚手架 
  - `yarn start`
  - 重启后, 才会重新读取目录, 读取`.env.development/production` 文件通过node中的`process`模块读取
- ⑤ 在 **utils/url.js** 文件中,  创建 BASE_URL 变量,  设置其值为 `process.env.REACT_APP_URL`

```js
const BASE_URL = process.env.REACT_APP_URL
// process 是 Node 提供的用来获取当前进程的对象
// 打印 process
```

- ⑥ 导出 BASE_URL

```js
export { BASE_URL }
```

- ⑦ 使用 BASE_URL  修改图片地址

```js
//  utils/index.js 引入
import { BASE_URL } from './utils/url.js'

// 引入 import {BASE_URL } from './urils/urils' 太长了,而且 './urils' 已经引入过了, 可以不用在引入这么多次了, 所以可以在 index.js 里面引入在导出
export { BASE_URL } from './url'

// 那以后引入使用
import { BASE_URL } from './utils'

// 使用 : 以后图片
<img src={ `${BASE_URL}${item.imgSrc}` } />  或者
<img src={ BASE_URL + item.imgSrc  } />

// 尝试修改  Index 组件里面的
```



#### react 脚手架中的环境变量说明

- 1 当运行命令 `yarn start` 的时候，脚手架就会读取：`.env.development` 这个配置文件中的环境变量
- 2 当运行命令 `yarn build` 的时候，脚手架就会读取：`.env.production` 这个配置文件中的环境变量



## axios 优化

- ① 在 utils/api.js 文件中, 导入 axios 和 BASE_URL
- ② 调用 axios.create() 方法创建一个 axios 实例
- ③ 给 create() 方法, 添加 配置 baseURL, 值为 : BASE_URL,   并且导出

```js
const API = axios.create({
	baseURL : BASE_URL
})
export { API }

// 在 utils/index.js  导入立马导出
export { API } from './api.js'
```

- ④ 导入 API , 使用 API 代替 axios , 去掉接收地址中的 http://localhost:8080

```js
import { API  } from '../utils'

// 请求
const res = await API.get('/home/groups')

// 尝试修改  Index 组件里面的
```



## 备

- 环境变量 =>Index => 测试图片使用 BASE_URL 替换 http://localhost:8080
- axios优化 => Index => 使用API 替换 axios+基路径http://localhost:8080
- 复习以前vue 处理 基本路径的

```js
// app.js 
import axios from 'axios'

axios.defaults.baseURL = localhost:8080
再把设置好基准路径的axios 添加到vue的原型上
Vue.protoType.$axios = axios

因为 所有 的vue实例组件都是继承 Vue的, 所以所有的组件内 
this.$axios 都是可以直接使用的有基准路径的axios

```





# React 第十五天

## 动画库

## react-spring



## react-motion 





## formik 表单验证



# React 十七天

## 防抖(输入框防抖 -- 面试)

在输入框中,使用防抖, 保证只会发送最后一次的请求

```js
cleartimeout(this.timeId)
this.timeId = setTimeout(() =>{
    // 发送请求
    
}, 500)
```



方式2: lodash库 (面试会涉及) 

使用函数的方法`_.debounce()`



## 节流(按钮节流)

一般可以应用在点击获取验证码, 规定时间内不允许在点击

```js
<button onClick={this.fn}>节流的演示</button>

isOk = false

fn = () => {
    if (this.isOk) {
      return
    }

    console.log('-------------------')

    // 发送请求了
    this.isOk = true
    console.log('我要发送请求了')
    setTimeout(() => {
      console.log('请求结束了')
      this.isOk = false
    }, 5000)
  }
```



# React 二十一天

## 中间件

- [redux、express中间件对比](https://www.jianshu.com/p/922194db2ae2)
- redux 中间件采用的是 洋葱模型
- 中间件实际上就是 扩展了 store.dispatch
  - 注意：使用中间件后，我们调用 store.dispatch 就不再是 redux 默认的dispatch了，而是，中间件包装后的dispatch
- 中间件的执行时机：

```js
// 没有中间件： dispatch 直接将 action 传递给 reducer
store.dispatch ----> reducer

// 有了中间件： dispatch 没有直接将 action 传递给 reducer，而是，先执行中间件的代码，等到所有的中间件都执行完成后，才会将 action 传递给 reducer
store.dispatch ----> 中间件1 -> 中间件2 -> 中间件3 ----> reducer
```

### redux 中间件原理

- 一个中间件就是包装了 store.dispatch（也就是redux原生的dispatch），并且，会返回一个新的函数，这个新的函数，就做为了新的 store.dispatch
- 也就是说：只要使用了中间件，我们再拿到的 store.dispatch 就不再是原生的dispatch，中间件，包装后的dispatch



**[express 中间件 和 redux 中间件](https://www.jianshu.com/p/922194db2ae2)**

express 是 线性模型, redux中间件是洋葱模型



## redux 中间件使用1 - redux-logger

> createStore.js 文件

- 安装中间件 : `yarn add redux-logger`

```js
import logger from 'redux-logger'
```

- 导入redux中的一个函数：`applyMiddleware`

```js
import { applyMiddleware } from 'redux'
```

- 2 将创建好的中间件或者第三方的中间件，作为参数传递给 applyMiddleware

```js
const middlewares = applyMiddleware(logger)
```

- 3 将 middlewares 传递给 createStore，作为它的第三个参数

```js
const store = createStore(reducer, initialState, middlewares)
```



## redux 中间件使用2-redux-thunk(异步action)

#### 1.介绍使用

- 默认情况下 : redux 自身只会处理同步数据流
- 但是,如果涉及到异步操作, 就应该使用`redux-thunk` 这种中间件,来处理异步数据流
- 作用 : 用在 在 redux 中 处理异步数据流

```js
// 没有使用 redux-thunk 时候, 处理同步数据的 action
const addTodo = (text) => ({ type : 'ADD_TODO',text })

// 有了 redux-thunk 以后,  处理异步数据的 action
const addTodoAsync = (text) => {
  
  return (dispatch) => {
   // 在此处,就可以处理异步操作了
   setTimeout(()=>{
     
     dispatch( addTodo(text) )
   },3000)
    
  }
}
```

#### 2. redux-thunk 具体使用步骤

- 安装 : `yarn add redux-thunk`
- 在 configStore.js 到中 导入thunk
- 
- 将thunk 作为中间件, 传递给 store

```js
import thunk from 'redux-thunk'

const middlewares = applyMiddleware(thunk, logger)
  
// 之前的效果还有,说明 thunk 不会对我们之前写的同步有影响
```

- 在 actions 中 创建 异步 action, 用来封装异步操作

```js
// 添加异步 action 实现异步添加任务的操作
const addTodoAsync = text =>{
  return dispatch => {
    setTimeout(() => {
      
      dispatch(addTodo(text))
    }, 3000);
  }
}
// 导出
export { addTodoAsync,....., setVisibilityFilter }
```

- 在 AddTodo.js 使用

```js
// 引入
import { addTodo, addTodoAsync } from '../actions'

// 分发动作
dispatch(addTodoAsync(value))
```



#### 3. axios 发送请求示例

```js
export const ml_todoList = list => ({ type: TODO_LIST, list })

// 异步获取todos数据
export const ml_todoListSync = () => {
  return async dispatch => {
    const res = await axios.get(`https://jsonplaceholder.typicode.com/todos`)
    let list = res.data.slice(0, 10)
    dispatch(ml_todoList(list))
  }
}
```



## redux 中间件使用3 - redux-devtools

### 1. 安装插件

- 链接 : https://github.com/zalmoxisus/redux-devtools-extension
- 安装的工具,不能使用

### 2. 没有其他中间件

```js
const store = createStore(
  reducer,
  initTodos,
  window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()   #+++
)
```



### 3. 有其他中间件

- 安装插件 : `yarn add redux-devtools-extension`
- 使用

```js
import { createStore, applyMiddleware } from 'redux';
import { composeWithDevTools } from 'redux-devtools-extension';

const middlewres = applyMiddleware(logger, thunk, window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__())

const store = createStore(
  reducer,
  initTodos,
  composeWithDevTools(middlewres)       # ++++ 
)
```







## React-hooks

 *Hook* 是 React 16.8 的新增特性。它可以让我们在函数组件中使用类似`class`组件的`state`

 Hook 为已知的 React 概念提供了更直接的 API：props， state，context，refs 以及生命周期 

>  Hook 在 class 内部是**不**起作用的。但你可以使用它们来取代 class 。 

![](./image/useState和useEffect.png)



### useState

 **`调用 useState` 方法的时候做了什么?** 

 它定义一个 “state 变量”。我们的变量叫 `count`， 但是我们可以叫他任何名字，比如 `banana`。这是一种在函数调用时保存变量的方式 —— `useState` 是一种新方法，它与 class 里面的 `this.state` 提供的功能完全相同。一般来说，在函数退出后变量就就会”消失”，而 state 中的变量会被 React 保留。 



 **`useState` 需要哪些参数？** 

`useState(number/string)` 方法里面唯一的参数就是初始 state。不同于 class 的是，我们可以按照需要使用数字或字符串对其进行赋值，而不一定是对象。在示例中，只需使用数字来记录用户点击次数，所以我们传了 `0` 作为变量的初始 state。（如果我们想要在 state 中存储两个不同的变量，只需调用 `useState()` 两次即可。） 



 **`useState` 方法的返回值是什么？**

 返回值为一个数组：当前 state 以及更新 state 的函数。这就是我们写 `const [count, setCount] = useState(初始state)` 的原因。这与 class 里面 `this.state.count` 和 `this.setState` 类似，唯一区别就是你需要成对的获取它们。

```js
import React, { useState } from 'react';

function Example() {
  // 声明一个新的叫做 “count” 的 state 变量
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

****

**多次调用setCount**

在一个函数中多次调用 `setCount()` 时, 会和 `setState` 一个数据更新是异步的, 只会拿到原来的值, 得到的结果是相同,如果想要得到上一个`setCount` 的 state , 可以采用第一个参数为函数式

```js
<button onClick={() => {
    setCount((count) => {
        count + 1
    })
    setCount((count) => {
        count + 1
    })
}}>
```





### useEffect

你可以把 `useEffect` Hook 看做 `componentDidMount`，`componentDidUpdate` 和 `componentWillUnmount` 这三个函数的组合。 

在初次渲染和`state` 更新都会触发`useEffect( () => {} )`

函数的返回值, 将会在组件卸载时调用(`相当于调用了componentWillUnmount`)

```js
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // Similar to componentDidMount and componentDidUpdate:
  useEffect(() => {
    // Update the document title using the browser API
    document.title = `You clicked ${count} times`;
      
    # 挂载  
    window.addEventListener('mousemove', handleFn)
    
      # return 的函数会在组件卸载时调用
    return () => {
        window.removeEventListener('mousemove', handleFn)
    }
  }, [count]) # 参数2: 依赖项, 决定 return 的函数执行与否
  
  handleFn = () => { console.log('哈哈') }
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```



**useEffect参数**

- param1:  箭头函数 ( componentDidMount , componentDidUpdate)  return 值为 componenetWillUnmount
- param2:  [依赖项]
  - 当依赖项数据发生变化, useEffect 里的函数就会执行
  - 如果不发生变化,  return 的函数则不会执行



**effect的条件执行**

- 默认情况下，effect 会在每轮组件渲染完成后执行
- 但是 不是每次都需要执行的, 比如在上一章的注册鼠标移动事件, 每次组件更新都会注册一次
- 要实现这一点，可以给 useEffect 传递第二个参数，它是 effect 所依赖的值数组

```js
// 注册事件
useEffect(() => {
  console.log('注册')

  window.addEventListener('mousemove', handleMousemove)
  return () => {
    window.removeEventListener('mousemove', handleMousemove)
  }
}, [参数2 为依赖项])

// 比如使用count 

useEffect({

},[count])  
// 当 count 发生变化的时候才会出执行, 
// 如果count 不变就不需要执行

```

- 此时，只有当 `参数2 依赖项` 改变后才会重新创建订阅。

  - 如果你要使用此优化方式，请确保数组中包含了所有外部作用域中会发生变化且在 effect 中使用的变量
  - 如果想执行只运行一次的 effect（仅在组件挂载和卸载时执行），可以传递一个空数组（[]）作为第二个参数 (这就告诉 React 你的 effect 不依赖于 props 或 state 中的任何值，所以它永远都不需要重复执行)
  - 依赖项数组不会作为参数传给 effect 函数

- 改造之后 : 

  ```js
  // 添加标题
  useEffect(() => {
    document.title = `你点击了${count}次`
  }, [count])    # 这里添加
    
  // 注册事件
  useEffect(() => {
    console.log('注册')
    
    window.addEventListener('mousemove', handleMousemove)
    return () => {
      window.removeEventListener('mousemove', handleMousemove)
    }
  }, [])   # 这里添加
  ```





### useContext

3.1 介绍

- useContext 用来简化 context

3.2 回忆

```js
// 第一步: 创建 context
const context = React.createContext()

class Child22 extends React.Component {
  render() {
    return (
      <context.Provider value="123">
        <div>
          context-类 <One></One>{' '}
        </div>
      </context.Provider>
    )
  }
}
class One extends React.Component {
  render() {
    return <context.Consumer>{data => <div>传递:{data}</div>}</context.Consumer>
  }
}
```



3.3 使用 useContext 改造

- 切记 : hook 是用在函数组件里的, 所以一定要把 Three 组件改为 函数组件,不然会有提示
- `Invalid hook call. Hooks can only be called inside of the body of a function component`

```js
// 第一步: 创建 context
const context = React.createContext()

const Child11 = () => {
  return (
    // 第二步 : 包裹
    <context.Provider value="666">
      <div>
        context-fn <One></One>{' '}
      </div>
    </context.Provider>
  )
}
const One = () => {
  // 第三步 : 返回值
  const value = useContext(context)

  return <div>传递 : {value}</div>
}
```



### useReducer

**4.1 介绍**

- 使用 useReducer 替代 redux 

**4.2 redux 回忆**

```js
// 创建 store
import { createStore } from 'redux'
// rducer
let reducer = (state, action) => {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 }
    case 'decrement':
      return { count: state.count - 1 }
    default:
      return { count: state.count }
  }
}
// 初始值
let initialState = { count: 100 }
// 创建 store
const store = createStore(
  reducer,
  initialState,
  window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
)
// 监听数据的变化
store.subscribe(() => {
  console.log('数据变化', store.getState())
})

//2. 创建组件
const Child = () => {
  return (
    <div>
      <div>Count:{store.getState().count}</div>
      <button onClick={() => store.dispatch({ type: 'increment' })}>+1</button>
      <button onClick={() => store.dispatch({ type: 'decrement' })}>-1</button>
    </div>
  )
}
```



**4.3 使用 useReducer 改造 redux**

```js
//1. 引入包
import React, { useReducer } from 'react'

// reducer
const reducer = (state = 1, action) => {
  switch (action.type) {
    case 'increment':
      return state + 1
    case 'decrement':
      return state - 1
    default:
      return state
  }
}

//2. 创建组件
const Child = () => {
  const [state, dispatch] = useReducer(reducer, 1)

  return (
    <div>
      函数组件 {state}
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>1</button>
    </div>
  )
}
```

