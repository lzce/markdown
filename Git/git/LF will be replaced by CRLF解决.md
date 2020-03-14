
### LF
mac等linxu系统默认使用`LF换行`

### crlf
windows默认使用`crlf`换行



### 操作建议
建议设置全局的git的`core.autocrlf=false`,windows也使用LF换行。



### 配置全局`core.autocrlf`
执行下面的命令：
```
git config  --global core.autocrlf "false"
```

### 配置单个项目的`core.autocrlf`
在项目根目录下执行下面的命令：
```
git config   core.autocrlf "false"
```






###  参考
- [git如何避免”warning: LF will be replaced by CRLF“提示](https://www.zhihu.com/question/50862500)
- [LF will be replaced by CRLF in git](https://stackoverflow.com/questions/5834014/lf-will-be-replaced-by-crlf-in-git-what-is-that-and-is-it-important)