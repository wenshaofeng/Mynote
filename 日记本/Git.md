

## 术语

## 版本控制系统 / 源代码管理器

**版本控制系统**（简称 **VCS**）是一个管理源代码不同版本的工具。**源代码管理器**（简称 **SCM**）是版本控制系统的另一个名称。

Git 是一个 SCM（因此也是 VCS！）。Git 网站的 URL 是 [https://git-scm.com/](https://git-scm.com/) （注意它的域名中直接包含“SCM”！）。

## 提交（Commit）

Git 将数据看做微型文件系统的一组快照。每次 **commit**（在 Git 中保持项目状态），它都对文件当时的状况拍照，并存储对该快照的引用。你可以将其看做游戏中的保存点，它会保存项目的文件和关于文件的所有信息。

你在 Git 中的所有操作都是帮助你进行 commit，因此 commit 是 Git 中的基本单位。

## 仓库（Repository / repo）

**仓库**是一个包含项目内容以及几个文件（在 Mac OS X 上默认地处于隐藏状态）的目录，用来与 Git 进行通信。仓库可以存储在本地，或作为远程副本存储在其他计算机上。仓库是由 commit 构成的。

## 工作目录 / 工作区（Working Directory）

**工作目录**是你在计算机的文件系统中看到的文件。当你在代码编辑器中打开项目文件时，你是在工作目录中处理文件。

与这些文件形成对比的是保持在仓库中（在 commit 中！）的文件。

在使用 Git 时，工作目录与命令行工具的 *current working directory* （当前工作目录）不一样，后者是 shell 当前正在查看的目录。

## 检出（Checkout）

**检出**是指将仓库中的内容复制到工作目录下。

## 暂存区 / 暂存索引 / 索引（Staging Area / Staging Index / Index）

Git 目录下的一个文件，存储的是即将进入下个 commit 内容的信息。可以将**暂存区**看做准备工作台，Git 将在此区域获取下个 commit。暂存索引中的文件是准备添加到仓库中的文件。

## SHA

**SHA** 是每个 commit 的 ID 编号。以下是 commit 的 SHA 示例：`e2adf8ae3e2e4ed40add75cc44cf9d0a869afeb6`。

它是一个长 40 个字符的字符串（由 0–9 和 a–f 组成），并根据 Git 中的文件或目录结构的内容计算得出。SHA 的全称是"Secure Hash Algorithm"（安全哈希算法）。如果你想了解哈希算法，请参阅我们的[计算机科学入门课程](https://www.udacity.com/course/intro-to-computer-science--cs101)。

## 分支（Branch）

**分支**是从主开发流程中分支出来的新的开发流程。这种分支开发流程可以在不更改主流程的情况下继续延伸下去。

回到之前关于游戏保存点的示例，你可以将分支看做在游戏中设立保存点后，尝试一个有风险的招式。如果有风险的招式不奏效，则回到保存的位置。令分支非常强大的关键之处是你可以在一个分支上设定保存点，然后切换到另一个分支并继续设定保存点。



#####初始化一个Git仓库，使用git init命令。

添加文件到Git仓库，分两步：

* 使用命令git add <file>，注意，可反复多次使用，添加多个文件；
* 使用命令git commit -m <message>，完成。

* 要随时掌握工作区的状态，使用git status命令。

* 如果git status告诉你有文件被修改过，用git diff可以查看修改内容。
###git log 小结


我们快速总结下 git log 命令。git log 命令用于显示仓库中所有 commit 的信息。

$ git log
默认情况下，该命令会显示仓库中每个 commit 的：

SHA 作者 日期  消息

我强调了“默认情况下”是因为 git log 命令显示的信息远不止这些。

git 使用命令行分页器 less 浏览所有信息。以下是 less 的重要快捷键：

要按行向下滚动，使用 j 或 ↓

要按行向上滚动，使用 k 或 ↑

要按页向下滚动，使用空格键或 Page Down 按钮

要按页向下滚动，使用 b 或 Page Up 按钮

要退出，使用 q
git log --pretty=oneline 参数 


####$ git log --stat
此命令会：

- 显示被修改的文件

- 显示添加/删除的行数

- 显示一个摘要，其中包含修改/删除的总文件数和总行数


####$ git log -p
git log -p 小节
总结下，-p 选项（和 --patch 选项一样）用来更改 git log 显示信息的方式：

此命令会向默认输出中添加以下信息：

显示被修改的文件

显示添加/删除的行所在的位置

显示做出的实际更改

###查找改变
git log 
git show 
git log --stat(摘要) 、git log -p（实际更改） 、 git log --oneline（缩写） 

####git add 命令用于将文件从工作目录移到暂存区。

$ git add <file1> <file2> … <fileN>
此命令：

可接受多个文件名（用空格分隔）

此外，可以使用句点 . 来代替文件列表，告诉 git 添加当前目录至暂存区（以及所有嵌套文件）


####git commit 小结
git commit 命令会取出暂存区的文件并保存到仓库中。

$ git commit
此命令：

将打开配置中指定的代码编辑器

（请参阅第一节课中的 git 配置流程，了解如何配置编辑器）

在代码编辑器中：

必须提供提交说明

以 # 开头的行是注释，将不会被记录

添加提交说明后保存文件

关闭编辑器以进行提交

然后使用 git log 检查你刚刚提交的 commit



###$ git diff
  用来查看已经执行但是尚未 commit 的更改：

此命令会显示：

- 已经修改的文件
- 添加/删除的行所在的位置
- 执行的实际更改

###git branch 小结
总结下，git branch 命令用来管理 git 中的分支：

```
# 列出所有分支

$ git branch


# 创建新的"footer-fix"分支

$ git branch footer-fix


# 删除"footer-fix"分支

$ git branch -d footer-fix

      注意，无法删除当前所在的分支。因此要删除 sidebar 分支，你需要切换
              到 master 分支，或者创建并切换到新的分支。


 删除内容让人比较紧张。但是不用担心。如果某个分支上有任何其他分支
上都没有包含的 commit（也就是这个 commit 是要被删除的分支独有
 的），git 不会删除该分支。如果你创建了 sidebar 分支，向其添加了 
commit，然后尝试使用 git branch -d sidebar 删除该分支，git 不会让你删
除该分支，因为你无法删除当前所在的分支。如果你切换到 master 分支
并尝试删除 sidebar 分支，git 也不会让你删除，因为 sidebar 分支上的新 
commit 会丢失！要强制删除，你需要使用大写的 D 选项 - git branch -D sidebar。
```

##GitHub
#####[Git"Could not read from remote repository.Please make sure you have the correct access rights."解决方案](https://blog.csdn.net/u014702999/article/details/72783140)

##踩过的坑

- 问题:当在码云上修改了Readme文件而忘记pull到本地时，
本地提交会报错
![错误日志](https://upload-images.jianshu.io/upload_images/9249356-23f54aa158b31cdf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
解决方案
![image.png](https://upload-images.jianshu.io/upload_images/9249356-f15f879fe767f4a6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://img-blog.csdn.net/20160813000020921)
