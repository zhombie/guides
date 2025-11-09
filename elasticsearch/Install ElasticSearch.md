```
rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch
```

```
sudo tee /etc/yum.repos.d/elasticsearch.repo <<'EOF'
[elasticsearch]
name=Elasticsearch repository for 9.x packages
baseurl=https://artifacts.elastic.co/packages/9.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=0
type=rpm-md
EOF
```

```
sudo dnf update -y
```

```
sudo dnf install -y elasticsearch
```
