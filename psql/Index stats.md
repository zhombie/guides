# Index utilization

```sql
SELECT *
FROM pg_stat_user_indexes
WHERE schemaname = '<schema>' AND relname = '<table>';
```

# Last reset date & time

```sql
SELECT stats_reset 
FROM pg_stat_database 
WHERE datname = current_database();
```
