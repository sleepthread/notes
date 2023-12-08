[MyBatis](https://so.csdn.net/so/search?q=MyBatis&spm=1001.2101.3001.7020 "https://so.csdn.net/so/search?q=MyBatis&spm=1001.2101.3001.7020") 插入null 或 更新null SQL Server 报错

## [](#)[](#)报错信息

java实体类属性类型`Double`；sql server数据库对应的类型`float`  
使用Mybatis向sql server插入空值float类型的数据报错，其他类型没发现报错，报错信息如下：  
本文链接：[https://blog.csdn.net/qq_24505485/article/details/103573657](https://blog.csdn.net/qq_24505485/article/details/103573657 "https://blog.csdn.net/qq_24505485/article/details/103573657")

```
`### Error updating database.  Cause: com.microsoft.sqlserver.jdbc.SQLServerException: 操作数类型冲突: varbinary 与 float 不兼容
### The error may exist in com/xxxx/xxxx/xxxxDao.java (best guess)
### The error may involve com/xxxx/xxxx/xxxxDao.updateJingShaLingYong-Inline
### The error occurred while setting parameters
### SQL: UPDATE XXXXXXXX SET XXX=?,XXXXX=? WHERE id=?
### Cause: com.microsoft.sqlserver.jdbc.SQLServerException: 操作数类型冲突: varbinary 与 float 不兼容
; uncategorized SQLException; SQL state [S0002]; error code [206]; 操作数类型冲突: varbinary 与 float 不兼容; nested exception is com.microsoft.sqlserver.jdbc.SQLServerException: 操作数类型冲突: varbinary 与 float 不兼容] with root cause
com.microsoft.sqlserver.jdbc.SQLServerException: 操作数类型冲突: varbinary 与 float 不兼容
    at com.microsoft.sqlserver.jdbc.SQLServerException.makeFromDatabaseError(SQLServerException.java:262)
    at com.microsoft.sqlserver.jdbc.SQLServerStatement.getNextResult(SQLServerStatement.java:1624)
    at com.microsoft.sqlserver.jdbc.SQLServerPreparedStatement.doExecutePreparedStatement(SQLServerPreparedStatement.java:594)
    at com.microsoft.sqlserver.jdbc.SQLServerPreparedStatement$PrepStmtExecCmd.doExecute(SQLServerPreparedStatement.java:524)
    at com.microsoft.sqlserver.jdbc.TDSCommand.execute(IOBuffer.java:7194)
    at com.microsoft.sqlserver.jdbc.SQLServerConnection.executeCommand(SQLServerConnection.java:2979)
    at com.microsoft.sqlserver.jdbc.SQLServerStatement.executeCommand(SQLServerStatement.java:248)
    at com.microsoft.sqlserver.jdbc.SQLServerStatement.executeStatement(SQLServerStatement.java:223)` 

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17

```

## [](#)[](#)排查过程

经过实际测试，我将报错的sql直接在Microsoft SQL Server Management Studio中运行 是可以将float字段设置为null的。所以问题应该出现在了框架上；网络检索后，有人指出是因为Mybatis无法对null进行类型转换导致的（`//todo 以后有时间会深入分析下具体原因`）

## [](#)[](#)解决办法：

1. 更新数据库字段为decimal或numeric
2. 给原来的实体类属性指定jdbcType（指定为DOUBLE也可以，其他数字类型我还没试）  
    xml或注解配置中可以这样指定jdbcType`#{field1, jdbcType=NUMERIC}）`（  
    使用Mybatis Plus 3.1.2以上版本，可以这样配置属性注解  
    `@TableField(updateStrategy = FieldStrategy.IGNORED, jdbcType = JdbcType.NUMERIC)`

## [](#)[](#)其他可能解决的办法

在mybatis的配置文件中进行如下设置（不过该方法对我无效）：

```
`<settings>
        <setting name="jdbcTypeForNull" value="NULL" />
</settings>` 

- 1
- 2
- 3

```

官网[jdbcTypeForNull设置](https://mybatis.org/mybatis-3/configuration.html#settings "https://mybatis.org/mybatis-3/configuration.html#settings")的介绍如下：  
[https://mybatis.org/mybatis-3/configuration.html#settings](https://mybatis.org/mybatis-3/configuration.html#settings "https://mybatis.org/mybatis-3/configuration.html#settings")

|Setting|Description|Valid Values|Default|
|---|---|---|---|
|jdbcTypeForNull|Specifies the JDBC type for null values when no specific JDBC type was provided for the parameter. _**Some drivers require specifying the column JDBC type**_ but others work with generic values like NULL, VARCHAR or OTHER.|JdbcType enumeration. Most common are: NULL, VARCHAR and OTHER|OTHER|

这里可能是因为对mssql-jdbc驱动无效吧！

参考链接：[https://stackoverflow.com/questions/16191296/insert-null-in-a-database](https://stackoverflow.com/questions/16191296/insert-null-in-a-database "https://stackoverflow.com/questions/16191296/insert-null-in-a-database")  
本文链接：[https://blog.csdn.net/qq_24505485/article/details/103573657](https://blog.csdn.net/qq_24505485/article/details/103573657 "https://blog.csdn.net/qq_24505485/article/details/103573657")