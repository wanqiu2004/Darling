### 前言
通过使用Bash Shell的高级功能、Shell脚本和各种Red Hat Enterprise Linux工具，
提高工作的效率。


创建并执行Bash Shell脚本： 许多简单的系统管理任务可以通过命令行工具完成。
对于更复杂的任务，通常需要将多个命令串联在一起，使它们能够互相传递结果。
通过使用Bash Shell脚本功能，可以将Linux命令组合成Shell脚本，来解决重复的实际问题。


Bash Shell脚本是一个可执行文件，包含一系列命令，可能还包括编程逻辑来控制任务中的决策。
当脚本编写得当时，可以将其与其他脚本一起使用。Shell脚本技能对于系统管理员是必不可少的。




### 简单入门
脚本的第一行以“#!”符号开头，这通常被称为she-bang或hash-bang，
这是一个解释器指令，指示需要处理文件其余部分的命令解释器和可选的命令选项。
对于普通的Bash语法脚本文件，第一行是这样的指令：
```bash
#!/usr/bin/bash
```


要将Shell脚本作为普通命令执行，脚本文件必须具有执行权限。
可以使用`chmod`命令修改文件的权限。或将执行权限授予特定用户或用户组。


`PATH`环境变量与`which`命令查询


可以使用反斜杠字符（`\`）、单引号（`''`）或双引号（`""`）来去除特殊含义。

反斜杠字符（`\`）会去除紧随其后的单个字符的特殊含义。

单引号会保留其中所有字符的字面含义

双引号可以抑制通配符（文件名模式匹配）和Shell扩展，但仍然允许命令和变量替换。

单引号将所有文本按字面意思解释。抑制通配符匹配和Shell扩展，还会抑制命令和变量替换。
在单引号内，问号（`?`）也作为元字符需要进行转义，防止其被展开。





`echo`命令消息可以指示脚本的进度，并可以重定向到标准输出、标准错误，日志文件
在显示错误消息时，是将错误消息重定向到STDERR，以便将其与正常的程序输出分开。

示例：

```Bash
[user@host ~]$ cat ~/bin/hello
#!/usr/bin/bash
echo "Hello, world"
echo "ERROR: Houston, we have a problem." >&2
[user@host ~]$ hello 2> hello.log
Hello, world
[user@host ~]$ cat hello.log
ERROR: Houston, we have a problem.
```




### 引导练习1
1. 使用`vim`命令在家目录下创建`firstscript.sh`文件。
```bash
#!/usr/bin/bash
echo "This is my first bash script" > ~/output.txt
echo "" >> ~/output.txt
echo "#####################################################" >> ~/output.txt
```

```bash
[student@servera ~]$ sh firstscript.sh

[student@servera ~]$ cat output.txt
This is my first bash script
#####################################################
```


2. 编辑 `firstscript.sh` 脚本。
```bash
#!/usr/bin/bash
echo "This is my first bash script" > ~/output.txt
echo "" >> ~/output.txt
echo "#####################################################" >> ~/output.txt
echo "LIST BLOCK DEVICES" >> ~/output.txt
echo "" >> ~/output.txt
lsblk >> ~/output.txt
echo "" >> ~/output.txt
echo "#####################################################" >> ~/output.txt
echo "FILESYSTEM FREE SPACE STATUS" >> ~/output.txt
echo "" >> ~/output.txt
df -h >> ~/output.txt
echo "#####################################################" >> ~/output.txt
```


3. 查看脚本生成的输出文件。
```bash
[student@servera ~]$ cat output.txt
This is my first bash script
#####################################################
LIST BLOCK DEVICES
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sr0     11:0    1  558K  0 rom
vda    252:0    0   10G  0 disk
 ├─vda1 252:1    0    1M  0 part
 ├─vda2 252:2    0  200M  0 part /boot/efi
 ├─vda3 252:3    0  500M  0 part /boot
 └─vda4 252:4    0  9.3G  0 part / 
vdb    252:16   0    5G  0 disk
vdc    252:32   0    5G  0 disk
vdd    252:48   0    5G  0 disk
#####################################################
FILESYSTEM FREE SPACE STATUS
Filesystem      Size  Used Avail Use% Mounted on
devtmpfs        844M     0  844M   0% /dev
tmpfs           888M     0  888M   0% /dev/shm
tmpfs           355M  9.4M  346M   3% /run
/dev/vda4       9.4G  1.7G  7.7G  18% /
/dev/vda3       495M  161M  335M  33% /boot
/dev/vda2       200M  7.6M  193M   4% /boot/efi
tmpfs           178M     0  178M   0% /run/user/1000
#####################################################
```




### 循环和条件语句在脚本中的应用
常常需要处理重复性任务。可能需要每分钟检查一次进程，持续 10 分钟，
以确认该进程是否已经完成。或对多个目标执行命令，比如备份系统中的多个数据库。


在 Bash 中，`for` 循环的语法如下：
```bash
for VARIABLE in LIST; do
    COMMAND $VARIABLE
done
```

这个循环将处理你在 `LIST` 中提供的字符串，直到处理完列表中的最后一个字符串。每次迭代，`for` 循环将 `LIST` 中的每个字符串临时存储为 `VARIABLE` 的值，并执行使用该变量的命令块。`VARIABLE` 的名字可以任意选择，通常在命令块中使用变量的值。

你可以通过用户直接输入的列表，或者通过 shell 展开（如变量、花括号扩展、文件名扩展或命令替换）来提供字符串。

以下是几种不同方式向 `for` 循环提供字符串的示例：

1.  **直接列出字符串**
    
    ```bash
    [user@host ~]$ for HOST in host1 host2 host3; do echo $HOST; done
    host1
    host2
    host3
    ```
    
2.  **使用花括号扩展**
    
    ```bash
    [user@host ~]$ for HOST in host{1,2,3}; do echo $HOST; done
    host1
    host2
    host3
    ```
    
3.  **使用数字范围扩展**
    
    ```bash
    [user@host ~]$ for HOST in host{1..3}; do echo $HOST; done
    host1
    host2
    host3
    ```
    
4.  **使用文件名扩展**
    
    ```bash
    [user@host ~]$ for FILE in file{a..c}; do ls $FILE; done
    filea
    fileb
    filec
    ```
    
5.  **通过命令替换提供列表**
    
    ```csharp
    [user@host ~]$ for PACKAGE in $(rpm -qa | grep kernel); \
    do echo "$PACKAGE was installed on \
    $(date -d @$(rpm -q --qf "%{INSTALLTIME}\n" $PACKAGE))"; done
    kernel-tools-libs-5.14.0-70.2.1.el9_0.x86_64 was installed on Thu Mar 24 10:52:40 PM EDT 2022
    kernel-tools-5.14.0-70.2.1.el9_0.x86_64 was installed on Thu Mar 24 10:52:40 PM EDT 2022
    kernel-core-5.14.0-70.2.1.el9_0.x86_64 was installed on Thu Mar 24 10:52:46 PM EDT 2022
    kernel-modules-5.14.0-70.2.1.el9_0.x86_64 was installed on Thu Mar 24 10:52:47 PM EDT 2022
    kernel-5.14.0-70.2.1.el9_0.x86_64 was installed on Thu Mar 24 10:53:04 PM EDT 2022
    ```
    
6.  **使用 `seq` 生成数字序列**
    
    ```bash
    [user@host ~]$ for EVEN in $(seq 2 2 10); do echo "$EVEN"; done
    2
    4
    6
    8
    10
    ```

## Response:
### Bash 脚本的退出码

在脚本解析并处理完所有内容后，脚本进程会退出，并将控制权返回给调用它的父进程。然而，脚本也可以在未完成时退出，例如，当脚本遇到错误时。可以使用 `exit` 命令立即退出脚本，并跳过剩余的脚本处理。

`exit` 命令可以带上一个可选的整数参数，范围从 0 到 255，表示退出码。退出码会返回给父进程，用来指示脚本退出时的状态。退出码值为 0 表示脚本成功完成并且没有错误，其他非零值则表示错误退出码。脚本开发者定义这些退出码，通常会使用不同的值来表示遇到的不同错误条件。可以通过内置变量 `$?` 获取上一个执行命令的退出码，如下所示：

#### 示例：

```bash
[user@host bin]$ cat hello
#!/usr/bin/bash
echo "Hello, world"
exit 0

[user@host bin]$ ./hello
Hello, world

[user@host bin]$ echo $?
0
```

如果在 `exit` 命令后没有指定退出码参数，脚本将返回最后一个执行命令的退出码。

* * *

### 字符串和目录的测试逻辑，以及数值比较

为了确保脚本在遇到意外情况时不会轻易中断，建议验证命令输入，如命令行参数、用户输入、命令替换、变量扩展和文件名扩展等。可以使用 Bash 中的 `test` 命令来检查脚本中的条件。

所有命令在执行完毕后都会产生退出码，要查看退出状态，只需在执行 `test` 命令后立即查看 `$?` 变量。退出状态为 0 表示成功执行且没有任何需要报告的内容，非零值则表示存在某种条件或错误。

可以使用各种运算符进行测试，判断一个数是否大于（gt）、大于或等于（ge）、小于（lt）、小于或等于（le）或等于（eq）另一个数。

你还可以使用运算符测试两个字符串是否相同（`=` 或 `==`）或不相同（`!=`），或者测试字符串的长度是否为零（`-z`）或非零（`-n`）。你还可以测试文件是否存在，例如是否为常规文件（`-f`）或目录（`-d`），以及文件是否具有某些特殊属性，例如是否为符号链接（`-L`）或用户是否有读取权限（`-r`）。

#### 注意：

Shell 脚本使用的运算符类型远不止这些，`test` 命令的手册页列出了所有的条件表达式运算符和相关描述。`bash` 命令手册页也解释了运算符的使用和求值，但阅读起来可能比较复杂。Red Hat 推荐学生通过质量高的书籍和课程来学习 Shell 编程。

以下示例演示了 `test` 命令与 Bash 数值比较运算符的用法：

#### 示例：

```bash
[user@host ~]$ test 1 -gt 0 ; echo $?
0

[user@host ~]$ test 0 -gt 1 ; echo $?
1
```

通过使用 Bash 的测试命令语法 `[ <TESTEXPRESSION> ]` 或更新的扩展测试命令语法 `[[ <TESTEXPRESSION> ]]`，可以进行测试，后者支持文件名扩展和正则表达式模式匹配。大多数情况下，推荐使用 `[[ <TESTEXPRESSION> ]]` 语法。

以下是使用 Bash 测试命令语法和数值比较运算符的示例：

#### 示例：

```bash
[user@host ~]$ [[ 1 -eq 1 ]]; echo $?
0

[user@host ~]$ [[ 1 -ne 1 ]]; echo $?
1

[user@host ~]$ [[ 8 -gt 2 ]]; echo $?
0

[user@host ~]$ [[ 2 -ge 2 ]]; echo $?
0

[user@host ~]$ [[ 2 -lt 2 ]]; echo $?
1

[user@host ~]$ [[ 1 -lt 2 ]]; echo $?
0
```

## Response:
### Bash 字符串比较运算符示例

以下示例演示了 Bash 字符串比较运算符的使用：

#### 示例：

```bash
[user@host ~]$ [[ abc = abc ]]; echo $?
0

[user@host ~]$ [[ abc == def ]]; echo $?
1

[user@host ~]$ [[ abc != def ]]; echo $?
0
```

*   `=` 和 `==` 用于测试两个字符串是否相等，若相等返回 0，否则返回 1。
*   `!=` 用于测试两个字符串是否不相等，若不相等返回 0，否则返回 1。

### Bash 字符串单目（单参数）运算符示例

以下示例演示了 Bash 字符串单目运算符的使用：

#### 示例：

```bash
[user@host ~]$ STRING=''; [[ -z "$STRING" ]]; echo $?
0

[user@host ~]$ STRING='abc'; [[ -n "$STRING" ]]; echo $?
0
```

*   `-z` 用于测试字符串是否为空，若为空返回 0，否则返回 1。
*   `-n` 用于测试字符串是否非空，若非空返回 0，否则返回 1。

### 注意事项

在使用测试命令时，括号中的空格是必需的，因为它们将测试表达式中的各个词语和元素分开。Shell 的命令解析机制通过识别空格和其他元字符，按照内建的解析规则将命令元素分割成词语和运算符。为深入理解这一高级概念，可以查阅 `getopt(3)` 手册页。

此外，左方括号 `[` 本身就是 `test` 命令的一个内建别名。Shell 中的词语，无论是命令、子命令、选项、参数还是其他标记元素，都会被空格分隔开。

## Response:
### 条件结构

简单的 Shell 脚本代表了一系列按顺序执行的命令。程序员通过在 Shell 脚本中加入条件结构来实现决策功能。当满足特定条件时，脚本可以执行特定的操作。

### 使用 If/Then 结构

最简单的条件结构是 `if/then` 结构，其语法如下：

```bash
if <CONDITION>; then
    <STATEMENT>
    ...
    <STATEMENT>
fi
```

在这种结构中，如果脚本满足给定的条件，则会执行 `then` 后的语句块。如果条件不满足，则不执行任何操作。`if/then` 语句常用的条件包括之前提到的数字比较、字符串比较以及文件测试等。`fi` 语句用于结束 `if/then` 结构。

#### 示例：

以下代码段演示了如何使用 `if/then` 结构来启动 `psacct` 服务（如果该服务未激活）：

```bash
[user@host ~]$ systemctl is-active psacct > /dev/null 2>&1
[user@host ~]$ if [[ $? -ne 0 ]]; then sudo systemctl start psacct; fi
```

*   `systemctl is-active psacct` 检查 `psacct` 服务的状态，如果该服务没有活动状态，命令的退出状态码会为非零。
*   `[[ $? -ne 0 ]]` 检查上一个命令的退出状态码是否不等于 0，即服务没有运行。
*   如果条件为真，`sudo systemctl start psacct` 会启动 `psacct` 服务。

## Response:
### 使用 If/Then/Else 结构

你可以进一步扩展 `if/then` 结构，使其根据条件是否满足采取不同的行动。使用 `if/then/else` 结构可以实现这种行为，其语法如下：

```bash
if <CONDITION>; then
    <STATEMENT>
    ...
    <STATEMENT>
else
    <STATEMENT>
    ...
    <STATEMENT>
fi
```

在这种结构中，如果条件满足，则执行 `then` 后的语句块；如果条件不满足，则执行 `else` 后的语句块。

#### 示例：

以下代码段演示了如何使用 `if/then/else` 语句来启动 `psacct` 服务（如果未激活）并停止它（如果已激活）：

```bash
[user@host ~]$ systemctl is-active psacct > /dev/null 2>&1
[user@host ~]$ if [[ $? -ne 0 ]]; then \
    sudo systemctl start psacct; \
else \
    sudo systemctl stop psacct; \
fi
```

*   `systemctl is-active psacct` 用于检查 `psacct` 服务的状态，如果服务未激活，命令的退出状态码为非零。
*   `[[ $? -ne 0 ]]` 检查上一个命令的退出状态码是否不为 0，表示服务未启动。
*   如果条件为真（即服务未启动），则执行 `sudo systemctl start psacct` 启动服务；如果条件为假（即服务已启动），则执行 `sudo systemctl stop psacct` 停止服务。

## Response:
### 使用 If/Then/Elif/Then/Else 结构

可以扩展 `if/then/else` 结构，以便测试多个条件，并在满足特定条件时执行不同的操作。这个结构通过引入 `elif` 语句来支持多条件判断。其语法如下：

```bash
if <CONDITION>; then
    <STATEMENT>
    ...
    <STATEMENT>
elif <CONDITION>; then
    <STATEMENT>
    ...
    <STATEMENT>
else
    <STATEMENT>
    ...
    <STATEMENT>
fi
```

在这个条件结构中，Bash 按照脚本中条件的顺序逐一进行测试。当某个条件为真时，Bash 会执行与该条件相关联的操作，并跳过其余条件的测试。如果没有任何条件为真，Bash 会执行 `else` 语句块中的操作。

#### 示例：

以下代码示例演示了如何使用 `if/then/elif/then/else` 语句来判断 `mariadb` 服务是否正在运行，如果是，则运行 `mysql` 客户端；如果不是，则判断 `postgresql` 服务是否在运行，如果是，则运行 `psql` 客户端：

```bash
[user@host ~]$ systemctl is-active mariadb > /dev/null 2>&1
[user@host ~]$ if [[ $? -eq 0 ]]; then
    mysql -u root -p
elif systemctl is-active postgresql > /dev/null 2>&1; then
    psql -U postgres
else
    echo "Both services are inactive."
fi
```

*   首先，脚本检查 `mariadb` 服务是否激活。如果激活，则执行 `mysql -u root -p` 启动 MySQL 客户端。
*   如果 `mariadb` 服务未激活，脚本会继续检查 `postgresql` 服务是否激活。如果激活，则执行 `psql -U postgres` 启动 PostgreSQL 客户端。
*   如果两个服务都没有激活，则执行 `else` 部分，输出 `"Both services are inactive."` 表示两个服务都未启动。

## Response:
### 循环和条件结构在脚本中的应用

#### 目标：

*   使用 `for` 循环有效地打印多个服务器的主机名。

#### 目标成果：

*   创建一个 `for` 循环，从命令行和 shell 脚本中迭代处理一系列项。

#### 开始之前：

在工作站机器上作为 `student` 用户，使用 `lab` 命令准备系统进行本次练习。此命令将准备您的环境并确保所需的资源已就绪。

```bash
[student@workstation ~]$ lab start console-commands
```

#### 练习步骤：

1.  **使用 `ssh` 和 `hostname` 命令打印 `servera` 和 `serverb` 机器的主机名到标准输出：**

```bash
[student@workstation ~]$ ssh student@servera hostname
servera.lab.example.com

[student@workstation ~]$ ssh student@serverb hostname
serverb.lab.example.com
```

2.  **创建一个 `for` 循环来在 `servera` 和 `serverb` 机器上执行 `hostname` 命令：**

```bash
[student@workstation ~]$ for HOST in servera serverb
> do
> ssh student@${HOST} hostname
> done
servera.lab.example.com
serverb.lab.example.com
```

#### 解释：

*   通过 `for` 循环，我们将 `servera` 和 `serverb` 作为目标服务器列表，依次运行 `ssh` 命令连接到每个服务器并执行 `hostname` 命令。
*   变量 `${HOST}` 在每次循环迭代时会被替换为服务器的名称，从而让命令分别在每台服务器上执行。

通过这种方式，您可以轻松地对多个服务器进行批量操作，减少手动执行命令的时间。

## Response:
### 创建一个脚本来执行相同的 `for` 循环

#### 目标：

*   创建一个 Shell 脚本，并确保脚本可以通过 PATH 环境变量访问。
*   脚本的功能是执行与之前相同的 `for` 循环，打印多个服务器的主机名。

#### 步骤：

1.  **创建 `/home/student/bin` 目录（如果它还不存在）：**

```bash
[student@workstation ~]$ mkdir ~/bin
```

2.  **验证 `bin` 子目录是否已经添加到 `PATH` 环境变量中：**

```bash
[student@workstation ~]$ echo $PATH
/home/student/.local/bin:/home/student/bin:/sbin:/bin:/usr/sbin:/usr/bin:/usr/local/sbin:/usr/local/bin:/home/student/.venv/labs/bin
```

如果 `/home/student/bin` 不在 `PATH` 中，您可以手动将它添加到 `.bashrc` 或 `.bash_profile` 文件中。

3.  **创建名为 `printhostname.sh` 的脚本并保存到 `/home/student/bin` 目录中：**

```bash
[student@workstation ~]$ vim ~/bin/printhostname.sh
```

在 `vim` 编辑器中输入以下脚本内容：

```bash
#!/usr/bin/bash
# Execute for loop to print server hostname.
for HOST in servera serverb
do
  ssh student@${HOST} hostname
done
exit 0
```

然后，保存并退出编辑器。

4.  **使用 `cat` 命令验证脚本内容：**

```bash
[student@workstation ~]$ cat ~/bin/printhostname.sh
#!/usr/bin/bash
# Execute for loop to print server hostname.
for HOST in servera serverb
do
  ssh student@${HOST} hostname
done
exit 0
```

5.  **给脚本文件添加可执行权限：**

```bash
[student@workstation ~]$ chmod +x ~/bin/printhostname.sh
```

6.  **从家目录运行脚本：**

```bash
[student@workstation ~]$ printhostname.sh
servera.lab.example.com
serverb.lab.example.com
```

7.  **验证脚本的退出代码是否为 0：**

```bash
[student@workstation ~]$ echo $?
0
```

#### 解释：

*   `mkdir ~/bin` 创建了一个新的目录来存放脚本文件。
*   `echo $PATH` 用于确认 `/home/student/bin` 是否在 `PATH` 环境变量中，确保脚本可以从任何地方调用。
*   `vim ~/bin/printhostname.sh` 创建并编辑脚本文件，脚本内使用 `for` 循环连接到远程服务器并执行 `hostname` 命令。
*   `chmod +x ~/bin/printhostname.sh` 给脚本文件添加了执行权限。
*   执行 `printhostname.sh` 后，脚本按预期输出了两台服务器的主机名。
*   最后，使用 `echo $?` 确认脚本执行后返回了退出码 `0`，表示脚本成功执行没有错误。

通过这个过程，您创建了一个可以反复执行的 Shell 脚本，并能够在任何地方运行它。

## Response:
### 使用正则表达式匹配命令输出中的文本

#### 目标

*   编写正则表达式来匹配数据。
*   使用 `grep` 命令在文本文件中应用正则表达式进行搜索。
*   利用 `grep` 搜索文件内容和从管道命令传递的数据。

### 编写正则表达式

正则表达式提供了一种模式匹配机制，可以帮助用户查找特定的内容。工具如 `vim`、`grep`、`less` 都可以使用正则表达式，而编程语言如 Perl、Python 和 C 也支持正则表达式，但它们的语法可能有所不同。

正则表达式是一种独特的语言，具有自己的语法和规则。以下是 Bash 中实现的正则表达式语法介绍，并附有示例。

### 简单的正则表达式

最简单的正则表达式是完全匹配搜索的字符串。完全匹配意味着正则表达式中的字符与要查找的字符串中的字符类型和顺序完全一致。

#### 示例

假设用户正在查看以下文件，并希望查找所有出现的模式 `cat`：

```bash
cat
dog
concatenate
dogma
category
educated
boondoggle
vindication
chilidog
```

在这个文件中，`cat` 字符串是精确匹配 `c` 字符后接 `a` 和 `t` 字符，中间没有其他字符。使用 `cat` 字符串作为正则表达式进行搜索时，将返回以下匹配项：

```bash
cat
concatenate
category
educated
vindication
```

在这个例子中，`grep` 会查找文件中所有包含 `cat` 字符串的行，并返回这些行的内容。可以通过以下命令来进行搜索：

```bash
grep 'cat' 文件名
```

输出将是：

```bash
cat
concatenate
category
educated
vindication
```

### 小结

1.  **正则表达式的作用**：通过正则表达式可以灵活地匹配和查找文件中某些模式或文本。
2.  **简单的匹配**：最简单的正则表达式是直接匹配整个字符串，例如 `cat` 会匹配所有包含该字符串的行。

下一步可以介绍更复杂的正则表达式匹配，如字符类、量词、边界匹配等，以及如何使用 `grep` 进行更复杂的文本搜索。

## Response:
### 匹配行的开始和结束

正则表达式通常会在行中的任意位置匹配搜索的字符串：无论是在行的开头、中间还是结尾。如果你希望仅在行的开头或结尾进行匹配，可以使用行锚定元字符来控制匹配的位置。

*   **匹配行的开始**：使用插入符号 `^` 来表示行的开头。
*   **匹配行的结束**：使用美元符号 `$` 来表示行的结尾。

### 示例

假设我们有以下文件内容：

```bash
cat
dog
concatenate
dogma
category
educated
boondoggle
vindication
chilidog
```

#### 使用 `^` 匹配行的开头

正则表达式 `^cat` 将匹配位于行首的 `cat` 字符串。这个正则表达式会匹配以下两行：

```bash
cat
category
```

因为 `cat` 出现在行的开始处，而 `category` 是以 `cat` 开头的单词。

```bash
grep '^cat' 文件名
```

输出为：

```bash
cat
category
```

#### 使用 `$` 匹配行的结尾

正则表达式 `cat$` 仅匹配以 `cat` 结尾的行。这个正则表达式不会找到任何匹配项，因为没有行是以 `cat` 结尾的。

```bash
grep 'cat$' 文件名
```

输出为空，因为没有行的结尾是 `cat`。

#### 使用 `$` 匹配行尾的特定字符串

要找到以 `dog` 结尾的行，可以使用正则表达式 `dog$`。这个正则表达式会匹配以下两行：

```
dog
chilidog
```

这两行分别是以 `dog` 结尾的单词和以 `dog` 结尾的单词（`chilidog`）。

```bash
grep 'dog$' 文件名
```

输出为：

```
dog
chilidog
```

#### 精确匹配整行的内容

如果你想要找到完全匹配某个字符串的行，可以同时使用行首和行尾锚定符。例如，`^cat$` 将仅匹配完全是 `cat` 的行，也就是说，行首和行尾都必须是 `cat`，没有其他字符。

```bash
grep '^cat$' 文件名
```

输出为：

```bash
cat
```

### 小结

1.  **匹配行首**：使用 `^` 来表示匹配行的开始。
2.  **匹配行尾**：使用 `$` 来表示匹配行的结尾。
3.  **精确匹配整行**：通过同时使用 `^` 和 `$` 来匹配整行文本，例如 `^cat$` 仅匹配完全是 `cat` 的行。

这种方式可以让你更精确地定位文本文件中的特定位置。

## Response:
### 通配符和量词在正则表达式中的使用

正则表达式使用点号字符（`.`）作为通配符，匹配每一行中的任意单个字符。通过这种方式，可以实现非常灵活的匹配模式。

### 通配符（Wildcard）

1.  **`.` 通配符**：匹配任何单个字符。
    
    例如，正则表达式 `c.t` 将匹配任意以 `c` 开头、`t` 结尾且中间有一个字符的字符串。可能的匹配包括：
    
    *   `cat`
    *   `cut`
    *   `cot`
    *   `concatenate`
    *   `vindication`
    *   `c$t`
    
    `.` 通配符不限制中间字符的类型，因此它可以匹配任何字符。
    

### 字符集（Character Classes）

通过使用方括号 `[]`，可以指定一个字符集来匹配特定的字符。例如，`c[aou]t` 会匹配以 `c` 开头、接着是 `a`、`o` 或 `u` 中的任意一个字符，最后是 `t` 的字符串。可以匹配的字符串包括：

*   `cat`
*   `cot`
*   `cut`

在这种情况下，方括号 `[]` 使得你可以精确指定字符集，而不是仅使用通配符 `.`。

### 量词（Multipliers）

量词用于限定通配符或前一个字符匹配的次数。最常用的量词是星号 `*`，它表示“零个或多个”匹配项。星号可以应用于字符或其他表达式。

1.  **`*` 量词**：匹配零个或多个字符。
    
    *   正则表达式 `c[aou]*t` 可以匹配 `coat` 或 `coot`。
    *   正则表达式 `c.*t` 匹配所有以 `c` 开头、以 `t` 结尾的字符串，包括：
        *   `cat`
        *   `coat`
        *   `culvert`
        *   `ct`（注意，这里匹配的是 `c` 和 `t` 之间没有字符的情况）
    
    正则表达式 `c.*t` 会匹配任何以 `c` 开头，接着是零个或多个字符，最后是 `t` 结尾的字符串。
    

### 精确次数的量词

除了 `*`，还有一些量词可以限定更精确的字符出现次数。比如 `{n}` 表示“精确出现 n 次”。

2.  **`{n}` 量词**：匹配前一个字符或表达式恰好出现 n 次。
    
    *   例如，`c.\{2\}t` 会匹配以 `c` 开头，接着是任意两个字符，然后是 `t` 结尾的字符串。
    
    下面是一个匹配例子，其中 `c.\{2\}t` 匹配以 `c` 开头、两个字符后以 `t` 结尾的字符串：
    
    *   `cat`
    *   `coat`
    
    `c.\{2\}t` 会匹配如下两个单词：
    *   `cat`
    *   `coat`

### 区别于 Shell 文件模式匹配

正则表达式和 Shell 文件模式匹配（通常被称为文件通配符或文件名扩展）有很多相似之处，例如两者都使用 `*` 作为通配符。然而，它们在语法和规则上存在差异，可能会让初学者感到混淆。具体区别如下：

*   **文件模式匹配**：主要用于命令行中匹配文件名（例如 `ls *.txt`），用来简便地指定多个文件名。
*   **正则表达式**：可以在各种文本处理工具中使用，例如 `grep`、`sed`、`awk`、`python` 和 `perl`，它们用于匹配复杂的文本模式。

正则表达式的功能要比文件模式匹配强大得多，能够表示几乎任何形式或模式，适用于文本数据的处理和提取。

### 小结

1.  **`.`** 匹配任意单个字符。
2.  **`[]`** 用于指定字符集，匹配其中的任意一个字符。
3.  **`*`** 匹配零个或多个字符。
4.  **`{n}`** 用于指定字符或表达式出现的精确次数。

这些特性使得正则表达式能够非常灵活和强大，适用于各种文本搜索和处理任务。

## Response:
| 选项 | 描述 |
| --- | --- |
| `.` | 句点（`.`）匹配任何单个字符。 |
| `?` | 前面的项目是可选的，并且最多匹配一次。 |
| `*` | 前面的项目匹配零次或多次。 |
| `+` | 前面的项目匹配一次或多次。 |
| `{n}` | 前面的项目精确匹配 n 次。 |
| `{n,}` | 前面的项目匹配 n 次或更多次。 |
| `{,m}` | 前面的项目匹配最多 m 次。 |
| `{n,m}` | 前面的项目匹配至少 n 次，但不超过 m 次。 |
| `[:alnum:]` | 字母数字字符：包括 `[:alpha:]` 和 `[:digit:]`；在 `C` 语言环境和 ASCII 字符编码中，该表达式等同于 `[0-9A-Za-z]`。 |
| `[:alpha:]` | 字母字符：包括 `[:lower:]` 和 `[:upper:]`；在 `C` 语言环境和 ASCII 字符编码中，该表达式等同于 `[A-Za-z]`。 |
| `[:blank:]` | 空白字符：空格和制表符。 |
| `[:cntrl:]` | 控制字符：在 ASCII 中，这些字符的八进制代码是 000 到 037，以及 177（DEL）。 |
| `[:digit:]` | 数字字符：0 1 2 3 4 5 6 7 8 9。 |
| `[:graph:]` | 图形字符：包括 `[:alnum:]` 和 `[:punct:]`。 |
| `[:lower:]` | 小写字母；在 `C` 语言环境和 ASCII 字符编码中：a b c d e f g h i j k l m n o p q r s t u v w x y z。 |
| `[:print:]` | 可打印字符：包括 `[:alnum:]`、`[:punct:]` 和空格。 |
| `[:punct:]` | 标点字符；在 `C` 语言环境和 ASCII 字符编码中：\`! " # $ % & ' ( ) \* + , - . / : ; < = > ? @ \[ \\ \] ^ \_ ' { |
| `[:space:]` | 空白字符：在 `C` 语言环境中，包括制表符、换行符、垂直制表符、换页符、回车符和空格。 |
| `[:upper:]` | 大写字母；在 `C` 语言环境和 ASCII 字符编码中：A B C D E F G H I J K L M N O P Q R S T U V W X Y Z。 |
| `[:xdigit:]` | 十六进制数字：0 1 2 3 4 5 6 7 8 9 A B C D E F a b c d e f。 |
| `\b` | 匹配单词边界处的空字符串。 |
| `\B` | 匹配空字符串，前提是它不在单词的边界处。 |
| `\<` | 匹配单词的开始处的空字符串。 |
| `\>` | 匹配单词的结束处的空字符串。 |
| `\w` | 匹配单词构成字符。是 `[_[:alnum:]]` 的同义词。 |
| `\W` | 匹配非单词构成字符。是 `[^_[:alnum:]]` 的同义词。 |
| `\s` | 匹配空白字符。是 `[[:space:]]` 的同义词。 |
| `\S` | 匹配非空白字符。是 `[^[:space:]]` 的同义词。 |

## Response:
在命令行中匹配正则表达式

`grep` 命令使用正则表达式来隔离匹配的数据。你可以使用 `grep` 命令来匹配单个文件或多个文件中的数据。当你使用 `grep` 来匹配多个文件时，它会打印文件名，后跟冒号字符，然后是匹配正则表达式的行。

### 使用 `grep` 命令隔离数据

`grep` 命令指定一个正则表达式和一个文件，来解析该文件并查找匹配项。

例如，使用以下命令来匹配以“computer”开头的单词：

```bash
[user@host ~]$ grep '^computer' /usr/share/dict/words
computer
computerese
computerise
computerite
computerizable
computerization
computerize
computerized
computerizes
computerizing
computerlike
computernik
computers
```

> 注意：推荐使用单引号来括住正则表达式，以防止任何 shell 特殊字符（如 `$`、`*` 和 `{}` 等）被解释为 shell 元字符。将正则表达式放入单引号内，确保这些字符按预期传递给命令，而不是由 shell 解释。

### 使用管道操作符（`|`）将其他命令的输出传递给 `grep`

`grep` 命令还可以处理来自其他命令的输出，方法是使用管道操作符（`|`）。以下是一个示例，显示 `ps aux` 命令的输出中包含 "chrony" 的行：

```bash
[root@host ~]# ps aux | grep chrony
chrony
     662  0.0  0.1  29440  2468 ?        S    10:56   0:00 /usr/sbin/chronyd
```

## Response:
### `grep` 命令选项

`grep` 命令具有许多有用的选项，用于控制它如何解析行。以下是常见 `grep` 选项的表格：

| **选项** | **功能** |
| --- | --- |
| `-i` | 使用提供的正则表达式但不区分大小写（执行不区分大小写的匹配）。 |
| `-v` | 只显示不包含正则表达式匹配的行。 |
| `-r` | 在一组文件或目录中递归地查找匹配正则表达式的数据。 |
| `-A NUMBER` | 显示匹配正则表达式后的 `NUMBER` 行。 |
| `-B NUMBER` | 显示匹配正则表达式前的 `NUMBER` 行。 |
| `-e` | 如果使用多个 `-e` 选项，则可以提供多个正则表达式，使用逻辑 OR 来匹配。 |

查看 `man` 页面以查找更多 `grep` 命令的选项。

## Response:
### `grep` 命令示例

以下示例展示了如何使用不同的配置文件和日志文件进行搜索。

#### 示例 1：使用 `-i` 选项进行不区分大小写的搜索

默认情况下，正则表达式是区分大小写的。可以使用 `-i` 选项来执行不区分大小写的搜索。以下是搜索 `/etc/httpd/conf/httpd.conf` 配置文件中的 `serverroot` 正则表达式的示例。

```bash
[user@host ~]$ cat /etc/httpd/conf/httpd.conf
...output omitted...
ServerRoot "/etc/httpd"
#
# Listen: Allows you to bind Apache to specific IP addresses and/or
# ports, instead of the default. See also the <VirtualHost>
# directive.
#
# Change this to Listen on a specific IP address, but note that if
# httpd.service is enabled to run at boot time, the address may not be
# available when the service starts.  See the httpd.service(8) man
# page for more information.
#
#Listen 12.34.56.78:80
Listen 80
...output omitted...

[user@host ~]$ grep -i serverroot /etc/httpd/conf/httpd.conf
# with "/", the value of ServerRoot is prepended -- so 'log/access_log'
# with ServerRoot set to '/www' will be interpreted by the
# ServerRoot: The top of the directory tree under which the server's
# ServerRoot at a non-local disk, be sure to specify a local disk on the
# same ServerRoot for multiple httpd daemons, you will need to change at
ServerRoot "/etc/httpd"
```

#### 示例 2：使用 `-v` 选项进行反向搜索

使用 `-v` 选项进行反向搜索，该选项只显示不匹配正则表达式的行。以下示例返回所有不包含 `server` 正则表达式的行，且不区分大小写。

```bash
[user@host ~]$ grep -v -i server /etc/hosts
127.0.0.1 localhost.localdomain localhost
172.25.254.254 classroom.example.com classroom
172.25.254.254 content.example.com content
172.25.254.254 materials.example.com materials
### rht-vm-hosts file listing the entries to be appended to /etc/hosts
172.25.250.9 workstation.lab.example.com workstation
```

## Response:
### 专业翻译

```
172.25.250.254 bastion.lab.example.com bastion
172.25.250.220 utility.lab.example.com utility
172.25.250.220 registry.lab.example.com registry
```

要查看文件并避免被注释行分散注意力，可以使用 `grep` 命令的 `-v` 选项。在以下示例中，正则表达式匹配所有以井号 (`#`) 或分号 (`;`) 开头的行。这两种字符在行首表示注释，这些行会被从输出中省略。

```bash
[user@host ~]$ grep -v '^[#;]' /etc/ethertypes
IPv4   0800   ip ip4   # Internet IP (IPv4)
X25  0805
ARP  0806 ether-arp #
FR_ARP  0808      # Frame Relay ARP        [RFC1701]
```

`grep` 命令的 `-e` 选项允许你同时搜索多个正则表达式。以下示例使用 `less` 和 `grep` 命令的组合，查找 `/var/log/secure` 日志文件中所有出现的 `pam_unix`、`user root` 和 `Accepted publickey`。

```bash
[root@host ~]# cat /var/log/secure | grep -e 'pam_unix' -e 'user root' -e 'Accepted publickey' | less
Mar  4 03:31:41 localhost passwd[6639]: pam_unix(passwd:chauthtok): password changed for root
Mar  4 03:32:34 localhost sshd[15556]: Accepted publickey for devops from 10.30.0.167 port 56472 ssh2: RSA SHA256:M8ikhcEDm2tQ95Z0o7ZvufqEixCFCt+wowZLNzNlBT0
Mar  4 03:32:34 localhost systemd[15560]: pam_unix(systemd-user:session): session opened for user devops(uid=1001) by (uid=0)
```

要在打开的文件中搜索文本（例如在 `vim` 或 `less` 命令中打开的文件），首先输入斜杠 (`/`)，然后输入要查找的模式。按下回车键开始搜索，按 `N` 查找下一个匹配项。

```bash
[root@host ~]# vim /var/log/boot.log
...output omitted...
[^[[0;32m  OK  ^[[0m] Finished ^[[0;1;39mdracut pre-pivot and cleanup hook^[[0m.]^M
         Starting ^[[0;1;39mCleaning Up and Shutting Down Daemons^[[0m...^M
[^[[0;32m  OK  ^[[0m] Stopped target ^[[0;1;39mRemote Encrypted Volumes^[[0m.]^M
[^[[0;32m  OK  ^[[0m] Stopped target ^[[0;1;39mTimer Units^[[0m.]^M
[^[[0;32m  OK  ^[[0m] Closed ^[[0;1;39mD-Bus System Message Bus Socket^[[0m.]^M
/Daemons
[root@host ~]# less /var/log/messages
...output omitted...
Mar  4 03:31:19 localhost kernel: pci 0000:00:02.0: vgaarb: setting as boot VGA device
Mar  4 03:31:19 localhost kernel: pci 0000:00:02.0: vgaarb: VGA device added: decodes=io+mem, owns=io+mem, locks=none
Mar  4 03:31:19 localhost kernel: pci 0000:00:02.0: vgaarb: bridge control possible
Mar  4 03:31:19 localhost kernel: vgaarb: loaded
```

## Response:
### 专业翻译

```go
Mar  4 03:31:19 localhost kernel: SCSI subsystem initialized
Mar  4 03:31:19 localhost kernel: ACPI: bus type USB registered
Mar  4 03:31:19 localhost kernel: usbcore: registered new interface driver usbfs
Mar  4 03:31:19 localhost kernel: usbcore: registered new interface driver hub
Mar  4 03:31:19 localhost kernel: usbcore: registered new device driver usb
/device
```

### 使用正则表达式在命令输出中匹配文本

在本实验中，您将搜索系统日志和命令输出中的文本，以更高效地查找信息。

#### 目标

*   高效地在日志文件和配置文件中搜索文本。

#### 开始之前

作为工作站计算机上的学生用户，使用 `lab` 命令准备系统进行此练习。此命令确保所有必要的资源都可用。

```bash
[student@workstation ~]$ lab start console-regex
```

#### 操作步骤

1.  登录到 `servera` 机器上的学生账户，并切换到 root 用户。

```bash
[student@workstation ~]$ ssh student@servera
...输出省略...
[student@servera ~]$ sudo -i
[sudo] password for student: student
[root@servera ~]#
```

2.  使用 `grep` 命令查找 `postfix` 和 `postdrop` 组和用户的 GID 和 UID。为此，请使用 `rpm -q --scripts` 命令，该命令查询特定软件包的信息并显示作为安装过程的一部分所使用的脚本。

```bash
[student@servera ~]$ rpm -q --scripts postfix | grep -e 'user' -e 'group'
# 如有必要，添加用户和组
/usr/sbin/groupadd -g 90 -r postdrop 2>/dev/null
/usr/sbin/groupadd -g 89 -r postfix 2>/dev/null
/usr/sbin/groupadd -g 12 -r mail 2>/dev/null
/usr/sbin/useradd -d /var/spool/postfix -s /sbin/nologin -g postfix -G mail -M -r -u 89 postfix 2>/dev/null
setgid_group=postdrop
```

3.  修改之前的正则表达式，以显示 `/var/log/maillog` 文件中的前两条消息。在此搜索中，不需要使用脱字符 (`^`)，因为您不是在搜索行首字符。

## Response:
### 专业翻译

```bash
[root@servera ~]# grep 'postfix' /var/log/maillog | head -n 2
Apr  1 15:27:16 servera postfix/postfix-script[3121]: starting the Postfix mail system
Apr  1 15:27:16 servera postfix/master[3123]: daemon started -- version 3.5.9, configuration /etc/postfix
```

4.  查找 Postfix 服务器的队列目录名称。搜索 `/etc/postfix/main.cf` 配置文件中的所有与队列相关的信息。使用 `grep` 命令的 `-i` 选项来忽略大小写的区别。

```bash
[root@servera ~]# grep -i 'queue' /etc/postfix/main.cf
# testing.  When soft_bounce is enabled, mail will remain queued that
# The queue_directory specifies the location of the Postfix queue.
queue_directory = /var/spool/postfix
# QUEUE AND PROCESS OWNERSHIP
# The mail_owner parameter specifies the owner of the Postfix queue
# is the Sendmail-compatible mail queue listing command.
# setgid_group: The group for mail submission and queue management
```

5.  确认 Postfix 服务是否写入了 `/var/log/messages` 文件。使用 `less` 命令，然后使用斜杠字符（`/`）搜索该文件。按 `n` 键跳转到下一个匹配的条目，按 `q` 键退出 `less` 命令。

```bash
[root@servera ~]# less /var/log/messages
...输出省略...
Apr  1 15:27:15 servera systemd[1]: Starting Postfix Mail Transport Agent...
...输出省略...
Apr  1 15:27:16 servera systemd[1]: Started Postfix Mail Transport Agent.
...输出省略...
/Postfix
```

6.  使用 `ps aux` 命令确认 Postfix 服务器当前是否在运行。使用 `grep` 命令限制输出为必要的行。

```bash
[root@servera ~]# ps aux | grep postfix
root        3123  0.0  0.2  38172  4384 ?        Ss   15:27   0:00 /usr/libexec/postfix/master -w
postfix     3124  0.0  0.4  45208  8236 ?        S    15:27   0:00 pickup -l -t unix -u
postfix     3125  0.0  0.4  45252  8400 ?        S    15:27   0:00 qmgr -l -t unix -u
root        3228  0.0  0.1 221668  2288 pts/0    S+   15:55   0:00 grep --color=auto postfix
```

7.  确认 `qmgr`、`cleanup` 和 `pickup` 队列是否已正确配置。使用 `grep` 命令的 `-e` 选项来匹配同一个文件中的多个条目。`/etc/postfix/master.cf` 文件是配置文件。

```bash
[root@servera ~]# grep -e qmgr -e pickup -e cleanup /etc/postfix/master.cf
pickup
    unix  n       -       n       60      1       
cleanup   unix  n       -       n       -       0       
qmgr
 #qmgr
      unix  n       -       n       300     1       
     unix  n       -       n       300     1       
pickup
 cleanup
 qmgr
 oqmgr
```

8.  作为学生用户返回工作站机器。

```bash
[root@servera ~]# exit
logout
[student@servera ~]$ exit
logout
Connection to servera closed.
[student@workstation ~]$
```

## Response:
### 专业翻译：提升命令行生产力

在这个实验中，你将创建一个 Bash 脚本，用于从不同的主机中筛选并获取相关信息。

**学习目标**

*   创建一个 Bash 脚本并将其输出重定向到文件。
*   使用循环来简化代码。
*   使用 `grep` 和正则表达式过滤相关内容。

**开始之前** 作为工作站机器上的学生用户，使用 `lab` 命令来准备你的系统进行此练习。此命令将准备好你的环境并确保所有所需资源可用。

```bash
[student@workstation ~]$ lab start console-review
```

### 实验步骤

1.  在工作站机器上创建 `/home/student/bin/bash-lab` 脚本文件。脚本中的初始内容为 shebang 解释器指令。
2.  编辑你新创建的脚本文件，遵循以下要求，从 `servera` 和 `serverb` 主机中获取信息。这些系统使用 SSH 密钥进行身份验证，因此不需要密码。

**命令或文件**

```bash
hostname -f
echo "#####"
lscpu
echo "#####"
/etc/selinux/config
echo "#####"
/var/log/secure
echo "#####"
```

**要求的内容**

*   获取所有输出。
*   获取所有输出。
*   仅获取以 `CPU` 开头的行。
*   获取所有输出。
*   忽略空行，忽略以 `#` 开头的行。
*   获取所有输出。
*   获取所有包含 "Failed password" 的条目。
*   获取所有输出。

## Response:
### 专业翻译：保存所需信息并执行脚本

在实验中，你需要将所需的信息保存到工作站上的 `/home/student` 目录中的 `output-servera` 和 `output-serverb` 文件中。

**注意事项**

*   你可以在 `servera` 和 `serverb` 主机上使用 `sudo` 命令，无需输入密码。
*   记得使用循环来简化脚本。
*   你还可以使用多个 `grep` 命令，通过管道字符 (`|`) 连接起来。

### 实验步骤

1.  **编写脚本**
    
    *   创建一个脚本 `/home/student/bin/bash-lab`，内容包括从 `servera` 和 `serverb` 主机收集信息，并将输出分别保存到 `output-servera` 和 `output-serverb` 文件。
    *   使用 SSH 密钥验证来远程访问 `servera` 和 `serverb`，无需输入密码。
    *   使用循环简化脚本，确保多个 `grep` 命令使用管道连接。
2.  **脚本内容示例：**
    
    ```bash
    #!/bin/bash
    
    # 主机列表
    hosts=("servera" "serverb")
    
    # 循环遍历主机
    for host in "${hosts[@]}"; do
        echo "##### $host #####"
        
        # 获取 hostname -f 输出
        ssh $host "hostname -f" >> /home/student/output-$host
        
        echo "#####" >> /home/student/output-$host
        
        # 获取 lscpu 输出
        ssh $host "lscpu" | grep -i "^CPU" >> /home/student/output-$host
        
        echo "#####" >> /home/student/output-$host
        
        # 获取 /etc/selinux/config 输出，忽略空行和注释行
        ssh $host "cat /etc/selinux/config" | grep -v "^#" | grep -v "^$" >> /home/student/output-$host
        
        echo "#####" >> /home/student/output-$host
        
        # 获取 /var/log/secure 输出，过滤 "Failed password"
        ssh $host "cat /var/log/secure" | grep "Failed password" >> /home/student/output-$host
        
        echo "#####" >> /home/student/output-$host
    done
    ```
    
3.  **执行脚本**
    
    *   执行 `/home/student/bin/bash-lab` 脚本，确保所有数据正确地保存到 `output-servera` 和 `output-serverb` 文件中。
    *   使用 `cat` 命令查看输出文件内容，确保信息已正确保存。
4.  **评分与检查**
    
    *   作为工作站上的学生用户，使用 `lab` 命令来评分你的作业：
    
    ```bash
    [student@workstation ~]$ lab grade console-review
    ```
    
    *   如果有任何失败，按照反馈进行修正并重新运行该命令，直到成功为止。

### 结果

通过这些步骤，你将创建一个 Bash 脚本来收集来自 `servera` 和 `serverb` 的信息，并将其保存到工作站上的文件中。

## Response:
### 按照要求创建和编辑 Bash 脚本

#### 1\. 创建脚本文件目录和文件

首先，确保 `/home/student/bin/` 目录存在。如果没有，创建它：

```bash
[student@workstation ~]$ mkdir -p /home/student/bin
```

#### 2\. 使用 Vim 编辑脚本文件

接下来，使用 `vim` 命令创建并编辑脚本文件 `/home/student/bin/bash-lab`：

```bash
[student@workstation ~]$ vim ~/bin/bash-lab
```

在 `vim` 编辑器中，插入以下内容并保存文件：

```bash
#!/usr/bin/bash
```

*   按 `i` 进入插入模式，输入上面的内容。
*   按 `Esc` 退出插入模式。
*   输入 `:wq` 保存并退出。

#### 3\. 使脚本文件可执行

为了能够执行这个脚本，需要为其添加执行权限：

```bash
[student@workstation ~]$ chmod a+x ~/bin/bash-lab
```

#### 4\. 编辑脚本以符合要求

接下来，你需要修改脚本文件，使其符合从 `servera` 和 `serverb` 主机获取所需信息的要求。具体来说，你需要使用 SSH 远程访问这两个主机，并获取相关输出。根据任务要求，你可以编写一个脚本，通过 SSH 自动从远程主机收集信息并保存到本地文件。

如果你需要进一步的脚本帮助或如何从主机获取信息的示例，可以继续向我询问。

## Response:
### 编辑 Bash 脚本以符合要求

你需要编辑 `/home/student/bin/bash-lab` 脚本文件，按照要求获取并处理 `servera` 和 `serverb` 主机上的信息，并保存到本地文件中。下面是脚本内容的一个示例，展示了如何获取所需的信息并处理：

```bash
#!/usr/bin/bash

# Define the hosts
hosts=("servera" "serverb")

# Loop through each host
for host in "${hosts[@]}"; do
    echo "Gathering information from $host..."

    # Get the fully qualified domain name (FQDN)
    ssh "$host" "hostname -f" >> /home/student/output-"$host"

    # Separator
    echo "#####" >> /home/student/output-"$host"

    # Get CPU information
    ssh "$host" "lscpu" | grep -i '^CPU' >> /home/student/output-"$host"

    # Separator
    echo "#####" >> /home/student/output-"$host"

    # Get SELinux configuration
    ssh "$host" "cat /etc/selinux/config" >> /home/student/output-"$host"

    # Separator
    echo "#####" >> /home/student/output-"$host"

    # Get secure log entries and filter for "Failed password"
    ssh "$host" "cat /var/log/secure" | grep "Failed password" >> /home/student/output-"$host"

    # Separator
    echo "#####" >> /home/student/output-"$host"
done
```

### 脚本解析

1.  **定义主机**：通过数组 `hosts=("servera" "serverb")` 定义了两个主机。
2.  **循环遍历主机**：使用 `for` 循环遍历 `servera` 和 `serverb` 主机，执行每个 SSH 命令来获取信息。
3.  **获取信息**：
    *   使用 `hostname -f` 获取完整的主机名。
    *   使用 `lscpu` 获取 CPU 信息，并通过 `grep` 过滤出以 `CPU` 开头的行。
    *   使用 `cat /etc/selinux/config` 获取 SELinux 配置。
    *   使用 `cat /var/log/secure` 获取日志并通过 `grep "Failed password"` 过滤出失败的密码条目。
4.  **输出到文件**：每次从主机获取信息后，都将结果追加到 `/home/student/output-servera` 或 `/home/student/output-serverb` 文件中。

### 执行脚本

确保脚本文件已经保存并具有执行权限。执行脚本：

```bash
[student@workstation ~]$ ~/bin/bash-lab
```

### 完成任务后

你可以使用 `cat` 命令来查看生成的输出文件内容：

```bash
[student@workstation ~]$ cat /home/student/output-servera
[student@workstation ~]$ cat /home/student/output-serverb
```

通过这种方式，你可以将从远程主机收集到的信息保存到本地，并根据要求处理和过滤日志数据。

## Response:
你的脚本已经正确地实现了以下功能：

1.  获取 `servera` 和 `serverb` 主机的主机名（`hostname -f`）。
2.  获取 CPU 信息并仅输出以 `CPU` 开头的行（`lscpu | grep '^CPU'`）。
3.  获取并过滤掉空行和注释行的 SELinux 配置文件内容（`grep -v '^$' /etc/selinux/config | grep -v '^#'`）。
4.  获取 `secure` 日志文件中所有包含 "Failed password" 的记录（`sudo grep 'Failed password' /var/log/secure`）。

### 执行脚本

脚本已成功执行，并将数据输出到 `/home/student/output-servera` 和 `/home/student/output-serverb` 文件中。

### 输出文件内容

1.  **output-servera** 文件：
    
    ```bash
    servera.lab.example.com
    #####
    CPU op-mode(s):                  32-bit, 64-bit
    CPU(s):                          2
    CPU family:                      6
    #####
    SELINUX=enforcing
    SELINUXTYPE=targeted
    #####
    Apr  1 05:42:07 servera sshd[1275]: Failed password for invalid user operator1 from 172.25.250.9 port 42460 ssh2
    Apr  1 05:42:09 servera sshd[1277]: Failed password for invalid user sysadmin1 from 172.25.250.9 port 42462 ssh2
    Apr  1 05:42:11 servera sshd[1279]: Failed password for invalid user manager1 from 172.25.250.9 port 42464 ssh2
    #####
    ```
    
2.  **output-serverb** 文件：
    
    ```bash
    serverb.lab.example.com
    #####
    CPU op-mode(s):                  32-bit, 64-bit
    CPU(s):                          2
    CPU family:                      6
    #####
    SELINUX=enforcing SELINUXTYPE=targeted
    #####
    Apr  1 05:42:14 serverb sshd[1252]: Failed password for invalid user operator1 from 172.25.250.9 port 53494 ssh2
    Apr  1 05:42:17 serverb sshd[1257]: Failed password for invalid user sysadmin1 from 172.25.250.9 port 53496 ssh2
    Apr  1 05:42:19 serverb sshd[1259]: Failed password for invalid user manager1 from 172.25.250.9 port 53498 ssh2
    #####
    ```
    

### 接下来操作

1.  **评估任务**： 根据你的脚本执行和输出，使用以下命令进行任务评分：
    
    ```bash
    [student@workstation ~]$ lab grade console-review
    ```
    
2.  如果系统报告任何失败，请根据提示修改脚本并重新执行，直到通过测试为止。

## Response:
总结：

*   创建并执行简单的 Bash 脚本，以完成基本的管理任务。
*   使用循环在命令行和脚本中遍历一系列项。
*   使用条件结构将决策逻辑集成到 Shell 脚本中。
*   通过使用正则表达式和 `grep` 命令在日志和配置文件中搜索文本。
