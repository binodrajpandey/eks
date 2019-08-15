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
`kubectl get nodes`
3. List out pods
`kubectl get pods`
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

