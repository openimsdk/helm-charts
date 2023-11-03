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
   + Add repository: `helm repo add openim https://openimsdk.github.io/helm-charts`
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


## Setting up ingress-nginx and NFS in Kubernetes

Before we dive into the installation steps for `ingress-nginx` and `NFS`, it's important to note that the methods provided here are basic. Depending on the complexity of your environment and requirements, you might want to explore other choices.

### 1. Installing NFS (Network File System)

NFS is widely used for sharing directories and files over the network. Here, we're focusing on the NFS Subdir External Provisioner which dynamically provisions NFS persistent volumes.

#### Method 1: Using Helm from the Official Repository

The official Helm repository contains a detailed guide on how to install the `nfs-subdir-external-provisioner`. You can access and read more about it [here](https://github.com/openimsdk/helm-charts/tree/main/infra/nfs-subdir-external-provisioner).

#### Method 2: Using the Local Repository

If you prefer to use the local repository for installation, follow these steps:

1. Update the `config.yaml` file under the directory [infra/nfs-subdir-external-provisioner](https://github.com/openimsdk/helm-charts/tree/main/infra/nfs-subdir-external-provisioner). Modify the `image` and `nfs` values:

```
image:
  repository: m.daocloud.io/registry.k8s.io/sig-storage/nfs-subdir-external-provisioner

nfs:
  server: YOUR_NFS_SERVER_IP
  path: YOUR_NFS_MOUNT_PATH
```

Replace `YOUR_NFS_SERVER_IP` with your internal or public IP address and `YOUR_NFS_MOUNT_PATH` with your NFS mount directory.

1. Deploy NFS using the following Helm command:

```
helm install nfs-subdir-external-provisioner ./infra/nfs-subdir-external-provisioner/ -f infra/nfs-subdir-external-provisioner/config.yaml -n openim
```

### 2. Installing ingress-nginx

`ingress-nginx` is an Ingress controller for Kubernetes that provides NGINX as a reverse proxy and load balancer.

#### Configuration

Update the [config.yaml](https://github.com/openimsdk/helm-charts/blob/main/infra/ingress-nginx/config.yaml) file under the directory `infra/ingress-nginx`:

```bash
controller:
  name: controller
  image:
    registry: m.daocloud.io
    image: registry.k8s.io/ingress-nginx/controller
  hostNetwork: true
  service:
    enabled: true
    type: NodePort
    nodePorts:
      http: 32080
      https: 32443
      tcp:
        8080: 32808
  admissionWebhooks:
    patch:
      enabled: true
      image:
        registry: m.daocloud.io
        image: registry.k8s.io/ingress-nginx/kube-webhook-certgen

defaultBackend:
  enabled: false
  name: defaultbackend
  image:
    registry: m.daocloud.io
    image: registry.k8s.io/defaultbackend-amd64
```

#### Installation:

Execute the following Helm command to deploy `ingress-nginx`:

```bash
helm install ingress-nginx ./infra/ingress-nginx/ -f infra/ingress-nginx/config.yaml -n openim
```

#### Detailed Explanation for ingress-nginx:

+ **controller**: Defines the main configuration for the ingress-nginx controller.
  + `name`: Name of the controller.
  + `image`: Specifies the image details for the ingress-nginx controller.
  + `hostNetwork`: If set to true, the NGINX ingress controller will use the host's network namespace, allowing it to see the real client IP.
  + `service`: Specifies the service details for exposing the ingress-nginx controller.
  + `admissionWebhooks`: Configuration for the Kubernetes admission webhooks. The patch webhook adds the certificate volume to the ingress controller pod.
+ **defaultBackend**: It is a service that handles all traffic that the ingress controller (NGINX) cannot route to an application in the cluster. In this configuration, it's disabled.

For further reading and more advanced configurations for `ingress-nginx`, you can refer to the official [ingress-nginx documentation](https://kubernetes.github.io/ingress-nginx/).

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
helm install openim-chat -f k8s-chat-server-config.yaml -f config-chatserver.yaml ./openim/openim-chat/ -n openim
```

## Install Web and Admin Frontends

+ **Web**: `helm install imwebfront -f k8s-webfront-config.yaml ./openim/webfront/ -n openim`
+ **Admin**: `helm install imadminfront -f k8s-adminfront-config.yaml ./openim/adminfront/ -n openim`

**Note**: Set domain details in respective `-config.yaml` files, reflecting your domain and TLS details.
