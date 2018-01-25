# Dokcer Install #
```
卸载旧版本
sudo yum remove docker docker-common docker-selinux docker-engine
先决条件（实际可能不需要）
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
添加yum源
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
安装docker-ce
sudo yum clean all
sudo yum install docker-ce
```
