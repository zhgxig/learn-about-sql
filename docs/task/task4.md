#### 作业一(各部门工资最高的员工)
1.创建employee表
```
create table employee(
id int primary key,
name varchar(50),
salary int,
department_id int,
);
```

<pre>
+---------------+-------------+------+------+---------+-------+
| Field         | Type        | Null | Key  | Default | Extra |
+---------------+-------------+------+------+---------+-------+
| id            | int(11)     | NO   | PRI  | NULL    |       |
| name          | varchar(50) | YES  |      | NULL    |       |
| salary        | int(11)     | YES  |      | NULL    |       |
| department_id | int(11)     | YES  |      | NULL    |       |
+---------------+-------------+------+------+---------+-------+
</pre>


2.创建department表
```
create table department(
 id int primary key,
 name varchar(50));
```

<pre>
+-------+-------------+------+------+---------+-------+
| Field | Type        | Null | Key  | Default | Extra |
+-------+-------------+------+------+---------+-------+
| id    | int(11)     | NO   | PRI  | NULL    |       |
| name  | varchar(50) | YES  |      | NULL    |       |
+-------+-------------+------+------+---------+-------+
</pre>


3.employee插入数据
```
insert into employee
 values (1, "Joe", 70000, 1),
(2, "Henry", 80000, 2),
(3, "Sam", 60000, 2),
(4, "Max", 90000, 1)
;
```

<pre>
+----+-------+--------+---------------+
| id | name  | salary | department_id |
+----+-------+--------+---------------+
|  1 | Joe   |  70000 |             1 |
|  2 | Henry |  80000 |             2 |
|  3 | Sam   |  60000 |             2 |
|  4 | Max   |  90000 |             1 |
+----+-------+--------+---------------+
</pre>

4.department插入数据
```
insert into department
values (1, "IT"),
(2, "Sales");
```

<pre>
+----+-------+
| id | name  |
+----+-------+
|  1 | IT    |
|  2 | Sales |
+----+-------+
</pre>

5.找出每个部门工资最高的员工
```
SELECT d.name, e.Name ,e.salary
FROM employee e 
JOIN department d
ON e.department_id = d.id
WHERE salary IN
    (SELECT MAX(salary)
    FROM Employee
    GROUP BY department_id order by department_id);
```

<pre>
+-------+-------+--------+
| name  | Name  | salary |
+-------+-------+--------+
| IT    | Max   |  90000 |
| Sales | Henry |  80000 |
+-------+-------+--------+
</pre>


#### 作业二(改变相邻俩学生的座位)
1.创建seat表
```
create table seat(
id int primary key auto_increment,
student varchar(50));
```

<pre>
+---------+-------------+------+------+---------+----------------+
| Field   | Type        | Null | Key  | Default | Extra          |
+---------+-------------+------+------+---------+----------------+
| id      | int(11)     | NO   | PRI  | NULL    | auto_increment |
| student | varchar(50) | YES  |      | NULL    |                |
+---------+-------------+------+------+---------+----------------+
</pre>

2.插入数据
```
insert into seat 
values (1, "Abbot"),
(2, "Doris"),
(3, "Emerson"),
(4, "Green"),
(5, "Jeames");
```

<pre>
+----+---------+
| id | student |
+----+---------+
|  1 | Abbot   |
|  2 | Doris   |
|  3 | Emerson |
|  4 | Green   |
|  5 | Jeames  |
+----+---------+
</pre>


3.改变相邻俩学生的座位,如果学生人数是奇数，则不需要改变最后一个同学的座位.
```
SELECT (
    CASE WHEN id%2=1 and id = (SELECT COUNT(*) FROM seat) THEN id
	WHEN id%2 =1 THEN id+1
	ELSE id-1
	END
	) AS id,student
FROM seat
GROUP BY id
ORDER BY id;
```
<pre>
+----+---------+
| id | student |
+----+---------+
|  1 | Abbot   |
|  2 | Doris   |
|  3 | Emerson |
|  4 | Green   |
|  5 | Jeames  |
+----+---------+
</pre>


#### 作业三(分数排名)
1.创建score表
```
creat table score(
id int primary key auto_increment,
Score float(4));
```

<pre>
+-------+---------+------+------+---------+----------------+
| Field | Type    | Null | Key  | Default | Extra          |
+-------+---------+------+------+---------+----------------+
| id    | int(11) | NO   | PRI  | NULL    | auto_increment |
| Score | float   | YES  |      | NULL    |                |
+-------+---------+------+------+---------+----------------+
</pre>

2.插入数据
```
insert into score
values (1, 3.50),
(2, 3.65),
(3, 4.00),
(4, 3.85),
(5, 4.00), 
(6, 3.65);
```

<pre>
+----+-------+
| id | Score |
+----+-------+
|  1 |   3.5 |
|  2 |  3.65 |
|  3 |     4 |
|  4 |  3.85 |
|  5 |     4 |
|  6 |  3.65 |
+----+-------+
</pre>

3.编写一个 SQL 查询来实现分数排名。如果两个分数相同，则两个分数排名（Rank）相同。请注意，平分后的下一个名次应该是下一个连续的整数值。换句话说，名次之间不应该有“间隔”。
```
SELECT Score,(
	SELECT COUNT(DISTINCT(Score))+1
	FROM score
	WHERE Score>s1.Score
) AS RANK
FROM score AS s1
GROUP BY Score, id
ORDER BY Score DESC,Id ASC;
```

<pre>
+-------+------+
| Score | RANK |
+-------+------+
|     4 |    1 |
|     4 |    1 |
|  3.85 |    2 |
|  3.65 |    3 |
|  3.65 |    3 |
|   3.5 |    4 |
+-------+------+
</pre>

