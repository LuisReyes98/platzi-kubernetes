# Troubleshooting Guide

## Comandos usados para solucionar problemas

```sh
kubectl get pods
kubectl get pods -o wide
kubectl get nodes
kubectl get svc
kubectl logs <pod-name>
kubectl logs <pod-name> -f
kubectl logs <pod-name> -c <container-name>
kubectl logs <pod-name> -c <container-name> -f
kubectl exec -it <pod-name> -- /bin/bash
kubectl exec -it <pod-name> -- /bin/sh
kubectl exec -it <pod-name> -- /bin/sh -c "ls -la"
kubectl logs deployment/<deployment-name>
kubectl logs deployment/<deployment-name> -f
kubectl logs deployment/<deployment-name> -c <container-name>
kubectl logs deployment/<deployment-name> -c <container-name> -f
kubectl describe pod <pod-name>
kubectl describe node <node-name>
kubectl describe svc <svc-name>
kubectl describe deployment <deployment-name>
kubectl describe ingress <ingress-name>
kubectl describe secret <secret-name>
kubectl rollout restart deployment/<deployment-name>
kubectl rollout status deployment/<deployment-name>
kubectl rollout undo deployment/<deployment-name>
kubectl rollout undo deployment/<deployment-name> --to-revision=<revision-number>
kubectl rollout history deployment/<deployment-name>
kubectl rollout history deployment/<deployment-name> --revision=<revision-number>
```

## Install metrics server on EKS

```
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

## Ver las metricas de los pods

```
kubectl top pods -n backend
```

## Comandos para solucionar problemas de MySQL

### Instalar mysql-client en el pod de alpine

```
apk add mysql-client -y
```

## Conectar a la base de datos
```
mysql -u $DB_USER -h $DB_HOST -D $DB_NAME -p
```


## Mis notas

```sh
kubectl get pods -n backend
# Describir un pod de  un namespace específico
kubectl describe pod <pod-name> -n backend

# apply -f con un namespace específico
kubectl apply  -n backend -f <file.yaml>

# obtener eventos de un pod específico
kubectl events -n backend --field-selector involvedObject.name=<pod-name>

# ver logs de un pod específico
kubectl logs <pod-name> -n backend

# Entrar en consola dentro de un pod
kubectl  -n backend exec -it <pod-name> -- bash
kubectl  -n backend exec -it <pod-name> -- sh

# Ver variables de entorno en consola
env
env | grep DB_

# Connect to mysql
mysql -u $DB_USER -h $DB_HOST -D $DB_NAME -p
```


Se debuguea el error de un pod con el comando `kubectl describe pod <pod-name>` y se lee la seccion de eventos para entender el error.


### Tipos de errores y su significado

- ImagePullBackOff: No se puede descargar la imagen del contenedor.
- CrashLoopBackOff: El contenedor se está reiniciando continuamente debido a un error en la aplicación.
- CreateContainerConfigError: Error al crear la configuración del contenedor, generalmente debido a variables de entorno o secretos mal configurados.

- OOMKilled: Out Of Memory Killed, el contenedor ha sido terminado por consumir demasiada memoria. y no tener recursos suficientes asignados.