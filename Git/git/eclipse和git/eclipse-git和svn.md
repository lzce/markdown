### 不需要同步文件
- 不需要同步：.settings/.project/.classpath
- 项目自动生成文件：包括.settings,.project,和.classpath等。[eclipse项目中的.settings .project .classpath 个人见解](http://blog.csdn.net/baicp3/article/details/13277461)



### git
- git使用案例: [eclipse上使用git上传或下载代码至github](http://blog.csdn.net/u014785687/article/details/73473769)和[Eclipse导入git上的maven web项目部署](http://blog.csdn.net/u014785687/article/details/73473769)
- 导入没有.settings/.project/.classpath的maven项目: [eclipse引入没有.project文件的方法](http://blog.csdn.net/oqqyeyi/article/details/41309049)
- eclipse导入远程git仓库中的maven项目: 经过自己亲身实践,分为2步,(1)File->Import->Git->Projects from Git->next->Clone URI->next->拷贝远程ssh链接到URI,其它都默认->next->选择分支(比如master)->next->选择要保存代码的文件夹(Directory)->next->选择import as general project->next->保持默认->finish.导入以后,右键选择导入的项目->delete->不要勾选Delete project contents on disk->OK.(2)File->Import->Maven->Existing Maven Projects->next->选择刚刚从git导入时保存项目的文件夹->Finish.
- git提交时“There are no staged files”错误: [eclipse git 提交时提示 “There are no staged files”](http://blog.csdn.net/Andy2019/article/details/70149122)



### svn
- 删除无效svn地址: [删除Eclipse自动保存的SVN资源库URL](https://blog.csdn.net/yang5726685/article/details/59118432)