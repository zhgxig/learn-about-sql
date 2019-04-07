
1. SQL SELECT TOP 子句
```
SELECT column_name(s)
FROM table_name
LIMIT number;
```

2.  SQL LIKE 操作符
```
SELECT * FROM Websites
WHERE name NOT LIKE '%oo%';
```
    
3. SQL 通配符
>通配符可用于替代字符串中的任何其他字符

```
SELECT * FROM Websites
WHERE name LIKE '_oogle';

SELECT * FROM Websites
WHERE name REGEXP '^[^A-H]';
```

|通配符 |描述 |
|--- |--- |
|% |替代0个或多个字符 |
|_ |替代一个字符 |
|[charlist] |字符列中的任何单一字符 |
|[^charlist]或[!charlist] |不在字符列中的任何单一字符 |
    
4. SQL IN 操作符
>IN 操作符允许您在 WHERE 子句中规定多个值。

```
SELECT * FROM Websites
WHERE name IN ('Google','菜鸟教程');
```
    
5. SQL BETWEEN 操作符
>BETWEEN 操作符选取介于两个值之间的数据范围内的值。这些值可以是数值、文本或者日期。

```
SELECT * FROM Websites
WHERE (alexa BETWEEN 1 AND 20)
AND country NOT IN ('USA', 'IND');

SELECT * FROM Websites
WHERE name BETWEEN 'A' AND 'H';

SELECT * FROM access_log
WHERE date BETWEEN '2016-05-10' AND '2016-05-14';
```
    
6. SQL 别名
>通过使用 SQL，可以为表名称或列名称指定别名。基本上，创建别名是为了让列名称的可读性更强。

```
SELECT name AS n, country AS c
FROM Websites;

SELECT name, CONCAT(url, ', ', alexa, ', ', country) AS site_info
FROM Websites;

SELECT w.name, w.url, a.count, a.date 
FROM Websites AS w, access_log AS a 
WHERE a.site_id=w.id and w.name="菜鸟教程";
```

+ 在查询中涉及超过一个表
+ 在查询中使用了函数
+ 列名称很长或者可读性差
+ 需要把两个列或者多个列结合在一起


7. SQL 连接(JOIN)
>SQL join 用于把来自两个或多个表的行结合起来。

```
SELECT Websites.id, Websites.name, access_log.count, access_log.date
FROM Websites
INNER JOIN access_log
ON Websites.id=access_log.site_id;
```

+ INNER JOIN：如果表中有至少一个匹配，则返回行
+ LEFT JOIN：即使右表中没有匹配，也从左表返回所有的行
+ RIGHT JOIN：即使左表中没有匹配，也从右表返回所有的行
+ FULL JOIN：只要其中一个表中存在匹配，则返回行


8. SQL INNER JOIN 关键字
>INNER JOIN 关键字在表中存在至少一个匹配时返回行。

```
SELECT Websites.name, access_log.count, access_log.date
FROM Websites
INNER JOIN access_log
ON Websites.id=access_log.site_id
ORDER BY access_log.count;
```


9. SQL LEFT JOIN 关键字
>LEFT JOIN 关键字从左表（table1）返回所有的行，即使右表（table2）中没有匹配。如果右表中没有匹配，则结果为 NULL。

```
SELECT Websites.name, access_log.count, access_log.date
FROM Websites
LEFT JOIN access_log
ON Websites.id=access_log.site_id
ORDER BY access_log.count DESC;
```


10.  SQL RIGHT JOIN 关键字
>RIGHT JOIN 关键字从右表（table2）返回所有的行，即使左表（table1）中没有匹配。如果左表中没有匹配，则结果为 NULL。

```
SELECT Websites.name, access_log.count, access_log.date
FROM access_log
RIGHT JOIN Websites
ON access_log.site_id=Websites.id
ORDER BY access_log.count DESC;
```


11.  SQL FULL OUTER JOIN 关键字
>FULL OUTER JOIN 关键字只要左表（table1）和右表（table2）其中一个表中存在匹配，则返回行.
>FULL OUTER JOIN 关键字结合了 LEFT JOIN 和 RIGHT JOIN 的结果。

```
SELECT Websites.name, access_log.count, access_log.date
FROM Websites
FULL OUTER JOIN access_log
ON Websites.id=access_log.site_id
ORDER BY access_log.count DESC;
```