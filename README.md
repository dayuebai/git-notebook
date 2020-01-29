# Git 学习笔记

## 前言

我在本科毕业前有过将近两年的Git使用经验。最开始学习Git是通过阅读廖雪峰老师的教程，后来在做科研和实习时有了Git更多的使用经验。
遗憾的是一直以来并没有系统地学习Git，也没有对Git的使用经验做过整理。最近本科毕业后，我在实习中使用Git时获得些新的收获，所以想借此机会
结合廖雪峰老师的教程，对Git做一次系统梳理，也将个人使用经验添加在笔记中作为日后回顾。此笔记适合对Git有使用经验的人阅读，因为我并不会很详细地介绍Git基础知识,
而是会更多地介绍我个人对Git的使用经验和理解。推荐刚接触Git的小伙伴们详细阅读 [廖雪峰老师的Git教程](https://www.liaoxuefeng.com/wiki/896043488029600/900003767775424)。
此笔记中如有需改进或错误的地方，欢迎读者指正。目前联系方式：[dayueb26@gmail.com](dayueb26@gmail.com).

参考文档：

* [廖雪峰Git教程](https://www.liaoxuefeng.com/wiki/896043488029600/900003767775424)
* [Git官网文档](https://git-scm.com/doc)

## Git 简介

Git是一个分布式版本控制系统。

1. 什么是版本控制系统？

    就是说这个系统会将你每次提交的修改记录成为一个版本存储在系统中。每个版本会包含修改人，修改内容，修改时间等信息。使用者可以在任何时刻查看自己的修改历史或回退到任意一个版本。

2. 那什么是分布式？

    与Git这样分布式版本控制系统相对立的就是以SVN和CVS为代表的集中式版本控制系统。集中式版本控制系统通常会有一个中央服务器用来存储版本库，开发团队工作成员开始工作时需要先从版本库
    获取最新版本，再开始工作；而分布式版本控制系统可以使得每个开发人员本地环境离线存储一个完整的版本库，再通过一个中央服务器(比如Github) 推送自己本次的修改，以便其他同事更新代码。
    为了让团队各成员的代码保持同步状态，这两种版本控制系统都会部署一个中央服务器，区别在于哪里呢？
    
    * 如上所述，Git使得每个开发人员本地离线储存一个版本库，当需要推送代码时再推送到中央服务器（言外之意：可以一直在本地commit）。SVN将完整版本库信息只存储在中央服务器，
      在每次提交（commit）时都会推送本次修改到中央服务器。一旦SVN系统的中央服务器宕机，会导致团队所有人无法提交自己手上的代码。
    
    * 从使用者角度来讲，当我对一个版本库完成修改时，SVN使用者会通过`svn ci -m "commit message"`来提交这次修改，此时本次修改就会同步到中央服务器；
      Git使用者会通过`git commit -m "commit message"`提交修改，此时本次修改只是离线存储在自己本地的版本库中。使用者可再通过`git push`指令推送新增版本到中央服务器。
      
## Git vs SVN

我有过一小段SVN使用经验，个人体会Git相比SVN另一大优势就是提供良好的分支管理（成本很低）。Git使用者可以创建任意多个不同分支用来处理不同的任务：bug fix，new feature，etc. 在建立新分支时
Git只会存储diff信息，并不会为每个新分支存储整个代码库信息，这使得创建新分支成本低、速度快。SVN其实也提供了分支管理，但是使用起来就没有Git那么顺手了（个人体验）。

## 工作区 vs 暂存区 vs 版本库

1. 工作区(Working directory)：即为我们日常工作的目录。

2. 暂存区(Stage/Index)：当我们在任意一个工作目录下执行`git init`指令，我们就把当前工作目录变成了一个版本库。执行`ls -a`指令可以发现一个名为`.git`的目录，这个目录储存当前版本库的诸多信息，一旦删掉，这个目录就不再是一个版本库了。
   在版本库中，有一部分区域被命名为暂存区（stage/index), `git add`指令就可以将untracked file/modified file加入暂存区中，`git commit` 默认将暂存区中所有文件提交到版本库当前分支。
   
3. 版本库：`git init`除了在版本库中创建了一个暂存区，还创建了一个默认名为`master`的分支和一个名为`HEAD`的指针。使用一些图形可视化工具可以清楚的看到Git将提交的每一个版本穿成一条时间线，**HEAD指针始终指向着当前版本**。

## 分支管理



## 远程仓库



## Git 自定义

## 其他注意事项

1. Git这类的版本控制系统只能跟踪文本文件的改动，二进制文件虽然也可在版本控制系统中管理，但是只能追踪文件大小、文件mode等变化，并不能跟踪其内容变化。
    
2. Git可以追踪file mode 变化，例如：我们通过`chmod a+x file_name` 指令将一个文件变成可执行文件，再执行`git status`就会看到这个文件出现在 not staged change中，通过`git diff`可以发现mode发生变化。

## Git常用指令汇总&示例

0. git init
1. git add 
2. git commit
3. git log --pretty=oneline
4. git reset --hard Head
5. git reflog
6. git diff
7. git checkout --file (实际上是用版本库里的版本替代工作区中的版本，无论该文件是被修改还是删除，但前提是版本库中要存在该文件版本)
8. git reset HEAD file （将添加在暂存区的文件移动回工作区，修改状态变为unstaged, 可以再通过`git checkout -- file`指令丢弃当前修改）
9. git rm file (对比 git add)

## FAQ

    