# kvm 安装 #
> #yum安装  
yum install libvirt* virt-* qemu-kvm* -y  
#自启动  
systemctl start libvirtd
systemctl enable libvirtd