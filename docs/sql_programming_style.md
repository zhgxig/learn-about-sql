#### SQL编程风格

1.命名的建议
+ 使用统一的、描述性强的字段命名规则
+ 保证字段名是独一无二且不是保留字的，不要使用连续的下划线，不用下划线结尾
+ 最好以字母开头
```
id 标识符——user_id 用户标识 item_id 商品标识
at 表示某个事件发生的时间——ord_at 订单时间 exam_dt 考试时间
num 表示某事相关的数字——sale_num 销量
name 用字母表示名称——stu_name 学生名 等
```

2.格式建议
+ 最好使用标准SQL函数而不是特定供应商Oracle、Mysql等的函数以提高可移植性
+ 大小写的运用，系统关键字大写，字段表名小写
+ 灵活使用空格和缩进来增强可读性——两大法宝空白隔道与垂直间距

```
select name,id,sex
from (select *
from school_score
where class_cd=110)
where sex = 'man'
and exam_dt = '2016-06-01';

--空白隔道+垂直间距+大小写+缩进
SELECT name, id, sex
  FROM (SELECT *
          FROM school_score
         WHERE class_cd = 110)
 WHERE sex = 'man'
   AND exam_dt = '2016-06-01';
```

3.语法建议
+ 尽量使用BETWEEN而不是多个AND
+ 同样，使用 IN 而不是多个OR
+ 利用CASE语句嵌套处理更复杂的逻辑结构
+ 避免UNION语句与临时表
```
SELECT CASE postcode
       WHEN 'BN1' THEN 'Brighton'
       WHEN 'EH1' THEN 'Edinburgh'
       END AS city
  FROM office_locations
 WHERE country = 'United Kingdom'
   AND opening_time BETWEEN 8 AND 9
   AND postcode IN ('EH1', 'BN1', 'NN1', 'KW1');
```