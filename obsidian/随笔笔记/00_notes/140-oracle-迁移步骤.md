# 1.测试数据泵

使用expdp和impdp导出导入整个数据库之前，需要先测试版本、环境的可用性，所以先使用一个库表都比较少的用户来导入导出来测试方案是否可行。



## 1.1准备导出，已有则跳过

```sql
# 创建数据目录
CREATE DIRECTORY EXPDP_DUMP AS 'F:\oracle_backup\expdp';
# 查看数据目录
select * from DBA_DIRECTORIES;
```



## 1.2执行导出

```sql
# 按照模式导出单个用户下的表
expdp ewf/ewf123@ORCL directory=EXPDP_DUMP dumpfile=ewf.dmp logfile=ewf_logfile.log schemas=ewf
```



## 1.3准备导入

```sql
# 创建表空间
CREATE TABLESPACE EWF
DATAFILE '/home/oracle/app/oradata/orcl106/EWF.dbf'
SIZE 100M
AUTOEXTEND ON
NEXT 50M
MAXSIZE UNLIMITED;

# 创建用户名
CREATE USER EWF
IDENTIFIED BY ewf123
DEFAULT TABLESPACE EWF
TEMPORARY TABLESPACE temp
QUOTA UNLIMITED ON EWF;

# 授予用户权限
GRANT CONNECT TO EWF;
GRANT RESOURCE TO EWF;
GRANT CREATE SESSION TO EWF;
GRANT CREATE TABLE TO EWF;
GRANT CREATE VIEW TO EWF;
GRANT CREATE SEQUENCE TO EWF;
GRANT CREATE PROCEDURE TO EWF;
GRANT CREATE DBA TO EWF;

# 删除数据目录
drop directory IMPDP_DUMP ;

# 创建数据目录
CREATE DIRECTORY IMPDP_DUMP AS '/home/oracle/backup';

# 查看数据目录
select * from DBA_DIRECTORIES;

# 授予用户有读写数据目录的权限
grant read,write on directory IMPDP_DUMP to ewf;

# 失败的原因是没有权限，切换到root账号，授予/home/oracle/backup的所有者是oracle
chown oracle /home/oracle/backup
chown oracle /home/oracle/backup/EWF.DMP

```



## 1.4执行导入

```sql
# 按照模式导入单个用户下的表
impdp ewf/ewf123@orcl106 DIRECTORY=IMPDP_DUMP DUMPFILE=EWF.DMP schemas=ewf

grant read,write on directory IMPDP_DUMP to ewf;
grant become user to ewf;

impdp ewf/ewf123@orcl DIRECTORY=IMPDP_DUMP DUMPFILE=HB_FRCST_ZJ.DMP schemas=HB_FRCST_ZJ

impdp ewf/ewf123@orcl DIRECTORY=IMPDP_DUMP DUMPFILE=HB_SYQ_ZJ.DMP schemas=HB_SYQ_ZJ
```





# 2.数据泵全库迁移



## 2.1准备导出，已有则跳过

```sql
# 创建数据目录
CREATE DIRECTORY EXPDP_DUMP AS 'F:\oracle_backup\expdp';
# 查看数据目录
select * from DBA_DIRECTORIES;
```



## 2.2执行导出

```sql
# 导整个库
expdp ewf/ewf123@ORCL directory=EXPDP_DUMP dumpfile=oracle140.dmp logfile=oracle140_logfile.log full=y
```



## 1.3准备导入

```sql
# 创建表空间 - 创建用户名 - 授予用户权限
# sql语句在文件中，直接执行，这里就不在粘贴了

# 失败的原因是没有权限，切换到root账号，授予/home/oracle/backup的所有者是oracle
chown oracle /mnt/data/oradatabackup
chown oracle /mnt/data/oradatabackup/ORACLE140.DMP


用oracle账号
执行命令 su - oracle
就可以了
```



## 1.4执行导入

```sql
# 重新建数据目录
drop directory IMPDP_DUMP ;
CREATE DIRECTORY IMPDP_DUMP AS '/mnt/data/oradatabackup';
grant read,write on directory IMPDP_DUMP to system;
grant become user to system;

grant read,write on directory IMPDP_DUMP to system;
grant become user to system;

# 整库导入
impdp system/ewater@orcl DIRECTORY=IMPDP_DUMP DUMPFILE=ORACLE140.DMP full=y
```




错误处理：
```sql

# impdp 遇到ORA-31685
对用户进行授权后，删除已导入的数据，重复导入，解决该问题
grant create materialized view to system;
grant dba to system;
```