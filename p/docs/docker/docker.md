# docker使用指南

## 安装 docker 和 docker-compose

-   [docker](https://docs.docker.com/engine/installation/)
-   [docker-compose](https://docs.docker.com/compose/install/)

把当前用户加到 docker 用户组里面：

```
sudo gpasswd -a ${USER} docker
```

docker 加速器

-   在/etc/docker/daemon.json

```
"registry-mirrors": ["https://6evg8u3r.mirror.aliyuncs.com"]
```

重启 Docker Daemon:

```
sudo systemctl daemon-reload
sudo systemctl restart docker
```

## 编写规则

-   使用#来注释
-   FROM 指令告诉 Docker 使用哪个镜像作为基础
-   RUN 开头的指令会在创建中运行，比如安装一个软件包
-   COPY 指令将文件复制进镜像中
-   WORKDIR 指定工作目录
-   CMD/ENTRYPOINT 容器启动执行命令

(RUN 和 CMD/ENTRYPOINT 都是执行命令，区别在于 RUN 是在镜像构建过程中执行的，而 CMD/ENTRYPOINT 是在镜像生成实例的时候执行的。)

```Dockerfile

```

获取镜像的命令：docker pull [选项][docker registry 地址]<仓库名>:<标签>

-ti 是两个命令：-i 是以交互模式运行容器，-t 是为容器重新分配一个伪输入终端，这里我们打算进入 bash 执行一些命令并查看返回结果，因此我们需要交互式终端。

—rm 这个参数是指容器退出后随之将其删除。

--volume 是增加一个数据卷，具体什么是数据卷，将在后面的文章详细讲，这里只需要理解–volume=”\$(pwd)”:/bot 的意思就是把当前目录映射到容器里的 bot

## docke 命令

```
#1. 查看正在运行的容器

docker ps

#查看所有容器
docker ps -a

#2. 删除容器
 #可以一次删除多个，再rm 后面使用空格隔开依次写上要删除的容器

docker rm container_id
docker rm container_name

#3. 运行容器

docker run -d -P  dedecms/php php 123.php
docker run -d -p  8008:80 docker.io/nginx

# 指定IP+PORT
docker run -d -p  127.0.0.1:8008:80 docker.io/nginx

#指定协议 ,默认tcp
 docker run -d -p  127.0.0.1:8008:80/udp docker.io/nginx

给容器命名
docker rrun -d -P --name dedecms  docker.io/nginx

#测试 curl http://localhost:8008/
将容器内部端口80映射到本机端口8008上

-d:让容器在后台运行。
-P:将容器内部使用的网络端口映射到我们使用的主机上。

#4. 查看容器端口映射情况

docker port container_id
docker port container_name
或者
docker ps

#5. 查看容器输出

docker logs -f container_id

#6. 查看容器内进程

docker top container_name

#7. 查看容器详细的配置

docker inspect container_name

#8. 停止容器

docker stop container_id
docker stop container_name

#9. 重启容器

docker start container_id
docker start container_name
docker restart container_id
docker restart container_name

#10. 查看最后一次创建的容器

docker ps -l

#11. 查看运行日志,用来排查容器运行出错效果不错

docker logs container_id
docker logs container_name
```

## docker-compose 命令

```
构建运行项目
docker-compose up -d
docker-compose

-d: 后台启动模式
查看运行运行的项目
docker-compose ps
一次性的运行项目
docker-compose run contianername1 containername2
启动-停止-移除
# 启动
docker-compose start
docker-compose restart

# 停止
docker-compose stop

# 暂停一个容器
docker-compose pause container_id

# 移除
docker-compose down
#加入参数移除数据卷 --valumes
docker-compose down --valumes

docker-compose rm container_id
注意：docker-compose rm不会删除应用的网络和数据卷，docker-compose down删除的更彻底

查看容器输出
docker-compose logs
```

## [持续集成使用指南](201812003.md)
