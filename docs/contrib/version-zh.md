# OpenIM Helm 图表的高级版本管理

OpenIM Helm 图表采用了一套复杂的版本管理系统，涵盖了多种图表，如 `openim-server`、`openim-chat`、`openim-web` 和 `openim-admin`。这一系统虽然复杂，但确保了图表部署和维护的流畅和高效。

## 版本控制的独特方法

不同于传统软件版本控制常依赖的分支概念，OpenIM 的 Helm 图表使用基于标签的系统。这种方法简化了版本管理流程，如下：

- **Chart.yaml 文件**：每个图表目录中都包含一个 `Chart.yaml` 文件，这个文件对于管理每个单独图表的版本至关重要。它包含了 `version` 键，每个新版本发布时都会更新此键。

```yaml
version: 0.1.17
```

- **自动化 CICD**：开发者不需要手动管理分支、标签或发布。这些方面都通过连续集成和连续部署（CICD）系统自动处理。当一个新的图表版本推送到仓库时，就会触发 CICD 流水线。

- **标签和发布**：CICD 系统自动构建新版本并将其发布到 Helm 仓库。它还会标记发布，例如，`openim-admin-0.1.2`。标签结构被精心设计，以便于导航和版本跟踪。

> 标签命名规范：**v1.0.0-k8s** 对比 **k8s-v1.0.0**

1. **v1.0.0-k8s**：此格式遵循传统的版本系统（主要.次要.补丁）并添加了一个分支特定的标识符，便于通过版本号识别和排序。
   
2. **k8s-v1.0.0**：这里，分支标识符位于版本号之前。这对于拥有多个分支的仓库特别有用，因为它允许快速区分分支特定的构建。

**统一策略**：

- 对于需要多种版本策略的单分支仓库，如 helm-charts，**k8s-v1.0.0** 更为方便和可辨识。
- 对于多分支场景，如 `openim-web` 和 `openim-admin`，需要本地标签，**v1.0.0-k8s** 更适合。它有助于更好的版本控制，并在管理相关的镜像和发布时提供帮助。

## 发布流程和安装

标签完成后，CICD 自动化处理发布流程。例如，可以本地下载和提取如 `https://github.com/openimsdk/helm-charts/releases/tag/openim-admin-0.1.2` 的发布：

```bash
tar -zxvf openim-admin-0.1.2.tgz
```

细节：

```bash
openim-admin# tree 
.
├── Chart.yaml
├── README.md.gotmpl
├── templates
│   ├── deployment.yaml
│   ├── _helpers.tpl
│   ├── hpa.yaml
│   ├── ingress.yaml
│   ├── NOTES.txt
│   ├── serviceaccount.yaml
│   ├── service.yaml
│   └── tests
│       └── test-connection.yaml
└── values.yaml
```

这种提取揭示了一个可以使用 Helm 部署的结构化目录：

```bash
helm install openim-admin ./openim-admin
```

## 网络接口和仓库集成

CICD 还自动化部署了网络接口，如 `https://openimsdk.github.io/helm-charts/`。用户可以使用以下命令添加 OpenIM Helm 仓库：

```bash
helm repo add openim https://openimsdk.github.io/helm-charts/
```

然后搜索可用的

 OpenIM 图表：

```bash
helm search repo openim
```