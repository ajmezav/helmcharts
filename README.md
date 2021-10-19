# helmcharts
 Este repo tiene el chart para instalar un apache de prueba

 helm create apache_prueba

 helm package apache_prueba

helm repo index .

helm install --dry-run myapache apache_prueba/apache_prueba