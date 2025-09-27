# Kubernetes

## ¿Qué Kubernetes es y por qué es importante?

un sistema de orquestacion

si un musico deja de tocar, el sistema se encarga de reemplazarlo o agregar mas musicos para que la orquesta siga tocando con la nueva alta demanda.

### ¿Por qué aprender Kubernetes?
Alta disponibilidad: Kubernetes garantiza que, si un contenedor falla, otro toma inmediatamente su lugar, asegurando la continuidad del servicio.
Escalabilidad automática: cuando el tráfico de una aplicación incrementa, Kubernetes añade más recursos automáticamente para gestionar la carga adicional.
Portabilidad: Kubernetes asegura que tu aplicación funcionará de la misma manera, ya sea en una computadora local o en la nube.

### Configuración de un clúster local
Configurar un clúster local es similar a montar una orquesta desde cero en tu computadora. MiniKube es una herramienta clave en este proceso:

minikube start
- pods
- deployments
- replica set


## Configurar un clúster local con Minikube

### Instalar

https://kubernetes.io/docs/tasks/tools/

https://minikube.sigs.k8s.io/docs/start/?arch=%2Flinux%2Fx86-64%2Fstable%2Fdebian+package

- `kubectl`
- `minikube`

```sh
minikube start --driver=docker
```

```sh
docker ps
```

```sh
kubectl get nodes
```

```sh
kubectl get pods -A
```

```sh
minikube addons list

minikube addons enable registry

minikube addons enable metrics-server
```

### Contextos

```sh
kubectl config get-contexts
```

```sh
kubectl config use-context minikube
```


### Minikube

```sh
kubectl run hello-cloud --image=nginx
```

```sh
minikube dashboard
```

```sh
minikube start

minikube stop
```



# Clase 3



Kubernetes se compone principalmente de servidores y nodos con:

- Nodos Master: se recomienda tener mas de un nodo maestro para tener alta disponibilidad.

- Nodos Worker: son los encargados de ejecutar las aplicaciones y servicios en contenedores.

![cluster_k8s](image.png)

En desarrollo trabajaremos con un solo nodo en local con Minikube.

### Nodos maestros

![alt text](image-1.png)

El api server es el punto de entrada de todas las peticiones al cluster.

permitiendo que nuestro cluster orqueste recursos y servicios.



### Nodos Worker

![alt text](image-2.png)

En estos nodos worker es donde encontraras todos los pods de tus aplicaciones.



