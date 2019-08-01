> presented by TOWER  
> Version control with Git - made easy  
 
 # GITCHEAT SHEET
 
 ## CREATE
 
 Clone an existing repository  

 ```sh
 $ git clone ssh://user@domain.com/repo.git # 克隆现有仓库
 ```

 Create a new local repository  

 ```sh
 $ git init # 创建新的本地仓库
 ```
 
 ## LOCAL CHANGES
 
 Changed files in your working directory  
 
 ```sh
 $ git status  # 更改了工作目录中的文件
 ```

 Changes to tracked files  
 
 ```sh
 $ git diff  # 对跟踪文件的更改
 ```

 Add all current changes to the next commit  

 ```sh
 $ git add .  # 将所有当前更改添加到下一个提交
 ```

 Add some changes in `<file>` to the next commit  
 
 ```sh
 $ git add -p <file>  # 向下一次提交中添加中的一些更改
 ```
 
 Commit all local changes in tracked files  
 
 ```sh
 $ git commit -a  # 提交跟踪文件中的所有本地更改
 ```
 
 Commit previously staged changes  
 
 ```sh
 $ git commit  # 提交之前暂存的更改
 ```
 
 Change the last commit. Don‘t amend published commits!  
 
 ```sh
 $ git commit --amend    # 更改最后一次提交。不要修改发布的提交！
 ```
 
 ## COMMIT HISTORY
 Show all commits, starting with newest  
 
 ```sh
 $ git log  # 显示所有提交，从最新开始
 ```
 
 Show changes over time for a specific file 
 
 ```sh
 $ git log -p <file>  # 显示随时间变化的特定文件
 ```
 
 Who changed what and when in `<file>`  
 
 ```sh
 $ git blame <file>  # 谁改变了什么文件，何时改变了文件
 ```
 
 ## BRANCHES & TAGS
 
 List all existing branches  

 ```sh
 $ git branch -av  # 列出所有现有分支
 ```
 
 Switch HEAD branch  
 
 ```sh
 $ git checkout <branch>  # 切换HEAD分支
 ```
 
 Create a new branch based on your current HEAD  
 
 ```sh
 $ git branch <new-branch>  # 根据您当前的 HEAD 创建一个新分支
 ```
 
 Create a new tracking branch based on a remote branch  
 
 ```sh
 $ git checkout --track <remote/branch>  # 基于远程分支创建新的跟踪分支
 ```
 
 Delete a local branch  

 ```sh
 $ git branch -d <branch>  # 删除本地分支
 ```
 
 Mark the current commit with a tag  

 ```sh
 $ git tag <tag-name>  # 使用 tag 标记当前提交
 ```
 
 ## UPDATE & PUBLISH
 List all currently configured remotes  
 
 ```sh
 $ git remote -v  # 列出所有当前配置的远程设备
 ```
 
 Show information about a remote  
 
 ```sh
 $ git remote show <remote>  # 
 ```
 
 Add new remote repository, named `<remote>`  

 ```sh
 $ git remote add <shortname> <url>  # 
 ```
 
 Download all changes from `<remote>`,  but don‘t integrate into HEAD  

 ```sh
 $ git fetch <remote>  # 
 ```

 Download changes and directly merge/integrate into  HEAD  

 ```sh
 $ git pull <remote> <branch>  # 下载更改并直接合并/集成到HEAD中
 ```

 Publish local changes on a remote  
 
 ```sh
 $ git push <remote> <branch>  # 在远程上发布本地更改
 ```

 Delete a branch on the remote  
 
 ```sh
 $ git branch -dr <remote/branch>  # 删除远程设备上的分支
 ```

 Publish your tags  
 
 ```sh
 $ git push --tags  # 发布你的标签
 ```

 MERGE & REBASE
 
 Merge `<branch>` into your current HEAD  
 
 ```sh
 $ git merge <branch>  # 合并`<branch>` 进你当前的HEAD
 ```

 Rebase your current HEAD onto `<branch>` Don‘t rebase published commits!  
 
 ```sh
 $ git rebase <branch>   # 将当前的HEAD重新打开 不要重新发布已发布的提交！
 ```

 Abort a rebase  
 
 ```sh
 $ git rebase --abort  # 中止一个变基
 ```

 Continue a rebase after resolving conflicts  
 
 ```sh
 $ git rebase --continue  # 解决冲突后继续变基
 ```

 Use your configured merge tool to  solve conflicts  
 
 ```sh
 $ git mergetool  # 使用配置的合并工具解决冲突
 ```

 Use your editor to manually solve conflicts and  (after resolving) mark file as resolved  
 
 ```sh
 $ git add <resolved-file>  # 使用编辑器手动解决冲突并（解析后）将文件标记为已解决
```

 ```sh
 $ git rm <resolved-file>  
 ```

 ## UNDO

 Discard all local changes in your working  directory  
 
 ```sh
 $ git reset --hard HEAD  # 放弃工作目录中的所有本地更改
 ```

 Discard local changes in a specific file  

 ```sh
 $ git checkout HEAD <file>  # 放弃特定文件中的本地更改
 ```

 Revert a commit  (by producing a new commit with contrary changes)  

 ```sh
 $ git revert <commit>  # 恢复提交（通过生成具有相反更改的新提交）
 ```

 Reset your HEAD pointer to a previous commit...and discard all changes since then  

 ```sh
 $ git reset --hard <commit>  # 将HEAD指针重置为先前的提交...并放弃此后的所有更改
 ```

 ...and preserve all changes as unstaged changes  

 ```sh
 $ git reset <commit>  # ...并将所有更改保留为未暂存更改
 ```

 ...and preserve uncommitted local changes  

 ```sh
 $ git reset --keep <commit>  # ...并保留未提交的本地更改
```

## COMMIT RELATED CHANGES

A commit should be a wrapper for related changes. For example, fixing two different bugs should produce two separate commits. Small commits make it easier for other developers to understand the changes and roll them back if something went wrong.     
With tools like the staging area and the ability to stage only parts of a file, Git makes it easy to create very granular commits. 

一个提交应该是相关更改的集合。例如，修复两个不同的bug应该发出两个单独的提交。提交消息使其他开发者更容易理解，同时如果出了什么问题就可以把它们退回去。    
有了诸如分阶段区域和对文件的部分进行暂存的能力，Git使创建很细致的提交变得非常容易。

## COMMIT OFTEN 

Committing often keeps your commits small and, again, helps you commit only related changes. Moreover, it allows you to share your code more frequently with others. That way it‘s easier for everyone to integrate changes regularly and avoid having merge conflicts. Having few large commits and sharing them rarely, in contrast, makes it hard to solve conflicts.

提交经常使您的承诺保持较小，并且再次帮助您提交仅相关的更改。此外，它允许您更频繁地与其他人共享代码。这样对每个人来说都比较容易定期集成更改，避免合并冲突。相反，很少有大量的提交，并且很少分享它们，这使得解决冲突变得困难。

## DON‘T COMMIT HALF-DONE WORK 

You should only commit code when it‘s completed. This doesn‘t mean you have to complete a whole, large feature before committing. Quite the contrary: split the feature‘s implementation into logical chunks and remember to commit early and often. But don‘t commit just to have something in the repository before leaving the office at the end of the day. If you‘re tempted to commit just because you need a clean working copy (to check out a branch, pull in changes, etc.) consider using Git‘s «Stash» feature instead.

您应该只在代码完成时提交代码。这并不意味着您必须在提交之前完成一个完整的大型功能。完全相反：分裂特性的实现分为逻辑块，并记住要尽早提交和经常提交。但是，在一天结束之后离开办公室，不要只是为了在仓库中留下一些东西而提交代码。如果仅仅因为需要一个干净的工作副本（为了检索分支，拉取变化等）而想提交代码，可以考虑使用Git的«stash»功能。

## TEST CODE BEFORE YOU COMMIT 

Resist the temptation to commit some-thing that you «think» is completed. Test it thoroughly to make sure it really is completed and has no side effects (as far as one can tell). While committing half-baked things in your local repository only requires you to forgive yourself, having your code tested is even more important when it comes to pushing/sharing your code with others.

反对冒着风险去做一些你自己认为已经完成的事情。彻底测试它，以确保它真的完成了，而且没有副作用（尽力）。虽然在本地存储库中提交半成品，只需要您原谅自己就行，但是涉及到推送/与他人共享代码时，进行代码测试就更重要了。

## WRITE GOOD COMMIT MESSAGES

Begin your message with a short summary of your changes (up to 50 characters as a gui-deline). Separate it from the following body by including a blank line. The body of your message should provide detailed answers to the following questions: 

- What was the motivation for the change?
- How does it differ from the previous implementation?  

Use the imperative, present tense («change», not «changed» or «changes») to be consistent with generated messages from commands like git merge.

开始您的消息，以一个简短的变化总结（多达50个字符就作为一个指导原则）。将它与下面的正文分隔开，方法是包含一个空行。您的消息正文应该提供如以下问题的详细解答：

- 改变的动机是什么？  
- 它与以前的实施方式有何不同？  

使用祈使句、现在时态（省去变化、不改变或改变），与来自Git合并的命令生成的消息一致。

## VERSION CONTROL IS NOT  A BACKUP SYSTEM

Having your files backed up on a remote server is a nice side effect of having a version control system. But you should not use your VCS like it was a backup system. When doing version control, you should pay attention to committing semantically (see «related changes») - you shouldn‘t just cram in files.

在远程服务器上备份文件是拥有版本控制系统的一个很好的方式。但是你不应该像使用备份系统一样使用你的VCS。在执行版本控制时，您将应该注意语义上的（见相关的变化）-而不应该只是在文件中填充。

## USE BRANCHES 

Branching is one of Git‘s most powerful features - and this is not by accident: quick and easy branching was a central requirement from day one. Branches are the perfect tool to help you avoid mixing up different lines of development. You should use branches extensively in your development workflows: for new features, bug fixes, ideas... 

分支是Git最强大的特性之一，这不是偶然的：从第一天起，快速和容易的分支是的最重要的要求。分支是帮助你避免混淆不同方向的生产的完美工具. 您应该在开发工作流程中广泛使用分支：用于新特性、bug修复、想法……

## AGREE ON A WORKFLOW 

Git lets you pick from a lot of different work-flows: long-running branches, topic branches, merge or rebase, git-flow... Which one you choose depends on a couple of factors: your project, your overall development and deployment workflows and (maybe most importantly) on your and your teammates‘ personal preferences. However you choose to work, just make sure to agree on a common workflow that everyone follows. 

Git允许您从许多不同的工作流中选择：长时间运行的分支、主题分支、合并或重基、git-flow等等。您选择哪一个取决于以下几个因素：你的项目，你的整体开发和部署工作流程，（也许最重要的）是你和你的队友的个人喜好。无论你选择哪一个工作，只要确保达成一个共同的每个人都遵循的工作流程。

## HELP & DOCUMENTATION 

Get help on the command line  

```sh
$ git help <command>  # 在命令行上获取帮助
```

## FREE ONLINE RESOURCES

http://www.git-tower.com/learn  
http://rogerdudler.github.io/git-guide/  
http://www.git-scm.org/ 
