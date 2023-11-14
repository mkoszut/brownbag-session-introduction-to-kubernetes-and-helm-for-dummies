# Kubernetes via Command Line

## Create a cluster with additional configuration

In the command below is an additional config because we need it to expose service to the host machine

```
kind create cluster --config kind-config.yaml
```

## Create a deployment

```
kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1
```

## Scale up

```
kubectl scale --replicas=2 deployment/kubernetes-bootcamp
```

## Create a service

```
kubectl create service nodeport kubernetes-bootcamp  --node-port 30001 --tcp=8080:8080
```

## Delete the cluster

```
kind delete cluster
```
