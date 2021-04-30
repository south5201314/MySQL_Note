[TOC]

# 查询

## 基本的查询

| 命令                             | 描述                             |
| -------------------------------- | -------------------------------- |
| SELECT * FROM 表名;              | 查询表中所有的数据               |
| SELECT 列名1,列名2... FROM 表名; | 查询指定列的数据                 |
| SELECT DISTINCT 列名 FROM 表名;  | 查询唯一的数据                   |
| SELECT 列名 AS 别名 FROM 表名;   | 查询指定列数据，并把给列起个别名 |

说明：

* 别名使用双引号，以便在别名中包含空格或特殊的字符并区分大小写。
* 日期和字符只能在单引号中出现。

## 过滤和排序数据

### 过滤

| 命令                                  | 描述                 |
| ------------------------------------- | -------------------- |
| SELECT 列名 FROM 表名 WHERE 条件语句; | 根据指定条件查询数据 |

* 比较运算

| 操作符 | 含义               |
| ------ | ------------------ |
| =      | 等于               |
| >      | 大于               |
| <      | 小于               |
| >=     | 大于等于           |
| <=     | 小于等于           |
| <>     | 不等于(也可以是!=) |

* 逻辑运算

| 操作符 | 含义   |
| ------ | ------ |
| AND    | 逻辑与 |
| OR     | 逻辑或 |
| NOT    | 逻辑非 |

* 其它运算

| 操作符                         | 含义                 |
| ------------------------------ | -------------------- |
| BETWEEN...AND...               | 在两值之间(包含边界) |
| IN('列表元素1','列表元素2'...) | 等于列表中的某个元素 |
| LIKE                           | 模糊查询             |
| IS NULL                        | 是否是空值           |

说明：

* 使用 LIKE 运算选择类似的值。
* 通配符：
  * % 表示零个或多个字符(任意个字符)。
  * _ 代表一个字符。

* 如果模糊中包含字符 % _ (通配符)，则需要使用转义。默认转义字符 /[通配符]，也可以使用`ESCAPE`自定义转义字符：

```java
`SELECT * FROM 表名 WHERE 列名 LIKE '_$%' ESCAPE  '$‘`  
```

### 排序

* `ORDER BY` 子句在`SELECT`语句的结尾。
* 排序类型：
  * ASC(ascend)：升序(默认是升序)。
  * DESC(descend)：降序。

```java
//正常排序
SELECT 列名 FROM 表名 ORDER BY 需排序的列 [ASC/DESC];
//根据列的别名排序
SELECT 列名1 AS 别名1,列名2 AS 别名2... FROM 表名 DRDER BY 别名1,[别名2...];
//多个列排序
SELECT * FROM 表名 DRDER BY 列名1,列名2[或者别名];
```

说明：字符串的比较是根据字符集的大小来进行的，类似于java的字符串大小比较。

## 常见函数

### 字符函数

| 函数                 | 参数描述                         | 功能描述                                                   |
| -------------------- | -------------------------------- | ---------------------------------------------------------- |
| LENGTH(str)          | 字符串                           | 获取字节长度                                               |
| LOWER(str)           | 字符串                           | 把大写转换成小写                                           |
| UPPER(str)           | 字符串                           | 把小写转换成大写                                           |
| CONCAT(str...)       | 多个字符串                       | 连接字符串                                                 |
| SUBSTR(str,pos,len)  | 字符串，起始位置，字符长度       | 截取字符子串                                               |
| INSTR(str,s)         | 被插入的字符串，需要插入的字符串 | 插入字符                                                   |
| LPAD(str,len,s)      | 字符串，长度，填充的字符串       | 左填充，原字符串长度不够用指定字符串填充                   |
| RPAD(str,len,s)      | 字符串，长度，填充的字符串       | 右填充，原字符串长度不够用指定字符串填充                   |
| TRIM(s FROM str)     | 指定清除的字符串，被清除的字符串 | 清除前后的指定字符串，如果不指定str FROM则默认清除的是空格 |
| REPLACE(str,old,new) | 字符串，旧字符串，新字符串       | 用新的字符串替换旧的字符串                                 |

### 数学函数

| 函数                 | 参数描述           | 功能描述             |
| -------------------- | ------------------ | -------------------- |
| ROUND(number,len)    | 浮点数，保留的位数 | 四舍五入取正         |
| CEIL(number)         | 浮点数             | 向上取正             |
| FLOOR(number)        | 浮点数             | 向下取正             |
| TRUNCATE(number,len) | 浮点数，保留的位数 | 截断，不进行四舍五入 |
| MOD(divdend,divisor) | 被除数，除数       | 取模，求余数         |

### 日期函数

| 函数                        | 参数描述               | 功能描述                                 |
| --------------------------- | ---------------------- | ---------------------------------------- |
| NOW()                       | 无                     | 获取当前系统日期和时间                   |
| CURDATA()                   | 无                     | 获取当前系统日期                         |
| CURTIME()                   | 无                     | 获取当前系统时间                         |
| YEAR(data)                  | 日期时间               | 获取年                                   |
| MONTH(data)                 | 日期时间               | 获取月                                   |
| MONTHNAME(data)             | 日期时间               | 获取月，英文的形式                       |
| DAY(data)                   | 日期时间               | 获取日                                   |
| HOUR(data)                  | 日期时间               | 获取小时                                 |
| MINUTE(data)                | 日期时间               | 获取分钟                                 |
| SECOND(data)                | 日期时间               | 获取秒                                   |
| STR_TO_DATE(datastr,format) | 日期时间字符串，格式化 | 把字符串中的日期时间按一定格式转换成时间 |
| DATE_FORMAT(date,format)    | 日期时间，格式化       | 把日期时间按一定格式转换成字符串         |

* 日期时间格式符

| 格式化 | 功能                 |
| ------ | -------------------- |
| %Y     | 四位的年份           |
| %y     | 两位的年份           |
| %m     | 两位的月份(01,02...) |
| %c     | 月份(1,2....11,12)   |
| %d     | 日(01,02)            |
| %H     | 小时(24小时制)       |
| %h     | 小时(12小时制)       |
| %i     | 分钟(00,01...59)     |
| %s     | 秒(00,01...59)       |

### 其它函数

| 函数       | 参数描述 | 功能描述               |
| ---------- | -------- | ---------------------- |
| VERSION()  | 无       | 获取MySQL版本          |
| DATABASE() | 无       | 获取当前使用的数据库   |
| USER()     | 无       | 获取当前使用的登录账户 |

### 流程控制函数

* IF表达式(与java中三元运算符差不多)。
* 特点：可以在任何地方使用。

```sql
SELECT [列名,] IF(条件语句,true返回的值,false返回的值) [FROM 表名] [WHERE 条件语句];
```

* CASE表达式

  * switch格式

    ```mysql
    # 如果THEN后是语句，必须加分号并且只能在BEGIN END中使用
    SELECT [列名,] 
    CASE 条件表达式
    WHEN 常量1 THEN 返回值1或语句1
    WHEN 常量2 THEN 返回值2或语句2
    WHEN 常量3 THEN 返回值3或语句3
    [...]
    ELSE 返回值n或语句n
    END [AS 别名]
    [FROM 表名];
    ```
    
  * IF-THEN-ELSE格式
  
    ```mysql
    # 如果THEN后是语句，必须加分号并且只能在BEGIN END中使用
    SELECT [列名,]
    CASE
    WHEN 条件表达式1 THEN 结果为true时返回值1或语句1
    WHEN 条件表达式2 THEN 结果为true时返回值2或语句2
    WHEN 条件表达式3 THEN 结果为true时返回值3或语句3
    [...]
    ELSE 返回值n或语句n
    END [AS 别名]
    [FROM 表名];
    ```
## 分组函数

* 作用：处理一组数据，并返回一个值。

| 函数        | 参数描述 | 功能描述       |
| ----------- | -------- | -------------- |
| AVG(list)   | 列名     | 求平均值       |
| COUNT(list) | 列名     | 求非空的总个数 |
| MAX(list)   | 列名     | 求最大值       |
| MIN(list)   | 列名     | 求最小值       |
| SUM(list)   | 列名     | 求和           |

说明：

* 以上分组函数都忽略NULL值。
* COUNT(*)：用于返回表中的记录总数，适用于任意数据类型；也可以使用COUNT(1)返回表中的记录总数，参数可以是不为NULL,不为表中的字段(列)的任意类型的任意值。

## 分组查询

### 分组数据

* GROUP BY子句将表中的数据分成若干组。

* WHERE一定放在FROM后面。

* 在SELECT 列表中所有未包含在组函数中的列都应该包含在 GROUP BY 子句中。

  ```mysql
  SELECT department_id,AVG(salary)
  FROM employees
  GROUP BY department_id;# department_id 字段未包含在组函数中
  ```

* 包含在 GROUP BY 子句中的列不必包含在SELECT 列表中。

  ```mysql
  SELECT AVG(salary)
  FROM employees
  GROUP BY department_id;# department_id 字段不必包含在SELECT列表
  ```

* 非法使用组函数
  * 不能在WHERE子句中使用组函数。
  * 可以在HAVING子句中使用组函数。

### 过滤分组

* 使用HAVING过滤分组。

* 过滤的是分组后的数据，使用了组函数的数据。

  ```mysql
  SELECT [列名... ,][函数,]组函数 AS 别名
  FROM 表名
  WHERE 过滤原始表的数据的条件
  GROUP BY 分组字段1,[分组字段2...]
  HAVING 过滤分组后表的数据的条件
  [ORDER BY 列名 ASC[DESC]];
  ##
  SELECT department_id,TRUNCATE(AVG(salary),2) AS 平均工资
  FROM `employees`
  WHERE `department_id` IS NOT NULL
  GROUP BY `department_id`
  HAVING 平均工资>6000 AND department_id>50;
  ```

总结：

* 分组查询可以理解为先把数据按照要求映射，再使用组函数归约。

## 分表查询

* 按语法(年代)分类：
  * sql92标准：仅仅支持内连接。
  
    ```mysql
    SELECT [分组函数,]查询列表
    FROM 表1 AS 表别名1,表2 AS 表别名2
    WHERE 连接条件[AND 过滤条件]
    [GROUP BY 分组字段]
    [ORDER BY 排序字段 DESC[ASC]]
    ```
  
  * sql99标准：支持内连接、外连接(左外和右外)和交叉连接。
  
    ```mysql
    SELECT [分组函数,]查询列表
    FROM 表1 AS 表别名
    [INNER、LEFT、RIGHT、CROSS] JOIN 表2 # INNER内连接,LEFT、RIGHT左、右外连接,CROSS交叉连接
    ON 连接条件
    [WHERE 过滤条件]
    [GROUP BY 分组字段]
    [ORDER BY 排序字段 DESC[ASC]]
    ```

### 内连接

* sql92表中在 WHERE 子句中写入连接条件；sql99表中在ON子句中写入连接条件。
* 在表中有相同列时，在列名之前加上表名前缀或表的别名。

* 用一个表的一个字段或多个字段与另外一个表(多个表、当前表)的一个字段或多个字段进行WHERE条件运算(=、<>、<、BETWEEN...AND....)，如果多个条件运算则用AND分隔。
* 连接 n个表,至少需要 n-1个连接条件，使用AND分隔。
* 表的别名
  * 使用别名可以简化查询。
  * 使用表名前缀可以提高执行效率。

#### 等值连接

* sql92标准：WHERE子句连接条件是等值(=)。

```mysql
# 查询员工部门名
SELECT e.last_name,e.job_id,j.job_title
FROM employees AS e,jobs AS j # jobs部门表
WHERE e.job_id = j.job_id;# 匹配两个表中相等的字段
```

* sql99标准：使用INNER关键字。

```mysql
# 查询员工部门名
SELECT e.last_name,e.job_id,j.job_title
FROM employees AS e INNER JOIN jobs AS j
ON e.job_id = j.job_id
WHERE e.last_name LIKE '%k%';
```

#### 非等值连接

* sql92标准：WHERE子句连接条件是非等值。

```mysql
# 查询员工工资等级
SELECT last_name,grade_level,salary
FROM employees,job_grades# job_grades 工资等级表
WHERE salary BETWEEN lowest_sal/*最低*/ AND highest_sal/*最高*/;# 一个表的字段与另外一个表的字段进行条件匹配
```

* sql99标准：

```mysql
# 查询员工工资等级
SELECT e.last_name,g.grade_level,e.salary
FROM employees AS e
INNER JOIN job_grades g
ON e.salary BETWEEN g.lowest_sal AND highest_sal;
```

#### 自连接

* 当前表连接自己。
* 用当前表某个字段与当前表的另外一个字段进行匹配。

* sql92标准：

```mysql
# 查询员工的领导名字
SELECT e1.last_name,e1.manager_id,e2.last_name AS manager_name
FROM employees e1,employees e2
WHERE e1.manager_id = e2.employee_id;# 用员工信息的领导id字段与员工表的员工id(领导也是员工)进行匹配
```

* sql99标准：

```mysql
# 查询员工的领导名字
SELECT e.last_name,e.manager_id,m.last_name
FROM employees AS e
INNER JOIN employees m
ON e.manager_id = m.employee_id;
```

### 外连接

* 应用场景：用于查询一个表中有，另外一个表没有的记录。
* 特点：
  * 外连接的查询结果为主表的所有记录
    * 如果从表中有和它匹配的，则显示匹配的值。
    * 如果从表中没有和它匹配的，则显示null。
    * 外连接查询结果=内连接结果+主表中有而从表中没有的记录(左、右外连接)。
    * 全外连接查询结果=内连接结果+主表中有而从表中没有的记录+从表中有而主表中没有的记录。
* 外连接中分主表和从表，不同类型的外连接的主表和从表的位置都不一样。
  * 左外连接：LEFT JOIN左边是主表，右边是从表。
  * 右外连接：RIGHT JOIN右边是主表，左边是从表。
  * 全外连接：不分主表和从表，那个表都可以是主表或者从表。

#### 左外连接

```mysql
SELECT 查询列表[,分组函数]
FROM 主表 AS 主表别名
LEFT JOIN 从表 AS 从表别名
ON 连接条件 # 可以有多个连接条件
[LEFT JOIN 从表1 AS 从表1别名]# 可以有多个从表,在此表前的表都是主表
[ON 连接条件] # 可以有多个连接条件
[GROUP BY 分组字段]
[ORDER BY 排序字段 DESC[ASC]]
```

```mysql
# 查询没有男朋友的女神的数据
SELECT b.*,bo.*
FROM beauty AS b
LEFT JOIN boys AS bo
ON b.boyfriend_id = bo.id
WHERE bo.id IS NULL;
```

#### 右外连接

```mysql
SELECT 查询列表[,分组函数]
FROM 从表 AS 从表别名
RIGHT JOIN 主表 AS 主表别名
ON 连接条件 # 可以有多个连接条件
[RIGHT JOIN 主表1 AS 主表1别名]# 可以有多个主表,前一个表示是此主表的从表
[ON 连接条件] # 可以有多个连接条件
[GROUP BY 分组字段]
[ORDER BY 排序字段 DESC[ASC]]
```

#### 全外连接

* MySQL语法中没有全外连接，可以简单连接为左外连接+右外连接。
* 全外连接查询结果=内连接结果+主表中有而从表中没有的记录+从表中有而主表中没有的记录。

```mysql
SELECT 查询列表[,分组函数]
FROM 主表 AS 主表别名
FULL JOIN 从表 AS 从表别名
ON 连接条件 # 可以有多个连接条件
[FULL JOIN 从表1 AS 从表1别名]# 可以有多个主表
[ON 连接条件] # 可以有多个连接条件
[GROUP BY 分组字段]
[ORDER BY 排序字段 DESC[ASC]]
```

### 交叉连接

* 笛卡尔积，所有表中的所有行互相连接。

sql92标准：

```mysql
SELECT 查询列表[,分组函数]
FROM 主表 AS 主表别名,从表1 AS 从表别名1[从表2 AS 从表别名2...]
[GROUP BY 分组字段]
[ORDER BY 排序字段 DESC[ASC]]
```

sql99标准：

```mysql
SELECT 查询列表[,分组函数]
FROM 主表 AS 主表别名
CROSS JOIN 从表 AS 从表别名
ON 连接条件 # 可以有多个连接条件
[CROSS JOIN 从表1 AS 从表1别名]# 可以有多个主表
[ON 连接条件] # 可以有多个连接条件
[GROUP BY 分组字段]
[ORDER BY 排序字段 DESC[ASC]]
```

## 子查询

* 出现在其他语句内部的select语句，称为子 查询或内查询。

* 内部嵌套其他select语句的查询，称为外查询或主查询。

* 注意：

  * 子查询要包含在括号内。

  * 将子查询放在比较条件的右侧。

  * 单行操作符对应单行子查询(比较运算符)，多行操作符对应多行子查询。

  * 多行操作符：

    | 操作符    | 含义                           |
    | --------- | ------------------------------ |
    | IN/NOT IN | 等于列表中的任意一个值         |
    | ANY\|SOME | 和子查询返回列表的某一个值比较 |
    | ALL       | 和子查询返回的列表的所有值比较 |

### WHERE/HAVING子查询

* 支持单行子查询和多行子查询。

#### 单行子查询

* 单行子查询也叫标量子查询(一列一行)

```mysql
# WHERE
SELECT 查询列表
FROM 表
WHERE 列名[值] 单行运算符 (
    子查询语句
)
# HAVING
SELECT 查询列表,分组函数
FROM 表
GROUP BY 分组字段
HAVING 列名[值] 单行运算符 (
    子查询语句
)
```

#### 多行子查询

* 一列多行。

```mysql
# WHERE
SELECT 查询列表
FROM 表
WHERE 列名[值] 单行运算符 多行运算符(
    子查询语句
)
#HAVING
SELECT 查询列表,分组函数
FROM 表
GROUP BY 分组字段
HAVING 列名[值] 单行运算符 多行运算符(
    子查询语句
)
```

### SELECT子查询

* 只支持单行子查询(标量子查询)

```mysql
SELECT 查询列表,(
    子查询语句 # 结果只能是单行单列
)
FROM 表;
```

```mysql
# 查询部门信息和该部门的员工个数
# SELECT 子查询
SELECT d.*,(
    SELECT COUNT(*)
    FROM employees e
    WHERE e.department_id = d.department_id
) AS 个数
FROM departments d;
```

### FROM子查询

* 子查询的结果得到一个新的表(虚拟表)。

```mysql
SELECT 查询列表
FROM 表 表别名
[JOIN TYPE] JOIN (
    子查询语句
) AS 表别名; # 得到一个新的表(虚拟表)
```

```mysql
# 查询部门信息和该部门的员工个数
# FROM 子查询
SELECT d.*,t.count
FROM `departments` d
JOIN (
    SELECT e.`department_id`,COUNT(*) AS 'count'
    FROM employees e
    GROUP BY department_id
) AS t
ON d.department_id = t.department_id;
```

## 分页查询

* LIMIT 字句必须放在整个查询语句的最后。

```mysql
SELECT 查询列表,[分组函数]
FROM 表
WHERE 过滤条件语句
[GROUP BY 分组字段]
[HAVING 分组后过滤条件语句]
[ORDER BY 排序字段 DESC[ASC]]
LIMIT startIndex,size # startIndex:开始索引(索引从0开始) size:长度(查询多少个)
# 应用场景：多页网页(52论坛),点击下一页或上一页
# startIndex = (page-1) * size # page:页数 size:一页多少条数据
```

## 联合查询

* 把多个查询语句的结果组成一个查询结果。

* 应用场景：要查询的数据来自于多个表，且多个表没有直接的连接关系，但查询的数据的信息是一致的。
* 特点：
  * 多条查询语句的查询列表是一致的。
  * 多条查询语句的查询的每一列的类型和顺序最好一致。
  * UNION关键字默认去重，使用的UNION ALL 可以包含重复现。

```mysql
# 查询语句1
SELECT 查询列表
FROM 表
....
UNION
# 查询语句2
SELECT 查询列表
FROM 表
....
UNION
.... # 可以有多个查询语句
```

# 插入

## 方式一

* 语法

  ```mysql
  INSERT INTO 表[(column,column...)]
  VALUES (value,value...)[,(value,value...)...] # 可以同时查询多行数据
  ```

*  字符和日期型数据应包含在单引号中。

* 可以使用子查询，子查询的结果当做VALUES插入到表中，不必书写 VALUES 子句。

  ```mysql
  # 把有男朋友的女神名插入到男神表中
  INSERT INTO boys(boyName,userCP)
  SELECT NAME,100
  FROM beauty AS b
  JOIN boys AS bo
  ON b.boyfriend_id = bo.id;
  ```

## 方式二

* 语法

  ```mysql
  INSERT INTO 表
  SET 列名 = 值,列名 = 值...
  ```

* 一次只能插入一条数据，不支持子查询。

# 更新

## 单表更新

* 语法

  ```mysql
  UPDATE 表 #需要修改的表
  SET 列名 = 新值[,列名 = 值...] #可以修改多个
  [WHERE 筛选条件] #如果没有筛选条件就全部修改表中的数据
  ```

## 多表更新

* 需要进行表的连接。

* 语法

  ```mysql
  # sql92语法
  UPDATE 表1 AS 表别名1,表2 AS 表别名2
  SET 列 = 值... #可以根据别名或表名指定修改不用表的值
  WHERE 连接条件 
  AND 过滤条件;
  
  # sql99语法
  UPDATE 主表 别名
  [JOIN TYPE] JOIN 从表 别名
  ON 连接条件
  SET [别名.]列名 = 值,[别名.]列名 = 值... #可以根据表名或别名修改主表或从表中的数据,也可以两个表都修改。
  WHERE 过滤条件;
  ```

  ```mysql
  # 修改张无忌女朋友的手机号为114
  UPDATE boys bo
  INNER JOIN beauty b ON bo.id = b.boyfriend_id
  SET b.phone = "114"
  WHERE bo.boyName = '张无忌';
  ```

# 删除

## 方式一

### 单表删除

* 语法

```mysql
DELETE FROM 表名 WHERE 筛选条件;
```

### 多表删除

```mysql
# sql92语法
DELETE 表名[别名] #需要删除数据的表,可以指定多个。
FROM 表名1 AS 别名1,表名2 AS 别名2
WHERE 连接条件
AND 筛选条件;

# sql99语法
DELETE 表名[别名] #需要删除数据的表,可以指定多个。
FROM 表名 AS 别名
[JOIN TYPE] JOIN 从表 AS 别名
ON 连接条件
WHERE 筛选条件;
```

## 方式二

* 清空表中数据并重置主键。

  ```mysql
  TRUNCATE table 表名;
  ```