Packages

```
dnf update
```

```
dnf install epel-release
```

```
dnf install coturn
```

Setup

```
mv /etc/coturn/turnserver.conf /etc/coturn/turnserver.conf.bak
```

```
systemctl enable coturn
```

```
systemctl start coturn
```

Firewall

```
firewall-cmd --list-all
```

```
firewall-cmd --add-port=3478/tcp --zone=public --permanent
firewall-cmd --add-port=3478/udp --zone=public --permanent
firewall-cmd --add-port=3479/tcp --zone=public --permanent
firewall-cmd --add-port=3479/udp --zone=public --permanent
firewall-cmd --add-port=54000-65535/udp --zone=public --permanent
```

```
firewall-cmd --reload
```
