


## CLI's used
`kubectl` – A command line tool for working with Kubernetes clusters.

`eksctl` – A command line tool for working with EKS clusters that automates many individual tasks. 

## Types of nodes in EKS

`Fargate – Linux`: Select this type of node if you want to run Linux applications on AWS Fargate. Fargate is a serverless compute engine that lets you deploy Kubernetes pods without managing Amazon EC2 instances.

`self-managed nodes – Linux` : Select this type of node if you want to run Amazon Linux applications on Amazon EC2 instances.

```bash
eksctl create cluster --name my-cluster --region region-code --fargate

kubectl get nodes -o wide # view nodes


```