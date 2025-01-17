# 查询



```sql
# 查询所有用户及默认表空间
select * from dba_users order by user_id asc;

# 查询所有表空间详细信息
select * from dba_data_files order by file_id asc;


1)查询所有表空间

select tablespace_name from dba_tablespaces;
select tablespace_name from user_tablespaces;

2)查询使用过的表空间  

select distinct tablespace_name from dba_all_tables;

select distinct tablespace_name from user_all_tables;

3)查询表空间中所有表的名称

select *  from dba_all_tables where tablespace_name = 'SYNC_PLUS_1' and owner='GDSDCZJ'

# 查询系统用户
select * from all_users
select * from dba_users

```







# 创建用户

```sql
创建新用户：create user yz_test  identified by 123456; 注释：create user 用户名  identified by 密码;


create tablespace yz_test_space  datafile 'D:\exeFile\installPackage\OracleDB\oracle-tableSpace\yz_test_space.dbf' size 2048M;
注释：create tablespace 表空间名 datafile 位置及名称 size 大小;
前提：D:\exeFile\installPackage\OracleDB\oracle-tableSpace，有这个文件夹，不会自动创建文件夹。

授权用户使用表空间：alter user yz_test  quota unlimited on yz_test_space;

给用户授权：grant connect,resource,dba to yz_test; 


 create tablespace orcl datafile '/mnt/data/oradata/orcl/orcl.dbf' size 200M AutoExtend On Next 10M segment space management auto;

```





# 删除用户

```sql
# 删除用户：加了cascade就可以把用户连带的数据全部删掉。
drop user user-name cascade;

# 删除表空间：
drop tablespace tablespace_name;
# 包括物理文件：
drop tablespace tablespace_name including contents and datafiles cascade constraint;
```



# 导入导出

在10g之前，传统的导出和导入分别使用EXP工具和IMP工具，从10g开始，不仅保留了原有的EXP和IMP工具，还提供了数据泵导出导入工具EXPDP和IMPDP。

1、exp和expdp最明显的区别就是导出速度的不同。expdp导出是并行导出。(如果把exp导出比喻为一个工人在挖土，那么expdp就相当于一个挖掘机在挖土)

2、exp和expdp导出不止是速度的不同，同时导出机制也完全不同，所有用expdp导出的[dmp](https://so.csdn.net/so/search?q=dmp&spm=1001.2101.3001.7020)文件只能用impdp的方式导入。

3、EXP和IMP是客户端工具程序，它们既可以在可以客户端使用，也可以在服务端使用。

4、EXPDP和IMPDP是服务端的工具程序，他们**只能在ORACLE服务端**使用，不能在客户端使用。

5、命令使用的区别，expdp命令新增了目录对象directory，file替换为dumpfile，log替换成logfile，还添加了一个reuser_dumpfile=ture参数

其中：

数据泵取只能在服务器端运行，客户端只能用来连接服务器启动[导入导出]操作






## 数据泵-导出exp

```sql
exp user/password@localhost/orcl file=D:\GPSDATA0613.dmplog=e:\log.txt full=y ignore=y;

```



full=y是指导出全部，把表、存储过程、函数等一起导出，导入时也一样，导入中的ignore=y是忽略重复表，就是原来你存在这些表中的某个的话，会报错误信息，加上这个就不会了。




## 数据泵-导入imp

```sql
imp user/password@localhost/orcl file= D:\GPSDATA0613.dmp full=y ignore=y;

```

full=y是指导出全部，把表、存储过程、函数等一起导出，导入时也一样，导入中的ignore=y是忽略重复表，就是原来你存在这些表中的某个的话，会报错误信息，加上这个就不会了。





## 数据泵-导出expdp



### 创建目录映射

```sql
 CREATE DIRECTORY my_dir AS '/path/to/directory';
```

1. 查询现有目录是否满足条件

```sql
select * from DBA_DIRECTORIES;
```
删除数据目录
```sql
drop directory my_dir ;
```


```sql
expdp 用户名/密码@数据库实例 DIRECTORY=目录名称 DUMPFILE=导出文件名.dmp   EXCLUDE=TABLE:"IN ('table1','table2')"  INCLUDE=TABLE:"IN ('EMPLOYEES', 'DEPARTMENTS')"   FULL=Y


--按用户导
expdp user/password@SID schemas=u_mom_um dumpfile=expdp.dmp directory=dmp logfile=expdlog.log;

--按表名导
expdp user/password@SID tables=test1,test2 dumpfile=expdp.dmp directory=dmp logfile=expdlog.log;

--按查询条件导
expdp user/password@SID directory=dmp dumpfile=expdp.dmp Tables=test query='WHERE id<20' logfile=expdlog.log;

--按表空间导
expdp user/password@SID directory=dmp dumpfile=expdp.dmp TABLESPACES={#表空间1},{#表空间2} logfile=expdlog.log;

--导整个库
expdp user/password@SID directory=dmp dumpfile=expdp.dmp FULL=y logfile=expdlog.log;


expdp system/password DIRECTORY=dump_dir DUMPFILE=full_backup.dmp LOGFILE=full_backup.log FULL=YES



--导整个库
expdp ewf/ewf123@ORCL directory=EXPDP_DUMP dumpfile=ewf.dmp logfile=ewf_logfile.log schemas=ewf
expdp ewf/ewf123@ORCL directory=EXPDP_DUMP dumpfile=ewf.dmp logfile=ewf_logfile.log FULL=y


```




## 数据泵-导入impdp

```sql
--命令参考
impdp 用户名/密码@数据库实例 DIRECTORY=目录名称 DUMPFILE=导入文件的名称.dmp REMAP_SCHEMA=源用户名:目标用户名
--举例
impdp user/password@SID DIRECTORY=DMPDATA DUMPFILE=fileName.dmp remap_tablespace=um_dev:um remap_schema=u_um_dev:u_um

# 从一个用户导入到另一个用户
impdp ewf/ewf123@orcl106 DIRECTORY=IMPDP_DUMP DUMPFILE=EWF.dmp schemas=ewf remap_schema=ewf:system

# 从一个表空间导入到另一个表空间
impdp ewf/ewf123@orcl106 DIRECTORY=IMPDP_DUMP DUMPFILE=EWF.dmp tablespaces=tbsp_1


impdp ewf/ewf123@orcl106 DIRECTORY=IMPDP_DUMP DUMPFILE=EWF.dmp schemas=ewf
impdp ewf/ewf123@orcl106 DIRECTORY=IMPDP_DUMP DUMPFILE=ORACLE140.DMP full=y
```


## 过程错误处理

```sql


```

