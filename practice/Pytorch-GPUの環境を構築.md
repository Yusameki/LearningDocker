# Dockerを試す

Takayama様のDockerFileからGPU動作のPytorch環境を構築したい！



> Docker Imageのビルド

```shell
#DockerFileが用意されたのでそのままビルド
$ docker build -f Dockerfile -t baabp/st:torch-cuda .

Successfully built 37c739e1f4a8
Successfully tagged baabp/st:torch-cuda
```



> Imageの確認

```shell
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
baabp/st            torch-cuda          37c739e1f4a8        3 minutes ago       10.8GB
```



> Docker コンテナの起動

```shell
#Coposeファイルの要求に従って起動したい
$ docker-compose up
Creating baabp-st_master ... error

ERROR: for baabp-st_master  Cannot create container for service baabp-st_master: status code not OK but 500: {"Message":"Unhandled exception: Filesharing has been cancelled","StackTrace":" ....
ERROR: Encountered errors while bringing up the project.
```

エラーが出た，調べてみたらDockerのShareフォルダの問題かも．

File Sharingに全Diskを追加．

```shell
$ docker-compose up -d
Creating baabp-st_master ... error

ERROR: for baabp-st_master  Cannot create container for service baabp-st_master: Unknown runtime specified nvidia....
ERROR: Encountered errors while bringing up the project.
```

Nvidia-Dockerが無かったので，docker runを試みる．

```shell
$ docker run --gpus all nvidia/cuda nvidia-smi
docker: Error response from daemon: could not select device driver "" with capabilities: [[gpu]].
```

調べたら，nvidia-container-runtimeがwindowsに対応していないことが分かった．

Docker desktopはWSL2インストール後必要なくなるためアンインストールする．



> windowsでGPUを動かすために

更に調べると，まだリリースしていないwindowsの20xxx版にWSL2が搭載されていることが分かった．

WSLはwindowsに搭載されているLinuxなので，当然Linuxに対応したnvidia-container-runtimeが使用できる．

しかし，WSLにはnvidiaのドライバーを導入することが出来ないため，CUDAも当然使えない．

そこでWSL2になると，なんと専用のGPUドライバーが

[CUDA on Windows Subsystem for Linux (WSL) - Public Preview](https://developer.nvidia.com/cuda/wsl)

出ていることが分かった．

[CUDA on WSL User Guide](https://docs.nvidia.com/cuda/wsl-user-guide/index.html#abstract)

このサイトのガイドに従ってインストール．まとめると

1. Windowsのinsiderプログラムに参加し，previewにアップデート
2. WSL2をオンにする
3. Ubuntuをダウンロード
4. CUDAをインストール
5. dockerとnvidia-container-runtimeを導入する

になります．

時間があったらWSL2でGPUを使う手順を別ファイルでまとめる．



> インストールが終わったらGPUベンチマークで試す

```shell
$ docker run --gpus all nvcr.io/nvidia/k8s/cuda-sample:nbody nbody -gpu -benchmark 
> Compute 6.1 CUDA device: [TITAN X (Pascal)]
28672 bodies, total time for 10 iterations: 23.859 ms
= 344.556 billion interactions per second
= 6891.125 single-precision GFLOP/s at 20 flops per interaction
#TITAN Xが無事に認識できた！
```



> Docker-composeをインストールする

普通のLinuxと同じ扱いなので下のオフィシャルガイドに従ってやる

[Docker Compose のインストール](http://docs.docker.jp/compose/install.html#linux-compose)

```shell
#事前準備としてcurlが必要
$ sudo curl -L https://github.com/docker/compose/releases/download/1.16.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
```



> もう一度buildする

```shell
#docker-composeファイルを使ってビルドしてみる
$ docker-compose build
ERROR: Version in "./docker-compose.yml" is unsupported.

#バージョンが違ったみたい，最新版を探してインストール
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.26.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

#もう一度試す
$ docker-compose build

```

