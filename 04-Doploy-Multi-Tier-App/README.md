# Doploy Multi-tier App

## About this Section

In this section we are going to deploy mutli-tier app with **mysql**  as the backend db and **phpMyAdmin** as the web front UI.

after this section you are able to ``ingress services`` by lable and scale them with ``replicas count`` and even connect them to each other via ``services`` and pass ``secret`` ``variables`` to the pods

generate the base64 code of your give string im using 1qaz!QAZ for the mysql root user password in the lab

```shell
echo -n '1qaz!QAZ' | base64
```

create the secret with name: 'mysql-secrets', key: 'root-password' value: base64OutputOfTheLastCmd

```shell
kubectl create -f files/mysqlSec.yaml 
```

check is it created or not

```shell
kubectl get secret
```

deploying the mysql pod

```shell
kubectl create -f files/mysqlDep.yaml 
```

watch the deploying process

```shell
watch kubectl get pod 
```

create a service to access mysql pod named by 'mysql-service'

```shell
kubectl create -f files/mysqlSvc.yaml 
```

check everything to be sure it fine

```shell
kubectl describe pod mysql-deployment 
```

deploying the phpMyAdmin pod

```shell
kubectl create -f files/phpDep.yaml 
```

watch the deploying process

```shell
watch kubectl get pod
```

create a service to access phpMyAdmin pod(s) named by 'phpmyadmin-service'

```shell
kubectl create -f files/phpSvc.yaml  
kubectl get service
```

check are they created or not

```shell
kubectl get pod
```

create the ingress to all external users access to your phpMyAdmin pod(s) va kubenetes internal Load Balancer

```shell
kubectl create -f files/phpIng.yaml
kubeclt get ingress
kubectl describe ingress phpmyadmin-ingress
```

check are they created or not

```shell
kubectl get all
```

where should my users access to php? lets find out

```shell
kubectl describe ingress phpmyadmin-ingress | grep phpmyadmin-service:80
```

check the found ip address. if its ok you can point a browser to the ip and login

```shell
curl http://ipOfTheLastCmd
```
