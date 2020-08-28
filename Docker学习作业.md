# Docker学习作业1

> Docker安装nginx

```shell
#1.搜索镜像	search
#2.下载镜像	pull
```

```shell
PS C:\Windows\system32> #docker pull nginx
Using default tag: latest
latest: Pulling from library/nginx
bf5952930446: Pull complete
cb9a6de05e5a: Pull complete
9513ea0afb93: Pull complete
b49ea07d2e93: Pull complete
a5e4a503d449: Pull complete
Digest: sha256:b0ad43f7ee5edbc0effbc14645ae7055e21bc1973aee5150745632a24a752661
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest
```

> 运行测试

```shell
PS C:\Windows\system32> #docker run -d --name nginx01 -p 3344:80 nginx
dbb2fdf01794597bcbd90e7ccdd3eb0cb141922e340547e061b1ea7ec0f41273
PS C:\Windows\system32> #docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
dbb2fdf01794        nginx               "/docker-entrypoint.…"   7 seconds ago       Up 6 seconds        0.0.0.0:3344->80/tcp   nginx01
8ee32f7376bc        centos              "/bin/bash"              5 hours ago         Up 5 hours                                 elated_galileo
ba68a79f276c        ed15b5429189        "/docker-entrypoint.…"   6 hours ago         Up 6 hours          80/tcp                 quirky_brown
```

> 端口模式概要图

![docker-ports.png](https://github.com/Yusameki/LearningDocker/blob/master/Pictures/docker-ports.png?raw=true)

得开放3344端口才能从外部访问。



