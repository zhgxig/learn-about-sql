#### 项目一
1.创建表
```
CREATE TABLE email (
ID INT NOT NULL PRIMARY KEY,
Email VARCHAR(255)
);
```
2.插入数据
```
INSERT INTO email VALUES('1','a@b.com');
INSERT INTO email VALUES('2','c@d.com');
INSERT INTO email VALUES('3','a@b.com');
```
3.查找 Email 表中所有重复的电子邮箱
```
select 
    Email 
from email 
group by Email 
having count(Email) > 1;
```


#### 项目二
1.创建表
```
CREATE TABLE World (
name VARCHAR(50) NOT NULL,
continent VARCHAR(50) NOT NULL,
area INT NOT NULL,
population INT NOT NULL,
gdp INT NOT NULL
);
```
2.插入数据
```
INSERT INTO World
  VALUES('Afghanistan','Asia',652230,25500100,20343000);
INSERT INTO World 
  VALUES('Albania','Europe',28748,2831741,12960000);
INSERT INTO World 
  VALUES('Algeria','Africa',2381741,37100000,188681000);
INSERT INTO World
  VALUES('Andorra','Europe',468,78115,3712000);
INSERT INTO World
  VALUES('Angola','Africa',1246700,20609294,100990000);
```
3.输出国家的面积超过300万平方公里，或者(人口超过2500万并且gdp超过2000万)
```
select * 
from World 
where area > 3000000 
or (population > 25000000 and gdp > 2000000);
```