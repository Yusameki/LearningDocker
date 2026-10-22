<div align="center">

# 🐳 学习 Docker 的一点记录

**跟着视频一点点抄下来、又自己动手跑过一遍的 Docker 笔记**

<sub>[English](README.md) · [日本語](README.ja.md) · **中文**</sub>

<sub>主要参考了 [狂神说](https://space.bilibili.com/95256449) 的 [视频](https://www.bilibili.com/video/BV1og4y1q7M4)，非常感谢 🙏</sub>

</div>

---

## 📑 目录

- [安装 Docker（Ubuntu）](#安装-dockerubuntu)
- [基础指令笔记](#基础指令笔记)
- [小练习](#小练习)

---

## 安装 Docker（Ubuntu）

### ① 卸载老版本

```bash
sudo apt-get remove docker docker-engine docker.io containerd runc
```

### ② 设置存储库

```shell
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
```

指纹应该是这样：

```
pub   rsa4096 2017-02-22 [SCEA]
      9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
sub   rsa4096 2017-02-22 [S]
```

```shell
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

### ③ 安装 Docker Engine

```shell
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

### ④ 检查一下

```shell
sudo docker run hello-world
```

看到熟悉的 `Hello from Docker!` 就装好啦 ✨

## 基础指令笔记

入门的时候把最常用的那批命令都抄了一遍，汇总在这里：

→ [Docker 常用指令](https://github.com/Yusameki/LearningDocker/blob/master/Docker常用指令.md)

## 小练习

边学边动手的几个小作业：

| 练习 | 内容 |
| --- | --- |
| [Docker 安装 Nginx](https://github.com/Yusameki/LearningDocker/blob/master/practice/Docker小练习1-nginx.md) | 第一次把镜像跑成网页 |
| [Docker 部署 Tomcat](https://github.com/Yusameki/LearningDocker/blob/master/practice/Docker小练习2-tomcat.md) | 顺手试了端口映射 |
| [commit 一个自带 webapps 的 tomcat](https://github.com/Yusameki/LearningDocker/blob/master/practice/Docker实战演练1-commit.md) | 用自己的容器搓镜像 |
| [nvidia-docker（日本語）](https://github.com/Yusameki/LearningDocker/blob/master/practice/nvidia-docker-on-windows.md) | 在 Windows 上让容器摸到 GPU |

---

<div align="center">
<sub>记录还在慢慢补，Docker 的路也还在慢慢走 (´-ω-`)</sub>
</div>
