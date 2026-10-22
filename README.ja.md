<div align="center">

# 🐳 Docker を少しずつ学んだ記録

**動画を見ながら書き写して、そのあと自分で一回動かしてみた Docker ノート**

<sub>[English](README.md) · **日本語** · [中文](README.zh-CN.md)</sub>

<sub>主に [狂神説](https://space.bilibili.com/95256449) の [動画](https://www.bilibili.com/video/BV1og4y1q7M4) を参考にしました。本当にありがとう 🙏</sub>

</div>

---

## 📑 目次

- [Docker のインストール（Ubuntu）](#docker-のインストールubuntu)
- [基本コマンドのメモ](#基本コマンドのメモ)
- [小さな練習](#小さな練習)

---

## Docker のインストール（Ubuntu）

### ① 古いバージョンを削除

```bash
sudo apt-get remove docker docker-engine docker.io containerd runc
```

### ② リポジトリを設定

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

フィンガープリントはこうなるはずです：

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

### ③ Docker Engine をインストール

```shell
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

### ④ 確認する

```shell
sudo docker run hello-world
```

見覚えのある `Hello from Docker!` が出ればインストール完了です ✨

## 基本コマンドのメモ

入門のときに、よく使うコマンドを一通り写しました。ここにまとめてあります：

→ [Docker のよく使うコマンド](https://github.com/Yusameki/LearningDocker/blob/master/Docker常用指令.md) *（中国語）*

## 小さな練習

学びながら手を動かした小課題たち：

| 練習 | 内容 |
| --- | --- |
| [Docker で Nginx](https://github.com/Yusameki/LearningDocker/blob/master/practice/Docker小练习1-nginx.md) *（中）* | はじめてイメージを Web ページにした |
| [Docker で Tomcat をデプロイ](https://github.com/Yusameki/LearningDocker/blob/master/practice/Docker小练习2-tomcat.md) *（中）* | ついでにポートマッピングも試した |
| [webapps 入りの tomcat を commit](https://github.com/Yusameki/LearningDocker/blob/master/practice/Docker实战演练1-commit.md) *（中）* | 自分のコンテナからイメージを作る |
| [nvidia-docker（日本語）](https://github.com/Yusameki/LearningDocker/blob/master/practice/nvidia-docker-on-windows.md) | Windows 上でコンテナから GPU を触る |

---

<div align="center">
<sub>記録はまだ少しずつ増えていきます。Docker の道もまだまだ続きます (´-ω-`)</sub>
</div>
