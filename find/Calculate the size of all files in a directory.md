Raw

```
find . -type f -mtime +30 -exec du -b {} + | awk '{total += $1} END {print "Total size:", total, "bytes"}'
```

Human-readable

```
find . -type f -mtime +30 -exec du -b {} + | awk '{total += $1} END {printf "Total size: %.2f GB\n", total/1024/1024/1024}'
```
