# NodeJs 社区项目



## 项目搭建

### 创建相关的文件目录

**创建主文件夹**

```shell
$ mkdir blog
```

**创建初始化package.json**

```shell
$ npm init -y
```

**下载express和 mongoose**

```shell
$ npm i express mongoose
```

**创建一个Git仓库**

```shell
$ git init
#git忽略文件
.gitignore
```



## 创建`app.js` 服务器

### 开放静态资源

```js
app.use('/public/', express.static(path.join(__dirname, './public/')))
app.use('/node_modules/', express.static(path.join(__dirname, './node_modules/')))
```



## 页面的渲染

### 子模板

对于公共的头部和底部, 可以使用子模板(include)引入页面中

```js
//语法

{{ include '公共页面.html' }}
```



### 继承模板(extend)

对于继承的模板, 公共部分不会重复加载, 只需要在需要继承的页面中, 挖坑`block`  在继承的页面中把自己独有的地方天入相应的坑中

```js
{{ extend 'contend' }}
//自己的css样式
{{block 'head'}}{{/block}}
                  
                  
{{block 'body'}}{{/block}}
<script src="/node_modules/jquery/dist/jquery.js"></script>
<script src="/node_modules/bootstrap/dist/js/bootstrap.js"></script>
 //自己的script                 
{{block 'script'}}{{/block}}
```





## 路由设计

| 路径      | 请求方法 | get参数 | post参数                     | 是否需要权限 | 备注         |
| --------- | -------- | ------- | ---------------------------- | ------------ | ------------ |
| /         | GET      |         |                              |              | 渲染首页     |
| /register | GET      |         |                              |              | 渲染注册页面 |
| /register | POST     |         | email , nickname ,  password |              | 处理注册请求 |
| /login    | GET      |         |                              |              | 渲染登录页面 |
| /login    | POST     |         | email , password             |              | 处理登录请求 |
| /logout   | GET      |         |                              |              | 处理退出请求 |





