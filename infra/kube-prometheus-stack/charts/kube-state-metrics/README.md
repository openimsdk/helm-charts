# kube-state-metrics

![Version: 5.14.0](https://img.shields.io/badge/Version-5.14.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 2.10.0](https://img.shields.io/badge/AppVersion-2.10.0-informational?style=flat-square)

Install kube-state-metrics to generate and expose cluster-level metrics

**Homepage:** <https://github.com/kubernetes/kube-state-metrics/>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| tariq1890 | <tariq.ibrahim@mulesoft.com> |  |
| mrueg | <manuel@rueg.eu> |  |
| dotdc | <david@0xdc.me> |  |

## Source Code

* <https://github.com/kubernetes/kube-state-metrics/>

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| annotations | object | `{}` |  |
| autosharding.enabled | bool | `false` |  |
| collectors[0] | string | `"certificatesigningrequests"` |  |
| collectors[10] | string | `"limitranges"` |  |
| collectors[11] | string | `"mutatingwebhookconfigurations"` |  |
| collectors[12] | string | `"namespaces"` |  |
| collectors[13] | string | `"networkpolicies"` |  |
| collectors[14] | string | `"nodes"` |  |
| collectors[15] | string | `"persistentvolumeclaims"` |  |
| collectors[16] | string | `"persistentvolumes"` |  |
| collectors[17] | string | `"poddisruptionbudgets"` |  |
| collectors[18] | string | `"pods"` |  |
| collectors[19] | string | `"replicasets"` |  |
| collectors[1] | string | `"configmaps"` |  |
| collectors[20] | string | `"replicationcontrollers"` |  |
| collectors[21] | string | `"resourcequotas"` |  |
| collectors[22] | string | `"secrets"` |  |
| collectors[23] | string | `"services"` |  |
| collectors[24] | string | `"statefulsets"` |  |
| collectors[25] | string | `"storageclasses"` |  |
| collectors[26] | string | `"validatingwebhookconfigurations"` |  |
| collectors[27] | string | `"volumeattachments"` |  |
| collectors[2] | string | `"cronjobs"` |  |
| collectors[3] | string | `"daemonsets"` |  |
| collectors[4] | string | `"deployments"` |  |
| collectors[5] | string | `"endpoints"` |  |
| collectors[6] | string | `"horizontalpodautoscalers"` |  |
| collectors[7] | string | `"ingresses"` |  |
| collectors[8] | string | `"jobs"` |  |
| collectors[9] | string | `"leases"` |  |
| containerSecurityContext.allowPrivilegeEscalation | bool | `false` |  |
| containerSecurityContext.capabilities.drop[0] | string | `"ALL"` |  |
| containers | list | `[]` |  |
| customLabels | object | `{}` |  |
| customResourceState.config | object | `{}` |  |
| customResourceState.enabled | bool | `false` |  |
| extraArgs | list | `[]` |  |
| extraManifests | list | `[]` |  |
| global.imagePullSecrets | list | `[]` |  |
| global.imageRegistry | string | `""` |  |
| hostNetwork | bool | `false` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.registry | string | `"m.daocloud.io"` |  |
| image.repository | string | `"registry.k8s.io/kube-state-metrics/kube-state-metrics"` |  |
| image.sha | string | `""` |  |
| image.tag | string | `""` |  |
| imagePullSecrets | list | `[]` |  |
| initContainers | list | `[]` |  |
| kubeRBACProxy.containerSecurityContext | object | `{}` |  |
| kubeRBACProxy.enabled | bool | `false` |  |
| kubeRBACProxy.extraArgs | list | `[]` |  |
| kubeRBACProxy.image.pullPolicy | string | `"IfNotPresent"` |  |
| kubeRBACProxy.image.registry | string | `"quay.io"` |  |
| kubeRBACProxy.image.repository | string | `"brancz/kube-rbac-proxy"` |  |
| kubeRBACProxy.image.sha | string | `""` |  |
| kubeRBACProxy.image.tag | string | `"v0.14.0"` |  |
| kubeRBACProxy.resources | object | `{}` |  |
| kubeRBACProxy.volumeMounts | list | `[]` |  |
| kubeTargetVersionOverride | string | `""` |  |
| kubeconfig.enabled | bool | `false` |  |
| kubeconfig.secret | string | `nil` |  |
| metricAllowlist | list | `[]` |  |
| metricAnnotationsAllowList | list | `[]` |  |
| metricDenylist | list | `[]` |  |
| metricLabelsAllowlist | list | `[]` |  |
| namespaceOverride | string | `""` |  |
| namespaces | string | `""` |  |
| namespacesDenylist | string | `""` |  |
| networkPolicy.enabled | bool | `false` |  |
| networkPolicy.flavor | string | `"kubernetes"` | Flavor of the network policy to use. Can be: * kubernetes for networking.k8s.io/v1/NetworkPolicy * cilium     for cilium.io/v2/CiliumNetworkPolicy |
| nodeSelector | object | `{}` |  |
| podAnnotations | object | `{}` |  |
| podDisruptionBudget | object | `{}` |  |
| podSecurityPolicy.additionalVolumes | list | `[]` |  |
| podSecurityPolicy.annotations | object | `{}` |  |
| podSecurityPolicy.enabled | bool | `false` |  |
| prometheus.monitor.additionalLabels | object | `{}` |  |
| prometheus.monitor.annotations | object | `{}` |  |
| prometheus.monitor.bearerTokenFile | string | `""` |  |
| prometheus.monitor.bearerTokenSecret | object | `{}` |  |
| prometheus.monitor.enabled | bool | `false` |  |
| prometheus.monitor.honorLabels | bool | `false` |  |
| prometheus.monitor.interval | string | `""` |  |
| prometheus.monitor.jobLabel | string | `""` |  |
| prometheus.monitor.labelLimit | int | `0` |  |
| prometheus.monitor.labelNameLengthLimit | int | `0` |  |
| prometheus.monitor.labelValueLengthLimit | int | `0` |  |
| prometheus.monitor.metricRelabelings | list | `[]` |  |
| prometheus.monitor.namespace | string | `""` |  |
| prometheus.monitor.namespaceSelector | list | `[]` |  |
| prometheus.monitor.podTargetLabels | list | `[]` |  |
| prometheus.monitor.proxyUrl | string | `""` |  |
| prometheus.monitor.relabelings | list | `[]` |  |
| prometheus.monitor.sampleLimit | int | `0` |  |
| prometheus.monitor.scheme | string | `""` |  |
| prometheus.monitor.scrapeTimeout | string | `""` |  |
| prometheus.monitor.selectorOverride | object | `{}` |  |
| prometheus.monitor.targetLabels | list | `[]` |  |
| prometheus.monitor.targetLimit | int | `0` |  |
| prometheus.monitor.tlsConfig | object | `{}` |  |
| prometheusScrape | bool | `true` |  |
| rbac.create | bool | `true` |  |
| rbac.extraRules | list | `[]` |  |
| rbac.useClusterRole | bool | `true` |  |
| releaseLabel | bool | `false` |  |
| releaseNamespace | bool | `false` |  |
| replicas | int | `1` |  |
| resources | object | `{}` |  |
| revisionHistoryLimit | int | `10` |  |
| securityContext.enabled | bool | `true` |  |
| securityContext.fsGroup | int | `65534` |  |
| securityContext.runAsGroup | int | `65534` |  |
| securityContext.runAsNonRoot | bool | `true` |  |
| securityContext.runAsUser | int | `65534` |  |
| securityContext.seccompProfile.type | string | `"RuntimeDefault"` |  |
| selectorOverride | object | `{}` |  |
| selfMonitor.enabled | bool | `false` |  |
| service.annotations | object | `{}` |  |
| service.clusterIP | string | `""` |  |
| service.loadBalancerIP | string | `""` |  |
| service.loadBalancerSourceRanges | list | `[]` |  |
| service.nodePort | int | `0` |  |
| service.port | int | `8080` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.imagePullSecrets | list | `[]` |  |
| serviceAccount.name | string | `nil` |  |
| tolerations | list | `[]` |  |
| topologySpreadConstraints | list | `[]` |  |
| verticalPodAutoscaler.controlledResources | list | `[]` |  |
| verticalPodAutoscaler.enabled | bool | `false` |  |
| verticalPodAutoscaler.maxAllowed | object | `{}` |  |
| verticalPodAutoscaler.minAllowed | object | `{}` |  |
| volumeMounts | list | `[]` |  |
| volumes | list | `[]` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.9.1](https://github.com/norwoodj/helm-docs/releases/v1.9.1)
