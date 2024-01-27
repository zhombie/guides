# Guides

---

## Linux

### 1. sudo command without password prompt configuration:

* Firstly, change sudoers configuration. in order to change configurations, enter sudoers configuration file by:
```
sudo visudo
```

* Add following line at the bottom, in order to make **journalctl** usage without password prompt for **sampleuser**:
```
sampleuser ALL = (root) NOPASSWD: /bin/journalctl
```

### 2. Calculate script execution time (tested on python script):

* Simple example:

```
time python <script-name>.py
```

* If you have Pipenv environment:

```
time pipenv run python <script-name>.py
```

---

## ssh

### 1. ssh connection without password prompt

* Add your computer ssh key to ```~/.ssh/autorized_keys``` by entering locally:

if you already have known hostname in ssh configuration enter:

```ssh-copy-id -i ~/.ssh/id_rsa.pub <remote address>```

if not:

```ssh-copy-id -i ~/.ssh/id_rsa.pub root@<remote address> -p 22```

where, ```~/.ssh/id_rsa.pub``` is ssh public key on your local computer. second argument is ssh connection.

### 2. ssh chain tunnel

> Means remote server, that you really need is only accessible from another remote server. there is no limit on ssh server jumps

```
Host remote-server1
  HostName server1.com
  User root
  Port 1234

Host remote-server2
  HostName 192.168.0.1
  User root
  ProxyJump remote-server1
  LocalForward 25555 127.0.0.1:5555
```

above ssh configuration shows us that we can connect directly to remote-server2 by ```ssh remote-server2``` simple command & ssh can decide that it has to connect firstly **remote-server1** and then connect to **remote-server2** on its own. all this work is done by attribute **ProxyJump**.

also there is another feature that provides ssh, which forwards network traffic by **LocalForward** attribute. it means, that all data sent to port 25555 will be sent to remote server.

### 3. ssh cleanup branches

```
git fetch -p && git branch -vv | awk '/: gone]/{print $1}' | xargs git branch -d
```


## scp

### 1. Download file from remote server

```
scp user@127.0.0.1:~/path/to/file.extension /path/to/target/output/directory/
```
