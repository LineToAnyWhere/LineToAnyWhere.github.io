# Dokcer 常用命令 #
## docker 信息 ##  
docker info  
docker images 

## docker 镜像操作 ##
docker search xx  
docker pull xx  
docker image rm xx  
docker rmi xx  
#导出镜像  
docker image save xx > xx.tar.gz  
#导入镜像  
docker image load -i xx.tar.gz  
#镜像标签  
docker image tag 源：tag 目标：tag  
#查看镜像构建过程  
docker image history xx  
#查询镜像详情  
docker image inspect xx

## docker 容器操作 ##  
docker container create xximg  
docker rm xx  
docker start xx  
docker stop xx  
#创建并进入一个容器  
docker run -it docker.io/nginx /bin/bash  
docker run -p 80:80 --name ngx_demo -d nginx  
#进入容器  
docker exec -it xx /bin/bash  
#容器自启动  
docker run --restart=always 

## docker 网络管理 ## 
#网络配置查看  
docker container inspect 容器id
#跨主机通信macvlan
docker network create --driver macvlan --subnet 172.16.1.0/24 --gateway 172.16.1.1 -o parent=eth1 macvlan_1  
#设置eth1的网卡为混杂模式  
ip link set eth1 promisc on  
#创建使用macvlan网络的容器  
docker run -it --network macvlan_1 --ip=172.16.1.3 busybox:latest /bin/sh  

#跨主机通信之overlay

## 容器数据卷 ##
#宿主机与容器间传输  
docker cp 容器ID:目录 目的

## 构建dockerfile ##
```
FROM docker.io/centos:7.8.2003
MAINTAINER L.T.Any
RUN yum update -y && yum install netCDF4
CMD ["/bin/bash","~/init.sh"]
ENTRYPOINT ls -l
USER root
EXPOSE 8080
ENV JAVA_HOME /opt/path/java/java_1.8/
ENV PATH $PATH:$JAVA_HOME/bin
ADD ./mynetCDF4.tar.gz /opt/project/mynetCDF4/
VOLUME ["/jtdata/"]
WORKDIR /opt/project/mynetCDF4
RUN tar xf mynetCDF4.tar.gz
ONBUILD RUN rm -rf /opt/project/mynetCDF4
```
#运行上述镜像
docker run -p 80:8080 mynetCDF4
