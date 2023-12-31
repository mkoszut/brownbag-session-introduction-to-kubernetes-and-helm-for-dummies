# Kubernetes via manifests

## Create a cluster with additional configuration

In the command below is an additional config because we need it to expose service to the host machine

```
kind create cluster --config kind-config.yaml
```

## Create deployment

```
kubectl apply -f - <<EOF
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: kubernetes-bootcamp
  name: kubernetes-bootcamp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: kubernetes-bootcamp
  template:
    metadata:
      labels:
        app: kubernetes-bootcamp
    spec:
      containers:
      - image: gcr.io/google-samples/kubernetes-bootcamp:v1
        name: kubernetes-bootcamp
EOF
```

or

```
kubectl apply -f ./manifests/kubernetes-bootcamp.deployment.yaml
```

## Create a port-forward

```
kubectl port-forward pod/... 8080 8080
```

## Scale up

We can edit the file `./manifests/kubernetes-bootcamp.deployment.yaml` and apply changes.

## Create a service

```
kubectl apply -f - <<EOF
apiVersion: v1
kind: Service
metadata:
  labels:
    app: kubernetes-bootcamp
  name: kubernetes-bootcamp
spec:
  ports:
  - name: http
    nodePort: 30001
    port: 8080
    protocol: TCP
    targetPort: 8080
  selector:
    app: kubernetes-bootcamp
  type: NodePort
EOF
```

or

```
kubectl apply -f ./manifests/kubernetes-bootcamp.service.yaml
```

## Delete the cluster

```
kind delete cluster
```
