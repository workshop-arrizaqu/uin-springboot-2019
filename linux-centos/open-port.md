# Open Port

```
[root@mos-db-prod adminmos]# firewall-cmd --get-active-zones
FirewallD is not running
[root@mos-db-prod adminmos]# firewall-cmd --zone=public --add-port=5432/tcp --permanent
FirewallD is not running
[root@mos-db-prod adminmos]# systemctl start firewalld.service
[root@mos-db-prod adminmos]# firewall-cmd --get-active-zones
[root@mos-db-prod adminmos]# firewall-cmd --zone=public --add-port=5432/tcp --permanent
Warning: ALREADY_ENABLED: 5432:tcp
success
[root@mos-db-prod adminmos]# firewall-cmd --reload
success
```

## Referency

https://stackoverflow.com/questions/24729024/open-firewall-port-on-centos-7



