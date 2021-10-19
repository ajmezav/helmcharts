# helmcharts
 Este repo tiene el chart para instalar un apache de prueba

 helm create apache_prueba

 helm package apache_prueba

helm repo index .
Probar antes de instalar:
helm install --dry-run myapache apache_prueba/apache_prueba
Instalar:
helm install --dry-run myapache apache_prueba/apache_prueba
Hacer actualización del chart instalado
helm upgrade myapache apache_prueba/apache_prueba

Cuando se hace una actualización en el chart no olvidar:

crear de nuevo el repo o comprimir con "helm package" y crear el nuevo index , aparte de cambiar el versionamiento en el Chart.yaml