### NOTE
Before you create your first cluster, make sure that you have installed all the required tools on the system you will be using to access the cluster:
- AWS Command Line Interface (AWS CLI)
- kubectl
- (Optional) eksctl
# Create EKS Cluster & Node Groups
## Step-01: Create EKS Cluster using eksctl
- It will take approximately 15 to 20 minutes to set up the Cluster Control Plane. This will create only master node. We will create worker nodes seperately. 
```
# Create Cluster
eksctl create cluster --name=eksdemo1 \
                      --region=ap-south-1a \
                      --zones=ap-south-1b \
                      --without-nodegroup 
# Get List of clusters
eksctl get cluster
```
## Step-02: Create & Associate IAM OIDC Provider for our EKS Cluster
- An IAM OIDC (OpenID Connect) Provider is an entity in AWS Identity and Access Management (IAM) that describes an external identity provider (IdP) service that supports the OpenID Connect (OIDC) standard
### Use Cases
- #### Mobile and Web Applications: 
Useful for applications that require access to AWS resources but don't want to manage their own user identities
- #### Third-Party Integrations:
Enables third-party applications to authenticate users via OIDC and access AWS resources.
### Create IAM OIDC Provider for our EKS Cluster
- To enable and use AWS IAM roles for Kubernetes service accounts on our EKS cluster, we must create & associate OIDC identity provider.
- To do so using eksctl we can use the below command.
```
# Template
eksctl utils associate-iam-oidc-provider \
    --region region-code \
    --cluster <cluter-name> \
    --approve

# Replace with region & cluster name
eksctl utils associate-iam-oidc-provider \
    --region ap-south-1 \
    --cluster eksdemo1 \
    --approve
```
## Step-03: Create EC2 Keypair
- Create a new EC2 Keypair with name as kube-demo
- This keypair we will use it when creating the EKS NodeGroup.
- This will help us to login to the EKS Worker Nodes using Terminal.

## Step-04: Create Node Group with additional Add-Ons in Public Subnets
- These add-ons will create the respective IAM policies for us automatically within our Node Group role.
```
# Create Public Node Group   
eksctl create nodegroup --cluster=eksdemo1 \
                       --region=ap-south-1 \
                       --name=eksdemo1-ng-public1 \
                       --node-type=t3.medium \
                       --nodes=2 \
                       --nodes-min=2 \
                       --nodes-max=4 \
                       --node-volume-size=20 \
                       --ssh-access \
                       --ssh-public-key=kube-demo \
                       --managed \
                       --asg-access \
                       --external-dns-access \
                       --full-ecr-access \
                       --appmesh-access \
                       --alb-ingress-access 
```
## Step-05: Verify Cluster & Nodes
### Verify NodeGroup subnets to confirm EC2 Instances are in Public Subnet
- Verify the node group subnet to ensure it created in public subnets
- Go to Services -> EKS -> eksdemo -> eksdemo1-ng-public1
- Click on Route Table Tab.
- We should see that internet route via Internet Gateway (0.0.0.0/0 -> igw-xxxxxxxx)
