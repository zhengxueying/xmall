###### Helm 安装

1. helm客户端安装

   1. 下载想要的版本<https://github.com/helm/helm/releases>
   2. 解压并将解压后的二进制helm文件移动到/usr/local/bin/helm

2. 安装Tiller

   1. helm init即可安装

   2. 将tiller添加到kube-system的命名空间

      ```
      kubectl create serviceaccount --namespace kube-system tiller
      
      kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
      
      kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}'      
      
      helm init --service-account tiller --upgrade
      ```




###### 安装PV、PVC、StorageClass

​	参考0_sc-pv-pvc/README.md



###### 安装各组件

​	除activeMQ外其他组件均使用helm安装

​	安装前需要先创建pv和pvc，当前zookeeper没有使用pvc

 	1. mysql安装：helm install --name mysql  stable/mysql --set persistence.existingClaim=mysql-pvc -f values.yaml
 	2. zookeeper安装：helm install --name zookeeper stable/zookeeper -f values.yaml
 	3. elasticsearch安装： helm install --name elasticsearch stable/elasticsearch -f values.yaml
 	4. redis安装： helm install --name redis stable/redis -f values.yaml
 	5. activeMQ安装：kubectl apply -f amq.yaml

​	