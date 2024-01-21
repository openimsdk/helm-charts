# minio

![Version: 12.8.8](https://img.shields.io/badge/Version-12.8.8-informational?style=flat-square) ![AppVersion: 2023.9.20](https://img.shields.io/badge/AppVersion-2023.9.20-informational?style=flat-square)

MinIO(R) is an object storage server, compatible with Amazon S3 cloud storage service, mainly used for storing unstructured data (such as photos, videos, log files, etc.).

**Homepage:** <https://bitnami.com>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| VMware, Inc. |  | <https://github.com/bitnami/charts> |

## Source Code

* <https://github.com/bitnami/charts/tree/main/bitnami/minio>

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| oci://registry-1.docker.io/bitnamicharts | common | 2.x.x |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| apiIngress.annotations | object | `{}` |  |
| apiIngress.apiVersion | string | `""` |  |
| apiIngress.enabled | bool | `false` |  |
| apiIngress.extraHosts | list | `[]` |  |
| apiIngress.extraPaths | list | `[]` |  |
| apiIngress.extraRules | list | `[]` |  |
| apiIngress.extraTls | list | `[]` |  |
| apiIngress.hostname | string | `"minio.local"` |  |
| apiIngress.ingressClassName | string | `""` |  |
| apiIngress.path | string | `"/"` |  |
| apiIngress.pathType | string | `"ImplementationSpecific"` |  |
| apiIngress.secrets | list | `[]` |  |
| apiIngress.selfSigned | bool | `false` |  |
| apiIngress.servicePort | string | `"minio-api"` |  |
| apiIngress.tls | bool | `false` |  |
| args | list | `[]` |  |
| auth.existingSecret | string | `""` |  |
| auth.forceNewKeys | bool | `false` |  |
| auth.forcePassword | bool | `false` |  |
| auth.rootPassword | string | `"openIM123"` |  |
| auth.rootUser | string | `"root"` |  |
| auth.useCredentialsFiles | bool | `false` |  |
| clientImage.digest | string | `""` |  |
| clientImage.registry | string | `"docker.io"` |  |
| clientImage.repository | string | `"bitnami/minio-client"` |  |
| clientImage.tag | string | `"2023.9.20-debian-11-r0"` |  |
| clusterDomain | string | `"cluster.local"` |  |
| command | list | `[]` |  |
| commonAnnotations | object | `{}` |  |
| commonLabels | object | `{}` |  |
| containerPorts.api | int | `9000` |  |
| containerPorts.console | int | `9001` |  |
| containerSecurityContext.enabled | bool | `true` |  |
| containerSecurityContext.runAsNonRoot | bool | `true` |  |
| containerSecurityContext.runAsUser | int | `1001` |  |
| customLivenessProbe | object | `{}` |  |
| customReadinessProbe | object | `{}` |  |
| customStartupProbe | object | `{}` |  |
| defaultBuckets | string | `"openim"` |  |
| deployment.updateStrategy.type | string | `"Recreate"` |  |
| disableWebUI | bool | `false` |  |
| extraDeploy | list | `[]` |  |
| extraEnvVars | list | `[]` |  |
| extraEnvVarsCM | string | `""` |  |
| extraEnvVarsSecret | string | `""` |  |
| extraVolumeMounts | list | `[]` |  |
| extraVolumes | list | `[]` |  |
| fullnameOverride | string | `""` |  |
| global.imagePullSecrets | list | `[]` |  |
| global.imageRegistry | string | `""` |  |
| global.storageClass | string | `"nfs-client"` |  |
| hostAliases | list | `[]` |  |
| image.debug | bool | `false` |  |
| image.digest | string | `""` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.pullSecrets | list | `[]` |  |
| image.registry | string | `"docker.io"` |  |
| image.repository | string | `"bitnami/minio"` |  |
| image.tag | string | `"2023.9.20-debian-11-r0"` |  |
| ingress.annotations | object | `{}` |  |
| ingress.apiVersion | string | `""` |  |
| ingress.enabled | bool | `false` |  |
| ingress.extraHosts | list | `[]` |  |
| ingress.extraPaths | list | `[]` |  |
| ingress.extraRules | list | `[]` |  |
| ingress.extraTls | list | `[]` |  |
| ingress.hostname | string | `"minio.local"` |  |
| ingress.ingressClassName | string | `""` |  |
| ingress.path | string | `"/"` |  |
| ingress.pathType | string | `"ImplementationSpecific"` |  |
| ingress.secrets | list | `[]` |  |
| ingress.selfSigned | bool | `false` |  |
| ingress.servicePort | string | `"minio-console"` |  |
| ingress.tls | bool | `false` |  |
| initContainers | list | `[]` |  |
| kubeVersion | string | `""` |  |
| lifecycleHooks | object | `{}` |  |
| livenessProbe.enabled | bool | `true` |  |
| livenessProbe.failureThreshold | int | `5` |  |
| livenessProbe.initialDelaySeconds | int | `5` |  |
| livenessProbe.periodSeconds | int | `5` |  |
| livenessProbe.successThreshold | int | `1` |  |
| livenessProbe.timeoutSeconds | int | `5` |  |
| metrics.prometheusAuthType | string | `"public"` |  |
| metrics.prometheusRule.additionalLabels | object | `{}` |  |
| metrics.prometheusRule.enabled | bool | `false` |  |
| metrics.prometheusRule.namespace | string | `""` |  |
| metrics.prometheusRule.rules | list | `[]` |  |
| metrics.serviceMonitor.apiVersion | string | `""` |  |
| metrics.serviceMonitor.enabled | bool | `false` |  |
| metrics.serviceMonitor.honorLabels | bool | `false` |  |
| metrics.serviceMonitor.interval | string | `"30s"` |  |
| metrics.serviceMonitor.jobLabel | string | `""` |  |
| metrics.serviceMonitor.labels | object | `{}` |  |
| metrics.serviceMonitor.metricRelabelings | list | `[]` |  |
| metrics.serviceMonitor.namespace | string | `""` |  |
| metrics.serviceMonitor.path | string | `"/minio/v2/metrics/cluster"` |  |
| metrics.serviceMonitor.relabelings | list | `[]` |  |
| metrics.serviceMonitor.scrapeTimeout | string | `""` |  |
| metrics.serviceMonitor.selector | object | `{}` |  |
| metrics.serviceMonitor.tlsConfig | object | `{}` |  |
| mode | string | `"standalone"` |  |
| nameOverride | string | `""` |  |
| networkPolicy.allowExternal | bool | `true` |  |
| networkPolicy.enabled | bool | `false` |  |
| networkPolicy.extraFromClauses | list | `[]` |  |
| nodeAffinityPreset.key | string | `""` |  |
| nodeAffinityPreset.type | string | `""` |  |
| nodeAffinityPreset.values | list | `[]` |  |
| nodeSelector | object | `{}` |  |
| pdb.create | bool | `false` |  |
| pdb.maxUnavailable | string | `""` |  |
| pdb.minAvailable | int | `1` |  |
| persistence.accessModes[0] | string | `"ReadWriteOnce"` |  |
| persistence.annotations | object | `{}` |  |
| persistence.enabled | bool | `true` |  |
| persistence.existingClaim | string | `""` |  |
| persistence.mountPath | string | `"/bitnami/minio/data"` |  |
| persistence.size | string | `"1Gi"` |  |
| persistence.storageClass | string | `""` |  |
| podAffinityPreset | string | `""` |  |
| podAnnotations | object | `{}` |  |
| podAntiAffinityPreset | string | `"soft"` |  |
| podLabels | object | `{}` |  |
| podSecurityContext.enabled | bool | `true` |  |
| podSecurityContext.fsGroup | int | `1001` |  |
| priorityClassName | string | `""` |  |
| provisioning.args | list | `[]` |  |
| provisioning.buckets | list | `[]` |  |
| provisioning.cleanupAfterFinished.enabled | bool | `false` |  |
| provisioning.cleanupAfterFinished.seconds | int | `600` |  |
| provisioning.command | list | `[]` |  |
| provisioning.config | list | `[]` |  |
| provisioning.containerSecurityContext.enabled | bool | `true` |  |
| provisioning.containerSecurityContext.runAsNonRoot | bool | `true` |  |
| provisioning.containerSecurityContext.runAsUser | int | `1001` |  |
| provisioning.enabled | bool | `false` |  |
| provisioning.extraCommands | list | `[]` |  |
| provisioning.extraVolumeMounts | list | `[]` |  |
| provisioning.extraVolumes | list | `[]` |  |
| provisioning.groups | list | `[]` |  |
| provisioning.podAnnotations | object | `{}` |  |
| provisioning.podLabels | object | `{}` |  |
| provisioning.podSecurityContext.enabled | bool | `true` |  |
| provisioning.podSecurityContext.fsGroup | int | `1001` |  |
| provisioning.policies | list | `[]` |  |
| provisioning.resources.limits | object | `{}` |  |
| provisioning.resources.requests | object | `{}` |  |
| provisioning.schedulerName | string | `""` |  |
| provisioning.users | list | `[]` |  |
| provisioning.usersExistingSecrets | list | `[]` |  |
| readinessProbe.enabled | bool | `true` |  |
| readinessProbe.failureThreshold | int | `5` |  |
| readinessProbe.initialDelaySeconds | int | `5` |  |
| readinessProbe.periodSeconds | int | `5` |  |
| readinessProbe.successThreshold | int | `1` |  |
| readinessProbe.timeoutSeconds | int | `1` |  |
| resources.limits | object | `{}` |  |
| resources.requests | object | `{}` |  |
| schedulerName | string | `""` |  |
| service.annotations | object | `{}` |  |
| service.clusterIP | string | `""` |  |
| service.externalTrafficPolicy | string | `"Cluster"` |  |
| service.extraPorts | list | `[]` |  |
| service.headless.annotations | object | `{}` |  |
| service.loadBalancerIP | string | `""` |  |
| service.loadBalancerSourceRanges | list | `[]` |  |
| service.nodePorts.api | string | `""` |  |
| service.nodePorts.console | string | `""` |  |
| service.ports.api | int | `9000` |  |
| service.ports.console | int | `9001` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.automountServiceAccountToken | bool | `true` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.name | string | `""` |  |
| sidecars | list | `[]` |  |
| startupProbe.enabled | bool | `false` |  |
| startupProbe.failureThreshold | int | `60` |  |
| startupProbe.initialDelaySeconds | int | `0` |  |
| startupProbe.periodSeconds | int | `10` |  |
| startupProbe.successThreshold | int | `1` |  |
| startupProbe.timeoutSeconds | int | `5` |  |
| statefulset.drivesPerNode | int | `1` |  |
| statefulset.podManagementPolicy | string | `"Parallel"` |  |
| statefulset.replicaCount | int | `4` |  |
| statefulset.updateStrategy.type | string | `"RollingUpdate"` |  |
| statefulset.zones | int | `1` |  |
| terminationGracePeriodSeconds | string | `""` |  |
| tls.autoGenerated | bool | `false` |  |
| tls.enabled | bool | `false` |  |
| tls.existingSecret | string | `""` |  |
| tls.mountPath | string | `""` |  |
| tolerations | list | `[]` |  |
| topologySpreadConstraints | list | `[]` |  |
| volumePermissions.containerSecurityContext.runAsUser | int | `0` |  |
| volumePermissions.enabled | bool | `false` |  |
| volumePermissions.image.digest | string | `""` |  |
| volumePermissions.image.pullPolicy | string | `"IfNotPresent"` |  |
| volumePermissions.image.pullSecrets | list | `[]` |  |
| volumePermissions.image.registry | string | `"docker.io"` |  |
| volumePermissions.image.repository | string | `"bitnami/os-shell"` |  |
| volumePermissions.image.tag | string | `"11-debian-11-r72"` |  |
| volumePermissions.resources.limits | object | `{}` |  |
| volumePermissions.resources.requests | object | `{}` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.9.1](https://github.com/norwoodj/helm-docs/releases/v1.9.1)
