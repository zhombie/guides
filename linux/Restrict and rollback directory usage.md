# Restrict Visual Studio Code

```shell
rm -rf /home/centos/.vscode-server
```

```shell
install -d -o root -g root -m 0000 /home/centos/.vscode-server
```

```shell
chattr +i /home/centos/.vscode-server
```

# Restrict Cursor

```shell
rm -rf /home/centos/.cursor
```

```shell
install -d -o root -g root -m 0000 /home/centos/.cursor
```

```shell
chattr +i /home/centos/.cursor
```

```shell
rm -rf /home/centos/.cursor-server
```

```shell
install -d -o root -g root -m 0000 /home/centos/.cursor-server
```

```shell
chattr +i /home/centos/.cursor-server
```

# Restrict Claude Code

```shell
rm -rf /home/centos/.claude
```

```shell
install -d -o root -g root -m 0000 /home/centos/.claude
```

```shell
chattr +i /home/centos/.claude
```

```shell
rm -rf /home/centos/.claude-server
```

```shell
install -d -o root -g root -m 0000 /home/centos/.claude-server
```

```shell
chattr +i /home/centos/.claude-server
```

# Restrict Copilot

```shell
rm -rf /home/centos/.copilot
```

```shell
install -d -o root -g root -m 0000 /home/centos/.copilot
```

```shell
chattr +i /home/centos/.copilot
```

# Rollback

```shell
chattr -i <path>
```

```shell
rmdir <path>
```
