# OpenIM Helm Charts

OpenIM Helm Charts simplify deployment and management of OpenIM instant messaging platform and associated middleware on Kubernetes clusters.

## Prerequisites

1. Installed and configured Kubernetes (K8s) environment.
2. Two domain names: one for MinIO API, another for OpenIM Server API.
3. Configured StorageClass (e.g., NFS-Client).
4. *(Optional)* For K8s with LoadBalancer-configured Ingress Controller nodes, no need to configure TLS items in `-config.yaml` files.
5. If you also need to open the grafana web page to view the monitoring and logging, you also need to prepare a second domain name, which can be a subdomain name. If you want to enable minio's console web access, you will also need a separate domain name, which can be a subdomain.

> **Note**: The next release will feature single domain access and IP-based URL access.
> Aliyun provides free certificate service (20), Once you've downloaded it to the server, Use:
> `kubectl create secret tls openimtls1-secret --cert=fullchain.pem --key=privkey.pem -n openim`
> you need to modify the `infra/prometheus-config.yaml` file to use the secret name `openimtls1-secret` and the domain name `openim.example.com` to access the openim server. prometheusUrl is the url accessed by the real Prometheu.


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

+ **Install**: `helm install [RELEASE_NAME] charts/openim-server`
+ **Uninstall**: `helm uninstall [RELEASE_NAME]`
+ **Upgrade**: `helm upgrade [RELEASE_NAME] [CHART] --install`
+ **List Releases**: `helm list`

*For detailed command explanations, visit Helm's official [documentation](https://helm.sh/docs/).*

## Directory Structure

+ **openim-admin**: Helm Chart for "openim-admin" service with `Chart.yaml`, `templates/`, and `values.yaml`.
+ **adminfront-config.yaml**: Configuration for "openim-admin".
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

```bash
image:
  repository: m.daocloud.io/registry.k8s.io/sig-storage/nfs-subdir-external-provisioner

nfs:
  server: YOUR_NFS_SERVER_IP
  path: YOUR_NFS_MOUNT_PATH
```

Replace `YOUR_NFS_SERVER_IP` with your internal or public IP address and `YOUR_NFS_MOUNT_PATH` with your NFS mount directory.

1. Deploy NFS using the following Helm command:

```bash
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

<!-- 安装监控 -->
## Install Prometheus and Grafana

If you need to enable monitoring, install the kube-prometheus-stack component:

```bash
helm install kube-prometheus-stack infra/kube-prometheus-stack/ -f infra/prometheus-config.yaml -n openim
```

> **Note**
> To enable monitoring you need a domain name to access grafana web pages. Please change prometheus-config.yaml to your real domain name and tls name.
> if you want prometheus pull openim-server metrics ,you need to set the two following enable: true of config-imserver.yaml
> global:
>   monitor:
>     enabled: true
> config:
>   prometheus:
>      enable: true
>
> **Note**
> Your prometheus-config.yaml file is configured with a feature to send alerts via email. 
> You just need to update it with your actual smtp_from, smtp_auth_username, smtp_auth_password, and email_configs field information.
> 
## Install loki and promtail

If you need to enable loki, install the loki-stack component:

```bash
helm install loki-stack infra/loki-stack/ -n openim
```

> **Note**
> To enable monitoring you need change loki.storageClassName to your real storageClassName.
> in this we use grafana in kube-prometheus-stack for loki display,so you should config the datasource of loki using "http://loki-stack:3100"
> 
## Install OpenIM Server Service

```bash
helm install openimserver -f k8s-open-im-server-config.yaml -f config-imserver.yaml -f notification.yaml  ./charts/openim-server/ -n openim
```

Ensure domain info in `open-im-server-config.yaml`. Sync with middleware's `-config.yaml` if changes were made during its setup.

## Install OpenIM Chat Service

```bash
helm install openimchat -f k8s-chat-server-config.yaml -f config-chatserver.yaml ./charts/openim-chat/ -n openim
```

## Install Web and Admin Frontends

+ **Web**: `helm install imwebfront -f k8s-webfront-config.yaml ./charts/openim-web/ -n openim`
+ **Admin**: `helm install imadminfront -f k8s-adminfront-config.yaml ./charts/openim-admin/ -n openim`

**Note**: Set domain details in respective `-config.yaml` files, reflecting your domain and TLS details.


## FAQ

**How to deploy multiple Kubernetes environments with namespaces**

**Specifically, why are ingress-nginx, nfs, and kube-prometheus-stack using the same configuration?**

**Answer:**

Ingress-nginx, nfs, and kube-prometheus-stack are all core Kubernetes components that are used in many different environments. It is often more efficient to use a single configuration for these components, rather than creating separate configurations for each environment.

For example, ingress-nginx is used to provide external access to services running in Kubernetes. A single ingress controller can be configured to route traffic to different services in different environments. This can save time and effort, as it eliminates the need to create and manage separate ingress controllers for each environment.

Similarly, nfs is used to provide shared storage for Kubernetes pods. A single nfs server can be configured to provide storage to pods in different environments. This can improve performance and reliability, as it eliminates the need to create and manage separate nfs servers for each environment.

Finally, kube-prometheus-stack is a collection of Prometheus and Grafana components that can be used to collect and monitor metrics from Kubernetes. A single kube-prometheus-stack can be configured to collect metrics from pods in different environments. This can provide a unified view of the health and performance of all Kubernetes environments.

**Of course, there are some cases where it may be necessary to use separate configurations for ingress-nginx, nfs, and kube-prometheus-stack. For example, if you need to have different security or performance requirements for different environments. However, in general, using a single configuration is a good way to simplify and streamline the deployment of multiple Kubernetes environments.**