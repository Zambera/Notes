# MySQL

~~~~sql
什么是关系型数据库
什么是用户

--什么是字段
--数据库中的字段类型  整数int bigint 浮点数decimal(m,p) 字符串char varchar 日期datetime timestamp
--表和字段的命名规范

什么是SQL
表结构*  增删改查
表结构   可视化增删改查
~~~~



常用命令

- 数据库连接

~~~~sql
mysql -u root -p //连接数据库
mysql -h 192.168.12.151 -u root -p //连接远程数据库
~~~~



查看数据库	show databases

创建数据库 create database name

删除数据库 drop database name

切换数据库 use databasename

查询当前数据库 select database();



DQL数据库查询语言 select

DML数据库管理操作insert update delete

DDL数据库定义语言 create table drop alter

DCL数据库控制语言 commit rollback



表结构的管理

表结构查询	

~~~~sql
desc name;
~~~~

表结构新建	

~~~~sql
create name（
​	字段名 字段类型 [属性] [约束],
​	字段名 字段类型 [属性] [约束]
);
create table dept(
	id int not null,
    dept_name varchar(20)
)
show tables;
表名和字段名必须使用小写字母和数字
禁止数字开头
禁止下划线之间只有一个数字 level_3_name 不行
单词和单词之间使用下划线
表名不要使用复数
~~~~

表结构删除

~~~~sql
insert into tablename values(01,'cacas',20,1,003,'hsa');//一一对应
insert into emps(empno,age,address) values(04,23,'csc');

select dept_name,address from dept;
update dept set dept_address='csac' where id=01;//不写where条件，修改所有内容
delete from dept where id=01;
~~~~

浮点 float double decimal(有效数，小数位数)

char固定长度 查询速度更快 varchar(<5000)可变长度

date年月日 datetime年月日时分秒 timestamp时间戳 time时分秒

text

logtext



### 查询

~~~~sql
--mysql默认不区分大小写
select * from emp;--查询所有列，不建议使用
select empno from emp;--查询指定列
select empno as 编号,empname 员工名称 from emp;--取别名 as 可省略
select * from emp where ename='king';--条件查询，精确匹配
SELECT * FROM emp WHERE sal>2000;--范围查询
SELECT * FROM emp WHERE sal>2000 and sal<3000;--多条件查询 and or
SELECT * FROM emp WHERE hiredate>'1987-1-1';--日期查询

--去重查询
select distinct job from emp;
SELECT DISTINCT job,deptno FROM emp;--多个条件都相同才去重
--null条件查询
SELECT * FROM emp WHERE comm='';
SELECT * FROM emp WHERE comm=null;
SELECT * FROM emp WHERE comm=not null;

SELECT ename,sal,sal*12,(sal+IFNULL(comm,0)) *13 FROM emp;
--字符串连接
SELECT ename,job,CONCAT(ename,'的工作是',job) FROM emp;
--结果集是指 查询返回的二维表数据
--模糊查询
--%任意个字符_任意一个字符 like模糊匹配
SELECT * FROM emp WHERE ename LIKE 'C%';
--范围比较
SELECT * FROM emp WHERE sal BETWEEN 2975 and 3000;
select * from emp where sal >= 2975 and sal <=3000;
-- in 
SELECT * FROM emp WHERE deptno in (10,20,30);
-- 日期查询
-- 需要使用日期相关的函数（api 字符串函数 数字函数 日期函数
SELECT * FROM emp WHERE YEAR(hiredate)='1981';--==
SELECT * FROM emp WHERE hiredate >'1981-1-1' and hiredate <'1981-12-31';
SELECT * FROM emp WHERE MONTH(hiredate)=11;
SELECT * FROM emp WHERE DAY(hiredate)=22;
SELECT * FROM emp WHERE LAST_DAY(hiredate) =hiredate;--返回当月最后一天的日期
--日期格式化 date_format
--%Y 年 %m 月 %d 天 %h 时 %i 分 %s 秒
DATE_FORMAT(hiredate,'%Y-%y-%M-%m-%D-%d')-- 1981-81-February-02-20th-20

--排序查询  ORDER BY 字段  asc desc降序
SELECT * FROM emp ORDER BY hiredate asc,sal desc;

-- 聚合函数 max() min() avg()  sum()
-- count()参数为某一列时，统计该列的非空记录数

--子查询 查找返回最高的
SELECT * FROM emp WHERE sal =(
	SELECT max(sal) FROM emp
)

--分组查询
SELECT deptno,COUNT(*),max(sal) FROM emp GROUP BY deptno;-- 单字段
-- 分组结果筛选
SELECT avg(sal),deptno FROM emp GROUP BY deptno HAVING AVG(sal)<2000;
~~~~

#### 多表查询

~~~~sql
-- 笛卡尔集 A+B 3*3 直接
select * from emp,dept;
-- 内连接 where 关联条件   
SELECT count(*),dname FROM emp a,dept b WHERE a.deptno=b.deptno GROUP BY a.deptno
-- inner join on
SELECT * FROM emp a inner join dept b on a.deptno=b.deptno; 
-- 外连接 左右 主表完全显示 匹配副表的相同字段
SELECT * FROM emp a LEFT|RIGHT JOIN dept b on a.deptno=b.deptno;
~~~~

#### 合并查询

~~~~sql
union -- 把两个完成不同的表结果合并到一个结果集
union all -- 不去重
select job from emp 
union
select dname from dept
~~~~

#### 分页查询

~~~~sql
limit
select * from emp limit 2,2 --offset,count offset =(i-1)*count
select * from emp limit 5
~~~~

#### 高级子查询

```mysql
-- 单行单列

-- 多行单列  all(全部) any(任意)
select * from emp where sal>
all(select sal from emp where deptno=20);
-- 单行多列
select * from emp where (job,deptno) = (select job,deptno from emp where ename = 'smith')
-- 多行多列
select * from emp where (job,deptno) in (select job,deptno from emp)
```

