# Kubernetes via Command Line

## Create cluster with additional configuration

We need it to expose service to host machine.

```
kind create cluster --config kind-config.yaml
```

## Create deployment

```
kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1
```

## Scale up

```
kubectl scale --replicas=2 deployment/kubernetes-bootcamp
```

## Create service

```
kubectl create service nodeport kubernetes-bootcamp  --node-port 30001 --tcp=8080:8080
```

## Delete cluster

```
kind delete cluster
```
