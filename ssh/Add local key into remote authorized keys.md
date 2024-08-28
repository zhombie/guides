# ssh connection without password prompt

* Add your local ssh key to ```~/.ssh/autorized_keys``` by entering locally:

if you already have known hostname in ssh configuration enter:

```ssh-copy-id -i ~/.ssh/id_ed25519.pub <remote address>```

if not:

```ssh-copy-id -i ~/.ssh/id_ed25519.pub root@<remote address> -p 22```

where, ```~/.ssh/id_ed25519.pub``` is ssh public key on your local computer, second argument is ssh connection
