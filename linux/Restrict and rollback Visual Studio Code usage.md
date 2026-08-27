# Restrict

```shell
rm -rf /home/centos/.vscode-server
```

```shell
install -d -o root -g root -m 0000 /home/centos/.vscode-server
```

```shell
chattr +i /home/centos/.vscode-server
```

# Rollback

```shell
chattr -i /home/centos/.vscode-server
```

```shell
rmdir /home/centos/.vscode-server
```
