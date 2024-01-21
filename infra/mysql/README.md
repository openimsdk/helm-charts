# mysql

![Version: 9.12.3](https://img.shields.io/badge/Version-9.12.3-informational?style=flat-square) ![AppVersion: 8.0.34](https://img.shields.io/badge/AppVersion-8.0.34-informational?style=flat-square)

MySQL is a fast, reliable, scalable, and easy to use open source relational database system. Designed to handle mission-critical, heavy-load production applications.

**Homepage:** <https://bitnami.com>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| VMware, Inc. |  | <https://github.com/bitnami/charts> |

## Source Code

* <https://github.com/bitnami/charts/tree/main/bitnami/mysql>

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| oci://registry-1.docker.io/bitnamicharts | common | 2.x.x |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| architecture | string | `"standalone"` |  |
| auth.createDatabase | bool | `true` |  |
| auth.customPasswordFiles | object | `{}` |  |
| auth.database | string | `"openIM_v3"` |  |
| auth.existingSecret | string | `""` |  |
| auth.password | string | `""` |  |
| auth.replicationPassword | string | `"openIM123"` |  |
| auth.replicationUser | string | `"replicator"` |  |
| auth.rootPassword | string | `"openIM123"` |  |
| auth.usePasswordFiles | bool | `false` |  |
| auth.username | string | `""` |  |
| clusterDomain | string | `"cluster.local"` |  |
| commonAnnotations | object | `{}` |  |
| commonLabels | object | `{}` |  |
| diagnosticMode.args[0] | string | `"infinity"` |  |
| diagnosticMode.command[0] | string | `"sleep"` |  |
| diagnosticMode.enabled | bool | `false` |  |
| extraDeploy | list | `[]` |  |
| fullnameOverride | string | `""` |  |
| global.imagePullSecrets | list | `[]` |  |
| global.imageRegistry | string | `""` |  |
| global.storageClass | string | `"nfs-client"` |  |
| image.debug | bool | `false` |  |
| image.digest | string | `""` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.pullSecrets | list | `[]` |  |
| image.registry | string | `"docker.io"` |  |
| image.repository | string | `"bitnami/mysql"` |  |
| image.tag | string | `"8.0.34-debian-11-r56"` |  |
| initdbScripts | object | `{}` |  |
| initdbScriptsConfigMap | string | `""` |  |
| kubeVersion | string | `""` |  |
| metrics.containerSecurityContext.enabled | bool | `true` |  |
| metrics.containerSecurityContext.runAsNonRoot | bool | `true` |  |
| metrics.containerSecurityContext.runAsUser | int | `1001` |  |
| metrics.enabled | bool | `false` |  |
| metrics.extraArgs.primary | list | `[]` |  |
| metrics.extraArgs.secondary | list | `[]` |  |
| metrics.image.digest | string | `""` |  |
| metrics.image.pullPolicy | string | `"IfNotPresent"` |  |
| metrics.image.pullSecrets | list | `[]` |  |
| metrics.image.registry | string | `"docker.io"` |  |
| metrics.image.repository | string | `"bitnami/mysqld-exporter"` |  |
| metrics.image.tag | string | `"0.15.0-debian-11-r50"` |  |
| metrics.livenessProbe.enabled | bool | `true` |  |
| metrics.livenessProbe.failureThreshold | int | `3` |  |
| metrics.livenessProbe.initialDelaySeconds | int | `120` |  |
| metrics.livenessProbe.periodSeconds | int | `10` |  |
| metrics.livenessProbe.successThreshold | int | `1` |  |
| metrics.livenessProbe.timeoutSeconds | int | `1` |  |
| metrics.prometheusRule.additionalLabels | object | `{}` |  |
| metrics.prometheusRule.enabled | bool | `false` |  |
| metrics.prometheusRule.namespace | string | `""` |  |
| metrics.prometheusRule.rules | list | `[]` |  |
| metrics.readinessProbe.enabled | bool | `true` |  |
| metrics.readinessProbe.failureThreshold | int | `3` |  |
| metrics.readinessProbe.initialDelaySeconds | int | `30` |  |
| metrics.readinessProbe.periodSeconds | int | `10` |  |
| metrics.readinessProbe.successThreshold | int | `1` |  |
| metrics.readinessProbe.timeoutSeconds | int | `1` |  |
| metrics.resources.limits | object | `{}` |  |
| metrics.resources.requests | object | `{}` |  |
| metrics.service.annotations."prometheus.io/port" | string | `"{{ .Values.metrics.service.port }}"` |  |
| metrics.service.annotations."prometheus.io/scrape" | string | `"true"` |  |
| metrics.service.clusterIP | string | `""` |  |
| metrics.service.port | int | `9104` |  |
| metrics.service.type | string | `"ClusterIP"` |  |
| metrics.serviceMonitor.annotations | object | `{}` |  |
| metrics.serviceMonitor.enabled | bool | `false` |  |
| metrics.serviceMonitor.honorLabels | bool | `false` |  |
| metrics.serviceMonitor.interval | string | `"30s"` |  |
| metrics.serviceMonitor.jobLabel | string | `""` |  |
| metrics.serviceMonitor.labels | object | `{}` |  |
| metrics.serviceMonitor.metricRelabelings | list | `[]` |  |
| metrics.serviceMonitor.namespace | string | `""` |  |
| metrics.serviceMonitor.relabelings | list | `[]` |  |
| metrics.serviceMonitor.scrapeTimeout | string | `""` |  |
| metrics.serviceMonitor.selector | object | `{}` |  |
| nameOverride | string | `""` |  |
| namespaceOverride | string | `""` |  |
| networkPolicy.allowExternal | bool | `true` |  |
| networkPolicy.enabled | bool | `false` |  |
| networkPolicy.explicitNamespacesSelector | object | `{}` |  |
| primary.affinity | object | `{}` |  |
| primary.args | list | `[]` |  |
| primary.command | list | `[]` |  |
| primary.configuration | string | `"[mysqld]\ndefault_authentication_plugin=mysql_native_password\nskip-name-resolve\nexplicit_defaults_for_timestamp\nbasedir=/opt/bitnami/mysql\nplugin_dir=/opt/bitnami/mysql/lib/plugin\nport=3306\nsocket=/opt/bitnami/mysql/tmp/mysql.sock\ndatadir=/bitnami/mysql/data\ntmpdir=/opt/bitnami/mysql/tmp\nmax_allowed_packet=16M\nbind-address=*\npid-file=/opt/bitnami/mysql/tmp/mysqld.pid\nlog-error=/opt/bitnami/mysql/logs/mysqld.log\ncharacter-set-server=UTF8\ncollation-server=utf8_general_ci\nslow_query_log=0\nlong_query_time=10.0\n\n[client]\nport=3306\nsocket=/opt/bitnami/mysql/tmp/mysql.sock\ndefault-character-set=UTF8\nplugin_dir=/opt/bitnami/mysql/lib/plugin\n\n[manager]\nport=3306\nsocket=/opt/bitnami/mysql/tmp/mysql.sock\npid-file=/opt/bitnami/mysql/tmp/mysqld.pid"` |  |
| primary.containerSecurityContext.enabled | bool | `true` |  |
| primary.containerSecurityContext.runAsNonRoot | bool | `true` |  |
| primary.containerSecurityContext.runAsUser | int | `1001` |  |
| primary.customLivenessProbe | object | `{}` |  |
| primary.customReadinessProbe | object | `{}` |  |
| primary.customStartupProbe | object | `{}` |  |
| primary.existingConfigmap | string | `""` |  |
| primary.extraEnvVars | list | `[]` |  |
| primary.extraEnvVarsCM | string | `""` |  |
| primary.extraEnvVarsSecret | string | `""` |  |
| primary.extraFlags | string | `""` |  |
| primary.extraPorts | list | `[]` |  |
| primary.extraVolumeMounts | list | `[]` |  |
| primary.extraVolumes | list | `[]` |  |
| primary.hostAliases | list | `[]` |  |
| primary.initContainers | list | `[]` |  |
| primary.lifecycleHooks | object | `{}` |  |
| primary.livenessProbe.enabled | bool | `true` |  |
| primary.livenessProbe.failureThreshold | int | `3` |  |
| primary.livenessProbe.initialDelaySeconds | int | `5` |  |
| primary.livenessProbe.periodSeconds | int | `10` |  |
| primary.livenessProbe.successThreshold | int | `1` |  |
| primary.livenessProbe.timeoutSeconds | int | `1` |  |
| primary.name | string | `"primary"` |  |
| primary.nodeAffinityPreset.key | string | `""` |  |
| primary.nodeAffinityPreset.type | string | `""` |  |
| primary.nodeAffinityPreset.values | list | `[]` |  |
| primary.nodeSelector | object | `{}` |  |
| primary.pdb.create | bool | `false` |  |
| primary.pdb.maxUnavailable | string | `""` |  |
| primary.pdb.minAvailable | int | `1` |  |
| primary.persistence.accessModes[0] | string | `"ReadWriteOnce"` |  |
| primary.persistence.annotations | object | `{}` |  |
| primary.persistence.enabled | bool | `true` |  |
| primary.persistence.existingClaim | string | `""` |  |
| primary.persistence.selector | object | `{}` |  |
| primary.persistence.size | string | `"1Gi"` |  |
| primary.persistence.storageClass | string | `""` |  |
| primary.persistence.subPath | string | `""` |  |
| primary.podAffinityPreset | string | `""` |  |
| primary.podAnnotations | object | `{}` |  |
| primary.podAntiAffinityPreset | string | `"soft"` |  |
| primary.podLabels | object | `{}` |  |
| primary.podManagementPolicy | string | `""` |  |
| primary.podSecurityContext.enabled | bool | `true` |  |
| primary.podSecurityContext.fsGroup | int | `1001` |  |
| primary.priorityClassName | string | `""` |  |
| primary.readinessProbe.enabled | bool | `true` |  |
| primary.readinessProbe.failureThreshold | int | `3` |  |
| primary.readinessProbe.initialDelaySeconds | int | `5` |  |
| primary.readinessProbe.periodSeconds | int | `10` |  |
| primary.readinessProbe.successThreshold | int | `1` |  |
| primary.readinessProbe.timeoutSeconds | int | `1` |  |
| primary.resources.limits | object | `{}` |  |
| primary.resources.requests | object | `{}` |  |
| primary.runtimeClassName | string | `""` |  |
| primary.schedulerName | string | `""` |  |
| primary.service.annotations | object | `{}` |  |
| primary.service.clusterIP | string | `""` |  |
| primary.service.externalTrafficPolicy | string | `"Cluster"` |  |
| primary.service.extraPorts | list | `[]` |  |
| primary.service.headless.annotations | object | `{}` |  |
| primary.service.loadBalancerIP | string | `""` |  |
| primary.service.loadBalancerSourceRanges | list | `[]` |  |
| primary.service.nodePorts.mysql | string | `""` |  |
| primary.service.ports.mysql | int | `3306` |  |
| primary.service.sessionAffinity | string | `"None"` |  |
| primary.service.sessionAffinityConfig | object | `{}` |  |
| primary.service.type | string | `"ClusterIP"` |  |
| primary.sidecars | list | `[]` |  |
| primary.startupProbe.enabled | bool | `true` |  |
| primary.startupProbe.failureThreshold | int | `10` |  |
| primary.startupProbe.initialDelaySeconds | int | `15` |  |
| primary.startupProbe.periodSeconds | int | `10` |  |
| primary.startupProbe.successThreshold | int | `1` |  |
| primary.startupProbe.timeoutSeconds | int | `1` |  |
| primary.terminationGracePeriodSeconds | string | `""` |  |
| primary.tolerations | list | `[]` |  |
| primary.topologySpreadConstraints | list | `[]` |  |
| primary.updateStrategy.type | string | `"RollingUpdate"` |  |
| rbac.create | bool | `false` |  |
| rbac.rules | list | `[]` |  |
| secondary.affinity | object | `{}` |  |
| secondary.args | list | `[]` |  |
| secondary.command | list | `[]` |  |
| secondary.configuration | string | `"[mysqld]\ndefault_authentication_plugin=mysql_native_password\nskip-name-resolve\nexplicit_defaults_for_timestamp\nbasedir=/opt/bitnami/mysql\nplugin_dir=/opt/bitnami/mysql/lib/plugin\nport=3306\nsocket=/opt/bitnami/mysql/tmp/mysql.sock\ndatadir=/bitnami/mysql/data\ntmpdir=/opt/bitnami/mysql/tmp\nmax_allowed_packet=16M\nbind-address=*\npid-file=/opt/bitnami/mysql/tmp/mysqld.pid\nlog-error=/opt/bitnami/mysql/logs/mysqld.log\ncharacter-set-server=UTF8\ncollation-server=utf8_general_ci\nslow_query_log=0\nlong_query_time=10.0\n\n[client]\nport=3306\nsocket=/opt/bitnami/mysql/tmp/mysql.sock\ndefault-character-set=UTF8\nplugin_dir=/opt/bitnami/mysql/lib/plugin\n\n[manager]\nport=3306\nsocket=/opt/bitnami/mysql/tmp/mysql.sock\npid-file=/opt/bitnami/mysql/tmp/mysqld.pid"` |  |
| secondary.containerSecurityContext.enabled | bool | `true` |  |
| secondary.containerSecurityContext.runAsNonRoot | bool | `true` |  |
| secondary.containerSecurityContext.runAsUser | int | `1001` |  |
| secondary.customLivenessProbe | object | `{}` |  |
| secondary.customReadinessProbe | object | `{}` |  |
| secondary.customStartupProbe | object | `{}` |  |
| secondary.existingConfigmap | string | `""` |  |
| secondary.extraEnvVars | list | `[]` |  |
| secondary.extraEnvVarsCM | string | `""` |  |
| secondary.extraEnvVarsSecret | string | `""` |  |
| secondary.extraFlags | string | `""` |  |
| secondary.extraPorts | list | `[]` |  |
| secondary.extraVolumeMounts | list | `[]` |  |
| secondary.extraVolumes | list | `[]` |  |
| secondary.hostAliases | list | `[]` |  |
| secondary.initContainers | list | `[]` |  |
| secondary.lifecycleHooks | object | `{}` |  |
| secondary.livenessProbe.enabled | bool | `true` |  |
| secondary.livenessProbe.failureThreshold | int | `3` |  |
| secondary.livenessProbe.initialDelaySeconds | int | `5` |  |
| secondary.livenessProbe.periodSeconds | int | `10` |  |
| secondary.livenessProbe.successThreshold | int | `1` |  |
| secondary.livenessProbe.timeoutSeconds | int | `1` |  |
| secondary.name | string | `"secondary"` |  |
| secondary.nodeAffinityPreset.key | string | `""` |  |
| secondary.nodeAffinityPreset.type | string | `""` |  |
| secondary.nodeAffinityPreset.values | list | `[]` |  |
| secondary.nodeSelector | object | `{}` |  |
| secondary.pdb.create | bool | `false` |  |
| secondary.pdb.maxUnavailable | string | `""` |  |
| secondary.pdb.minAvailable | int | `1` |  |
| secondary.persistence.accessModes[0] | string | `"ReadWriteOnce"` |  |
| secondary.persistence.annotations | object | `{}` |  |
| secondary.persistence.enabled | bool | `true` |  |
| secondary.persistence.existingClaim | string | `""` |  |
| secondary.persistence.selector | object | `{}` |  |
| secondary.persistence.size | string | `"1Gi"` |  |
| secondary.persistence.storageClass | string | `""` |  |
| secondary.persistence.subPath | string | `""` |  |
| secondary.podAffinityPreset | string | `""` |  |
| secondary.podAnnotations | object | `{}` |  |
| secondary.podAntiAffinityPreset | string | `"soft"` |  |
| secondary.podLabels | object | `{}` |  |
| secondary.podManagementPolicy | string | `""` |  |
| secondary.podSecurityContext.enabled | bool | `true` |  |
| secondary.podSecurityContext.fsGroup | int | `1001` |  |
| secondary.priorityClassName | string | `""` |  |
| secondary.readinessProbe.enabled | bool | `true` |  |
| secondary.readinessProbe.failureThreshold | int | `3` |  |
| secondary.readinessProbe.initialDelaySeconds | int | `5` |  |
| secondary.readinessProbe.periodSeconds | int | `10` |  |
| secondary.readinessProbe.successThreshold | int | `1` |  |
| secondary.readinessProbe.timeoutSeconds | int | `1` |  |
| secondary.replicaCount | int | `1` |  |
| secondary.resources.limits | object | `{}` |  |
| secondary.resources.requests | object | `{}` |  |
| secondary.runtimeClassName | string | `""` |  |
| secondary.schedulerName | string | `""` |  |
| secondary.service.annotations | object | `{}` |  |
| secondary.service.clusterIP | string | `""` |  |
| secondary.service.externalTrafficPolicy | string | `"Cluster"` |  |
| secondary.service.extraPorts | list | `[]` |  |
| secondary.service.headless.annotations | object | `{}` |  |
| secondary.service.loadBalancerIP | string | `""` |  |
| secondary.service.loadBalancerSourceRanges | list | `[]` |  |
| secondary.service.nodePorts.mysql | string | `""` |  |
| secondary.service.ports.mysql | int | `3306` |  |
| secondary.service.sessionAffinity | string | `"None"` |  |
| secondary.service.sessionAffinityConfig | object | `{}` |  |
| secondary.service.type | string | `"ClusterIP"` |  |
| secondary.sidecars | list | `[]` |  |
| secondary.startupProbe.enabled | bool | `true` |  |
| secondary.startupProbe.failureThreshold | int | `15` |  |
| secondary.startupProbe.initialDelaySeconds | int | `15` |  |
| secondary.startupProbe.periodSeconds | int | `10` |  |
| secondary.startupProbe.successThreshold | int | `1` |  |
| secondary.startupProbe.timeoutSeconds | int | `1` |  |
| secondary.terminationGracePeriodSeconds | string | `""` |  |
| secondary.tolerations | list | `[]` |  |
| secondary.topologySpreadConstraints | list | `[]` |  |
| secondary.updateStrategy.type | string | `"RollingUpdate"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.automountServiceAccountToken | bool | `true` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.name | string | `""` |  |
| serviceBindings.enabled | bool | `false` |  |
| startdbScripts | object | `{}` |  |
| startdbScriptsConfigMap | string | `""` |  |
| volumePermissions.enabled | bool | `false` |  |
| volumePermissions.image.digest | string | `""` |  |
| volumePermissions.image.pullPolicy | string | `"IfNotPresent"` |  |
| volumePermissions.image.pullSecrets | list | `[]` |  |
| volumePermissions.image.registry | string | `"docker.io"` |  |
| volumePermissions.image.repository | string | `"bitnami/os-shell"` |  |
| volumePermissions.image.tag | string | `"11-debian-11-r72"` |  |
| volumePermissions.resources | object | `{}` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.9.1](https://github.com/norwoodj/helm-docs/releases/v1.9.1)
