# OpenIM Helm Charts

!!! 中文文档可能不是最新的，请参考 [英文文档](./README.md)。

OpenIM Helm Charts 用于在 Kubernetes 集群上轻松部署和管理 OpenIM 即时消息通信平台及其相关中间件。

## 用户指南

要使用这些 Helm Charts，您需要先安装 [Helm](https://helm.sh/)。请参考 Helm 的 [文档](https://helm.sh/docs/) 来开始使用 Helm。

一旦 Helm 安装完毕，请按如下方式添加 Helm 仓库：

```
helm repo add openim https://openim.github.io/helm-charts
```

接下来，您可以运行 `helm search repo openim` 来查看可用的 Charts。

### 安装 Chart

```bash
helm install [RELEASE_NAME] openim-server
```

*查看下面的[配置](https://github.com/helm-charts/tree/main/charts/)信息。*

*有关命令文档，请参考 [helm install](https://helm.sh/docs/helm/helm_install/)。*

### 卸载 Chart

```bash
helm uninstall [RELEASE_NAME]
```

这将删除与 Chart 相关的所有 Kubernetes 组件并卸载发布。

*有关命令文档，请参考 [helm uninstall](https://helm.sh/docs/helm/helm_uninstall/)。*

### 升级 Chart

```bash
helm upgrade [RELEASE_NAME] [CHART] --install
```

*有关命令文档，请参考 [helm upgrade](https://helm.sh/docs/helm/helm_upgrade/)。*

### 列出发布

```bash
helm list
```

## 目录结构

### openim-admin

这个目录包含了 "openim-admin" 服务的 Helm Chart。

+ `Chart.yaml`: 包含了 Chart 的基本信息和版本。
+ `templates/`: 包含了 Kubernetes 模板文件。
+ `values.yaml`: 默认配置文件。

### adminfront-config.yaml

包含了 "openim-admin" 服务的自定义配置信息。

### chat-server

这个目录包含了 "chat-server" 服务的 Helm Chart。

+ `Chart.yaml`: 包含了 Chart 的基本信息和版本。
+ `charts/`: (可选) 如果 Chart 依赖其他 Chart，可以将它们放在这个目录下。
+ `templates/`: 包含了 Kubernetes 模板文件。
+ `values.yaml`: 默认配置文件。

### infra

这个目录包含了 OpenIM 所依赖的所有中间件的 Helm Charts 或相关配置。

+ `ingress-nginx`, `kafka`, `minio`, `mongodb`, `mysql`, `nfs-subdir-external-provisioner`, `redis`: 这些目录可能包含了对应中间件的 Helm Charts。
+ `kafka-config.yaml`, `minio-config.yaml`, `mongodb-config.yaml`, `mysql-config.yaml`, `redis-config.yaml`: 这些文件包含了对应中间件的自定义配置。

## 前提条件

+ 已安装并配置好的 Kubernetes（K8s）环境。
+ 至少有两个可用的域名：一个用于 MinIO API 访问，另一个用于 OpenIM Server API 访问。
+ 已配置的 StorageClass（此示例使用 NFS-Client）。
+ （可选）如果您的 K8s 系统的 Ingress Controller 节点配置了 LoadBalancer，所有 `-config.yaml` 文件中的域名信息无需配置 TLS 项。

> 注意：下个版本将推出基于单一域名访问和基于 IP 的 URL 访问功能。

## 安装中间件

在部署 OpenIM 服务之前，我们需要部署一些依赖的中间件服务。

为了方便部署和管理，我们为这些中间件提供了一套 Helm Charts，它们位于 infra 目录下。

以下命令将分别安装 MySQL、Kafka、MinIO、MongoDB 和 Redis 中间件：

```bash
helm repo add openim-infra https://xxxxx.xxx
helm install openim-mysql infra/mysql -f infra/mysql-config.yaml
helm install openim-kafka infra/kafka -f infra/kafka-config.yaml
helm install openim-minio infra/minio -f infra/minio-config.yaml
helm install openim-mongodb infra/mongodb -f infra/mongodb-config.yaml
helm install openim-redis infra/redis -f infra/redis-config.yaml
```

> **注意**
>
> 如果 OpenIM 集群部署在 `openim` 命名空间中，则需要使用 `-n` 参数指定命名空间。如果命名空间不存在，可以使用 `--create-namespace` 创建一个新的命名空间。
> 如果要使用 GitHub Container Registry 中的 Helm chart，您通常不需要使用 helm repo add 命令添加仓库，因为 GitHub Container Registry 不是标准的 Helm 仓库类型。

这些配置文件包括账户信息，例如 `minio-config.yaml` 还包括域名信息。

## 安装 OpenIM Server 服务

```bash
helm install openim-server -f open-im-server-config.yaml -f notification.yaml ./open-im-server/
```

请确保在 `open-im-server-config.yaml` 中配置域名信息。账户信息默认与中间件（infra/）的 `-config.yaml` 文件同步。如果在安装中间件时修改了 `config.yaml`，请同步修改 `open-im-server-config.yaml`。

## 安装 OpenIM Chat 服务

```bash
helm install openim-chat -f chat-server-config.yaml ./openim-chat
```

请确保在 `chat-server-config.yaml` 中配置域名信息。账户信息默认与中间件的 `-config.yaml` 文件同步。如果在安装中间件时修改了 `config.yaml`，请同步修改 `chat-server-config.yaml`。

## 安装 Webfront

```bash
helm install imwebfront -f webfront-config.yaml ./openim-web/
```

请确保在 `webfront-config.yaml` 中配置了域名信息。


## 安装 Adminfront

```bash
helm install imadminfront -f adminfront-config.yaml ./openim-admin/
```

请确保在 `adminfront-config.yaml` 中配置了域名信息。

## 卸载方法

如果您需要卸载 OpenIM 及其相关组件，可以使用以下 Helm 命令：

```bash
helm uninstall [RELEASE_NAME]
```

其中 `[RELEASE_NAME]` 是您在安装时指定的名称，例如 `openimserver`。

## 调试 Helm Charts

如果您需要调试 Helm Charts，可以使用以下命令：

```bash
helm install [RELEASE_NAME] [CHART] --dry-run --debug
```

或者使用 `helm template` 命令：

```bash
helm template [CHART] --name [RELEASE_NAME] --debug
```

## 更多信息

要了解有关 OpenIM 和各个组件的配置和使用的详细信息，请访问[OpenIM官方文档](https://docs.openim.io/)。