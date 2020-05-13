# Dokcer 常用命令 #
## docker 信息 ##  
>docker info  
docker images 
docker inspect 容器ID

## docker 镜像操作 ##
> docker search xx  
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
> docker container create xximg  
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
> #网络配置查看  
docker container inspect 容器id
#跨主机通信macvlan
docker network create --driver macvlan --subnet 172.16.1.0/24 --gateway 172.16.1.1 -o parent=eth1 macvlan_1  
#设置eth1的网卡为混杂模式  
ip link set eth1 promisc on  
#创建使用macvlan网络的容器  
docker run -it --network macvlan_1 --ip=172.16.1.3 busybox:latest /bin/sh  
#跨主机通信之overlay

## 容器数据卷 ##
> #宿主机与容器间传输  
docker cp 容器ID:目录 目的  
#只读权限挂载  
docker run -it -v /home/:/home:ro centos /bin/bash  
#挂载其他容器数据卷  
docker run -it --volumes-from dbdata centos /bin/bash  
#备份数据卷  
在卷中安装tar  
yum install tar  
docker run --volumes-from dbdata -v $(pwd):/home/backup --name worker centos tar zcf /home/backup/backup.tar.gz /home/demo  
#还原数据卷  
docker run -it -v /dbdata2 --name backup centos /bin/bash  
docker run -it --privileged=true --volumes-from backup -v /home/demo/demo2:/ceshi centos tar xf /ceshi/backup.tar.gz -C /dbdata2

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
> #生成自定义镜像  
docker build -t mynetCDF4:v1.0  
#运行上述镜像  
docker run -p 80:8080 mynetCDF4  
#创建一个nginx镜像  
docker commit 容器id nginx:v1.0  

## docker私有仓库 ##
> #运行私有仓库  
docker run -d -p 5000:5000 --restart=always --name registry -v /opt/myregistry:/var/lib/registry registry  
#镜像打签  
docker image tag mynginx:v1.0 192.168.50.50:35000/mynginx:v1.0  
#上传镜像  
docker image push 192.168.50.50:35000/mynginx:v1.0  
#修改信任  
"insecure-registries":["192.168.50.50:35000"]  
#删除镜像  
docker exec -it registry /bin/sh  
rm -rf /var/lib/registry/docker/registry/v2/repositories/nginx  
registry garbage-collect /etc/docker/registry/config.yml  
或
rm -rf /opt/project/docker-registry/docker/registry/v2/repositories/nginx  
docker exec -it gracious_hellman registry garbage-collect /etc/docker/registry/config.yml  
#查看镜像列表  
http://192.168.50.50:35000/v2/_catalog  
#为私有仓库添加basic认证  
yum install httpd-tools -y  
mkdir -p /opt/project/docker-auth/
htpasswd -Bbn jiutian jiutian@123 >> /opt/project/docker-auth/htpasswd  
docker run -d -p 35000:5000 -v /opt/project/docker-auth/:/auth/ -v /opt/project/docker-registry/:/var/lib/registry/ -e "REGISTRY_AUTH=htpasswd" -e "REGISTRY_AUTH_HTPASSWD_REALM=Registry Realm" -e REGISTRY_AUTH_HTPASSWD_PATH=/auth/htpasswd registry  
docker login 192.168.50.50:35000  
登录成功后会在/root/.docker/config.json写入配置信息
