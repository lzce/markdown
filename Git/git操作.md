## 创建分支
`git checkout -b 分支名` : 切换并切换分支

`git branch 分支名`: 只会创建分支
## 删除分支
`git branch -d 分组名`: 删除分支

## 切换分支
`git checkout 分支名` : 切换分支

## 合并分支
`git checkout master(要合并的分支)` : 首先切换到合并的分支

`git merge dev(被合并的分支)` : 合并dev分支内容到master 

## 提交本地仓库
`git add .` : 将代码提交到暂存区 

`git commit -m message` : 提交到本地仓库

`git push origin master` : 将本地master分支提交到远程仓库

## 克隆远程仓库代码
`git clone 仓库地址`: 拉取仓库代码

## 上传代码之前拉取更新
 git pull <远程主机名> <远程分支名>:<本地分支名>
 
 比如: 要取回origin主机的next分支，与本地的master分支合并，需要写成下面这样
 
 ```git
 $ git pull origin next:master
 ```

## 关联远程仓库
`git remote -v` : 查看远程仓库链接

`git remote add origin(别名,默认origin)  远程仓库地址`: 与远程仓库关联

`git remote remove origin(别名)`: 取消远程仓库的关联


## 分支之间的同步
```shell
git checkout dev
git rebase master

git push --force 强制提交
```