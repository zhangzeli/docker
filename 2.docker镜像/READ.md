## About Docker Images
```
Docker镜像含有启动容器所需的文件系统，因此，其用于创建并且启动docker容器
采用分层构建机制，最底层为bootfs,其之为rootfs
    bootfs:用于系统引导的文件系统,包括bootloader和kernel,容器启动完成后会被卸载以节约内存资源
    rootfs:位于bootfs之上,表现为docker容器的根文件系统;
        传统模式中,系统启动之时,内核挂载rootfs时会首先将其挂载为"只读"模式,完整性自检完成后将其重新挂载为读写模式
        docker中,rootfs由内核挂载为"只读"模式,而后通过"联合挂载"技术额外挂载一个"可写"层
```
![bootfs图](../_img/2/rootfs.jpg)

## Docker Image Layer
```
    位于下层的镜像称为父镜像(parent image),最底层的称为基础镜像(base image)
    最上层为"可读"层,其下的均为"只读"层
```
![image图](../_img/2/image_layer.jpg)


## Docker Hub
+ Docker Hub provides the following major features
    - Image Repositories
    - Automated Builds
    - WebHooks
    - Organizations
    - GitHub and Bitbucket Integration

## Getting images 
```
默认会从docker hub 下载
docker pull <registry>[:<port>]/[<namespace>/]<name>:<tag>
docker pull quay.io/coreos/flannel:v0.10.0-amd64
```

## 镜像相关的操作
+ 镜像的生成途径
    - 基于容器制作
    - 基于DockerFile
    - Docker Hub automated builds
```
docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]

1.启动容器
    docker run --name zb1 -it busybox
2.制作镜像
    docker commit -a "zhangzeli<853089986@qq.com>" -c 'CMD ["/bin/httpd","-f","-h","/data/html"]' -p zb1 zzl/httpd:v0.2
```

## 镜像的导入和导出
```
docker save
    Save one or more images to tar archive
    Usage: docker  save [options] image[image...]
        --output,-o:write to a file,instead of STDOUT

docker load 
    Load an image from a tar archive or STDIN
    Usage: docker load [OPTIONS]
        --input,-i:Read from tar archive file,instead of STDIN
        --quite,-q:Suppress the load output
```