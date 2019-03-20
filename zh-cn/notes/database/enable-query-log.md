# 启用MySQL查询日志

你可以在你的数据库执行下面的语句来启用MySQL查询日志：

```sql
SET GLOBAL general_log = 'ON';
SET GLOBAL log_output = 'table';
```

然后你就可以用下面的SQL去获取日志：

```sql
SELECT * FROM mysql.general_log;
```
