# Docker学习概要

###  前言

感谢[狂神说](https://space.bilibili.com/95256449)给了我一些新的知识，

~~最后半年的学校生活~~，加油!

---



### 一图流

> (截取自https://www.bilibili.com/video/BV1og4y1q7M4?p=13)

![commands.png](https://github.com/Yusameki/LearningDocker/blob/master/Pictures/commands.png?raw=true)



---

### 具体常用指令

每一个指令的要求具体输入`--help`查看

选了几个看起来用得比较多的记录一下~（实时更新后缀详细）

```shell
attach		#进入指定容器当前的shell
commit		#将当前容器保存为新的镜像 -a="作者" -m="信息" id 名字：版本
cp		#从容器中拷贝指定文件or目录到主机
exec		#进入容器并新建一个shell
export		#导出容器内内容并归档为tar文件
images		#列出当前镜像
import		#对应export
info		#系统信息
inspect		#容器的详细信息
kill		#强杀指定容器
logs		#输出当前容器的日志信息
ps		#输出容器列表
pull		#从docker镜像源搞来指定镜像
push		#推送镜像到docker服务器
restart		#重启容器
rm		#移除容器
rmi		#移除镜像
run		#运行镜像 -it动态运行 -d后台运行 -p 主机端口：容器内端口 -v 主机目录：容器内目录
search		#在hub中搜索镜像
top		#查看 容器中 运行中的进程信息
```



### 挂载相关

```shell
#确定匿名挂载或者具名挂载，和指定路径挂载
-v 容器内路径	#匿名挂载
-v 卷名：容器内路径	#具名挂载
-v /宿主机路径：容器内路径	#指定路径挂载

#通过 -v 容器内路径：ro/rw 改变读写权限
ro readonly	#只读
rw readwrite	#可读可写
```



## DockerFile

![dockerfile.png](https://github.com/Yusameki/LearningDocker/blob/master/Pictures/dockerfile.png?raw=true)

### 基础知识

1.每个指令都要大写

2.从上到下依次执行

3.#表示注释

4.每个指令都会创建一个新的镜像层并提交

![dockerfile-structure.png](https://github.com/Yusameki/LearningDocker/blob/master/Pictures/dockerfile-structure.png?raw=true)















