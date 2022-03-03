# Git 快速入门笔记(一)——基础知识

0. **Git是什么？**

   Git是目前世界上最先进的**分布式版本控制系统**。在Git管理的项目中，Git会记录每一次修改，以便操作人员进行文件/源码的版本控制与管理。可以参考一下[廖雪峰大佬博客的例子](https://www.liaoxuefeng.com/wiki/896043488029600/896067008724000)。

   注：本文也是一边看廖雪峰大佬的博客一边实践整理出的个人学习笔记。

1. **创建版本库**

   - 在合适的地方创建空文件夹，不妨命名为`learngit`

   - 在该文件夹下打开终端/CMD，确保当前路径为`xxx/learngit`后，输入

     ```shell
     git init
     ```

     对该文件夹进行初始化。命令执行完毕，Git已完成版本仓的新建。

2. **把文件添加到版本库**

   例如，我们需要向`learngit`库中添加`readme.txt`文件，只需要：

   - 在`learngit`文件夹下创建新文件`readme.txt`

   - 用`git add`命令将文件添加到本地仓库

     ```shell
     git add readme.txt
     ```

   - 用`git commit` 命令将文件提交到仓库

     ```shell
     git commit -m "Wrote a readme.txt"
     ```

     注意：`-m "..."`中，双引号内的内容为本次提交的说明。

3. **查看仓库当前状态**

   查看自上次提交后，有哪些文件被修改过：

   ```shell
   git status
   ```

   查看自上次提交后，文件被修改的内容：

   ```shell
   git diff
   ```

4. **查看仓库更新历史记录：**

   ```shell
   git log
   ```

   如果嫌输出信息太多，看得眼花缭乱的，可以试试加上`--pretty=oneline`参数。

   在`log`中，`commit`之后跟着的便是每一次提交操作完成后的`commit ID`，即版本号。

5. **版本回退**

   Git中，用`HEAD`表示当前版本，上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个`^`比较容易数不过来，所以写成`HEAD~100`。

   退回至上一版本：

   ```shell
   git reset --hard HEAD^
   ```

   退回至任一版本：

   ```shell
   git reset --hard commit_id
   ```

   Git提供了一个命令`git reflog`用来记录你的每一次命令，即**可以查看命令历史**，以便决要回到未来的那个版本。

6. **撤销修改**

   仍然以`readme.txt`文件为例，若`readme.txt`**自修改后还没有放到暂缓区**或者`readme.txt`**已经添加到暂存区后，又进行了修改**，则可以使用`git checkout -- file`可以丢弃工作区的修改：

   ```shell
   git checkout -- readme.txt
   ```

   若是**修改后已经添加到暂存区并且还未提交**，则可以使用`git reset HEAD <file>`将暂存区的修改撤销：

   ```shell
   git reset HEAD readme.txt
   ```

   若是**修改后已经添加到暂存区并且提交**，则需要使用版本回退。

7. **删除文件**

   一般情况下，可以直接将文件夹中没用的文件删了，而后使用`git rm file`命令将其从版本库中删除：

   ```shell
   git rm test.txt
   git commit -m "Delete test.txt"
   ```

   