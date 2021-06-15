## 实验6（期末考核） 基于Oracle的公司人事信息管理数据库设计 
### 胡世林    201810414309     软工18-3
### 期末考核要求
```
自行设计一个信息系统的数据库项目，自拟某项目名称。
设计项目涉及的表及表空间使用方案。至少5张表和5万条数据，两个表空间。
设计权限及用户分配方案。至少两类角色，两个用户。
在数据库中建立一个程序包，在包中用PL/SQL语言设计一些存储过程和函数，实现比较复杂的业务逻辑，用模拟数据进行执行计划分析。
设计自动备份方案或则手工备份方案。
设计容灾方案。使用两台主机，通过DataGuard实现数据库整体的异地备份(可选)。
```

### 实验步骤

#### 1.表空间创建

```mysql
create or replace PACKAGE MyPack IS
  FUNCTION Get_HireDateTimePeopleNum(V_DEPARTMENT_ID NUMBER) RETURN NUMBER;
  PROCEDURE Get_Employees(V_EMPLOYEE_ID NUMBER);
END MyPack;
```

![avatar](/test6/pic1.png)


#### 2.创表
##### 2.1 dept表
![avatar](/test6/pic2.png)
##### 2.2 emp表
![avatar](/test6/pic3.png)
##### 2.3 salgrade表
![avatar](/test6/pic4.png)
##### 2.4 project表
![avatar](/test6/pic5.png)
##### 2.5 dept_job表
![avatar](/test6/pic6.png)

#### 3.数据插入
##### 3.1 salgrade表
![avatar](/test6/pic7.png)
##### 3.2 dept表
![avatar](/test6/pic8.png)
##### 3.3 emp表
![avatar](/test6/pic9.png)
共三万条数据
![avatar](/test6/pic10.png)
##### 3.4 dept_job表
![avatar](/test6/pic11.png)
共五百条数据
![avatar](/test6/pic12.png)
##### 3.5 project表
![avatar](/test6/pic13.png)
共两万条数据
![avatar](/test6/pic14.png)
#### 5.创建角色和权限分配
```
create user test1 identified by test;
grant select on "Reader" to test1;
grant select on "Book" to test1;
grant select on "ORDERS" to test1;
grant select on "ADMIN" to test1;
grant select on "LOGS" to test1;
```
![avatar](/test6/pic15.png)

#### 6.存储过程和函数
![avatar](/test6/pic16.png)
#### 7.备份(windows下)
```
@echo off
set t_date=%date% 
set t_time=%time%
set t_n=%t_date:~0,4%
set t_y=%t_date:~5,2% 
set t_r=%t_date:~8,2% 
set t_h=%t_time:~0,2%
set t_m=%t_time:~3,2%
set full_name=CTEurope%t_y%%t_r%%t_h%%t_m%
exp eutest/1@gentle file=%full_name%.dmp1
"C:\Program Files\WinRAR\Rar.exe" a -k -r -s -m1 %full_name%.rar %full_name%.dmp
del %full_name%.dmp
```
将这个bat文件添加到windows的任务计划中，设置每隔多少时间运行一次，备份文件会自动以当前时间来保存并压缩。
### 项目总结
通过本次实验，我完成了我完成了公司人事信息管理数据库的设计，为乐完成五张表的建立和五万条数据的插入，采用了随机时间和随机字符串来完成，设计了两类角色，两个用户，使用的存储过程来实现重复插入，最初在mysql上完成，最后转到Oracle来实现，是比较麻烦的。总的来说，还是很有收获的，希望下来能继续深入研究。