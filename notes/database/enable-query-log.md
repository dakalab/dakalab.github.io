# Enable MySQL Query Log

You can enable and watch raw sql query log in your mysql server by using below commands:

```sql
SET GLOBAL general_log = 'ON';
SET GLOBAL log_output = 'table';
```

Then you can use below sql to fetch query logs:

```sql
SELECT * FROM mysql.general_log;
```
