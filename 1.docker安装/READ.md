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