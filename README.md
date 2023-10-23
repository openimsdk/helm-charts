

# Response and Translation into English:

## OpenIM Helm Charts

OpenIM Helm Charts are utilized for easy deployment and management of the OpenIM instant messaging platform and its related middleware on Kubernetes clusters.

## Prerequisites

+ Installed and configured Kubernetes (K8s) environment.
+ At least two available domain names: one for MinIO API access, and another for OpenIM Server API access.
+ Configured StorageClass (this example uses NFS-Client).
+ (Optional) If your K8s system’s Ingress Controller nodes are configured with LoadBalancer, all domain information in `-config.yaml` files do not need to configure TLS items.

> **Note**: The next version will introduce single domain access and IP-based URL access features.

## User Guide

To use these Helm Charts, you first need to install [Helm](https://helm.sh/). Please refer to Helm's [documentation](https://helm.sh/docs/) to get started with Helm.

Once Helm is installed, add the Helm repository as follows:

```
helm repo add openim https://openim.github.io/helm-charts
```

Next, you can run `helm search repo openim` to view the available Charts.

### Install Chart

```
helm install [RELEASE_NAME] openim/openim-server
```

*See the [configuration](https://github.com/openim/helm-charts/tree/main/charts/) information below.*

*For command documentation, refer to [helm install](https://helm.sh/docs/helm/helm_install/).*

### Uninstall Chart

```
helm uninstall [RELEASE_NAME]
```

This will delete all Kubernetes components related to the Chart and uninstall the release.

*For command documentation, refer to [helm uninstall](https://helm.sh/docs/helm/helm_uninstall/).*

### Upgrade Chart

```
helm upgrade [RELEASE_NAME] [CHART] --install
```

*For command documentation, refer to [helm upgrade](https://helm.sh/docs/helm/helm_upgrade/).*

### List Releases

```bash
helm list
```

## Directory Structure

### adminfront

This directory contains the Helm Chart for the "adminfront" service.

+ `Chart.yaml`: Contains basic information and version of the Chart.
+ `templates/`: Contains Kubernetes template files.
+ `values.yaml`: Default configuration file.

### adminfront-config.yaml

Contains custom configuration information for the "adminfront" service.

### chat-server

This directory contains the Helm Chart for the "chat-server" service.

+ `Chart.yaml`: Contains basic information and version of the Chart.
+ `charts/`: (Optional) If the Chart depends on other Charts, they can be placed in this directory.
+ `templates/`: Contains Kubernetes template files.
+ `values.yaml`: Default configuration file.

### infra

This directory contains all Helm Charts or related configurations for the middleware that OpenIM depends on.

+ `ingress-nginx`, `kafka`, `minio`, `mongodb`, `mysql`, `nfs-subdir-external-provisioner`, `redis`: These directories may contain Helm Charts for the corresponding middleware.
+ `kafka-config.yaml`, `minio-config.yaml`, `mongodb-config.yaml`, `mysql-config.yaml`, `redis-config.yaml`: These files contain custom configurations for the corresponding middleware.

## Prerequisites

+ Installed and configured Kubernetes (K8s) environment.
+ At least two available domain names: one for MinIO API access, and another for OpenIM Server API access.
+ Configured StorageClass (this example uses NFS-Client).
+ (Optional) If your K8s system’s Ingress Controller nodes are configured with LoadBalancer, all domain information in `-config.yaml` files do not need to configure TLS items.

> Note: The next version will introduce single domain access and IP-based URL access features.

## Install Middleware

Before deploying the OpenIM services, we need to deploy some dependent middleware services.

For easy deployment and management, we provide a set of Helm Charts for these middleware, located in the infra directory.

The following commands will respectively install MySQL, Kafka, MinIO, MongoDB, and Redis middleware:

```bash
helm repo add openim-infra https://xxxxx.xxx
helm install im-mysql im-infra/mysql -f mysql-config.yaml
helm install im-kafka im-infra/kafka -f kafka-config.yaml
helm install im-minio im-infra/minio -f minio-config.yaml
helm install im-mongodb im-infra/mongodb -f mongodb-config.yaml
helm install im-redis im-infra/redis -f redis-config.yaml
```

> **Note**
>
> If the OpenIM cluster is deployed in the `openim` namespace, use the `-n` argument to specify the namespace. If the namespace does not exist, you can use `--create-namespace` to create a new namespace.

These configuration files include account information, for example, `minio-config.yaml` also includes domain information.

## Install OpenIM Server Service

```bash
helm install openim-server -f open-im-server-config.yaml -f notification.yaml ./openim/open-im-server/
```

Ensure that the domain information is configured in `open-im-server-config.yaml`. Account information defaults to sync with the middleware (`infra/`) `-config.yaml` files. If `config.yaml` was modified when installing the middleware, please sync modify `open-im-server-config.yaml`.

## Install OpenIM Chat Service

```bash
helm install openim-chat -f chat-server-config.yaml ./openim/openim-chat
```

Ensure that the domain information is configured in `chat-server-config.yaml`. Account information defaults to sync with the middleware `-config.yaml` files. If `config.yaml` was modified when installing the middleware, please sync modify `chat-server-config.yaml`.