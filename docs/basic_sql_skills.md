#### sql

1.sql
>SQL，指结构化查询语言，全称是 Structured Query Language

>RDBMS 数据库程序，RDBMS 指关系型数据库管理系统，全称 Relational Database Management System。

>SQL 对大小写不敏感：SELECT 与 select 是相同的。

+ SELECT - 从数据库中提取数据
+ UPDATE - 更新数据库中的数据
+ DELETE - 从数据库中删除数据
+ INSERT INTO - 向数据库中插入新数据
+ CREATE DATABASE - 创建新数据库
+ ALTER DATABASE - 修改数据库
+ CREATE TABLE - 创建新表
+ ALTER TABLE - 变更（改变）数据库表
+ DROP TABLE - 删除表
+ CREATE INDEX - 创建索引（搜索键）
+ DROP INDEX - 删除索引

2.create database


3.create table


4.simple select 
>SELECT 语句用于从数据库中选取数据

+ 1. `SELECT DISTINCT`  语句用于返回唯一不同的值。
    ```
    SELECT DISTINCT column_name,column_name
    FROM table_name;
    ```
+ 2. `WHERE` 子句 用于过滤记录。
    ```
    SELECT * FROM Websites WHERE id=1;
    ```
+ 3. `AND & OR` 运算符用于基于一个以上的条件对记录进行过滤

+ 4. `ORDER BY` 关键字用于对结果集进行排序。
    ```
    SELECT column_name,column_name
    FROM table_name
    ORDER BY column_name,column_name ASC|DESC;
    ```
    
+ 5. `INSERT INTO` 语句用于向表中插入新记录。
    ```
    INSERT INTO table_name
    VALUES (value1,value2,value3,...);
    
    INSERT INTO table_name (column1,column2,column3,...)
    VALUES (value1,value2,value3,...);
    
    INSERT INTO Websites (name, url, alexa, country)
    VALUES ('百度','https://www.baidu.com/','4','CN');
    ```
    
+ 6. `UPDATE` 语句用于更新表中已存在的记录。
    ```
    UPDATE Websites 
    SET alexa='5000', country='USA' 
    WHERE name='菜鸟教程';
    ```

+ 7. `DELETE` 语句用于删除表中的行。
    ```
    DELETE FROM Websites
    WHERE name='百度' AND country='CN';
    ```

5.基本运算符  

|运算符|描述|
|---|---|
|=|等于|
|<>|不等于 !=|
|>|大于|
|<|小于|
|>=|大于等于|
|<=|小于等于|
|between|在某个范围内|
|like|模糊|
|in|指定针对某个列的多个可能值|