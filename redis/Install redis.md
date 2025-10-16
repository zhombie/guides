# Redis

```
dnf update -y
```

```
dnf install nano -y
```

```
cat <<EOF > /etc/yum.repos.d/redis.repo
[Redis]
name=Redis
baseurl=http://packages.redis.io/rpm/rockylinux9
enabled=1
gpgcheck=1
EOF
```

```
curl -fsSL https://packages.redis.io/gpg > /tmp/redis.key
```

```
rpm --import /tmp/redis.key
```

```
dnf install redis -y
```

```
cp /etc/redis/redis.conf /etc/redis/redis.conf.bak
```

```
bind 127.0.0.1 <internal ip address>
maxmemory 6gb
maxmemory-policy allkeys-lru
requirepass qbox
appendonly yes
save 900 1
save 300 10
save 60 10000
```

```
systemctl enable --now redis
```

```
systemctl status redis
```

```
firewall-cmd --permanent --zone=public --add-rich-rule='rule family="ipv4" source address="<remote ip address>/32" port protocol="tcp" port="6379" accept'
```

```
firewall-cmd --reload
```

```
firewall-cmd --list-all
```
