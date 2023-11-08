## docker-Java-kubernetes-project
Deploying Java Applications with Docker and Kubernetes
1. you need to have maven installed on your pc. All those command may need a sudo or a root privilege!
```
apt install maven
git clone https://github.com/jkhazri/OC-java-demo.git
```
2. run this command to create a folder named targed that will be used by the appliucation.The command builds the project from source code:
```
cd shopfront/
mvn clean install

cd productcatalogue/
mvn clean install

cd stockmanager/
mvn clean install
```
3. time to deploy the application on the cluster kubernetes.
```
cd kubernetes /
kubectl apply -f shopfront-service.yaml
kubectl apply -f productcatalogue-service.yaml
```
4. now the application should be running us expect . to check please run those commands :
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
The port 30648 is used to expose the shopfront service all you need  to do is check this on your browser http://"IPaddress":30648
