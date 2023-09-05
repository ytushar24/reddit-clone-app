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

