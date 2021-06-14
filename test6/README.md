
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

容灾方案	DataGuard设计正确	10

得分合计

2019 年  11  月  18 日


目		录


一、需求分析

1、背景分析

2、数据结构需求分析

3、事务处理需求分析

4、关系模式

二、方案图表设计

22、读者信息实体E-R图：

3、信息实体E-R图：

4、记录信息实体E-R图：

5、记录信息实体E-R图：

6、罚款信息实体E-R图：

7、总的信息实体E-R图：

8、数据字典

三、数据库各表实现

1、创建表空间

2、书本类别表建立

3、创建书库表

4、借书证表建立

5、借书记录表建立

6、还书记录表建立

7、罚款单表建立

8、存储过程实例

四、数据库实施

五、总结

六、备份与恢复

七、参考文献





一、需求分析

1、背景分析


随着图书馆规模的不断扩大，图书数量也相应的增加，有关图书的各种信息量也成倍增加，面对着庞大的信息量，传统的人工方式管理会导致图书馆管理上的混乱，人力与物力过多浪费，图书馆管理费用的增加，从而使图书馆的负担过重，影响整个图书馆的运作和控制管理，因此，必须制定一套合理、有效，规范和实用的图书管理系统，对图书资料进行集中统一的管理

同时，IT产业和互联网获得了飞速发展，计算机应用已渗透到了各个领域，引起了信息管理的革命，实现了信息的自动化处理，提高了处理的及时性和正确性。

提高图书管理工作效率，作到信息的规范管理，科学统计和快速查询，让图书馆更好的为学校，社会服务。

2、数据结构需求分析

图书馆管理信息系统需要完成功能主要有：

(1) 读者基本信息的输入，包括借书证编号、读者姓名、读者性别。

(2) 读者基本信息的查询、修改，包括读者借书证编号、读者姓名、读者性别等。

(3) 书籍类别标准的制定、类别信息的输入，包括类别编号、类别名称。

(4) 书籍类别信息的查询、修改，包括类别编号、类别名称。

(5) 书籍库存信息的输入，包括书籍编号、书籍名称、书籍类别、作者姓名、出版社名称。

(6) 书籍库存信息的查询，修改，包括书籍编号、书籍名称、书籍类别、作者姓名、出版社名称等。

(7) 借书信息的输入，包括读者借书证编号、书籍编号。

(8) 借书信息的查询、修改，包括借书证编号、读者编号、读者姓名、书籍编号、书籍名称等。

(9) 还书信息的输入，包括借书证编号、书籍编号。

(10) 还书信息的查询和修改，包括还书读者借书证编号、读者姓名、书籍编号、书籍名称等。

(11) 超期还书罚款输入，还书超出期限包括超出期限还书的读者借书证号，书籍编号，罚款金额。

(12) 超期还书罚款查询，删除，包括读者借书证编号、读者姓名、书籍编号、书籍名称，罚款金额等

3、事务处理需求分析


(1)在读者信息管理部分,要求:

a.可以查询读者信息。



b.可以对读者信息进行添加及删除的操作。


(2 )在书籍信息管理部分,要求:


a.可以浏览书籍信息,要求:

b.可以对书籍信息进行维护,包括添加及删除的操作。

(3)在借阅信息管理部分,要求:。

a.可以浏览借阅信息。

b.可以对借阅信息进行维护操作。

(4)在归还信息管理部分，要求:

a.可以浏览归还信息

b.对归还信息可修改维护操作

(5)在管理者信息管理部分,要求:

a.显示当前数据库中管理者情况。

b.对管理者信息维护操作。

(6)在罚款信息管理部分,要求:

a.可以浏览罚款信息

b.对罚款信息可以更新

4、关系模式

(1)	书籍类别（种类编号，种类名称）

(2)	读者（借书证编号，读者姓名，读者性别，读者种类）

(3)	书籍（书籍编号，书籍名称，书籍类别，书记作者，出版社名称）

(4)	借阅（借书证编号，书籍编号）

(5)	还书（借书证编号，书籍编号）

(6)	罚款（借书证编号，读者姓名，借书证编号，书籍编号）

以上通过关系代数方法的进行运算得到所需要的结果，在实验结果中可以看到。

二、方案图表设计

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

表2-1　 book_sytle 书籍类别信息表

表中列名	数据类型	可否为空	说明



book_styleno	varchar	not null(主键)	种类编号

book_style	Varchar	not null	种类名称



表2-2　　system_readers读者信息表格

表中列名	数据类型	可否为空	说明

reader_id	varchar	not null(主键)	读者借书证号

reader_name	varchar	not null	读者姓名

reader_sex	varchar	not null	读者性别

reader_type	varchar	null	读者种类



表2-3　system_book书籍信息表

表中列名	数据类型	可否为空	说明

book_id	Varchar	Not null(主键)	书籍编号

book_name	Varchar	Not null	书籍名称

book_style	Varchar	Not null	书籍类别

book_author	Varchar	Not null	书籍作者

book_pub	Varchar    
出版社名称
isborrowed	Varchar	Not Null	是否被借出


表2-4　borrow_record 借阅记录信息表

表中列名	数据类型	可否为空	说明

reader_id	Varchar	Not null(外主键)	读者借阅证编号

book_id	Varchar	Not null(外主键)	书籍编号

borrow_date	Varchar	Not null	读者借书时间





表2-5　return_record 借阅记录信息表

表中列名	数据类型	可否为空	说明

reader_name	Varchar	Not null(外主键)	读者借阅证编号

reader_id	Varchar	Not null(外主键)	书籍编号



表2-6　reader_fee 罚款记录信息表

reader_id   varchar	Not null	读者借书证编号

reader_name	varchar	Not null	读者姓名

book_id	varchar	Not null(外主键)	书籍编号

book_name	varchar	Not null	书籍名称

book_fee	varchar	Not Null	罚款金额





三、数据库各表实现

1、创建表空间与用户赋权

create temporary tablespace user01.dbf 

tempfile '/home/oracle/app/oracle/oradata/orcl/user01.dbf' 

size 50m   on

autoextend

next 50m maxsize 20480m

extent management local;



create tablespace user02.dbf

logging

datafile '/home/oracle/app/oracle/oradata/orcl/pdborcl/user02.dbf’

size 50m

autoextend on

next 50m maxsize 20480m

extent management local;


1.1

创建角色role2

create role role2

创建用户ft

create user ft;

赋予角色ft权限connect

grant connect to ft;

1.2


创建普通角色role1


create role role1;


授权connect，resource，creat view

grant connect，resource，creat view to role1;



创建普通用户moguohui 密码123

create user moguohui identified by 123 default tablespace user02 temporary tablespace temp;





授权dba给moguohui（参考test6_design.docx）

grant dba to moguohui;







2、书本类别表建立

create table book_style

( 

   bookstyleno varchar(30) primary key,

   bookstyle varchar(30)

);










3、创建书库表

create table system_books

( 

  bookid varchar(20) primary key,

  bookname varchar(30) Not null, 

  bookstyleno varchar(30) Not null,


  bookauthor varchar(30),

  bookpub varchar(30) ,

 

  isborrowed varchar (2) ,

foreign key (bookstyleno) references book_style (bookstyleno)

);







4、借书证表建立

create table system_readers 

( readerid varchar(9)primary key,

  readername varchar(9)not null ,

  readersex varchar(2) not null,

  readertype varchar(10),

 );





5、借书记录表建立

create table borrow_record

( bookid varchar(20)  primary key,

  readerid varchar（9），  

  foreign key (bookid) references system_books(bookid),

  foreign key (readerid) references system_readers(readerid)

);



6、还书记录表建立

create table return_record

( bookid varchar(20) primary key,

  readerid varchar(9),

foreign key (bookid) references system_books(bookid),

  foreign key (readerid) references system_readers(readerid)

);



7、罚款单表建立

create table reader_fee

( readerid varchar(9)not null,

  readername varchar(9)not null ,

  bookid varchar(20) primary key,

  bookname varchar(30) Not null, 

  bookfee varchar(30) ,

   foreign key (bookid) references system_books(bookid),

  foreign key (readerid) references system_readers(readerid)

);



8.存储过程实例



为表borrow_record建存储过程test12（参考test6_design.docx）



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



四、数据库实施

1、将书籍类别加入表book_style中

INSERT INTO  book_style VALUES ('1', '人文艺术类');



INSERT INTO  book_style VALUES ('2', '自然科学类');

INSERT INTO  book_style VALUES ('3', '社会科学类');

INSERT INTO  book_style VALUES ('4', '图片艺术类');

INSERT INTO  book_style VALUES ('5', '政治经济类');

INSERT INTO  book_style VALUES ('6', '工程技术类');

INSERT INTO book_style VALUES（'7'，'语言技能能类'）；


2、将已有的图书加入system_books表中

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


3、将已有图书证的读者加入system_readers表中

INSERT INTO system_readers VALUES ('X05620206', '陈特', '男', '学生')；

INSERT INTO system_readers VALUES ('X05620207', '陈远鹏', '男', '学生' );

INSERT INTO system_readers VALUES ('X05620204', '赵铭静', '女', '学生');

INSERT INTO system_readers VALUES ('X05620202', '潘虹', '女', '学生');

INSERT INTO system_readers VALUES ('008415', '蒋伟', '男', '教师' );

INSERT INTO system_readers VALUES ('001456', '李叶风', '女', '教师');




4、添加已借书读者的记录，同时将在已借出的借阅标记置


insert into borrow_record(bookid,readerid)



values('00125415152','X05620202')；

update system_books

set isborrowed=0

where  bookid='00125415152'；







insert into borrow_record(bookid,readerid)

values('00125415153','X05620206')；

update system_books

set isborrowed=0

where  bookid='00125415153' and isborrowed='1'；






insert into borrow_record(bookid,readerid

values('5455515','X05620207')；

update system_books

set isborrowed=0

where bookid='5455515' and  isborrowed='1'；


insert into borrow_record(bookid,readerid）
值（'015115'，'X05620204'）

更新system_book

set isborrowed=0

where bookid='015115' and  isborrowed='1'；

insert into borrow_record(bookid,readerid)

values('15154656','001456')；

update system_books

set isborrowed=0

where bookid='15154656' and  isborrowed='1'；

insert into borrow_record(bookid,readerid)

values('565800020','008415')；

update system_books

set isborrowed=0

where bookid='565800020' and  isborrowed='1'；


五、总结

通过此次数据库的课程设计，真正达到了学与用的结合，增强了对数据库方面应用的理解，对自己今后参与开发数据库系统积累了不少经验，在实验过程中，从建立数据开始，对灵据库设计理念及思想上有更高的认识，从需求分析，到概念设计和逻辑设计，E-R图的表示，数据字典的创建，懂得了不少有关数据库开发过程中的知识，在实验中建表，及其关系模式，关系代数的建立及理解，将SQL语的查询语句用得淋漓尽致，增强了自己在数据库中应用SQL语言的灵活性，其中包括，插入、删除、修改、查询,牵涉表和表之间的联系，主建与外主键的定义，约束项的设置，使逻辑更严密，在学习过程中，我也能过上网查了不少资料，也看了一些别人设计的图书馆管理信息系统的设计报告，学以致用，自我创新，独立完成了这份自己的报告，从中在学到用，从用又到学，不断修改，系统更新。虽然不能达到完善系统，但也做到了尽善尽美，加强理论学习对完善系统会有很多帮助。

六、备份与恢复
1.全备份

[oracle@oracle-pc ~]$ cat rman_level0.sh


[oracle@oracle-pc ~]$ ./rman_level0.sh



2.查看备份文件



[oracle@oracle-pc ~]$ rman backup



3.查看备份内容

[oracle@oracle-pc ~]$ rman target /



RMAN> list backup;

List of Backup Sets


==================




4.备份后修改数据

[oracle@oracle-pc ~]$ sqlplus moguohui/123@pdborcl



SQL> create table ti(id varchar(15),name varchar(50));



Table created.



SQL> insert into t1 values(1,'zhang');



1 row created;



SQL> commit;



Commit complete.



SQL> select *from t1;



ID              name

-------------------------------------

1               zhang

2               wang



5.模拟数据库崩溃



[oracle@oracle-pc ~]$ rm /home/oracle/app/oracle/oradata/orcl/pdborcl/

SAMPLE_SCHEMA_users01.dbf





删除数据库文件后修改数据



[oracle@oracle-pc ~]$ sqlplus moguohui/123@pdborcl



insert into t1 values(2,'wang');



1 row created.



SQL> commit;



Commit complete.



SQL> select * from t1;



ID               NAME

-----------------------------------------------------
1                zhang

2                wang







6.恢复数据库



SQL> shutdown abort



ORACLE instance shut down



SQL> startup mount



ORACLE instance started





[oracle @ oracle-pc〜] $ rman target/

RMAN> restore database ;

RMAN> recover database;



RMAN> alter database open;

RMAN> exit



7查看数据是否恢复

[oracle@oracle-pc ~]$ sqlplus moguohui/123@pdborcl



SQL>select *from t1;



ID             NAME

--------------------------------------------------



1              zhang

2              wang



SQL>



8删除备份集

[oracle@oracle-pc ~]$ rman target



DO yuu want to delete the above objects(enter YES or NO)?YES





七、参考文献

[1]张建勤.基于Oracle安全策略的研究.计算机光盘软件与应用,2013(10)

[2]萨师煊.数据库原理.高等教育出版社,2006.8

[3]庄王健.网页设计三剑客白金教程.电子工业出版社,2006.01

[4]邹婷.Dreamweaver 8 标准教程.北京:中国青年出版社,2006,153-165

[5]丁荣涛.商业网页设计与制作.北京:北京大学出版社.2006

[6]互联网上提供的网页制作素材及特效





