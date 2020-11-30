---
title: Git
date:
updated:
type: "tags"
categories: git
comments:
description: Git版本控制
keywords: Git,版本控制
top_img: https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=283932388,350254066&fm=26&gp=0.jpg
cover: https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=283932388,350254066&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
# git

## 1.工作流程

```
1.克隆 Git 资源作为工作目录。
2.在克隆的资源上添加或修改文件。
3.如果其他人修改了，你可以更新资源。
5.在提交前查看修改。
6.提交修改。
7.在修改完成后，如果发现错误，可以撤回提交并再次修改并提交。
```



## 2.工作区暂存区，版本库

```
工作区：就是你在电脑里能看到的目录。
暂存区：英文叫stage, 或index。一般存放在 ".git目录下" 下的index文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。
版本库：工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。
```



## 3.基本操作

```
git init
Git 使用 git init 命令来初始化一个 Git 仓库，Git 的很多命令都需要在 Git 的仓库中运行，所以 git init 是使用 Git 的第一个命令。
在执行完成 git init 命令后，Git 仓库会生成一个 .git 目录，该目录包含了资源的所有元数据，其他的项目目录保持不变（不像 SVN 会在每个子目录生成 .svn 目录，Git 只在仓库的根目录生成 .git 目录）。


git clone
我们使用 git clone 从现有 Git 仓库中拷贝项目（类似 svn checkout）。
克隆仓库的命令格式为：git clone <repo>

git add
git add 命令可将该文件添加到缓存，如我们添加以下两个文件：
新项目中，添加所有文件很普遍，我们可以使用 git add . 命令来添加当前项目的所有文件。
"AM" 状态的意思是，这个文件在我们将它添加到缓存之后又有改动。改动后我们再执行 git add 命令将其添加到缓存中：

git status
命令用于查看项目的当前状态。

git diff
执行 git diff 来查看执行 git status 的结果的详细信息。
git diff 命令显示已写入缓存与已修改但尚未写入缓存的改动的区别。git diff 有两个主要的应用场景。
尚未缓存的改动：git diff
查看已缓存的改动： git diff --cached
查看已缓存的与未缓存的所有改动：git diff HEAD
显示摘要而非整个 diff：git diff --stat
git status 显示你上次提交更新后的更改或者写入缓存的改动， 而 git diff 一行一行地显示这些改动具体是啥。

git commit
使用 git add 命令将想要快照的内容写入缓存区， 而执行 git commit 将缓存区内容添加到仓库中。
Git 为你的每一个提交都记录你的名字与电子邮箱地址，所以第一步需要配置用户名和邮箱地址。
如果你觉得 git add 提交缓存的流程太过繁琐，Git 也允许你用 -a 选项跳过这一步。命令格式如下：
git commit -a

git reset HEAD
git reset HEAD 命令用于取消已缓存的内容。

git rm
如果只是简单地从工作目录中手工删除文件，运行 git status 时就会在 Changes not staged for commit 的提示。
要从 Git 中移除某个文件，就必须要从已跟踪文件清单中移除，然后提交。可以用以下命令完成此项工作
git rm <file>
如果删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项 -f
git rm -f <file>
如果把文件从暂存区域移除，但仍然希望保留在当前工作目录中，换句话说，仅是从跟踪清单中删除，使用 --cached 选项即可
git rm --cached <file>

git mv
git mv 命令用于移动或重命名一个文件、目录、软连接。
```

## 4.分支管理

```
几乎每一种版本控制系统都以某种形式支持分支。使用分支意味着你可以从开发主线上分离开来，然后在不影响主线的同时继续工作。

有人把 Git 的分支模型称为必杀技特性，而正是因为它，将 Git 从版本控制系统家族里区分出来。

创建分支命令：
git branch (branchname)

切换分支命令:
git checkout (branchname)

当你切换分支的时候，Git 会用该分支的最后提交的快照替换你的工作目录的内容， 所以多个分支不需要多个目录。
合并分支命令:
git merge 

列出分支基本命令：
git branch
Git 教程
Git 教程
Git 安装配置
Git 工作流程
Git 工作区、暂存区和版本库
Git 创建仓库
Git 基本操作
Git 分支管理
Git 查看提交历史
Git 标签
Git Github
 Git Gitee
Git 服务器搭建
 Git 基本操作Git 查看提交历史 
Git 分支管理
几乎每一种版本控制系统都以某种形式支持分支。使用分支意味着你可以从开发主线上分离开来，然后在不影响主线的同时继续工作。

有人把 Git 的分支模型称为必杀技特性，而正是因为它，将 Git 从版本控制系统家族里区分出来。

//推送新分支  git push --set-upstream origin style
//比较本地分支和远程分支的区别
git diff master origin/style
将本地分支命名为temp分支
git fetch origin master:temp


//
情况1： 本地有分支dev，远程没有dev分支，要将本地dev分支提交到远程的dev分支

              首先切换到dev分支： git  checkout dev

　　　　检测是否有为提交内容：git status

　　　　将未提交内容添加到暂存区： git add .（或git add 具体文件名称）

　　　    将暂存区内容提交到本地版本库： git commit -m"本次提交内容说明"

　　　　推送到远程：git push origin dev:dev (推送成功后，在远程可以看到已经新建了一个dev分支)

情况2: 将远程dev分支上的内容，合并至远程的master分支上

　　　　　　本地切换到master分支上: git checkout master

　　　　　　合并dev分支到master上： git merge dev, （看有无冲突，有冲突要解决冲突）

　　　  　　 合并完成后，推送到远程 git  push  origin master

情况三：　拉取上线分支，一般来说，我们在dev分支上进行开发，要上线时，拉去一个新的分支，并将dev分支上的内容复制一边，上线完成后，将上线分支上的内容合并到master上，保证master始终是稳定的版本

　　　　本地上线分支，需要新建一个分支时：

　　　　　在本地新建一个分支,并切换： git  checkout - b  vesion1.1

　　　　　拉取远程dev分支： git  fetch origin dev

　　　　　推送到远程：　git push origin version1.1:version1.1

　　　  本地已经有了上线分支，并且在上线分支上也有修改时

　　　　　当前分支为version1.1

　　　　　1.首先要将version1.1的修改内容提交到版本库，否则，git merge origin/dev会失败

　　　　　2.如果git merge origin/dev失败，出现CONFLICT (content): Merge conflict 字样，在冲突文件中查看，解决冲突。

　　　　　3. 解决冲突时，修改了文件，则必须再次提交到版本库。

　　　　　4. 推送到远程: push origin version1.1


创建分支命令：
git branch (branchname)

切换分支命令:
git checkout (branchname)
当你切换分支的时候，Git 会用该分支的最后提交的快照替换你的工作目录的内容， 所以多个分支不需要多个目录。

合并分支命令:
git merge 
你可以多次合并到统一分支， 也可以选择在合并之后直接删除被并入的分支。

git branch
没有参数时，git branch 会列出你在本地的分支。
当你执行 git init 的时候，默认情况下 Git 就会为你创建 master 分支。

删除分支命令：
git branch -d (branchname)
例如 $ git merge newtest



//推送空分支并且清除
```

## 5.合并冲突

```
合并冲突
合并并不仅仅是简单的文件添加、移除的操作，Git 也会合并修改。
在 Git 中，我们可以用 git add 要告诉 Git 文件冲突已经解决	
```

## 6.pull和push

```
$ git push <远程主机名> <本地分支名>:<远程分支名>
$ git push origin master
上面命令表示，将本地的master分支推送到origin主机的master分支。如果后者不存在，则会被新建。 
origin是一个远程厂库地址。

git pull 与 git push操作的目的相同，但是操作的目标相反。命令格式如下：


区别

git commit是将本地修改过的文件提交到本地库中。
git commit 主要是将暂存区里的改动给提交到本地的版本库。每次使用git commit 命令我们都会在本地版本库生成一个40位的哈希值，这个哈希值也叫commit-id，

git push是将本地库中的最新信息发送给远程库。
在使用git commit命令将修改从暂存区提交到本地版本库后，只剩下最后一步将本地版本库的分支推送到远程服务器上对应的分支了

```

## 7.推送流程

```
gitclone
git add .
git commit "备注信息"

git config --global user.email "1092283755@qq.com"
git config --global user.name "mikasa"

git push -u origin master


```

## 8.删除

```
git rm -r -n --cached 文件/文件夹名称 

加上 -n 这个参数，执行命令时，是不会删除任何文件，而是展示此命令要删除的文件列表预览。

git rm -r --cached 文件/文件夹名称

git commit -m "提交说明"
git push origin master

```

## 9.提交到远程仓库

```
// 添加远程仓库
git remote add origin git@github.com:zcz147258/person_web.git

// 查看已添加的远程仓库
git remote -v

// 如果要删除
// git remote rm RemoteQPS

// 如果要重命名
// git rename RemoteQPS QPS

//无法提交填写 
git pull origin master --allow-unrelated-histories
然后vim  esc  :wq
执行 git pull origin master --allow-unrelated-histories

//添加到待提交列表，提交到本地仓库
git add *
git commit -m 'git commit 1'

//将本地仓库提交到远程仓库
//git push origin master



错误
	Pull is not possible because you have unmerged files.
	git reset --hard FETCH_HEAD
找回误操作
	git reflog
	git reset --hard */id
	
	

```

## 10设置 SSH密钥

```
1. 安装git，从程序目录打开 “Git Bash” ,
2. ssh-keygen -t rsa -C "email@email.com" ,email@email.com是自己github账号
3. 提醒你输入key的名称，你可以不用输入，一路回车，就OK了；
4. 一般会在用户目录下生成三个文件，例如我生成的文件在C:\Users\SmallHacker\.ssh目录下；
5,进入该用户的目录下用命令cat id_rsa.pub打开文件并复制里面的全部内容；
6,打开github账号–>Settings–>SSH and GPG keys–>New SSH key,并把复制好的内容全部粘贴进去" ；
add SSH key
```

## 11.branch

```
//$ git checkout -b style   创建本地分支
$ git push origin style:style    推送本地新创建的分支到远程

git push origin :style
删除远程分支里面的内容 

//检查添加的远程库
git remote -v
//添加远程库 
git remote add origin https://gitee.com/zczsylm/GBN_taoke.git
//删除远程库
git remote remove origin
//
git push origin style1:style
推送分支到远程分支

```

