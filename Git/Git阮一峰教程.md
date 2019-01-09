<!-- TOC -->

- [创建版本库](#创建版本库)
- [时光机穿梭](#时光机穿梭)
  - [版本回退](#版本回退)
  - [工作区和暂存区](#工作区和暂存区)
  - [管理修改](#管理修改)
  - [撤销修改](#撤销修改)
  - [删除文件](#删除文件)
- [远程仓库](#远程仓库)
  - [通过SSH绑定电脑](#通过ssh绑定电脑)
  - [添加远程库](#添加远程库)
  - [从远程仓库克隆](#从远程仓库克隆)
- [分支管理](#分支管理)
  - [创建与合并分支](#创建与合并分支)
  - [解决冲突](#解决冲突)
  - [分支管理策略](#分支管理策略)
  - [Bug分支](#bug分支)
  - [Feature分支](#feature分支)
  - [多人协作](#多人协作)
  - [Rebase](#rebase)
- [标签管理](#标签管理)
  - [创建标签](#创建标签)
  - [操作标签](#操作标签)
  - [使用 GitHub](#使用-github)

<!-- /TOC -->

# 创建版本库

初始化一个Git仓库，创建一个目录，使用`git init`命令。

该命令使执行所在目录变成Git可以管理的仓库，同时多出跟踪管理版本号的 .git 目录。

添加文件到Git仓库，分两步：

1. 使用命令`git add <file>`，注意，可反复多次使用，添加多个文件；
2. 使用命令`git commit -m <message>`，完成。

简单解释一下`git commit`命令，`-m`后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。

# 时光机穿梭

要随时掌握工作区的状态，使用`git status`命令。

如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容。

## 版本回退

`HEAD`指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。

穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。

要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。

## 工作区和暂存区

本地文件夹就是一个工作区。工作区有一个隐藏目录`.git`，这个不算工作区，而是Git的版本库。

Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫`HEAD`。需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

所以，`git add`命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行`git commit`就可以一次性把暂存区的所有修改提交到分支。

`git status`查看工作区是否干净。

## 管理修改

提交后，用`git diff HEAD -- readme.txt`命令可以查看工作区和版本库里面最新版本的区别。

第一次修改 -> `git add` -> 第二次修改 -> `git commit`

第二次修改的内容没有放入暂存区。

## 撤销修改

场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD <file>`，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

## 删除文件

一般情况下，你通常直接在文件管理器中把没用的文件删了，或者用`rm`命令删了。这个时候，Git知道你删除了文件，因此，工作区和版本库就不一致了，`git status`命令会立刻告诉你哪些文件被删除了。

现在你有两个选择，一是确实要从版本库中删除该文件，那就用命令`git rm`删掉，并且`git commit`。

另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本。`git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

# 远程仓库

## 通过SSH绑定电脑

第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果没有就需要创建。

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

第2步：登陆 GitHub，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容。GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。

## 添加远程库

要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git`；

关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；

## 从远程仓库克隆

要克隆一个仓库，首先必须知道仓库的地址，然后使用`git clone`命令克隆。

```
$ git clone git@github.com:michaelliao/gitskills.git
```

Git支持多种协议，包括`https`，但通过`ssh`支持的原生`git`协议速度最快。

从现在起，只要本地作了提交，就可以通过命令：

```
$ git push origin master
```

把本地`master`分支的最新修改推送至GitHub，现在，你就拥有了真正的分布式版本库！

# 分支管理

## 创建与合并分支

查看分支：`git branch`

创建分支：`git branch <name>`

切换分支：`git checkout <name>`

创建+切换分支：`git checkout -b <name>`

合并某分支到当前分支：`git merge <name>`

删除分支：`git branch -d <name>`

## 解决冲突

当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。

Git用`<<<<<<<`，`=======`，`>>>>>>>`标记出不同分支的内容。

用`git log --graph`命令可以看到分支合并图。

## 分支管理策略

合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。

## Bug分支

修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场。

## Feature分支

开发一个新feature，最好新建一个分支；

如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name>`强行删除。

## 多人协作

查看远程库信息，使用`git remote -v`；

本地新建的分支如果不推送到远程，对其他人就是不可见的；

从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；

在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；

建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；

从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。

## Rebase

rebase 操作可以把本地未push的分叉提交历史整理成直线；

rebase 的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

# 标签管理

## 创建标签

命令`git tag <tagname>`用于新建一个标签，默认为`HEAD`，也可以指定一个commit id；

命令`git tag -a <tagname> -m "blablabla..."`可以指定标签信息；

命令`git tag`可以查看所有标签。

## 操作标签

命令`git push origin <tagname>`可以推送一个本地标签；

命令`git push origin --tags`可以推送全部未推送过的本地标签；

命令`git tag -d <tagname>`可以删除一个本地标签；

命令`git push origin :refs/tags/<tagname>`可以删除一个远程标签。

## 使用 GitHub

在GitHub上，可以任意Fork开源仓库；

自己拥有Fork后的仓库的读写权限；

可以推送pull request给官方仓库来贡献代码。

