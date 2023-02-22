---
title: Hive SQL Recipe
categories:
  - 大数据
tags:
  - hive
  - sql
layout:
  - article
date: 2023-02-22 21:31:13
---
> 彼采葛兮

* [清单](#00)
  * [Hive操作表](#01)
  * [Hive查询语句](#02)
  * [Hive函数](#03)

<h3 id="01">Hive对表操作命令</h3>
1. 模糊搜表`show tables like '*name*';`
2. 表结构信息`desc table_name;`
3. 分区信息`show partitions table_name`
4. 修改表名`alter table old_table_name rename to new_table_name;` 
5. 从查询语句给表插入数据`insert overwrite table table_name partition(dt) select & from table_name;`
6. 复制表结构`create table new_table_name like table_name;`
7. 添加字段`alter table table_name add columns(columns_values bigint comment 'comment_text');`
8. 修改字段`alter table table_name change old_column new_column string comment 'comment_text';`
9. 删除分区`alter table table_name drop partition(dt='2023-02-22');`
10. 添加分区`alter table table_name add partition(dt='2023-02-22');`
11. 删除空数据库`drop database myhivedatabase;`
12. 强制删除数据库`drop database myhivedatabase cascde;`
13. 删除表`drop table if exisit table_name;`
14. 建表`create table if not exisit table_name;`
15. 清空表`truncate table table_name;`

<h3 id="02">Hive查询语句</h3>
1. 分组`group by`
   ```select name from student group by sex having score>95```
2. 连接
   1. 内连接`inner join`
   2. 左连接`left join`
   3. 右连接`right join`
   4. 全外连接`full join`
3. 排序`order by`
   1. 升序`asc(ascend)`
   2. 降序`desc(descend)`
4. 排序
   1. 局部排序`sort by`, 基于mapreduce的内部排序，不是全局结果集的全排序
   2. 分区排序`distribute by`, 一般结合`sort by`使用进行分区排序

<h3 id="03">Hive函数</h3>
1. 聚合函数
2. 关系运算
