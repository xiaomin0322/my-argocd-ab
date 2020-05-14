# argocd-canary
default-ab-ng.yaml  a/b测试  
default-canary-ng.yaml 金丝雀   


#执行步骤   
1.安装k8s Nginx Ingress Controller   #参考：https://juejin.im/post/5dca749af265da4d556d0016      
2.kubectl apply -f default-ab-ng.yaml   
3.kubectl argo rollouts get rollout rollout-canary  #查看是否启动完成  
4.kubectl patch rollout rollout-canary --type merge -p '{"spec": {"template": { "spec": { "containers": [{"name": "nginx","image": "nginx:1.15.5"}]}}}}' #执行绿版本  
5.kubectl argo rollouts get rollout rollout-canary  #查看是否启动完成   
6.测试效果： 
![image](https://github.com/xiaomin0322/my-argocd-ab/blob/master/old.png) 
![image](https://github.com/xiaomin0322/my-argocd-ab/blob/master/new.png)

7.参考资料： 
https://argoproj.github.io/argo-rollouts/features/traffic-management/nginx/ 
