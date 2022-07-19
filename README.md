![Imagen.](/image/wordpress-web.png "Imagen.")

#
# _Wordpress en Kubernetes_

### Comenzando 🚀
_Este es un simple despliegue de **wordpress** en **kubernetes** ._
_El despliegue consta de 4 archivos **.yml**._

#### _Descripción:_
- **00-namespaces.yml** Crea el namespaces para aislar el recurso.
- **01-wordpress-service.yml** Crea el servicio necesario para acceder a la aplicación.
- **02-wordpress-rc.yml** Crea el Replicaron Controller y la imagen.
- **03-wordpress-lb.yml** Crea el Load Balancer para acceder desde afuera del clúster.


# 
### Hora de meter mano 🛠️

_Clonamos el repo en el clúster._

```ssh
 git clone https://github.com/parrot26/k8s-wordpress.git
```


_Empezamos a crear los recursos aplicando los manifiestos_

```ssh
kubectl apply -f 00-namespaces.yml
```

```ssh
kubectl apply -f 01-wordpress-service.yml
```

```ssh
kubectl apply -f 02-wordpress-rc.yml
```

```ssh
kubectl apply -f 03-wordpress-lb.yml
```

### _Para acceder a la aplicación a través del Load Balancer_

_Verificamos a IP pública del Load Balancer_

```ssh
kubectl -n wordpress-test get svc
```

_Se obtiene algo parecido a esto:_

```
NAME           TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)        AGE
wordpress      NodePort       10.152.182.178   <none>           80:30000/TCP   21h
wordpress-lb   LoadBalancer   10.152.182.162   192.168.100.30   80:31398/TCP   21h
```

_Ahora podemos acceder desde un navegador remoto:_

_Según este ejemplo nuestra IP pública es **192.168.100.30**, entonces vamos al navegador web externo:_

```
http://192.168.100.30
```

### _Nota:_

_Para poder acceder remotamente vía web tiene que estar permitido el tráfico en el FW del server donde está el clúster._


# Plus:

_Sí estás utilizando **ArgoCD** en tu clúster podes aplicar este manifiesto y desplegar todo de forma automática sin tener que estar clonando el repo e ir aplicando todos los recursos de a uno_

_Creas un archivo **nombre_archivo.yml** y copias este contenido:_

```
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: wordpress-app
  namespace: argocd
spec:
  source:
    path: .
    repoURL: https://github.com/parrot26/k8s-wordpress.git
    targetRevision: HEAD
  destination:
    namespace: wordpress-test
    server: 'https://kubernetes.default.svc'
  project: default
```

_Guardas los cambios, le das permiso de ejecución al archivo y lo ejecutas con el siguiente comando:_

```
kubectl apply -f nombre_archivo.yml
```

_Listo! Después entrando a ArgoCD tenes que darle a SYNC a la aplicación_

# 
### Contribuyendo 🖇️

_Las contribuciones son lo que hacen que la comunidad de código abierto sea un lugar mejor. Cualquier contribución que hagas será muy apreciada._

_Si queres aportar con alguna sugerencia para mejorarlo, simplemente un **fork** en el repo y crear un **pull request**. También podes abrir un issue con la etiqueta **enhancement**. ¡No te olvides de sumar una estrella al repo! **¡Gracias de nuevo!**_

# 
### Autor ✒️

* **Juan Pablo Soto** - [GitHub](https://github.com/parrot26) - [Linkedin](www.linkedin.com/in/juanpablosoto26)



# 
### Expresiones de Gratitud 🎁

* Comenta a otros sobre este repo 📢
* Invita una cerveza 🍺 o un café ☕ a alguien del equipo. 
* Da las gracias públicamente 🤓.

#### _Gracias a:_

* [Kubernetes](https://kubernetes.io)
* [GitHub](https://github.com/)
* [Git](https://git-scm.com/)
* [Linkedin](https://www.linkedin.com/)
* [ArgoCD](https://argoproj.github.io/cd/)


---
⌨️ con ❤️ por [Juan Pablo Soto](https://github.com/parrot26)





