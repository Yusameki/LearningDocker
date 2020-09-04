# Docker-commit

> Docker制作一个一开始就有webapps的tomcat

```shell
#启动一个默认的tomcat
```

```shell
$ docker run -it -p 8080:8080 --name tomcat01 tomcat
```



> 进入tomcat并修改webapps

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



> 提交新镜像

```shell
$ docker commit -a="yusameki" -m="add webapps" 22b07304da81 tomcat01:1.0
sha256:bd36d07b5c71dc91bc1475549236f2cc68386e8d783bfd31284344afc4099500
```

完成新镜像！

```shell
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
tomcat01            1.0                 bd36d07b5c71        46 seconds ago      652MB
```

