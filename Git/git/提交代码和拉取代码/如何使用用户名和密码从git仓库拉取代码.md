### git仓库访问方式
一般git仓库支持通过2种方式访问：
- ssh
- http(或者https)


### 什么时候需要用户名和密码
使用http时需要git仓库用户名和密码。注意，这里的用户名不是git全局用户名。参考[Why is Git always asking for my password?](https://help.github.com/en/articles/why-is-git-always-asking-for-my-password)



### 电脑如何保存git仓库用户名和密码
可以通过命令`git config --list`查看：
```
credential.helper=osxkeychain
user.name=ChenXin
user.email=xin979@126.com
core.quotepath=false
core.autocrlf=input
```
这里的`credential.helper`就是保存方式。不同的平台保存方式不一样，具体如下：
- mac: osxkeychain
- windows: 凭据管理器

注意：只要第一次输入git仓库用户名和密码错误，后面就再也不会弹出输入提示。只有把之前的错误的删除，才能重新弹出输入提示。




### windows输错git仓库用户名和密码如何重新输入
windows使用凭据管理器管理git仓库用户名和密码。输错了的话，需要去`控制面板`->`用户账户`->`凭据管理器`删除之前保存的错误git仓库用户名和密码。参考[Git 远程仓库clone时 密码输错了 如何修改](https://blog.csdn.net/qq_38423105/article/details/80942234)


### mac输错git仓库用户名和密码如何重新输入
去osxkeychain删除错误的。

### github


参考[Caching your GitHub password in Git](https://help.github.com/en/articles/caching-your-github-password-in-git)