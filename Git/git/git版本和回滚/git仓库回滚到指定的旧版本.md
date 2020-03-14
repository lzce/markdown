
### 版本回滚原理
`HEAD`指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。


### 查看最近的commit_id
执行`git log`:
```
$ git log
commit 3eb9053f892dc9329792a94b8bb2e6208d8484a2 (HEAD -> master, origin/master)
Author: Nathan.Chen <xin979@126.com>
Date:   Thu Oct 31 15:46:56 2019 +0800

    第三次commit

commit c2a753147f0f9c310d2639b45707b38dbbbd0deb
Author: Nathan.Chen <xin979@126.com>
Date:   Thu Oct 31 15:29:01 2019 +0800

    第二次commit

commit 5776ac2c49555f5bfb63620744090b6ecdc0e97c
Author: Nathan.Chen <xin979@126.com>
Date:   Thu Oct 31 15:03:19 2019 +0800

    first commit


```
上面的commit后面是commit_id。

可以使用`git log -n`指定显示最近`n`个版本，比如`git log -2`



### 回滚到指定的旧版本
这里假设要回滚到`first commit`时对应的commit_id号`5776ac2c49555f5bfb63620744090b6ecdc0e97c`,执行`git reset --hard 5776ac2c49555f5bfb63620744090b6ecdc0e97c`,操作结果为：
```
$ git reset --hard 5776ac2c49555f5bfb63620744090b6ecdc0e97c
HEAD is now at 5776ac2 first commit

```
执行`git push -f origin master`将修改强制提交到仓库










### 参考
- [git-命令查看版本记录](https://blog.csdn.net/cxu123321/article/details/92063708)
- [git回滚到任意版本](https://blog.csdn.net/liulangshusheng2012/article/details/82682515)