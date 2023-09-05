# Reddit Clone App

This is a Reddit clone application designed to run on a Kubernetes cluster. It allows you to create and manage posts similar to the popular social platform Reddit. Below are the steps to set up and deploy the app on your own Kubernetes cluster.

## Prerequisites

Before you begin, ensure you have the following tools and resources installed and set up on your local system:

- Docker
- kubeadm
- kubectl
- git

## Setting Up Your Kubernetes Cluster

1. Create two AWS EC2 instances:
   - Both instances should run Ubuntu.
   - Use `t2.medium` instance type (or adjust as needed).
   - One instance will serve as the master node, and the other as a worker node.

2. Install `kubeadm` on both the master and worker nodes. You can follow the official Kubernetes documentation for installation instructions.

3. On the master node, initialize the cluster and generate a token:
   ```bash
   kubeadm init
   ```
4. Copy the generated join token from the output.
   
5. On the worker node, join the cluster using the token you copied:
   ```bash
   kubeadm join <master-node-ip>:<master-node-port> --token <token> --discovery-token-ca-cert-hash <hash>
   ```
## Building and Deploying the Reddit Clone App

1. clone this repository to your local machine to build the Docker image:
   ```bash
   git clone https://github.com/ytushar24/reddit-clone-app.git
   ```
2. Build the Docker image for the Reddit clone app:
   ```bash
   cd reddit-clone
   docker build -t reddit-clone-app:latest .
   ```
3. Deploy the app on the Kubernetes worker node using the provided deployment.yml file:
   ```bash
   cd k8s
   kubectl apply -f deployment.yml
   ```
4. Deploy the service for the app on the Kubernetes worker node using the provided service.yml file:
   ```bash
   kubectl apply -f service.yml
   ```
5. Deploy the ingress resource on the Kubernetes worker node using the provided ingress.yml file:
   ```bash
   kubectl apply -f ingress.yml
   ```
6. Deploy the Horizontal Pod Autoscaler on the Kubernetes worker node using the provided HorizontalPodAutoscaler.yml file:
   ```bash
   kubectl apply -f HorizontalPodAutoscaler.yml
   ```
The Horizontal Pod Autoscaler ensures that new pods are created when the CPU utilization of the existing pods reaches 80%.

Now, your Reddit clone app should be up and running on your Kubernetes cluster. You can access it through the provided Ingress URL or the nodeport specified in service.yml.

Don't forget to expose the ports in the inbound rule setting of the chosen cloud provider.

```bash
curl -L domain.com/test
```

Enjoy using your Reddit clone app!



   

