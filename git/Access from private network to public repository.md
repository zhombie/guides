### Local machine

1) Add configuration for remote-vm with RemoteForward
```
Host remove-vm
  HostName 192.168.200.10
  User root
  RemoteForward 222 git.jetbrains.space:22
```

### Remote machine

1) Generate ssh key pair
```
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519 -q -N "" -C "[TEST] root@192.168.200.10"
```

2) Add configuration for git.jetbrains.space

```
nano ~/.ssh/config
```

```
Host git.jetbrains.space
  HostName git.jetbrains.space
  User git
  Port 222
```

3) Copy ssh public key & add to profile

```
cat ~/.ssh/id_ed25519.pub
```
