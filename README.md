# Kubernetes

# Clase 1

## ¿Qué es Kubernetes y por qué es esencial?
¿Has notado cómo plataformas populares como Netflix y Spotify gestionan eficientemente millones de usuarios sin interrupciones? Esto es posible gracias a Kubernetes, a menudo referido como "K ocho S". Kubernetes es una herramienta que garantiza que las aplicaciones en la nube funcionen de manera impecable, como una orquesta perfectamente sincronizada.

## ¿Cómo funciona Kubernetes?
Imagina que Kubernetes es el director de una orquesta, donde cada contenedor es un músico. En caso de que un músico cometiera un error o dejara de tocar, Kubernetes automáticamente lo sustituiría para que la música continuara sin interrupciones. Ahora, si la audiencia aumenta de repente, Kubernetes añade más músicos automáticamente, asegurando que la sinfonía no se vea afectada.

## ¿Por qué aprender Kubernetes?
Alta disponibilidad: Kubernetes garantiza que, si un contenedor falla, otro toma inmediatamente su lugar, asegurando la continuidad del servicio.
Escalabilidad automática: cuando el tráfico de una aplicación incrementa, Kubernetes añade más recursos automáticamente para gestionar la carga adicional.
Portabilidad: Kubernetes asegura que tu aplicación funcionará de la misma manera, ya sea en una computadora local o en la nube.
## ¿Qué aprenderás sobre Kubernetes?
Al embarcarte en este viaje de aprendizaje, descubrirás cómo montar tu propio clúster local utilizando herramientas como MiniKube. Aprenderás a manejar una arquitectura compleja de Kubernetes, entendiendo cómo cada parte de la "orquesta", como pods, deployments y réplicas, trabaja en conjunto. Además, se profundizará en el despliegue de aplicaciones que no solo sean escalables, sino también tolerantes a errores, garantizando así que la "música" nunca se detenga, incluso frente a fallos.

## Configuración de un clúster local
Configurar un clúster local es similar a montar una orquesta desde cero en tu computadora. MiniKube es una herramienta clave en este proceso:

```sh
minikube start
```

Este comando lanza un clúster local básico en tu máquina, proporcionando el entorno necesario para ejecutar Kubernetes de manera local.

## Resolución de problemas y optimización
Una parte crucial del aprendizaje con Kubernetes es aprender a solucionar problemas como un verdadero director de orquesta. Estarás equipado para identificar y resolver problemas de manera eficiente, manteniendo la armonía y continuidad de tus aplicaciones.

A medida que te adentres en el universo de Kubernetes, descubrirás que no es solo una herramienta. Es el director que transforma la gestión de la infraestructura en una sinfonía perfecta. Este curso es tu oportunidad para nutrir tus habilidades en infraestructura, desarrollo y la nube y elevarlas a un nivel profesional sólido y avanzado. ¡Únete y comienza a convertirte en un maestro orquestador del mundo tecnológico!

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


# Clase 2
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

Cuales son mis contextos disponibles?

```sh
kubectl config get-contexts
```

Cambiar de contexto a minikube

```sh
kubectl config use-context minikube
```

Cual es mi contexto actual?

```sh
kubectl config current-context
```

Cuales son los clusters disponibles?

```sh
kubectl config get-clusters
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

## ¿Cómo configurar un clúster local de Kubernetes con MiniKube?
Kubernetes es una herramienta poderosa y compleja, pero no es necesario tener un clúster gigante para comenzar a trabajar con ella. Puedes configurar un clúster en tu máquina local utilizándolo de manera simple y efectiva. MiniKube es la solución ideal para testar y experimentar con Kubernetes sin mucha complicación, y en este artículo te mostraremos cómo hacerlo. Sigue leyendo para descubrir cómo instalar y configurar MiniKube y KubeCtl en pasos sencillos.

##  ¿Qué herramientas necesitas instalar?
Para trabajar con Kubernetes en un entorno local, se requieren dos herramientas esenciales:

KubeCtl: permite la comunicación con el clúster.
MiniKube: despliega una instancia de Docker para simular el entorno de Kubernetes.
## Instalación de KubeCtl
Para instalar KubeCtl en macOS usando HomeBrew, simplemente ejecuta:

`brew install kubectl`
Una vez instalado, puedes verificar su funcionamiento ejecutando:

```sh
kubectl version --client
kubectl --help
```
Esto te proporcionará una lista de comandos básicos a utilizar. No te preocupes si parece mucha información; a lo largo del aprendizaje te familiarizarás con estos comandos.

## Instalación de MiniKube
Similarmente, para instalar MiniKube usando HomeBrew:
```sh
brew install minikube
```
Con MiniKube, puedes ejecutar:
```sh
minikube --help
```
Este comando te mostrará varias opciones, como iniciar, detener clústers, y conectar diferentes plugins.

¿Cómo inicializar tu clúster con MiniKube?
Ya con las herramientas instaladas, el siguiente paso es inicializar el clúster. Esto lo logras ejecutando:

```sh
minikube start --driver=docker
```

Este comando utiliza Docker como driver por defecto, pero MiniKube te permite trabajar con otros hypervisors como HyperB o VirtualBox, dependiendo de tu sistema operativo.

¿Cómo aprovechar las funcionalidades de MiniKube?
MiniKube no solo facilita la creación de clústers, sino que también cuenta con utilidades adicionales:

Crear clústers multinodo.
Configurar un dashboard de manera sencilla.
Exponer servicios a través de tunelización.
Además, puedes listar los plugins disponibles con:

minikube addons list
Para mejorar aún más la funcionalidad, puedes habilitar ciertos complementos como el 'registry' y el 'Metric Server':

```sh
        minikube addons enable registry
        eval $(minikube docker-env)
        minikube addons enable metrics-server
```
¿Cómo interactuar con tu clúster local?
Una vez completada la configuración, puedes ejecutar comandos básicos para interactuar con tu clúster local. Por ejemplo, para ver los nodos:

```sh
kubectl get nodes
```
Para gestionar y visualizar las imágenes de Docker dentro de tu clúster, puedes ejecutar:
```sh
docker images
```
Para comprobar el contexto del clúster y cambiar entre diferentes contextos, utiliza:

```sh
kubectl config get-contexts
kubectl config use-context "nombre-contexto"
```
¿Cómo desplegar aplicaciones en Kubernetes?
Puedes desplegar aplicaciones en tu entorno de Kubernetes de forma rápida. Por ejemplo, para desplegar una imagen de prueba:

```sh
kubectl run hello-cloud --image=nginx
```
Luego, verifica el estado de tus pods con:

```sh
kubectl get pods
```
¿Cómo usar el dashboard de Kubernetes?
MiniKube te permite interactuar con Kubernetes a través de un dashboard web. Puedes acceder a él con el siguiente comando:

```sh
minikube dashboard
```
Esto abrirá una URL en tu navegador, donde podrás visualizar tus pods, deployments y más, ofreciendo una representación gráfica del funcionamiento interno de Kubernetes.

Es impresionante como herramientas como MiniKube y KubeCtl pueden simplificar el aprendizaje y experimentación de Kubernetes. No te detengas aquí; continúa explorando, practicando y desarrollando tus habilidades para estar preparado en ambientes de producción reales.

Kubernetes se compone principalmente de servidores y nodos con:

- Nodos Master: se recomienda tener mas de un nodo maestro para tener alta disponibilidad.

- Nodos Worker: son los encargados de ejecutar las aplicaciones y servicios en contenedores.

![cluster_k8s](image.png)

En local puedes trabajar con un solo servidor en la capa de los maestros.

En desarrollo trabajaremos con un solo nodo en local con Minikube.

### Nodos maestros

![alt text](image-1.png)

El api server es el punto de entrada de todas las peticiones al cluster.

permitiendo que nuestro cluster orqueste recursos y servicios.

Al examinar a fondo los nodos maestro, encontramos varios componentes esenciales que conforman el control plane:

- API Server: Es el punto de entrada para toda comunicación dentro del cluster. Cuando ejecutas un comando como kubectl get pods, este llega al API Server, que se comunica con otros componentes para proporcionar la respuesta adecuada.

- etcd: Esta base de datos llave-valor de alta concurrencia registra cada cambio realizado, asegurando que el cluster siempre mantenga actualizado su estado deseado. Funciona como la "memoria" persistente de Kubernetes.

- Controller Manager: No es un solo controlador, sino un conjunto de ellos que monitorean diferentes aspectos del cluster, verifica que el estado deseado vs el estado actual coincidan, organizando y levantando recursos según sea necesario:

  - **El Node Controller** verifica la salud de todos los nodos
  - **El Replication Controller** asegura que exista la cantidad correcta de pods
  - **El Endpoint Controller** gestiona la comunicación entre servicios

- **Scheduler**: Decide en qué nodo se ejecutará cada pod, basándose en los recursos requeridos (CPU, memoria, GPU) y los recursos disponibles en cada nodo worker.

#### Ejemplo de una orquesta musical:
Si el control plain es un directo de orquesta
Enviando y recibiendo las partipuras con el API Server, guardandolas en el estado deseado del cluster en una base de datos etcd.
Controller Manager es la tarea de estar validando que los musicos no es equivoquen y siempre esten presente
y el Scheduler seria durante el concierto cuando indica que seccion musical debe tocar.

### Nodos Worker

![alt text](image-2.png)

Los nodos worker contienen componentes igualmente importantes:

- **Kubelet**: Este agente se ejecuta en cada nodo worker y se comunica con el API Server para garantizar que los contenedores funcionen correctamente. Si detecta errores, informa para que se tomen acciones correctivas.

- **kube-proxy**: Gestiona la capa de red del cluster, facilitando la comunicación entre pods y con el exterior.

- **Container Runtime Interface (CRI)**: Es el encargado de ejecutar los contenedores dentro del nodo. Aunque anteriormente se utilizaba Docker por defecto, las versiones más recientes de Kubernetes han migrado a containerd. (Anteriormente era Docker), con esta se comunica con todos los contenedores en ejecución.
K8s no corre contenedores directamente, sino que utiliza el CRI para gestionarlos.

![alt text](image-3.png)

Los namespaces son la separación lógica de recursos dentro del cluster. Y dentro de cada uno vive nuestro pod, nuestra unidad fundamental dentro de k8s.


## ¿Cómo se organizan las cargas de trabajo en Kubernetes?
Kubernetes utiliza conceptos importantes para organizar y gestionar las cargas de trabajo de manera eficiente:

## ¿Qué son los namespaces y cuál es su función?
Los namespaces proporcionan una separación lógica de recursos dentro del cluster. Esta organización depende del caso de uso específico de cada empresa:

- Algunos equipos definen namespaces por tipo de aplicación (frontend/backend)
- Otros prefieren organizar por equipos funcionales (pagos, interfaz de usuario, API)
- Lo importante es que Kubernetes se adapta a cualquier caso de uso sin inconvenientes
Dentro de estos namespaces viven los pods, que son la unidad fundamental de Kubernetes. Un pod puede contener uno o múltiples contenedores, dependiendo de las necesidades específicas.

## ¿Cómo gestionan los services la comunicación en Kubernetes?

Los services usan kube-proxy dentro de los nodos worker para gestionar la comunicación entre pods y con el exterior.

Los services son componentes que aceptan tráfico y lo redirigen a grupos específicos de pods. Existen diferentes tipos:

- **NodePort**: Utilizado principalmente en entornos de desarrollo, expone un puerto específico en cada nodo worker para permitir comunicación externa hacia los pods. No se recomienda para entornos productivos. **Nos permite abrir trafico del exterior hacia los pods de un cluster para casos de prueba, no es recomendado en entornos productivos.**

- **ClusterIP**: Permite comunicación interna dentro del cluster mediante una IP específica. Facilita el balanceo de carga entre pods asociados a una misma aplicación. Garantiza mejor conexion hacia cada uno de nuestros pods.

- **LoadBalancer**: Al trabajar con Kubernetes en la nube, este tipo de servicio crea automáticamente un balanceador de carga en el proveedor de servicios cloud, garantizando un tráfico más escalable y resiliente. Crea un loadbalancer dentro de nuestro cloud provider (AWS, GCP, Azure) para distribuir el trafico entre los nodos worker. Para permitirnos un mejor trafico entre los componentes.

- **ExternalName**: **Altamente recomendado para entornos productivos**, permite mapear un nombre público (como una base de datos RDS en AWS) a un nombre privado dentro del cluster. Optimiza los tiempos de comunicación entre servicios internos y externos.


## ¿Cómo funciona el flujo de una aplicación en Kubernetes?
El despliegue de una aplicación en Kubernetes sigue un proceso bien definido:

![alt text](image-4.png)

1. Se despliega un pod dentro de un namespace específico, determinas la cantidad de pods que viviran dentro de una aplicacion.
2. El scheduler determina en qué nodo worker colocarlo
3. El kubelet en ese nodo arranca el contenedor correspondiente
4. El kube-proxy establece la capa de red para permitir comunicaciones
5. Los servicios (como un Ingress o un balanceador de carga) redirigen las peticiones HTTP desde Internet hacia los pods correctos

Este proceso completo permite que Kubernetes actúe como un verdadero director de orquesta, coordinando todos los elementos para que nuestra aplicación funcione de manera óptima, escalable y resistente a fallos.

La arquitectura de Kubernetes representa una solución elegante para los desafíos de la computación moderna, permitiendo despliegues resilientes y escalables sin importar la complejidad de la aplicación. ¿Has implementado Kubernetes en tu organización? ¿Qué otros aspectos de su arquitectura te gustaría explorar? Comparte tu experiencia en los comentarios.

# Clase 4 Introducción a la API de Kubernetes y Kubectl

## ¿Cómo configurar y empezar a trabajar con Kubernetes usando MiniKube?
Conocer cómo configurar y gestionar Kubernetes eficientemente es fundamental para cualquier profesional en el área de DevOps o administración de sistemas. Con un clúster configurado con MiniKube, podemos comenzar a explorar las capacidades de Kubernetes. A continuación, te ofrecemos una guía paso a paso basada en prácticas recomendadas para que puedas aprovechar al máximo las herramientas a tu disposición.

## ¿Cuál es el primer paso para iniciar con MiniKube y Kubernetes?
Primero, se debe tener el clúster local configurado con MiniKube. Este es una herramienta esencial que te permite gestionar tu clúster localmente, ofreciendo una plataforma flexible para diferentes configuraciones, como trabajar con múltiples nodos o diferentes versiones de Kubernetes. Para iniciar el clúster, usamos el comando:

```sh
minikube start --driver=docker
```

Este comando, además de levantar el clúster, puede ser complementado con varios parámetros específicos según tus necesidades, como el driver que prefieras usar.

Para ver los distintos perfiles de MiniKube que tienes configurados, puedes ejecutar:

```sh
minikube profile list
```

Los perfiles te permiten trabajar en diversas versiones de k8s o docker dependiendo de tus requerimientos.


## ¿Qué es KubeCTL y cómo interactuamos con Kubernetes?

```sh
kubectl get --help
```

KubeCTL es el puente esencial hacia el API server de tu clúster de Kubernetes. A través de este, podemos efectuar una variedad de solicitudes como crear, leer, actualizar y eliminar (CRUD) recursos. Un ejemplo básico para consultar los recursos es el comando:

```sh
kubectl get pods
```

Con este, podemos listar los pods activos en nuestro namespace actual. Sin embargo, para obtener más detalles, podemos usar:

```sh
kubectl get pods -o wide
```

Para buscar los pods a lo largo de todos los namespaces, utilizamos:

```sh
kubectl get pods -A
```

y verlos con detalles:

```sh
kubectl get pods -o wide -A
```

## ¿Qué son los namespaces y cómo gestionarlos?
Los namespaces son cruciales para organizar y separar lógicamente los recursos dentro de Kubernetes. Por defecto, el clúster tiene un namespace de "default", pero puedes crear y eliminar adicionales según sea necesario:

- Crear un nuevo namespace:

```sh
kubectl create namespace k8s-demo
```

```sh
kubectl create ns k8s-demo
```

- Validar la creación del namespace:

```sh
kubectl get namespaces
```

```sh
kubectl get ns
```

- Eliminar un namespace:

```sh
kubectl delete namespace k8s-demo
```

```sh
kubectl delete ns k8s-demo
```


## ¿Cómo gestionamos nodos dentro de Kubernetes?
Un aspecto importante de Kubernetes es la gestión de nodos que conforman el clúster, donde ejecutamos operaciones con:

- Listar nodos:

```sh
kubectl get nodes
```

- Describir un nodo:

```sh
kubectl describe node ${NOMBRE_DEL_NODO}
```

Estos comandos ofrecen información valiosa sobre el rol, estado y recursos del nodo.

## ¿Cómo se aplican configuraciones operadores declarativas e imperativas?

Kubernetes permite dos estilos para gestionar configuraciones:

Declarativa: utiliza archivos YAML para definir el estado deseado del sistema.
Imperativa: ejecuta comandos directamente para llevar a cabo una acción específica.
Para aplicar un pod usando un archivo YAML de manera imperativa, utilizamos:

```sh
kubectl apply -f simple-pod.yaml
```

Y para borrar ese pod si ya no es necesario:

```sh
kubectl delete pod
```

```sh
kubectl describe pods ${NOMBRE_DEL_POD}
```

```sh
kubectl delete pod lonely-pod
```


## ¿Cómo mantener nuestro clúster a punto con MiniKube?
Para personalizar nuestro clúster y expandir sus funcionalidades, MiniKube ofrece varios add-ons. Algunos esenciales para mejorar la gestión son:

```sh
minikube addons list
```


- Metric Server: para obtener métricas del clúster y posibilidades de autoescalamiento.

```sh
minikube addons enable metrics-server
```
- Registry: vincula el registro de Docker con MiniKube.

```sh
minikube addons enable registry
```

Estos componentes son críticos para un manejo eficiente y un desarrollo fluido dentro de Kubernetes.

Ahora que hemos explorado las bases para interactuar y gestionar Kubernetes con MiniKube y KubeCTL, es momento de aprender a desplegar aplicaciones complejas. ¡Sigue explorando y aprende más sobre el despliegue de aplicaciones frontend y backend con Kubernetes!

# Clase 5 Diferencias entre enfoques declarativos e imperativos

05-declarative-vs-imperative

## Imperative

## Create a pod imperatively
```bash
kubectl run mypod --image=nginx
```

## Get a pod imperatively
```bash
kubectl get pods
```

## Delete a pod imperatively
```bash
kubectl delete pod mypod
```

# Declarative

## Create a pod declaratively

```bash
kubectl apply -f mypod.yaml
```

`-f` flag is for file


## Delete a pod declaratively
```bash
kubectl delete -f mypod.yaml
```


## Liveness probe:

indica si el contenedor está vivo. Si falla, el contenedor se reinicia.

https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/

# Clase 6 Pods, ReplicaSets y Deployments

```sh
kubectl get namespaces
```


Crear namespace

```sh
kubectl create ns pod-test
```


Crear un pod dentro del namespace pod-test
```sh
kubectl create pod -n pod-test
```


## Que es un pod?

Un Pod es la unidad más pequeña y básica de Kubernetes. Representa una instancia de una aplicación en ejecución en el clúster. Un Pod puede contener uno o más contenedores que comparten:

- Red: Todos los contenedores dentro de un Pod comparten la misma dirección IP y puerto.
- Almacenamiento: Los contenedores pueden compartir volúmenes montados.
- Ciclo de vida: Los contenedores dentro de un Pod se crean, ejecutan y eliminan juntos.

### Forma imperativa (CLI)

**Crear un pod de nginx**

```sh
kubectl run nginx-nodeport --image=nginx --restart=Never --port=80
```

```sh
kubectl describe pods nginx-nodeport
```

```sh
kubectl get svc
```

**Ver pods existentes**

```sh
kubectl get pods
```

**Exponer un servicio con port-forward**

```sh
kubectl port-forward pod/nginx-nodeport 8080:80
```

# Que significa Stateless vs statefull: tener o no tener estado, ahí está el dilema.

En Kubernetes, las aplicaciones pueden ser stateless (sin estado) o stateful (con estado). Esto afecta cómo se diseñan y gestionan los Pods.

#### Stateless (sin estado):
- No guardan datos persistentes entre reinicios.
- Ejemplo: Servidores web como Nginx o aplicaciones que procesan solicitudes HTTP.
- Escalabilidad sencilla: Puedes agregar o eliminar réplicas sin preocuparte por la consistencia de datos.

#### Stateful (con estado):
- Guardan datos persistentes y necesitan mantener el estado entre reinicios.
- Ejemplo: Bases de datos como MySQL o Redis.
- Requieren volúmenes persistentes (Persistent Volumes) para almacenar datos.

## ReplicaSets: Garantizar la disponibilidad de Pods.

Los replicasets en kubernetes son responsables de mantener un número estable de réplicas de pods en ejecución en todo momento. Si un pod falla o se elimina, el replicaset automáticamente crea un nuevo pod para reemplazarlo, asegurando así la disponibilidad continua de la aplicación.

### Forma declarativa

**Crear un ReplicaSet**

```sh
kubectl apply -f replicaset.yaml
```

**Ver pods existentes**

```sh
kubectl get pods
```

**Ver ReplicaSet existentes**

```sh
kubectl get replicaset
```

**Eliminar un Pod**

```sh
kubectl delete pod nginx-replicaset-<pod-id>
```
Al eliminar un Pod, el ReplicaSet automáticamente crea un nuevo Pod para mantener el número deseado de réplicas (pods).


Eliminar replicaset

```sh
kubectl delete -f replicaset.yaml
```

## Deployments: Gestión declarativa de aplicaciones.

Un Deployment es una capa superior que gestiona ReplicaSets y proporciona una forma declarativa de implementar aplicaciones. Es la forma más común de gestionar aplicaciones en Kubernetes.


### Forma declarativa

**Crear un Deployment**

```sh
kubectl apply -f deployment.yaml
```

**Ver pods existentes**

```sh
kubectl get pods
```

**Ver Deployment existentes**

```sh
kubectl get deployment
```

Ver replicaset que creo el deployment

```sh
kubectl get replicaset
```

El beneficio de usar deployments es que nos facilita gestionar nuevas versiones de nuestra aplicacion. Y actualizar sin degradacion del servicio.

El deployment es el objeto mayor que orquesta a un replicaset.

**Describe el replicaset de un deployment**

```sh
kubectl describe replicaset <replicaset-name>
```

Y mostrara la informacion del deployment que lo controla

```txt
Name:           hello-deployment-584f88f49b
Namespace:      default
Selector:       app=hello,pod-template-hash=584f88f49b
Labels:         app=hello
                pod-template-hash=584f88f49b
Annotations:    deployment.kubernetes.io/desired-replicas: 4
                deployment.kubernetes.io/max-replicas: 5
                deployment.kubernetes.io/revision: 1
Controlled By:  Deployment/hello-deployment
Replicas:       4 current / 4 desired
Pods Status:    4 Running / 0 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:  app=hello
           pod-template-hash=584f88f49b
  Containers:
   hello-app:
    Image:         gcr.io/google-samples/hello-app:1.0
    Port:          8080/TCP
    Host Port:     0/TCP
    Environment:   <none>
    Mounts:        <none>
  Volumes:         <none>
  Node-Selectors:  <none>
  Tolerations:     <none>
Events:
  Type    Reason            Age   From                   Message
  ----    ------            ----  ----                   -------
  Normal  SuccessfulCreate  15m   replicaset-controller  Created pod: hello-deployment-584f88f49b-t9tkd
  Normal  SuccessfulCreate  15m   replicaset-controller  Created pod: hello-deployment-584f88f49b-swhzn
  Normal  SuccessfulCreate  15m   replicaset-controller  Created pod: hello-deployment-584f88f49b-7gm8l
  Normal  SuccessfulCreate  15m   replicaset-controller  Created pod: hello-deployment-584f88f49b-br6zw
```

**Eliminar un Pod**

```sh
kubectl delete pod hello-deployment-<pod-id>
```

**Actualizar la imagen del Deployment**

```sh
kubectl set image deployment/hello-deployment hello-app=gcr.io/google-samples/hello-app:2.0
```

**Verificar el progreso de la actualización**

```sh
kubectl rollout status deployment/hello-deployment
```

**Verificar los Pods actualizados**

```sh
kubectl get pods
```

Si haces que falle a prosposito la actualizacion

```sh
kubectl set image deployment/hello-deployment hello-app=gcr.io/google-samples/hello-app:3.0
```


**Verificar los Pods actualizados**
Donde podemos ver un error de imagen

```sh
kubectl get pods
```

```
NAME                                READY   STATUS              RESTARTS   AGE
hello-deployment-584f88f49b-br6zw   1/1     Running             0          24m
hello-deployment-584f88f49b-swhzn   1/1     Running             0          24m
hello-deployment-584f88f49b-t9tkd   1/1     Running             0          24m
hello-deployment-657cbcfdfd-dgh7p   0/1     ContainerCreating   0          5s
hello-deployment-657cbcfdfd-tgwrn   0/1     ErrImagePull        0          5s
```

**Y en el estaus del rollout** podemos ver que hay un error

```sh
kubectl rollout status deployment/hello-deployment
```
```text
Waiting for deployment "hello-deployment" rollout to finish: 2 out of 4 new replicas have been updated...
```

**Revertir la última actualización**

```sh
kubectl rollout undo deployment/hello-deployment
```


**Exponer un Deployment**

```sh
kubectl port-forward deploy/hello-deployment 8080:8080
```


# Clase 7 Servicios e Ingress: Exposición de aplicaciones

La capacidad de exponer aplicaciones al mundo exterior es fundamental en los entornos de Kubernetes. Entre las diversas opciones disponibles, el Ingress destaca por ofrecer una capa adicional de personalización que va más allá de los servicios tradicionales. Comprender las diferencias entre estos mecanismos de exposición permite a los desarrolladores y administradores de sistemas elegir la solución más adecuada para cada escenario.

## ¿Qué opciones tenemos para exponer servicios en Kubernetes?

Antes de profundizar en el Ingress, es importante revisar los diferentes tipos de servicios que Kubernetes ofrece para exponer aplicaciones:

**NodePort**: Expone un puerto específico en cada uno de los nodos del clúster de Kubernetes. Esto permite aceptar tráfico desde Internet o desde el interior del clúster hacia un grupo de pods, simplemente especificando la dirección IP y el puerto configurado.

**ClusterIP**: Asigna a cada servicio una IP dentro del rango del cluster CIDR. Este tipo facilita la comunicación entre diferentes pods del mismo namespace, de diferentes namespaces o incluso de diferentes hosts, lo cual es esencial para aplicaciones expuestas al mundo real o microservicios que necesitan comunicarse internamente.

**LoadBalancer**: Cuando trabajamos con un clúster de Kubernetes en AWS, este tipo de servicio es gestionado automáticamente por la capa de red de AWS.

**ExternalName**: Similar a los registros CNAME en DNS, actúa como un wrapper de una dirección bien construida (como una dirección de base de datos en AWS). Estos servicios permiten agregar capacidades de caché y resolución de nombres que optimizan el tráfico desde el interior del clúster hacia servicios externos.

## ¿Qué es el Ingress y cómo se diferencia de los otros servicios?

El Ingress va más allá de los servicios mencionados anteriormente y proporciona capacidades avanzadas para exponer aplicaciones:

- Permite realizar balanceo de carga
- Ofrece validación de terminación SSL
- Facilita la gestión de hosting virtual mediante paths y subpaths en los hosts registrados

Un caso de uso típico sería un cliente que desea acceder a una aplicación llamada "myapp.com". Con Ingress, podemos configurar diferentes rutas:

- `api.myapp.com/login` que dirige al usuario a servicios de backend

- `myapp.com/dashboard` que conduce a servicios frontend con interfaces de usuario

Esta separación lógica mediante nombres de dominio y paths hace que las aplicaciones sean mucho más accesibles para los usuarios finales.

![ingres kubernetes](image-5.png)

Hay diferentes tipos de ingress managers como:

![alt text](image-6.png)


## Habilita el Ingress controller:

```bash
minikube addons enable ingress
```

## Verifica que el NGINX Ingress controller esté funcionando:

```bash
kubectl get pods -n ingress-nginx
```

## Despliega una app "hello, world":

```bash
kubectl create deployment web --image=gcr.io/google-samples/hello-app:1.0
```

```bash
kubectl get deploy
```

## Exposición del Deployment:

```bash
kubectl expose deployment web --type=NodePort --port=8080
```

```bash
kubectl get service
```

```bash
kubectl delete service web
```

## Accede al servicio usando la IP proporcionada:

```bash
minikube service web --url
```

## Crea un Ingress:

```bash
kubectl apply -f https://k8s.io/examples/service/networking/example-ingress.yaml
```

## Verifica que el Ingress esté correctamente configurado:

```bash
kubectl get ingress
```

```bash
kubectl describe ingress example-ingress
```


```bash
minikube tunnel
```

```bash
curl http://hello-world.example
```

# Clase 8 ConfigMaps y Secrets: Configuración y datos sensibles