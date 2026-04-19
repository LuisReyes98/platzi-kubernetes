# Leer logs en Kubernetes

En Kubernetes, los **logs solo existen a nivel de Pod/contenedor**, porque son los contenedores los que realmente ejecutan procesos. Los Deployments, Services, ReplicaSets, etc. son abstracciones que no generan logs propios, pero puedes acceder a los logs de los pods que gestionan usando selectores de etiquetas.

## Logs de un Pod

El comando básico es `kubectl logs`:

```bash
# Logs de un pod
kubectl logs <nombre-del-pod>

# Si el pod tiene múltiples contenedores, especifica cuál
kubectl logs <nombre-del-pod> -c <nombre-del-contenedor>

# Seguir los logs en tiempo real (como tail -f)
kubectl logs -f <nombre-del-pod>

# Ver las últimas N líneas
kubectl logs --tail=100 <nombre-del-pod>

# Logs desde hace un tiempo específico
kubectl logs --since=1h <nombre-del-pod>

# Logs del contenedor anterior (útil si el pod se reinició por un crash)
kubectl logs --previous <nombre-del-pod>

# En un namespace específico
kubectl logs <nombre-del-pod> -n <namespace>
```

## Logs de un Deployment

Usas la flag `deployment/` o el selector de etiquetas:

```bash
# Opción 1: directamente con el nombre del deployment
kubectl logs deployment/<nombre-deployment>

# Opción 2: usando selector de etiquetas (ve logs de TODOS los pods que coincidan)
kubectl logs -l app=<nombre-app>

# Seguir logs de todos los pods del deployment
kubectl logs -f deployment/<nombre-deployment>

# Con --all-containers si hay sidecars
kubectl logs deployment/<nombre-deployment> --all-containers=true
```

## Logs de un Service

Los Services no tienen logs propios (son solo reglas de red). Para ver los logs de los pods detrás de un service, usa su selector:

```bash
# Primero revisa qué selector usa el service
kubectl describe service <nombre-service>

# Luego usa ese selector para ver los logs
kubectl logs -l app=<valor-del-selector>
```

## Logs de otros recursos

```bash
# StatefulSet
kubectl logs statefulset/<nombre>

# DaemonSet
kubectl logs daemonset/<nombre>

# Job
kubectl logs job/<nombre-job>

# ReplicaSet
kubectl logs rs/<nombre-replicaset>
```

## Combinaciones útiles

```bash
# Todos los pods con una etiqueta, siguiendo en vivo
kubectl logs -f -l app=mi-app --all-containers=true

# Logs de pods con múltiples etiquetas
kubectl logs -l "app=mi-app,tier=backend"

# Con timestamps
kubectl logs <pod> --timestamps=true

# Limitar la cantidad de pods mostrados (por defecto hay un límite)
kubectl logs -l app=mi-app --max-log-requests=10
```

## Tip práctico: stern

Si trabajas mucho con Kubernetes, instala [`stern`](https://github.com/stern/stern), una herramienta que hace mucho más fácil seguir logs de múltiples pods simultáneamente con colores:

```bash
stern <patron-nombre-pod>
stern -l app=mi-app
stern --namespace produccion .
```

## Resumen del flujo mental

Cuando quieras logs de cualquier recurso, pregúntate: **"¿qué pods genera este recurso?"**. Luego usa `kubectl logs` apuntando a esos pods, ya sea por nombre, por el recurso padre (`deployment/`, `statefulset/`), o por selector de etiquetas (`-l key=value`).