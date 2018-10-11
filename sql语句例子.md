###查询出s_emp表中所有的员工信息
~~~
 SELECT  *  FROM  s_emp
~~~
###查询出s_emp表中所有的员工的部门ID，工资
~~~
SELECT  dept_id , salary  FROM  s_emp
~~~
###查询出s_emp表中所有的员工的年薪
~~~
SELECT  salary*12  FROM  s_emp
~~~
###括号可以改变运算符运算的优先顺序
~~~
SELECT  last_name, salary, 12 * (salary + 100) FROM   s_emp;
~~~
###查询出s_emp表中所有的员工的姓名
~~~
SELECT firname_name || last_name FROM  s_emp
给列起别名
SELECT firname_name || last_name   “姓名”  FROM  s_emp
~~~
###查询出s_emp表中所有的员工的工资
~~~
SELECT  last_name, salary*commission_pct/100  “工资” FROM  s_emp;
空值的处理
SELECT last_name , salary+salary*NVL(commission_pct,0)/100 FROM  s_emp;
~~~
###查询出s_dept表的部门名称
~~~
SELECT  name  FROM   s_dept;
去掉重复行
SELECT  DISTINCT name FROM   s_dept;
~~~
###查询出s_emp表中所有的员工的部门ID及职称()去掉多列重复行
~~~
SELECT    DISTINCT dept_id, title  FROM   s_emp;
~~~
##条件查询
###查询s_emp表要求输出员工姓名(firs_name、last_name)和实际工资(基本工资+提成)
~~~
~~~
###查询基本语法 --- 查询出s_emp表中dept_id为41的员工信息
####SELECT <列名> FROM <表名> [WHERE <查询条件表达式>]
~~~
SELECT * FROM S_emp WHERE dept_id= 41
~~~
### WHERE条件查询
###查询出s_emp表中last_name为Smith的员工的信息
~~~
SELECT *  FROM s_emp WHERE last_name = 'Smith'
~~~
###查询出s_emp表中部门ID为50并且工资大于1500的员工的信息:
~~~
SELECT * FROM s_emp WHERE salary>1500 and dept_id=50
~~~
### WHERE条件查询-BETWEEN&IN
### 查询出s_emp表中工资在1500到2000之间的员工信息
~~~
SELECT * FROM s_emp WHERE salary between 1500  and 2000
~~~
###查询出s_dept表中region_id为1，3的部门信息
~~~
SELECT * FROM s_dept WHERE region_id in (1,3)
~~~
### WHERE条件查询-like
### 查询出s_emp表中姓中含有字母a的员工信息
~~~
SELECT * FROM s_emp WHERE last_name like '%a%'
~~~
###查询出s_emp表姓中第二个字母为a的员工信息
~~~
SELECT * FROM s_emp WHERE last_name like '_a%'
~~~
###查询出当前用户下所有以‘s_’开头的表
~~~
SELECT table_name FROM user_tables WHERE table_name like 'S\_%' escape '\'
~~~
###空值的查询
### 查询出s_emp表中非销售职位的员工信息
~~~
SELECT * FROM s_emp WHERE commission_pct is  null
~~~
##查询结果排序
### 查询出s_emp表将部门ID为41的员工的工资按从高到低排列显示出来
~~~
SELECT * FROM s_emp WHERE dept_id=41 ORDER BY salary DESC
~~~
## 函数
~~~
单行函数
Character
Number
Date
Conversion
多行函数
Group
字符函数
LOWER   将字符串转换成小写 
UPPER   将字符串变为大写 
INITCAP 将字符串的第一个字母变为大写 
CONCAT  拼接两个字符串，与 || 相同 
SUBSTR  取字符串的子串 
LENGTH  以字符给出字符串的长度 
NVL 以一个值来替换空值
~~~
###数字函数
~~~
ROUND(value,precision)   按precision 精度4舍5入  
TRUNC(value,precision)    按precision 截取value
~~~
###Round&Trunc函数
~~~
ROUND (45.923, 2)       45.92
ROUND (45.923, 0)       46
ROUND (45.923, -1)      50
TRUNC (45.923, 2)       45.92
TRUNC (45.923)          45
TRUNC (45.923, -1)      40
~~~
###日期函数
~~~
MONTHS_BETWEEN(date2,date1)     给出 Date2 - date1的月数
ADD_MONTHS      增加或减去月份
NEXT_DAY ( date,’day’)      给出日期date之后下一天的日期
LAST_DAY(date)      返回日期所在月的最后一天

MONTHS_BETWEEN(‘01-SEP-95’,‘11-JAN-94’)        19.774194
ADD_MONTHS('11-JAN-94',6)       '11-JUL-94‘
NEXT_DAY('01-SEP-95','FRIDAY')      '08-SEP-95‘
LAST_DAY('01-SEP-95')       '30-SEP-95'
~~~
###转换函数
~~~
TO_CHAR(date, 'fmt')       转换日期格式到字符串
~~~
###转换函数
~~~
TO_NUMBER(‘String’)             转换字符串到数字 
TO_DATE(‘String’)             转换字符串到日期格式 
SELECT to_date(‘2009-09-22’,’yyyy-mm-dd’) FROM dual
~~~
###转换函数嵌套
### 查询员工表中manager_id为空的员工查询出来，并将空列的值置为“No Manager”
~~~
SELECT  last_name,NVL(TO_CHAR(manager_id),'No Manager') FROM s_emp WHERE manager_id IS NULL;
~~~
##关联查询
### 简单关联查询的语法
~~~
SELECT   table.column, table.column FROM  table1, table2
WHERE    table1.column1 = table2.column2
~~~
###查询员工表中last_name为’Biri’的员工的last_name与部门名称查询出来
~~~
SELECT e.last_name , d.name FROM  s_emp e , s_dept d  WHERE  e.dept_id = d.id  and e.last_name = ‘Biri’
~~~