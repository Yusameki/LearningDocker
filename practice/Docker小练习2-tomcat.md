# Docker小练习2

> Docker安装tomcat

```shell
#直接用docker run命令实现安装和运行
 可以在docker hub上搜索版本号实现指定版本下载
```

```shell
$ docker run tomcat #如果加-rm的话可以实现stop容器就删除（不推荐）
Unable to find image 'tomcat:latest' locally
latest: Pulling from library/tomcat
d6ff36c9ec48: Already exists
c958d65b3090: Already exists
edaf0a6b092f: Already exists
80931cf68816: Already exists
bf04b6bbed0c: Pull complete
8bf847804f9e: Pull complete
6bf89641a7f2: Pull complete
3e97fae54404: Pull complete
10dee6830d45: Pull complete
680b26b7a444: Pull complete
Digest: sha256:cbdcddc4ca9b47e42c7d0c2db78cbc0f7a8b4bbe1fa395f4a53c5a236db29146
Status: Downloaded newer image for tomcat:latest
#正常启动后关闭并删除容器
```



> 运行测试

```shell
#看看有没有这个镜像
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
tomcat              latest              d5eef28cf41d        10 hours ago        647MB

#启动tomcat
$ docker run -d -p 3355:8080 --name tomcat01 tomcat
25cac9ccdb78a57d18dfb62d983c29eb25c18a3741921cd4bbaf2abc1e1c4357
#-d 后台启动
```



> 浏览器进入测试

![tomcat-browser.png](https://github.com/Yusameki/LearningDocker/blob/master/Pictures/tomcat-browser.png?raw=true)

测试进入没问题，但是无法显示tomcat



> 进入tomcat寻找理由

```shell
root@25cac9ccdb78:/usr/local/tomcat# ll
bash: ll: command not found
root@25cac9ccdb78:/usr/local/tomcat# ls
BUILDING.txt     LICENSE  README.md      RUNNING.txt  conf  logs            temp     webapps.dist
CONTRIBUTING.md  NOTICE   RELEASE-NOTES  bin          lib   native-jni-lib  webapps  work        
root@25cac9ccdb78:/usr/local/tomcat# cd webapps
root@25cac9ccdb78:/usr/local/tomcat/webapps# ls

#发现问题：1.缺乏linux命令（ll），2.没有webapps。
#原因：默认最小镜像，保证最小可运行环境。

root@25cac9ccdb78:/usr/local/tomcat# cd webapps.dist/
root@25cac9ccdb78:/usr/local/tomcat/webapps.dist# ls
ROOT  docs  examples  host-manager  manager    

#发现在webapps.dist下有webapps，复制进去即可（那为什么不一开始就）

root@25cac9ccdb78:/usr/local/tomcat# cp -r webapps.dist/* webapps
```



> 重新用浏览器访问测试

![tomcat-success.png](https://github.com/Yusameki/LearningDocker/blob/master/Pictures/tomcat-success.png?raw=true)

成功访问！