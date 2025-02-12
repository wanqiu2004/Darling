/usr/bin/vmhgfs-fuse .host:/ ~/www/vod/ -o subtype=vmhgfs-fuse,allow_other
/etc/fuse.conf
ffmpeg -i input.mp4  -f hls -hls_time 10 -hls_list_size 0 index.m3u8
ffmpeg -i i.jpg -vf "crop=in_w:in_w*9/16" index.jpg
ffmpeg -i .\小七纯欲JK清纯班长\index.m3u8 -vf "select='eq(pict_type\,I)'" -vsync vfr -frame_pts true .\1\%3d.jpg
ffmpeg.exe -i .\index.mp4 -v error -f null -
ffmpeg.exe -hide_banner -i .\Natali.mp4 -filter_complex "[0:v]split=2[v360p][v1080p]; [v360p]scale=640:-1[v360p_out]; [v1080p]scale=1920:-1[v1080p_out]" -map "[v360p_out]" -f hls -hls_time 10 -hls_list_size 0 360p/index.m3u8 -map "[v1080p_out]" -f hls -hls_time 10 -hls_list_size 0 1
080p/index.m3u8
ffmpeg.exe -i .\index.mp4 -vf scale=-1:360 -f hls -hls_time 10 -hls_list_size 0 .\360p\index.m3u8

python -c "import urllib.parse; print(dir(urllib.parse))"
ip -6 addr show ens33 | grep -E -o 'inet6 [0-9a-fA-F:]+'
ip -4 addr show ens33 | grep -E -o 'inet [0-9.]+'
mailx
sudo dnf config-manager --set-disabled epel
sudo ip route add default via 192.168.1.1 dev ens33
dnf repolist all


javac --module-source-path src -d out -m com.example.helloworld
java --module-path out -m com.example.helloworld/com.example.helloworld.HelloWorldSwing
jar -c -f com.example.helloworld.jar --main-class com.example.helloworld.HelloWorldSwing -C out/com.example.helloworld .
jpackage -n HelloWorldApp --input . --main-jar com.example.helloworld.jar --main-class com.example.helloworld.HelloWorldSwing --type app-image --dest output
Compress-Archive .\HelloWorldApp\ MyApp



Let's Encrypt
sudo dnf install python3 augeas-libs
sudo python3 -m venv /opt/certbot/
sudo /opt/certbot/bin/pip install --upgrade pip
sudo /opt/certbot/bin/pip install certbot certbot-nginx
sudo ln -s /opt/certbot/bin/certbot /usr/bin/certbot
sudo certbot certonly --nginx
vim /etc/crontab
```
0 0,12 * * * root /opt/certbot/bin/python -c 'import random; import time; time.sleep(random.random() * 3600)' && sudo certbot renew -q 
```


---
HISTSIZE：该变量决定了当前 shell 会话中可以保存多少条历史命令。
HISTFILESIZE：该变量决定了历史记录文件（通常是 ~/.bash_history）中可以保存多少条命令。
HISTTIMEFORMAT：如果设置了这个变量，它会用于指定历史命令的时间戳格式。格式字符串与 strftime 函数兼容，可以自定义时间戳的输出格式。比如，可以设置为 export HISTTIMEFORMAT="%F %T "，以便显示 YYYY-MM-DD HH:MM:SS 格式的时间s。


ACL Ansible arp awk blkid certbot chmod chown chroot cron curl df diff dnf du export fdisk find firewall FreeIPA git grep head hostnamectl ip journalctl jq kill KVM logrotate lsblk lscpu lsof LVM mkdir mkfs mount mtr NetworkManager NFS nmcli nmtui parted passwd Podman ps rpm rsync Samba sed SELinux sha256sum shopt sort source ss Stratis sudo sysctl syslog systemd tail tar tcpdump tee timedatectl tr tree tuned uniq unset uptime useradd vmstat watch wc wget XFS wipefs dd which jobs env printenv wireguard dante ls ping

---
diff -q -s -c -y --suppress-common-lines -r -B 

---
tree \
  -a \                # 显示所有文件，包括隐藏文件
  -d \                # 仅列出目录
  -l \                # 跟随符号链接指向的目录
  -f \                # 显示完整路径
  -i \                # 不显示缩进线条
  -L <level> \        # 设置最大显示深度
  -P <pattern> \      # 仅列出匹配指定模式的文件
  -I <pattern> \      # 排除匹配指定模式的文件
  --filelimit <#> \   # 限制目录中条目数量，超过限制的目录不被进入
  --timefmt <fmt> \   # 自定义时间格式
  -p \                # 显示文件类型和权限
  -u \                # 显示文件的用户名或 UID
  -g \                # 显示文件的组名或 GID
  -h \                # 显示易读的文件大小（KB, MB等）
  -D \                # 显示最后修改时间
  -t \                # 按修改时间排序
  -J \                # 输出 JSON 格式
  -r \                # 反向排序
  --dirfirst \        # 先列出目录，再列出文件

---
星期一 Mon
星期二 Tue
星期三 Wed
星期四 Thu
星期五 Fri 
星期六 Sat
星期日 Sun


---
at 从标准输入或指定的文件读取命令
batch 是基于系统负载的调度，任务会在系统空闲时执行。

日期的指定必须在时间指定之后。
1. YY-MM-DD
```
at 3pm 2025-01-15
这个命令将在 2025 年 1 月 15 日的 15:00 执行任务。
```

2. 可以指定午夜（midnight）、中午（noon）或下午茶时间（teatime，4pm）

3. 相对时间：now + count time-units

4. 使用 today 和 tomorrow 可以确保任务在当天或次日执行
如果你指定了一个过去的时间，at 会立即执行任务

/etc/at.allow 和 /etc/at.deny 互斥

-f file 从指定文件中读取任务的命令 
-l 列出当前用户的 at 队列任务 
-r 删除指定的任务
-c 打印指定任务的详细内容


---

Cron 是一个在系统启动时启动的守护进程

crontab 是用于安装、删除或列出 cron 守护进程所使用的 crontab 文件的程序。
-T：测试 crontab 文件的语法，不安装该文件。
-l：列出当前用户的 crontab。
-r：删除当前用户的 crontab。
-e：使用 VISUAL 或 EDITOR 环境变量指定的编辑器编辑当前用户的 crontab。编辑完后，退出编辑器会自动安装修改过的 crontab。



一个有效的 crontab 行要么是环境设置，要么是 cron 命令。环境设置的格式如下：
`name = value`

Cron 命令的格式每行包含五个时间和日期字段，接着是一个用户名（如果是系统 crontab 文件的话），然后是一个命令。
cron 每分钟检查一次 cron 条目。


1. 允许使用数字范围。范围由两个用连字符（-）分隔的数字组成。指定的范围是包含两个端点的。例如，8-11 表示在 8、9、10 和 11
2. 随机化执行时间范围由两个数字用波浪号（~）分隔。例如，6~15 在“分钟”字段中表示从 6 到 15 分钟之间随机选择一个分钟。该范围是包含上下限的
3. 列表允许指定一组数字或范围，用逗号分隔。例如，"1,2,5,9" 或 "0-4,8-12"。
4. 步进值可以与范围一起使用。在范围后跟 /数字 会指定在该范围内按指定的数字跳过。例如，"0-23/2" 可以用于“小时”字段，表示每隔一小时执行一次命令步进值也可以在星号（*）后使用，例如，"*/2" 表示每两小时执行一次。
5. 可以在“月份”和“星期几”字段中使用名称。使用特定日或月的前三个字母（大小写不敏感）。也可以使用名称的范围和列表。例如，"mon,wed,fri" 或 "jan-mar"。

crontab 支持以下特殊时间规格（以 @ 开头的别名），可代替常规的时间字段定义：

@reboot：系统重启后执行一次。
@yearly：每年执行一次，等同于 0 0 1 1 *。
@annually：每年执行一次，等同于 0 0 1 1 *。
@monthly：每月执行一次，等同于 0 0 1 * *。
@weekly：每周执行一次，等同于 0 0 * * 0。
@daily：每天执行一次，等同于 0 0 * * *。
@hourly：每小时执行一次，等同于 0 * * * *。



/etc/cron.allow：允许使用 crontab 的用户列表。
/etc/cron.deny：禁止使用 crontab 的用户列表。


/etc/crontab：系统的主 crontab 文件，定义了系统级的定时任务。
/var/spool/cron/：用户定义的 crontab 文件存储目录。
/etc/cron.d/：用于存储系统级的 crontab 文件。


crontab -T file -e -l -r 

---


# 定位并准确解读系统事件日志，以便进行故障排除。

## Describe System Log Architecture

1. 日志有什么用？对于我有什么用？谁会用？普遍性？
```
日志用于审计系统和排除故障。
RHEL 使用基于 Syslog 协议的标准日志系统来记录系统消息。
许多程序利用该日志系统记录事件
```


2. EL使用什么工具实现？日志存在哪里？是否重启清零？所有程序都使用吗？
```
systemd-journald 和 rsyslog 服务在EL中处理 syslog 消息。


systemd-journald 服务是操作系统事件日志架构的核心。它从多个来源收集事件消息：
- 系统内核
- 启动过程的早期阶段的输出
- 守护进程的标准输出和标准错误
- Syslog 事件
systemd-journald 服务将日志重构为标准格式，并将它们写入结构化、索引化的系统日志。
默认情况下，这些日志存储内存


rsyslog 是一个日志管理服务，它从systemd-journald中接收syslog消息，并对其进行处理。
将 syslog 消息分类，并将其写入位于 /var/log 目录下的日志文件重启后依然存在


/var/log 目录还包含来自系统上其他服务的日志文件
| 日志文件            | 存储的消息类型                                                                 |
|---------------------|-------------------------------------------------------------------------------|
| `/var/log/messages`  | 大多数 syslog 消息都记录在这里。例外情况包括关于身份验证和邮件处理、计划任务执行以及纯粹的调试相关消息。 |
| `/var/log/secure`    | 记录关于安全性和身份验证事件的 syslog 消息。                                      |
| `/var/log/maillog`   | 记录关于邮件服务器的 syslog 消息。                                               |
| `/var/log/cron`      | 记录关于计划任务执行的 syslog 消息。                                             |
| `/var/log/boot.log`  | 记录关于系统启动的非 syslog 控制台消息。                                         |


有些应用程序不使用 syslog 服务来管理它们的日志消息。例如，Apache Web 服务器将日志消息保存到 /var/log 目录下的一个子目录中。



## Review Syslog Files

1. syslog消息是如何被处理的？

程序将事件记录到系统中。每条日志消息都会根据设施（即产生消息的子系统）和优先级（即消息的严重性）进行分类。

rsyslog使用设施和优先级来确定如何处理它们。
规则在 /etc/rsyslog.conf 文件和/etc/rsyslog.d目录下
软件可以通过在 /etc/rsyslog.d 目录中安装适当的文件，轻松地添加规则。

3. 什么是设施？什么是优先级？
| 代码 | 设施         | 设施描述             |
| ---- | ------------ | -------------------- |
| 0    | kern         | 内核消息             |
| 1    | user         | 用户级消息           |
| 2    | mail         | 邮件系统消息         |
| 3    | daemon       | 系统守护进程消息     |
| 4    | auth         | 身份验证与安全消息   |
| 5    | syslog       | 内部 syslog 消息      |
| 6    | lpr          | 打印机消息           |
| 7    | news         | 网络新闻消息         |
| 8    | uucp         | UUCP 协议消息        |
| 9    | cron         | 时钟守护进程消息     |
| 10   | authpriv     | 非系统授权消息       |
| 11   | ftp          | FTP 协议消息         |
| 16-23| local0 到 local7 | 自定义本地消息   |


| 代码 | 优先级 | 优先级描述           |
| ---- | ------ | -------------------- |
| 0    | emerg  | 系统不可用           |
| 1    | alert  | 必须立即采取行动     |
| 2    | crit   | 严重条件             |
| 3    | err    | 非致命错误           |
| 4    | warning| 警告条件             |
| 5    | notice | 正常但重要的事件     |
| 6    | info   | 信息性事件           |
| 7    | debug  | 调试级别的消息       |


3. 配置行长什么样子？什么含义？

每行的左侧表示规则匹配的 syslog 消息的设施和优先级，右侧表示将日志消息保存到哪个文件
`authpriv.*                  /var/log/secure`
会将发送到 authpriv 设施的所有优先级的消息记录到 /var/log/secure 文件中
更加具体的是：
```
#### 规则 ####

# 将所有内核消息记录到控制台。
# 记录其他信息会让屏幕变得杂乱。
#kern.*                                                 /dev/console

# 记录所有级别为 info 或更高级别的消息（除了邮件相关消息）。
# 不记录私人身份验证消息！
*.info;mail.none;authpriv.none;cron.none                /var/log/messages

# `authpriv` 文件具有受限访问权限。
authpriv.*                                              /var/log/secure

# 将所有邮件消息集中记录到一个地方。
mail.*                                                  -/var/log/maillog

# 记录 cron 相关的消息
cron.*                                                  /var/log/cron

# 所有用户都会收到紧急消息
.emerg                                                 :omusrmsg:

# 将新闻错误消息（优先级为 crit 及以上）保存到特定文件。
uucp,news.crit                                          /var/log/spooler

# 将启动消息也保存到 boot.log 文件
local7.*                                                /var/log/boot.log
```

## Log File Rotation

1. 什么是日志轮换？有什么用？会怎么做？cron不好吗？

防止文件占用过多的 /var/log 目录空间。
会重命名，并附加一个表示轮换日期的扩展名。
logrotate命令经过通常四周的轮换后，最旧的日志文件会被丢弃
一个定时任务每天运行 logrotate 命令，检查是否有日志文件需要轮换。
logrotate也可以在日志文件达到特定大小时进行轮换。


## Analyze a Syslog Entry

1. 这日志一行什么意思啊？我要最新的！
syslog通常按时间顺序排列，最旧的消息在日志文件的开头，最新的消息位于文件的末尾。
/var/log/secure 的一行是这样的：
`Mar 20 20:11:48 localhost sshd[1433]: Failed password for student from 172.25.0.10 port 59344 ssh2`

tail -f /path/to/file 命令输出指定文件的最后十行，并继续输出文件中新写入的行。
	


## Send Syslog Messages Manually

1. 非常好，我要自己发送一个syslog！

logger 命令用于将消息发送到 rsyslog 服务。默认情况下，它将消息发送到 user 类型，优先级为 notice
这对于测试对 rsyslog 服务配置所做的更改非常有用。

请执行以下 logger 命令：
`[root@host ~]# logger -p local7.notice "Log entry created on host"`


---

## Guided Exercise
在/etc/rsyslog.d/目录内创建my.conf文件
写入*.debug /var/log/message-debug这一行
systenctm restart rsyslog.service
logger -p user.debug '😁'
---

## 查找并解释系统日志中的条目，

1. 我该如何找到我要的日志？

systemd-journald 服务将日志数据存储在一个名为 journal 的结构化、索引化的二进制文件中。

在EL中，基于内存的 /run/log 目录默认存储系统日志。当系统关闭时，/run/log 目录的内容会丢失。
要获取日志消息，可以使用 journalctl 命令。可以使用该命令查看日志中的所有消息，或者搜索特定的事件。

会突出显示重要的日志信息；优先级为 notice 或 warning 的消息会以粗体显示，而优先级为 error 或更高的消息则会以红色显示。

默认情况下，journalctl 命令的 -n 选项会显示最后 10 条日志记录。
类似于 tail 命令，journalctl 命令的 -f 选项会输出系统日志的最后 10 行，并继续输出新添加的日志条目。
journalctl 命令的 -p 选项允许你显示指定优先级
（可以用名称或数字表示）及其以上的日志条目。

显示指定 systemd 单元的日志条目。 journalctl -u sshd.service

可以将输出限制为特定的时间范围。--since 和 --until 选项。这两个选项都需要以 "YYYY-MM-DD hh:mm:ss" 格式的时间参数
还可以指定从相对当前时间起的所有条目


---
## Guided Exercise

搜索系统日志，记录符合特定标准的事件条目。

使用 journalctl 命令的 -p warning 选项，显示机器上警告级别及以上的日志事件。
journalctl -p warning
显示过去 10 分钟内从当前时间起在 servera 机器上记录的所有日志事件。
journalctl --since "-10min"
显示从今天早上 09:00:00 以来来自 sshd 服务的所有日志事件。
journalctl --since 9:00:00 _SYSTEMD_UNIT="sshd.service"

---


## 不管不管，我要将journal的日志记录到磁盘

/etc/systemd/journald.conf 文件中的 Storage 参数定义了系统日志是否以易失方式存储（即重启后丢失）或以持久方式存储（即重启后保留）。

- persistent：将日志存储在 /var/log/journal 目录中，重启后日志仍然存在。如果 /var/log/journal 目录不存在，systemd-journald 服务将创建该目录。
- volatile：将日志存储在易失的 /run/log/journal 目录中。由于 /run 文件系统是临时的，仅在运行时内存中存在，因此其中的数据，包括系统日志，在重启后不会保留。
- auto：如果 /var/log/journal 目录存在，systemd-journald 服务将使用持久存储；如果该目录不存在，则使用易失存储。如果未设置 Storage 参数，则默认使用此选项。

- none：不使用任何存储。系统将丢弃所有日志，但仍然可以转发日志。
然而，即使是持久日志，系统也不会永久保存所有数据。日志具有内置的日志轮换机制，
此外，系统不会允许日志文件变得比它们所在文件系统的 10% 还大，或者文件系统剩余空间少于 15%。

在 /etc/systemd/journald.conf 文件中取消注释 Storage=auto 行，并将 Storage 参数设置为 persistent 值。
sudo systemctl restart systemd-journald.service



## Maintain Accurate Time

计算机可以从公共的NTP服务（例如NTP Pool Project）获取准确的时间信息，另一种选择是与高质量的硬件时钟同步，以为本地客户端提供准确的时间。
timedatectl 命令显示当前系统的时间相关设置概览，包括当前时间、时区和NTP同步设置。

---

#  Archive and Transfer Files

##  Create Archives from the Command Line

存档是一个包含多个文件的常规文件或设备文件。设备文件可以是磁带驱动器、闪存驱动器或其他可移动媒体。
存档文件用于创建可管理的个人备份，或者在其他方法（如 rsync）不可用或更复杂时简化通过网络传输一组文件的任务。


执行 tar 操作时需要以下命令之一：

-c 或 --create：创建存档文件。
-t 或 --list：列出存档的内容。
-x 或 --extract：提取存档。
-f 或 --file：后跟存档文件名，用于创建或打开存档文件。
-p 或 --preserve-permissions：提取文件时保留原文件的权限。

以下是 tar 命令中的压缩选项，用于选择压缩算法：

-a 或 --auto-compress：根据存档文件的后缀自动确定使用的压缩算法。
-z 或 --gzip：使用 gzip 压缩算法，生成 .tar.gz 后缀的文件。
-j 或 --bzip2：使用 bzip2 压缩算法，生成 .tar.bz2 后缀的文件。
-J 或 --xz：使用 xz 压缩算法，生成 .tar.xz 后缀的文件。
-Z 或 --compress：使用 LZ 变体算法，生成 .tar.Z 后缀的文件。


要使用 tar 命令创建存档，可以使用 -c 和 -f 选项，首先指定存档文件名，然后列出要包含在存档中的文件和目录。
`tar -cf mybackup.tar myapp1.log myapp2.log myapp3.log`
默认情况下，tar 会从绝对路径名中去掉前导的 / 字符，以便将文件存储为相对路径。
这种做法更安全，因为提取绝对路径时会覆盖现有文件。使用相对路径存档的文件，可以提取到新目录中而不会覆盖已有文件。

用户必须对所存档的目标文件具有读取权限。存档中不会包含用户无法读取的文件，也不会包含用户没有读取和执行权限的目录。
存档文件中默认不会保留扩展文件属性，例如访问控制列表（ACL）和 SELinux 文件上下文。使用 --xattrs 和 --selinux 选项可以将扩展属性包括在内。

## List Archive Contents

使用 tar 命令的 -t 选项可以列出指定存档文件中的文件名，并使用 -f 选项指定存档文件。文件列表会使用相对路径名
`tar -tf /root/etc-backup.tar`

为了避免覆盖现有文件，建议将 tar 存档提取到一个空目录中。
如果 root 用户提取存档，提取的文件将保留原始的用户和组所有权。
如果是普通用户提取文件，文件的所有权将归该用户。

以下命令列出 /root/etc.tar 存档的内容，然后将其提取到 /root/etcbackup 目录：
tar -tf /root/etc.tar
tar -xf /root/etc.tar

## Create a Compressed Archive

tar 命令支持以下压缩方法，及其他一些方法：

- gzip 压缩是经典的、最快的压缩方法，并且在各个平台上广泛支持。`tar -czf /root/etcbackup.tar.gz /etc`
- bzip2 压缩创建的存档更小，但比 gzip 的支持范围窄。`tar -cjf /root/logbackup.tar.bz2 /var/log`
- xz 压缩是更新的压缩方法，提供最佳的压缩比。`tar -cJf /root/sshconfig.tar.xz /etc/ssh`


## Extract Compressed Archive Contents

tar 命令可以自动识别使用的压缩类型，因此无需指定压缩选项。如果指定了错误的压缩类型，tar 会报告所选的压缩类型与文件类型不匹配。
gzip、bzip2、xz 和 compress 等算法也作为独立命令存在，可以用于压缩单个文件，但不允许将多个文件（如整个目录）压缩成一个文件。
如果只想解压一个压缩文件或压缩存档文件而不提取其中的内容，可以使用独立的解压命令，如 gunzip、bunzip2、unxz 和 uncompress。

gzip 和 xz 命令提供了 -l 选项，可以查看压缩文件的未压缩大小。使用此选项可以在解压前检查是否有足够的空间。
例如，使用 gzip 命令查看 .tar.gz 文件的未压缩大小：
`gzip -l file.tar.gz`


















## 3. 调优系统性能



## 10 配置和保护 SSH
# ? 身份验证代理转发，例如 ssh-agent。
**SSH2 的结构 分为三个层次**：
- 传输层 transport layer：负责密钥交换、算法协商和加密保护，确保数据的完整性和机密性。
- 用户身份验证层 user authentication layer：在已建立的安全连接上进行用户认证，支持多种身份验证方式（如密码认证、公钥认证等）。
- 连接层 connection layer：在已认证的连接上复用多个并发的通道，并提供登录会话的隧道功能和 TCP 转发。



Open SSH有这些应用及配置文件
ssh(1) — 基本的类似 rlogin/rsh 的客户端程序
sshd(8) — 允许登录的守护进程
ssh_config(5) — 客户端配置文件
sshd_config(5) — 守护进程配置文件


sftp(1) — 类似 FTP 的程序，通过 SSH1 和 SSH2 协议工作
scp(1) — 文件复制程序，类似 rcp
ssh-keygen(1) — 密钥生成工具
sftp-server(8) — SFTP 服务器子系统（由 sshd 自动启动）
ssh-keyscan(1) — 从多个主机收集公钥的工具
ssh-keysign(8) — 用于基于主机的身份验证的辅助程序



OpenSSH 做了一些增强和扩展，提供了一些额外的功能，
提供了 SFTP 文件传输协议，支持文件的安全传输。
基于 SSH 的虚拟专用网络SSH 支持使用 tun(4) 网络伪设备进行虚拟专用网络（VPN）隧道，使两个网络可以安全地连接。
充当 SOCKS 代理服务器。
端口转发   隧道和虚拟网络接口




1. ssh（SSH 客户端）是一个用于登录远程计算机并在远程计算机上执行命令的程序。

目标可以通过 [user@]hostname 或者形如 ssh://[user@]hostname[:port] 的 URI 指定
如果指定了命令，它将在远程主机上执行，而不是登录到默认的 shell。

身份验证：公钥 证书 密码

第一次连接到服务器时，ssh客户端工具会向你展示服务器公钥的指纹（除非你禁用 你可以使用 ssh-keygen 工具查看指纹：ssh-keygen -l -f /etc/ssh/ssh_host_rsa_key


绑定地址
端口转发
-D [bind_address:]port: 动态端口转发，使 ssh 充当 SOCKS 服务器。当连接到此端口时，会通过安全的 SSH 通道转发连接。
-L [bind_address:]port:host:hostport: 本地端口转发，将连接到本地 TCP 或 Unix 套接字的请求转发到远程主机和端口。
指定一个 替代配置文件指定一个 替代配置文件-F configfile
-i identity_file: 指定用于公钥身份验证的 私钥文件。默认使用 ~/.ssh/id_rsa、~/.ssh/id_ecdsa、~/.ssh/id_ed25519
不执行远程命令只需要端口转发-N
-o option 选项允许你在命令行中指定 配置文件格式 的选项。
-p port
指定要连接的远程主机端口。
-Q query_option
查询支持的算法，适用于以下功能：

cipher（支持的对称加密算法）
cipher-auth（支持的对称加密算法，支持认证加密）
help（用于 -Q 标志的支持查询项）
mac（支持的消息完整性码算法）
kex（密钥交换算法）
key（支持的密钥类型）
key-ca-sign（有效的 CA 签名算法，用于证书）
key-cert（证书密钥类型）
key-plain（非证书密钥类型）
key-sig（所有密钥类型和签名算法）
protocol-version（支持的 SSH 协议版本）
sig（支持的签名算法）


-R [bind_address:]port:host:hostport
指定将连接从远程（服务器）主机上的给定 TCP 端口或 UNIX 套接字转发到本地。该选项用于创建反向端口转发。
-v
详细模式。
-W host:port
请求将客户端的标准输入和输出通过安全通道转发到 host 上的 port。此选项隐式启用 -N、-T、ExitOnForwardFailure 和 ClearAllForwardings，尽管这些选项可以在配置文件或通过 -o 命令行选项覆盖。
-w local_tun[:remote_tun]
请求使用指定的 tun(4) 设备在客户端（local_tun）和服务器（remote_tun）之间转发隧道设备。如果未指定 remote_tun，默认值为 "any"。

请注意，Tunnel 配置指令未设置时，将默认使用 "point-to-point" 隧道模式。如果需要不同的隧道转发模式，请在 -w 之前指定。




3. ssh-keygen 用于生成、管理和转换 SSH 身份验证密钥。
通过 -t 选项可以指定要生成的密钥类型。如果没有任何参数调用，ssh-keygen 将生成一个 Ed25519 密钥。
运行一次 ssh-keygen 来创建认证密钥，存储在 ~/.ssh/id_ecdsa、~/.ssh/id_ecdsa_sk、~/.ssh/id_ed25519、~/.ssh/id_ed25519_sk 或 ~/.ssh/id_rsa 文件中。
ssh-keygen 会生成密钥并询问保存私钥的文件名。公钥会保存为相同名称的文件，但文件名后会加上 .pub 后缀。该程序还会询问一个密码短语。
密码短语可以为空，表示没有密码（主机密钥必须没有密码），也可以是任意长度的字符串。密码短语类似于密码，
但它可以是一个包含多个单词、标点符号、数字、空格或任何字符的短语。好的密码短语通常长 10-30 个字符，
-p 选项用于 更改现有私钥的密码短语

-b bits
指定要生成的密钥的位数。对于 RSA 密钥，最小大小为 1024 位，默认是 3072 位。一般认为 3072 位足够了。
对于 ECDSA 密钥，-b 标志通过选择三种椭圆曲线尺寸之一（256、384 或 521 位）来确定密钥长度。
尝试使用这些三种以外的位长度会失败。ECDSA-SK、Ed25519 和 Ed25519-SK 密钥有固定长度，-b 标志会被忽略。

-C comment
提供一个新的注释。

-c
请求更改私钥和公钥文件中的注释。程序将提示输入包含私钥的文件、如果密钥有密码则输入密码，以及新注释。

-E fingerprint_hash
指定显示密钥指纹时使用的哈希算法。有效选项为：“md5”和“sha256”。默认值是“sha256”。

-f filename
指定密钥文件的文件名。

-H
哈希 known_hosts 文件。将指定文件中的所有主机名和地址替换为哈希表示；原始内容会移动到以 .old 结尾的文件中。
这些哈希值仍然可以被 ssh 和 sshd 正常使用，但如果文件内容被泄露，则不会揭示身份信息。
此选项不会修改已存在的哈希主机名，因此在包含哈希和非哈希名称的文件中使用是安全的。

-l
显示指定公钥文件的指纹。ssh-keygen 会尝试找到匹配的公钥文件并打印其指纹。如果与 -v 一起使用，则会提供密钥的 ASCII 艺术表示。


-F hostname | [hostname]:port
在 known_hosts 文件中搜索指定的主机名（可选端口号），列出找到的所有实例。此选项用于查找已哈希的主机名或地址，也可以与 -H 选项结合使用，以哈希格式打印找到的密钥。

-l
此选项用于显示指定公钥文件的指纹。ssh-keygen 会尝试找到指定公钥文件，并显示其指纹。指纹是一种通过哈希算法生成的简短的、唯一的标识符，用来验证公钥的身份。
通常，指纹以十六进制形式显示，并且可以帮助你在没有查看整个公钥的情况下，快速确认公钥的真实性
与 -v 一起使用，则会提供密钥的 ASCII 艺术表示。

-t key_type：指定要生成的密钥类型（如 ecdsa、ed25519、rsa 等）。
-V validity_interval：定义证书的有效期，适用于签名密钥时。
-v：启用详细模式，用于调试。
-Y sign：使用 SSH 密钥对文件或数据进行签名。
-Y verify：验证由 SSH 密钥签名的文件或数据的签名。

-P passphrase：输入 旧密码，用于需要验证旧密码的操作（如修改密码）。
-p：交互式地输入旧密码并设置新密码，适用于手动更改密码的情况。
-N new_passphrase：直接指定 新密码，无需输入旧密码，通常用于脚本或自动化任务中。


ssh-keygen 支持签署密钥以生成可用于用户或主机身份验证的证书。










一些配置文件是：
              ~/.ssh/默认存放用户配置和认证信息的目录。这里包含 SSH 公钥、私钥、已知主机密钥等文件。建议目录的权限是用户可读、可写、可执行，其他人不可访问。
        ~/.ssh/authorized_keys列出可以用来登录用户账户的公钥。该文件中列出的公钥可以是 ECDSA、Ed25519、RSA 等类型的密钥。要有严格的权限控制（通常为 600）
        ~/.ssh/config用户级别的 SSH 配置文件，用于指定 SSH 客户端连接时的行为。文件格式和配置选项在 ssh_config(5) 中有详细说明。
        ~/.ssh/environment
        ~/.ssh/id_ecdsa, ~/.ssh/id_ed25519, ~/.ssh/id_rsa用户的私钥文件，用于身份验证。这些文件包含敏感数据，必须对用户可读、可写、可执行，但不能对其他人可访问。
        ~/.ssh/id_ecdsa.pub, ~/.ssh/id_ed25519.pub, ~/.ssh/id_rsa.pub用户的公钥文件，用于身份验证。这些文件不是敏感信息，可以（但不强制）对所有人可读。
        ~/.ssh/known_hosts存储用户已经登录过的主机的公钥。它列出了所有已经连接的主机密钥，且这些主机密钥尚未存在于系统范围的已知主机列表中。
        ~/.ssh/rc登录时由 SSH 执行的命令文件，命令会在用户的 shell 或命令启动之前执行。可以用于执行一些定制操作。

        /etc/ssh/ssh_config系统范围的 SSH 配置文件，定义了 SSH 客户端的全局行为。
        /etc/ssh/ssh_known_hosts存储系统范围内已知的所有主机密钥。系统管理员应为组织中的所有机器准备这个文件，它应该是所有人可读的。
        /etc/ssh/sshrc








一些算法是：
RSA DSA ECDSA Ed25519

