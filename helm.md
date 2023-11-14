# Helm

## Create cluster with additional configuration

We need it to expose service to host machine.

```
kind create cluster --config kind-config.yaml
```

## Create chart

```
helm create brownbag-kubernetes-bootcamp
```

## Update chart configuration

In the file `values.yaml` set a new values

```
image:
  repository: gcr.io/google-samples/kubernetes-bootcamp
  tag: v1

service:
  type: NodePort
  port: 8080
```

## Install chart on the cluster

In the chart directory

```
helm install brownbag-kubernetes-bootcamp .
```

## Expose the application

We need to add NodePort in the service, in the file `templates/service.yaml`

```
{{- if eq .Values.service.type "NodePort" }}
nodePort: 30001
{{- end }}
```

apply changes

```
helm upgrade brownbag-kubernetes-bootcamp .
```

## Scale up

We can just edit the file `values.yaml` in the chart directory

```
replicaCount: 2
```

and apply changes

```
helm upgrade brownbag-kubernetes-bootcamp .
```

### Delete cluster

```
kind delete cluster
```
