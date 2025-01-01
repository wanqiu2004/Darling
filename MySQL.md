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
