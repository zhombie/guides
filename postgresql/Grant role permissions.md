```sql
SELECT grantee, table_schema, table_name, privilege_type
FROM information_schema.role_table_grants
WHERE grantee = 'test';
```

```sql
SELECT schemaname, matviewname, matviewowner
FROM pg_catalog.pg_matviews
WHERE has_table_privilege('test', format('%I.%I', schemaname, matviewname), 'SELECT')
ORDER BY schemaname, matviewname;
```

```sql
SELECT grantee, table_schema, table_name, privilege_type
FROM information_schema.role_table_grants 
WHERE grantee = 'test' AND table_name IN (SELECT table_name FROM information_schema.views)
ORDER BY table_schema, table_name;
```

```sql
SELECT rolname, rolsuper, rolcreaterole, rolcreatedb, rolcanlogin
FROM pg_roles
WHERE rolname = 'test';
```

```sql
SELECT datname, has_database_privilege('test', datname, 'CONNECT') AS can_connect
FROM pg_database;
```

```sql
SELECT r.rolname AS role, m.rolname AS member
FROM pg_auth_members am
JOIN pg_roles r ON am.roleid = r.oid
JOIN pg_roles m ON am.member = m.oid WHERE m.rolname = 'test';
```

```sql
grant usage on schema public to test;
```

```sql
grant select on public.table1 to test;
```

```sql
grant select on public.table2 to test;
```

```sql
grant select on public.table3 to test;
```

```sql
grant select on public.table4 to test;
```

```sql
grant select on public.table5 to test;
```
