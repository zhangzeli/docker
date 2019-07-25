[dockerfile-reference](https://docs.docker.com/v17.09/engine/reference/builder/)

# Dockerfile Format
```
Format
    1. # Comment
    2. INSTRUCTION arguments
The instruction is not case-sensitive
    However,convention is for then to be UPPER CASE to distinguish them from arguments more easily

Docker runs instruction in a Dockerfile in order
```

# Dockerfile Instructions

```
FROM
    from 指令是最重要的一个且必须为DockerFile文件开篇的第一个非注释行，用于为镜像文件构建过程
    指定基准镜像，后续的指令运行于此基准镜像所提供的运行环境

    实践中，基准镜像可以是任何可用镜像文件，默认情况下，docker build 会在docker主机上查找指定的镜像文件，在其不存在的时候
    则会从docker hub registry 上拉取所需要的镜像文件
    如果找不到指定的文件，docker build 会返回一个错误信息
Syntax
    FROM <REPOSITORY>[:tag] 或
    FROM <REPOSITORY>@<digest>
```

```
MAINTANIER(depreacted) -> LABLE
    用于让dockerfile制作提供本人的详细信息
    Dockerfile并不限制MAINTAINER指令可在出现的位置，但是推荐将其放置于FROM指令之后
Syntax 
    MAINTANIER <authtor's detail>
```


```
COPY
    用于从docker主机复制文件至创建的新镜像文件
    Dockerfile并不限制MAINTAINER指令可在出现的位置，但是推荐将其放置于FROM指令之后
Syntax 
    COPY <src>..<dest>
    COPY ["<src>","<dest>"]
文件复制准则
    <src>必须式build上下文中的路径，不能是其父目录
    如果src是目录，则其内部文件或子目录会被递归复制，但src目录自身不会被复制
    如果指定了多个src,或在src中使用了通配符，则dest必须是一个目录，且必须以/结尾
    如果dest事先不存在，它将被自动创建，这包括其父目录路径
```

```
WORKDIR
ADD
```

```
VOLUME
    用于在image中创建一个挂载点目录，以挂载Docker host上的卷或其它容器上的卷
Syntax
    VOLUME <mountpoint>
    VOLUME ["<mountpoint>"]
```


```
EXPOSE
    用于为容器打开指定要监听的端口以实现与外部通信
Syntax
    EXPOSE <port>[/<protocol>][<port>[/<protocol>]]
    protocol用于指定传输协议，可以为tcp或udp二者之一，默认为TCP协议
EXPOSE指令可以一次指定多个端口，列如
    EXPOSE 11211/udp 11211/tcp
```


```
ENV
    用于为镜像定义所需要的环境变量，并可被Dockerfile文件中位于其后的其它指令 如（ENV,ADD,COPY）所调用
    调用格式为$variable_name 或${variable_name}
Syntax
    ENV <key> <value>
    ENV <key>=<value>
    第一种格式中<key>之后的所有内容均被视作其<value>的组成部分，因此，一次只能设置一个变量
    第二中格式可用一次设置多个变量，每个变量为一个"key=value"的键值对，如果<value>中包含特殊字符可用（\）进行转义；
    另外反斜线也可用于续航
```

```
RUN
CMD 
    类似于RUN指令，CMD指令也可用用于运行任何命令或应用程序，不过，二者的运行时间点不同
        RUN指令运行于镜像文件构建过程中，而CMD指令运行于基于Dockerfile构建出得到新镜像文件启动一个容器时
        CMD指令的首要目的在于为启动的容器指定默认要运行的程序，且其运行结束后，容器也将终止；不过，CMD指令的命令其实可以被docker run 命令行的选项所覆盖
        在Dockerfile中可以存在多个CMD指令，但仅最后一个会生效
Syntax
    CMD <command>
    CMD ["<EXECUTABLE>","PARAM1","PARAM2"]
    CMD ["PARAM1","PARAM2"] 

    前两种语法格式的意义同RUN
    第三种则用于为ENTRYPOINT指令提供默认参数

ENTRYPOINT 
    类似CMD指令的功能，用于为容器指定默认运行程序，从而使得容器像一个单独的可执行程序
    与CMD不同的是，有ENTRYPOINT启动的程序不会被docker run命令行指定的参数所覆盖，而且，这些命令行参数会被当做参数传递给ENTRYPOINT指定的程序
        不过，docker run 命令的 --entrypoint选项的参数可覆盖ENTRYPOINT指令指定的程序
Syntax
    ENTRYPOINT <command>
    ENTRYPOINT ["<executable>","<param1>","<param2>"]

docker run命令传入的命令参数会覆盖CMD指令的内容并且附加到ENTRYPOINT命令最后做为其参数使用
Dockerfile 文件中也可以存在多个ENTRYPOINT指令，但仅最后一个会生效
```


```
USER
    用于指定运行image时的或运行Dockerfile中任何RUN,CMD或ENTRPOINT指令指定的程序时的用户名或UID
        RUN指令运行于镜像文件构建过程中，而CMD指令运行于基于Dockerfile构建出得到新镜像文件启动一个容器时
        默认情况下，container的运行身份为root
Syntax
    USER <uid>|<username>
    需要注意的式，<uid>可以为任何数字，但是实践中其必须为etc/passwd中某用户的有效UID,否则，docker run 命令将运行失败
```

```
HEALTHCHECK
    For example
        HEALTHCHECK --interval=5m --timout=3s \
        CMD curl -f http://localhost || exit 1
```

```
SHELL
    用于指定docker build 过程中运行的程序，其可以式任何命令

Syntax   
    RUN <command>或
    RUN ["executable","param1","param2"]
JSON数组中要用双引号
```

```
ARG
    在build-time阶段
```

```
ONBULD
    用于在Dockerfile中定义一个触发器
```