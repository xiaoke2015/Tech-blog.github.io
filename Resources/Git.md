# Git
Git 是用于 Linux内核开发的版本控制工具

## Git 工作流程

一般工作流程如下：

- 克隆 Git 资源作为工作目录。
- 在克隆的资源上添加或修改文件。
- 如果其他人修改了，你可以更新资源。
- 在提交前查看修改。
- 提交修改。
- 在修改完成后，如果发现错误，可以撤回提交并再次修改并提交。

![](https://www.runoob.com/wp-content/uploads/2015/02/git-process.png)


Git 常用的是以下 6 个命令：git clone、git push、git add 、git commit、git checkout、git pull，后面我们会详细介绍

![](https://www.runoob.com/wp-content/uploads/2015/02/git-command.jpg)

# 基础

## git init

Git 使用 git init 命令来初始化一个 Git 仓库，Git 的很多命令都需要在 Git 的仓库中运行，所以 git init 是使用 Git 的第一个命令。

在执行完成 git init 命令后，Git 仓库会生成一个 .git 目录，该目录包含了资源的所有元数据，其他的项目目录保持不变。

## git clone

我们使用 git clone 从现有 Git 仓库中拷贝项目（类似 svn checkout）。

克隆仓库的命令格式为：

`git clone [repo]`

如果我们需要克隆到指定的目录，可以使用以下命令格式：

`git clone [repo] [directory]`

参数说明：
- repo:Git 仓库。
- directory:本地目录。

## git config

git 的设置使用 git config 命令。

显示当前的 git 配置信息：

```shell
$ git config --list
credential.helper=osxkeychain
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
core.ignorecase=true
core.precomposeunicode=true 
```

设置提交代码时的用户信息
```
git config --global user.name 'runoob'
git config --global user.email test@runoob.com
```

如果只需要最近一次提交，那么很简单直接使用git commit –amend就可以搞定

解决方法一

```
git commit --amend --author="ljj <779454060@qq.com>"
```

## git add 

添加文件到仓库

`git add`

添加一个或多个文件到暂存区：

`git add [file1] [file2] ...`

添加指定目录到暂存区，包括子目录：：

`git add [dir]`

添加当前目录下的所有文件到暂存区：

`git add .`

## git status 

查看仓库当前的状态，显示有变更的文件。

`git status`

## git commit 

提交暂存区到本地仓库。

`git commit -m [message]`

没有文件添加时可用
`git commit -am [message]`

## git log

查看提交历史

`git log`

## git remote

命用于在远程仓库的操作

显示所有远程仓库：

`git remote -v`

添加远程版本库：

`git remote add [shortname] [url]`

- shortname

其他相关命令：

```
git remote rm name  # 删除远程仓库
git remote rename old_name new_name  # 修改仓库名
```


## git fetch

命令用于从远程获取代码库。该命令执行完后需要执行 git merge 远程分支合并到你所在的分支。

`git fetch`

## git pull

git pull 其实就是 git fetch 和 git merge FETCH_HEAD 的简写

`git pull [远程主机名] [远程分支名]:[本地分支名]`

git pull origin develop/1.3.0

## git push

命用于从将本地的分支版本上传到远程并合并

`git push [远程主机名] [本地分支名]:[远程分支名]`

## git branch 

创建分支命令:

`git branch [branchname]`

删除分支命令:

`git branch -d [branchname]`

查看远程分支命令:

`git branch -r`

## git checkout

切换分支命令:

`git checkout [branchname]`

我们也可以使用 git checkout -b [branchname] 命令来创建新分支并立即切换到该分支下

## git merge 

合并分支 分支合并到你所在的分支。

`git merge  [branchname]`

# 高级

## git reset

git reset 命令用于回退版本，可以指定退回某一次提交的版本。

git reset 命令语法格式如下：

`git reset [--soft | --mixed | --hard] [HEAD]`

--mixed 为默认，可以不用带该参数，用于重置暂存区的文件与上一次的提交(commit)保持一致，工作区文件内容保持不变。

`git reset  [HEAD] `

--soft 参数用于回退到某个版本：

`git reset --soft HEAD`

--hard 参数撤销工作区中所有未提交的修改内容，将暂存区与工作区都回到上一次版本，并删除之前的所有信息提交：

`git reset --hard HEAD`

HEAD 说明：

- HEAD 表示当前版本
- HEAD^ 上一个版本
- HEAD^^ 上上一个版本
- HEAD^^^ 上上上一个版本
以此类推...

可以使用 ～数字表示

- HEAD~0 表示当前版本
- HEAD~1 上一个版本
- HEAD^2 上上一个版本
- HEAD^3 上上上一个版本
以此类推...



## git blame 

如果要查看指定文件的修改记录可以使用 git blame 命令，格式如下：

`git blame [file]`

## git rebase

顾名思义，就是重新定义（re）起点（base）的作用，即重新定义分支的版本库状态。

`git rebase [newbase]`

git rebase解决合并冲突

修改冲突

git add .

git rebase --continue

## git rebase --abort 

会放弃合并，回到rebase操作之前的状态，之前的提交的不会丢弃；

## git rebase -i

命令可以压缩合并多次提交

`git rebase -i [commitHash]` 

合并最近两次提交

![](https://i.postimg.cc/7Zq17TPj/WX20201226-171357-2x.png)

输入 git rebase -i HEAD~2 命令后, 会弹出如下的编辑器

![](https://i.postimg.cc/pd5ddR5y/WX20201226-171839-2x.png)

将第二行的 pick 改为 s “s” 为 “squash” 的缩写 “squash” 的意思是 将倒数第二次提交 压缩为最后一次提交。然后保存，然后会弹出如下的编辑器

![](https://i.postimg.cc/8PykBjhj/WX20201226-171858-2x.png)

将下面的内容改成你想提交的概述即可，保存退出

![](https://i.postimg.cc/PxkdrZkF/WX20201226-171954-2x.png)

## git cherry-pick 

就是将指定的提交（commit）应用于其他分支。

`git cherry-pick [commitHash]`

## git stash

stash命令可用于临时保存和回复修改，可跨分支

保存，save为可选项，message为本次保存的注释

`git stash [save message]`

所有保存的记录列表

`git stash list`

恢复，num是可选项，通过git stash list可查看具体值。只能恢复一次

`git stash pop stash@{num}`

恢复，num是可选项，通过git stash list可查看具体值。可回复多次

`git stash apply stash@{num}`

删除某个保存，num是可选项，通过git stash list可查看具体值

`git stash drop stash@{num}`

删除所有保存

`git stash clear`

## 恢复删除的commit 进入工程下的.git文件下，git reflog命令

`git reflog`

查询到 commitid 

`git branch recover_branch_name 5b7cf2c(哈希码)`

# .gitignore


## git revert
用一次新的commit 撤销之前的commit





# 脚本

[![WX20210105-154404-2x.png](https://i.postimg.cc/JhHRfzXj/WX20210105-154404-2x.png)](https://postimg.cc/t1y0Py2g)


