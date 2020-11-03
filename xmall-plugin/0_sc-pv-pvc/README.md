 1. 先执行kubectl create -f storageClass.yaml
 2. 然后执行kubectl create -f pvs.yaml
 3. 再执行kubectl create -f pvcs.yaml

mysql的pv和pvc可以独立创建
