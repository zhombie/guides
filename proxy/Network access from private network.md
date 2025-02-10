### Local machine

1) Download Squid

a) Windows:
Example: https://squid.diladele.com/

b) MacOS:
Example: https://formulae.brew.sh/formula/squid

2) Launch Squid

3) Test

```
telnet 127.0.0.1 3128
```

4) Add RemoteForward

```
Host ...
  ...
  RemoteForward 3128 127.0.0.1:3128
```

### Remote machine

1) Add proxy environment variables

```
nano ~/.bashrc
```

```
export http_proxy=http://127.0.0.1:3128
export https_proxy=http://127.0.0.1:3128
export ALL_PROXY=http://127.0.0.1:3128
```

```
source ~/.bashrc
```

2) Reconfigure yum proxy

```
nano /etc/yum.conf
```

```
proxy=http://127.0.0.1:3128
```
