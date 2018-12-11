> 精通GIt（第二版）
> Pro GIt
> 2017年9月第一次出版

# 第二章 Git基础

## 2.1 获取Git仓库

有两种取得 Git 项目仓库的方法，第一种是在现有项目或目录下导入所有文件到 Git 中，第二种是从一个服务器克隆一个现有的 Git 仓库。

如果打算使用 Git 来对现有的项目进行管理，只需要进入该项目目录并输入以下命令。该命令将创建一个名为 `.git` 的子目录，这个子目录含有你初始化的 Git 仓库中所有的必须文件，这些文件是 Git 仓库的骨干。 此时，项目里的文件还没有被跟踪。可通过 `git add` 命令来实现对指定文件的跟踪，然后执行 `git commit` 提交。

```powershell
$ git init 

$ git add *.c
$ git add LICENSE
$ git commit -m 'initial project version'
```



克隆现有的仓库。Git 克隆的是该 Git 仓库服务器上的几乎所有数据，而不是仅仅复制完成你的工作所需要文件。 当执行 `git clone` 命令的时候，默认配置下远程 Git 仓库中的每一个文件的每一个版本都将被拉取下来。如下命令，会在当前目录下创建一个名为 “libgit2” 的目录，并在这个目录下初始化一个 `.git` 文件夹，从远程仓库拉取下所有数据放入 `.git` 文件夹，然后从中读取最新版本的文件的拷贝。同时可以在克隆远程仓库的时候，自定义本地仓库的名字。

```powershell
$ git clone https://github.com/libgit2/libgit2

$ git clone https://github.com/libgit2/libgit2 mylibgit
```



## 2.2 记录每次更新到仓库

工作目录下的每一个文件有两种状态：已跟踪或未跟踪。 已跟踪的文件是指那些被纳入了版本控制的文件，在上一次快照中有它们的记录，在工作一段时间后，它们的状态可能处于未修改，已修改或已放入暂存区。 工作目录中除已跟踪文件以外的所有其它文件都属于未跟踪文件，它们既不存在于上次快照的记录中，也没有放入暂存区。 初次克隆某个仓库的时候，工作目录中的所有文件都属于已跟踪文件，并处于未修改状态。

编辑过某些文件之后，由于自上次提交后你对它们做了修改，Git 将它们标记为已修改文件。 我们逐步将这些修改过的文件放入暂存区，然后提交所有暂存了的修改，如此反复。所以使用 Git 时文件的生命周期如下：

![Git ä¸æä"¶çå½å¨æå¾ã](https://git-scm.com/book/en/v2/images/lifecycle.png)

要查看哪些文件处于什么状态，可以用 `git status` 命令。

使用命令 `git add` 开始跟踪一个文件。

只要在 `Changes to be committed` 这行下面的，就说明是已暂存状态。 如果此时提交，那么该文件此时此刻的版本将被留存在历史记录中。 如果出现`Changes not staged for commit` ，说明已跟踪文件的内容发生了变化，但还没有放到暂存区。

`git add` 命令使用文件或目录的路径作为参数；如果参数是目录的路径，该命令将递归地跟踪该目录下的所有文件。

`git status` 命令的输出十分详细，但其用语有些繁琐。 如果你使用 `git status -s` 命令或 `git status --short` 命令，你将得到一种更为紧凑的格式输出。 

一般我们总会有些文件无需纳入 Git 的管理，也不希望它们总出现在未跟踪文件列表。 通常都是些自动生成的文件，比如日志文件，或者编译过程中创建的临时文件等。 在这种情况下，我们可以创建一个名为 `.gitignore` 的文件，列出要忽略的文件模式。

文件 `.gitignore` 的格式规范如下：

- 所有空行或者以 `＃` 开头的行都会被 Git 忽略。
- 可以使用标准的 glob 模式匹配。
- 匹配模式可以以（`/`）开头防止递归。
- 匹配模式可以以（`/`）结尾指定目录。
- 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（`!`）取反。

所谓的 glob 模式是指 shell 所使用的简化了的正则表达式。 星号（`*`）匹配零个或多个任意字符；`[abc]`匹配任何一个列在方括号中的字符（这个例子要么匹配一个 a，要么匹配一个 b，要么匹配一个 c）；问号（`?`）只匹配一个任意字符；如果在方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配（比如 `[0-9]` 表示匹配所有 0 到 9 的数字）。 使用两个星号（`*`) 表示匹配任意中间目录，比如`a/**/z` 可以匹配 `a/z`, `a/b/z` 或 `a/b/c/z`等。

尽管 `git status` 已经通过在相应栏下列出文件名的方式回答了这个问题，`git diff` 将通过文件补丁的格式显示具体哪些行发生了改变。此命令比较的是工作目录中当前文件和暂存区域快照之间的差异， 也就是修改之后还没有暂存起来的变化内容。若要查看已暂存的将要添加到下次提交里的内容，可以用 `git diff --cached` 命令。（Git 1.6.1 及更高版本还允许使用 `git diff --staged`，效果是相同的，但更好记些。）

每次准备提交前，先用 `git status` 看下，是不是都已暂存起来了， 然后再运行提交命令 `git commit`进行妥当第提交。默认的提交消息包含最后一次运行 `git status` 的输出，放在注释行里，另外开头还有一空行，供你输入提交说明。 退出编辑器时，Git 会丢掉注释行，用你输入提交附带信息生成一次提交。也可以在 `commit` 命令后添加 `-m` 选项，将提交信息与命令放在同一行。

Git 提供了一个跳过使用暂存区域的方式， 只要在提交的时候，给 `git commit` 加上 `-a` 选项，Git 就会自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 `git add` 步骤。

要从 Git 中移除某个文件，就必须要从已跟踪文件清单中移除（确切地说，是从暂存区域移除），然后提交。 可以用 `git rm` 命令完成此项工作，并连带从工作目录中删除指定的文件，这样以后就不会出现在未跟踪文件清单中了。如果只是简单地从工作目录中手工删除文件，运行 `git status` 时就会在 “Changes not staged for commit” 部分（也就是 *未暂存清单*），然后再运行 `git rm` 记录此次移除文件的操作。下一次提交时，该文件就不再纳入版本管理了。 

如果删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项 `-f`（译注：即 force 的首字母）。 这是一种安全特性，用于防止误删还没有添加到快照的数据，这样的数据不能被 Git 恢复。

另外一种情况是，如果想把文件从 Git 仓库中删除，也是从暂缓区中移除，也忘记将它们添加到`.gitignore` 文件，但仍然希望保留在当前工作目录中，可以使用 `--cached` 选项。

`git rm` 命令后面可以列出文件或者目录的名字，也可以使用 `glob` 模式。

不像其它的 VCS 系统，Git 并不显式跟踪文件移动操作。 如果在 Git 中重命名了某个文件，仓库中存储的元数据并不会体现出这是一次改名操作。不过 Git 非常聪明，它会推断出究竟发生了什么。要在 Git 中对文件改名，可以直接运行 `git mv` 就行了。其实，运行 `git mv` 就相当于运行了下面三条命令

```powershell
$ git mv file_from file_to

$ mv README.md README
$ git rm README.md
$ git add README
```



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