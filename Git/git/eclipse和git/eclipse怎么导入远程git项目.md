

### eclipse导入
- eclipse导入远程git仓库中的maven项目: 分为2步,(1)File->Import->Git->Projects from Git->next->Clone URI->next->拷贝远程ssh链接到URI,其它都默认->next->选择分支(比如master)->next->选择要保存代码的文件夹(Directory)->next->选择import as general project->next->保持默认->finish.导入以后,右键选择导入的项目->delete->不要勾选Delete project contents on disk->OK.注意,也可以不用前面的操作,直接在terminal中使用git clone命令.(2)File->Import->Maven->Existing Maven Projects->next->选择刚刚从git导入时保存项目的文件夹->Finish.