# prometheus-windows-exporter

![Version: 0.1.1](https://img.shields.io/badge/Version-0.1.1-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 0.22.0](https://img.shields.io/badge/AppVersion-0.22.0-informational?style=flat-square)

A Helm chart for prometheus windows-exporter

**Homepage:** <https://github.com/prometheus-community/windows_exporter/>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| jkroepke | <github@jkroepke.de> |  |

## Source Code

* <https://github.com/prometheus-community/windows_exporter/>

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| config | string | `"collectors:\n  enabled: '[defaults],container'"` |  |
| configmaps | list | `[]` |  |
| containerSecurityContext | object | `{}` |  |
| daemonsetAnnotations | object | `{}` |  |
| dnsConfig | object | `{}` |  |
| env | object | `{}` |  |
| extraArgs | list | `[]` |  |
| extraHostVolumeMounts | list | `[]` |  |
| extraInitContainers | list | `[]` |  |
| fullnameOverride | string | `""` |  |
| global.imagePullSecrets | list | `[]` |  |
| global.imageRegistry | string | `""` |  |
| hostNetwork | bool | `true` |  |
| hostPID | bool | `true` |  |
| image.digest | string | `""` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.registry | string | `"ghcr.io"` |  |
| image.repository | string | `"prometheus-community/windows-exporter"` |  |
| image.tag | string | `""` |  |
| imagePullSecrets | list | `[]` |  |
| livenessProbe.failureThreshold | int | `3` |  |
| livenessProbe.httpGet.httpHeaders | list | `[]` |  |
| livenessProbe.httpGet.scheme | string | `"http"` |  |
| livenessProbe.initialDelaySeconds | int | `0` |  |
| livenessProbe.periodSeconds | int | `10` |  |
| livenessProbe.successThreshold | int | `1` |  |
| livenessProbe.timeoutSeconds | int | `1` |  |
| nameOverride | string | `""` |  |
| namespaceOverride | string | `""` |  |
| nodeSelector."kubernetes.io/os" | string | `"windows"` |  |
| podAnnotations."cluster-autoscaler.kubernetes.io/safe-to-evict" | string | `"true"` |  |
| podLabels | object | `{}` |  |
| prometheus.monitor.additionalLabels | object | `{}` |  |
| prometheus.monitor.apiVersion | string | `""` |  |
| prometheus.monitor.attachMetadata.node | bool | `false` |  |
| prometheus.monitor.basicAuth | object | `{}` |  |
| prometheus.monitor.bearerTokenFile | string | `nil` |  |
| prometheus.monitor.enabled | bool | `false` |  |
| prometheus.monitor.interval | string | `""` |  |
| prometheus.monitor.jobLabel | string | `""` |  |
| prometheus.monitor.labelLimit | int | `0` |  |
| prometheus.monitor.labelNameLengthLimit | int | `0` |  |
| prometheus.monitor.labelValueLengthLimit | int | `0` |  |
| prometheus.monitor.metricRelabelings | list | `[]` |  |
| prometheus.monitor.namespace | string | `""` |  |
| prometheus.monitor.podTargetLabels | list | `[]` |  |
| prometheus.monitor.proxyUrl | string | `""` |  |
| prometheus.monitor.relabelings | list | `[]` |  |
| prometheus.monitor.sampleLimit | int | `0` |  |
| prometheus.monitor.scheme | string | `"http"` |  |
| prometheus.monitor.scrapeTimeout | string | `"10s"` |  |
| prometheus.monitor.selectorOverride | object | `{}` |  |
| prometheus.monitor.targetLimit | int | `0` |  |
| prometheus.monitor.tlsConfig | object | `{}` |  |
| prometheus.podMonitor.additionalLabels | object | `{}` |  |
| prometheus.podMonitor.apiVersion | string | `""` |  |
| prometheus.podMonitor.attachMetadata.node | bool | `false` |  |
| prometheus.podMonitor.authorization | object | `{}` |  |
| prometheus.podMonitor.basicAuth | object | `{}` |  |
| prometheus.podMonitor.bearerTokenSecret | object | `{}` |  |
| prometheus.podMonitor.enableHttp2 | string | `""` |  |
| prometheus.podMonitor.enabled | bool | `false` |  |
| prometheus.podMonitor.filterRunning | string | `""` |  |
| prometheus.podMonitor.followRedirects | string | `""` |  |
| prometheus.podMonitor.honorLabels | bool | `true` |  |
| prometheus.podMonitor.honorTimestamps | bool | `true` |  |
| prometheus.podMonitor.interval | string | `""` |  |
| prometheus.podMonitor.jobLabel | string | `""` |  |
| prometheus.podMonitor.labelLimit | int | `0` |  |
| prometheus.podMonitor.labelNameLengthLimit | int | `0` |  |
| prometheus.podMonitor.labelValueLengthLimit | int | `0` |  |
| prometheus.podMonitor.metricRelabelings | list | `[]` |  |
| prometheus.podMonitor.namespace | string | `""` |  |
| prometheus.podMonitor.oauth2 | object | `{}` |  |
| prometheus.podMonitor.params | object | `{}` |  |
| prometheus.podMonitor.path | string | `"/metrics"` |  |
| prometheus.podMonitor.podTargetLabels | list | `[]` |  |
| prometheus.podMonitor.proxyUrl | string | `""` |  |
| prometheus.podMonitor.relabelings | list | `[]` |  |
| prometheus.podMonitor.sampleLimit | int | `0` |  |
| prometheus.podMonitor.scheme | string | `"http"` |  |
| prometheus.podMonitor.scrapeTimeout | string | `""` |  |
| prometheus.podMonitor.selectorOverride | object | `{}` |  |
| prometheus.podMonitor.targetLimit | int | `0` |  |
| prometheus.podMonitor.tlsConfig | object | `{}` |  |
| rbac.create | bool | `true` |  |
| readinessProbe.failureThreshold | int | `3` |  |
| readinessProbe.httpGet.httpHeaders | list | `[]` |  |
| readinessProbe.httpGet.scheme | string | `"http"` |  |
| readinessProbe.initialDelaySeconds | int | `0` |  |
| readinessProbe.periodSeconds | int | `10` |  |
| readinessProbe.successThreshold | int | `1` |  |
| readinessProbe.timeoutSeconds | int | `1` |  |
| releaseLabel | bool | `false` |  |
| resources | object | `{}` |  |
| secrets | list | `[]` |  |
| securityContext.windowsOptions.hostProcess | bool | `true` |  |
| securityContext.windowsOptions.runAsUserName | string | `"NT AUTHORITY\\system"` |  |
| service.annotations | object | `{}` |  |
| service.nodePort | string | `nil` |  |
| service.port | int | `9182` |  |
| service.portName | string | `"metrics"` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.automountServiceAccountToken | bool | `false` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.imagePullSecrets | list | `[]` |  |
| serviceAccount.name | string | `nil` |  |
| sidecarHostVolumeMounts | list | `[]` |  |
| sidecarVolumeMount | list | `[]` |  |
| sidecars | list | `[]` |  |
| tolerations[0].effect | string | `"NoSchedule"` |  |
| tolerations[0].operator | string | `"Exists"` |  |
| updateStrategy.rollingUpdate.maxUnavailable | int | `1` |  |
| updateStrategy.type | string | `"RollingUpdate"` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.9.1](https://github.com/norwoodj/helm-docs/releases/v1.9.1)
