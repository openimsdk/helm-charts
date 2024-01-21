# Admin-API Helm Chart

## Introduction

This chart bootstraps an Admin-API deployment on a Kubernetes cluster using the Helm package manager.

Admin-API is the business server component of OpenIM Chat, an open source instant messaging platform.

## Prerequisites

- Kubernetes 1.12+
- Helm 3.0+

## Installing the Chart

To install the chart with the release name `my-admin-api`:

```bash
helm repo add openim https://github.com/openimsdk/helm-charts
helm install my-admin-api openim/admin-api
```

This command deploys Admin-API on the Kubernetes cluster in the default configuration. The [Parameters](https://chat.openai.com/c/892a8ceb-729a-496a-829b-98d2d1b74cc3#parameters) section lists the parameters that can be configured during installation.

## Uninstalling the Chart

To uninstall/delete the `my-admin-api` deployment:

```bash
helm delete my-admin-api
```

This command removes all the Kubernetes components associated with the chart and deletes the release.

## Parameters

The following table lists the configurable parameters of the Admin-API chart and their default values.

| Parameter          | Description       | Default        |
| ------------------ | ----------------- | -------------- |
| `image.repository` | Image repository  | `nil`          |
| `image.tag`        | Image tag         | `nil`          |
| `image.pullPolicy` | Image pull policy | `IfNotPresent` |
| ...                | ...               | ...            |

## Configuration

Refer to [values.yaml](https://github.com/openimsdk/helm-charts/blob/main/charts/admin-api/values.yaml) for the full run-down on defaults. These are YAML files that supply values to your templates.

## Upgrading

To upgrade the chart:

```bash
helm upgrade my-admin-api openim/admin-api
```

## Additional Information

+ Learn more about OpenIM Chat: [OpenIM Chat GitHub](https://github.com/openimsdk/chat)
+ OpenIM Helm Charts: [OpenIM Helm Charts GitHub](https://github.com/openimsdk/helm-charts)

## Maintainers

+ [OpenIM](https://github.com/openimsdk)

## License

This project is licensed under the [Apache License 2.0](https://github.com/openimsdk/chat/blob/main/LICENSE).