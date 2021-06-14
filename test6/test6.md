## **一． 需求分析**

#### 1.1背景

随着计算机的普及和信息技术的发展，人们的生活发生了日新月异的变化，各类计算机软件逐渐渗透到了社会的每个角落，大大地改善了人们的生活质量，提高了人们的工作效率。在高校中，图书借阅是学生获取知识的一个很重要的途径，如何既能方便学生借书，又能减轻图书馆管理人员的工作负担，高效地完成图书借阅管理工作，是一件非常重要的事情。 

成都十陵某高校拥有一个小型图书馆，为全校师生提供学习、阅读的空间。近几年来，随着生源的不断扩大，图书馆的规模也随之扩大，图书数量也相应地打量增加，有关图书借阅的各种信息成倍增加。面对如此巨大的信息量，图书馆管理人员很难支撑，因此，学校领导决定建立一套合理实用的图书借阅管理系统软件，以对校内的图书借阅信息进行统一、集中的管理。。

#### 1.2数据库选择


​		ORACLE数据库系统是美国ORACLE公司（甲骨文）提供的以分布式数据库为核心的一组软件产品，是目前最流行的客户/服务器(CLIENT/SERVER)或B/S体系结构的数据库之一。比如SilverStream就是基于数据库的一种中间件。ORACLE数据库是目前世界上使用最为广泛的数据管理系统，作为一个通用的数据库系统，它具有完整的数据管理功能；作为一个关系数据库，它是一个完备关系的产品；作为分布式数据库它实现了分布式处理功能。但它的所有知识，只要在一种机型上学习了ORACLE知识，便能在各种类型的机器上使用它。

#### 1.3 Oracle 的优势

   Oracle数据库的优点一：ORACLE7.X以来引入了共享SQL和多线索服务器体系结构。这减少了ORACLE的资源占用，并增强了ORACLE的能力，使之在低档软硬件平台上用较少的资源就可以支持更多的用户，而在高档平台上可以支持成百上千个用户。

  Oracle数据库的优点二：提供了基于角色(ROLE)分工的安全保密管理。在数据库管理功能、完整性检查、安全性、一致性方面都有良好的表现。

  Oracle数据库的优点三：支持大量多媒体数据，如二进制图形、声音、动画以及多维数据结构等。

  Oracle数据库的优点四：提供了与第三代高级语言的接口软件PRO系列，能在C,C++等主语言中嵌入SQL语句及过程化(PL/SQL)语句，对数据库中的数据进行操纵。加上它有许多优秀的前台开发工具如 POWER BUILD、SQLFORMS、VISIA BASIC 等，可以快速开发生成基于客户端PC 平台的应用程序，并具有良好的移植性。

  Oracle数据库的优点五：提供了新的分布式数据库能力。可通过网络较方便地读写远端数据库里的数据，并有对称复制的技术。




## **二． 概念结构设计**

#### 2.1表空间设计

​     创建一个表空间USERS02，用于保存书籍管理系统的各种表，首先需要定义数据文件的存储地址，并且定义该数据文件的大小为200M、的分配方式为自动扩展、表空间的管理方式为本地管理。

#### 2.2数据表设计

创建五个表，存储在表空间users中。这五个表是学生表、图书表、借阅表和管理员表，书籍种类表。

学生表的作用是存放学生信息，学号，学生姓名，等等学生相关的信息。

图书表的作用是存放图书信息，编号，书名，作者，价格等图书的相关信息。

借阅表的作用是对学生表和图书表的一个链接，显示哪些人借的哪些书。借阅的日期和还书日期等信息。

书籍种类表的作用是将图书表的书进行分类，存放种类编号，种类名等信息。

管理员信息表的作用是用于存放管理员的账号，密码，姓名，加入日期等相关信息。



#### 2.3存储过程和函数设计

存储过程的作用相当于单个表的操作方法，暂且只针对单个表的操作，例如调用存储过程的时候传一个Dept的参数，然后输出满足这个条件的学号和姓名，实现上面功能只调用这个存储过程就行。
	函数的创建与存储过程的创建相似，不同之处在于，函数有一个显示的返回值。所以函数里面必须包含一个return语句，来指明函数的返回值，能限定函数返回值的类型，但是无法约束返回值的长度，精度，刻度等。最终也只有一个return背执行。

#### 2.4备份与恢复设计

在对Oracle数据库进行备份与恢复设计时，要考虑发生故障后，利用已备份的数据或控制文件，重新建立一个完整的数据库。恢复可以是实例恢复或者是介质恢复，实例恢复是在当oracle实例出现失败后，oracle自动进行的恢复。而介质恢复则是在当存放数据库的介质出现故障时进行恢复。

#### 2.5数据库安全设计

数据库安全设计主要体现在为数据库建立用户，密码，以及不同等级用户的的权限！这样做就可以有效的让不同用户查阅的权限都在管理员的管理下，防止数据的改动和丢失！因此要访问数据库，用户必须指定有效的数据库用户账户，而且还要根据该用户账户的要求成功通过验证，每个数据库用户都有一个唯一的数据库账户。
	在本次综合实验中，我主要创建了system_gpfish和system_admin两个角色，分别对应不同的权限，这样就加强了对数据库的保护。另外，创建概要文件来描述如何使用系统的资源(主要是CPU资源)。将概要文件赋予某个数据库用户，在用户连接并访问数据库服务器时，系统就按照概要文件给他分配资源。




## **三． 逻辑结构设计**

数据表的设计


书籍表设计BOOK
字段名	数据类型	可以为空	注释
bookno	Number(10,0)	no	书籍编号，主键
bookname	Varchar2(20,BYTE)	no	书名
bookclass	Varchar2(20,BYTE)	no	书的种类，书种类表外键
writer	Varchar2(20,BYTE)	no	作者
price	Number(10,0)	no	价格



书的种类表设计BOOKCLASS
字段名	数据类型	可以为空	注释
classno	Number(10,0)	no	书籍种类的编号，主键
classname	Varchar2(20,BYTE)	no	书籍的种类名

管理员表设计MANAGER
字段名	数据类型	可以为空	注释
Adminname	Varchar2(20,BYTE)	no	管理员账号，主键
pwd	Varchar2(20,BYTE)	no	管理员密码
mname	Varchar2(20,BYTE)	no	管理员姓名
Join_date	DATE	no	加入日期


借阅信息表设计BORROW
字段名	数据类型	可以为空	注释
bookno	Varchar2(200,BYTE)	N0	书籍编号，书籍表外键
studyno	Varchar2(200,BYTE)	N0	学生学号，学生表外键
Borrow_date	Varchar2(20,BYTE)	N0	借书日期
Return_date	Varchar2(20,BYTE)	N0	还书日期


学生信息表设计STUDENT
字段名	数据类型	可以为空	注释
username	Varchar2(20,BYTE)	no	学生账号
studyno	Number(10,0)	no	学生学号，主键
name	Varchar2(10,BYTE)	no	学生姓名
password	Varchar2(20,BYTE)	no	学生密码
phone	Number(20,0)	no	学生电话



## **四． 物理结构设计**

创建user02表空间并分配数据文件，表空间初始大小200M，然后创建了一个名叫bookbases的数据库，指定了它的存储位置，以及创建数据库名为gpfish的管理员，创建角色system_gpfish和用户system_admin，然后授权和分配空间




```sql
CREATE TABLESPACE User02
DATAFILE
‘/home/oracle/app/oradata/orcl/pdborcl/pdbtest_user02_1.dbf’
SIZE 100M AUTOEXTEND ON NEXT 256M MAXSIZE UNLIMITED,
‘/home/oracle/app/oradata/orcl/pdborcl/pdbtest_user02_2.dbf’
SIZE 100M AUTOEXTEND ON NEXT 256M MAXSIZE UNLIMITED
EXTENT MANAGEMENT LOCAL SEGMENT SPACE MANAGEMENT AUTO;


create p1uggable database bookbases admin user gpfish identified by 123456 file_name_convert=('/home/orac1e/gpfish/myscott/',' /home/orac1e/gpfish/myscott2');|
$ sqlplus system/123@pdborcl
SQL> CREATE ROLE system_gpfish;
Role created.
SQL> GRANT connect,resource,CREATE VIEW TO system_gpfish;Grant succeeded.
SQL> CREATE USER system_admin IDENTIFIED BY 123456 DEFAULT TABLESPACE users TEMPORARY TABLESPACE temp;
User created.
SQL> ALTER USER new_user QUOTA 50M ON users;
User altered.
SQL> GRANT system_gpfish TO system_admin;Grant succeeded.
SQL> exit
```

然后对新创建的角色进行select,delete,insert,updata等权限.
此时使用创建好的用户system_gpfish登录,创建实体表.

书籍表的创建

```sql
CREATE TABLE BOOK 
(
  BOOKNO NUMBER(10, 0) NOT NULL 
, BOOKNAME VARCHAR2(20 BYTE) NOT NULL 
, BOOKCLASS VARCHAR2(20 BYTE) NOT NULL 
, WRITER VARCHAR2(20 BYTE) NOT NULL 
, PRICE NUMBER(10, 0) NOT NULL 
, CONSTRAINT BOOK_PK PRIMARY KEY 
  (
    BOOKNO 
  )
  ENABLE 
) 
LOGGING 
TABLESPACE "USERS" 
PCTFREE 10 
INITRANS 1 
STORAGE 
( 
  INITIAL 65536 
  NEXT 1048576 
  MINEXTENTS 1 
  MAXEXTENTS 2147483645 
  BUFFER_POOL DEFAULT 
);
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191127123414166.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01vbnN0ZXJCMA==,size_16,color_FFFFFF,t_70)




种类表的创建

```sql
CREATE TABLE BOOKCLASS 
(
  CLASSNO NUMBER(10, 0) NOT NULL 
, CLASSNAME VARCHAR2(20 BYTE) NOT NULL 
, CONSTRAINT BOOKCLASS_PK PRIMARY KEY 
  (
    CLASSNO 
  )
  ENABLE 
) 
LOGGING 
TABLESPACE "USERS" 
PCTFREE 10 
INITRANS 1 
STORAGE 
( 
  INITIAL 65536 
  NEXT 1048576 
  MINEXTENTS 1 
  MAXEXTENTS 2147483645 
  BUFFER_POOL DEFAULT 
);	
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191127123818103.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01vbnN0ZXJCMA==,size_16,color_FFFFFF,t_70)




管理员表创建

```sql
CREATE TABLE MANAGER 
(
  ADMINNAME VARCHAR2(20 BYTE) NOT NULL 
, PWD VARCHAR2(20 BYTE) NOT NULL 
, MNAME VARCHAR2(20 BYTE) NOT NULL 
, JOIN_DATE DATE NOT NULL 
, CONSTRAINT MANAGER_PK PRIMARY KEY 
  (
    ADMINNAME 
  )
  ENABLE 
) 
LOGGING 
TABLESPACE "USERS" 
PCTFREE 10 
INITRANS 1 
STORAGE 
( 
  BUFFER_POOL DEFAULT 
);	
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191127123839854.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01vbnN0ZXJCMA==,size_16,color_FFFFFF,t_70)




学生表的创建

```sql
CREATE TABLE STUDENT 
(
  USERNAME VARCHAR2(20 BYTE) NOT NULL 
, STUDYNO NUMBER(10, 0) NOT NULL 
, NAME VARCHAR2(10 BYTE) NOT NULL 
, PASSWORD VARCHAR2(20 BYTE) NOT NULL 
, PHONE NUMBER(20, 0) NOT NULL 
, CONSTRAINT STUDENT_PK PRIMARY KEY 
  (
    STUDYNO 
  )
  ENABLE 
) 
LOGGING 
TABLESPACE "USERS" 
PCTFREE 10 
INITRANS 1 
STORAGE 
( 
  BUFFER_POOL DEFAULT 
);
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191127123850289.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01vbnN0ZXJCMA==,size_16,color_FFFFFF,t_70)




借阅信息表的创建

```sql
CREATE TABLE BORROW 
(
  BOOKNO VARCHAR2(200 BYTE) NOT NULL 
, STUDYNO VARCHAR2(200 BYTE) NOT NULL 
, BORROW_DATE VARCHAR2(20 BYTE) NOT NULL 
, RETURN_DATE VARCHAR2(20 BYTE) NOT NULL 
) 
LOGGING 
TABLESPACE "USERS" 
PCTFREE 10 
INITRANS 1 
STORAGE 
( 
  INITIAL 65536 
  NEXT 1048576 
  MINEXTENTS 1 
  MAXEXTENTS 2147483645 
  BUFFER_POOL DEFAULT 
);	
 
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191127123906123.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01vbnN0ZXJCMA==,size_16,color_FFFFFF,t_70)



## **五． 数据库实施代码**

5.1插入数据

数据来源于网络，通过python爬虫获取，然后自动生成了sql语句转移到sqldeveloper进行插入
Python程序如下：
	根据每张表的不同字段修改python程序，生成对应的sql语句对剩下的四张表进行信息生成然后进行插入。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191127124059438.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01vbnN0ZXJCMA==,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20191127124113293.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01vbnN0ZXJCMA==,size_16,color_FFFFFF,t_70)

5.2程序包建立

（1）	建立一个程序包里面有一个函数和一个存储过程,用来获取书的种类和删除管理员，先建包
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191127124143476.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01vbnN0ZXJCMA==,size_16,color_FFFFFF,t_70)

（2）	在包的主体中创建函数和存储过程：

```sql
create or replace PACKAGE MyPack 
  IS
 
  FUNCTION get_bookclass(classno NUMBER) RETURN varchar2;
  PROCEDURE delmanager (adminuser in manager.adminname%type);
END MyPack;


create or replace package body MyPack 
is
  function get_bookclass(classno number)
  RETURN varchar2
  IS class_name 
  varchar2;
    BEGIN
      SELECT * into class_name  
        FROM bookclass WHERE classno = bookclass.classno;
      RETURN class_name;
    END get_bookclass;
    
    
 PROCEDURE delmanager
 (adminuser in manager.adminname%type)
  AS
    no_result EXCEPTION;
    begin
      
    delete from manager where adminname = adminuser;
    if sql%notfound then
      raise no_result;
    end if;
    dbms_output.put_line('delete completed!!!');
  exception
    when no_result then
      dbms_output.put_line('not found!!!');
    when others then
      dbms_output.put_line(sqlcode||'------'||sqlerrm);
    
    END;
END MyPack;
/
```
5.3建立备份方案
备份脚本如下：

```powershell
#rman_level1.sh 
#!/bin/sh

export NLS_LANG='SIMPLIFIED CHINESE_CHINA.AL32UTF8'
export ORACLE_HOME=/home/oracle/app/oracle/product/12.1.0/dbhome_1  
export ORACLE_SID=orcl  
export PATH=$ORACLE_HOME/bin:$PATH  


rman target / nocatalog msglog=/home/oracle/rman_backup/lv1_`date +%Y%m%d-%H%M%S`_L0.log << EOF
run{
configure retention policy to redundancy 1;
configure controlfile autobackup on;
configure controlfile autobackup format for device type disk to '/home/oracle/rman_backup/%F';
configure default device type to disk;
crosscheck backup;
crosscheck archivelog all;
allocate channel c1 device type disk;
backup as compressed backupset incremental level 1 database format '/home/oracle/rman_backup/dblv1_%d_%T_%U.bak'
   plus archivelog format '/home/oracle/rman_backup/arclv1_%d_%T_%U.bak';
report obsolete;
delete noprompt obsolete;
delete noprompt expired backup;
delete noprompt expired archivelog all;
release channel c1;
}
EOF

exit
```


测试：

```powershell
[oracle@oracle-pc ~]$ cat rman_level.sh
[oracle@oracle-pc ~]$ ./rman_level.sh
```

开始备份：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191127124334170.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01vbnN0ZXJCMA==,size_16,color_FFFFFF,t_70)

为了测试备份功能是否能够使用，现在模拟进行数据损坏备份，首先删除数据库文件：

```powershell
[oracle@oracle-pc~]$rm /home/oracle/app/oracle/oradata/orcl/pdborcl/SAMPLE_SCHEMA_users01.dbf
```

然后通过备份脚本进行数据恢复：

```powershell
sqlplus / as sysdba
SQL>shutdown immediate
SQL>shutdown abort
SQL>startup mount
rman target /
```

## **六．体会与总结**

通过自己实现的这个基于Oracle的书籍管理系统，体会到Oracle与Mysql数据库的差别，相比于MySQL，Oracle要相对难一点，但是在功能、安全、大数据储存都是碾压MySQL。
