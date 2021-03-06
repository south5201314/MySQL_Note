[TOC]

# 数值类型

## 整型

| 整数类型    | 字节 | 范围                                                         |
| ----------- | ---- | ------------------------------------------------------------ |
| Tinyint     | 1    | 有符号：-128~127 无符号0~255                                 |
| Smallint    | 2    | 有符号：-32768~32767 无符号：0~65535                         |
| Mediumint   | 3    | 有符号：-8388608~8388607 无符号：0~1677215                   |
| int/integer | 4    | 有符号：- 2147483648~2147483647 无符号：0~4294967295         |
| Bigint      | 8    | 有符号： -9223372036854775808 ~9223372036854775807 无符号：0~ 9223372036854775807*2+1 |

* 默认是有符号，设置无符号需要添加unsigned关键字。
* 如果插入的数值超过范围，则会报out of range异常，并插入临界值。
* 如果不设置长度，会有默认长度。
  * 长度代表显示的最大宽度，而不是数值的长度，如果长度不够则会在左边用0填充，但必须搭配zerofill关键字。

## 浮点型

### 浮点型类型

| 浮点数类型 | 字节 | 范围                                               |
| ---------- | ---- | -------------------------------------------------- |
| float      | 4    | ±1.75494351E-38~±3.402823466E+38                   |
| double     | 8    | ±2.2250738585072014E-308~ ±1.7976931348623157E+308 |

### 定点数类型

| 定点数类型   | 字节 | 范围                                                         |
| ------------ | ---- | ------------------------------------------------------------ |
| BEC(M,D)     | M+2  | 最大取值范围与double相同，给定decimal的有效取值范围由M和D 决定 |
| DECIMAL(M,D) | M+2  | 同上                                                         |

* M：整数部分+小数部分位数
* D：小数部分的位数(保留多少位小数，如果超过则自动四舍五入)
* 如果整数部分大于M-D的位数则会报错(早期的mysql是警告并保存临界值)
* M和D可以省略
  * 如果是DEC和DECIMAL，则M默认为10，D默认为0。
  * 如果float和double，则会根据插入的数值的精度来决定精度。

* 定点型的精度较高，如果要求插入的数值的精度较高，如货币运算等则需要考虑使用定点型。

# 字符类型

| 字符串类型 | 最多字符数 | 描述及存储需求   | 特点     | 空间 | 效率 |
| ---------- | ---------- | ---------------- | -------- | ---- | ---- |
| char(M)    | M          | M为0~255的整数   | 固定长度 | 较大 | 高   |
| varchar(M) | M          | M为0~65535的整数 | 可变长度 | 较小 | 低   |

* varchar需要指定最多字符数(M)，char可不指定，默认为1。
## 其它字符类型
* binary和varbinary类型，存储二进制字符串。

* Enum类型

  * 说明:又称为枚举类型哦，要求插入的值必须属于列表中指定的值之一。

    ```mysql
    # 创建表
    CREATE TABLE 表名(
        列名 ENUM(字符[字符串],字符[字符串]...);
    )
    # 插入数据
    INSERT INTO 表名[(列名)] VALUES(字符[字符串]);
    # VALUES的值只能是创建表时ENUM列表中的某个值
    ```

    ```mysql
    # 创建表
    CREATE TABLE t_enum(
        e ENUM('aaaa','bbbb','b','c')
    );
    # 插入数据
    INSERT INTO t_enum VALUES('aaaa'),('c');
    ```

* SET类型

  * 与ENUM类似，但SET里可以保存0~64个成员，某个成员之间用逗号隔开并组成一个字符串。

    ```mysql
    # 创建表
    CREATE TABLE t_set(
    s SET('aaa','ccc','q','w')
    );
    # 插入数据
    INSERT INTO t_set VALUES('aaa,ccc');
    ```

* blob类型
  * 存储较大的二进制。

* text类型
  * 存储较长的文本。

# 日期类型

| 日期时间类型 | 字节 | 最小值              | 最大值              |
| ------------ | ---- | ------------------- | ------------------- |
| date         | 4    | 1000-01-01          | 9999-12-31          |
| time         | 3    | -838:59:59          | 838:59:59           |
| year         | 1    | 1901                | 2155                |
| datetime     | 8    | 1000-01-01 00:00:00 | 9999-12-31 23:59:59 |
| timestamp    | 4    | 19700101080001      | 2038年的某个时刻    |

* timestamp和实际时区有关，更能反映实际的日期，而datetime则只能反映出插入时的当地时区。
* timestamp的属性受Mysql版本和SQLMode的影响很大。

