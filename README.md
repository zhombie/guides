# instructions

---

## linux

### 1. sudo command without password prompt configuration:

* firstly, change sudoers configuration. in order to change configurations, enter sudoers configuration file by:
```
sudo visudo
```

* add following line at the bottom, in order to make **journalctl** usage without password prompt for **sampleuser**:
```
sampleuser ALL = (root) NOPASSWD: /bin/journalctl
```

---

## ssh

### 1. ssh connection without password prompt

* add your computer ssh key to ```~/.ssh/autorized_keys``` by entering locally:

if you already have known hostname in ssh configuration enter:

```ssh-copy-id -i ~/.ssh/id_rsa.pub vlx```

if not:

```ssh-copy-id -i ~/.ssh/id_rsa.pub today@vlx.kz -p 22```

where, ```~/.ssh/id_rsa.pub``` is ssh public key on your local computer. second argument is ssh connection.
