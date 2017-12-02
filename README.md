#### Carlos Ocampo - A00052216
# Proyecto Kubernetes - Sistemas Distribuidos

Proyecto de Sistemas Distribuidos para construir y desplegar una app sencilla de Python en Kubernetes. 

## Requerimientos
- Docker
- Docker-compose
- Kubernetes

## Acerca de Kubernetes

Kubernetes coordina un cluster de computadores de alta disponibilidad que se conecta como una única unidad para trabajar. Las abstracciones en Kubernetes permite desplegar aplicaciones contenidas en un cluster sin necesidad de atarlas a una máquina individual.

Las aplicaciones contenidas son más flexibles y poseen mayor disponibilidad que otros modelos de despliegue en los cuales las aplicaciones se encuentran directamente instaladas en máquinas específicas como paquetes altamente integrados al host.
Kubernetes automatiza la distribución y la programación de los contenedores de las aplicaciones a lo largo del cluster de forma eficiente. Un cluster Kubernetes está compuesto por dos tipos de recursos, los cuales son mostrados en la Figura 1:

![][8]
Figura 1: Cluster Kubernetes

El Maestro es el responsable de gestionar y administrar el cluster. Este coordina todas las actividades del cluster, como la programación, el mantenimiento, las actualizaciones y la escalabilidad de las aplicaciones.

Un nodo es una máquina virtual o un computador físico que sirve como una máquina trabajadora en un cluster Kubernete. Cada nodo tiene un Kubelet, este es un agente para la administración de los nodos y la comunicación con el Maestro. Los nodos también deben contar con herramientas para el manejo de contenedores (Docker o rkt). Un cluster Kubernetes que maneje tráfico de producción debe tener mínimo 3 nodos.

Al desplegar una aplicación  en Kubernetes, se le indica al Maestro que inicie los contenedores de la aplicación. En este momento, el Maestro programa los contenedores para que correr en los nodos del cluster. Los nodos se comunican con el Maestro usando el API Kubernetes, el cual es expuesto por el Maestro.

## Desarrollo

### 1. Preparar el ambiente de kubernetes instalando minikube.

- Instalar VirtualBox

- Instalar Docker Toolbox for Windows

- Instalar la última versión de Minikube for Windows

### 2. Configuración
 
Para verificar el estado de minikube:

```bash
minikube status
```

Consultar versión de minikube: 

```bash
minikube version
```

Lanzar minikube 

```bash
minikube start
```

![][6]

Se puede comprobar en VirtualBox la VM corriendo

![][7]

### 3. Desplegar el proyecto.

Construir una imagen de docker desde un proyecto existente en python

```
cd Docker
```

![][1]

```
docker build -t rocco522/web .
docker push rocco522/web
```

![][2]

![][3]

Lanzar la aplicación con Docker compose
```
docker-compose up -d 
```

![][4]

Probar la aplicación
```
curl localhost:5000
```
![][5]

### 4. Correr en kubernetes

Desplegar la aplicación en Kubernetes
```bash
cd ../Kubernetes
kubectl create -f db-pod.yml
kubectl create -f db-svc.yml
kubectl create -f web-pod.yml
kubectl create -f web-svc.yml
kubectl create -f web-rc.yml
```

Verificar que los pods y los servicios fueron creados
```bash
kubectl get pods
kubectl get svc
```

Obtener el NodePort para el servicio web.
```bash
kubectl describe svc web
```

Probar la app 
```
kubectl get nodes
curl IP:PUERTO
```

[1]: Images/1.PNG
[2]: Images/4.PNG
[3]: Images/4.5.PNG
[4]: Images/5.5.PNG
[5]: Images/6.PNG
[6]: Images/7.PNG
[7]: Images/8.PNG
[8]: Images/cluster.png