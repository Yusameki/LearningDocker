<div align="center">

# 🐳 Learning Docker, bit by bit

**Docker notes I copied from a video series, then actually ran myself**

<sub>**English** · [日本語](README.ja.md) · [中文](README.zh-CN.md)</sub>

<sub>Main reference: [狂神说](https://space.bilibili.com/95256449)'s [video series](https://www.bilibili.com/video/BV1og4y1q7M4) — many thanks 🙏</sub>

</div>

---

## 📑 Contents

- [Install Docker (Ubuntu)](#install-docker-ubuntu)
- [Command cheat sheet](#command-cheat-sheet)
- [Small exercises](#small-exercises)

---

## Install Docker (Ubuntu)

### ① Remove old versions

```bash
sudo apt-get remove docker docker-engine docker.io containerd runc
```

### ② Set up the repository

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

The fingerprint should look like this:

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

### ③ Install Docker Engine

```shell
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

### ④ Check it

```shell
sudo docker run hello-world
```

If you see the familiar `Hello from Docker!`, you're done ✨

## Command cheat sheet

I copied down the most common commands while learning — collected here:

→ [Docker commands](https://github.com/Yusameki/LearningDocker/blob/master/Docker常用指令.md) *(in Chinese)*

## Small exercises

A few little assignments I did while learning:

| Exercise | What it covers |
| --- | --- |
| [Run Nginx in Docker](https://github.com/Yusameki/LearningDocker/blob/master/practice/Docker小练习1-nginx.md) *(zh)* | First time turning an image into a web page |
| [Deploy Tomcat in Docker](https://github.com/Yusameki/LearningDocker/blob/master/practice/Docker小练习2-tomcat.md) *(zh)* | Tried port mapping along the way |
| [Commit a tomcat with webapps baked in](https://github.com/Yusameki/LearningDocker/blob/master/practice/Docker实战演练1-commit.md) *(zh)* | Building an image from my own container |
| [nvidia-docker (日本語)](https://github.com/Yusameki/LearningDocker/blob/master/practice/nvidia-docker-on-windows.md) | Letting containers see the GPU on Windows |

---

<div align="center">
<sub>Still adding to these notes, still walking the Docker road (´-ω-`)</sub>
</div>
