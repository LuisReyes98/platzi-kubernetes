# Setting cluster on EKS AWS

## Prerequisites

- AWS CLI
- kubectl
- eksctl (https://eksctl.io/introduction/#installation)
    https://eksctl.io/


## Identificar el ID de la cuenta de AWS

```sh
aws sts get-caller-identity
```

## Create cluster

Crear el cluster de forma imperativa

```
eksctl create cluster --name=k8s-course --region=us-west-2 --node-type=t3.small --nodes=2 --nodes-min=1 --nodes-max=2
```

Crear el cluster de forma declarativa

```
eksctl create cluster -f simple-cluster.yaml
```

## Conocer los contextos del kubectl

```
kubectl config get-contexts
```

## Cambiar el contexto del kubectl

```
kubectl config use-context <context-name>
```

Ver los nodes del cluster

```sh
k get nodes
```

## Crear un pod de prueba

```
kubectl run hello-cloud --image=gcr.io/google-samples/hello-app:2.0 --restart=Never --port=8080
```

## Ver los pods existentes

```
kubectl get pods
```

## Exponer un servicio con port-forward
Cuando tenemos cluster en producción, no podemos exponer los pods directamente, por lo que deberiamos usar un LoadBalancer o un Ingress.

```
kubectl port-forward pod/hello-cloud 8080:8080
```

### Exponer un servicio con LoadBalancer

```
kubectl expose pod hello-cloud --type=LoadBalancer --port=8080 --target-port=8080 --name=hello-cloud
```

Para listar los servicios y obtener la IP del LoadBalancer:

```sh
kubectl get services
```

### Delete cluster

```
eksctl delete cluster --name=dev-1 --region=us-west-2
```


