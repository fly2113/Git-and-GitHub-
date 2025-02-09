# git和Github入门（拓展深化资源来自编程导航）

## 什么是git? 

- git是主流的分布式版本控制系统
- git只是管理工具，命令代码只需要学习基础命令即可，随用随查。
- git 有可视化管理工具，但不建议使用，自己敲命令更好。

### git常用命令：

> 提交记录的ID有2种：1、哈希值；2、相对索引

> git官方使用电子书：https://github.com/Maplespe/DWMBlurGlass.git

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

- git log：查看提交的历史记录。包含作者、提交时间、提交记录的哈希值

- git checkout HEAD **文件名以及后缀**：将所选文件恢复到最后一次提交时的状态

  >HEAD总是指向当前分支的最近一次的提交记录，通常指的是分支名，但是可以更改它的指向

### 一、配置相关

```java
git config --global user.name "Your Name"      # 设置全局用户名
git config --global user.email "email@example.com"  # 设置全局邮箱
git config --global credential.helper store    # 缓存用户名密码（HTTPS协议）
git config --list                              # 查看所有配置
```

### 二、仓库初始化

```
git init                      # 初始化创建本地仓库
git clone <远程仓库地址>        # 克隆远程仓库到本地
```

### **三、基本操作**

```
git add <文件名>              # 添加文件到暂存区
git add .                    # 添加所有修改到暂存区
git commit -m "提交说明"      # 提交暂存区内容到本地仓库
git commit --amend      
git status                   # 查看工作区状态
git diff                     # 查看未暂存的修改差异
git diff --staged            # 查看已暂存的修改差异
```

### **四、分支管理**

**交互式的rebase**:修改提交树 -- 从一系列的提交记录中找到想要的提交记录最好方法

> git rebase -i HEAD~2
>
> 交互式 rebase 指的是使用带参数 `--interactive` 的 rebase 命令, 简写为 `-i`
>
> 后面的HEAD~2就是从哪个特定的提交记录后面开始改变
>
> 如果你在命令后增加了这个选项, Git 会打开一个 UI 界面并列出将要被复制到目标分支的备选提交记录，它还会显示每个提交记录的哈希值和提交说明，提交说明有助于你理解这个提交进行了哪些更改。
>
> 在实际使用时，所谓的 UI 窗口一般会在文本编辑器 —— 如 Vim —— 中打开一个文件

```
git branch                    # 查看本地分支
git branch <分支名>           # 创建新分支
git branch <分支名> 提交记录ID  # 在指定提交上创建新分支
git checkout <分支名>         # 切换分支
git checkout -b<分支名>       # 创建并切换到新分支
git switch <分支名>           # 切换分支（Git 2.23+推荐）
git merge <分支名>            # 合并提交
'需要切换到你想要合并的主分支上并将分支名指向想合并的提交上，另一个提交也是如此，然后再输入其他分支名'
git rebase <分支名>           # 变基操作（整理提交历史）移动一个记录
 实际上就是取出一系列的提交记录，“复制”它们，然后在另外一个地方逐个的放下去。
'将所在分支上的指定提交记录复制到另一个分支上，从而创建一个更线性的提交历史。但原本的提交结点并未消失'

git branch -f <分支名> 目标提交记录 # 让分支指向一个提交记录，可以是哈希值也可以是相对HEAD~3
git branch -d <分支名>        # 删除已合并的分支
git branch -D <分支名>        # 强制删除未合并的分支
```

##### 多分支Rebase

> git rebase <分支名> <分支名>   # 合并分支    将第二个分支上的所有提交记录移动到第一个分支上，最后第																				二个分支名指向合并后的最后一个提交记录上，并切换到该分																				支名。



### **五、远程仓库操作**

```
git remote add origin <远程仓库地址>  # 关联远程仓库
git remote -v                 # 查看远程仓库信息
git fetch origin              # 拉取远程仓库更新（不合并）
git pull origin <分支名>      # 拉取并合并远程分支到当前分支
git push -u origin <分支名>   # 推送本地分支到远程（首次推送用 -u）
git push origin --delete <分支名>  # 删除远程分支
```

------

### **六、撤销与回退**

>`git reset` 通过把分支记录回退几个提交记录来实现撤销改动。你可以将这想象成“改写历史”。
>
>`git reset` 向上移动分支，原来指向的提交记录就跟从来没有提交过一样。

```
git checkout -- <文件名>      # 丢弃工作区的修改
本地分支撤销：
git reset HEAD <文件名>       # 取消暂存区的修改
git reset HEAD~1             # 回退基于HEAD的上面（HEAD原本指向的记录就没有了，HEAD仍然指向分支名）
git reset --hard <commit-id>  # 回退到指定提交（⚠️谨慎使用）
远程分支撤销：
git revert <commit-id>        # 撤销某次提交（生成新提交，这个新的提交就和撤销的提交的parent提交一致）
```

------

### **七、查看历史记录**

```
git log                       # 查看提交历史的历史记录。包含作者、提交时间、提交记录的哈希值
git log --oneline             # 简洁模式查看历史
git log -p                    # 查看详细修改内容
git reflog                    # 查看所有操作记录（包括被删除的提交）
```

------

### **八、储藏与恢复**

```
git stash                     # 临时保存工作区修改
git stash pop                 # 恢复最近一次储藏的内容
git stash list                # 查看所有储藏记录
```

------

### **九、标签管理**

> 可以（在某种程度上 —— 因为标签可以被删除后重新在另外一个位置创建同名的标签）永久地将某个特定的提交命名为里程碑，然后就可以像分支一样引用了。更难得的是，它们并不会随着新的提交而移动。你也不能切换到某个标签上面进行修改提交，它就像是提交树上的一个锚点，标识了某个特定的位置。
>
> 切换标签时会进入分离HEAD状态

```
git tag                       # 查看所有标签
git tag <标签名>              # 创建轻量标签
git tag <标签名> <记录id>      # 为指定提交记录创建标签若不写id则默认为当前HEAD位置
git tag -a <标签名> -m "描述"  # 创建含注释的标签
git push origin <标签名>      # 推送标签到远程
git checkout <标签名>			# 切换到某一标签指定的提交上
git describe <ref> 				# 用来描述离你最近的锚点（也就是标签）
							# <ref>可以是任何能被 Git 识别成提交记录的引用，如果你没有指定的话，Git 								会使用你目前所在的位置（HEAD）
							它输出的结果是这样的：<tag>_<numCommits>_g<hash>
tag 表示的是离 ref 最近的标签， numCommits 是表示这个 ref 与 tag 相差有多少个提交记录， hash 表示的是你所给定的 ref 所表示的提交记录哈希值的前几位。
当 ref 提交记录上有某个标签时，则只输出标签名称



```

------

### **十、整理提交记录、协作与补丁**

```
git fetch --all               # 获取所有远程仓库的更新
git cherry-pick <commit-id>   # 应用指定提交到当前分支，后面的commit-id可以多个，以空格间隔。
							  # 跟rebase不同的是，它可以把部分记录移动过来而不是全部；
							  # 适用于知道你所需要的提交记录（并且还知道这些提交记录的哈希值）时
							  #cherry-pick 可以将提交树上任何地方的提交记录取过来追加到 HEAD 上（只								# 要不是 HEAD 上游的提交就没问题）。
							  

git format-patch              # 生成补丁文件（用于代码传递）
```

### 十一、 HEAD指向移动

> 操作符 `^` 与 `~` 符一样，后面也可以跟一个数字。
>
> 但是该操作符后面的数字与 `~` 后面的不同，并不是用来指定向上返回几代，而是指定合并提交记录的某个 parent 提交。还记得前面提到过的一个合并提交有两个 parent 提交吧，所以遇到这样的节点时该选择哪条路径就不是很清晰了。
>
> Git 默认选择合并提交的“第一个” parent 提交，在操作符 `^` 后跟一个数字可以改变这一默认行为。
>
> 
>
> 还支持链式操作：git checkout HEAD~ ^2 ~2 (可以移动4次)
>
> ​		这里：~移动一次； ^2 选择第二个parent； ~2 再移动两次
>
> 

```
绝对移动：
git checkout **具体提交记录的哈希值**      #分离HEAD,使它指向的不再是分支名而是具体的提交记录。比较令人										 #欣慰的是，Git 对哈希的处理很智能。你只需要提供能够唯一标识提     									  #交记录的前几个字符即可。																		fed2da64c0efc5293610bdd892f82a58e8cbc5d8
									   #因此我可以仅输入`fed2` 而不是上面的一长串字符。
相对移动：
git checkout 分支名^         #单步移动使用方向键^向上移动一个提交记录，一个^是一步，两个^^是两步以此类推
							#多步移动使用 ~<num> 向上移动多个提交记录，如 ~3
							
git checkout HEAD^          #也可以将 HEAD 作为相对引用的参照。





```

### 十二、个性设置

> 来自https://nulab.com/zh-cn/learn/software-development/git-tutorial/how-to-use-git/git-on-command-line/default-settings/   猴子都能懂的Git入门

```
$ git config --global user.name ""		# 设置用户名
$ git config --global user.email ""		# 设置邮箱

$ git config --global color.ui auto		# 设置 Git 输出颜色
$ git config --global alias.co checkout # 給 Git 命令设置别名，将“checkout”缩写为“co”来执行命令
```



### **常用场景示例**

1. **首次推送本地项目到远程**：

   ```
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin <远程仓库地址>
   git push -u origin master
   ```

2. **解决合并冲突**：

   - 执行 `git pull` 后出现冲突
   - 手动编辑文件解决冲突
   - `git add <冲突文件>`
   - `git commit -m "解决冲突"`

------

**注意事项**：

- `git reset --hard` 会永久删除未提交的修改，慎用！
- 避免直接操作远程主分支（如 `master/main`），推荐使用分支开发
- 推荐使用 `git switch` 代替 `git checkout` 切换分支（Git 2.23+）

建议配合可视化工具（如 VS Code GitLens、SourceTree）提升效率。



## 什么是Github?

官网入门教程：https://docs.github.com/zh/get-started/start-your-journey/hello-world































































