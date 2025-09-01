```sql
SELECT grantee, table_schema, table_name, privilege_type
FROM information_schema.role_table_grants
WHERE grantee = 'test';
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

```
grant usage on schema public to test;
grant select on public.table1 to test;
grant select on public.table2 to test;
grant select on public.table3 to test;
grant select on public.table4 to test;
grant select on public.table5 to test;
```
