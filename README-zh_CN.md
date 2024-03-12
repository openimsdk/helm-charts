# OpenIM Helm Charts

OpenIM 的Kubernetes 系统的helm chart部署脚本，一共分三部分，一部分是基础组件(Prometheus，loki，可选部分)，一部分是应用中间件(kafka，mongodb，mysql，redis，minio)，
一部分是应用服务(openim-server,openim-chat,openim-web,openim-admin)

目前最新版本如下:
服务            chart-version    imageVersion
openim-server   0.1.2            release-v3.6
openim-chat     0.1.2            release-v1.6
openim-admin    0.1.2            toc-base-open-k8s.35
openim-web      0.1.1            preview-k8s

**关于helm chart版本管理**

+ [版本管理](./docs/contrib/version-zh.md)

## 系统要求

1. 系统环境要求
    + Kubernetes version:1.20+
    + Helm chart version:3.0+
    + Memory free size:8G+
    + Disk free size:20G+
2. Kubernetes 环境要求
    + 安装部署了StorageClass 用于持久化.在这个仓库,在 infra/nfs-subdir-external-provisioner 目录,我们提供了用NFS实现StorageClass 的简单方式.
    + 如果你有自己更专业的storageclass持久化存储实现，请替换在各chart脚本文件中的storageClass 名称.
    + 安装了Ingress-nginx-controller.如果你使用的是其他ingress-controller，请更改各chart的ingress配置.
3. 域名要求:
    + 最好有两个域名, 一个域名用于 OpenIM API, 一个域名用于 Grafana 网页访问.如果你只有一个域名或者没有域名，那么只能使用OpenIM API的功能.

> **注意**: 下个版本，我们将适配chart脚本的ingress配置适用traefik和istio.

## 文件夹结构
+ **docs/**: 用户操作文档，主要关于怎么使用grafana查看Prometheus监控和loki日志
+ **charts/**: "openim-admin","openim-chat","openim-server","openim-web"四个业务服务的helm chart脚本
+ **infra**: 中间件的helm chart脚本和config配置文件(e.g. kafka,minio,mongodb,mysql,redis;prometheus and loki 也包含在里面).
+ **config-imserver.yaml**: openim-server的配置文件,会被用于创建k8s的configmap，挂载到openim-server的容器目录中.
+ **config-chatserver.yaml**: openim-chat的配置文件,会被用于创建k8s的configmap，挂载到openim-chat的容器目录中.
+ **k8s-adminfront-config.yaml**:  openim-admin 前端服务helm chart 变量的自定义配置文件
+ **k8s-chat-server-config.yaml**:  openim-chat服务helm chart 变量的自定义配置文件
+ **k8s-open-im-server-config.yaml**: openim-server服务helm chart 变量的自定义配置文件
+ **k8s-webfront-config.yaml**: openim-web前端服务helm chart 变量的自定义配置文件


## Quick Start

### [可选]安装 prometheus

安装 kube-prometheus-stack 组件:

1. 安装kube-prometheus-stack 组件，你需要一个域名用于grafana网页访问. 请修改 prometheus-config.yaml 里面的域名信息和对应的kubernetes tls名称.
2. 用'kubectl create secret tls <yourtlsname> --cert=domain.crt --key=domain.key -n openim' 导入你域名的https文件证书创建你的域名的tls名称.
```bash
helm install kube-prometheus-stack infra/kube-prometheus-stack/ -f infra/prometheus-config.yaml -n openim
```

> **注意**
> 如果你想使用Prometheus的告警功能，请修改alertmanager.config 文件中的邮件名称和授权码成真实有效的.
>

### [可选]安装 loki

安装 loki-stack 组件:
修改 infra/loki-stack/values.yaml文件中loki.persistence.storageClassName成你k8s系统真实的storageclass.
```bash
helm install loki-stack infra/loki-stack/ -n openim
```

### [可选]安装 livekit

livekit 目前还没有集成到 helm charts 中，如果有音视频的需求，那么请你参考 livekit 的 helm charts 部署：[https://github.com/livekit/livekit-helm](https://github.com/livekit/livekit-helm)。除此之外，还需要修改对应的 [config-chatserver.yaml](config-chatserver.yaml) 中关于 livekit 的配置项。



> **注意**
> 这里我们使用的是 kube-prometheus-stack组件中的grafana，所以你应该在grafana的数据源配置loki使用url= "http://loki-stack:3100"
>

### 安装中间件

通过helm chart脚本部署中间件服务:

1. 安装im-kafka,修改 infra/kafka-config.yaml 文件中global.storageClass变量成你真实的storageClass.
```
helm install im-kafka infra/kafka -f infra/kafka-config.yaml -n openim
```

2. 安装im-mongodb,修改 infra/mongodb-config.yaml 文件中global.storageClass变量成你真实的storageClass.
```
helm install im-mongodb infra/mongodb -f infra/mongodb-config.yaml -n openim
```

3. 安装im-redis,修改 infra/redis-config.yaml 文件中global.storageClass变量成你真实的storageClass.
```
helm install im-redis infra/redis -f infra/redis-config.yaml -n openim
```

4. 安装im-minio,修改 infra/minio-config.yaml 文件中global.storageClass变量成你真实的storageClass; 并且修改域名信息成你真实的域名和tls名称.
```
helm install im-minio infra/minio -f infra/minio-config.yaml -n openim
```

## 安装OpenIM Server

1. 修改 k8s-open-im-server-config.yaml文件中的域名和tls名称成你系统真实的域名和tls名称.
2. 修改 config-imserver.yaml 文件中的对象存储配置部分的域名成你系统真实的域名:
```
   object:
   enable: "minio"
   apiURL: "https://openim1.server.top/api"# 修改openim1.server.top 成你真实的域名
   minio:
   bucket: "openim"
   endpoint: "http://im-minio:9000"
   accessKeyID: "root"
   secretAccessKey: "openIM123"
   sessionToken: ''
   signEndpoint: "https://openim1.server.top/im-minio-api" # 修改openim1.server.top 成你真实的域名
```
3. 假如你想Prometheus拉取openimserver的metrics数据你需要设置config-imserver.yaml文件中两处 enable=true
```
 global:
   monitor:
     enabled: true #set true
 config:
   prometheus:
      enable: true #set true
      prometheusUrl: "https://openim2.server.top/" # 修改openim2.server.top 成你真实的grafana域名
```
4. 安装openim-server
```bash
helm install openimserver -f k8s-open-im-server-config.yaml -f config-imserver.yaml -f notification.yaml  ./charts/openim-server/ -n openim
```

## 安装 OpenIM Chat Service
1.  修改 k8s-chat-server-config.yaml文件中的域名和tls名称成你系统真实的域名和tls名称 .
2. 安装openimchat
```bash
helm install openimchat  -f k8s-chat-server-config.yaml -f config-chatserver.yaml ./charts/openim-chat/ -n openim
```

## 安装Web Frontends
1. 修改 k8s-webfront-config.yaml文件中的域名和tls名称成你系统真实的域名和tls名称 .
2. 安装openim-web
```
helm install openim-web -f k8s-webfront-config.yaml ./charts/openim-web/ -n openim
```

## 安装Openim-admin Frontends
1. 修改 k8s-adminfront-config.yaml文件中的域名和tls名称成你系统真实的域名和tls名称 .
2. 安装openim-admin
```
helm install openim-admin -f k8s-adminfront-config.yaml ./charts/openim-admin/ -n openim
```


## 怎么使用 grafana
[docs/user-guider-zh.md](docs/contrib/user-guide-zh.md)
