# OpenIM Helm Charts

OpenIM Helm Charts simplify deployment and management of OpenIM instant messaging platform and associated middleware on Kubernetes clusters.

The latest version is as follows:

```bash
service         chart-version    imageVersion
openim-server   0.1.2            release-v3.6
openim-chat     0.1.2            release-v1.6
openim-admin    0.1.2            toc-base-open-k8s.35
openim-web      0.1.1            preview-k8s
```

## Prerequisites

1. System environment required
    + Kubernetes version:1.20+
    + Helm chart version:3.0+
    + Memory free size:8G+
    + Disk free size:20G+
2. Kubernetes environment required
    + installed StorageClass.in this repo,in the infra/nfs-subdir-external-provisioner fold,we provide easy StorageClass implemented by NFS.If you have your own implemented professional storageclass, please replace the storageClass variable in each chart files.
    + installed Ingress-nginx-controller.If your use other ingress controller ,you need change the ingress config in all chart files.
3. Two domain names best: It is best to prepare two domain names for the OpenIM service, one for the OpenIM API, and one for the Grafana web page. If you only have one domain name or none ,If you only have one domain name or do not have one, you can only use the Openim API function ,and cannot use the Grafana web page for prometheus and loki.

> **Note**: the next release ,we will adapt the chart's ingress configuration for traefik and istio ingress-controller.

## Directory Structure
+ **docs/**: user-guide docs,how to use grafana and loki
+ **charts/**: Helm Charts for "openim-admin","openim-chat","openim-server","openim-web"
+ **infra**: Contains Helm Charts/configurations for middleware OpenIM relies on(e.g. kafka,minio,mongodb,mysql,redis;prometheus and loki are also included).
+ **config-imserver.yaml**: openim-server's config file,Used to generate configmap for openim-server.
+ **config-chatserver.yaml**: openim-chat's config file,Used to generate configmap for openim-chat.
+ **k8s-adminfront-config.yaml**: custom values configurations for openim-admin chart
+ **k8s-chat-server-config.yaml**: custom values configurations for openim-chat chart
+ **k8s-open-im-server-config.yaml**: custom values configurations for openim-server chart
+ **k8s-webfront-config.yaml**: custom values configurations for openim-web chart

> Detailed directory info can be found in the respective directories.

## Quick Start

### [Optional]Install prometheus

If you need to enable monitoring, install the kube-prometheus-stack component:

1. To enable monitoring you need a domain name to access grafana web pages. Please change prometheus-config.yaml to your real domain name and tls name.
2. Use 'kubectl create secret tls <yourtlsname> --cert=domain.crt --key=domain.key -n openim' to create your tls name about your domain name.

```bash
helm install kube-prometheus-stack infra/kube-prometheus-stack/ -f infra/prometheus-config.yaml -n openim
```

> **Note**
> If your want prometheus alert function,you should change alertmanager.config section to your truly email information.
>

### [Optional]Install loki

If you need to enable loki, install the loki-stack component:
Change loki.persistence.storageClassName to your real storageClassName in infra/loki-stack/values.yaml.

```bash
helm install loki-stack infra/loki-stack/ -n openim
```

> **Note**
> in this we use grafana in kube-prometheus-stack for loki display,so you should config the datasource of loki using "http://loki-stack:3100"
>

### Install Middleware

Deploy required middleware services:

1. install im-mysql,change global.storageClass in infra/mysql-config.yaml to your real storageClass.

```bash
helm install im-mysql infra/mysql -f infra/mysql-config.yaml -n openim
```

2. install im-kafka,change global.storageClass in infra/kafka-config.yaml to your real storageClass.

```bash
helm install im-kafka infra/kafka -f infra/kafka-config.yaml -n openim
```

3. install im-mongodb,change global.storageClass in infra/mongodb-config.yaml to your real storageClass.

```bash
helm install im-mongodb infra/mongodb -f infra/mongodb-config.yaml -n openim
```

4. install im-redis,change global.storageClass in infra/redis-config.yaml to your real storageClass.

```bash
helm install im-redis infra/redis -f infra/redis-config.yaml -n openim
```

5. install im-minio,change global.storageClass in infra/minio-config.yaml to your real storageClass; and change domain, tls name to your real configuration.

```bash
helm install im-minio infra/minio -f infra/minio-config.yaml -n openim
```

## Install OpenIM Server

1. change domain, tls name to your real configuration in k8s-open-im-server-config.yaml.
2. change domain name to your real name in config-imserver.yaml in object configuration:

```yaml
   object:
   enable: "minio"
   apiURL: "https://openim1.server.top/api"# change openim1.server.top to your real domain name
   minio:
   bucket: "openim"
   endpoint: "http://im-minio:9000"
   accessKeyID: "root"
   secretAccessKey: "openIM123"
   sessionToken: ''
   signEndpoint: "https://openim1.server.top/im-minio-api" # change openim1.server.top to your real domain name
```

3. if you want prometheus pull openim-server metrics ,you need to set the two section enable=true in config-imserver.yaml

```yaml
 global:
   monitor:
     enabled: true #set true
 config:
   prometheus:
      enable: true #set true
      prometheusUrl: "https://openim2.server.top/" # also change openim2.server.top your real domain name for grafana website
```

4. install openim-server

```bash
helm install openimserver -f k8s-open-im-server-config.yaml -f config-imserver.yaml -f notification.yaml  ./charts/openim-server/ -n openim
```

## Install OpenIM Chat

1. change domain, tls name to your real configuration in k8s-chat-server-config.yaml.
2. install openim-chat

```bash
helm install openimchat  -f k8s-chat-server-config.yaml -f config-chatserver.yaml ./charts/openim-chat/ -n openim
```

## Install OpenIM-Web Frontends

1. change domain, tls name to your real configuration in k8s-webfront-config.yaml.
2. install openim-web

```bash
helm install openim-web -f k8s-webfront-config.yaml ./charts/openim-web/ -n openim
```

## Install Openim-admin Frontends

1. change domain, tls name to your real configuration in k8s-adminfront-config.yaml.
2. install openim-admin

```bash
helm install openim-admin -f k8s-adminfront-config.yaml ./charts/openim-admin/ -n openim
```

## How to use grafana
[docs/user-guider.md](docs/user-guide.md)
