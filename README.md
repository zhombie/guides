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

## [ssh](ssh)

---

## [scp](scp)
