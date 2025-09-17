```sql
SELECT *
FROM pg_stat_user_indexes
WHERE schemaname = '<schema>' AND relname = '<table>';
```
