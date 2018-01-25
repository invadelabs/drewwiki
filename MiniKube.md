---
title: MiniKube
layout: default
---

Notes [1](https://kubernetes.io/docs/getting-started-guides/minikube/)
[2](https://kubernetes.io/docs/concepts/containers/images/#using-a-private-registry)
[3](https://kubernetes.io/docs/getting-started-guides/ubuntu/local/)

Ubuntu Minikube VirtualBox

Install kubectl
===============

``` bash
sudo snap install juju --classic
sudo snap install kubectl --classic
```

Install and place minikube
==========================

Drop into /usr/local/bin/minikube

``` bash
curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.24.1/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
```

Start Minikube with VirtualBox
==============================

``` bash
minikube start --vm-driver=virtualbox
```

Setup environment
=================

``` bash
eval $(minikube docker-env)
docker ps
```

Add bash completion for minikube and kubectl
============================================

``` bash
kubectl completion bash >> ~/.bash_completion
minikube completion bash >> ~/.bash_completion
source ~/.bash_profile
```

Start a sample container
========================

``` bash
drew@drew-8570w:~$ kubectl run hello-minikube --image=k8s.gcr.io/echoserver:1.4 --port 8080
deployment "hello-minikube" created
```

Expose an endpoint into the container
-------------------------------------

``` bash
drew@drew-8570w:~$ kubectl expose deployment hello-minikube --type=NodePort
service "hello-minikube" exposed
drew@drew-8570w:~$ kubectl get pod
NAME                              READY     STATUS    RESTARTS   AGE
hello-minikube-7844bdb9c6-ntm28   1/1       Running   0          30s

drew@drew-8570w:~$ curl $(minikube service hello-minikube --url)
 curl http://192.168.99.100:31919
```

Notes
=====

Start, drop, delete, checkout k8s dashboard, status, etc:

``` bash
minikube get-k8s-versions

minikube stop

minikube delete

minikube dashboard

minikube status
```
