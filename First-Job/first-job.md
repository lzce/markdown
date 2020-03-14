# Vue-element-admin
【文档教程】https://juejin.im/post/59097cd7a22b9d0065fb61d2

这是一个后台管理系统的模板框架，里面有许多实用常见的功能。

## 项目拉取
```js
git clone git@github.com:PanJiaChen/vue-element-admin.git
```
## 入职开发流程
到公司的第一天该干的事情
环境 -> 项目仓库(账密) -> clone 项目 -> 分析项目 -> 改BUG or 新功能

- 项目私有仓库：gitolite / gogs / 码云 / gitlab
- 公司分配给你：私有仓库的账号密码
- 分析项目：技术栈 package.json

## 开发环境 
node：是前端开发环境必须的，有必要了解一下node的版本，注意**环境变量**

git：也是必须的，主要是命令行、客户端，也有可能是SVN

VScode： 开发工具

chrome: 调试环境，包括相应的插件（Vuedetools等）

## 拿公司项目
项目仓库是私有的
仓库中可能存在多个项目，每个项目都有自己的仓库地址

项目老大会给我们分配一个管理项目的用户名和密码，可以通过这个用户名看对应的项目（clone、push、pull）

1. 通过公司给的仓库账号密码，`git clone 仓库地址`拉取项目
2. `npm i` 下载依赖包

## 分析项目
1. 搞清楚项目技术栈
2. 跑通项目的具体功能开发流程（可以问项目老大）

### 以vue-element-admin为例
组件中的事件处理函数 dispatch -> store 中 action -> 涉及到发请求 -> 在api文件中定义发送请求的方法 -> 在request中axios.create()

- 页面组件 -> 负责页面展示
  - 事件处理函数dispatch 到 vuex action中
- action 中封装为promise
  - 请求 -> api
  - api -> request
  

## 权限控制
之前做的vue后台管理系统权限控制

- 权限
- 角色
- 用户

为用户分配角色,为角色分配权限,间接的为用户分配权限

用户显示的菜单是服务器直接返回的, 菜单又是路由的地址, 导致前端路由跳转依赖后端, 后端路由依赖前端

- *vue-element-admin* 中的权限控制
前端控制完整的路由表

- `router.addRoutes`是vue-router提供动态添加路由的一个API
  - 参数是一个数组, 符合规则的路由规则数组

## mockjs
[文档示例](http://mockjs.com/examples.html)
能够拦截Ajax请求

## el-scrollbar element-ui隐藏组件
这是element-ui的隐藏组件,官方没有文档,但是可以直接使用

[参考文档](https://segmentfault.com/a/1190000015068613)

