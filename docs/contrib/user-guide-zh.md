# 用户操作 Documents

1. 本文档教你怎么使用Grafana查看Prometheus的监控指标包括openimserver的自定义指标和物理节点node的指标，中间件的性能指标。
2. 本文档教你怎么使用grafana查看loki收集的服务日志
## 怎么访问 grafana 网页
1. 通过安装kube-prometheus-stack 组件时候配置的域名访问
2. 通过openim管理后台网页的链接入口访问
   + openim管理后台网页地址:https://yourdomain/openim-admin-front/
   + 管理后台默认用户名和密码 (admin1:admin1).
   + 点击下图链接，将打开grafana网页.
     ![../images/img.png](../images/img.png)
## 怎么使用grafana查看监控指标
1. 登入grafana使用默认用户名和密码(admin:prom-operator)
2. 默认情况下Prometheus的数据源已经配置好的,
   你只需要导入自定义的openim的dashboard仪表盘就你查看openimserver的自定义指标.
   + 点击下图的import按钮
     ![../images/$&)
     +拷贝 k8s-custom.yaml 到下图区域,接着点击load按钮
     ![../images/$&)
   + 选择你的 k8s namespace ,截止你将要查看到自定义指标信息
     ![../images/$&)
3. 使用 Node exposer dashboard仪表盘查看物理节点信息
   ![../images/$&)
   ![../images/$&)
## 使用grafana查看loki收集的日志
1. 增加loki数据源
   ![../images/$&)
   + 设置loki datasource url= http://loki-stack:3100 ,and click save&test button
     ![../images/$&)

2. 使用 k8s-loki.yaml导入日志仪表盘
   ![../images/$&)
   + 接着你将要看到 openimserver的日志
     ![../images/$&)