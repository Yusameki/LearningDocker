# Docker学习初级小结 

###  前言

感谢[狂神说](https://space.bilibili.com/95256449)给了我一些新的知识，

~~最后半年的学校生活~~，加油!

Yusameki整理

---



### 一图流

> (截取自https://www.bilibili.com/video/BV1og4y1q7M4?p=13)

![commands.png](https://github.com/Yusameki/LearningDocker/blob/master/Pictures/commands.png?raw=true)



---

### 具体常用指令

每一个指令的要求具体输入`--help`查看

选了几个看起来用得比较多的记录一下~

```shell
attach		#进入指定容器当前的shell
commit		#将当前容器保存为新的镜像
cp			#从容器中拷贝指定文件or目录到主机
exec		#进入容器并新建一个shell
export		#导出容器内内容并归档为tar文件
images		#列出当前镜像
import		#对应export
info		#系统信息
inspect		#容器的详细信息
kill		#强杀指定容器
logs		#输出当前容器的日志信息
ps			#输出容器列表
pull		#从docker镜像源搞来指定镜像
push		#推送镜像到docker服务器
restart		#重启容器
rm			#移除容器
rmi			#移除镜像
run			#运行镜像
search		#在hub中搜索镜像
top			#查看 容器中 运行中的进程信息
```





















