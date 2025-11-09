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
sudo dnf install --enablerepo=elasticsearch elasticsearch
```

```
mv /var/lib/elasticsearch /data/elasticsearch
```

```
sudo semanage fcontext -a -t elasticsearch_var_lib_t "/data/elasticsearch(/.*)?"
```

```
cp /etc/elasticsearch/elasticsearch.yml /etc/elasticsearch/elasticsearch.yml.bak
```

```
nano /etc/elasticsearch/elasticsearch.yml
```

```
cp /etc/elasticsearch/jvm.options /etc/elasticsearch/jvm.options.bak
```

```
sudo systemctl enable --now elasticsearch
```

```
systemctl status elasticsearch
```

```
curl -X GET http://localhost:9200/ -v
```

```
ss -tulnp | grep 9200
```
