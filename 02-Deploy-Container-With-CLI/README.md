# Deploy Containers Using CLI (kubectl)

## About this Section

In this section we are going to deploy a `pod` using kubectl
I'm using nginx image from docker hub as web server.
after this section you are able to `expose services` and `create pods` from docker images

### Create a `Pod` with nginx image from docker hub, With the second cmd check the list of pods

```shell
kubectl run http --image=nginx
kubectl get pods
```

#### Get more useful information about the pod named by `http`

```shell
kubectl describe pod http
```

### Expose the pod by creating a `Service` with `NodePort` type which will assign a free random TCP port from your node1 server, With the second cmd check out is the service created or not? and find out about the random port

```shell
kubectl expose pod http --type NodePort --port=8000 --target-port=80
kubectl get service http
```

#### Check the status of service and use cURL to be sure you have access to index.html of nginx

```shell
curl http://kube-node1:<Port From Sevice>
```

### You can run this cmd on the node1 server ro check out the docker container

```shell
docker ps | grep nginx
```
