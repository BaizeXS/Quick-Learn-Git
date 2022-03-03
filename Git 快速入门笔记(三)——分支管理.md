# Git 快速入门笔记(三)——分支管理

0. 为什么要使用分支？

   所谓分支，可以理解为多元宇宙的时间线。在Marvel多元宇宙中，有一个宇宙被称为主宇宙，而我们在开发项目的过程中也会有一条“主时间线”，通常称其为`master分支`或`main分支`。

   那么分支有什么用呢？我们在开发一个项目的时候，通常会开发多个功能，在完成核心功能后，其余功能可以分给几个小伙伴分别开发接口。为了让每个人都能够同时进行开发，并且在开发过程中不对“主时间线”产生不必要的“影响”，我们可以使用分支技术。即每个人都可以创建一个属于自己的分支，别人看不到，还可以继续在原来分支基础上正常工作。开发完毕后，多个功能可以同时或者不同时一次性合并到“主时间线”上，从而提高开发效率。

1. **分支基础命令**

- 查看分支

  ```shell
  git branch
  ```

- 创建分支

  ```shell
  git branch <name>
  ```

- 切换分支

  ```shell
  # 方法一
  git checkout <name>
  # 方法二
  git switch <name>
  ```

- 创建并切换分支

  ```shell
  # 方法一
  git checkout -b <name>
  # 方法二
  git switch -c <name>
  ```

- 合并某分支到当前分支

  通常会使用快速合并，即`Fast Forward`。两种合并模式的主要区分如下：

  - 普通模式合并，合并后的历史有分支，能看出来曾经做过合并
  - 而`Fast Forward`合并就看不出来曾经做过合并。普通模式合并要创建一个新的`commit`，所以加上`-m`参数

  ```shell
  # 快速合并Fast Forward
  git merge <name>
  # 普通模式合并
  git merge --no-ff -m "Some Message" <name>
  ```

- 删除分支

  ```shell
  # 删除分支
  git branch -d <name>
  # 强制删除分支
  git branch -D <name>
  ```

- 暂存工作区

  Git还提供了一个`stash`功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作。恢复暂存区有两种方式：

  - 使用`git stash apply`时，stash内容并不删除，需要运行`git stash drop`来删除
  - 使用`git stash pop`时，会自动将stash中的内容删除

  ```shell
  # 创建暂存区
  git stash
  # 查看暂存区
  git stash list
  # 恢复暂存区且不删除stash中的内容
  git stash apply
  # 恢复暂存区且删除stash中的内容
  git stash pop
  ```

- 复制一个特定的提交到当前分支

  例如在`master`分支上修复的bug，想要合并到当前dev分支，可以用`git cherry-pick <commit>`命令，把bug提交的修改“复制”到当前分支，避免重复劳动。

  ```shell
  git cherry-pick <commit id>
  ```

- 查看分支合并图

  ```shell
  git log -- graph
  ```

- 推送分支

  ```shell
  git push origin <branch name>
  ```

- 在本地创建和远程分支对应的分支

  ```shell
  git checkout -b branch-name origin/branch-name
  ```

- 建立本地分支和远程分支的关联

  ```shell
  git branch --set-upstream branch-name origin/branch-name
  ```

- 抓取分支

  ```shell
  git pull
  ```

  若有冲突，要先处理冲突。当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。

- Rebase

  ```shell
  git rebase
  ```

  rebase操作可以把本地未push的分叉提交历史整理成直线

  



