# Darling
[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/wanqiu2004/Darling)


可以使用Markdown语法编写README及pr issues
个人资料 README 让您能够与 GitHub 社区分享有关自己的信息。该 README 会显示在您个人资料页面的顶部。
如果没有个人的README.md可以
创建一个与用户名相同名称的仓库，并在初始化仓库时添加一个 README.md 文件。
要再次修改点击个人资料照片，然后点击 Your profile

要生成表格可以这样：
| Rank | Languages |
|-----:|-----------|
|     1| JavaScript|
|     2| Python    |
|     3| SQL       |

创建一个可展开的折叠部分：
添加open属性默认展开
<details>
  <summary>My top languages</summary>

  | Rank | Languages |
  |-----:|-----------|
  |     1| JavaScript|
  |     2| Python    |
  |     3| SQL       |

</details>
<details open>
  <summary>My top languages</summary>

  | Rank | Languages |
  |-----:|-----------|
  |     1| JavaScript|
  |     2| Python    |
  |     3| SQL       |

</details>


---
> If we pull together and commit ourselves, then we can push through anything.

— Mona the Octocat

可以添加HTML同款的注释
<!-- TO DO: add more details about me later -->

GitHub 上的每个评论区都包含一个文本格式工具栏，

在 GitHub 上任意页面的右上角，单击您的个人资料照片，然后单击“设置”。
在左侧边栏中，单击外观。
在“Markdown 编辑器字体首选项”下，选择编辑 Markdown 时使用等宽（等宽）字体。


使用两个或更多标题时，GitHub 会自动生成一个目录，在左上角

Ctrl+ I Ctrl + B

左边~~ 右边 ~~表示删除线

\<ins>是下划线
\<sub>下标
\<sup>上标


CTRL E 是代码段

三重\`是代码段
`git status
git add
git commit
`


Command+K来创建链接

自定义
\<a name="my-custom-anchor-point"></a>
CTRL K的url部分填#my-custom-anchor-poin

\![](https://myoctocat.com/assets/images/base-octocat.svg)
CTRL K 在最前面添加!然后填图片的url可以查看图片

在一行或多行文本前加上-创建无序列表
\1. 创建有序列表

\1. First list item
\   - asdfsadfsadfasdf
\     - sadfsadfsadf


- [x] #739
- [x] https://github.com/octo-org/octo-repo/issues/740
- [ ] Add delight to the experience when all tasks are complete :tada:

\- [ ] asdfasdf   任务列表


输入后:在输入一些字符会显示建议的表情符号列表。

\> [!NOTE]
\> Useful information that users should know, even when skimming content.
> [!NOTE]
> Useful information that users should know, even when skimming content.

