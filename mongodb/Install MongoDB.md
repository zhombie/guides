# Install repo

```
sudo tee /etc/yum.repos.d/mongodb-org-8.2.repo <<'EOF'
[mongodb-org-8.2]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/9/mongodb-org/8.2/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://pgp.mongodb.com/server-8.0.asc
EOF
```

# Install MongoDB Community edition

```
dnf install -y mongodb-org
```

# Backup `mongod.conf`

```
cp /etc/mongod.conf /etc/mongod.conf.bak
```

# SELinux configuration

> If you want to install MongoDB into custom directory (for example, `/data/mongodb`)

```
mv /var/lib/mongo /data/mongodb
```

```
sudo dnf install -y git make checkpolicy policycoreutils selinux-policy-devel
```

```
git clone https://github.com/mongodb/mongodb-selinux <path>
```

```
cd mongodb-selinux
```

```
make
```

```
make install
```

> `setuptools` should be at `/usr/lib/python3.9/site-packages/`, not `/usr/local/lib/python3.9/site-packages/`

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
sudo semanage fcontext -a -t mongod_var_lib_t "/data/mongodb(/.*)?"
```

```
sudo restorecon -R /data/mongodb
```

```
ls -Zd /data/mongodb
```

```
sudo python3 -m pip install --upgrade setuptools
```

# Start systemctl `mongod`

```
sudo systemctl start mongod
```

```
sudo systemctl status mongod
```
