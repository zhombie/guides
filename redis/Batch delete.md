```shell
redis-cli -n 1 --scan --pattern "*:key:*" | xargs -r redis-cli -n 1 DEL
```

```shell
redis-cli -n 1 --scan --pattern "*:key:*" | xargs -r redis-cli -n 1 UNLINK
```
