# Update packages

```
dnf update -y
```

# Install nano

```
dnf install nano -y
```

# Install repo

```
cat <<EOF > /etc/yum.repos.d/redis.repo
[Redis]
name=Redis
baseurl=http://packages.redis.io/rpm/rockylinux9
enabled=1
gpgcheck=1
EOF
```

# Install GPG key

```
curl -fsSL https://packages.redis.io/gpg > /tmp/redis.key
```

```
rpm --import /tmp/redis.key
```

# Install Redis

```
dnf install redis -y
```

# Backup `redis.conf`

```
cp /etc/redis/redis.conf /etc/redis/redis.conf.bak
```

# Configuration

```
bind 127.0.0.1 <internal ip address>
maxmemory 6gb
maxmemory-policy allkeys-lru
requirepass foobared
appendonly yes
save 900 1
save 300 10
save 60 10000
```

# SELinux configuration

> If you want to install Redis into custom directory (for example, `/data/redis`)

```
mv /var/lib/redis /data/redis
```

Edit `ReadWriteDirectories=` from `ReadWriteDirectories=-/var/lib/redis` to `ReadWriteDirectories=-/data/redis`

```
nano /usr/lib/systemd/system/redis.service
```

Edit `dir` from `dir /var/lib/redis` to `dir /data/redis`

```
nano /etc/redis/redis.conf
```

```
systemctl daemon-reload
```

# Downgrade setuptools

```
sudo rm -rf /usr/local/lib/python3.9/site-packages/setuptools*
sudo rm -rf /usr/local/lib/python3.9/site-packages/pkg_resources*
```

```
sudo python3 -m pip install --force-reinstall "setuptools<70" --prefix=/usr --root-user-action ignore
```

```
python3 -c "import setuptools, os; print(setuptools.__file__)"
```

```
sudo semanage fcontext -a -t redis_var_lib_t "/data/redis(/.*)?"
```

```
sudo restorecon -R /data/redis
```

```
ls -Zd /data/redis
```

# Rollback setuptools

```
sudo python3 -m pip install --upgrade setuptools
```

# Start systemctl `redis`

```
systemctl enable --now redis
```

```
systemctl status redis
```

# Firewall configuration

```
firewall-cmd --permanent --zone=public --add-rich-rule='rule family="ipv4" source address="<remote ip address>/32" port protocol="tcp" port="6379" accept'
```

```
firewall-cmd --reload
```

```
firewall-cmd --list-all
```
