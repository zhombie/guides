```
firewall-cmd --permanent --zone=public --add-rich-rule='rule family="ipv4" source address="<ip address>/32" port protocol="tcp" port="<port>" accept'
```

```
firewall-cmd --reload
```

```
firewall-cmd --list-all
```
