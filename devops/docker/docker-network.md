# Docker Network

1. Create Docker Network
2. Connect Docker Network
3. Create Static IP Docker Network

Create Docker Network

```
docker create network java_net
```

Connect Docker Network

```
docker connect network java_net app1
docker connect network java_net app2
```

Create Static IP Docker Network

```
docker create network --submit=172.15.0.0/16 java_net

```



