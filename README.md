## Helm charts apache prueba

 Este repo tiene el chart para instalar un apache de prueba en un cluster de K8s, el objetivo de este ejercicio se realizo para practicar la creación un Chart propio. Los pasos que se siguieron fueron los siguientes:
 
 * Se crea una carpeta donde se va almacenar toda la información del Chart y templates
 * Se crea el template de referencia con el comando: helm create apache_prueba , al hacer esto se creara la siguiente estructura:

❯ tree prueba

prueba
├── Chart.yaml
├── charts
├── templates
│   ├── NOTES.txt
│   ├── _helpers.tpl
│   ├── deployment.yaml
│   ├── hpa.yaml
│   ├── ingress.yaml
│   ├── service.yaml
│   ├── serviceaccount.yaml
│   └── tests
│       └── test-connection.yaml
└── values.yaml

Para este ejemplo solo dejaremos los siguientes archivos ❯ tree apache_prueba
apache_prueba
├── Chart.yaml
├── charts
├── templates
│   ├── NOTES.txt
│   ├── _helpers.tpl
│   └── deployment.yaml
└── values.yaml


donde Chart.yaml tiene el versionamient y descripcion de mi Chart, el archivo values.yaml los valores que quiero que sean leidos como parametros en mis templates y que el usuario final puede modificar al instalar el Chart , la carpeta templates contiene los manifiestos que desplegará el chart en este caso es un deployment.

* Una ves tenga mis templates y Chart configurado adecuadamente procedo a crear el repositorio: helm package apache_prueba,esto basicamente comprimira toda la estrucura que contiene la información del Chart
* Luego procedo a crear el index con siguiente comando:

helm repo index .
Probar antes de instalar:
helm install --dry-run myapache apache_prueba/apache_prueba
Instalar:
helm install --dry-run myapache apache_prueba/apache_prueba
Hacer actualización del chart instalado
helm upgrade myapache apache_prueba/apache_prueba

Cuando se hace una actualización en el chart no olvidar:

crear de nuevo el repo o comprimir con "helm package" y crear el nuevo index , aparte de cambiar el versionamiento en el Chart.yaml

helm repo update

helm search repo apache

helm repo add apache https://ajmezav.github.io/helmcharts/

helm upgrade  myapache apache/apache_prueba --set replica_pod=2
helm install 
