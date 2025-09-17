# Slow query

```sql
SELECT
    pid,
    user,
    application_name,
    client_addr,
    query_start,
    now() - query_start AS query_time,
    query,
    state,
    wait_event_type,
    wait_event
FROM pg_stat_activity
WHERE (now() - query_start) > interval '30 seconds'
ORDER BY query_time DESC;
```

# Blocking query

```sql
SELECT
    pid,
    pg_blocking_pids(pid) AS blocking_pids,
    user,
    application_name,
    client_addr,
    query_start,
    now() - query_start AS query_time,
    query,
    state,
    wait_event_type,
    wait_event
FROM pg_stat_activity
WHERE cardinality(pg_blocking_pids(pid)) > 0;
```
