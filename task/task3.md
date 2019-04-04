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

<pre>+---------+----------+
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