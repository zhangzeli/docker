## DOCKER程序环境
```
    docker程序环境：
        环境配置文件：
            /etc/sysyconfig/docker-network
            /etc/sysyconfig/docker-storage
            /etc/sysyconfig/docker
        Unit File:
            /usr/lib/systemd/system/docker.service
        Docker Registry配置文件：
            /etc/containers/registries.conf

        docker-ce:
            配置文件：/etc/docker/daemon.json

```
修改协议
[官方手册](https://docs.docker.com/engine/reference/commandline/dockerd/)



## DOCKER镜像加速
```
{
  "registry-mirrors": [
    "https://dockerhub.azk8s.cn",
    "https://reg-mirror.qiniu.com"
  ]
}

```

## DOCKER 常用命令
```
docker pull <registry>[:<port>]/[<namespace>/]<name>:<tag>

alpine版本是最小的版本，但是缺少调试工具.生产环境 不建议使用,一般自己构建并且上传到本地私有库

```
# docker配置

## docker 守护进程的C/S，其默认仅监听Unix Socket格式的地址，/var/run/docker.sock;
```
如果使用TCP套接字
/etc/docker/daemon.json:
    "hosts":["tcp://o.o.o.o:2375","unix:///var/run/docker.sock"]
客户端可以直接向docker传递”-H|--host“选项
```

## 自定义docker0桥的网络属性信息:/etc/docker/daemon.json文件

{
    "bip":"192.168.1.5/24",
    "fixed-cidr":"10.20.0.0/16",
    "fixed-cidr-v6":"2001.db8::/64",
    "mtu":1600,
    "default-gateway":"10.20.1.1",
    "default-gateway-v6":"2001.db8.abcd.::89",
    "dns":["10.20.1.2","10.20.1.3"]
}

核心选项为bip,及bridge，ip之意，用于docker0桥自身的IP地址；其它选项可通过此计算得出