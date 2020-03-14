### 总结
- 没有merge类型的commit
- 同一个分支的commit会排列在一起，并且一个分支的全部commit在另一个分支全部的commit前面



### idea中rebase类型
主要2种类型，它们是完全相反的操作：
- rebase current onto selected
- checkout and rebase onto current


### 前提
创建一个git工程，只包含一个文件`reset.txt`,所有的修改都是改这个文件


### rebase current onto selected
rebase前操作：从master分支checkout新分支b。按时间先后，操作如下：
- b做一次修改`b1`
- master做一次修改`m1`
- b做一次修改`b2`
- master做一次修改`m2`

rebase操作：idea中切换到master分支，在`local branches-> origin/b`右键选择`rebase current onto selected`,这里的current指的是当前选择的分支(master),selected指`origin/b`分支。


git bash中查看分支历史如下：

```
$ git log
commit 25755e074e913098117a1e6b1b1f6c3a5f90b6ab (HEAD -> master)
Author: Nathan.Chen <xin979@126.com>
Date:   Thu Oct 31 17:43:30 2019 +0800

    m2

commit 47129978b2554fc83bbbe11ed0f6939bf35ad0f8
Author: Nathan.Chen <xin979@126.com>
Date:   Thu Oct 31 17:42:15 2019 +0800

    m1

commit dfbbdd16f1ee9a0306a9d600b1ad9cba87bef8fe (origin/b, b)
Author: Nathan.Chen <xin979@126.com>
Date:   Thu Oct 31 17:42:59 2019 +0800

    b2

commit 59e7f9c8e0b5a4304150287bbf5f1456ad188699
Author: Nathan.Chen <xin979@126.com>
Date:   Thu Oct 31 17:41:49 2019 +0800

    b1

commit 5776ac2c49555f5bfb63620744090b6ecdc0e97c
Author: Nathan.Chen <xin979@126.com>
Date:   Thu Oct 31 15:03:19 2019 +0800

    first commit

```
可以看到，这里commit顺序是先b（b1、b2）再master（m1、m2）,master的commit记录是以b为基准的

操作结果：master合并了b的代码，但是b没有合并master的代码。



### checkout and rebase onto current
rebase前操作：从master分支checkout新分支b。按时间先后，操作如下:
- b做一次修改`b1`
- master做一次修改`m1`
- b做一次修改`b2`
- master做一次修改`m2`


rebase操作：idea中切换到master分支，在`local branches-> origin/b`右键选择`checkout and rebase onto current `,这里的current指的是当前选择的分支(master),selected指`origin/b`分支。



git bash中查看分支历史如下：
```
$ git log
commit 3cf0e2c19d074541de719c8d5710ae3df90ae8d4 (HEAD -> b)
Author: Nathan.Chen <xin979@126.com>
Date:   Thu Oct 31 17:30:29 2019 +0800

    b2

commit 85c632dbd6baf060b633b3db0acaeb57b5d918f0
Author: Nathan.Chen <xin979@126.com>
Date:   Thu Oct 31 17:29:35 2019 +0800

    b1

commit ad4bc9ccb41e0d9708a09de98b2e276a402d031d (origin/master, master)
Author: Nathan.Chen <xin979@126.com>
Date:   Thu Oct 31 17:30:58 2019 +0800

    m2

commit 59a8f7142a0547ee21a29bb9e2bf9c4c243e799f
Author: Nathan.Chen <xin979@126.com>
Date:   Thu Oct 31 17:30:00 2019 +0800

    m1

commit 5776ac2c49555f5bfb63620744090b6ecdc0e97c
Author: Nathan.Chen <xin979@126.com>
Date:   Thu Oct 31 15:03:19 2019 +0800

    first commit


```

可以看到，这里commit顺序是先master(m1、m2)再b(b1、b2),b的commit是以master为基准的.



操作结果：b合并了master的代码,但是master没有合并b的代码