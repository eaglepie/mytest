Git 常用使用说明（以windows为例）：

第一，下载并安装git，百度或者谷歌搜git 到官方下载即可。有windows，linux以及mac几个版本，下载自己系统的对应版本即可。
第二，创建github账号，打开网址https://github.com注册一个帐号。
什么是Git和GitHub
Git —The stupid content tracker, 傻瓜内容跟踪器，是一个由Linux内核开发者Linus为了更好地管理Linux内核开发而创立的分布式版本控制软件。
GitHub — 学生做版本控制最讨厌的就是找服务器，配置太麻烦了。GitHub这个网站为每个用户提供服务器托管其Git代码库，免费空间为300M。注册GitHub后你就会有0.3G的免费空间，不过只能创建公开项目。
为什么不选CVS或SVN
Git提交/克隆/pull/push的速度更快
Git的绝大多数操作都可以在本地完成，不需要频繁连接服务器。
GitHub选择的默认通信方式是SSH，所以要先在Git里面生成SHH Key，打开Git Bash在其中输入如下命令：
$ ssh-keygen -t rsa -C "3sdfsf80@xinlang.com"
之后会让你选择是否对存放SSH Key的文件夹进行加密，一般都不需要的。一路回车，就OK了。
在c盘，当前用户文件夹下，有个.ssh 文件夹，在里边 找到 id_rsa.pub文件，用记事本打开，复制其中的全部内容。
登陆你的GitHub账户，依次点击Account Settings > SSH Public Keys > Add another public key，把id_rsa.pub中的内容拷贝进去 。
至此，基本的设置已经完成了。
测试你的Git

经过上述配置，你的Gti应该可以通过SSH连接GitHub服务器了，让我们来测试下，输入如下命令：
$ ssh -T git@github.com

The authenticity of host 'github.com (xxx.xxx.xxx.xxx)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'github.com,xxx.xxx.xxx.xxx' (RSA) to the list of known hosts.
Hi eaglepie! You've successfully authenticated, but GitHub does not provide shell access.

如上提示会在“C:\Users\电脑用户名\Desktop\Vscode\.ssh”目录下生成一个“known_hosts”的文件夹。

会给出提示，输入“yes”即可。
如果提示“Hi username! You've successfully authenticated,....”就表示你的ssh运作良好。
如果提示你的密钥不正确，那么你需要重新确认上一步的操作是否完整无误。
第三，建立本地git仓库

首先，git要求使用者必须提供自己的身份标识，为此我们需要在git bash中执行以下命令：

$ git config --global user.name  'yourname'
$ git config --global user.email  youremail@xxx.com

其次，选择git仓库目录

我们假设将git仓库目录放在D盘的OpenSource目录下，可以通过在git bash中执行以下命令完成：

$ cd /d 【切换到D盘】
$ mkdir OpenSource  【创建目录】
$ cd OpenSource 【切换到创建的目录文件，很重要】
$ pwd 【pwd命令用于显示当前目录。会显示“/d/OpenSource”】

注：git bash支持大多linux bash终端命令，你可以自己尝试更多终端操作。

最后，建立项目并初始化git仓库，运行命令。

$ git init

执行此操作后，git将在OpenSource目录下创建一个隐藏目录（.git），这个目录就是git用来管理软件版本的仓库。
这里是直接在OpenSource目录下创建的git仓库，当然你也可以切换到OpenSource目录，然后在此目录下再创建目录以及git仓库。

如果你没有看到.git目录，那是因为这个目录默认是隐藏的，用ls -ah命令就可以看见。

现在我们编写一个readme.txt文件，内容如下：
Git is a version control system.
Git is free software.
一定要放到OpenSource目录下（子目录也行），因为这是一个Git仓库，放到其他地方Git再厉害也找不到这个文件。
第一步，用命令git add告诉Git，把文件添加到仓库：
git add readme.txt
执行上面的命令，没有任何显示，这就对了，Unix的哲学是“没有消息就是好消息”，说明添加成功。

第二步，用命令git commit告诉Git，把文件提交到仓库：

$ git commit -m "wrote a readme file"
简单解释一下git commit命令，-m后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。

嫌麻烦不想输入-m "xxx"行不行？确实有办法可以这么干，但是强烈不建议你这么干，因为输入说明对自己对别人阅读都很重要。实在不想输入说明的童鞋请自行Google，我不告诉你这个参数。

git commit命令执行成功后会告诉你，1个文件被改动（我们新添加的readme.txt文件），插入了两行内容（readme.txt有两行内容）。

为什么Git添加文件需要add，commit一共两步呢？因为commit可以一次提交很多文件，所以你可以多次add不同的文件，比如：

$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "add 3 files."

第四，使用git管理项目(略过)

第五，将项目提交到github管理，gitpush
如果 第二步(第二，创建github账号) 测试无错，那么 经过 以下两步 就可以将本地的文件提交到github仓库了。
1、登录GitHub后，你可以在右上边靠中那里找到一个按钮“creat a New Repository”，点击过后，填入项目名称、说明等 过后就可以创建了，然后会出现一个提示页面，记下类似  git@github.com:XXX/XXX.git 的地址，这个就是你这个项目的地址了。
【第一个xxx是你的git用户名，第二个xxx是你刚刚建立的项目名称】
目前，在GitHub上的这个mytest仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。

现在，我们根据GitHub的提示，在本地的OpenSource仓库下运行命令：

$ git remote add origin git@github.com:eaglepie/mytest.git
$ git push -u origin master
如果出现错误提示“error: failed to push some refs to 'git@github.com:eaglepie/mytest.git'”
出现错误的主要原因是github中的README.md文件不在本地代码目录中
可以通过如下命令进行代码合并【注：pull=fetch+merge]
$ git pull --rebase origin master
执行上面代码后可以看到本地代码库中多了README.md文件
此时再执行语句 git push -u origin master即可完成代码上传到github

尝试增加一个新文件用以测试 Git 是否好好工作。
结果在 Push 时却显示
Branch master set up to track remote branch master from origin.
Everything up-to-date
检查文件时却发现实际上一个都没更新上去。
再执行下面的语句：
$ git add Git_Readme.txt 【这句好像一定要执行】
$ git commit -m "how to use git" 【一定要重新写commit，这个内容可以写中文，已测试】

如果commit不成功就会提示如下：

On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
        modified:   Git_Readme.txt
        
如果commit成功就会提示：

[master 6407d9f] add a error fixed
 1 file changed, 16 insertions(+)


$ git push -u origin master 【再执行这个语句就可以提交了】


参考网址：
http://www.runoob.com/git/git-tutorial.html
http://www.bootcss.com/p/git-guide/
http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000
http://blog.csdn.net/wh_19910525/article/details/8128916【非常好的博文】
http://www.jianshu.com/p/8d26730386f3【github上传时出现error: src refspec master does not match any解决办法】
http://www.jianshu.com/p/835e0a48c825【如何解决failed to push some refs to git】

git push 提示 Everything up-to-date的参考网址：
http://blog.csdn.net/g1036583997/article/details/50532651
http://blog.csdn.net/kangear/article/details/10822805 
如果新建一个分支要切过去才能push到这个分支，不然还在master分支，就会出现这个错误。切回去后commit要重新填。之后就没有问题了。

http://www.oschina.net/question/68606_238945
问：Virtual Studio Code 如何关闭已经打开的目录？
答：打开一个新窗口 然后关闭原先的，打开新的目录就行啊
