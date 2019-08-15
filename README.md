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


