# openim-charts

OpenIM Helm charts 用于在Kubernetes集群上部署和管理OpenIM即时消息通信平台及其依赖的中间件。

## 目录结构

### adminfront

这个目录包含了“adminfront”服务的Helm Chart。

+ `Chart.yaml`: 包含了chart的基本信息和版本。
+ `templates/`: 包含了Kubernetes的模板文件。
+ `values.yaml`: 默认的配置文件。

### adminfront-config.yaml

包含了“adminfront”服务的自定义配置信息。

### chat-server

这个目录包含了“chat-server”服务的Helm Chart。

+ `Chart.yaml`: 包含了chart的基本信息和版本。
+ `charts/`: (可选) 如果chart依赖其他chart，可以将它们放在这个目录下。
+ `templates/`: 包含了Kubernetes的模板文件。
+ `values.yaml`: 默认的配置文件。

### chat-server-config.yaml

包含了“chat-server”服务的自定义配置信息。

### infra

这个目录包含了OpenIM依赖的所有中间件的Helm charts或者相关的配置。

+ `ingress-nginx`, `kafka`, `minio`, `mongodb`, `mysql`, `nfs-subdir-external-provisioner`, `redis`: 这些目录可能包含了对应中间件的Helm charts。
+ `kafka-config.yaml`, `minio-config.yaml`, `mongodb-config.yaml`, `mysql-config.yaml`, `redis-config.yaml`: 这些文件包含了对应中间件的自定义配置。

### notification.yaml

可能包含了与通知或者消息传递有关的配置。

### open-im-server

这个目录包含了“open-im-server”服务的Helm Chart。

+ `Chart.yaml`: 包含了chart的基本信息和版本。
+ `charts/`: (可选) 如果chart依赖其他chart，可以将它们放在这个目录下。
+ `templates/`: 包含了Kubernetes的模板文件。
+ `values.yaml`: 默认的配置文件。

### open-im-server-config.yaml

包含了“open-im-server”服务的自定义配置信息。

### webfront

这个目录包含了“webfront”服务的Helm Chart。

+ `Chart.yaml`: 包含了chart的基本信息和版本。
+ `templates/`: 包含了Kubernetes的模板文件。
+ `values.yaml`: 默认的配置文件。

### webfront-config.yaml

包含了“webfront”服务的自定义配置信息。


## 前提条件

+ 已经安装并配置好的Kubernetes（k8s）环境。
+ 至少有两个可用的域名：一个用于MinIO API访问，另一个用于OpenIM Server API访问。
+ 已配置的storageclass（此示例使用nfs-client）。
+ （可选）如果您的k8s系统的ingress-control节点配置了loadbalance，所有*-config.yaml的域名信息不需要配置TLS项。

> 注：下个版本将推出基于单一域名访问和基于IP的URL访问功能。

## 安装中间件

在部署OpenIM服务之前，我们需要部署一些依赖的中间件服务。下面的命令分别安装了MySQL, Kafka, MinIO, MongoDB, 和Redis中间件。

```bash
helm repo add im-infra https://xxxxx.xxx
helm install im-mysql im-infra/mysql -f mysql-config.yaml
helm install im-kafka im-infra/kafka -f kafka-config.yaml
helm install im-minio im-infra/minio -f minio-config.yaml
helm install im-mongodb im-infra/mongodb -f mongodb-config.yaml
helm install im-redis im-infra/redis -f redis-config.yaml
```

说明：这些配置文件包括了账户信息，例如，`minio-config.yaml`还包括了域名信息。

## 安装openimserver服务

```bash
helm install openimserver -f open-im-server-config.yaml -f notification.yaml ./open-im-server/
```

说明：您需要在`open-im-server-config.yaml`中配置域名信息。账户信息默认与中间件的*-config.yaml同步。如果在安装中间件时修改了`config.yaml`，请同步修改`open-im-server-config.yaml`。

## 安装openimchat服务

```bash
helm install openimchat -f chat-server-config.yaml ./chat-server/
```

说明：您需要在`chat-server-config.yaml`中配置域名信息。账户信息默认与中间件的 `*-config.yaml` 同步。如果在安装中间件时修改了`config.yaml`，请同步修改`chat-server-config.yaml`。

## 安装webfront

```bash
helm install imwebfront -f webfront-config.yaml ./webfront/
```

说明：在`webfront-config.yaml`中，请确保配置了域名信息。

## 安装adminfront

```bash
helm install imadminfront -f adminfront-config.yaml ./adminfront/
```

说明：在`adminfront-config.yaml`中，请确保配置了域名信息。

## 卸载方法

如果你需要卸载OpenIM及其相关组件，可以使用以下Helm命令进行卸载：

```bash
helm uninstall [RELEASE_NAME]
```

其中`[RELEASE_NAME]`是你在安装时指定的名字，例如`openimserver`。

## 更多信息

欲了解更多关于OpenIM和各个组件的配置和使用信息，请访问[OpenIM官方文档](https://docs.openim.io/)。
