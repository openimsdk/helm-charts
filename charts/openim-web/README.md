# OpenIM-Web Helm Chart

## Introduction

This chart deploys OpenIM-Web on a Kubernetes cluster using the Helm package manager. OpenIM-Web is the front-end web chat component of OpenIM, providing a user interface for real-time messaging.

## Prerequisites

- Kubernetes 1.12+
- Helm 3.0+

## Installing the Chart

To install the chart with the release name `my-openim-web`:

```bash
helm repo add openim https://github.com/openimsdk/helm-charts
helm install my-openim-web openim/openim-web
```

This command deploys OpenIM-Web on the Kubernetes cluster in the default configuration. The [Parameters](https://chat.openai.com/c/892a8ceb-729a-496a-829b-98d2d1b74cc3#parameters) section lists the parameters that can be configured during installation.

## Uninstalling the Chart

To uninstall/delete the `my-openim-web` deployment:

```bash
helm delete my-openim-web
```

This command removes all the Kubernetes components associated with the chart and deletes the release.

## Parameters

The following table lists the configurable parameters of the OpenIM-Web chart and their default values.

| Parameter          | Description       | Default        |
| ------------------ | ----------------- | -------------- |
| `image.repository` | Image repository  | `nil`          |
| `image.tag`        | Image tag         | `nil`          |
| `image.pullPolicy` | Image pull policy | `IfNotPresent` |
| ...                | ...               | ...            |

## Configuration

Refer to the [values.yaml](https://github.com/openimsdk/helm-charts/blob/main/charts/openim-web/values.yaml) for a comprehensive rundown on defaults. These YAML files supply values to your templates.

## Upgrading

To upgrade the chart:

```bash
helm upgrade my-openim-web openim/openim-web
```

## Additional Information

+ Learn more about OpenIM: [OpenIM GitHub](https://github.com/openimsdk/open-im-server)
+ OpenIM Helm Charts repository: [OpenIM Helm Charts](https://github.com/openimsdk/helm-charts)

## Maintainers

+ [OpenIM](https://github.com/openimsdk)

## License

This project is licensed under the [Apache License 2.0](https://github.com/openimsdk/open-im-server/blob/main/LICENSE).