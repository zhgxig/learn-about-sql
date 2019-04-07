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


#### 作业四(行程和用户)
1.创建trips表
```
CREATE TABLE trips(
Id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
Client_Id INT NOT NULL,
Driver_Id INT NOT NULL,
City_Id INT NOT NULL,
Status ENUM('completed', 'cancelled_by_driver', 'cancelled_by_client') NOT NULL,
Request_at DATE DEFAULT NULL);
```

<pre>
+------------+---------------------------------------------------------------+------+------+---------+----------------+
| Field      | Type                                                          | Null | Key  | Default | Extra          |
+------------+---------------------------------------------------------------+------+------+---------+----------------+
| Id         | int(11)                                                       | NO   | PRI  | NULL    | auto_increment |
| Client_Id  | int(11)                                                       | NO   |      | NULL    |                |
| Driver_Id  | int(11)                                                       | NO   |      | NULL    |                |
| City_Id    | int(11)                                                       | NO   |      | NULL    |                |
| Status     | enum(&apos;completed&apos;,&apos;cancelled_by_driver&apos;,&apos;cancelled_by_client&apos;) | NO   |      | NULL    |                |
| Request_at | date                                                          | YES  |      | NULL    |                |
+------------+---------------------------------------------------------------+------+------+---------+----------------+
</pre>

2.创建user表
```
CREATE TABLE Users(
Users_Id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
Banned VARCHAR(10) NOT NULL,
Role ENUM('client', 'driver', 'partnet') NOT NULL);
```

<pre>
+----------+-----------------------------------+------+------+---------+----------------+
| Field    | Type                              | Null | Key  | Default | Extra          |
+----------+-----------------------------------+------+------+---------+----------------+
| Users_Id | int(11)                           | NO   | PRI  | NULL    | auto_increment |
| Banned   | varchar(10)                       | NO   |      | NULL    |                |
| Role     | enum(&apos;client&apos;,&apos;driver&apos;,&apos;partnet&apos;) | NO   |      | NULL    |                |
+----------+-----------------------------------+------+------+---------+----------------+
</pre>

3.插入trips的数据
```
INSERT INTO trips
VALUES (1,1,10,1,'completed','2013-10-01'),
(2,2,11,1, 'cancelled_by_driver','2013-10-01'),
(3,3,12,6,'completed','2013-10-01'),
(4,4,13,6,'cancelled_by_client','2013-10-01'),
(5,1,10,1,'completed','2013-10-02'),
(6,2,11,6,'completed','2013-10-02'),
(7,3,12,6,'completed','2013-10-02'),
(8,2,12,12,'completed','2013-10-03'),
(9,3,10,12,'completed','2013-10-03'),
(10,4,13,12, 'cancelled_by_driver','2013-10-03');
```

<pre>
+----+-----------+-----------+---------+---------------------+------------+
| Id | Client_Id | Driver_Id | City_Id | Status              | Request_at |
+----+-----------+-----------+---------+---------------------+------------+
|  1 |         1 |        10 |       1 | completed           | 2013-10-01 |
|  2 |         2 |        11 |       1 | cancelled_by_driver | 2013-10-01 |
|  3 |         3 |        12 |       6 | completed           | 2013-10-01 |
|  4 |         4 |        13 |       6 | cancelled_by_client | 2013-10-01 |
|  5 |         1 |        10 |       1 | completed           | 2013-10-02 |
|  6 |         2 |        11 |       6 | completed           | 2013-10-02 |
|  7 |         3 |        12 |       6 | completed           | 2013-10-02 |
|  8 |         2 |        12 |      12 | completed           | 2013-10-03 |
|  9 |         3 |        10 |      12 | completed           | 2013-10-03 |
| 10 |         4 |        13 |      12 | cancelled_by_driver | 2013-10-03 |
+----+-----------+-----------+---------+---------------------+------------+
</pre>



4.插入user的数据
```
INSERT INTO Users
VALUES (1, 'No', 'client'),
(2, 'Yes', 'client'),
(3, 'No', 'client'),
(4, 'No', 'client'),
(10, 'No', 'driver'),
(11, 'No', 'driver'),
(12, 'No', 'driver'),
(13, 'No', 'driver');
```

<pre>
+----------+--------+--------+
| Users_Id | Banned | Role   |
+----------+--------+--------+
|        1 | No     | client |
|        2 | Yes    | client |
|        3 | No     | client |
|        4 | No     | client |
|       10 | No     | driver |
|       11 | No     | driver |
|       12 | No     | driver |
|       13 | No     | driver |
+----------+--------+--------+
</pre>


5.查出 2013年10月1日 至 2013年10月3日 期间非禁止用户的取消
```
SELECT t.Request_at AS 'Day', ROUND((SUM(CASE WHEN t.Status LIKE 'cancelled%' THEN 1 ELSE 0 END))/COUNT(*),2) AS 'Cancellation Rate'  FROM Trips AS t INNER JOIN User AS u  ON u.Users_Id = t.Client_Id AND u.Banned = 'No'  
GROUP BY t.Request_at 
order by t.Request_at;
```

<pre>
+------------+-------------------+
| Day        | Cancellation Rate |
+------------+-------------------+
| 2013-10-01 |              0.33 |
| 2013-10-02 |              0.00 |
| 2013-10-03 |              0.50 |
+------------+-------------------+
</pre>



#### 作业五(各部门前3高工资的员工)

1.各部门前3高工资的员工
```
SELECT d.name, e.Name ,e.salary
FROM employee e 
JOIN department d
ON e.department_id = d.id
WHERE salary IN
    (select salary 
    from employee 
    group by department_id, salary
    order by department_id, salary desc
    having count(distinct department_id) <= 3 
    )
order by e.department_id asc, e.salary desc;
```

#### 作业六(分数排名)

1.实现排名功能，但是排名是非连续的
```
SELECT Score,
        (SELECT COUNT(Score)
            FROM score AS s2 
            WHERE s2.Score>=s1.Score
        ) 
FROM score AS s1
ORDER BY Score DESC
; 
```