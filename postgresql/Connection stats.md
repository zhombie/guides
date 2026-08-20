```sql
SELECT
  current_setting('max_connections')::int                    AS max_connections,
  current_setting('superuser_reserved_connections')::int     AS su_reserved,
  current_setting('reserved_connections')::int               AS reserved,   -- new in PG16
  count(*)                                                   AS current_total,
  count(*) FILTER (WHERE backend_type = 'client backend')     AS client_conns,
  current_setting('max_connections')::int
    - current_setting('superuser_reserved_connections')::int
    - current_setting('reserved_connections')::int
    - count(*) FILTER (WHERE backend_type = 'client backend') AS available
FROM pg_stat_activity;
```

```sql
SELECT datname, usename, state, count(*)
FROM pg_stat_activity
WHERE backend_type = 'client backend'
GROUP BY 1,2,3
ORDER BY 4 DESC;
```

```sql
SELECT
  pid, application_name, client_addr, state,
  now() - backend_start  AS conn_age,
  now() - state_change   AS in_state,
  now() - xact_start     AS xact_age,
  query
FROM pg_stat_activity
WHERE backend_type = 'client backend'
ORDER BY state, in_state DESC;
```

```sql
SELECT
  usename,
  application_name,
  client_addr,
  state,
  count(*) AS connections
FROM pg_stat_activity
GROUP BY usename, application_name, client_addr, state
ORDER BY connections DESC;
```
