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
cp /etc/coturn/turnserver.conf /etc/coturn/turnserver.conf.bak
```

```
systemctl enable --now coturn
```

Firewall

```
firewall-cmd --list-all
```

```
firewall-cmd --add-port=3478/tcp --zone=public --permanent
firewall-cmd --add-port=3478/udp --zone=public --permanent
firewall-cmd --add-port=54000-65535/udp --zone=public --permanent
```

```
firewall-cmd --reload
```
