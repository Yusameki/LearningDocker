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

Docker desktopはWSL2インストール後Ubuntu版と衝突するためアンインストールする．



> windowsでGPUを動かすために

更に調べると，まだ正式リリースしていないwindowsの20xxx版にWSL2が搭載されていることが分かった．

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

普通のLinuxと同じ扱いなので下のオフィシャルガイドに従ってやる．

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

#権限を設定する
sudo chmod +x /usr/local/bin/docker-compose

#もう一度試す
$ docker-compose build
Successfully built 856c99167742
Successfully tagged baabp/st:torch-cuda
#ビルド成功！

#ビルドを確認
$ docker images
REPOSITORY                       TAG                 IMAGE ID            CREATED             SIZE
baabp/st                         torch-cuda          856c99167742        12 minutes ago      10.8GB 
```



> コンテナ起動

docker-compose upでコンテナを起動する

```shell
$ docker-compose up
Creating network "satorch-master_default" with the default driver
Creating baabp-st_master ... done
Attaching to baabp-st_master
#起動成功？
$ docker ps
CONTAINER ID        IMAGE                 COMMAND             CREATED             STATUS              PORTS                                                      NAMES
cd0e23e6d855        baabp/st:torch-cuda   "/bin/bash"         6 minutes ago       Up 6 minutes        0.0.0.0:6006-6007->6006-6007/tcp, 0.0.0.0:8008->8008/tcp   baabp-st_master
```

コンテナに入ってみる

```shell
$ docker attach cd0e23e6d855
root@cd0e23e6d855:/src#
```

コンテナに入った，しかし全てのコマンドが使えない．

完全なるLinux環境が必要になるかも．

VSCodeのWSL Remoteを使って実現する．

1. VSCodeのWSL RemoteからWSLのUbuntuをRemoteで起動．
2. Ubuntu版のDocker Extensionをインストール．
3. Docker ExtensionでDockerの管理をして，コンテナに入る．

```shell 
$ docker exec -it cd0e23e6d8551edc91f5a34fb3db4098d0956f326a47d405af958ebda60bf022 bash <
root@cd0e23e6d855:/src# ls
Dockerfile  README.md  data  docker-compose.yml  notebook  requirements.txt  src
#srcフォルダは外部と連携しているため，ファイルにアクセス可能
```



> 色々試す

1. Jupyter Notebook

```shell
#色々の設定
root@cd0e23e6d855:/src# jupyter notebook --generate-config
Writing default config to: /root/.jupyter/jupyter_notebook_config.py
root@cd0e23e6d855:/src# jupyter notebook password
Enter password: 
Verify password: 
[NotebookPasswordApp] Wrote hashed password to /root/.jupyter/jupyter_notebook_config.json

#起動
root@cd0e23e6d855:/src# jupyter lab --ip=0.0.0.0 --port=8008 --allow-root
[I 14:19:42.807 LabApp] Writing notebook server cookie secret to /root/.local/share/jupyter/runtime/notebook_cookie_secret
[I 14:19:43.888 LabApp] JupyterLab extension loaded from /usr/local/lib/python3.6/dist-packages/jupyterlab
[I 14:19:43.889 LabApp] JupyterLab application directory is /usr/local/share/jupyter/lab
[I 14:19:43.892 LabApp] Serving notebooks from local directory: /src
[I 14:19:43.892 LabApp] Jupyter Notebook 6.1.3 is running at:
[I 14:19:43.892 LabApp] http://cd0e23e6d855:8008/
```

coposeファイルより，ローカルの8008ポートにあるはずなのでブラウザーで起動してみる

`http://localhost:8008/`

![jupyter.png](https://github.com/Yusameki/LearningDocker/blob/master/Pictures/jupyter.png?raw=true)

ちゃんと起動していることが分かる．