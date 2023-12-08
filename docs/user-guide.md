# User guide Documents

1. Using Grafana to View Openim Custom Metrics and System Performance Metrics(e.g. Node exposer) and Middleware Metrics(e.g. redis exposer,mongodb exposer)
2. Using Grafana to view logs collected by loki
## How to Open grafana website
1. through the domain name set during the installation of kube-prometheus-stack chart
2. through the openim-adminfront website
   + open adminfront website by:https://yourdomain/openim-admin-front/
   + Log in using the default username and password (admin1:admin1).
   + check the follow link,then will open grafana website.
   ![img.png](img.png)
## How to use grafana view metrics
1. log in grafana using the default username and password(admin:prom-operator)
2. The default Prometheus data source is already configured, 
   so in the second step, you only need to import the openim custom dashboard to view the openim custom metrics.
   + click the import button in follow picture
   ![img_1.png](img_1.png)
   + copy k8s-custom.yaml content to follow section,and click load button
   ![img_2.png](img_2.png)
   + select your k8s namespace ,and then you will view the openim custom metrics
   ![img_3.png](img_3.png)
3. view node metrics by the default Node exposer dashboard
   ![img_4.png](img_4.png)
   ![img_5.png](img_5.png)
## How to use grafana view logs 
1. add loki datasource
   ![img_6.png](img_6.png)
   + set loki datasource url= http://loki-stack:3100 ,and click save&test button
   ![img_7.png](img_7.png)
   
2. import log view dashboard using k8s-loki.yaml
   ![img_8.png](img_8.png)
   + then you will view the logs of openimserver
   ![img_9.png](img_9.png)




