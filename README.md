# OpenIM Helm Charts

OpenIM Helm Charts simplify deployment and management of OpenIM instant messaging platform and associated middleware on Kubernetes clusters.

## Prerequisites

1. Installed and configured Kubernetes (K8s) environment.
2. Two domain names: one for MinIO API, another for OpenIM Server API.
3. Configured StorageClass (e.g., NFS-Client).
4. *(Optional)* For K8s with LoadBalancer-configured Ingress Controller nodes, no need to configure TLS items in `-config.yaml` files.

> **Note**: The next release will feature single domain access and IP-based URL access.

## Quick Start

1. **Setup Helm**:

   + Install [Helm](https://helm.sh/).
   + Add repository: `helm repo add openim https://openim.github.io/helm-charts`
   + Search available charts: `helm search repo openim`

   > Because Github packages are OCI compliant, helm packages on GitHub do not require the `helm repo add` to add packages

2. **Install Middleware**:

   + Add repo: `helm repo add openim-infra https://xxxxx.xxx`
   + Deploy middleware services using commands in the `Install Middleware` section below.

3. **Deploy OpenIM Services**: Use commands in `Install OpenIM Server Service`, `Install OpenIM Chat Service`, `Install Web Frontend`, and `Install Admin Frontend` sections.

## Commands Overview

+ **Install**: `helm install [RELEASE_NAME] openim/openim-server`
+ **Uninstall**: `helm uninstall [RELEASE_NAME]`
+ **Upgrade**: `helm upgrade [RELEASE_NAME] [CHART] --install`
+ **List Releases**: `helm list`

*For detailed command explanations, visit Helm's official [documentation](https://helm.sh/docs/).*

## Directory Structure

+ **adminfront**: Helm Chart for "adminfront" service with `Chart.yaml`, `templates/`, and `values.yaml`.
+ **adminfront-config.yaml**: Configuration for "adminfront".
+ **chat-server**: Helm Chart for "chat-server" with associated files.
+ **infra**: Contains Helm Charts/configurations for middleware OpenIM relies on.

Detailed directory info can be found in the respective directories.

## Install Middleware

Deploy required middleware services:

```bash
helm install im-mysql infra/mysql -f infra/mysql-config.yaml -n openim
helm install im-kafka infra/kafka -f infra/kafka-config.yaml -n openim
helm install im-minio infra/minio -f infra/minio-config.yaml -n openim
helm install im-mongodb infra/mongodb -f infra/mongodb-config.yaml -n openim
helm install im-redis infra/redis -f infra/redis-config.yaml -n openim
```

> **Note**
>
> If the OpenIM cluster is deployed in the `openim` namespace, use the `-n` argument to specify the namespace. If the namespace does not exist, you can use `--create-namespace` to create a new namespace. Please do not modify the following chart names: `im-mysql`, `im-kafka`, `im-minio`, `im-mongodb`, `im-redis`, otherwise, you will need to synchronize the `serviceName` information to `config-imserver.yaml` and `config-chatserver.yaml`. Please do not modify the account information in these five configuration files, otherwise, you will need to synchronize the middleware account information to `config-imserver.yaml` and `config-chatserver.yaml`.
>
> These configuration files include account information, for example, `minio-config.yaml` also includes domain information.



## Install OpenIM Server Service

```bash
helm install openimserver -f k8s-open-im-server-config.yaml -f config-imserver.yaml -f notification.yaml  ./openim/openim-server/ -n openim
```

Ensure domain info in `open-im-server-config.yaml`. Sync with middleware's `-config.yaml` if changes were made during its setup.

## Install OpenIM Chat Service

```bash
helm install openim-chat -f k8s-chat-server-config.yaml ./openim/openim-chat/ -n openim
```

## Install Web and Admin Frontends

+ **Web**: `helm install imwebfront -f k8s-webfront-config.yaml ./openim/webfront/ -n openim`
+ **Admin**: `helm install imadminfront -f k8s-adminfront-config.yaml ./openim/adminfront/ -n openim`

**Note**: Set domain details in respective `-config.yaml` files, reflecting your domain and TLS details.
