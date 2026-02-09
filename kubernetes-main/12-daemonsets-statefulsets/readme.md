# 12-daemonsets-statefulsets

# Create a DaemonSet

```bash
kubectl apply -f daemonset.yaml
```

Cada replica que tenemos en el daemonset se configura para que se ejecute en un nodo a la vez

Debemos tener 1 nodo para cada replica que queramos ejecutar

# Verify the setup
```bash
kubectl get ds
kubectl get pods -l app=nginx-app
```

# Create a StatefulSet and its PersistentVolume

```bash
# Make sure your PV and PVC exist first
kubectl apply -f pv-pvc.yaml
# Then apply the StatefulSet
kubectl apply -f statefulset.yaml
```

El persisten volume, en el ejemplo es una carpeta pero en produccion puede ser una base de datos SQL por ejemplo


Al borrar la union pv, pvc , hay que eliminar el pvc.

El estatefulset esta diseñado para aplicaciones que requieren el uso de bases de datos.

El statefulset necesita un service

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  clusterIP: None  # Headless service
```

El daemon set NO es persistente.

# Verify the setup
```bash
kubectl get sts
kubectl get pods -l app=nginx-app
kubectl get pvc my-pvc
```

# Delete the StatefulSet
```bash
kubectl delete sts nginx-sts
```


![alt text](image.png)

![alt text](image-1.png)

![alt text](image-2.png)

![alt text](image-3.png)

Con el statefulset y el daemonset no podemos hacer rollback inmediato como hariamos con un deployment.


### ¿Cuáles son los casos de uso y limitaciones de DaemonSets y StatefulSets?

#### Casos de uso para DaemonSets:
- Agentes de monitoreo: como Prometheus, que necesitan ejecutarse en cada nodo
- Recolección de logs: herramientas como Logstash o Fluentd
- Proxies de red: como kube-proxy
- Daemons de almacenamiento: que necesitan ejecutarse en cada nodo


#### Casos de uso para StatefulSets:
- Bases de datos: MySQL, PostgreSQL (para desarrollo, no siempre recomendado para producción)
- Sistemas distribuidos: Kafka, Elasticsearch
- Aplicaciones que requieren identidades persistentes

#### Limitaciones:

Tanto los DaemonSets como los StatefulSets tienen restricciones importantes a considerar:

No permiten rollbacks inmediatos como los Deployments
Solo se pueden escalar o reducir de un pod a la vez
Esto puede afectar la experiencia del usuario dependiendo del dominio de aplicación
Es importante entender estas limitaciones para determinar si estos objetos son adecuados para tu caso de uso específico o si sería mejor utilizar otras alternativas como los Deployments.

El poder de Kubernetes radica en su capacidad para desacoplar componentes y crear pods efímeros cuando sea necesario, proporcionando soluciones específicas para diferentes escenarios de despliegue a través de sus diversos objetos y recursos.

¿Has utilizado DaemonSets o StatefulSets en tus proyectos? ¿Qué otros casos de uso crees que serían adecuados para estos objetos? Comparte tu experiencia en los comentarios.



### Otras diferencias entre DaemonSets y StatefulSets y Deployments:

Los pods creados por estas entidades son controlados de forma diferente.

- Deployments: los pods de un Deployment son efímeros y pueden ser reemplazados, son controlados por un ReplicaSet, y no tienen identidad persistente.

- DaemonSets: los pods de un DaemonSet se ejecutan en cada nodo y no tienen identidad persistente, pero son controlados por el DaemonSet controller.

- StatefulSets: los pods de un StatefulSet tienen identidad persistente y son controlados por el StatefulSet controller, lo que les permite mantener su estado a través de reinicios y escalados.

### Aporte Platzi Estudiantes
Compañeros, aquí está un resumen claro de los conceptos que el profesor explicó. Espero que les ayude a entender mejor

Pod = Unidad Básica

• Es lo más pequeño en Kubernetes

• Contiene uno o más contenedores que se escalan juntos

• Son EFÍMEROS (se pueden eliminar y recrear)

══════

🚀 LOS 3 TIPOS DE WORKLOADS

1. DEPLOYMENT 📌 Para aplicaciones web normales

✅ Uso: Aplicaciones sin estado (APIs, sitios web)

✅ Ventaja: Fácil de escalar y gestionar

❌ Limitación: Los pods son intercambiables, pierden datos al reiniciar

💡 Ejemplo: Una API REST que no guarda datos importantes

2. STATEFULSET 📌 Para aplicaciones que NECESITAN guardar datos

✅ Uso: Bases de datos, aplicaciones con estado

✅ Ventaja: Cada pod tiene su propio almacenamiento permanente

✅ Extra: Cada pod tiene un nombre DNS único y estable (<pod-name>.<service-name>.<namespace>.svc.cluster.local)

💡 Ejemplo: MySQL, PostgreSQL, MongoDB

3. DAEMONSET 📌 Para servicios que deben estar en TODOS los nodos

✅ Uso: Monitoreo, logging, servicios de sistema

✅ Ventaja: Se ejecuta automáticamente en cada servidor del cluster

✅ Auto-escala: Si agregas un servidor, se instala automáticamente

💡 Ejemplo: Agente de monitoreo como Prometheus

═════

🤔 ¿CUÁL USAR? - GUÍA RÁPIDA

¿Mi aplicación guarda datos importantes?

NO → DEPLOYMENT

SÍ → STATEFULSET

¿Necesito que algo corra en CADA servidor?

SÍ → DAEMONSET

════

📊 TABLA COMPARATIVA RÁPIDA

DEPLOYMENT STATEFULSET DAEMONSET

Datos: Se pierden Se mantienen Depende

Escalamiento: Manual Manual Automático

Identidad: Intercambiable Única Una por nodo

Uso típico: Web apps Bases de datos Agentes/Monitoreo

═════

💡 EJEMPLOS DEL MUNDO REAL

DEPLOYMENT:

• Sitio web de e-commerce

• API de usuarios

• Frontend de React/Vue

STATEFULSET:

• Base de datos MySQL (En local para desarrollo)

• Sistema de colas como Kafka

• Elasticsearch cluster

DAEMONSET:

• Antivirus en cada servidor

• Recolector de logs

• Agente de backup

════