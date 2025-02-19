# home-assistant

![Version: 1.1.0](https://img.shields.io/badge/Version-1.1.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 2025.2.0](https://img.shields.io/badge/AppVersion-2025.2.0-informational?style=flat-square)

A Helm chart for home assistant on Kubernetes

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| jessebot | <jessebot@linux.com> | <https://github.com/jessebot> |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` | affinity to have the home assisant pod attracted to a specific node |
| autoscaling.enabled | bool | `false` |  |
| autoscaling.maxReplicas | int | `100` |  |
| autoscaling.minReplicas | int | `1` |  |
| autoscaling.targetCPUUtilizationPercentage | int | `80` |  |
| extraEnv | list | `[]` | extra environment variables to pass to the home assistant container, see: https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/#define-an-environment-variable-for-a-container |
| extraVolumeMounts | list | `[]` | Additional volumeMounts on the output Deployment definition. example device mount:   - mountPath: /dev/ttyACM0    name: usb |
| extraVolumes | list | `[]` | Additional volumes on the output Deployment definition. example device as volume:   - hostPath:      path: >-        /dev/serial/by-id/usb-ITEAD_SONOFF_Zigbee_3.0_USB_Dongle_Plus_V2_20230509111242-if00      type: CharDevice    name: usb |
| fullnameOverride | string | `""` | fullname override to use for all chart resources, instead of helm release name |
| homeAssistant.automations | string | `""` | contents of automations.yaml file to create, ignored if homeAssistant.existingAutomationsConfigMap set |
| homeAssistant.configuration | string | `""` | any data you'd like to see put into your configuration.yaml # example config configuration: |   # this enables proxies such as the ingress nginx controller   http:     use_x_forwarded_for: true     trusted_proxies:       - 10.0.0.0/8   mobile:    config: |
| homeAssistant.existingAutomationsConfigMap | string | `""` | name of existing automations ConfigMap |
| homeAssistant.existingConfigurationConfigMap | string | `""` | name of existing ConfigMap |
| homeAssistant.existingScenesConfigMap | string | `""` | name of existing scenes ConfigMap |
| homeAssistant.existingThemesConfigMap | string | `""` | name of existing themes ConfigMap |
| homeAssistant.owner.create | bool | `false` | whether to create an initial owner (admin) user to disable registration |
| homeAssistant.owner.debug | bool | `false` | enable debug mode for the user creation job. WARNING: This reveals secret data |
| homeAssistant.owner.existingSecret | string | `""` | existingSecret for the owner user's credentials secret keys must be: ADMIN_NAME, ADMIN_USERNAME, ADMIN_PASSWORD, ADMIN_LANGUAGE, EXTERNAL_URL |
| homeAssistant.owner.externalURL | string | `""` | if your home assistant is using ingress, this is the external url you connect to, example: https://home-assistant.cooldogsonline.net/ (ignored if owner.existingSecret is set) |
| homeAssistant.owner.language | string | `"en"` | language of the owner user, ignored if owner.existingSecret is set |
| homeAssistant.owner.name | string | `"admin"` | name of the owner user, ignored if owner.existingSecret is set |
| homeAssistant.owner.password | string | `""` | login password of the owner user, ignored if owner.existingSecret is set |
| homeAssistant.owner.username | string | `"admin"` | login username of the owner user, ignored if owner.existingSecret is set |
| homeAssistant.scenes | string | `""` | conents of scenes.yaml file to create, ignored if homeAssistant.existingScenesConfigMap set |
| homeAssistant.setupHacsJobs | object | `{"enabled":false}` | hacs is the [home assistant community store](https://hacs.xyz/) |
| homeAssistant.setupHacsJobs.enabled | bool | `false` | enable the hacs setup job, requires persistence to be on |
| homeAssistant.themes | string | `""` | contents of themes.yaml file to create, ignored if homeAssistant.existingThemesConfigMap set |
| homeAssistant.timezone | string | `""` | The timezone to use for this container. Use one of the identifers here: https://en.wikipedia.org/wiki/List_of_tz_database_time_zones#List |
| image.pullPolicy | string | `"IfNotPresent"` | image pullPolicy. If using tag: latest, set image.pullPolicy: Always |
| image.repository | string | `"ghcr.io/home-assistant/home-assistant"` | image repository that defaults to the official Home Assistant GitHub ghcr.io repo |
| image.tag | string | `""` | Overrides the image tag whose default is the chart appVersion. |
| imagePullSecrets | list | `[]` |  |
| ingress.annotations | object | `{}` |  |
| ingress.className | string | `"nginx"` |  |
| ingress.enabled | bool | `false` | enable external traffic to this pod |
| ingress.hosts[0].host | string | `"chart-example.local"` |  |
| ingress.hosts[0].paths[0].path | string | `"/"` |  |
| ingress.hosts[0].paths[0].pathType | string | `"ImplementationSpecific"` |  |
| ingress.tls | list | `[]` |  |
| livenessProbe.enabled | bool | `true` |  |
| livenessProbe.httpGet.path | string | `"/"` |  |
| livenessProbe.httpGet.port | string | `"http"` |  |
| nameOverride | string | `""` |  |
| nodeSelector | object | `{}` |  |
| persistence.accessMode | string | `"ReadWriteOnce"` | acccessMode for your persistent volume |
| persistence.annotations | object | `{}` | annotations for your persistent volume |
| persistence.enabled | bool | `false` | enable or disable persistent volumes |
| persistence.existingClaim | string | `""` | use an existing persistent volume claim instead of creating one with this chart |
| persistence.size | string | `"8Gi"` | size of your persistent volume |
| persistence.storageClass | string | `""` | storageClass for your persistent volume. if using vanilla k3s, set to local-path |
| podAnnotations | object | `{}` |  |
| podLabels | object | `{}` | labels to apply to all pods |
| podSecurityContext | object | `{}` |  |
| readinessProbe.enabled | bool | `true` |  |
| readinessProbe.httpGet.path | string | `"/"` |  |
| readinessProbe.httpGet.port | string | `"http"` |  |
| replicaCount | int | `1` |  |
| resources | object | `{}` | resource requests and limits. example: for requesting a USB device from the    [generic device plugin](https://github.com/squat/generic-device-plugin)   limits:    squat.ai/serial: 1 |
| securityContext | object | `{}` |  |
| service.port | int | `80` | default port to expose |
| service.targetPort | int | `8123` | default port for the home home-assistant container |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` | Annotations to add to the service account |
| serviceAccount.automount | bool | `true` | Automatically mount a ServiceAccount's API credentials? |
| serviceAccount.create | bool | `true` | Specifies whether a service account should be created |
| serviceAccount.name | string | `""` | If not set and create is true, a name is generated using the fullname template |
| tolerations | list | `[]` | tolerations to have the home assisant pod tolerate node taints |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.11.0](https://github.com/norwoodj/helm-docs/releases/v1.11.0)
