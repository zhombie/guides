```
SELECT setval('schema.table_id_seq', (SELECT MAX(id) + 1 FROM schema.table));
```
