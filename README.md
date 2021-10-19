### Helm charts: apache prueba

Este repositorio tiene el chart para instalar un apache de prueba en un cluster de K8s, el objetivo de este ejercicio se realizó para practicar la creación de un Chart propio. El deployment a usar es el mismo de este ejercicio: https://github.com/ajmezav/Cronjob-with-kubectl---restart-deployment-apache/blob/main/deployment_apache.yaml . Los pasos que se siguieron fueron los siguientes:

 * Tener instalado HELM en el equipo https://helm.sh/docs/intro/install/
 
 * Se crea una carpeta donde se va almacenar toda la información del Chart y templates
 
 * Se crea el template de referencia con el comando: 
 
  ```bash
  helm create apache_prueba 
  ```
  , al hacer esto se creará la siguiente estructura: 


   ![image](https://user-images.githubusercontent.com/56460214/137990437-f85fa675-086a-4997-8982-5f231bd69491.png)

   _Para este ejemplo solo dejaremos los siguientes archivos:_

   ![image](https://user-images.githubusercontent.com/56460214/137990536-00d1ad70-ba77-4b4f-9ccf-ca9e8d9c0bdb.png)



  ;Donde ___Chart.yaml___ tiene el versionamiento y descripción de el Chart personalizado, el archivo ___values.yaml___ contiene los valores que seran leídos como parametros en  los templates y que el usuario final puede modificar al instalar el Chart , la carpeta templates contiene los manifiestos que desplegará el chart en este caso es un deployment.

* Una vez se tenga los templates y Chart configurado adecuadamente se procede a crear el repositorio con el comando : 
 
`helm package apache_prueba`, esto básicamente comprimirá toda la estructura que contiene el repositorio Helm (Chart, values,templates ,etc)

* Luego se procede a crear el index con el siguiente comando:

`helm repo index .`

* Por último se publica el repositorio en algún website , para este caso se hace uso de _GitHub Pages ref https://pages.github.com/_ 

![image](https://user-images.githubusercontent.com/56460214/137991145-cdf14975-f54b-4cd7-9f71-e949bd2e17c9.png)

### Instalar el Chart:

* Se agrega el repositorio con:

  ```bash
  helm repo add apache https://ajmezav.github.io/helmcharts/
  helm repo update
  ```
 
* Validar que se agrego el repositorio: 

 ```bash
 helm search repo apache
 ```

* Se procede a probar la instalación :

 ```bash
 helm install --dry-run myapache apache/apache_prueba
  ```

* Instalación:

```bash
 helm install myapache apache/apache_prueba
 ```

### Hacer actualización del chart instalado

Para actualizar el Chart se debe crear de nuevo el repo o comprimir con _"helm package"_ y crear el nuevo _index_ , aparte de cambiar el versionamiento en el _Chart.yaml_ y publicar los cambios en Git , por último se procede a actualizar la instalación del Chart:

```bash
 helm repo update
 helm upgrade myapache apache/apache_prueba
 ```

### Valores parametrizables en el Chart:

Se puede cambiar la cantidad de réplicas de Pods a desplegar con este chart:

```bash
helm install  myapache apache/apache_prueba --set replica_pod=2
```

Para ver qué opciones se pueden configurar en un chart, use `helm show values apache/apache_prueba`


### Uninstall Chart

```bash 
helm uninstall myapache
```

### Listar y remover Repos de Helm

```bash
 helm repo list
 helm repo remove apache
 ```

_Ref:_ _https://helm.sh/es/docs/intro/using_helm/_
