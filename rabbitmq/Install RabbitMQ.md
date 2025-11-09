# Install repo

```
rpm --import 'https://github.com/rabbitmq/signing-keys/releases/download/3.0/rabbitmq-release-signing-key.asc'
rpm --import 'https://github.com/rabbitmq/signing-keys/releases/download/3.0/cloudsmith.rabbitmq-erlang.E495BB49CC4BBE5B.key'
rpm --import 'https://github.com/rabbitmq/signing-keys/releases/download/3.0/cloudsmith.rabbitmq-server.9F4587F226208342.key'
```

```
sudo tee /etc/yum.repos.d/rabbitmq.repo <<'EOF'
##
## Zero dependency Erlang RPM
##

[modern-erlang]
name=modern-erlang-el9
# Use a set of mirrors maintained by the RabbitMQ core team.
# The mirrors have significantly higher bandwidth quotas.
baseurl=https://yum1.rabbitmq.com/erlang/el/9/$basearch
        https://yum2.rabbitmq.com/erlang/el/9/$basearch
repo_gpgcheck=1
enabled=1
gpgkey=https://github.com/rabbitmq/signing-keys/releases/download/3.0/cloudsmith.rabbitmq-erlang.E495BB49CC4BBE5B.key
gpgcheck=1
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
metadata_expire=300
pkg_gpgcheck=1
autorefresh=1
type=rpm-md

[modern-erlang-noarch]
name=modern-erlang-el9-noarch
# Use a set of mirrors maintained by the RabbitMQ core team.
# The mirrors have significantly higher bandwidth quotas.
baseurl=https://yum1.rabbitmq.com/erlang/el/9/noarch
        https://yum2.rabbitmq.com/erlang/el/9/noarch
repo_gpgcheck=1
enabled=1
gpgkey=https://github.com/rabbitmq/signing-keys/releases/download/3.0/cloudsmith.rabbitmq-erlang.E495BB49CC4BBE5B.key
       https://github.com/rabbitmq/signing-keys/releases/download/3.0/rabbitmq-release-signing-key.asc
gpgcheck=1
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
metadata_expire=300
pkg_gpgcheck=1
autorefresh=1
type=rpm-md

##
## RabbitMQ Server
##

[rabbitmq-el9]
name=rabbitmq-el9
baseurl=https://yum2.rabbitmq.com/rabbitmq/el/9/$basearch
        https://yum1.rabbitmq.com/rabbitmq/el/9/$basearch
repo_gpgcheck=1
enabled=1
# Cloudsmith's repository key and RabbitMQ package signing key
gpgkey=https://github.com/rabbitmq/signing-keys/releases/download/3.0/cloudsmith.rabbitmq-server.9F4587F226208342.key
       https://github.com/rabbitmq/signing-keys/releases/download/3.0/rabbitmq-release-signing-key.asc
gpgcheck=1
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
metadata_expire=300
pkg_gpgcheck=1
autorefresh=1
type=rpm-md

[rabbitmq-el9-noarch]
name=rabbitmq-el9-noarch
baseurl=https://yum2.rabbitmq.com/rabbitmq/el/9/noarch
        https://yum1.rabbitmq.com/rabbitmq/el/9/noarch
repo_gpgcheck=1
enabled=1
# Cloudsmith's repository key and RabbitMQ package signing key
gpgkey=https://github.com/rabbitmq/signing-keys/releases/download/3.0/cloudsmith.rabbitmq-server.9F4587F226208342.key
       https://github.com/rabbitmq/signing-keys/releases/download/3.0/rabbitmq-release-signing-key.asc
gpgcheck=1
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
metadata_expire=300
pkg_gpgcheck=1
autorefresh=1
type=rpm-md
EOF
```

# Update packages

```
dnf update -y
```

# Install RabbitMQ

```
dnf install -y logrotate erlang rabbitmq-server
```

# Test

```
erl -version
```

```
rabbitmqctl version
```

# Enable RabbitMQ Management

```
rabbitmq-plugins enable rabbitmq_management
```

# RabbitMQ configuration

```
sudo tee /etc/rabbitmq/rabbitmq.conf <<'EOF'
# Listen on all interfaces
listeners.tcp.default = 5672

# Web management UI
management.tcp.port = 15672
management.tcp.ip   = 0.0.0.0

# Enable memory and disk thresholds
vm_memory_high_watermark.relative = 0.7
disk_free_limit.absolute = 10G

# Logging
log.console = false
log.file.level = info
log.dir = /var/log/rabbitmq
log.file.rotation.count = 10
log.file.rotation.size = 20971520

# Default vhost tuning
default_user = <username>
default_pass = <password>
EOF
```

> If you want to install RabbitMQ into custom directory (for example, `/data/rabbitmq`)

```
mv /var/lib/rabbitmq /data/rabbitmq
```

Edit `WorkingDirectory=` from `WorkingDirectory=-/var/lib/rabbitmq` to `WorkingDirectory=-/data/rabbitmq`

```
nano /usr/lib/systemd/system/rabbitmq-server.service
```

# Systemctl start `rabbitmq-server`

```
systemctl enable --now rabbitmq-server
```

```
systemctl status rabbitmq-server
```

# User management

```
rabbitmqctl add_user <username> <password>
```

```
rabbitmqctl set_permissions -p / qbox ".*" ".*" ".*"
```

```
rabbitmqctl list_user_permissions <username>
```

```
rabbitmqctl set_user_tags <username> administrator
```

```
rabbitmqctl list_users
```

```
rabbitmqctl delete_user guest
```

# Logrotate configuration

```
sudo tee /etc/logrotate.d/rabbitmq <<'EOF'
/var/log/rabbitmq/*.log {
    weekly
    rotate 10
    compress
    missingok
    notifempty
    copytruncate
}
EOF
```

# Test

```
rabbitmq-diagnostics status
```

# Firewall configuration

```
firewall-cmd --permanent --zone=public --add-rich-rule='rule family="ipv4" source address="<remote ip address>/32" port protocol="tcp" port="5672" accept'
```

```
firewall-cmd --reload
```

```
firewall-cmd --list-all
```
