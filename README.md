# Docker学习
学习docker的一点记录，

参考了[狂神说](https://space.bilibili.com/95256449)的[视频](https://www.bilibili.com/video/BV1og4y1q7M4)。

非常感谢。



## Docker安装（Ubuntu）

> 卸载老版本

```bash
$ sudo apt-get remove docker docker-engine docker.io containerd runc
```



> 设置存储库

```shell
$ sudo apt-get update

$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
    
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

$ sudo apt-key fingerprint 0EBFCD88

pub   rsa4096 2017-02-22 [SCEA]
      9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
sub   rsa4096 2017-02-22 [S]

$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```



> 安装Docker Engine

```shell
 $ sudo apt-get update
 $ sudo apt-get install docker-ce docker-ce-cli containerd.io
```



> 检查安装结果

```shell
$ sudo docker run hello-world
```



## 初步学习

入门了一些非常基础的操作，

总结：

[Docker常用指令](https://github.com/Yusameki/LearningDocker/blob/master/Docker常用指令.md)



## 练习

> 小作业

[Docker安装Nginx](https://github.com/Yusameki/LearningDocker/blob/master/practice/Docker小练习1-nginx.md)

[Docker部署Tomcat](https://github.com/Yusameki/LearningDocker/blob/master/practice/Docker小练习2-tomcat.md)