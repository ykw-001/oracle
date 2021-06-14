
期末项目设计报告

题    目	基于Oracle的借书管理系统的数据库设计


课    程	Oracle数据库应用

学    院	信息科学与工程学院

专    业	软件工程	年级	2018级

学生姓名	晏康文	学号	201810414225

指导教师	赵卫东	职称	副教授


评分项	评分标准	满分	得分

文档整体	文档内容详实、规范，美观大方	10

表设计	表，表空间设计合理，数据合理	20

用户管理	权限及用户分配方案设计正确	10

PL/SQL设计	存储过程和函数设计正确	25

备份方案	备份方案设计正确	25

得分合计

2021  06月  10 日



一、方案图表设计

根据所要实现的功能设计，可能建立它们之间的关系，进而实现逻辑结构功能。

图书管理信息系统可以划分的实体有：书籍类别信息实体、读者信息实体、书籍信息实体、借阅记录信息实体，归还记录信息实体。用E-R图一一描述这些实体。



总体E-R图:参考test6_design.docx

1、图书类别实体E-R图（参考test6_design.docx）


2、读者信息实体E-R图：（参考test6_design.docx）

3、信息实体E-R图：（参考test6_design.docx）

4、记录信息实体E-R图：（参考test6_design.docx）

5、记录信息实体E-R图：（参考test6_design.docx）

6、罚款信息实体E-R图：（参考test6_design.docx）

7、总的信息实体E-R图：（参考test6_design.docx）

8、数据字典

表1-1　 book_sytle 书籍类别信息表

| 表中列名     | 数据类型 | 可否为空       | 说明     |
| ------------ | -------- | -------------- | -------- |
| book_styleno | varchar  | not null(主键) | 种类编号 |
| book_style   | Varchar  | not null       | 种类名称 |

表1-2　　system_readers读者信息表格

| 表中列名    | 数据类型 | 可否为空       | 说明         |
| ----------- | -------- | -------------- | ------------ |
| reader_id   | varchar  | not null(主键) | 读者借书证号 |
| reader_name | varchar  | not null       | 读者姓名     |
| reader_sex  | varchar  | not null       | 读者性别     |
| reader_type | varchar  | null           | 读者种类     |



表1-3　system_book书籍信息表

| 表中列名    | 数据类型 | 可否为空       | 说明       |
| ----------- | -------- | -------------- | ---------- |
| book_id     | Varchar  | Not null(主键) | 书籍编号   |
| book_name   | Varchar  | Not null       | 书籍名称   |
| book_style  | Varchar  | Not null       | 书籍类别   |
| book_author | Varchar  | Not null       | 书籍作者   |
| book_pub    | Varchar  | Null           | 出版社名称 |
| isborrowed  | Varchar  | Not Null       | 是否被借出 |




表1-4　borrow_record 借阅记录信息表

| 表中列名   | 数据类型 | 可否为空         | 说明           |
| ---------- | -------- | ---------------- | -------------- |
| reader_id  | Varchar  | Not null(外主键) | 读者借阅证编号 |
| book_id    | Varchar  | Not null(外主键) | 书籍编号       |
| borrowdate | Varchar  | Not null         | 读者借书时间   |



表1-5　return_record 借阅记录信息表

| 表中列名    | 数据类型 | 可否为空         | 说明           |
| ----------- | -------- | ---------------- | -------------- |
| reader_name | Varchar  | Not null(外主键) | 读者借阅证编号 |
| reader_id   | Varchar  | Not null(外主键) | 书籍编号       |



表1-6　reader_fee 罚款记录信息表

| reader_id   | varchar | Not null         | 读者借书证编号 |
| ----------- | ------- | ---------------- | -------------- |
| reader_name | varchar | Not null         | 读者姓名       |
| book_id     | varchar | Not null(外主键) | 书籍编号       |
| book_name   | varchar | Not null         | 书籍名称       |
| book_fee    | varchar | Not Null         | 罚款金额       |



二、数据库各表实现

1、创建表空间与用户赋权

```sql
create tablespace Userspace
datafile 'E:\oracle\oracledatabase\ORCL\user1.dbf'
size 50m
autoextend on
next 50m maxsize 20480m
extent management local;
```

```sql
create tablespace Userspace01

logging

datafile 'E:\oracle\oracledatabase\ORCL\user2.dbf’

size 50m

autoextend on

next 50m maxsize 20480m

extent management local;
```


1.1

```sql
//创建角色role2

create role role2

//创建用户ft

create user ft;

//赋予角色ft权限connect

grant connect to ft;
```

1.2

```
//创建普通角色role1

create role role1;


//授权connect，resource，create view

grant connect，resource，create view to role1;


//创建普通用户moguohui 密码123

create user moguohui identified by 123 default tablespace user02 temporary tablespace temp;



//授权dba给moguohui（参考test6_design.docx）

grant dba to moguohui;
```





2、书本类别表建立

```sql
create table book_style
( 
   bookstyleno varchar(30) primary key,
   bookstyle varchar(30)
);
```




3、创建书库表

```sql
create table system_books
( 
  book_id varchar(20) primary key,
  book_name varchar(30) Not null, 
  book_styleno varchar(30) Not null,
  book_author varchar(30),
  book_pub varchar(30) ,
  isborrowed varchar (2) ,
  foreign key (book_styleno) references book_style (bookstyleno)
);
```



4、借书证表建立

```sql
create table system_readers 
( 
  reader_id varchar(9)primary key,
  reader_name varchar(9)not null ,
  reader_sex varchar(2) not null,
  reader_type varchar(10),
 );
```



5、借书记录表建立

```sql
create table borrow_record
(  
  book_id varchar(20)  primary key,
  reader_id varchar(9),
  foreign key (book_id) references system_books(book_id),
  foreign key (reader_id) references system_readers(reader_id)
);
```



6、还书记录表建立

```sql
create table return_record
( 
  book_id varchar(20) primary key,
  reader_id varchar(9),
  foreign key (book_id) references system_books(book_id),
  foreign key (reader_id) references system_readers(reader_id)
);
```



7、罚款单表建立

```sql
create table reader_fee
( 
  reader_id varchar(9)not null,
  reader_name varchar(9)not null ,
  book_id varchar(20) primary key,
  book_name varchar(30) Not null, 
  book_fee varchar(30) ,
  foreign key (book_id) references system_books(book_id),
  foreign key (reader_id) references system_readers(reader_id)
);
```



8.存储过程实例

为表borrow_record建存储过程test12

```sql
create or replace procedure test12
is cursor c
is 
select *from borrow_record;
v_emp c%rowtype;
begin open c;
loop fetch c into v_emp;
exit when (c%notfound);
dbms_output.putline(v_emp.nsrmc);
end loop;
close c;
end test12;
```



三、数据库实施

1、将书籍类别加入表book_style中

```sql
INSERT INTO  book_style VALUES ('1', '人文艺术类');

INSERT INTO  book_style VALUES ('2', '自然科学类');

INSERT INTO  book_style VALUES ('3', '社会科学类');

INSERT INTO  book_style VALUES ('4', '图片艺术类');

INSERT INTO  book_style VALUES ('5', '政治经济类');

INSERT INTO  book_style VALUES ('6', '工程技术类');

INSERT INTO book_style VALUES（'7'，'语言技能能类');
```

2、将已有的图书加入system_books表中

```sql
INSERT INTO system_books VALUES ('00127415153', '计算机原理', '6', '王爱英', '清华大学', '0');


INSERT INTO system_books VALUES ('12215121', 'C程序设计', '6', '谭浩强', '清华大学', '1');


INSERT INTO system_books VALUES ('9787308020558', '计算机体系', '6', '石教英', '浙江大学',  '1');


INSERT INTO system_books VALUES ('45456141414', '数据结构', '6', '吴伟民，严蔚敏', '清华大学', '1');


INSERT INTO system_books VALUES ('5455515', '中华5000年', '1', '吴强', '北京大学', '0');


INSERT INTO system_books VALUES ('015115', '古代埃及', '3', '赵文华', '北京大学',  '0');


INSERT INTO system_books VALUES ('1514514', '日本文化', '1', '吴小鹏', '北京大学', '1');


INSERT INTO system_books VALUES ('15154656', '经济学', '5', '李小刚', '北京大学',  '0');


INSERT INTO system_books VALUES ('5658', '影视文学', '4', '苏庆东', '北京大学出', '1');


INSERT INTO system_books VALUES ('565800020', '宇宙奥秘', '2', '苏庆东', '北京大学',  '0');

INSERT INTO system_books VALUES ('00125415152', '计算机原理', '6', '王爱英', '清华大学',  '0');
```

3、将已有图书证的读者加入system_readers表中

```sql
INSERT INTO system_readers VALUES ('X05620206', '陈特', '男', '学生')；
INSERT INTO system_readers VALUES ('X05620207', '陈远鹏', '男', '学生' );
INSERT INTO system_readers VALUES ('X05620204', '赵铭静', '女', '学生');
INSERT INTO system_readers VALUES ('X05620202', '潘虹', '女', '学生');
INSERT INTO system_readers VALUES ('008415', '蒋伟', '男', '教师' );
INSERT INTO system_readers VALUES ('001456', '李叶风', '女', '教师');
```



4、添加已借书读者的记录，同时将在已借出的借阅标记置

```sql
insert into borrow_record(book_id,reader_id)

values('00125415152','X05620202');

update system_books

set isborrowed=0

where  book_id='00125415152';



insert into borrow_record(book_id,reader_id)

values('00127415153','X05620206');

update system_books

set isborrowed=0

where  bookid='00127415153' and isborrowed='1';




insert into borrow_record(book_id,reader_id

values('5455515','X05620207');

update system_books

set isborrowed=0

where book_id='5455515' and  isborrowed='1';

                          
insert into borrow_record(book_id,reader_id）
values（'015115'，'X05620204'）

//更新system_book

set isborrowed=0

where book_id='015115' and  isborrowed='1';


insert into borrow_record(book_id,reader_id)

values('15154656','001456');

update system_books

set isborrowed=0

where book_id='15154656' and  isborrowed='1';


                          
insert into borrow_record(book_id,reader_id)

values('565800020','008415');

update system_books

set isborrowed=0

where book_id='565800020' and  isborrowed='1';
```



五、备份与恢复
1.全备份（参考test6_design.docx）

2.查看备份文件（参考test6_design.docx）

3.查看备份内容（参考test6_design.docx）

4.备份后修改数据（参考test6_design.docx）

5.模拟数据库崩溃（参考test6_design.docx）

6.恢复数据库（参考test6_design.docx）

7.查看数据是否恢复（参考test6_design.docx）

8.删除备份集（参考test6_design.docx）













