# Dockerを試す

Takayama様のDockerFileからGPU動作のPytorch環境を構築したい！



> Docker Imageのビルド

```shell
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
$ docker-compose up
Creating baabp-st_master ... error

ERROR: for baabp-st_master  Cannot create container for service baabp-st_master: status code not OK but 500: {"Message":"Unhandled exception: Filesharing has been cancelled","StackTrace":" 
ERROR: Encountered errors while bringing up the project.
```

エラーが出た，調べてみたらDockerのShareフォルダの問題かも

File Sharingに全Diskを追加

```shell
$ docker-compose up -d
Creating baabp-st_master ... error

ERROR: for baabp-st_master  Cannot create container for service baabp-st_master: Unknown runtime specified nvidia
```



