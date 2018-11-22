# docker

##编写规则

* 使用#来注释
* FROM 指令告诉 Docker 使用哪个镜像作为基础
* RUN 开头的指令会在创建中运行，比如安装一个软件包
* COPY 指令将文件复制进镜像中
* WORKDIR 指定工作目录
* CMD/ENTRYPOINT 容器启动执行命令

(RUN 和 CMD/ENTRYPOINT 都是执行命令，区别在于 RUN 是在镜像构建过程中执行的，而 CMD/ENTRYPOINT 是在镜像生成实例的时候执行的。)

``` Dockerfile
```

获取镜像的命令：docker pull [选项] [Docker Registry 地址]<仓库名>:<标签>  

-ti是两个命令：-i是以交互模式运行容器，-t是为容器重新分配一个伪输入终端，这里我们打算进入bash执行一些命令并查看返回结果，因此我们需要交互式终端。

—rm这个参数是指容器退出后随之将其删除。

--volume是增加一个数据卷，具体什么是数据卷，将在后面的文章详细讲，这里只需要理解–volume=”$(pwd)”:/bot的意思就是把当前目录映射到容器里的bot