---
title: HiveSQL基础命令清单
categories:
  - hive
tags:
  - sql
layout:
  - article
date: 2023-02-22 21:31:13
---
> 彼采葛兮

<!-- more -->

* [清单](#00)
  * [Hive操作表](#01)
  * [Hive查询语句](#02)
  * [Hive函数](#03)

<h3 id="01">Hive对表操作命令</h3>

| for what | how  |
|:--| :----  |
| 模糊搜表 | show tables like 'table_name' |
| 表结构 | desc table_name |
| 表分区 | show partitions table_name |
| 表结构 | desc table_name |
| 修改表名 | alter table old_table_name rename to new_table_name |
| 复制表 | create table if not exist new_table_name like table_name|
| 删除表 | drop table if exist table_name |
| 清空表 | truncate table table_name |
| 建表 | create table if not exist table_name |
| 删除表分区 | alter table table_name drop partition(dt='2023-02-28')|
| 添加表分区 | alter table table_name add partition(dt='2023-02-28')|
| 添加字段 | alter table table_name add columns(columns_values bigint comment 'comment_text')|
| 添加字段 | alter table table_name modify old_column new_column varchar(255) comment 'comment_text'|
|  |  |


<h3 id="02">Hive查询语句</h3>

select语法及语序
```apache
select expr1 ,expr2
from table_name
where dt='partition'  
group by column_list
order by order_condition desc(asc)
distribute by distribute_condition (sort by sort_condition)
limit number;  
```

| for what | how  | description  |
|:--| :----  | :----  |
| 局部排序 | sort by | 基于mapreduce的内部排序，不是全局结果集的全排序  |
| 分区排序 | distribute by | 一般结合sort by使用进行分区排序 |
| 内连接   |inner join| |
| 左连接   |left join| |
| 右连接   |right join| |
| 全外连接  |full join| |
   

<h3 id="03">Hive函数</h3>

1. 聚合函数

```apache
count(expr)  # 计数
sum(expr)    # 求和
avg(expr)    # 平均
min(expr)    # 最小
max(expr)    # 最大
```

2. 条件函数

```apache
if(expr, trueValue, falseValue)                                              # 如果expr为true，返回trueValue，否则返回falseValue
case when expr1 then result1 when expr2 then result2 ... else defaultValue   # 按照顺序判断expr是否满足条件，满足则返回对应结果，否则返回默认结果
```

3. 字符串函数

```apache
concat(str1, str2, ..., pattern)    # 合并两个或者多个字符串，若有一个str为null，则最终返回Null
substr(str, start, length)          # 返回从指定位置开始的指定长度的字符串
length(str)                         # 返回字符串的长度
upper(str)
lower(str)
trim(str)
ltrim(str)
rtrim(str)
```

4. 数组函数

```apache
array(expr1, expr2, ...)       # 创建一个数组，元素为表达式的值
array_contains(array, value)   # 判断数组是否包含指定值
array_size(array)              # 返回数组的大小
element_at(array, index)b      # 返回数组指定位置的元素值
```

5. 正则表达式函数

```apache
regexp_extract(str, pattern)                # 从字符串中提取匹配正则表达式的字串
regexp_replace(str, pattern, replacement)   # 替换字符串中匹配正则表达式的字串
regexp_like(str, pattern)                   # 判断字符串是否匹配正则表达式
```

6. 数值函数

```apache
abs(x)
ceil(x)      # 返回大于x的最小整数
floor(x)     # 返回小于等于x的最小整数
round(x, d)  # 保留d小数位数的x的四舍五入
```

7. 时间日期函数

```apache
now()
current_timestamp()
year(date)
month(date)
day(date)
hour(daye)
```

8. 其他函数

```apache
cast(expr AS type)           # 将表达式的类型转换为其他类型
coalesce(expr1, expr2, ...)  # 返回第一个非NULL表达式的值
nullif(expr1, expr2)         # 如果expr1等于expr2，返回NULL，否则返回expr1的值
rand([seed])                 # 返回一个随机数
```
