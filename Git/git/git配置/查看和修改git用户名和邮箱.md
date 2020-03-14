### git仓库用户名和git用户名
git仓库用户名和git用户名不是一个东西：
- git仓库用户名：git仓库用户名和密码只用于登陆git仓库，或者使用http方式访问git仓库代码时需要使用git仓库用户名密码。git仓库
- git用户名：在代码的版本历史中显示的用户名，便于团队开发时其它成员能够识别代码的修改者。

本文之后的用户名都指的是git用户名。


### 用户名和邮箱地址的作用
用户名和邮箱地址是本地git客户端的一个变量，不随git库而改变。每次commit都会用用户名和邮箱纪录。github的contributions统计就是按邮箱来统计的。




### 查看项目用户名和项目邮箱
```
$ git config user.name
$ git config user.email
```
或者可以使用一个命令查看：
```
git config --list
```

### 查看全局用户名和全局邮箱
```
$ git config  --global  user.name
$ git config  --global  user.email
```
或者可以使用一个命令查看：
```
git config  --global --list
```

### 修改项目用户名和项目邮箱
```
$ git config  user.name "username"
 
$ git config  user.email "email"

```

###  修改全局用户名和全局邮箱
```
 
$ git config --global user.name "username"
 
$ git config --global user.email "email"
```



### 参考
- [git config 全局配置，user.name和user.email设置](http://blog.csdn.net/handsomerocco/article/details/7740602)和
