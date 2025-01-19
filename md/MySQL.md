MySQL 软件提供了一个快速、多线程、多用户且功能强大的 SQL（结构化查询语言）数据库服务器。MySQL 服务器旨在满足关键任务、重负载生产系统的需求，同时也适合嵌入式的大规模分发软件。
MySQL 软件采用双重授权模式。用户可以选择以开源产品的形式，根据 GNU 通用公共许可证使用 MySQL 软件，或者购买 Oracle 提供的标准商业许可证。

- 什么是 MySQL?
MySQL 是目前最流行的开源 SQL 数据库管理系统，由 Oracle 公司开发、分发并提供支持。
MySQL 是一种数据库管理系统
数据库是结构化的数据集合，为了添加、访问和处理存储在计算机数据库中的数据，您需要一个数据库管理系统
MySQL 数据库是关系型的
关系型数据库将数据存储在独立的表中，而不是将所有数据放入一个大型存储库。
“MySQL”中的 SQL 是“结构化查询语言”（Structured Query Language）的缩写
SQL 由 ANSI/ISO SQL 标准定义。自 1986 年以来，SQL 标准不断演进，并存在多个版本。
与其他应用（如 Web 服务器）一起运行，占用极少的资源。
MySQL 数据库软件是一个客户端/服务器系统，包含一个支持不同后端的多线程 SQL 服务器、多个客户端程序和库、管理工具以及广泛的应用程序编程接口（API）。

HeatWave 是一个完全托管的数据库服务，由 HeatWave 内存查询加速器提供支持。这是唯一一个将事务、跨数据仓库和数据湖的实时分析以及机器学习集成到一个 MySQL 数据库中的云服务，无需 ETL 复制的复杂性、延迟、风险和成本。它适用于 OCI、AWS 和 Azure。

使用 C 和 C++ 编写。
使用 CMake 配置以提高可移植性。
支持多线程和多核 CPU。
提供特有的 SHOW 语句和 INFORMATION_SCHEMA 数据库以查询元信息。
支持大规模数据库（例如，50 亿行记录和 20 万个表）。
单表最多支持 64 个索引，索引列最多 16 列。
支持多种连接协议（如 TCP/IP、命名管道和 Unix 域套接字）。
提供多语言错误信息。


MySQL 的名字来源于联合创始人 Monty Widenius 的女儿 My。
MySQL 的海豚标志（我们的 Logo）的名字是 “Sakila”，它是通过我们举办的“给海豚取名”竞赛中，从用户建议的众多名字中挑选出来的。


MySQL 的发布模式分为两个主要版本：长期支持版（LTS，Long-Term Support） 和 创新版（Innovation）。无论是 LTS 还是创新版，都包含了漏洞修复和安全补丁，并且都被视为适合生产环境的高质量版本。


![](https://dev.mysql.com/doc/refman/8.4/en/images/mysql-lts-innovation-versioning-graph.png)


LTS版遵循 Oracle 生命周期支持政策：
5 年优质支持（Premier Support）
3 年扩展支持（Extended Support）


MySQL 连接器
每个连接器只发布一个版本号（最新版本），但保持与所有支持的 MySQL Server 版本兼容。
例如：MySQL Connector/Python 9.0.0 与 MySQL Server 8.0、8.4 和 9.0 都兼容。


MySQL 服务器最初是为中型数据库（每个表大约 100MB，包含 1000 万到 1 亿行）设计的，适用于小型计算机系统。如今，MySQL 服务器能够处理 TB 级别的数据库。


MySQL 服务器可以在不同的 SQL 模式下运行，并且可以根据 sql_mode 系统变量的值，为不同的客户端应用不同的模式。

---

# 安装 MySQL
使用通用二进制文件在 Unix/Linux 上安装 MySQL
在 Microsoft Windows 上安装 MySQL
在 Linux 上安装 MySQL
安装后的设置与测试


**如何获取 MySQL**
https://dev.mysql.com/downloads/

**使用 MD5 校验**

**安装 MySQL 时的目录布局，包括如何配置安装路径和 MySQL 文件的存放位置。**
对于 Windows 上的 MySQL 8.0，使用 MySQL 安装程序进行安装时，默认的安装目录是 C:\Program Files\MySQL\MySQL Server 8.0。
所有文件都位于此父目录下，使用下表所示的结构。
| 目录                                      | 目录内容                                           | 备注                                                       |
|-----------------------------------------|--------------------------------------------------|----------------------------------------------------------|
| bin                                     | mysqld 服务器、客户端和实用程序                    |                                                          |
| %PROGRAMDATA%\MySQL\MySQL Server 8.0\  | 日志文件、数据库                                    | Windows 系统变量 `%PROGRAMDATA%` 默认为 `C:\ProgramData`。 |
| docs                                    | 发布文档                                           | 使用 MySQL 安装程序时，使用“修改”操作选择此可选文件夹。      |
| include                                 | 包含（头文件）                                     |                                                          |
| lib                                     | 库文件                                             |                                                          |
| share                                   | 各种支持文件，包括错误消息、字符集文件、示例配置文件、用于数据库安装的 SQL 文件 |                                                          |

对于Linux：
安装还会在系统上创建一个名为 mysql 的用户和组。文件和资源被创建在系统目录下
MySQL 在安装结束后不会自动启动。


RPM 包的完整名称具有以下语法：
packagename-version-distribution-arch.rpm
distribution 和 arch 值表示构建该包的 Linux 发行版和处理器类型。

| 发行版值       | 适用平台                                                           |
|--------------|------------------------------------------------------------------|
| el{version}  | EL6 (8.0), EL7, EL8 和 EL9 基于平台（例如，Oracle Linux, Red Hat Enterprise Linux 和 CentOS） |
| fc{version}  | Fedora 39, 40 和 41                                               |
| sl5          | SUSE Linux Enterprise Server 15                                    |

| 文件或资源                                       | 位置                                                            |
|------------------------------------------------|---------------------------------------------------------------|
| 客户端程序和脚本                                   | /usr/bin                                                       |
| mysqld 服务器                                    | /usr/sbin                                                      |
| 配置文件                                          | /etc/my.cnf                                                    |
| 数据目录                                          | /var/lib/mysql                                                 |
| 错误日志文件                                      | 对于 RHEL、Oracle Linux、CentOS 或 Fedora 平台：/var/log/mysqld.log ；对于 SLES：/var/log/mysql/mysqld.log |
| secure_file_priv 的值                             | /var/lib/mysql-files                                           |
| System V 初始化脚本                               | 对于 RHEL、Oracle Linux、CentOS 或 Fedora 平台：/etc/init.d/mysqld；对于 SLES：/etc/init.d/mysql |
| systemd 服务                                      | 对于 RHEL、Oracle Linux、CentOS 或 Fedora 平台：mysqld；对于 SLES：mysql |
| PID 文件                                          | /var/run/mysql/mysqld.pid                                      |
| Socket                                            | /var/lib/mysql/mysql.sock                                      |
| 密钥环目录                                        | /var/lib/mysql-keyring                                         |
| Unix 手册页                                        | /usr/share/man                                                 |
| 包含（头文件）                                    | /usr/include/mysql                                             |
| 库                                               | /usr/lib/mysql                                                 |
| 各种支持文件（例如，错误消息和字符集文件）         | /usr/share/mysql                                                |


---
**重点**
从 MySQL Yum 仓库页面下载 RPM 包
选择并下载适用于您平台的发行版包，文件格式为：mysql84-community-release-{platform}-{version-number}.noarch.rpm
下面命令将 MySQL Yum 仓库添加到系统的仓库列表中，并下载 GnuPG 密钥以检查软件包的完整性。
`sudo yum localinstall mysql84-community-release-{platform}-{version-number}.noarch.rpm`
查看是否添加成功：
`yum repolist enabled | grep mysql.*-community`
安装：
`sudo yum install mysql-community-server`
查看安装成功：
`mysql --version`
为了确保 MySQL 安全，可以运行以下命令进行安全配置并设置 root 密码：
`sudo mysql_secure_installation`
- root 用户的密码
- 匿名用户
- root 用户'localhost' 连接
- 'test' 的数据库
- 重新加载权限表

在服务器初次启动时，如果服务器的数据目录为空，将发生以下情况：
服务器初始化。
SSL 证书和密钥文件在数据目录中生成。
安装并启用 validate_password。
创建了超级用户账户 root@localhost，并为超级用户设置了密码，该密码记录在错误日志文件中。要查看它，请使用以下命令：
```
$> sudo grep 'temporary password' /var/log/mysqld.log
尽快更改 root 密码，使用生成的临时密码登录并为超级用户账户设置自定义密码：
$> mysql -uroot -p
mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass4!';
```



# 13 数据类型
- 数值类型
- 日期与时间类型
- 字符串（字符与字节）类型
- 空间类型
- JSON 数据类型

SERIAL 是 BIGINT UNSIGNED NOT NULL AUTO_INCREMENT UNIQUE 的别名。

在定义整数列时，SERIAL DEFAULT VALUE 是 NOT NULL AUTO_INCREMENT UNIQUE 的别名。

MySQL 支持的整数类型的存储要求和取值范围
|类型|	存储（字节）|	带符号最小值	|无符号最小值	|带符号最大值	|无符号最大值
|---|---|---|---|---|---|
TINYINT	1	-128	0	127	255
SMALLINT	2	-32768	0	32767	65535
MEDIUMINT	3	-8388608	0	8388607	16777215
INT	4	-2147483648	0	2147483647	4294967295
BIGINT	8	-263	0	263-1	264-1


DECIMAL(5,2)5 是精度，2 是小数位数。可以存储的值范围是从 -999.99 到 999.99。语法 DECIMAL(M) 等价于 DECIMAL(M,0)

FLOAT 和 DOUBLE 类型用于表示近似数值数据。MySQL 使用四个字节存储单精度（FLOAT）值，使用八个字节存储双精度（DOUBLE）值。

BIT(M) 类型允许存储 M 位的值，其中 M 的范围为 1 到 64。
要指定位值，可以使用 b'value' 的表示法。value 是一个由零和一组成的二进制值。
默认左侧补零


当 MySQL 在数值列中存储一个超出该列数据类型允许范围的值时，结果取决于当时启用的 SQL 模式：
如果启用了严格的 SQL 模式（strict SQL mode），MySQL 会拒绝超出范围的值并报错，插入操作会失败，这符合 SQL 标准。
如果没有启用严格模式，MySQL 会将值修剪到该列数据类型范围的适当端点，并存储修剪后的结果。

SET sql_mode = 'TRADITIONAL';


SET sql_mode = '';


## 数值类型： 5种INT DECIMAL FLOAT DOUBLE BIT 

# 日期
MySQL 支持多种日期和时间数据类型，分别用于表示不同的时间值，包括 DATE、TIME、DATETIME、TIMESTAMP 和 YEAR。每种数据类型都有其有效值的范围，并且都有一个“零值”，可以在指定无效值时使用。STRICT模式：当启用严格 SQL 模式时，MySQL 会严格检查日期和时间值是否有效，并拒绝无效日期。MySQL 从 5.6.4 版本开始，支持将时间类型值的精度扩展到毫秒。自动初始化自动更新MySQL 允许存储 '0000-00-00' 作为“零值日期”。这种情况可能比使用 NULL 值更方便，因为它占用的空间更少，且便于索引。在某些场景下，使用 ZERO 日期比 NULL 更有优势。STRICT模式：当启用严格 SQL 模式时，MySQL 会严格检查日期和时间值是否有效，并拒绝无效日期。

DATE

仅表示日期，格式为 'YYYY-MM-DD'。
支持的范围是 '1000-01-01' 到 '9999-12-31'。
你可以通过字符串或数字将值赋给 DATE 列。
DATETIME[(fsp)]

日期和时间的组合，格式为 'YYYY-MM-DD HH:MM:SS[.fraction]'。
支持的范围是 '1000-01-01 00:00:00.000000' 到 '9999-12-31 23:59:59.499999'。
fsp 值可以在 0 到 6 之间，用来指定小数秒精度，默认值为 0。
TIMESTAMP[(fsp)]

时间戳，表示自 epoch（1970-01-01 00:00:00 UTC）以来的秒数，格式为 'YYYY-MM-DD HH:MM:SS[.fraction]'。
支持的范围是 '1970-01-01 00:00:01.000000' 到 '2038-01-19 03:14:07.499999'（UTC）。
fsp 值可以在 0 到 6 之间，用来指定小数秒精度，默认值为 0。
TIMESTAMP 类型有时会自动初始化和更新为当前的日期和时间（具体请参见 13.2.5 节）。
TIME[(fsp)]

时间类型，格式为 'HH:MM:SS[.fraction]'。
支持的范围是 '-838:59:59.000000' 到 '838:59:59.000000'。
fsp 值可以在 0 到 6 之间，用来指定小数秒精度，默认值为 0。
YEAR[(4)]

以 4 位数字表示年份，格式为 YYYY。
支持的范围是 1901 到 2155，或者 0000。



epoch（1970-01-01 00:00:00 UTC）

DATETIME 和 TIMESTAMP 数据类型提供了将当前日期和时间自动初始化和更新的功能。TIMESTAMP 类型的值在存储时会从当前时区转换为 UTC，并在检索时从 UTC 转换回当前时区。当前时区的值由 time_zone 系统变量提供




TIMESTAMP 和 DATETIME 列可以被自动初始化为当前的日期和时间（即当前时间戳），并在行数据修改时自动更新。
可以将当前时间戳指定为初始化、自动更新值，或者两者都指定：
自动初始化列：对于插入数据时没有为该列指定值的行，会将该列初始化为当前时间戳。
自动更新列：当行中的其他列的值发生变化时，自动更新该列为当前时间戳。要防止在其他列更改时自动更新该列，可以明确将该列设置为当前值。要在其他列不变化时仍然更新该列，可以显式将其设置为当前时间戳（例如，使用 CURRENT_TIMESTAMP）。


YEAR 类型是一个 1 字节的类型，用于表示年份值。


YEAR 类型的值以 YYYY 格式显示。
支持的年份范围是 1901 到 2155，以及特殊的 0000。数字字符串与字符串

默认值和自动更新值都使用 CURRENT_TIMESTAMP
DEFAULT CURRENT_TIMESTAMP\ 
ON UPDATE CURRENT_TIMESTAMP

## DATE TIME DATETIME TIMESTAMP YEAR CURRENT_TIMESTAMP


# 字符串
CHAR 类型的长度是固定的，存储时会将数据右侧填充空格，直到达到声明的长度长度范围为 0 到 255 字符。。
VARCHAR 类型是可变长度的字符串，最大长度可以指定为 0 到 65,535。
CHAR 和 VARCHAR 类型都通过指定一个长度来声明，该长度表示你想存储的最大字符数。例如，CHAR(30) 可以存储最多 30 个字符。
VARCHAR 的值是以 1 字节或 2 字节的长度前缀加数据的方式存储。长度前缀表示值的字节数。如果值的长度不超过 255 字节，则使用一个长度字节；如果值可能需要超过 255 字节，则使用两个长度字节。


CHAR VARCHAR ENUM SET


ENUM 类型是一个字符串对象，其值从创建表时显式列举的值列表中选择单个值。它通常用于列的值有限且预定义的场景。
ENUM 的值在内部以数字索引的方式存储，相较于直接存储字符串，能够减少存储空间。简化数据验证
缺点：
- 如果 ENUM 列表中的值看起来像数字，可能会导致混淆，难以区分文字值和其内部索引表示。
- 排序行为：ENUM 值是基于其索引数字进行排序的，而不是按字母顺序。这可能会导致在使用 ORDER BY 时出现意外的排序结果。

SET 类型是一个字符串对象，它可以包含零个或多个值组合，这些值必须从在创建表时指定的允许值列表中选择。
如果定义中有重复值，则会报错。
- 多标签系统
- 权限系统
- 支持多个选项的配置设置
- 用户偏好设置


在设计数据库时，如果需要在单个字段中存储多个选项并且选项的组合会不断变化，SET 类型是一个非常合适的选择。

 BINARY用于存储定长的二进制数据。如加密哈希值、UUID 等
 VARBINARY  BLOB最大存储4 GiB 
 TEXT

 ## 字符串类型 CHAR VARCHAR ENUM SET BINARY TEXT <sub>BLOB VARBINARY</sub>

CHAR[(M)]  VARCHAR(M)  BINARY[(M)]  TEXT[(M)]


字符单位字节单位 VARCHAR(M) BINARY(M) 默认值为 1  TEXT[(M)]   ENUM('value1', 'value2', ...)  SET('value1', 'value2', ...)



JSON 数据类型
MySQL能够高效地访问 JSON（JavaScript 对象表示法）文档中的数据。
二进制格式存储的 JSON 值允许服务器通过键或数组索引直接查找子对象或嵌套值，而无需读取文档中的所有其他值。
无效的文档会产生错误。
存储一个 JSON 文档所需的空间大致与 LONGBLOB 或 LONGTEXT 相同；
提供了一组 SQL 函数，支持对 JSON 值进行操作，如创建、操作和查询。

自动验证 JSON 文档的格式有效性。
提供专门的函数对 JSON 数据进行操作。
高效的存储和索引支持。


---

显式默认值（Explicit Default Values）
定义方式：通过 DEFAULT 子句在数据类型说明中明确指定默认值。
直接的固定值 i INT DEFAULT 0,
括号中的计算结果 f FLOAT DEFAULT (RAND() * RAND()),仅支持 文字、内置函数（确定性或非确定性）及操作符作为表达式。
TIMESTAMP 和 DATETIME 类型默认值可直接使用 CURRENT_TIMESTAMP（无需括号）。


隐式默认值（Implicit Default Values）
可为 NULL 的列：隐式设置为 DEFAULT NULL。
数值类型：默认值为 0。若定义为 AUTO_INCREMENT，默认值为下一个递增值。
日期时间类型：第一个 TIMESTAMP 列默认值为当前时间。
普通字符串默认值为空字符串 ''。
枚举类型 ENUM 默认值为定义的第一个枚举值。


插入默认值还可以这样：
```
INSERT INTO t4 VALUES();
INSERT INTO t4 VALUES(DEFAULT);
```



- 数据类型	数字 日期 字符串 JSON
- 数据类型默认值
- 数据类型存储要求
- 选择正确的列数据类型


数据类型
MySQL 支持以下主要数据类型：

数值类型			6	INT DECIMAL FLOAT DOUBLE BIT BIGINT
日期与时间类型		6	DATE TIME DATETIME TIMESTAMP YEAR CURRENT_TIMESTAMP
字符串（字符与字节）类型	6	CHAR VARCHAR ENUM SET TEXT BINARY 
空间类型			\
JSON 数据类型


SERIAL 是 BIGINT UNSIGNED NOT NULL AUTO_INCREMENT UNIQUE 的别名。
在定义整数列时，SERIAL DEFAULT VALUE 是 NOT NULL AUTO_INCREMENT UNIQUE 的别名。


DECIMAL 类型
语法：DECIMAL(M, D)
M 是精度，总位数。D 是小数位数。
例如，DECIMAL(5,2) 可存储的范围为 -999.99 到 999.99。
简写：DECIMAL(M) 等价于 DECIMAL(M, 0)。

浮点数类型
FLOAT 和 DOUBLE 用于表示近似数值：
FLOAT（单精度）：4 字节存储。
DOUBLE（双精度）：8 字节存储。
BIT 类型
BIT(M) 用于存储 M 位的值（1 ≤ M ≤ 64）。
使用 b'value' 的表示法表示二进制值（如 b'101'）。
默认左侧补零。
超范围数值处理
当插入的数值超出数据类型允许范围时：

日期与时间类型
MySQL 支持以下日期和时间类型：
类型	格式				范围
DATE	'YYYY-MM-DD'			'1000-01-01' 至 '9999-12-31'
DATETIME	'YYYY-MM-DD HH:MM:SS[.fraction]'	'1000-01-01 00:00:00.000000' 至 '9999-12-31 23:59:59.999999'
TIMESTAMP'YYYY-MM-DD HH:MM:SS[.fraction]'	'1970-01-01 00:00:01.000000' 至 '2038-01-19 03:14:07.999999'
TIME	'HH:MM:SS[.fraction]'		'-838:59:59.000000' 至 '838:59:59.000000'
YEAR	YYYY				1901 至 2155 或 0000

自动初始化与更新
TIMESTAMP 和 DATETIME 列可以自动初始化和更新为当前时间。
插入时自动初始化：DEFAULT CURRENT_TIMESTAMP
更新时自动更新：ON UPDATE CURRENT_TIMESTAMP
TIMESTAMP 值存储为 UTC 时间，并在检索时转换为当前时区。

字符串类型
类型	描述
CHAR	固定长度，右侧补空格，长度范围为 0 到 255。
VARCHAR	可变长度，长度范围为 0 到 65,535，存储时需额外使用 1 或 2 字节存储长度信息。
ENUM	枚举类型，可选择一个预定义的值列表中的单个值，存储为内部数字索引，节省空间。
SET	集合类型，可选择一个预定义值列表中的零个或多个值，适合多标签或权限设置场景。
BINARY	定长二进制数据，适用于加密哈希值等场景。
VARBINARY	可变长二进制数据。
TEXT	大型文本数据，存储上限为 4 GiB。
BLOB	二进制大对象，最大存储 4 GiB，适用于存储图像、音频等二进制数据。

JSON 数据类型
MySQL 提供对 JSON 数据的高效支持：
使用二进制格式存储，支持快速查找嵌套值。
提供操作 JSON 数据的 SQL 函数（如 JSON_EXTRACT、JSON_SET 等）。
自动验证 JSON 文档的格式有效性。
默认值的定义
显式默认值：通过 DEFAULT 子句指定，例如 i INT DEFAULT 0。
隐式默认值：若未指定，MySQL 根据类型提供默认值：
可为 NULL 的列：默认值为 NULL。
数值列：默认值为 0。
日期时间列：若为首个 TIMESTAMP 列，默认值为当前时间。
插入默认值的方式：
INSERT INTO table_name VALUES();
INSERT INTO table_name VALUES(DEFAULT);
选择正确的列数据类型
根据数据范围选择最小合适的存储类型，避免浪费存储空间。
使用 STRICT 模式 确保数据一致性。
充分利用 JSON、ENUM、SET 等特殊类型的特性，提升性能和灵活性。

```
**INT**
-- 创建表
CREATE TABLE example_int (
    id INT PRIMARY KEY,
    value INT UNSIGNED
);

-- 插入数据
INSERT INTO example_int (id, value) VALUES (1, 100), (2, 200);

-- 更新数据
UPDATE example_int SET value = 300 WHERE id = 1;

-- 删除数据
DELETE FROM example_int WHERE id = 2;

-- 查询数据
SELECT * FROM example_int;
```

```
-- 创建表
CREATE TABLE example_decimal (
    id INT PRIMARY KEY,
    price DECIMAL(10, 2)
);

-- 插入数据
INSERT INTO example_decimal (id, price) VALUES (1, 1234.56), (2, 789.99);

-- 更新数据
UPDATE example_decimal SET price = 1000.00 WHERE id = 1;

-- 删除数据
DELETE FROM example_decimal WHERE id = 2;

-- 查询数据
SELECT * FROM example_decimal;

```

```
-- 创建表
CREATE TABLE example_float (
    id INT PRIMARY KEY,
    score FLOAT
);

-- 插入数据
INSERT INTO example_float (id, score) VALUES (1, 95.5), (2, 80.75);

-- 更新数据
UPDATE example_float SET score = 100.0 WHERE id = 1;

-- 删除数据
DELETE FROM example_float WHERE id = 2;

-- 查询数据
SELECT * FROM example_float;

```

```
-- 创建表
CREATE TABLE example_double (
    id INT PRIMARY KEY,
    distance DOUBLE
);

-- 插入数据
INSERT INTO example_double (id, distance) VALUES (1, 1234567.89), (2, 9876543.21);

-- 更新数据
UPDATE example_double SET distance = 54321.99 WHERE id = 1;

-- 删除数据
DELETE FROM example_double WHERE id = 2;

-- 查询数据
SELECT * FROM example_double;

```

```
-- 创建表
CREATE TABLE example_bit (
    id INT PRIMARY KEY,
    flags BIT(8) -- 8 位
);

-- 插入数据
INSERT INTO example_bit (id, flags) VALUES (1, b'10101010'), (2, b'11110000');

-- 更新数据
UPDATE example_bit SET flags = b'00001111' WHERE id = 1;

-- 删除数据
DELETE FROM example_bit WHERE id = 2;

-- 查询数据
SELECT * FROM example_bit;

```

```
-- 创建表
CREATE TABLE example_bigint (
    id INT PRIMARY KEY,
    big_value BIGINT
);

-- 插入数据
INSERT INTO example_bigint (id, big_value) VALUES (1, 9223372036854775807), (2, 123456789012345);

-- 更新数据
UPDATE example_bigint SET big_value = 500000000000 WHERE id = 2;

-- 删除数据
DELETE FROM example_bigint WHERE id = 1;

-- 查询数据
SELECT * FROM example_bigint;

```

```
-- 创建表
CREATE TABLE example_date (
    id INT PRIMARY KEY,
    birth_date DATE
);

-- 插入数据
INSERT INTO example_date (id, birth_date) VALUES (1, '1990-01-01'), (2, '2000-12-31');

-- 更新数据
UPDATE example_date SET birth_date = '1985-05-15' WHERE id = 1;

-- 删除数据
DELETE FROM example_date WHERE id = 2;

-- 查询数据
SELECT * FROM example_date;

```

```
-- 创建表
CREATE TABLE example_time (
    id INT PRIMARY KEY,
    event_time TIME
);

-- 插入数据
INSERT INTO example_time (id, event_time) VALUES (1, '12:30:45'), (2, '23:59:59');

-- 更新数据
UPDATE example_time SET event_time = '00:00:00' WHERE id = 2;

-- 删除数据
DELETE FROM example_time WHERE id = 1;

-- 查询数据
SELECT * FROM example_time;

```

```
-- 创建表
CREATE TABLE example_datetime (
    id INT PRIMARY KEY,
    created_at DATETIME
);

-- 插入数据
INSERT INTO example_datetime (id, created_at) VALUES (1, '2025-01-07 14:30:00');

-- 更新数据
UPDATE example_datetime SET created_at = '2025-01-08 10:00:00' WHERE id = 1;

-- 查询数据
SELECT * FROM example_datetime;

```

```
-- 创建表
CREATE TABLE example_timestamp (
    id INT PRIMARY KEY,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

-- 插入数据
INSERT INTO example_timestamp (id) VALUES (1);

-- 自动更新时间戳
UPDATE example_timestamp SET id = 2 WHERE id = 1;

-- 查询数据
SELECT * FROM example_timestamp;

```

```
-- 创建表
CREATE TABLE example_year (
    id INT PRIMARY KEY,
    year YEAR
);

-- 插入数据
INSERT INTO example_year (id, year) VALUES (1, 2025), (2, 1999);

-- 更新数据
UPDATE example_year SET year = 2000 WHERE id = 2;

-- 删除数据
DELETE FROM example_year WHERE id = 1;

-- 查询数据
SELECT * FROM example_year;

```

```
-- 创建表
CREATE TABLE example_char (
    id INT PRIMARY KEY,
    code CHAR(5) -- 长度固定为 5
);

-- 插入数据
INSERT INTO example_char (id, code) VALUES (1, 'ABC'), (2, '12345');

-- 更新数据
UPDATE example_char SET code = 'XYZ' WHERE id = 1;

-- 删除数据
DELETE FROM example_char WHERE id = 2;

-- 查询数据
SELECT * FROM example_char;

```

```
-- 创建表
CREATE TABLE example_varchar (
    id INT PRIMARY KEY,
    description VARCHAR(255)
);

-- 插入数据
INSERT INTO example_varchar (id, description) VALUES (1, 'Hello, World!'), (2, 'MySQL VARCHAR Example');

-- 更新数据
UPDATE example_varchar SET description = 'Updated Text' WHERE id = 1;

-- 删除数据
DELETE FROM example_varchar WHERE id = 2;

-- 查询数据
SELECT * FROM example_varchar;

```

```
-- 创建表
CREATE TABLE example_enum (
    id INT PRIMARY KEY,
    status ENUM('active', 'inactive', 'pending')
);

-- 插入数据
INSERT INTO example_enum (id, status) VALUES (1, 'active'), (2, 'pending');

-- 更新数据
UPDATE example_enum SET status = 'inactive' WHERE id = 1;

-- 删除数据
DELETE FROM example_enum WHERE id = 2;

-- 查询数据
SELECT * FROM example_enum;

```

```
-- 创建表
CREATE TABLE example_set (
    id INT PRIMARY KEY,
    options SET('A', 'B', 'C', 'D')
);

-- 插入数据
INSERT INTO example_set (id, options) VALUES (1, 'A,B'), (2, 'C,D');

-- 更新数据
UPDATE example_set SET options = 'A,C' WHERE id = 1;

-- 删除数据
DELETE FROM example_set WHERE id = 2;

-- 查询数据
SELECT * FROM example_set;

```

```
-- 创建表
CREATE TABLE example_text (
    id INT PRIMARY KEY,
    content TEXT
);

-- 插入数据
INSERT INTO example_text (id, content) VALUES (1, 'This is a long text example.');

-- 更新数据
UPDATE example_text SET content = 'Updated long text.' WHERE id = 1;

-- 删除数据
DELETE FROM example_text WHERE id = 1;

-- 查询数据
SELECT * FROM example_text;

```

```
-- 创建表
CREATE TABLE example_binary (
    id INT PRIMARY KEY,
    hash BINARY(32) -- 固定长度为 32 字节
);

-- 插入数据
INSERT INTO example_binary (id, hash) VALUES (1, UNHEX('9c1185a5c5e9fc54612808977ee8f548b2258d31e12a13a72393b3f52f51167c'));

-- 查询数据
SELECT HEX(hash) AS hash_value FROM example_binary;

```

```
-- 创建表
CREATE TABLE example_json (
    id INT PRIMARY KEY,
    data JSON
);

-- 插入数据
INSERT INTO example_json (id, data) VALUES 
(1, '{"name": "John", "age": 30}'), 
(2, '{"name": "Jane", "skills": ["SQL", "Python"]}');

-- 更新数据
UPDATE example_json 
SET data = JSON_SET(data, '$.age', 31) 
WHERE id = 1;

-- 删除数据
DELETE FROM example_json WHERE id = 2;

-- 查询 JSON 数据
SELECT JSON_EXTRACT(data, '$.name') AS name FROM example_json;

```


----

# 第五章 教程
5.1 连接与断开服务器
5.2 输入查询
5.3 创建和使用数据库
5.4 获取数据库和表的相关信息
5.5 批量模式下使用mysql
5.6 常见查询示例
5.7 将MySQL与Apache结合使用

展示如何使用mysql客户端程序创建并使用一个简单的数据库
mysql（有时被称为“终端监视器”或简称“监视器”）是一个交互式程序，允许你连接到MySQL服务器，执行查询，并查看查询结果。
mysql也可以以批量模式运行：你可以事先将查询语句放入文件中，然后告诉mysql执行文件内容。

查看mysql提供的所有选项，可以通过--help选项来调用它：
`$> mysql --help`

作为匿名（未命名）用户连接运行在本地主机上的服务器
$> mysql
输入QUIT（或\q）来断开连接

## 5.2 输入查询
下面是一个简单的查询，要求服务器返回其版本号和当前日期。
`SELECT VERSION(), CURRENT_DATE;`
如果你检索的是表达式的值而不是表的列，mysql会使用表达式本身作为列标签。
mysql会显示返回的行数和查询执行所需的时间，从而大致反映服务器的性能。
这些值并不完全精确，因为它们表示的是实际的墙钟时间（而非CPU或机器时间），并且会受到服务器负载和网络延迟等因素的影响。
决定不执行当前正在输入的查询，可以通过输入\c来取消它

mysql数据库描述了用户的访问权限。

调用mysql时，在命令行中指定数据库。只需在提供连接参数后指定数据库名
`mysql -h host -u user -p menagerie`
 在上面示例中的menagerie不是你的密码。如果你想在命令行中提供密码（在-p选项之后），必须将密码紧接在-p后面，且中间不能有空格（例如，-ppassword，而不是-p password）。

随时通过执行`SELECT DATABASE()`语句来查看当前选择的是哪个数据库。