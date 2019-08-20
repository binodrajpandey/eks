# EKS
Why Do we need kubernetes?
Containers have following problems:
1. Containers could not communicate with each other.
2. Containers had to be deployed appropriately.
3. Containers had to be managed carefully
4. Auto Scaling is not possible.
5. Distributing traffic is challenging

So kubernetes is the containers management tools which automates container deployment, container scaling and container load balancing.

1. Provison an Amazon EKS cluster
https://docs.aws.amazon.com/eks/latest/userguide/getting-started-console.html
 a. Create roles for EKS
  Create VPC, subnets and security groups (CloudFormation)
  CloudFormation --> Create stack -->
  
2. Deploy Worker nodes (Cloud Formation)
3. Connect to EKS (Kubectl)
4. Run kubernetes apps on EKS cluster

Steps: 
1. Initialize Kubernetes master:

```kubeadm init --pod-network-cidr=192.168.0.0/16 --apiserver-advertise-address=192.168.56.101```
where 192.168.56.101 is the ip address of master.
2. List out nodes.
```
kubectl get nodes -n eai
kubectl get rs -n eai
kubectl get pods -n eai
kubectl get deployments -n eai 
kubectl get svc -n eai
```
`kubectl get deployments -n eai`

NAME                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE

gram-agent            2         2         2            2           19d
nginx-deployment      2         2         2            2           42d
usergram-client-app   1         1         1            1           19d

`kubectl get deployments -n eai|grep gram-agent`

gram-agent            2         2         2            2           19d
3. List out pods
`kubectl get pods`
List pods with node info.
`kubeclt get pods -o wide `
4. Create deployment
```
kubectl create deployment nginx --image=nginx
# kubectl create -f deployment.yaml
kubectl get deployments
kubectl describe deployment nginx
```
5. Create service
```
kubectl create service nodeport nginx --tcp=80:80
kubectl get svc
```
6. Delete deployment 
`kubectl delete deployment nginx`
`kubectl delete pod <podname>`
7. Update Pod
```
kubectl edit pod redis
kubectl describe pod redis
```
8. 
`kubectl taint nodes node-name key=value:taint:effect`


# Service Type
1. Node Port : It expose our app to the external world of the internet.
 a. Pods are ephemeral, We can not trust pod IP. When Pod gets destroyed it will be recreated with different IP.
 b. There is no connectivity between user and pod
 In order to address above two problem, We need NodePort to expose application to outside world. Once the service is deployed we can access the web application deployed in the pod can be accessed using node Ip and node port. Service of type node port can be with in single node or span over many nodes.
 
 There are three types of ports in the kubernetes.
 a. Node Port : Port on the node where pod is running. The range is from 30000-32767. 
 b. Port: Port on the service itself.
 c. Target Port: This is the port on actual pod where web app is running. Typically service port and target port is same.
 
 Downside of NodePort
- you can have only a service per port.
- port range between 30000-32767
- If node Ip is changed, you have to deal with that.

So, it is not recommended for production to directly expose your app. If you have a service that doesn't have to be always available or you are very cost sensitive, this could be useful. eg. demo app.  
2. ClusterIP
3. Node balancer
