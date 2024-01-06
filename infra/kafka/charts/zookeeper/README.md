# zookeeper

![Version: 12.1.3](https://img.shields.io/badge/Version-12.1.3-informational?style=flat-square) ![AppVersion: 3.9.0](https://img.shields.io/badge/AppVersion-3.9.0-informational?style=flat-square)

Apache ZooKeeper provides a reliable, centralized register of configuration data and services for distributed applications.

**Homepage:** <https://bitnami.com>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| VMware, Inc. |  | <https://github.com/bitnami/charts> |

## Source Code

* <https://github.com/bitnami/charts/tree/main/bitnami/zookeeper>

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| oci://registry-1.docker.io/bitnamicharts | common | 2.x.x |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| args | list | `[]` |  |
| auth.client.clientPassword | string | `""` |  |
| auth.client.clientUser | string | `""` |  |
| auth.client.enabled | bool | `false` |  |
| auth.client.existingSecret | string | `""` |  |
| auth.client.serverPasswords | string | `""` |  |
| auth.client.serverUsers | string | `""` |  |
| auth.quorum.enabled | bool | `false` |  |
| auth.quorum.existingSecret | string | `""` |  |
| auth.quorum.learnerPassword | string | `""` |  |
| auth.quorum.learnerUser | string | `""` |  |
| auth.quorum.serverPasswords | string | `""` |  |
| auth.quorum.serverUsers | string | `""` |  |
| autopurge.purgeInterval | int | `0` |  |
| autopurge.snapRetainCount | int | `3` |  |
| clusterDomain | string | `"cluster.local"` |  |
| command[0] | string | `"/scripts/setup.sh"` |  |
| commonAnnotations | object | `{}` |  |
| commonLabels | object | `{}` |  |
| configuration | string | `""` |  |
| containerPorts.client | int | `2181` |  |
| containerPorts.election | int | `3888` |  |
| containerPorts.follower | int | `2888` |  |
| containerPorts.tls | int | `3181` |  |
| containerSecurityContext.allowPrivilegeEscalation | bool | `false` |  |
| containerSecurityContext.enabled | bool | `true` |  |
| containerSecurityContext.runAsNonRoot | bool | `true` |  |
| containerSecurityContext.runAsUser | int | `1001` |  |
| customLivenessProbe | object | `{}` |  |
| customReadinessProbe | object | `{}` |  |
| customStartupProbe | object | `{}` |  |
| dataLogDir | string | `""` |  |
| diagnosticMode.args[0] | string | `"infinity"` |  |
| diagnosticMode.command[0] | string | `"sleep"` |  |
| diagnosticMode.enabled | bool | `false` |  |
| existingConfigmap | string | `""` |  |
| extraDeploy | list | `[]` |  |
| extraEnvVars | list | `[]` |  |
| extraEnvVarsCM | string | `""` |  |
| extraEnvVarsSecret | string | `""` |  |
| extraVolumeMounts | list | `[]` |  |
| extraVolumes | list | `[]` |  |
| fourlwCommandsWhitelist | string | `"srvr, mntr, ruok"` |  |
| fullnameOverride | string | `""` |  |
| global.imagePullSecrets | list | `[]` |  |
| global.imageRegistry | string | `""` |  |
| global.storageClass | string | `""` |  |
| heapSize | int | `1024` |  |
| hostAliases | list | `[]` |  |
| image.debug | bool | `false` |  |
| image.digest | string | `""` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.pullSecrets | list | `[]` |  |
| image.registry | string | `"docker.io"` |  |
| image.repository | string | `"bitnami/zookeeper"` |  |
| image.tag | string | `"3.9.0-debian-11-r11"` |  |
| initContainers | list | `[]` |  |
| initLimit | int | `10` |  |
| jvmFlags | string | `""` |  |
| kubeVersion | string | `""` |  |
| lifecycleHooks | object | `{}` |  |
| listenOnAllIPs | bool | `false` |  |
| livenessProbe.enabled | bool | `true` |  |
| livenessProbe.failureThreshold | int | `6` |  |
| livenessProbe.initialDelaySeconds | int | `30` |  |
| livenessProbe.periodSeconds | int | `10` |  |
| livenessProbe.probeCommandTimeout | int | `2` |  |
| livenessProbe.successThreshold | int | `1` |  |
| livenessProbe.timeoutSeconds | int | `5` |  |
| logLevel | string | `"ERROR"` |  |
| maxClientCnxns | int | `60` |  |
| maxSessionTimeout | int | `40000` |  |
| metrics.containerPort | int | `9141` |  |
| metrics.enabled | bool | `false` |  |
| metrics.prometheusRule.additionalLabels | object | `{}` |  |
| metrics.prometheusRule.enabled | bool | `false` |  |
| metrics.prometheusRule.namespace | string | `""` |  |
| metrics.prometheusRule.rules | list | `[]` |  |
| metrics.service.annotations."prometheus.io/path" | string | `"/metrics"` |  |
| metrics.service.annotations."prometheus.io/port" | string | `"{{ .Values.metrics.service.port }}"` |  |
| metrics.service.annotations."prometheus.io/scrape" | string | `"true"` |  |
| metrics.service.port | int | `9141` |  |
| metrics.service.type | string | `"ClusterIP"` |  |
| metrics.serviceMonitor.additionalLabels | object | `{}` |  |
| metrics.serviceMonitor.enabled | bool | `false` |  |
| metrics.serviceMonitor.honorLabels | bool | `false` |  |
| metrics.serviceMonitor.interval | string | `""` |  |
| metrics.serviceMonitor.jobLabel | string | `""` |  |
| metrics.serviceMonitor.metricRelabelings | list | `[]` |  |
| metrics.serviceMonitor.namespace | string | `""` |  |
| metrics.serviceMonitor.relabelings | list | `[]` |  |
| metrics.serviceMonitor.scrapeTimeout | string | `""` |  |
| metrics.serviceMonitor.selector | object | `{}` |  |
| minServerId | int | `1` |  |
| nameOverride | string | `""` |  |
| namespaceOverride | string | `""` |  |
| networkPolicy.allowExternal | bool | `true` |  |
| networkPolicy.enabled | bool | `false` |  |
| nodeAffinityPreset.key | string | `""` |  |
| nodeAffinityPreset.type | string | `""` |  |
| nodeAffinityPreset.values | list | `[]` |  |
| nodeSelector | object | `{}` |  |
| pdb.create | bool | `false` |  |
| pdb.maxUnavailable | int | `1` |  |
| pdb.minAvailable | string | `""` |  |
| persistence.accessModes[0] | string | `"ReadWriteOnce"` |  |
| persistence.annotations | object | `{}` |  |
| persistence.dataLogDir.existingClaim | string | `""` |  |
| persistence.dataLogDir.selector | object | `{}` |  |
| persistence.dataLogDir.size | string | `"8Gi"` |  |
| persistence.enabled | bool | `true` |  |
| persistence.existingClaim | string | `""` |  |
| persistence.labels | object | `{}` |  |
| persistence.selector | object | `{}` |  |
| persistence.size | string | `"8Gi"` |  |
| persistence.storageClass | string | `""` |  |
| podAffinityPreset | string | `""` |  |
| podAnnotations | object | `{}` |  |
| podAntiAffinityPreset | string | `"soft"` |  |
| podLabels | object | `{}` |  |
| podManagementPolicy | string | `"Parallel"` |  |
| podSecurityContext.enabled | bool | `true` |  |
| podSecurityContext.fsGroup | int | `1001` |  |
| preAllocSize | int | `65536` |  |
| priorityClassName | string | `""` |  |
| readinessProbe.enabled | bool | `true` |  |
| readinessProbe.failureThreshold | int | `6` |  |
| readinessProbe.initialDelaySeconds | int | `5` |  |
| readinessProbe.periodSeconds | int | `10` |  |
| readinessProbe.probeCommandTimeout | int | `2` |  |
| readinessProbe.successThreshold | int | `1` |  |
| readinessProbe.timeoutSeconds | int | `5` |  |
| replicaCount | int | `1` |  |
| resources.limits | object | `{}` |  |
| resources.requests.cpu | string | `"250m"` |  |
| resources.requests.memory | string | `"256Mi"` |  |
| schedulerName | string | `""` |  |
| service.annotations | object | `{}` |  |
| service.clusterIP | string | `""` |  |
| service.disableBaseClientPort | bool | `false` |  |
| service.externalTrafficPolicy | string | `"Cluster"` |  |
| service.extraPorts | list | `[]` |  |
| service.headless.annotations | object | `{}` |  |
| service.headless.publishNotReadyAddresses | bool | `true` |  |
| service.headless.servicenameOverride | string | `""` |  |
| service.loadBalancerIP | string | `""` |  |
| service.loadBalancerSourceRanges | list | `[]` |  |
| service.nodePorts.client | string | `""` |  |
| service.nodePorts.tls | string | `""` |  |
| service.ports.client | int | `2181` |  |
| service.ports.election | int | `3888` |  |
| service.ports.follower | int | `2888` |  |
| service.ports.tls | int | `3181` |  |
| service.sessionAffinity | string | `"None"` |  |
| service.sessionAffinityConfig | object | `{}` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.automountServiceAccountToken | bool | `true` |  |
| serviceAccount.create | bool | `false` |  |
| serviceAccount.name | string | `""` |  |
| sidecars | list | `[]` |  |
| snapCount | int | `100000` |  |
| startupProbe.enabled | bool | `false` |  |
| startupProbe.failureThreshold | int | `15` |  |
| startupProbe.initialDelaySeconds | int | `30` |  |
| startupProbe.periodSeconds | int | `10` |  |
| startupProbe.successThreshold | int | `1` |  |
| startupProbe.timeoutSeconds | int | `1` |  |
| syncLimit | int | `5` |  |
| tickTime | int | `2000` |  |
| tls.client.auth | string | `"none"` |  |
| tls.client.autoGenerated | bool | `false` |  |
| tls.client.enabled | bool | `false` |  |
| tls.client.existingSecret | string | `""` |  |
| tls.client.existingSecretKeystoreKey | string | `""` |  |
| tls.client.existingSecretTruststoreKey | string | `""` |  |
| tls.client.keystorePassword | string | `""` |  |
| tls.client.keystorePath | string | `"/opt/bitnami/zookeeper/config/certs/client/zookeeper.keystore.jks"` |  |
| tls.client.passwordsSecretKeystoreKey | string | `""` |  |
| tls.client.passwordsSecretName | string | `""` |  |
| tls.client.passwordsSecretTruststoreKey | string | `""` |  |
| tls.client.truststorePassword | string | `""` |  |
| tls.client.truststorePath | string | `"/opt/bitnami/zookeeper/config/certs/client/zookeeper.truststore.jks"` |  |
| tls.quorum.auth | string | `"none"` |  |
| tls.quorum.autoGenerated | bool | `false` |  |
| tls.quorum.enabled | bool | `false` |  |
| tls.quorum.existingSecret | string | `""` |  |
| tls.quorum.existingSecretKeystoreKey | string | `""` |  |
| tls.quorum.existingSecretTruststoreKey | string | `""` |  |
| tls.quorum.keystorePassword | string | `""` |  |
| tls.quorum.keystorePath | string | `"/opt/bitnami/zookeeper/config/certs/quorum/zookeeper.keystore.jks"` |  |
| tls.quorum.passwordsSecretKeystoreKey | string | `""` |  |
| tls.quorum.passwordsSecretName | string | `""` |  |
| tls.quorum.passwordsSecretTruststoreKey | string | `""` |  |
| tls.quorum.truststorePassword | string | `""` |  |
| tls.quorum.truststorePath | string | `"/opt/bitnami/zookeeper/config/certs/quorum/zookeeper.truststore.jks"` |  |
| tls.resources.limits | object | `{}` |  |
| tls.resources.requests | object | `{}` |  |
| tolerations | list | `[]` |  |
| topologySpreadConstraints | list | `[]` |  |
| updateStrategy.rollingUpdate | object | `{}` |  |
| updateStrategy.type | string | `"RollingUpdate"` |  |
| volumePermissions.containerSecurityContext.enabled | bool | `true` |  |
| volumePermissions.containerSecurityContext.runAsUser | int | `0` |  |
| volumePermissions.enabled | bool | `false` |  |
| volumePermissions.image.digest | string | `""` |  |
| volumePermissions.image.pullPolicy | string | `"IfNotPresent"` |  |
| volumePermissions.image.pullSecrets | list | `[]` |  |
| volumePermissions.image.registry | string | `"docker.io"` |  |
| volumePermissions.image.repository | string | `"bitnami/os-shell"` |  |
| volumePermissions.image.tag | string | `"11-debian-11-r51"` |  |
| volumePermissions.resources.limits | object | `{}` |  |
| volumePermissions.resources.requests | object | `{}` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.9.1](https://github.com/norwoodj/helm-docs/releases/v1.9.1)
