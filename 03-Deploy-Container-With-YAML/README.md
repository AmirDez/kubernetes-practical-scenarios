# Deploy Containers Using YAML

## About this Section

In this section we are going to deploy a "deployment" using YAML files
i'm using nginx image from docker hub as web server.
after this section you are able to ``expose services`` by lable and scale them with ``replicas count``

### Create a **deployment.yaml from the sample directory

```shell
kubectl create -f deployment.yaml
```

#### Check the status of deployment

```shell
kubectl get deployment
kubectl describe deployment nginx-web-app
```

### Create a **service.yaml from the sample directory for exposing

```shell
kubectl create -f service.yaml
```

#### Check the status of service and use cURL to be sure you have access to index.html of nginx

```shell
kubectl get svc
kubectl describe svc nginx-web-app-svc
curl kube-node1:30080
```

### Time to scale up: Update the deployment.yaml file to increase the number of instances running. For example, the file should look like this

```shell
replicas: 4
```

#### Use **apply to update your changes to kube cluster

```shell
kubectl apply -f deployment.yaml
```

#### Check what you have done :)

```shell
kubectl get deployment
kubectl get pods
curl kube-node1:30080
```
