# git和Github入门

## 什么是git? 

- git是主流的分布式版本控制系统
- git只是管理工具，命令代码只需要学习基础命令即可，随用随查。
- git 有可视化管理工具，但不建议使用，自己敲命令更好。

### git常用命令：

- 右击打开Git控制台（可在任何需要管理的文件内右击）

- git config -- global user.name 名称：配置用户名
- git config -- global user.email 邮箱：配置邮箱（可以随便打）

- git init：初始化一个git仓库

- git clone **Github链接**：克隆一个git仓库(拉取下载Github上的源码)

  > 注意：这里粘贴链接时不能用Ctrl+V,需要鼠标右击选择paste

- git add **.** :将工作区内的所有文件夹和非空文件夹设置为准备提交状态

- git add **文件名以及后缀**：将所选文件设置为准备提交状态

- git commit -m **“备注”**：提交所选文件并写上本次提交的备注

  > 提交的位置是git工具在本地创建的本地仓库位置

- git push origin **分支名** ：将项目推送到远程仓库如“Github”

- git log：查看提交的历史记录
- git checkout HEAD **文件名以及后缀**：将所选文件恢复到最后一次提交时的状态



## 什么是Github?

