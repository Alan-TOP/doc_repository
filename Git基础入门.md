# Git基础入门

<a name="3f03f25b"></a>
# Git 基础
![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555316511502-5c9db65b-0681-409f-a787-5c6c2442c4ec.png#align=left&display=inline&height=92&originHeight=92&originWidth=220&size=0&status=done&width=220)<br />Git 是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。<br />Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。<br />Git 与常用的版本控制工具 CVS, Subversion 等不同，它采用了分布式版本库的方式，不必服务器端软件支持。

---
<a name="c5fd4de3"></a>
## Git 与 SVN 区别
Git 不仅仅是个版本控制系统，它也是个内容管理系统(CMS)，工作管理系统等。<br />如果你是一个具有使用 SVN 背景的人，你需要做一定的思想转换，来适应 Git 提供的一些概念和特征。<br />Git 与 SVN 区别点：
* **1、Git 是分布式的，SVN 不是**：这是 Git 和其它非分布式的版本控制系统，例如 SVN，CVS 等，最核心的区别。<br />
* **2、Git 把内容按元数据方式存储，而 SVN 是按文件：**所有的资源控制系统都是把文件的元信息隐藏在一个类似 .svn、.cvs 等的文件夹里。<br />
* **3、Git 分支和 SVN 的分支不同：**分支在 SVN 中一点都不特别，其实它就是版本库中的另外一个目录。<br />
* **4、Git 没有一个全局的版本号，而 SVN 有：**目前为止这是跟 SVN 相比 Git 缺少的最大的一个特征。<br />
* **5、Git 的内容完整性要优于 SVN：**Git 的内容存储使用的是 SHA-1 哈希算法。这能确保代码内容的完整性，确保在遇到磁盘故障和网络问题时降低对版本库的破坏。<br />

![](https://cdn.nlark.com/yuque/0/2019/jpeg/267458/1555316511500-06ea9da0-fd7e-4458-a9b0-10db3e485ab7.jpeg#align=left&display=inline&height=398&originHeight=398&originWidth=707&size=0&status=done&width=707)

<a name="c816a7f4"></a>
# Git 安装配置
在使用Git前我们需要先安装 Git。Git 目前支持 Linux/Unix、Solaris、Mac和 Windows 平台上运行。<br />Git 各平台安装包下载地址为：[http://git-scm.com/downloads](http://git-scm.com/downloads)

---
<a name="5eba9a9e"></a>
## Linux 平台上安装
Git 的工作需要调用 curl，zlib，openssl，expat，libiconv 等库的代码，所以需要先安装这些依赖工具。<br />在有 yum 的系统上（比如 Fedora）或者有 apt-get 的系统上（比如 Debian 体系），可以用下面的命令安装：<br />各 Linux 系统可以使用其安装包管理工具（apt-get、yum 等）进行安装：
<a name="c19a5136"></a>
### Debian/Ubuntu
Debian/Ubuntu Git 安装命令为：<br />$ apt-get install libcurl4-gnutls-dev libexpat1-dev gettext \<br />  libz-dev libssl-dev

$ apt-get install git

$ git --version<br />git version 1.8.1.2
<a name="8c194707"></a>
### Centos/RedHat
如果你使用的系统是 Centos/RedHat 安装命令为：<br />$ yum install curl-devel expat-devel gettext-devel \<br />  openssl-devel zlib-devel

$ yum -y install git-core

$ git --version<br />git version 1.7.1
<a name="ffede4ab"></a>
### 源码安装
我们也可以在官网下载源码包来安装，最新源码包下载地址：[https://git-scm.com/download](https://git-scm.com/download)<br />安装指定系统的依赖包：<br />########## Centos/RedHat ##########<br />$ yum install curl-devel expat-devel gettext-devel \<br />  openssl-devel zlib-devel

########## Debian/Ubuntu ##########<br />$ apt-get install libcurl4-gnutls-dev libexpat1-dev gettext \<br />  libz-dev libssl-dev<br />解压安装下载的源码包：<br />$ tar -zxf git-1.7.2.2.tar.gz<br />$ cd git-1.7.2.2<br />$ make prefix=/usr/local all<br />$ sudo make prefix=/usr/local install

---
<a name="7c59103e"></a>
## Windows 平台上安装
在 Windows 平台上安装 Git 同样轻松，有个叫做 msysGit 的项目提供了安装包，可以到 GitHub 的页面上下载 exe 安装文件并运行：<br />安装包下载地址：[https://gitforwindows.org/](https://gitforwindows.org/)<br />
![image.png](https://cdn.nlark.com/yuque/0/2019/png/267458/1555316775367-27c16809-3a5f-4981-9c79-80fa72dc4f7c.png#align=left&display=inline&height=406&name=image.png&originHeight=406&originWidth=521&size=36844&status=done&width=521)<br />完成安装之后，就可以使用命令行的 git 工具（已经自带了 ssh 客户端）了，另外还有一个图形界面的 Git 项目管理工具。<br />在开始菜单里找到"Git"->"Git Bash"，会弹出 Git 命令窗口，你可以在该窗口进行 Git 操作。

---
<a name="c7473e58"></a>
## Mac 平台上安装
在 Mac 平台上安装 Git 最容易的当属使用图形化的 Git 安装工具，下载地址为：<br />[http://sourceforge.net/projects/git-osx-installer/](http://sourceforge.net/projects/git-osx-installer/)<br />安装界面如下所示：<br />![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555316654922-b6525892-0caf-4a45-bab4-dc9f089a76ae.png#align=left&display=inline&height=252&originHeight=252&originWidth=350&size=0&status=done&width=350)

---
<a name="14e27b81"></a>
## Git 配置
Git 提供了一个叫做 git config 的工具，专门用来配置或读取相应的工作环境变量。<br />这些环境变量，决定了 Git 在各个环节的具体工作方式和行为。这些变量可以存放在以下三个不同的地方：
* `/etc/gitconfig` 文件：系统中对所有用户都普遍适用的配置。若使用 `git config` 时用 `--system` 选项，读写的就是这个文件。
* `~/.gitconfig` 文件：用户目录下的配置文件只适用于该用户。若使用 `git config` 时用 `--global` 选项，读写的就是这个文件。
* 当前项目的 Git 目录中的配置文件（也就是工作目录中的 `.git/config` 文件）：这里的配置仅仅针对当前项目有效。每一个级别的配置都会覆盖上层的相同配置，所以 `.git/config` 里的配置会覆盖 `/etc/gitconfig` 中的同名变量。

在 Windows 系统上，Git 会找寻用户主目录下的 .gitconfig 文件。主目录即 $HOME 变量指定的目录，一般都是 C:\Documents and Settings\$USER。<br />此外，Git 还会尝试找寻 /etc/gitconfig 文件，只不过看当初 Git 装在什么目录，就以此作为根目录来定位。
<a name="6e354188"></a>
### 用户信息
配置个人的用户名称和电子邮件地址：<br />$ git config --global user.name "runoob"<br />$ git config --global user.email test@runoob.com<br />如果用了 **--global** 选项，那么更改的配置文件就是位于你用户主目录下的那个，以后你所有的项目都会默认使用这里配置的用户信息。<br />如果要在某个特定的项目中使用其他名字或者电邮，只要去掉 --global 选项重新配置即可，新的设定保存在当前项目的 .git/config 文件里。
<a name="8bf0eeb1"></a>
### 文本编辑器
设置Git默认使用的文本编辑器, 一般可能会是 Vi 或者 Vim。如果你有其他偏好，比如 Emacs 的话，可以重新设置：:<br />$ git config --global core.editor emacs
<a name="5d109c23"></a>
### 差异分析工具
还有一个比较常用的是，在解决合并冲突时使用哪种差异分析工具。比如要改用 vimdiff 的话：<br />$ git config --global merge.tool vimdiff<br />Git 可以理解 kdiff3，tkdiff，meld，xxdiff，emerge，vimdiff，gvimdiff，ecmerge，和 opendiff 等合并工具的输出信息。<br />当然，你也可以指定使用自己开发的工具，具体怎么做可以参阅第七章。
<a name="f26379de"></a>
### 查看配置信息
要检查已有的配置信息，可以使用 git config --list 命令：<br />$ git config --list<br />http.postbuffer=2M<br />user.name=runoob<br />user.email=test@runoob.com<br />有时候会看到重复的变量名，那就说明它们来自不同的配置文件（比如 /etc/gitconfig 和 ~/.gitconfig），不过最终 Git 实际采用的是最后一个。<br />这些配置我们也可以在 **~/.gitconfig** 或 **/etc/gitconfig** 看到，如下所示：<br />vim ~/.gitconfig <br />显示内容如下所示：<br />[http]<br />    postBuffer = 2M<br />[user]<br />    name = runoob<br />    email = test@runoob.com<br />也可以直接查阅某个环境变量的设定，只要把特定的名字跟在后面即可，像这样：<br />$ git config user.name<br />runoob

<a name="935b6c41"></a>
# Git 工作区、暂存区和版本库

---

我们先来理解下Git 工作区、暂存区和版本库概念
* **工作区：**就是你在电脑里能看到的目录。
* **暂存区：**英文叫stage, 或index。一般存放在 ".git目录下" 下的index文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。
* **版本库：**工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。

下面这个图展示了工作区、版本库中的暂存区和版本库之间的关系：<br />![](https://cdn.nlark.com/yuque/0/2019/jpeg/267458/1555316901247-1ebdea8d-ae70-4252-bd72-cab553170310.jpeg#align=left&display=inline&height=357&originHeight=357&originWidth=683&size=0&status=done&width=683)

<a name="ca8311f8"></a>
# Git 基础操作
**git init**<br />Git 使用 **git init** 命令来初始化一个 Git 仓库，Git 的很多命令都需要在 Git 的仓库中运行，所以 **git init** 是使用 Git 的第一个命令。<br />在执行完成 **git init** 命令后，Git 仓库会生成一个 .git 目录，该目录包含了资源的所有元数据，其他的项目目录保持不变（不像 SVN 会在每个子目录生成 .svn 目录，Git 只在仓库的根目录生成 .git 目录）。<br />**git clone**<br />我们使用 **git clone** 从现有 Git 仓库中拷贝项目（类似 **svn checkout**）。<br />比如<br />$ git clone git://github.com/schacon/grit.git<br />执行该命令后，会在当前目录下创建一个名为grit的目录，其中包含一个 .git 的目录，用于保存下载下来的所有版本记录。<br />如果要自己定义要新建的项目目录名称，可以在上面的命令末尾指定新的名字：<br />$ git clone git://github.com/schacon/grit.git mygrit<br />**以下命令只做了解，后期使用工具完全可以代替命令行**<br />**git add**<br />git add命令可将该文件添加到缓存<br />**git status**<br />git status命令用于查看项目的当前状态<br />**git diff**<br />执行git diff来查看执行git status的结果的详细信息。<br />git diff命令显示已写入缓存与已修改但尚未写入缓存的改动的区别.git diff有两个主要的应用场景。
* 尚未缓存的改动：**git diff**
* 查看已缓存的改动：**git diff --cached**
* 查看已缓存的与未缓存的所有改动：**git diff HEAD**
* 显示摘要而非整个diff：**git diff --stat**
* <br />

**git commit**<br />使用git add命令将想要快照的内容写入缓存区，而执行git commit将缓存区内容添加到仓库中。<br />Git为你的每一个提交都记录你的名字与电子邮箱地址，所以第一步需要配置用户名和邮箱地址。<br />$ git config --global user.name'runoob'<br />$ git config --global user.email test@runoob.com<br />接下来我们写入缓存，并提交对hello.php的所有改动。在首个例子中，我们使用-m选项以在命令行中提供提交注释。 <br />**git reset HEAD**<br />git reset HEAD命令用于取消已缓存的内容。<br />**git rm**<br />如果只是简单地从工作目录中手工删除文件，运行**git status**时就会在**未提交**的**提交**的**更改**。<br />要从Git中移除某个文件，就必须要从已跟踪文件清单中移除，然后提交。可以用以下命令完成此项工作<br />git rm <file><文件><br />如果删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项**-f**<br />git rm -f <file>- f <file><br />如果把文件从暂存区域移除，但仍然希望保留在当前工作目录中，换句话说，仅是从跟踪清单中删除，使用 **--cached**选项即可<br />**git mv**<br />git mv命令用于移动或重命名一个文件，目录，软连接。

<a name="2ec512a4"></a>
## 标签管理
![image.png](https://cdn.nlark.com/yuque/0/2019/png/267458/1555317966571-6831eeab-b4ad-4f54-a2ac-709acfe996aa.png#align=left&display=inline&height=202&name=image.png&originHeight=202&originWidth=609&size=48542&status=done&width=609)<br />

<a name="5aa52869"></a>
## 分支管理
![image.png](https://cdn.nlark.com/yuque/0/2019/png/267458/1555318021172-90f45299-806b-41ba-a00d-73b309b66a7c.png#align=left&display=inline&height=220&name=image.png&originHeight=220&originWidth=595&size=26848&status=done&width=595)<br /><br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/267458/1555318035387-5de9c9ab-0e96-47f0-a762-481fa7895ad6.png#align=left&display=inline&height=402&name=image.png&originHeight=402&originWidth=648&size=133999&status=done&width=648)<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/267458/1555318052898-55cf2403-ce14-46bf-a2a9-f34aafc3f22a.png#align=left&display=inline&height=392&name=image.png&originHeight=392&originWidth=650&size=136645&status=done&width=650)<br /><br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/267458/1555318068356-09e06b38-3b2c-4122-8db9-d17b45cc2596.png#align=left&display=inline&height=240&name=image.png&originHeight=240&originWidth=645&size=75181&status=done&width=645)<br />

<a name="8954b252"></a>
# 总结：（重要）
![image.png](https://cdn.nlark.com/yuque/0/2019/png/267458/1555319128131-be336a14-3947-413f-8a2c-1a58d2e8505d.png#align=left&display=inline&height=580&name=image.png&originHeight=580&originWidth=997&size=93975&status=done&width=997)<br />
<a name="2101baf2"></a>
## 总结三种实际业务场景操作步骤：
* 本地普通项目推送至GitHub
  1. 本地搭建好项目基础框架（已存在的非Git项目，省略该步骤，直接往下执行）
  1. 执行git init 操作，初始化该项目为git项目
  1. 执行git add，git commit，将项目推送至git本地分支（默认为master）
  1. 在远程GitHub上创建的新的git仓库，用于将本地项目做关联
  1. 执行git remote add origin +远程项目地址；，将本地项目与远程仓库做关联（因实际操作习惯，一般将远程分支命名为origin）
  1. 执行git push -u origin master ,将当前所在分支代码提交至远程GitHub仓库
  1. 在GitHub上查看，本地代码已全部提交上去
* 本地已存在的Git项目，需要推送至GitHub（同上面的d-g步骤）
  1. 在远程GitHub上创建的新的git仓库，用于将本地项目做关联
  1. 执行git remote add origin +远程项目地址；，将本地项目与远程仓库做关联（因实际操作习惯，一般将远程分支命名为origin）
  1. 执行git push -u origin master ,将当前所在分支代码提交至远程GitHub仓库
  1. 在GitHub上查看，本地代码已全部提交上去
* 同步GitHub上的项目至本地
  1. 本地在合适的位置创建一个新的文件夹（建议文件夹名同项目名）
  1. 进入该文件夹执行git clone +GitHub项目地址
  1. clone命令执行完毕之后，项目会下载到当前文件夹，并且已自动做好远程关联


<a name="3b9bd62e"></a>
# 补充：git中https和SSH

1. 在git中clone项目有两种方式：HTTPS和SSH，它们的区别如下：
  * HTTPS：不管是谁，拿到url随便clone，但是在push的时候需要验证用户名和密码；
  * SSH：clone的项目你必须是拥有者或者管理员，而且需要在clone前添加SSH Key。SSH 在push的时候，是不需要输入用户名的，如果配置SSH key的时候设置了密码，则需要输入密码的，否则直接是不需要输入密码的。
1. 在git中使用SSH Key的步骤：
  * **检查电脑是否存在SSH Key**：

$ cd ~/.ssh<br />$ ls
  * 如果存在id_rsa.pub 或 id_dsa.pub 文件，说明文件以及存在，跳过创建SSH Key步骤。
  * 创建SSH Key

$ ssh-keygen -t rsa -C "your_email@example.com"
  * return后（出现如下命令）会让你输入push时的密码（不是git登录密码），一般推荐滤过，直接按enter：

Generating public/private rsa key pair.
  * 出现如下命令说明SSH Key创建成功了：

```
Your identification has been saved in /Users/shenheping/.ssh/id_rsa.
Your public key has been saved in /Users/shenheping/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:sodR52iO2z6KZOaHjElmjlGtTu8UbiZ2p+KXma4Rums shpyoucan@163.com
The key's randomart image is:
+---[RSA 2048]----+
|                 |
|                 |
|   .    . .      |
|  . .  . +       |
| .... o S .      |
|..*o . O         |
|.X+=X== o        |
|.E*%O+.+.        |
|+oo**.ooo.       |
+----[SHA256]-----+
```

  * 查看SSH Key：

# 公钥<br />$ cat ~/.ssh/id_rsa.pub

# 秘钥<br />$ cat ~/.ssh/id_rsa<br /> 
  * **添加SSH Key到GitHub上**

这里需要将公钥id_rsa.pub添加到GitHub上，登陆GitHub进入设置界面，如图所示：<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/267458/1555321224965-4eb223e8-dcc0-4430-9fbb-9c7b713083c2.png#align=left&display=inline&height=445&name=image.png&originHeight=445&originWidth=1336&size=56995&status=done&width=1336)<br />点击New SSH Key按钮后进行Key的填写操作，完成SSH Key的添加。如下图：<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/267458/1555321422386-c7a6a0b2-6b45-4d73-983e-3582e3adb32e.png#align=left&display=inline&height=453&name=image.png&originHeight=453&originWidth=1088&size=40570&status=done&width=1088)<br />

添加SSH Key成功之后，继续输入命令进行测试。<br />ssh -T git@github.com<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/267458/1555321621247-3f7e43b8-ab96-4f41-b495-8c156bde70a7.png#align=left&display=inline&height=96&name=image.png&originHeight=96&originWidth=584&size=9983&status=done&width=584)<br /><br />出现上图结果则说明添加SSH Key成功。


![image.png](https://cdn.nlark.com/yuque/0/2019/png/267458/1555321703333-9c8bbc3d-d545-47ff-931f-c220a2546efc.png#align=left&display=inline&height=367&name=image.png&originHeight=367&originWidth=1004&size=36461&status=done&width=1004)
