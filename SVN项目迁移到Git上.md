
# SVN项目迁移到Git上（并带有完整的提交记录） #

公司需求：早期的一些项目使用的是SVN，现在想要更换为Git，需要代码迁移并且能在Git上看到之前在SVN中的项目的提交记录，公司没有使用gitlab，代码都push在公司的服务器上，用的是TortoiseGit来管理的。

 

第一步：公司服务器系统（centos6.8），安装git

    yum -y install git

第二步：创建git用户：

    useradd git  #创建名称为git的用户
    passwd git   #git用户对应的密码也为git

第三步：创建git仓库：

    mkdir /home/git/gitrepo
    cd /home/git/gitrepo
    git init --bare test.git
    chown -R git:git test.git

第四步：开始将svn代码做迁移操作，在windows上任意创建一个空文件夹GitTest，作为一个Git本地仓库，用来存放从SVN上迁移过来的代码。


第五步：在这个文件中打开Git Bash


第六步： 在GitBash中输入clone的命令，在Bash中输入如下指令, 就会开始迁移”git svn clone svnUrl”, 其中里面的svnUrl就是你要迁移的项目的SVN地址

    git svn clone svnUrl

这时会弹出来两个对话框, 让你输入SVN的账号和密码, 当你输入正确的SVN账号和密码时, 代码就会开始迁移. 就会出现如下类似的log



这就表示迁移成功了, 现在要想看以前的提交记录是否迁移过来的话, 我们就需要在命令行里进入的本地仓库根目录中(也就是带有.git的目录), 进入之后输入git log, 就可以看到以前的提交记录了。

第七步：push本地仓库到远程服务器仓库，注意：首先要确保你的远程服务器上有这么一个仓库

    #git remote add origin  git@192.168.66.13:/home/git/gitrepo/test.git

进行这两个操作的时候, 会提示你输入你的Git的账号和密码, 点击ok之后就会进行push操作.
注意: 这一步的时候可能会提示一个错误:fatal: remote origin already exists.

如果出现如上所说的错误，解决办法：

    $ git remote rm origin #删除远程git仓库

然后在执行第七步。

完成以上步骤后，测试一下，使用TortoiseGit客户端clone项目

在查看下是否有提交信息

转载于:https://www.cnblogs.com/new-journey/p/10178883.html