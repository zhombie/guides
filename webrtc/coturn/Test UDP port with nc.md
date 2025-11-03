# Remote machine

1) Install
```
dnf install nc
```

3) Connect
```
nc -u -l 55000
```

3) Wait for message

# Local machine

1) Connect
```
nc -u <public_ip_address> 55000
```

2) Send message
