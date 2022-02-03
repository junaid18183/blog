---
layout: post
title:  "Deploying Virtual  kubernetes Cluster"
description: "Deploying Virtual  kubernetes Cluster"
author: juned
categories: [ k8s ]
tags: [k8s]
image: assets/images/k8s.jpg
featured: true
hidden: true
---

# Deploying Virtual  kubernetes Cluster

### **Why Virtual Kubernetes Clusters?**

- **Cost Efficient**: much cheaper than "real" clusters (single pod and shared resources just like for namespaces)
- **Fast Provisioning**: can be created and cleaned up again in seconds (great for CI/CD or testing)
- **Cluster Scoped Resources**: more powerful than simple namespaces (virtual clusters allow users to use CRDs etc.)
- **Cluster Wide Permissions**: allow users to install apps which require cluster-wide permissions while being limited to actually just one namespace within the host cluster
- **Strict isolation**: complete separate Kubernetes control plane and access point for each vcluster while still being able to share certain services of the underlying host cluster
- **Great for Testing**: allow you to test different Kubernetes versions inside a single host cluster which may have a different version than the virtual clusters

For Details refer the official [documentation](https://github.com/loft-sh/vcluster) 

# Deploying the virtual cluster

Make sure you have access to existing cluster , this can be any real cluster or even rancher desktop / KIND. 

I am using RKE cluster with 4 nodes , deployed on AWS. 

```json
$ kubectl get node
NAME                            STATUS   ROLES                       AGE    VERSION
ip-172-31-70-152.ec2.internal   Ready    <none>                      114d   v1.21.5+rke2r2
ip-172-31-75-72.ec2.internal    Ready    <none>                      114d   v1.21.5+rke2r2
ip-172-31-77-33.ec2.internal    Ready    control-plane,etcd,master   114d   v1.21.5+rke2r2
ip-172-31-78-97.ec2.internal    Ready    <none>                      114d   v1.21.5+rke2r2
```

Since I want to access my VCluster from my laptop, I want to use the routable IP to be kube-api server , so I will use my existing clusters control planes public IP and create `vcluster-values.yaml` that way I can access my vcluster api server using the same public IP but with different port

I kept the the cluster version same as my existing cluster, however thats not the hard requirement.

```json
storage:
  size: 5Gi
syncer:
  image: loftsh/vcluster:0.5.3
  extraArgs:
  - --tls-san=18.215.199.234
  - --out-kube-config-server=https://18.215.199.234
vcluster:
  image: rancher/k3s:v1.21.5-k3s2
service:
  type: NodePort
```

Create the namespace in your existing cluster to hold our new vcluster ( so that we can segregate the resources ) 

```json
$ kubectl create ns vcluster-kubeflow
```

And now Create the Vcluster 

```json
$ vcluster create vcluster-kubeflow -n vcluster-kubeflow -f vcluster-values.yaml

[info]   execute command: helm upgrade vcluster-kubeflow vcluster --repo https://charts.loft.sh --version 0.5.3 --kubeconfig /var/folders/jl/yjcdl565151f6zn_4mrndfsc0000gn/T/2906172558 --namespace vcluster-kubeflow --install --repository-config='' --values /var/folders/jl/yjcdl565151f6zn_4mrndfsc0000gn/T/3483749369 --values vcluster-values.yaml
[done] √ Successfully created virtual cluster vcluster-kubeflow in namespace vcluster-kubeflow. Use 'vcluster connect vcluster-kubeflow --namespace vcluster-kubeflow' to access the virtual cluster
```

Take a note of the Port of the NodePort for the service, e.g. below is 32218

```json
$ kubectl get svc -n vcluster-kubeflow vcluster-kubeflow
NAME                TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)         AGE
vcluster-kubeflow   NodePort   10.43.49.113   <none>        443:32218/TCP   22m
```

And retrieve the kubeconfig change the Port with the value got before 

```json
$ vcluster connect vcluster-kubeflow -n vcluster-kubeflow --server=https://18.215.199.234:32266
[done] √ Virtual cluster kube config written to: ./kubeconfig.yaml. You can access the cluster via `kubectl --kubeconfig ./kubeconfig.yaml get namespaces`
```

Now using this kubeconfig file I can use this cluster as any normal cluster 

```json
$ kubectl get no --kubeconfig=/tmp/kubeconfig.yaml
NAME                           STATUS   ROLES    AGE   VERSION
ip-172-31-77-33.ec2.internal   Ready    <none>   55m   v1.21.5+k3s2
```