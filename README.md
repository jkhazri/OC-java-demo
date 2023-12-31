# docker-Java-kubernetes-project
## what you need to check before preparing your deployment

**Important**: 

Please make sure you have enough resources in your Vcluseter before you start your deployment.

**Best practice :** 
You may need to limit your application ressources by adding what we called ResourceQuota kubernetes kind in your deployment Yaml file.

In this example, I've added at the end of  the stockmanager-service.yaml file a ResourceQuota named stockmanager-resource-quota with limits for CPU, memory, and the number of pods  . 
Adjust these values based on your application's requirements and the available resources in your Kubernetes cluster.

If you need to learn more about the ResourceQuota , please refer to this documentation : https://kubernetes.io/docs/concepts/policy/resource-quotas/

```bash
---
apiVersion: v1
kind: ResourceQuota
metadata:
  name: stockmanager-resource-quota
spec:
  hard:
    cpu: "200m"      # 0.2 CPU cores
    memory: "256Mi"  # 256 Megabytes of memory
    pods: "1"        # 1 pod

```
Deploying Java Applications with Docker and Kubernetes
1. you need to have a kubernetes cluster installed on your pc.then clone the project and move under OC-java-demo folder.
```
git clone https://github.com/jkhazri/OC-java-demo.git
cd OC-java-demo
```

2. time to deploy the application on the cluster kubernetes.
   
Before that check the nodePort number it should be in the given port range of the vcluster.
You may need to change nodePort number inside the 3 yaml files under OC-java-demo/kubernetes/ folder shopfront-service.yaml / productcatalogue-service.yaml / stockmanager-service.yaml.

For example in the productcatalogue-service.yaml we have nodePort: 20100 so you may change this number. (choose diffrent port number in every yaml file)

```
apiVersion: v1
kind: Service
metadata:
  name: productcatalogue
  labels:
    app: productcatalogue
spec:
  type: NodePort
  selector:
    app: productcatalogue
  ports:
  - protocol: TCP
    port: 8020
    nodePort: 20100 # choose a port in the nodeport given range
    name: http
```

```
cd kubernetes
kubectl apply -f shopfront-service.yaml
kubectl apply -f productcatalogue-service.yaml
kubectl apply -f stockmanager-service.yaml

```
3. now the application should be running us expect . to check please run those commands :
```
kubectl get pods
kubectl get svc
```
kubectl get svc command gives you the services of the java application. Here an example this command output : 

```
NAME               TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
kubernetes         ClusterIP   10.96.0.1       <none>        443/TCP          17d
productcatalogue   NodePort    10.108.218.49   <none>        8020:32512/TCP   64m
shopfront          NodePort    10.96.31.170    <none>        8010:30648/TCP   64m
stockmanager       NodePort    10.96.86.248    <none>        8030:31601/TCP   3m4s
```

The port 30648 is used to expose the shopfront service all you need  to do is check this on your browser, for Example http://"IPaddress":30648 to check the service named shopfront.
The port number depends on the given port range.
