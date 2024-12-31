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
