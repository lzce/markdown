
### 总结
- 会多一条merge类型的commit
- 不同分支的commit按照时间先后排列




### merge
rebase前操作：从master分支checkout新分支b。按时间先后，操作如下：
- b做一次修改`b1`
- master做一次修改`m1`
- b做一次修改`b2`
- master做一次修改`m2`

rebase操作：idea中切换到master分支，在`remote branches-> origin/b1`右键选择`merge into current`,这里的current指的是当前选择的分支(master),selected指`origin/b1`分支。



git bash中查看分支历史如下：
```
$ git log
commit 5a2736f48d494e7986075bc7c0a765483c44dc0f (HEAD -> master)
Merge: d31cd2f 7f6dd07
Author: Nathan.Chen <xin979@126.com>
Date:   Thu Oct 31 18:07:53 2019 +0800

    Merge branch 'b'

    # Conflicts:
    #       reset.txt

commit d31cd2f3b1bfd414a27a0b723870fc5838bcc48f (origin/master)
Author: Nathan.Chen <xin979@126.com>
Date:   Thu Oct 31 18:07:17 2019 +0800

    m2

commit 7f6dd074fb6b91f9363c2fff6beea504eba0d4a5 (origin/b, b)
Author: Nathan.Chen <xin979@126.com>
Date:   Thu Oct 31 18:06:47 2019 +0800

    b2

commit f11b0112741b26ab58373a75cecc13156f18aa89
Author: Nathan.Chen <xin979@126.com>
Date:   Thu Oct 31 18:03:49 2019 +0800

    m1

commit 458606552d1f6499ab64c84fd4e6849b11bf193f
Author: Nathan.Chen <xin979@126.com>
Date:   Thu Oct 31 18:03:13 2019 +0800

    b1

commit 5776ac2c49555f5bfb63620744090b6ecdc0e97c
Author: Nathan.Chen <xin979@126.com>
Date:   Thu Oct 31 15:03:19 2019 +0800

    first commit

```
可以看到这里会多下面一条merge记录：
```
commit 5a2736f48d494e7986075bc7c0a765483c44dc0f (HEAD -> master)
Merge: d31cd2f 7f6dd07
Author: Nathan.Chen <xin979@126.com>
Date:   Thu Oct 31 18:07:53 2019 +0800

    Merge branch 'b'

    # Conflicts:
    #       reset.txt

```

并且commit的顺序是按照时间先后顺序。