# Git 快速入门笔记(四)——标签管理及琐碎

0. Q：为什么要使用标签？

   A：我们都知道，Git对版本仓库的管理，主要依赖于一个类似于指针的功能，记录了每一次的`commit`。但是`commit ID`太难记了，所以我们使用一些标签来指向特定的仓库中一些特别的`commit`。

1. 创建标签

   - 创建标签

     ```shell
     git tag <name> <commit id>
     ```

   - 创建带有说明的标签

     ```shell
     git tag -a <name> -m <"message"> <commit id>
     ```

   - 查看所有标签

     ```shell
     git tag
     ```

   - 查看标签信息

     ```shell
     git show <tagname>
     ```

2. 操作标签

   - 删除标签

     ```shell
     git tag -d <name>
     ```

   - 推送本地标签到远程

     ```shell
     git push origin <tagname>
     ```

   - 推送全部本地标签到远程

     ```shell
     git push origin --tags
     ```

   - 删除远程标签

     先删除本地标签，再执行如下命令：

     ```shell
     git push origin :refs/tags/<tagname>
     ```

3. GitHub

   - GitHub上可以Fork任意开源仓库
   - 自己拥有Fork后的仓库的读写权限
   - 可以推送pull request给官方仓库来贡献代码

4. `.gitignore`

   一些配置文件等不需要上传到远程仓库的文件可以通过添加`.gitignore`文件忽略他们。