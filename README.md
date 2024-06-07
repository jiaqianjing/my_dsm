## 使用说明

### step1: 创建 macvlan 虚拟网络
```shell
sh ./network_macvlan.sh
```

### step2: 创建并运行 dsm 容器
```shell
docker compose -p dsm up -d
```

### step3: 查看并登录 dsm web 控制台
1. linux 终端查看容器状态
   ```shell
   docker compose ls
   ```
2. 登录 web 控制台
   ```shell
   http://{{dsm_container_ip}}:5000
   ```

### 销毁 dsm 容器
```shell
docker compose -p dsm down
```
