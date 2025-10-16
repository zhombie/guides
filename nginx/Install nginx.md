```
tee /etc/yum.repos.d/nginx.repo > /dev/null <<'EOF'
[nginx-stable]
name=nginx stable repo
baseurl=https://nginx.org/packages/rhel/9/$basearch/
gpgcheck=1
enabled=1
gpgkey=https://nginx.org/keys/nginx_signing.key
module_hotfixes=true
EOF
```

```
dnf install -y nginx
```

```
systemctl enable --now nginx
```

```
systemctl status nginx
```

```
firewall-cmd --permanent --add-service=http
```

```
firewall-cmd --permanent --add-service=https
```

```
firewall-cmd --reload
```

```
firewall-cmd --list-all
```

```
setsebool -P httpd_can_network_connect 1
```
