使用docker运行nginx服务器
    运行
    docker run -d -p 80:80 --name webserver nginx
    停止并删除
    docker stop webserver
    docker rm webserver

查看docker的当前镜像
    docker images

查看docker的容器和镜像的信息
    docker info

创建并启动一个容器
    docker run 
    例子: sudo docker run -i -t ubuntu /bin/bash
    -i 参数保证容器中的STDIN是开启的
    -t 告诉Docker为要创建的容器分配一个伪tty终端
    ubuntu 告诉docker基于什么镜像来创建容器,示例中是Ubuntu镜像，是一个常备镜像(基础镜像)

查看所有的容器
    docker ps   查看当前正在运行的容器
    docker ps -a 查看所有容器
    docker ps -l 查看最后一次运行的容器

启动一个容器
    docker start 容器名

打开一个交互式shell，重新附着到容器的会话上
    docker attache 容器名