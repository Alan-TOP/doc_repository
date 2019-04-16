# Git&amp;Gitflow&amp;Sourcetree基础

<a name="922a3ca0"></a>
# Git主要优点
  1. 分布式存储 , 本地仓库包含了远程仓库的所有内容 . 安全性高 , 远程仓库文件丢失了也不怕
  1. 优秀的分支模型 , 创建/合并分支非常的方便
  1. 方便快速 , 由于代码本地都有存储 , 所以从远程拉取和分支合并时都非常快捷
<a name="5c5f6d3d"></a>
# git 团队协作的一些命令
* **1.开分支**
```
git branch 新分支名
例如，在master分支下，新开一个开发分支：
git branch dev
```
* **2.切换到新分支**
```
git checkout 分支名
例如，在master分支下，切换到新开的dev：
git checkout dev
```
* **3.开分支和切换分支合并到一个命令**
```
git checkout -b 新分支名
例如，新开一个开发分支，并立即切换到该分支：
git checkout -b dev
```
* **4.切换回原分支**
```
git checkout 原分支名
例如，切换回master
git checkout master
注意：当前分支有修改，还未commit的时候，会切换失败，应当先commit，但可以不用push
```
* **5.合并分支**
```
git merge 需要合并的分支名
例如，刚刚已经切换回master，现在需要合并dev的内容：
git merge dev
建议在GitLab(或者其他git系统)上面创建merge request的形式来进行分支的合并和代码审核。
```
* **6.查看本地分支列表**
```
git branch -a
前面带remotes/origin 的，是远程分支
```
* **7.查看远程分支列表**
```
git branch -r
```
* **8.向远程提交本地新开的分支**
```
git push origin 新分支名
例如，刚刚在master下新开的dev分支：
git push origin dev
```
* **9.删除远程分支**
```
git push origin :远程分支名
例如，删除刚刚提交到远程的dev分支：
git push origin :dev
```
* **10.删除本地分支**
```
git branch 分支名称 -d
例如，在master分支下，删除新开的dev分支：
git branch dev -d
注意：如果dev的更改，push到远程，在GitLab(或者其他git系统)上面进行了merge操作，但是本地master没有pull最新的代码，会删除不成功，可以先git pull origin master，或者强制删除
git branch dev -D
```
* **11.更新分支列表信息**
```
git fetch -p
```
* **12.TortoiseGit(乌龟git)**
```
不可否认，在windows下，这个是个不错的工具。不管你是命令行新手还是重度使用者，我觉得都可以尝试一下。
```

**当分支过多时 , 如何管理这些分支呢 ? 我们团队采用了Git Flow的模式**
<a name="fb48d630"></a>
# GitFlow的常用分支
<a name="master"></a>
## master
主分支 , 产品的功能全部实现后 , 最终在master分支对外发布<br />该分支为只读唯一分支 , 只能从其他分支(release/hotfix)合并 , 不能在此分支修改<br />另外所有在master分支的推送应该打标签做记录,方便追溯<br />例如release合并到master , 或hotfix合并到master
<a name="develop"></a>
## develop
主开发分支 , 基于master分支克隆<br />包含所有要发布到下一个release的代码<br />该分支为只读唯一分支 , 只能从其他分支合并<br />feature功能分支完成 , 合并到develop(不推送)<br />develop拉取release分支 , 提测<br />release/hotfix 分支上线完毕 , 合并到develop并推送
<a name="feature"></a>
## feature
功能开发分支 , 基于develop分支克隆 , 主要用于新需求新功能的开发<br />功能开发完毕后合到develop分支(未正式上线之前不推送到远程中央仓库!!!)<br />feature分支可同时存在多个 , 用于团队中多个功能同时开发 , 属于临时分支 , 功能完成后可选删除
<a name="release"></a>
## release
测试分支 , 基于feature分支合并到develop之后  , 从develop分支克隆<br />主要用于提交给测试人员进行功能测试 , 测试过程中发现的BUG在本分支进行修复 , 修复完成上线后合并到develop/master分支并推送(完成功能) , 打Tag<br />属于临时分支 , 功能上线后可选删除
<a name="hotfix"></a>
## hotfix
补丁分支 , 基于master分支克隆 , 主要用于对线上的版本进行BUG修复<br />修复完毕后合并到develop/master分支并推送 , 打Tag<br />属于临时分支 , 补丁修复上线后可选删除<br />所有hotfix分支的修改会进入到下一个release
<a name="6b11fc55"></a>
## 主要工作流程
1 . 初始化项目为gitflow , 默认创建master分支 , 然后从master拉取第一个develop分支<br />2 . 从develop拉取feature分支进行编码开发(多个开发人员拉取多个feature同时进行并行开发 , 互不影响)<br />3 . feature分支完成后 , 合并到develop(不推送 , feature功能完成还未提测 , 推送后会影响其他功能分支的开发)<br />   合并feature到develop , 可以选择删除当前feature , 也可以不删除 . 但当前feature就不可更改了 , 必须从release分支继续编码修改<br />4 . 从develop拉取release分支进行提测 , 提测过程中在release分支上修改BUG<br />5 . release分支上线后 , 合并release分支到develop/master并推送<br />    合并之后 , 可选删除当前release分支 , 若不删除 , 则当前release不可修改 . 线上有问题也必须从master拉取hotfix分支进行修改<br />6 . 上线之后若发现线上BUG , 从master拉取hotfix进行BUG修改<br />7 . hotfix通过测试上线后 , 合并hotfix分支到develop/master并推送<br />   合并之后 , 可选删除当前hostfix , 若不删除 , 则当前hotfix不可修改 , 若补丁未修复 , 需要从master拉取新的hotfix继续修改<br />8 . 当进行一个feature时 , 若develop分支有变动 , 如其他开发人员完成功能并上线 , 则需要将完成的功能合并到自己分支上<br />   即合并develop到当前feature分支<br />9 . 当进行一个release分支时 , 若develop分支有变动 , 如其他开发人员完成功能并上线 , 则需要将完成的功能合并到自己分支上<br />   即合并develop到当前release分支 (!!! 因为当前release分支通过测试后会发布到线上 , 如果不合并最新的develop分支 , 就会发生丢代码的情况)<br />引自大神的Git Flow 工作流程图<br />![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555060914466-ef2508e4-55b2-40aa-aef4-dc3b97add942.png#align=left&display=inline&height=395&originHeight=395&originWidth=643&size=0&status=done&width=643)<br /> 不喜欢命令行的同学 , 这里有完美支持Git Flow的图形化工具 - SourceTree(支持中文简体)<br /> ![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555060923784-b320ff44-d6a2-4028-9227-6d98436703c1.png#align=left&display=inline&height=393&originHeight=393&originWidth=623&size=0&status=done&width=623)

<a name="069290d3"></a>
# Git工作流指南：Gitflow工作流
在你开始阅读之前，请记住：流程应被视作为指导方针，而非“铁律”。我们只是想告诉你可能的做法。因此，如果有必要的话，你可以组合使用不同的流程<br />![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555059799628-b9e0b412-d19e-4e43-9b2e-2037ed84cff0.png#align=left&display=inline&height=348&originHeight=348&originWidth=614&size=0&status=done&width=614)<br />Gitflow工作流定义了一个围绕项目发布的严格分支模型。虽然比功能分支工作流复杂几分，但提供了用于一个健壮的用于管理大型项目的框架。<br />Gitflow工作流没有用超出功能分支工作流的概念和命令，而是为不同的分支分配一个很明确的角色，并定义分支之间如何和什么时候进行交互。除了使用功能分支，在做准备、维护和记录发布也使用各自的分支。当然你可以用上功能分支工作流所有的好处：Pull Requests、隔离实验性开发和更高效的协作。
<a name="3233fd77"></a>
### 工作方式
Gitflow工作流仍然用中央仓库作为所有开发者的交互中心。和其它的工作流一样，开发者在本地工作并push分支到要中央仓库中。
<a name="79d1312d"></a>
### 历史分支
相对使用仅有的一个master分支，Gitflow工作流使用2个分支来记录项目的历史。master分支存储了正式发布的历史，而develop分支作为功能的集成分支。这样也方便master分支上的所有提交分配一个版本号。<br />![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555059799731-24427c89-7c6e-4e7d-8ab9-032f936b1bda.png#align=left&display=inline&height=148&originHeight=148&originWidth=614&size=0&status=done&width=614)<br />剩下要说明的问题围绕着这2个分支的区别展开。
<a name="4376dec7"></a>
### 功能分支
每个新功能位于一个自己的分支，这样可以push到中央仓库以备份和协作。但功能分支不是从master分支上拉出新分支，而是使用develop分支作为父分支。当新功能完成时，合并回develop分支。新功能提交应该从不直接与master分支交互。<br />![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555059799612-eea732a7-f709-4410-a951-b5b20e39eb6d.png#align=left&display=inline&height=268&originHeight=268&originWidth=614&size=0&status=done&width=614)
> 注意，从各种含义和目的上来看，功能分支加上develop分支就是功能分支工作流的用法。但Gitflow工作流没有在这里止步。

<a name="875d8f44"></a>
### 发布分支
![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555059799622-b726c996-28f7-4728-b0f7-45dda1ca3559.png#align=left&display=inline&height=320&originHeight=320&originWidth=614&size=0&status=done&width=614)<br />一旦develop分支上有了做一次发布（或者说快到了既定的发布日）的足够功能，就从develop分支上fork一个发布分支。新建的分支用于开始发布循环，所以从这个时间点开始之后新的功能不能再加到这个分支上 —— 这个分支只应该做Bug修复、文档生成和其它面向发布任务。一旦对外发布的工作都完成了，发布分支合并到master分支并分配一个版本号打好Tag。另外，这些从新建发布分支以来的做的修改要合并回develop分支。<br />使用一个用于发布准备的专门分支，使得一个团队可以在完善当前的发布版本的同时，另一个团队可以继续开发下个版本的功能。<br />这也打造定义良好的开发阶段（比如，可以很轻松地说，『这周我们要做准备发布版本4.0』，并且在仓库的目录结构中可以实际看到）。
<a name="80efeccf"></a>
### 常用的分支约定：
> 用于新建发布分支的分支: develop
> 用于合并的分支: master
> 分支命名: release-* 或 release/*

<a name="bf57b65d"></a>
### 维护分支
![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555059799633-8cf084b6-f0d3-430b-9655-103e955d63b0.png#align=left&display=inline&height=380&originHeight=380&originWidth=614&size=0&status=done&width=614)<br />维护分支或说是热修复（hotfix）分支用于生成快速给产品发布版本（production releases）打补丁，这是唯一可以直接从master分支fork出来的分支。修复完成，修改应该马上合并回master分支和develop分支（当前的发布分支），master分支应该用新的版本号打好Tag。<br />为Bug修复使用专门分支，让团队可以处理掉问题而不用打断其它工作或是等待下一个发布循环。你可以把维护分支想成是一个直接在master分支上处理的临时发布。
<a name="1a63ac23"></a>
### 示例
下面的示例演示本工作流如何用于管理单个发布循环。假设你已经创建了一个中央仓库。
<a name="e3ac34da"></a>
#### _创建开发分支_
![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555059799658-0156c458-87f7-4131-bde2-5527e34030b0.png#align=left&display=inline&height=146&originHeight=146&originWidth=236&size=0&status=done&width=236)<br />第一步为master分支配套一个develop分支。简单来做可以本地创建一个空的develop分支，push到服务器上：
```
git branch develop
git push -u origin develop
```
以后这个分支将会包含了项目的全部历史，而master分支将只包含了部分历史。其它开发者这时应该克隆中央仓库，建好develop分支的跟踪分支：
```
git clone ssh://user@host/path/to/repo.git
git checkout -b develop origin/develop
```
现在每个开发都有了这些历史分支的本地拷贝。
<a name="1362197a"></a>
#### _工程师A和工程师B开始开发新功能_
![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555059799738-2f75a6f3-8704-4597-9092-e0d60452d209.png#align=left&display=inline&height=234&originHeight=234&originWidth=236&size=0&status=done&width=236)<br />这个示例中，工程师A和工程师B开始各自的功能开发。他们需要为各自的功能创建相应的分支。新分支不是基于master分支，而是应该基于develop分支：
```
git checkout -b some-feature develop
```
他们用老套路添加提交到各自功能分支上：编辑、暂存、提交：
```
git status
git add
git commit
```
<a name="7f02f6f5"></a>
#### _工程师A完成功能开发_
![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555059799670-a93da2d2-7776-47d3-8d84-eee40528f1e2.png#align=left&display=inline&height=104&originHeight=104&originWidth=236&size=0&status=done&width=236)<br />添加了提交后，工程师A觉得她的功能OK了。如果团队使用Pull Requests，这时候可以发起一个用于合并到develop分支。否则她可以直接合并到她本地的develop分支后push到中央仓库：
```
git pull origin develop
git checkout develop
git merge some-feature
git push
git branch -d some-feature
```
第一条命令在合并功能前确保develop分支是最新的。注意，功能决不应该直接合并到master分支。冲突解决方法和集中式工作流一样。
<a name="3134579b"></a>
#### _工程师A开始准备发布_
![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555059799638-691341cd-1e02-4974-af83-6cacc784730b.png#align=left&display=inline&height=144&originHeight=144&originWidth=236&size=0&status=done&width=236)<br />这个时候工程师B正在实现他的功能，工程师A开始准备她的第一个项目正式发布。像功能开发一样，她用一个新的分支来做发布准备。这一步也确定了发布的版本号：
```
git checkout -b release-0.1 develop
```
这个分支是清理发布、执行所有测试、更新文档和其它为下个发布做准备操作的地方，像是一个专门用于改善发布的功能分支。<br />只要工程师A创建这个分支并push到中央仓库，这个发布就是功能冻结的。任何不在develop分支中的新功能都推到下个发布循环中。
<a name="247b03c1"></a>
#### _工程师A完成发布_
![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555059799657-5a66cfa2-0fd9-4685-abca-4304aebc473d.png#align=left&display=inline&height=235&originHeight=235&originWidth=236&size=0&status=done&width=236)<br />一旦准备好了对外发布，工程师A合并修改到master分支和develop分支上，删除发布分支。合并回develop分支很重要，因为在发布分支中已经提交的更新需要在后面的新功能中也要是可用的。另外，如果工程师A的团队要求Code Review，这是一个发起Pull Request的理想时机。
```
git checkout master
git merge release-0.1
git push
git checkout develop
git merge release-0.1
git push
git branch -d release-0.1
```
发布分支是作为功能开发（develop分支）和对外发布（master分支）间的缓冲。只要有合并到master分支，就应该打好Tag以方便跟踪。
```
git tag -a 0.1 -m "Initial public release" master
git push --tags
```
Git有提供各种勾子（hook），即仓库有事件发生时触发执行的脚本。可以配置一个勾子，在你push中央仓库的master分支时，自动构建好对外发布。
<a name="fbd37e62"></a>
#### _最终用户发现Bug_
![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555059799673-52e93022-f65d-479a-abf8-77de2437a5ed.png#align=left&display=inline&height=125&originHeight=125&originWidth=236&size=0&status=done&width=236)<br />对外发布后，工程师A回去和工程师B一起做下个发布的新功能开发，直到有最终用户开了一个Ticket抱怨当前版本的一个Bug。为了处理Bug，工程师A（或工程师B）从master分支上拉出了一个维护分支，提交修改以解决问题，然后直接合并回master分支：
```
git checkout -b issue-#001 master
```
Fix the bug
```
git checkout master
git merge issue-#001
git push
```
就像发布分支，维护分支中新加这些重要修改需要包含到develop分支中，所以工程师A要执行一个合并操作。然后就可以安全地删除这个分支了：
```
git checkout develop
git merge issue-#001
git push
git branch -d issue-#001
```

Git是一个不错的版本管理工具，但也仅仅是工具。记住，这里演示的工作流只是可能用法的例子，而不是在实际工作中使用Git不可违逆的条例。所以不要畏惧按自己需要对工作流的用法做取舍。不变的目标就是让Git为你所用。

<a name="29e678ea"></a>
# SourceTree下GitFlow的使用
<a name="7512d8ee"></a>
## 1.准备工作
  sourceTree的下载安装，git中项目的创建，自行百度
<a name="b3f4ce0d"></a>
## 2.Git Flow的流程图
![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555061581285-e12d1028-19ff-4cfa-b53b-1de68895622f.png#align=left&display=inline&height=815&originHeight=815&originWidth=611&size=0&status=done&width=611)
<a name="2734037e"></a>
## 3.初始化
   首先，下载工程，点击“clone”，输入git工程地址,点击“克隆”，这里我将工程下载到C盘自己的工作空间里<br />   ![](https://cdn.nlark.com/yuque/0/2019/jpeg/267458/1555061595166-551685f7-aa5b-4778-b470-cf5a14291c2d.jpeg#align=left&display=inline&height=484&originHeight=1218&originWidth=1876&size=0&status=done&width=746)<br />下载完成，点击”Git工作流”，弹出框点击“确定”，项目代码库里自动增加了一个develop的分支。画面中看到，还有三类分支的命名规则：feature、release、hotfix，这就是未来承接具体开发工作的分支类型<br />![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555061611791-ca13cb35-97c0-4c9a-8227-f07dffb38780.png#align=left&display=inline&height=479&originHeight=1382&originWidth=2151&size=0&status=done&width=746)<br />将新创建的develop分支推送到远端仓库，点击‘推送’，弹出框里勾选新创建的develope分支并点击“推送”按钮<br />![](https://cdn.nlark.com/yuque/0/2019/jpeg/267458/1555061628783-85db58bd-ee3a-4697-8518-36d21cbc72fc.jpeg#align=left&display=inline&height=479&originHeight=1513&originWidth=2355&size=0&status=done&width=746)<br />然后我们会在git上看到这两个分支。这就是我们未来所有开发围绕的两个分支：master和develop。source Tree把git命令用具体的功能实现了，减少人为失误<br />![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555061640726-2eaaf3c2-7230-4aa5-9258-ece4bdb68616.png#align=left&display=inline&height=334&originHeight=806&originWidth=867&size=0&status=done&width=359)
<a name="f72fc670"></a>
## 4.创建分支
<a name="4.1hotfix"></a>
### 4.1hotfix
bug修复分支，用于解决生产环境发现的bug<br />派生于master;合并于master、develop<br />点击“git工作流”-“建立新的修复补丁”<br />![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555061659528-207b31f0-1740-487a-975c-53f76e0e74ba.png#align=left&display=inline&height=479&originHeight=1357&originWidth=2113&status=done&width=746)<br />输入“修复补丁名称”，点击“确定”<br />![](https://cdn.nlark.com/yuque/0/2019/jpeg/267458/1555061674888-524cea2f-ef59-4ddf-86a4-3fe9491f18ec.jpeg#align=left&display=inline&height=257&originHeight=1187&originWidth=2377&size=0&status=done&width=515)

打hotfix分支完毕<br />![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555061716621-9c39d997-8536-41cf-9e1b-484b2ee9cb4a.png#align=left&display=inline&height=322&originHeight=1361&originWidth=1676&size=0&status=done&width=396)<br />开发工作完成后，hotfix分支会同时合并到master与develope。点击“git工作流”，选择“完成修复补丁”<br />![](https://cdn.nlark.com/yuque/0/2019/jpeg/267458/1555061731551-697e85cc-1458-450a-a674-8f014031ac9d.jpeg#align=left&display=inline&height=561&originHeight=1483&originWidth=1972&size=0&status=done&width=746)<br />输入信息标签，可选择“删除分支”。不建议选择“推送变更到远程仓库”，合并分支后自测一遍再推送，养成百密不疏的好习惯<br />![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555061742056-36e99226-9068-413a-805f-5cd6697840b6.png#align=left&display=inline&height=367&originHeight=1453&originWidth=2152&size=0&status=done&width=544)<br />分支合并完毕，master和develope验证无误后，再推送到远程仓库。<br />![](https://cdn.nlark.com/yuque/0/2019/jpeg/267458/1555061757090-371954db-41bb-4f69-9358-964b34a2307f.jpeg#align=left&display=inline&height=421&originHeight=1002&originWidth=1501&size=0&status=done&width=631)
<a name="79d35b53"></a>
### 4.2 feature
功能开发分支，用于承接具体功能需求的开发<br />派生、合并都在develop分支<br /> 点击“git工作流”-“建立新的功能”<br />![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555061801511-60d65cd0-40dd-40a6-b6e8-4ec60411238b.png#align=left&display=inline&height=383&originHeight=1281&originWidth=2496&size=0&status=done&width=746)<br />输入功能名称后，点击“确定”<br />![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555061813054-ee872495-c816-4707-b05f-490083213f5e.png#align=left&display=inline&height=240&originHeight=677&originWidth=1380&size=0&status=done&width=489)<br />可以在目录中看到新分支<br />![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555061825071-560fd432-07d9-4f5c-b1ed-52e97904aa02.png#align=left&display=inline&height=357&originHeight=947&originWidth=857&size=0&status=done&width=323)<br />开发工作完成后，“git工作流”--“完成功能”<br />![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555061845349-705278ae-b51a-4a9d-ba2b-de37b4087aea.png#align=left&display=inline&height=432&originHeight=1445&originWidth=2496&size=0&status=done&width=746)<br />可选“删除分支”，点击“确定”。这里没有“推送变更到远程仓库”的选项，不知道为啥。觉得刚刚好方便再自测一下<br />![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555061855356-739aa35c-de58-404d-bce8-0ebee87c3c42.png#align=left&display=inline&height=303&originHeight=788&originWidth=1262&size=0&status=done&width=485)<br />可以看到feature分支已经被删除，并且已合并到develope分支，master分支保持原样。检查无误后就可以推送到远程仓库提测了。<br />![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555061865952-9a5baf99-99ad-427c-963c-c9577847312d.png#align=left&display=inline&height=349&originHeight=687&originWidth=847&size=0&status=done&width=430)
<a name="e4d78664"></a>
### 4.3 release
版本发布分支，用于完成发布准备的<br />派生于develop<br />合并于master、develop<br />当一个或多个需求开发完毕，由feature分支合并到develope后，可以提测后，就要创建release分支了。“git工作流”--“建立新的发布版本”<br />![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555061884261-88393320-ca77-46e7-a1fe-f818bc3755a6.png#align=left&display=inline&height=415&originHeight=1430&originWidth=2571&size=0&status=done&width=746)<br />按照命名规则输入发布版本名，点击“确定”<br />![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555061894048-f06deab8-7c28-4f83-87de-30290f2f94be.png#align=left&display=inline&height=229&originHeight=677&originWidth=1387&size=0&status=done&width=469)<br />这时可以看到分支创建完毕：<br />![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555061905549-2f4a7250-65fd-4ae2-9746-2045edfbeb73.png#align=left&display=inline&height=346&originHeight=904&originWidth=941&size=0&status=done&width=360)<br />测试结束，bug修改完毕时，将release分支合并到develope和master分支，选中分支--“git工作流”--“完成发布版本”<br />![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555061928002-d9c0e86c-70c1-4551-9bfc-a95034a78f8d.png#align=left&display=inline&height=415&originHeight=1430&originWidth=2571&size=0&status=done&width=746)<br />可选“删除分支”输入标签后，点击“确定”，此时不建议选“推送变更到远程仓库”，每次代码变更尽量都在本机自测<br />![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555061940629-f26824cb-0312-437a-be0d-ab224b71d4b4.png#align=left&display=inline&height=357&originHeight=906&originWidth=1259&size=0&status=done&width=496)<br />验证无误后，就可以推送到远程仓库了。<br />![](https://cdn.nlark.com/yuque/0/2019/png/267458/1555061952605-1ba47941-a25b-4b66-8504-5dc0e256f8e5.png#align=left&display=inline&height=385&originHeight=867&originWidth=941&size=0&status=done&width=418)<br />总结<br />**远程仓库仅仅应该存在两个分支，一个是master分支，存放线上（生产环境）版本，这个分支的代码总是可靠可用的；另一个是develop分支，这个分支用于日常需求开发**<br />master分支上的内容不应直接提交，应该由develop分支发布到release分支，经过QA测试确认可以上线后，再完成发布新版本功能然后合并入master分支；或者由hotfix分支修复完补丁合并上去<br />develop分支下允许有多个feature分支，并不会冲突；允许在仍然有feature在开发的情况下从develop分支拉取到release分支。




参考资料：<br />[https://www.cnblogs.com/myqianlan/p/4195994.html](https://www.cnblogs.com/myqianlan/p/4195994.html)    Git基本命令和GitFlow工作流<br />[https://blog.csdn.net/xingbaozhen1210/article/details/81386269](https://blog.csdn.net/xingbaozhen1210/article/details/81386269)    GitFlow详解教程<br />[https://blog.csdn.net/u011260970/article/details/79917462](https://blog.csdn.net/u011260970/article/details/79917462)    SourceTree下GitFlow的使用<br />[](https://www.cnblogs.com/iBrand2018/p/8708740.html)[https://www.cnblogs.com/iBrand2018/p/8708740.html](https://www.cnblogs.com/iBrand2018/p/8708740.html)    [SourceTree 实现 git flow 流程](https://www.cnblogs.com/iBrand2018/p/8708740.html)<br /><br /><br /><br /><br />推荐资料：<br />[https://github.com/xirong/my-git/blob/master/git-workflow-tutorial.md#23-gitflow工作流](https://github.com/xirong/my-git/blob/master/git-workflow-tutorial.md#23-gitflow%E5%B7%A5%E4%BD%9C%E6%B5%81)<br />[https://www.jianshu.com/p/3381d6fe74d4](https://www.jianshu.com/p/3381d6fe74d4)    gitflow的使用



