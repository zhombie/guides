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

# Index size

```sql
SELECT
    schemaname,
    relname,
    indexrelname,
    pg_size_pretty(pg_relation_size(indexrelid)) AS size
FROM pg_stat_user_indexes
WHERE idx_scan = 0
ORDER BY pg_relation_size(indexrelid) DESC;
```
