# Lista de entidades en Kubernetes que pueden ser gestionadas a través de kubectl y otros comandos:

- pods: `kubectl get pods`
- deployments: `kubectl get deployments`
- services: `kubectl get services`
- nodes: `kubectl get nodes`
- namespaces: `kubectl get namespaces`
- configmaps: `kubectl get configmaps`
- secrets
- volumes
- persistentvolumes `pv`
- persistentvolumeclaims `pvc`
- statefulsets
- daemonsets
- replicasets
- jobs
- cronjobs
- ingresses
- networkpolicies
- resourcequotas
- horizontalpodautoscalers
- verticalpodautoscalers


## Comparacion entre Deployments, DaemonSets y StatefulSets
extraido de: https://pabpereza.dev/docs/cursos/kubernetes/daemonset_y_statefulset_en_kubernetes_guia_completa

Comparemos primero los Deployments con los DeamonSets y StatefulSets:

| Característica | Deployments | DaemonSets | StatefulSets | ReplicaSets |
|---|---|---|---|---|
| Propósito principal | Gestionar aplicaciones sin estado | Ejecutar pods en todos los nodos | Gestionar aplicaciones con estado | Mantener un número estable de réplicas de pods |
| Escalabilidad | Escalado automático y manual | No escalable, un pod por nodo | Escalado manual | Escalado manual |
| Identidad de los pods | No garantiza identidad única | No garantiza identidad única | Garantiza identidad única | No garantiza identidad única |
| Persistencia de datos | No garantiza persistencia | No garantiza persistencia | Garantiza persistencia | No garantiza persistencia |
| Casos de uso comunes | Aplicaciones web, APIs | Agentes de monitoreo, logging | Bases de datos, sistemas distribuidos | Garantizar disponibilidad de pods (generalmente usado por Deployments) |
| Distribución de pods | Basado en el número deseado | Uno por nodo o subconjunto de nodos | Basado en el número deseado | Basado en el número deseado |
| Orden de despliegue | No garantiza orden específico | No garantiza orden específico | Garantiza orden de despliegue | No garantiza orden específico |
| Gestión de actualizaciones | Rolling updates, rollback | Rolling updates por nodo | Rolling updates ordenados | No gestiona actualizaciones automáticas |
| Relación con otros recursos | Gestiona ReplicaSets internamente | Independiente | Independiente | Usado internamente por Deployments |
