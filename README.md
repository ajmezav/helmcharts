### Helm charts: apache prueba

Este repositorio tiene el chart para instalar un apache de prueba en un cluster de K8s, el objetivo de este ejercicio se realizó para practicar la creación de un Chart propio. Los pasos que se siguieron fueron los siguientes:
 
 * Se crea una carpeta donde se va almacenar toda la información del Chart y templates
 
 * Se crea el template de referencia con el comando: 
 
  `helm create apache_prueba`  , al hacer esto se creará la siguiente estructura: 


   ![image](https://user-images.githubusercontent.com/56460214/137990437-f85fa675-086a-4997-8982-5f231bd69491.png)

   _Para este ejemplo solo dejaremos los siguientes archivos_

   ![image](https://user-images.githubusercontent.com/56460214/137990536-00d1ad70-ba77-4b4f-9ccf-ca9e8d9c0bdb.png)



  ;Donde ___Chart.yaml___ tiene el versionamiento y descripcion de mi Chart, el archivo ___values.yaml___ los valores que quiero que sean leídos como parametros en mis   templates y que el usuario final puede modificar al instalar el Chart , la carpeta templates contiene los manifiestos que desplegará el chart en este caso es un deployment.

* Una vez se tenga los templates y Chart configurado adecuadamente se procede a crear el repositorio con el comando : 
 
`helm package apache_prueba`, esto básicamente comprimira toda la estructura que contiene la información del Chart

* Luego procedo a crear el index con siguiente comando:

`helm repo index .`

* Por último se publica el repositorio en algún website , para este caso se hace uso de _GitHub Pages_

![image](https://user-images.githubusercontent.com/56460214/137991145-cdf14975-f54b-4cd7-9f71-e949bd2e17c9.png)

### Instalar el Chart:

* Se agrega el repositorio con:

 `helm repo add apache https://ajmezav.github.io/helmcharts/`

* Se procede a probar la instalación :

 `helm install --dry-run myapache apache/apache_prueba`

* Instalación:

 `helm install myapache apache/apache_prueba`

### Hacer actualización del chart instalado

Para actualizar el Chart se debe crear de nuevo el repo o comprimir con _"helm package"_ y crear el nuevo _index_ , aparte de cambiar el versionamiento en el _Chart.yaml_ , publicar los cambios en Git y luego sí se procede a actualizar la instalación:

`helm repo update
 helm upgrade myapache apache/apache_prueba`

### Valores parametrizables en el Chart:

Se puede cambiar la cantidad de réplicas de Pods a desplegar con este chart:

`helm install  myapache apache/apache_prueba --set replica_pod=2`



