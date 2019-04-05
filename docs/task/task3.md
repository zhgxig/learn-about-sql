#### 作业一
1.创建表(cources)
```
create table courses(
student varchar(50) not null,
class varchar(50) not null
);
```

2.插入数据
```
insert into courses values("A", "Math");

insert into courses values("B", "English");

insert into courses values("C", "Math");

insert into courses values("D", "Biology");

insert into courses values("E", "Math");

insert into courses values("F", "Computer");

insert into courses values("G", "Math");

insert into courses values("H", "Math");

insert into courses values("I", "Math");

insert into courses values("A", "Math");
```

<pre>
+---------+----------+
| student | class    |
+---------+----------+
| A       | Math     |
| B       | English  |
| C       | Math     |
| D       | Biology  |
| E       | Math     |
| F       | Computer |
| G       | Math     |
| H       | Math     |
| I       | Math     |
| A       | Math     |
+---------+----------+
</pre>

3.列出所有超过或等于5名学生的课(学生在每个课中不应被重复计算.)
```
select c_r.class 
from (select distinct * 
    from courses) as c_r 
group by c_r.class  
having count(c_r.class) >= 5;
```
<pre>
+-------+
| class |
+-------+
| Math  |
+-------+
</pre>

#### 作业二
1.创建表(salary)
```
create table salary(
id int primary key,
name varchar(50) not null,
sex varchar(50) not null,
salary varchar(50) not null
);

```

2.插入数据
```
insert into salary
values (1, "A", "m", 2500),
(2, "B", "f",  1500),
(3, "C", "m",  5500),
(4, "D", "f",  500);
```
<pre>
+----+------+-----+--------+
| id | name | sex | salary |
+----+------+-----+--------+
|  1 | A    | m   |   2500 |
|  2 | B    | f   |   1500 |
|  3 | C    | m   |   5500 |
|  4 | D    | f   |    500 |
+----+------+-----+--------+
</pre>

3.交换所有的 f 和 m 值
```
select id, name, 
case  when sex = "f" then "m" else "f" end 
sex, salary from salary;
```
<pre>
+----+------+------+--------+
| id | name | sex  | salary |
+----+------+------+--------+
|  1 | A    | f    |   2500 |
|  2 | B    | m    |   1500 |
|  3 | C    | f    |   5500 |
|  4 | D    | m    |    500 |
+----+------+------+--------+
</pre>

#### 作业三
1.创建表(person、address)
```
创建person

create table person(
Personid int primary key,
FirstName varchar(50) not null,
LastName varchar(50) not null,
);

创建address

create table address(
AddressId int primary key,
PersonId int not null,
City varchar(50) not null,
State varchar(50) not null
;
```

+ person 表
<pre>
+-----------+-------------+------+------+---------+-------+
| Field     | Type        | Null | Key  | Default | Extra |
+-----------+-------------+------+------+---------+-------+
| Personid  | int(11)     | NO   | PRI  | NULL    |       |
| FirstName | varchar(50) | NO   |      | NULL    |       |
| LastName  | varchar(50) | NO   |      | NULL    |       |
+-----------+-------------+------+------+---------+-------+
</pre>


+ address 表
<pre>
+-----------+-------------+------+------+---------+-------+
| Field     | Type        | Null | Key  | Default | Extra |
+-----------+-------------+------+------+---------+-------+
| AddressId | int(11)     | NO   | PRI  | NULL    |       |
| PersonId  | int(11)     | NO   |      | NULL    |       |
| City      | varchar(50) | NO   |      | NULL    |       |
| State     | varchar(50) | NO   |      | NULL    |       |
+-----------+-------------+------+------+---------+-------+
</pre>

2.person插入数据
```
insert into person
values (1, "xiao", "ming"),
(2, "xiao", "hong"),
(3, "xiao", "hei");
```
<pre>
+----------+-----------+----------+
| Personid | FirstName | LastName |
+----------+-----------+----------+
|        1 | xiao      | ming     |
|        2 | xiao      | hong     |
|        3 | xiao      | hei      |
+----------+-----------+----------+
</pre>

3.address插入数据
```
insert into address
values (1, 3, "shenzhen", "guangdong"),
(2, 2, "nanchang", "jiangxi"),
(3, 1, "wuhan", "hubei");
```
<pre>
+-----------+-------------+------+------+---------+-------+
| Field     | Type        | Null | Key  | Default | Extra |
+-----------+-------------+------+------+---------+-------+
| AddressId | int(11)     | NO   | PRI  | NULL    |       |
| PersonId  | int(11)     | NO   |      | NULL    |       |
| City      | varchar(50) | NO   |      | NULL    |       |
| State     | varchar(50) | NO   |      | NULL    |       |
+-----------+-------------+------+------+---------+-------+
</pre>

4.无论 person 是否有地址信息，都需要基于上述两表提供 person 的以下信息：FirstName, LastName, City, State
```
select ps.FirstName, ps.LastName, ad.City, ad.State from person as ps 
join address as ad 
on ps.PersonId = ad.PersonId;
```
<pre>
+-----------+----------+----------+-----------+
| FirstName | LastName | City     | State     |
+-----------+----------+----------+-----------+
| xiao      | hei      | shenzhen | guangdong |
| xiao      | hong     | nanchang | jiangxi   |
| xiao      | ming     | wuhan    | hubei     |
+-----------+----------+----------+-----------+
</pre>


#### 作业四
1.创建表(email)
```
CREATE TABLE email (
ID INT NOT NULL PRIMARY KEY,
Email VARCHAR(255)
```

2.插入数据
```
INSERT INTO email VALUES('1','a@b.com');
INSERT INTO email VALUES('2','c@d.com');
INSERT INTO email VALUES('3','a@b.com');
```

3.编写一个 SQL 查询，来删除 email 表中所有重复的电子邮箱，重复的邮箱里只保留 Id 最小 的那个.
```
delete e1 
from email e1, email e2 
where e1.email=e2.email and e1.id>e2.id;
```














