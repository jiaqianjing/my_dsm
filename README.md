## 使用说明

### step1: 创建 macvlan 虚拟网络
1. 创建 docker network 的 macvlan 接口
   ```shell
   sh ./network_macvlan.sh
   ```
2. 创建宿主机的 macvlan 接口 （用于宿主机和绑定 docker network macvlan 的容器通信），[传送门](https://blog.oddbit.com/post/2018-03-12-using-docker-macvlan-networks/#host-access)
   ```shell
   # 1. 在宿主机上创建一个名为 "mynet-shim" （可任意）的 macvlan 接口
   ip link add mynet-shim link enp4s0 type macvlan  mode bridge
   # 2. 设置这个设备的 ip (在上一步的脚本中已经设定好了)，并启动
   ip addr add 192.168.123.66/32 dev mynet-shim
   ip link set mynet-shim up
   # 3. 设置路由，使得主机和容器通信走这个创建的 macvlan 接口
   ip route add 192.168.123.64/28 dev mynet-shim
   ```   
<img width="1148" alt="image" src="https://github.com/jiaqianjing/my_dsm/assets/16071449/806f7722-aad0-46dd-aa8c-92014db6315a">



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
