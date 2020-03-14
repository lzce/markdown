### git仓库
git仓库包括2种：
- 本地仓库：本地项目根目录下面的`.git`
- 远程仓库：也就是git服务器



### 删除本地仓库(.git)
删除本地仓库也就是删除项目根目录下面的`.git`。只需要执行下面的命令即可：
```
find . -name ".git" | xargs rm -Rf
```


参考[如何删除git仓库](https://blog.csdn.net/nerosolomon/article/details/79453485)和[Git怎么删除本地仓库,创建新的仓库](https://blog.csdn.net/wltsysterm/article/details/79163375)

### 如何判断本地仓库删除
删除之前在项目根目录下面执行`git bash here`,会发现类似`master`的分支标记：
```
Nathan@DESKTOP-V5F8QTP MINGW64 /d/workspace/project/payGateway-JD (master)
```

删除以后`(master)`会消失




### 删除远程仓库(remote origin)：
- 使用`git remote rm origin`删除