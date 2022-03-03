# Git 快速入门笔记(二)——远程仓库

0. 为什么需要远程仓库

   现实中，我们会将某一台电脑作为服务器，每天24小时开机，其他每个人都可以从这个服务器仓库中克隆一份文件到自己的电脑，完成修改后再各自将修改后的文件推送到服务器仓库中，也从服务器仓库中拉取别人的提交。GitHub和Gitee等则是提供这种“服务器”的网站。

1. 基本设置

   因为需要连接到远程仓库，我们需要进行一下设置：

   - 注册GitHub账号

   - 在本地创建**==SSH Key==**：

     在终端/Git Bash中输入如下命令：

     ```shell
     $ ssh-keygen -t rsa -C "你用于注册Github的邮箱@example.com"
     ```

     在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件。这两个文件就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

   - 登陆Github，打开`Account settings`，选择`SSH Keys`页面，随后点击`Add SSH Key`

     <img src="https://gitee.com/baizexs/my_-picture_-host/raw/master/img/202203031731444.png" alt="GitHub" style="zoom:50%;" />

   - `title`可以随意填写，在Key文本框中粘贴`id_rsa.pub`的内容，随后点击`Add SSH Key`即可

     <img src="https://gitee.com/baizexs/my_-picture_-host/raw/master/img/NewRepo.png" alt="iShot2022-03-03 09.55.33" style="zoom:50%;" />

   - 注意：

     - GitHub允许添加多个SSH Key
     - 在GitHub上免费托管的Git仓库，是所有人可见的，但只有你自己能够修改。如果不想别人看到，可以自行搭建Git服务器或者向GitHub交点“保护费”，使用私有仓库。

2. 添加远程仓库

   - 创建远程仓库

     将鼠标移至“+”号，点击`New repository`

     <img src="https://gitee.com/baizexs/my_-picture_-host/raw/master/img/NewRepo2.png" alt="NewRepo" style="zoom:50%;" />

     填写仓库名，并点击`Creat repository`

     <img src="https://gitee.com/baizexs/my_-picture_-host/raw/master/img/NewRepo3.png" alt="NewRepo2" style="zoom:50%;" />

     其余几项为可选项。其中`Discription`为仓库内容的描述。`Public`表明这个仓库是公开的。后三项分别为`添加README文件`、`添加gitignore文件夹（忽略内容的文件夹）`和`选择开源证书`。

   - 将远程仓库与本地仓库关联

     在本地learngit仓库下，运行如下命令：

     ``` shell
     git remote add origin git@github.com:远程仓库路径.git
     ```

     例如我这里learngit仓库地址为

     <img src="https://gitee.com/baizexs/my_-picture_-host/raw/master/img/gitaddress.png" alt="Gitaddress" style="zoom:50%;" />

     那么我在本地learngit仓库下，运行命令应如下所示：

     ```shell
     git remote add origin git@github.com:baizexs/learngit.git
     ```

   - 把本地库的所有内容推送到远程库上

     第一次推送master分支到在远程仓库中，在本地learngit仓库下，执行如下命令：

     ```shell
     git push -u origin master
     ```

     `-u`参数将本地的`master`分支和远程的`master`分支关联起来。

     而后只要本地进行了提交操作，就可以执行如下命令将内容推送到GitHub：

     ```shell
     git push origin master
     ```

3. 删除远程仓库

   首先使用`git remote -v`命令查看远程库信息

   <img src="https://gitee.com/baizexs/my_-picture_-host/raw/master/img/remotev.png" alt="git remote -v" style="zoom:50%;" />

   随后根据名字删除，例如删除`origin`

   ```shell
   git remote rm origin
   ```

   注意：这里的删除只是解除了本地与远程的绑定，若想要彻底删除，可登陆GitHub后删除仓库。

4. 从远程克隆仓库

   ```shell
   git clone git@github.com:远程仓库路径.git
   ```

   即可从远程仓库克隆出一个本地库。（说白了就是从GitHub上下载下来了）

   注意：Git支持多种协议，如`https`，`ssh`等，但是`ssh`协议速度更快。