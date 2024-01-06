# loki

![Version: 2.16.0](https://img.shields.io/badge/Version-2.16.0-informational?style=flat-square) ![AppVersion: v2.6.1](https://img.shields.io/badge/AppVersion-v2.6.1-informational?style=flat-square)

Loki: like Prometheus, but for logs.

**Homepage:** <https://grafana.com/loki>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| Loki Maintainers | <lokiproject@googlegroups.com> |  |

## Source Code

* <https://github.com/grafana/loki>

## Requirements

Kubernetes: `^1.10.0-0`

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| alerting_groups | list | `[]` |  |
| annotations | object | `{}` |  |
| client | object | `{}` |  |
| config.auth_enabled | bool | `false` |  |
| config.chunk_store_config.max_look_back_period | string | `"0s"` |  |
| config.compactor.shared_store | string | `"filesystem"` |  |
| config.compactor.working_directory | string | `"/data/loki/boltdb-shipper-compactor"` |  |
| config.ingester.chunk_block_size | int | `262144` |  |
| config.ingester.chunk_idle_period | string | `"3m"` |  |
| config.ingester.chunk_retain_period | string | `"1m"` |  |
| config.ingester.lifecycler.ring.replication_factor | int | `1` |  |
| config.ingester.max_transfer_retries | int | `0` |  |
| config.ingester.wal.dir | string | `"/data/loki/wal"` |  |
| config.limits_config.enforce_metric_name | bool | `false` |  |
| config.limits_config.max_entries_limit_per_query | int | `5000` |  |
| config.limits_config.reject_old_samples | bool | `true` |  |
| config.limits_config.reject_old_samples_max_age | string | `"168h"` |  |
| config.memberlist.join_members[0] | string | `"{{ include \"loki.fullname\" . }}-memberlist"` |  |
| config.schema_config.configs[0].from | string | `"2020-10-24"` |  |
| config.schema_config.configs[0].index.period | string | `"24h"` |  |
| config.schema_config.configs[0].index.prefix | string | `"index_"` |  |
| config.schema_config.configs[0].object_store | string | `"filesystem"` |  |
| config.schema_config.configs[0].schema | string | `"v11"` |  |
| config.schema_config.configs[0].store | string | `"boltdb-shipper"` |  |
| config.server.grpc_listen_port | int | `9095` |  |
| config.server.http_listen_port | int | `3100` |  |
| config.storage_config.boltdb_shipper.active_index_directory | string | `"/data/loki/boltdb-shipper-active"` |  |
| config.storage_config.boltdb_shipper.cache_location | string | `"/data/loki/boltdb-shipper-cache"` |  |
| config.storage_config.boltdb_shipper.cache_ttl | string | `"24h"` |  |
| config.storage_config.boltdb_shipper.shared_store | string | `"filesystem"` |  |
| config.storage_config.filesystem.directory | string | `"/data/loki/chunks"` |  |
| config.table_manager.retention_deletes_enabled | bool | `false` |  |
| config.table_manager.retention_period | string | `"0s"` |  |
| containerSecurityContext.readOnlyRootFilesystem | bool | `true` |  |
| env | list | `[]` |  |
| extraArgs | object | `{}` |  |
| extraContainers | list | `[]` |  |
| extraEnvFrom | list | `[]` |  |
| extraPorts | list | `[]` |  |
| extraVolumeMounts | list | `[]` |  |
| extraVolumes | list | `[]` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"grafana/loki"` |  |
| image.tag | string | `"2.6.1"` |  |
| ingress.annotations | object | `{}` |  |
| ingress.enabled | bool | `false` |  |
| ingress.hosts[0].host | string | `"chart-example.local"` |  |
| ingress.hosts[0].paths | list | `[]` |  |
| ingress.tls | list | `[]` |  |
| initContainers | list | `[]` |  |
| livenessProbe.httpGet.path | string | `"/ready"` |  |
| livenessProbe.httpGet.port | string | `"http-metrics"` |  |
| livenessProbe.initialDelaySeconds | int | `45` |  |
| networkPolicy.enabled | bool | `false` |  |
| nodeSelector | object | `{}` |  |
| persistence.accessModes[0] | string | `"ReadWriteOnce"` |  |
| persistence.annotations | object | `{}` |  |
| persistence.enabled | bool | `false` |  |
| persistence.labels | object | `{}` |  |
| persistence.size | string | `"10Gi"` |  |
| podAnnotations."prometheus.io/port" | string | `"http-metrics"` |  |
| podAnnotations."prometheus.io/scrape" | string | `"true"` |  |
| podDisruptionBudget | object | `{}` |  |
| podLabels | object | `{}` |  |
| podManagementPolicy | string | `"OrderedReady"` |  |
| rbac.create | bool | `true` |  |
| rbac.pspEnabled | bool | `true` |  |
| readinessProbe.httpGet.path | string | `"/ready"` |  |
| readinessProbe.httpGet.port | string | `"http-metrics"` |  |
| readinessProbe.initialDelaySeconds | int | `45` |  |
| replicas | int | `1` |  |
| resources | object | `{}` |  |
| securityContext.fsGroup | int | `10001` |  |
| securityContext.runAsGroup | int | `10001` |  |
| securityContext.runAsNonRoot | bool | `true` |  |
| securityContext.runAsUser | int | `10001` |  |
| service.annotations | object | `{}` |  |
| service.labels | object | `{}` |  |
| service.nodePort | string | `nil` |  |
| service.port | int | `3100` |  |
| service.targetPort | string | `"http-metrics"` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.automountServiceAccountToken | bool | `true` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.name | string | `nil` |  |
| serviceMonitor.additionalLabels | object | `{}` |  |
| serviceMonitor.annotations | object | `{}` |  |
| serviceMonitor.enabled | bool | `false` |  |
| serviceMonitor.interval | string | `""` |  |
| serviceMonitor.prometheusRule.additionalLabels | object | `{}` |  |
| serviceMonitor.prometheusRule.enabled | bool | `false` |  |
| serviceMonitor.prometheusRule.rules | list | `[]` |  |
| serviceMonitor.scheme | string | `nil` |  |
| serviceMonitor.tlsConfig | object | `{}` |  |
| terminationGracePeriodSeconds | int | `4800` |  |
| tolerations | list | `[]` |  |
| topologySpreadConstraints.enabled | bool | `false` |  |
| tracing.jaegerAgentHost | string | `nil` |  |
| updateStrategy.type | string | `"RollingUpdate"` |  |
| useExistingAlertingGroup.configmapName | string | `""` |  |
| useExistingAlertingGroup.enabled | bool | `false` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.9.1](https://github.com/norwoodj/helm-docs/releases/v1.9.1)
