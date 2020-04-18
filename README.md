# instructions

1. sudo command without **password prompt** configuration:

in order to change configurations, enter sudoers configuration file by:
```
sudo visudo
```

add following line at the bottom, in order to make **journalctl** usage without password prompt for **sampleuser**:
```
sampleuser ALL = (root) NOPASSWD: /bin/journalctl
```
