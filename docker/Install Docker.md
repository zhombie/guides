```
dnf update -y
```

```
dnf config-manager --add-repo https://download.docker.com/linux/rhel/docker-ce.repo
```

```
dnf install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

```
systemctl enable --now docker
```

```
systemctl status docker
```
