## 实验4：对象管理

### 软件工程三班 胡世林 201810414309
### 实验目的
了解Oracle表和视图的概念，学习使用SQL语句Create Table创建表，学习Select语句插入，修改，删除以及查询数据，学习使用SQL语句创建视图，学习部分存储过程和触发器的使用。
### 实验场景
假设有一个生产某个产品的单位，单位接受网上订单进行产品的销售。通过实验模拟这个单位的部分信息：员工表，部门表，订单表，订单详单表。
### 实验内容
#### 录入数据
要求至少有1万个订单，每个订单至少有4个详单。至少有两个部门，每个部门至少有1个员工，其中只有一个人没有领导，一个领导至少有一个下属，并且它的下属是另一个人的领导（比如A领导B，B领导C）。
#### 序列的应用
插入ORDERS和ORDER_DETAILS 两个表的数据时，主键ORDERS.ORDER_ID, ORDER_DETAILS.ID的值必须通过序列SEQ_ORDER_ID和SEQ_ORDER_ID取得，不能手工输入一个数字。
#### 触发器的应用：
维护ORDER_DETAILS的数据时（insert,delete,update）要同步更新ORDERS表订单应收货款ORDERS.Trade_Receivable的值。
#### 查询数据：
```
1.查询某个员工的信息
2.递归查询某个员工及其所有下属，子下属员工。
3.查询订单表，并且包括订单的订单应收货款: Trade_Receivable= sum(订单详单表.ProductNum*订单详单表.ProductPrice)- Discount。
4.查询订单详表，要求显示订单的客户名称和客户电话，产品类型用汉字描述。
5.查询出所有空订单，即没有订单详单的订单。
6.查询部门表，同时显示部门的负责人姓名。
7.查询部门表，统计每个部门的销售总金额。
```
### 实验步骤
#### 1.用自己的用户连接上数据库 

![avatar](/test4/pic1.png)

#### 2.删除表序列

![avatar](/test4/pic2.png)

#### 3.创建departments表

![avatar](/test4/pic3.png)

#### 4.创建employee表

![avatar](/test4/pic4.png)
![avatar](/test4/pic5.png)

#### 5.在employees表创建索引

![avatar](/test4/pic6.png)
![avatar](/test4/pic7.png)

#### 6.创建products表

![avatar](/test4/pic8.png)

#### 7.创建order_id_temp临时表

![avatar](/test4/pic9.png)

#### 8.创建orders表

![avatar](/test4/pic10.png)

#### 9.创建本地分区索引并创建表order_details和对应索引

![avatar](/test4/pic11.png)
![avatar](/test4/pic12.png)
![avatar](/test4/pic13.png)
![avatar](/test4/pic14.png)

#### 10.创建三个触发器

![avatar](/test4/pic15.png)
![avatar](/test4/pic16.png)
![avatar](/test4/pic17.png)

#### 11. DDL for Sequence

![avatar](/test4/pic18.png)

#### 12. DDL for View VIEW_ORDER_DETAILS

![avatar](/test4/pic19.png)

#### 13. 插入DEPARTMENTS，EMPLOYEES数据

![avatar](/test4/pic20.png)
![avatar](/test4/pic21.png)

#### 14.批量插入订单数据，注意ORDERS.TRADE_RECEIVABLE（订单应收款）的自动计算,注意插入数据的速度

![avatar](/test4/pic22.png)

#### 15.最后动态增加一个PARTITION_BEFORE_2018分区

![avatar](/test4/pic23.png)

#### 16.一切就绪，开始测试：以下时间在0.02秒以内才正常：（id取值从1到20000000）

![avatar](/test4/pic24.png)
![avatar](/test4/pic25.png)
![avatar](/test4/pic26.png)

#### 17.递归查询某个员工及其所有下属，子下属员工

![avatar](/test4/pic27.png)

#### 18.查询分区表情况:

![avatar](/test4/pic28.png)

#### 19.查询分区索引情况:

![avatar](/test4/pic29.png)

#### 20.查询一个分区中的数据

![avatar](/test4/pic30.png)


#### 21.统计用户的所有表：

![avatar](/test4/pic31.png)

#### 22.统计完成后，查询表的统计信息：

![avatar](/test4/pic32.png)
![avatar](/test4/pic33.png)
![avatar](/test4/pic34.png)
![avatar](/test4/pic35png)
![avatar](/test4/pic36.png)
![avatar](/test4/pic37.png)

### 实验总结
在本次的实验中，我学习了Oracle表和视图的概念，学习使用SQL语句创建视图，学习部分存储过程和触发器的使用。在实验的过程中就是步骤有点多。