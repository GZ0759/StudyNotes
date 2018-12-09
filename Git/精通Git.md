> 精通GIt（第二版）
> Pro GIt
> 2017年9月第一次出版

# 第二章 Git基础

## 2.5 远程仓库的使用

查看远程仓库。如果想查看你已经配置的远程仓库服务器，可以运用`git remote` 命令，它会列出你指定的每一个远程服务器的简写。如果已经克隆了自己的仓库，那么至少应该能看到 origin，这是 Git 给克隆的仓库服务器的默认名字。可以指定选项`-v`，会显示需要读写远程仓库使用的 Git 保存的简写与其对应的 URL。如果远程仓库不止一个，该命令会将它们全部列出。

```powershell
$ git remote
origin

$ git remote -v
origin	https://github.com/schacon/ticgit (fetch)
origin	https://github.com/schacon/ticgit (push)
```



添加远程仓库。运行 `git remote add <shortname> <url>` 添加一个新的远程 Git 仓库，同时指定一个可以轻松引用的简写。

```powershell
$ git remote add pb https://github.com/paulboone/ticgit
$ git remote -v
origin	https://github.com/schacon/ticgit (fetch)
origin	https://github.com/schacon/ticgit (push)
pb	https://github.com/paulboone/ticgit (fetch)
pb	https://github.com/paulboone/ticgit (push)
```



从远程仓库中抓取与拉取。从远程仓库中获得数据，可以执行`git fetch [remote-name]`，这个命令会访问远程仓库，从中拉取所有本地还没有的数据。执行完成后，将会拥有那个远程仓库中所有分支的引用，可以随时合并或查看。

如果使用`close`命令克隆了一个仓库，命令会自动将其添加为远程仓库并默认以“origin”为简写。所以，`git fetch origin` 会抓取克隆（或上一次抓取）后新推送的所有工作。

必须注意 `git fetch` 命令会将数据拉取到你的本地仓库 ，它并不会自动合并或修改你当前的工作。 当准备好时你必须手动将其合并入你的工作。

如果有一个分支设置为跟踪一个远程分支，可以使用 `git pull`命令来自动的抓取然后合并远程分支到当前分支。 这可能是一个更简单或更舒服的工作流程；默认情况下，`git clone` 命令会自动设置本地 master 分支跟踪克隆的远程仓库的 master 分支， 运行 `git pull` 通常会从最初克隆的服务器上抓取数据并自动尝试合并到当前所在的分支。

```powershell
$ git fetch pb
remote: Counting objects: 43, done.
remote: Compressing objects: 100% (36/36), done.
remote: Total 43 (delta 10), reused 31 (delta 5)
Unpacking objects: 100% (43/43), done.
From https://github.com/paulboone/ticgit
 * [new branch]      master     -> pb/master
 * [new branch]      ticgit     -> pb/ticgit
```



推送到远程仓库。使用`git push [remote-name] [branch-name]`可以将 master 分支推送到 `origin` 服务器时），那么运行这个命令就可以将所做的备份到服务器。

只有当有克隆服务器的写入权限，并且之前没有人推送过时，这条命令才能生效。 当和其他人在同一时间克隆，他们先推送到上游然后你再推送到上游，你的推送就会毫无疑问地被拒绝。 你必须先将他们的工作拉取下来并将其合并进你的工作后才能推送。

```powershell
$ git push origin master
```



查看远程仓库。如果想查看某一个远程仓库的更多信息，可以使用 `git remote show [remote-name]` 命令。还可以告诉你运行推送和拉取命令时，所有引用抓取和分支合并的情况。

```powershell
$ git remote show origin
* remote origin
  Fetch URL: https://github.com/schacon/ticgit
  Push  URL: https://github.com/schacon/ticgit
  HEAD branch: master
  Remote branches:
    master                               tracked
    dev-branch                           tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (up to date)
```



远程仓库的移除与重命名。如果想要重命名引用的名字可以运行 `git remote rename` 去修改一个远程仓库的简写名。例如，想要将 `pb` 重命名为 `paul`， 就可以使用`git remote rename pb paul`命令。值得注意的是这同样也会修改远程分支的名字。如果因为一些原因想要移除一个远程仓库，又或者某一个贡献者不再贡献了，可以使用 `git remote rm` 。

```powershell
$ git remote rename pb paul
$ git remote
origin
paul

$ git remote rm paul
$ git remote
origin
```