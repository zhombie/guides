### Install

```
dnf install httpd-tools
```

### Create

```
htpasswd /etc/nginx/.htpasswd username
```

### Test

```
htpasswd -vb /etc/nginx/.htpasswd username password
```
