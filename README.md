# eng99_pre_assignment_project

![diagram](/images/pre-assignment-k8-cluster-diagram.png)

## Project summary

Creating multi-node k8 cluster on AWS to run a web app that is fully functional for customers to use. This app has to be highly available and highly scalable so that if we have high traffic we can cater for it and also available in different availability zone in case anything happens to one of the availability zones we have a load balancer that diverts traffic to the healthy instances.

we need to use an s3 bucket for a disaster recovery plan.
we need to monitor it with cloud watch and grfana.

node app with MongoDB
create 3 instances for the web app and
3 instances for MongoDB

## Multi-node kubernetes cluster on AWS

## Lunching ec2 instance

## Installing Docker and K8 on it

## Contarising the application

## Monitoring with cloud watch and grafana

## Creating a K8 Cluster on Linux

#### We will use `Minikube` to create a k8 cluster

Minikube single node Kubernetes cluster setup on AWS EC2 18.04LTS Ubuntu

#### Installation of Minikube on EC2 Ubuntu 18.04 LTS

**pre-requisits**

- AMI Ubuntu Server 18.04 LTS (HVM)
- SSD Volume Type- Instance Type t2.medium- Storage 8 GB (gp2)
- Security Group Name: k8- Security Group 
- SSH, `from your ip/0.0.0.0/0`
- Key Pair Create your own keypair.

#### SSH into EC2 instance
- Run `sudo apt-get update -y`
- Run `sudo apt-get upgrade -y`

#### Install kubectl
[check this link for more instructions if this link below doest work for you](https://minikube.sigs.k8s.io/docs/start/)

    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

- Make it executable
  
      chmod +x ./kubectl
- Move it to default location

      sudo mv ./kubectl /usr/local/bin/kubectl

#### Moving onto installing Docker
    sudo apt-get update && sudo apt-get install docker.io -y

- Check docker installation `docker version`

#### Let's install Minikube on AWS EC2 Linux Machine - Ubuntu 18.04LTS
- We will get this done in one go

      curl -Lo minikube <https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64> && chmod +x minikube && sudo mv minikube /usr/local/bin/

- check version `minikube version`

      `minikube version: v1.23.2`
#### Launching minikube

- Change to root user `sudo -i`
- To start Minikube; We are going to use the –vm-driver=none switch.
- The rationale is we don’t want to install a Hypervisor like VirtualBox on the AWS instance, we just want minikube to run using the host- Start command 

      minikube start --vm-driver=none

- Status check `minikube status`
- Expected output

      minikubetype: 
      Control Planehost: Running
      kubelet: Running
      apiserver: Running
      kubeconfig: Configured
### minikube trouble shooting on EC2 ubuntu 18.04LTS
- New versions may require conntract package explicitly installed
- `sudo apt-get install -y conntrack`

- restart minkube with driver=none
 `minikube start --vm-driver=none`
 
 > Note: minikube meant to work in admin mode- `sudo -i` then `minikube start`- To fast track we have an ami of k8 cluster `ami-08a121049feee27da`- All done#### K8 official doc
 <https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-strong-getting-started-strong> 
 - We need run the yml files from admin mode


# other K8 commands for local host
## install hyperhit and minikube
- For Mac users

      brew update
      brew install hyperkit
      brew install minikube
      kubectl
      minikube

## create minikube cluster
    minikube start --vm-driver=hyperkit
    kubectl get nodes
    minikube status
    kubectl version

## delete cluster and restart in debug mode
    minikube delete
    minikube start --vm-driver=hyperkit --v=7 --alsologtostderr
    minikube status

## kubectl commands
    kubectl get nodes
    kubectl get pod
    kubectl get services
    kubectl create deployment nginx-depl --image=nginx
    kubectl get deployment
    kubectl get replicaset
    kubectl edit deployment nginx-depl

## debugging
    kubectl logs {pod-name}
    kubectl exec -it {pod-name} -- bin/bash

## create mongo deployment
    kubectl create deployment mongo-depl --image=mongo
    kubectl logs mongo-depl-{pod-name}
    kubectl describe pod mongo-depl-{pod-name}

## delete deplyoment

    kubectl delete deployment mongo-depl
    kubectl delete deployment nginx-depl

## create or edit config file

    vim nginx-deployment.yaml
    kubectl apply -f nginx-deployment.yaml
    kubectl get pod
    kubectl get deployment

## delete with config
    kubectl delete -f nginx-deployment.yaml
## Metrics
kubectl top The kubectl top command returns current CPU and memory usage for a cluster’s pods or nodes, or for a particular pod or node if specified.

#### Some other useful links
- [troubleshooting-deployments](https://learnk8s.io/troubleshooting-deployments)
- [deploying-nodejs-kubernetes](https://learnk8s.io/deploying-nodejs-kubernetes)
- 