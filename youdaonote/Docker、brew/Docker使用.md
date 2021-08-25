参考文档：https://yeasy.gitbooks.io/docker_practice/image/commit.html



一、Docker 包括三个基本概念

- 镜像（Image）

- 容器（Container）

- 仓库（Repository）

二、命令

      1.  获取镜像   docker  pull

   docker pull [选项] [Docker Registry 地址[:端口号]/]仓库名[:标签]

- Docker 镜像仓库地址：地址的格式一般是 <域名/IP>[:端口号]。默认地址是 Docker Hub。

- 仓库名：如之前所说，这里的仓库名是两段式名称，即 <用户名>/<软件名>。对于 Docker Hub，如果不给出用户名，则默认为 library，也就是官方镜像。

     2.  运行容器（定制镜像）    docker  run

- $ 	docker run --name webserver -d -p 80:80 nginx

定制一个web服务器，这条命令会用 nginx 镜像启动一个容器，命名为 webserver，并且映射到 80 端口，这样就可以用浏览器去访问http://localhost 这个 nginx 服务器。

- 进入容器，修改内容

        $ docker exec -it webserver bash

         root@3729b97e8226:/# echo '<h1>Hello, Docker!</h1>' > /usr/share/nginx/html/index.html
root@3729b97e8226:/# exit
exit

- 查看具体的改动

      $ docker diff webserver

- 生成新的镜像

      docker commit [选项] <容器ID或容器名> [<仓库名>[:<标签>]]

$ docker commit \
    --author "Tao Wang <twang2218@gmail.com>" \
    --message "修改了默认网页" \
    webserver \
    nginx:v2

- 查看新生成的镜像

      $ docker image ls

- 查看镜像内的历史记录 

    $ docker history nginx:v2

- 运行新生成的镜像，此时可以访问http://localhost:81 看到结果

    docker run --name web2 -d -p 81:80 nginx:v2

     3.  列出已下载对镜像   docker  image  ls

     4.  删除镜像  docker  image  rm

      $ docker image rm [选项] <镜像1> [<镜像2> ...]

     5.  定制镜像



docker inspect 容器名 查看容器的配置信息，包含容器名、环境变量、运行命令、主机配置、网络配置和数据卷配置



>>root@rbtnode1: ~# docker inspect --format='{{.NetworkSettings.IPAddress}}' nginx1
>>172.16.57.5

>>root@rbtnode1: ~# docker inspect --format '{{.Name}} {{.State.Running}}' nginx1
>>/nginx1 true



 

Docker 常用命令



docker restart 容器ID或容器名   停止并重启

docker stop 容器ID或容器名 优雅的关闭，-t 增加超时时间，如果超时未能关闭则用kill强制关闭

docker kill 容器ID或容器名 强制关闭

docker ps—列出容器的各种属性

docker rm—移除容器

docker rmi—删除镜像

docker images 查看镜像信息

docker ps 查看正在运行的所有容器，-a 显示已暂停或停止的容器



镜像和容器

简单点说，镜像就类似操作系统光盘介质，容器相当于通过光盘安装后的系统。通过光盘(镜像)，我们能在不同机器上部署系统(容器)，系统内的操作只会保留在当前的系统(容器)中，如果要升级系统，需要使用到光盘，但是可能会导致操作系统的数据丢失



