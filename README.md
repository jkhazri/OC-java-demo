## docker-Java-kubernetes-project
Deploying Java Applications with Docker and Kubernetes
1. you need to have maven installed on your pc. All those command may need a sudo or a root privilege!
```
git clone https://github.com/jkhazri/OC-java-demo.git
```
```
2. time to deploy the application on the cluster kubernetes.
```
cd kubernetes /
kubectl apply -f shopfront-service.yaml
kubectl apply -f productcatalogue-service.yaml
```
3. now the application should be running us expect . to check please run those commands :
```
kubectl get pods
kubectl get svc
```
kubectl get svc command gives you the services of the java application 
```
NAME               TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
kubernetes         ClusterIP   10.96.0.1       <none>        443/TCP          17d
productcatalogue   NodePort    10.108.218.49   <none>        8020:32512/TCP   64m
shopfront          NodePort    10.96.31.170    <none>        8010:30648/TCP   64m
stockmanager       NodePort    10.96.86.248    <none>        8030:31601/TCP   3m4s
```
The port 30648 is used to expose the shopfront service all you need  to do is check this on your browser, for Example http://"IPaddress":30648 to check the service named shopfront.
The port number depends on the given port range. 
