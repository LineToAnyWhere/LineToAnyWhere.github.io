# k8s 常用命令 #
## k8s pod ##  
> #创建pod  
kubectl create -f xxx.yaml  
#查询pod  
kubectl get pod PODNAME  
kubectl describe pod PODNAME  
#删除pod  
kubectl delete pod PODNAME  
#更新pod  
kubectl replace /path/to/podyaml.yaml

## k8s service ##
> #创建service  
kubectl create service clusterip imgserver-pord --tcp=30000:80  
kubectl create service clusterip imgserver-develop --tcp=20000:80  
kubectl create service clusterip imgserver-testing --tcp=25000:80  
#访问service
访问service时访问service的域名  
servicename.default.svc.cluster.local.

## k8s 扩缩容 ##
> #扩缩容  
kubectl scale --replicas=3 deployment myapp
