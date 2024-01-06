# filebeat

![Version: 7.17.3](https://img.shields.io/badge/Version-7.17.3-informational?style=flat-square) ![AppVersion: 7.17.3](https://img.shields.io/badge/AppVersion-7.17.3-informational?style=flat-square)

Official Elastic helm chart for Filebeat

**Homepage:** <https://github.com/elastic/helm-charts>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| Elastic | <helm-charts@elastic.co> |  |

## Source Code

* <https://github.com/elastic/beats>

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| clusterRoleRules[0].apiGroups[0] | string | `""` |  |
| clusterRoleRules[0].resources[0] | string | `"namespaces"` |  |
| clusterRoleRules[0].resources[1] | string | `"nodes"` |  |
| clusterRoleRules[0].resources[2] | string | `"pods"` |  |
| clusterRoleRules[0].verbs[0] | string | `"get"` |  |
| clusterRoleRules[0].verbs[1] | string | `"list"` |  |
| clusterRoleRules[0].verbs[2] | string | `"watch"` |  |
| clusterRoleRules[1].apiGroups[0] | string | `"apps"` |  |
| clusterRoleRules[1].resources[0] | string | `"replicasets"` |  |
| clusterRoleRules[1].verbs[0] | string | `"get"` |  |
| clusterRoleRules[1].verbs[1] | string | `"list"` |  |
| clusterRoleRules[1].verbs[2] | string | `"watch"` |  |
| daemonset.affinity | object | `{}` |  |
| daemonset.annotations | object | `{}` |  |
| daemonset.enabled | bool | `true` |  |
| daemonset.envFrom | list | `[]` |  |
| daemonset.extraEnvs | list | `[]` |  |
| daemonset.extraVolumeMounts | list | `[]` |  |
| daemonset.extraVolumes | list | `[]` |  |
| daemonset.filebeatConfig."filebeat.yml" | string | `"filebeat.inputs:\n- type: container\n  paths:\n    - /var/log/containers/*.log\n  processors:\n  - add_kubernetes_metadata:\n      host: ${NODE_NAME}\n      matchers:\n      - logs_path:\n          logs_path: \"/var/log/containers/\"\n\noutput.elasticsearch:\n  host: '${NODE_NAME}'\n  hosts: '${ELASTICSEARCH_HOSTS:elasticsearch-master:9200}'\n"` |  |
| daemonset.hostNetworking | bool | `false` |  |
| daemonset.labels | object | `{}` |  |
| daemonset.maxUnavailable | int | `1` |  |
| daemonset.nodeSelector | object | `{}` |  |
| daemonset.resources.limits.cpu | string | `"1000m"` |  |
| daemonset.resources.limits.memory | string | `"200Mi"` |  |
| daemonset.resources.requests.cpu | string | `"100m"` |  |
| daemonset.resources.requests.memory | string | `"100Mi"` |  |
| daemonset.secretMounts | list | `[]` |  |
| daemonset.securityContext.privileged | bool | `false` |  |
| daemonset.securityContext.runAsUser | int | `0` |  |
| daemonset.tolerations | list | `[]` |  |
| deployment.affinity | object | `{}` |  |
| deployment.annotations | object | `{}` |  |
| deployment.enabled | bool | `false` |  |
| deployment.envFrom | list | `[]` |  |
| deployment.extraEnvs | list | `[]` |  |
| deployment.extraVolumeMounts | list | `[]` |  |
| deployment.extraVolumes | list | `[]` |  |
| deployment.filebeatConfig."filebeat.yml" | string | `"filebeat.inputs:\n- type: tcp\n  max_message_size: 10MiB\n  host: \"localhost:9000\"\n\noutput.elasticsearch:\n  host: '${NODE_NAME}'\n  hosts: '${ELASTICSEARCH_HOSTS:elasticsearch-master:9200}'\n"` |  |
| deployment.labels | object | `{}` |  |
| deployment.nodeSelector | object | `{}` |  |
| deployment.resources.limits.cpu | string | `"1000m"` |  |
| deployment.resources.limits.memory | string | `"200Mi"` |  |
| deployment.resources.requests.cpu | string | `"100m"` |  |
| deployment.resources.requests.memory | string | `"100Mi"` |  |
| deployment.secretMounts | list | `[]` |  |
| deployment.securityContext.privileged | bool | `false` |  |
| deployment.securityContext.runAsUser | int | `0` |  |
| deployment.tolerations | list | `[]` |  |
| dnsConfig | object | `{}` |  |
| envFrom | list | `[]` |  |
| extraContainers | string | `""` |  |
| extraEnvs | list | `[]` |  |
| extraInitContainers | list | `[]` |  |
| extraVolumeMounts | list | `[]` |  |
| extraVolumes | list | `[]` |  |
| filebeatConfig | object | `{}` |  |
| fullnameOverride | string | `""` |  |
| hostAliases | list | `[]` |  |
| hostPathRoot | string | `"/var/lib"` |  |
| image | string | `"docker.elastic.co/beats/filebeat"` |  |
| imagePullPolicy | string | `"IfNotPresent"` |  |
| imagePullSecrets | list | `[]` |  |
| imageTag | string | `"7.17.3"` |  |
| labels | object | `{}` |  |
| livenessProbe.exec.command[0] | string | `"sh"` |  |
| livenessProbe.exec.command[1] | string | `"-c"` |  |
| livenessProbe.exec.command[2] | string | `"#!/usr/bin/env bash -e\ncurl --fail 127.0.0.1:5066\n"` |  |
| livenessProbe.failureThreshold | int | `3` |  |
| livenessProbe.initialDelaySeconds | int | `10` |  |
| livenessProbe.periodSeconds | int | `10` |  |
| livenessProbe.timeoutSeconds | int | `5` |  |
| managedServiceAccount | bool | `true` |  |
| nameOverride | string | `""` |  |
| nodeSelector | object | `{}` |  |
| podAnnotations | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| priorityClassName | string | `""` |  |
| readinessProbe.exec.command[0] | string | `"sh"` |  |
| readinessProbe.exec.command[1] | string | `"-c"` |  |
| readinessProbe.exec.command[2] | string | `"#!/usr/bin/env bash -e\nfilebeat test output\n"` |  |
| readinessProbe.failureThreshold | int | `3` |  |
| readinessProbe.initialDelaySeconds | int | `10` |  |
| readinessProbe.periodSeconds | int | `10` |  |
| readinessProbe.timeoutSeconds | int | `5` |  |
| replicas | int | `1` |  |
| resources | object | `{}` |  |
| secretMounts | list | `[]` |  |
| serviceAccount | string | `""` |  |
| serviceAccountAnnotations | object | `{}` |  |
| terminationGracePeriod | int | `30` |  |
| tolerations | list | `[]` |  |
| updateStrategy | string | `"RollingUpdate"` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.9.1](https://github.com/norwoodj/helm-docs/releases/v1.9.1)
