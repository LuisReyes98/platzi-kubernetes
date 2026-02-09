# Despliegue de una aplicación de frontend y backend en Kubernetes

## Prerequisitos

- Tener instalado Kubernetes
- Tener instalado Docker
- Tener instalado kubectl
- Minikube instalado

## Configuracion de minikube para tomar imagenes de registry local

```sh
minikube start --driver=docker
```

```sh
eval $(minikube docker-env)

docker ps

docker-compose build
```

## Frontend

## Backend

minikube addons enable metrics-server



# Notas

Ejecutar todos los archivos de un directorio en kubernetes

```sh
kubectl apply -f k8s/backend/
```



🚨 ¡Cuidado con el error ErrImageNeverPull en Minikube!

Si al levantar tus Deployments de backend y frontend te aparece ErrImageNeverPull, es porque Kubernetes no puede encontrar tus imágenes dentro de Minikube.

🧐 El profesor usó antes:

eval $(minikube docker-env)

Y luego:

docker compose up --build

👉 Esto hizo que las imágenes se crearan directamente en Minikube y quedaran listas para los Pods, incluso después de detener los contenedores.

Si tú hiciste docker compose sin ese comando, las imágenes se quedaron solo en tu PC y Minikube no las ve.

✅ ¿Cómo arreglarlo?

Ejecuta:
eval $(minikube docker-env)

Reconstruye las imágenes:
docker build -t backend:latest ./backend docker build -t frontend:latest ./frontend

Lanza los Deployments:
kubectl apply -f k8s/backend/ kubectl apply -f k8s/frontend/

Y listo 🚀. Los Pods deberían levantar sin problemas.


## Para Node port local

```sh
minikube service frontend-service
```


## Para LoadBalancer local

```sh
minikube tunnel
```