### 版本控制工具的背景知识及初步运行 Git
# 如何保存代码历史记录？
最流行的一种叫做 RCS，RCS 的工作原理是在硬盘上保存补丁集（补丁是指文件修订前后的变化）；通过应用所有的补丁，可以重新计算出各个版本的文件内容。
# 协同合作
集中化的版本控制系统（Centralized Version Control Systems，简称 CVCS）应运而生。 
诸如 CVS、Subversion 以及 Perforce 等，都有一个单一的集中管理的服务器，保存所有文件的修订版本，而协同工作的人们都通过客户端连到这台服务器，取出最新的文件或者提交更新。
单点故障
# DVCS
分布式版本控制系统（Distributed Version Control System，简称 DVCS）面世了。 在这类系统中，像 Git、Mercurial 以及 Darcs 等，
客户端并不只提取最新版本的文件快照， 而是把代码仓库完整地镜像下来，包括完整的历史记录。

背景
大多数的 Linux 内核维护工作都花在了提交补丁和保存归档的繁琐事务上（1991－2002年间）。 到 2002 年，整个项目组开始启用一个专有的分布式版本控制系统 BitKeeper 来管理和维护代码。
2005 年，开发 BitKeeper 的商业公司同 Linux 内核开源社区的合作关系结束，他们收回了 Linux 内核社区免费使用 BitKeeper 的权力。 

- /etc/gitconfig如果在执行 git config 时带上 --system 选项，那么它就会读写该文件中的配置变量

- ~/.gitconfig 或 ~/.config/git/config 文件传递 --global 选项让 Git 读写此文件，这会对你系统上 所有 的仓库生效。

- .git/config）默认情况下用的就是它。


通过以下命令查看所有的配置[以及它们所在的文件]：
`git config --list [--show-origin]`


`git clone https://github.com/libgit2/libgit2 [自定义名]`
这会在当前目录下创建一个名为 “libgit2” 的目录，并在这个目录下初始化一个 .git 文件夹， 从远程仓库拉取下所有数据放入 .git 文件夹，然后从中读取最新版本的文件的拷贝。
初次克隆某个仓库的时候，工作目录中的所有文件都属于已跟踪文件，并处于未修改状态


![](https://git-scm.com/book/zh/v2/images/lifecycle.png)

`git status --short `
`git diff --staged`
--staged 和 --cached 是同义词

`给 git commit 加上 -a 选项，Git 就会自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 git add 步骤`

删除git仓库及磁盘文件
`$ git rm [--cached] README`
`$ git mv README.md README`

# .gitignore



git diff 修改之后还没有暂存起来的变化



---
git commit -a -m\
git status -s\
git rm\
git mv \
git diff
---


git log -<n>会列出所有的提交，最近的更新排在最上面。
列出每个提交的 **SHA-1 校验和**、**作者**的名字和电子邮件地址、**提交时间**以及**提交说明。**

git log -<n> --stat 选项在每次提交的下面列出所有被修改过的文件、有多少文件被修改了以及被修改过的文件的哪些行被移除或是添加了。 在每次提交的最后还有一个总结。


git log -<n> --patch[-p] 更加详细

--pretty 与 --graph


# git commit 手册
创建一个提交，含当前索引中的所有内容及描述，分支会更新以指向该提交









# 远程仓库的使用
与他人协作涉及管理远程仓库以及根据需要推送或拉取数据
- 如何添加远程仓库
- 移除无效的远程仓库、
- 管理不同的远程分支并定义它们是否被跟踪等等

想查看你已经配置的远程仓库服务器，可以运行 `git remote` 命令。 它会列出你指定的每一个远程服务器的简写。 \
如果你已经克隆了自己的仓库，那么至少应该能看到 origin ——这是 Git 给你克隆的仓库服务器的默认名字
添加一个自己的仓库
git remote add <shortname> <url> 添加一个新的远程 Git 仓库，同时指定一个方便使用的简写

从远程仓库中抓取与拉取使用`git fetch <remote>`
这个命令会访问远程仓库，从中拉取所有你还没有的数据。 执行完成后，你将会拥有那个远程仓库中所有分支的引用，可以随时合并或查看。

如果你使用 clone 命令克隆了一个仓库，命令会自动将其添加为远程仓库并默认以 “origin” 为简写。 所以，git fetch origin 会抓取克隆（或上一次抓取）后新推送的所有工作。 必须注意 git fetch 命令只会将数据下载到你的本地仓库——它并不会自动合并或修改你当前的工作。 当准备好时你必须手动将其合并入你的工作。


如果想要查看某一个远程仓库的更多信息，可以使用 git remote show <remote> 命令。
列出了当你在特定的分支上执行 git push 会自动地推送到哪一个远程分支。 它也同样地列出了哪些远程分支不在你的本地，哪些远程分支已经从服务器上移除了， 还有当你执行 git pull 时哪些本地分支可以与它跟踪的远程分支自动合并。


你可以运行 git remote rename 来修改一个远程仓库的简写名。 例如，想要将 pb 重命名为 paul，可以用 git remote rename 这样做：
$ git remote rename pb paul


当前分支设置了跟踪远程分支， 那么可以用 git pull 命令来自动抓取后合并该远程分支到当前分支。 默认情况下，git clone 命令会自动设置本地 master 分支跟踪克隆的远程仓库的 master 分支（或其它名字的默认分支）。 运行 git pull 通常会从最初克隆的服务器上抓取数据并自动尝试合并到当前所在的分支。


## 查看远程仓库 添加远程仓库 从远程仓库中抓取与拉取 远程仓库的重命名与移除




# Git 基础 - 打标签
列出标签
 git tag
创建标签
轻量标签（lightweight）和附注标签（annotated）。
git tag [-a]
后期打标签
git tag [-a] v1.2 9fceb02
共享标签
git push origin --tags
删除标签
本地标签可以通过 git tag -d <tagname> 删除。
删除远程标签需要使用 git push origin :refs/tags/<tagname> 或 git push origin --delete <tagname>。
检出标签：
使用 git checkout <tagname> 可以检出标签，但会进入“分离头指针”（detached HEAD）状态



# Git 基础 - Git 别名
觉得某些命令过于冗长或频繁使用，可以为它们创建别名。
git config --global alias.co checkout：将 git checkout 命令设置为 git co。













关于git log 
列出可以通过从给定提交开始沿父提交链接遍历而到达的提交，但排除那些可以通过在给定的提交前加上 ^ 来达到的提交。默认情况下，输出按时间倒序排列。
`$ git log foo bar ^baz`
列出所有可以从 foo 或 bar 到达的提交，但不包括从 baz 到达的提交


git log origin..HEAD
列出 当前分支（HEAD）中有，但远程分支（origin/main）中没有的提交。
同样功能的是git log HEAD ^origin


--follow显示该文件的完整历史，包括重命名之前的提交。
decorate附带引用名称（例如分支、标签）

--source
描述：显示每个提交所达到的引用名称。


-L<start>,<end>:<file>, -L:<funcname>:<file>可以多次使用 -L 选项


git log commit1..commit2列出从 commit1 到 commit2 之间的所有提交


-- path/to/file1 path/to/file2














提供了许多选项来限制显示的提交数量或过滤特定的提交
-<number>, -n <number>
--skip=<number>


--since=<date>, --after=<date>
--until=<date>, --before=<date>


--[no-]merges

--tags[=<pattern>]
git log --tags="v1.*"


--remotes[=<pattern>]
git log --remotes="origin/*"


显示两个分支 A 和 B 之间的差异
--cherry-mark  --cherry-pick--left-only, --right-only
--cherry 是 --right-only --cherry-mark --no-merges 的简写


--pretty=<format> 或 --format=<format>：此选项允许你指定一个自定义格式来显示提交日志。
--parents
功能：打印提交的父提交（以“commit parent...”的形式）。启用此选项后，父提交将被显示，帮助你理解该提交的来源。
应用场景：适用于你想要看到提交的父级关系或在分析某个提交时，需要查看它的直接父提交。
2. --children
功能：打印提交的子提交（以“commit child...”的形式）。启用此选项后，提交的所有子提交也会显示出来。
应用场景：用于查看某个提交的所有后续提交，帮助理解分支和合并的历史。
占位符说明：

%h：简短的提交哈希。


有时候我们提交完了才发现漏掉了几个文件没有添加，或者提交信息写错了。 此时，可以运行带有 --amend 选项的提交命令来重新提交：`git commit --amend`
例如，你提交后发现忘记了暂存某些需要的修改，可以像下面这样操作：
```
$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend
```
最终你只会有一个提交——第二次提交将代替第一次提交的结果。

 例如，你已经修改了两个文件并且想要将它们作为两次独立的修改提交， 但是却意外地输入 git add * 暂存了它们两个。如何只取消暂存两个中的一个呢？
git status 命令提示了你
`git reset HEAD <file>…​ 来取消暂存。`


如果你并不想保留对 CONTRIBUTING.md 文件的修改怎么办？ 如何方便地撤消修改——将它还原成某个提交的样子
git status 也告诉了你应该如何做。
`(use "git checkout -- <file>..." to discard changes in working directory)`


















