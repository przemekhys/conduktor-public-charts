<a name="readme-top" id="readme-top"></a>
# Conduktor Platform

> If you have any questions or [feedback](https://product.conduktor.help/c/55-helm-chart) contact our [support](https://www.conduktor.io/contact/support/).

## TL;DR

```console
$ helm repo add conduktor https://helm.conduktor.io
$ helm install my-platform conduktor/console \
    --create-namespace -n conduktor \
    --set config.organization.name="my-org" \
    --set config.admin.email="admin@conduktor.io" \
    --set config.admin.password="admin" \
    --set config.database.password="postgres" \
    --set config.database.username="postgres" \
    --set config.database.host="postgresql" \
    --set config.database.name="postgres" \
    --set config.license="${LICENSE}"
```

## Introduction

Helm Chart to deploy Conduktor Platform on Kubernetes.

[Snippets](#snippets) are available in this README to help you get started.

## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+

## Parameters

### Global parameters

Global Docker image parameters
Please, note that this will override the image parameters, including dependencies, configured to use the global value
Current available global Docker image parameters: imageRegistry, imagePullSecrets and storageClass

| Name                      | Description                                     | Value |
| ------------------------- | ----------------------------------------------- | ----- |
| `global.imageRegistry`    | Global Docker image registry                    | `""`  |
| `global.imagePullSecrets` | Global Docker registry secret names as an array | `[]`  |
| `global.storageClass`     | Global StorageClass for Persistent Volume(s)    | `""`  |

### Common parameters

| Name                     | Description                                                                             | Value           |
| ------------------------ | --------------------------------------------------------------------------------------- | --------------- |
| `nameOverride`           | String to partially override common.names.name                                          | `""`            |
| `fullnameOverride`       | String to fully override common.names.fullname                                          | `""`            |
| `namespaceOverride`      | String to fully override common.names.namespace                                         | `""`            |
| `commonLabels`           | Labels to add to all deployed objects                                                   | `{}`            |
| `commonAnnotations`      | Annotations to add to all deployed objects                                              | `{}`            |
| `clusterDomain`          | Kubernetes cluster domain name                                                          | `cluster.local` |
| `extraDeploy`            | Array of extra objects to deploy with the release                                       | `[]`            |
| `diagnosticMode.enabled` | Enable diagnostic mode (all probes will be disabled and the command will be overridden) | `false`         |
| `diagnosticMode.command` | Command to override all containers in the deployment                                    | `["sleep"]`     |
| `diagnosticMode.args`    | Args to override all containers in the deployment                                       | `["infinity"]`  |

### Platform product Parameters

You can paste here your Conduktor Platform Configuration

Refer to our [documentation](https://docs.conduktor.io/platform/configuration/env-variables/) for the full list of product configuration properties.

| Name                                   | Description                                                                                                                                            | Value      |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- |
| `config.organization.name`             | Your Conduktor Platform Organization, you can only set it at install! You will need to change it in the Conduktor Platform UI after the installation   | `""`       |
| `config.admin.email`                   | Your Conduktor Platform Admin email, you can only set it at install! You will need to change it in the Conduktor Platform UI after the installation    | `""`       |
| `config.admin.password`                | Your Conduktor Platform Admin password, you can only set it at install! You will need to change it in the Conduktor Platform UI after the installation | `""`       |
| `config.database.host`                 | Your Conduktor Platform Database host                                                                                                                  | `""`       |
| `config.database.port`                 | Your Conduktor Platform Database port                                                                                                                  | `5432`     |
| `config.database.name`                 | Your Conduktor Platform Database name                                                                                                                  | `postgres` |
| `config.database.username`             | Your Conduktor Platform Database username                                                                                                              | `""`       |
| `config.database.password`             | Your Conduktor Platform Database password                                                                                                              | `""`       |
| `config.license`                       | Conduktor Platform Enterprise license, if none given, the product will run in free tier                                                                | `""`       |
| `config.existingLicenseSecret`         | Name of an existing secret containing the license                                                                                                      | `""`       |
| `config.existingSecret`                | Name of an existing secret containing sensitive configuration                                                                                          | `""`       |
| `config.platform.external.url`         | Force the platform to redirect and use this URL (useful when behind a proxy to fix SSO issues)                                                         | `""`       |
| `config.platform.https.selfSigned`     | Enable HTTPS with a self-signed certificate (not recommended for production) based on 'config.platform.external.url' (required).                       | `false`    |
| `config.platform.https.existingSecret` | Enable HTTPS with an existing secret containing the tls.crt and tls.key (required).                                                                    | `""`       |

### Platform Monitoring product Parameters

You can paste here your Conduktor Platform Cortex Configuration

Refer to our [documentation](https://docs.conduktor.io/platform/configuration/cortex/) for the full list of product configuration properties.

| Name                                            | Description                                                                                 | Value   |
| ----------------------------------------------- | ------------------------------------------------------------------------------------------- | ------- |
| `monitoringConfig.existingSecret`               | The name of an existing Secret with your custom configuration for Conduktor Platform Cortex | `""`    |
| `monitoringConfig.scraper.skipSSLCheck`         | Skip TLS verification when scraping Platform metrics                                        | `false` |
| `monitoringConfig.scraper.caFile`               | Skip TLS verification when scraping Platform metrics                                        | `""`    |
| `monitoringConfig.storage.s3`                   | S3 storage configuration                                                                    | `{}`    |
| `monitoringConfig.storage.s3.endpoint`          | S3 endpoint                                                                                 |         |
| `monitoringConfig.storage.s3.region`            | S3 region                                                                                   |         |
| `monitoringConfig.storage.s3.bucket`            | S3 bucket name                                                                              |         |
| `monitoringConfig.storage.s3.insecure`          | S3 insecure                                                                                 |         |
| `monitoringConfig.storage.s3.accessKeyId`       | S3 access key id                                                                            |         |
| `monitoringConfig.storage.s3.secretAccessKey`   | S3 secret access key                                                                        |         |
| `monitoringConfig.storage.gcs`                  | GCS storage configuration                                                                   | `{}`    |
| `monitoringConfig.storage.gcs.bucketName`       | GCS bucket name                                                                             |         |
| `monitoringConfig.storage.gcs.serviceAccount`   | GCS service account                                                                         |         |
| `monitoringConfig.storage.azure`                | Azure storage configuration                                                                 | `{}`    |
| `monitoringConfig.storage.azure.accountName`    | Azure account name                                                                          |         |
| `monitoringConfig.storage.azure.accountKey`     | Azure account key                                                                           |         |
| `monitoringConfig.storage.azure.containerName`  | Azure container name                                                                        |         |
| `monitoringConfig.storage.azure.endpointSuffix` | Azure endpoint suffix                                                                       |         |
| `monitoringConfig.storage.swift`                | Swift storage configuration                                                                 | `{}`    |
| `monitoringConfig.storage.swift.authUrl`        | Swift auth url                                                                              |         |
| `monitoringConfig.storage.swift.password`       | Swift password                                                                              |         |
| `monitoringConfig.storage.swift.containerName`  | Swift container name                                                                        |         |
| `monitoringConfig.storage.swift.userId`         | Swift user id                                                                               |         |
| `monitoringConfig.storage.swift.username`       | Swift username                                                                              |         |
| `monitoringConfig.storage.swift.userDomainName` | Swift user domain name                                                                      |         |
| `monitoringConfig.storage.swift.userDomainId`   | Swift user domain id                                                                        |         |
| `monitoringConfig.storage.swift.domainId`       | Swift domain id                                                                             |         |
| `monitoringConfig.storage.swift.domainName`     | Swift domain name                                                                           |         |
| `monitoringConfig.storage.swift.projectId`      | Swift project id                                                                            |         |
| `monitoringConfig.storage.swift.regionName`     | Swift region name                                                                           |         |

### Platform Deployment Parameters

| Name                                          | Description                                                                                                                                                   | Value                          |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------ |
| `platform.image.registry`                     | Conduktor Platform image registry                                                                                                                             | `docker.io`                    |
| `platform.image.repository`                   | Conduktor Platform image repository                                                                                                                           | `conduktor/conduktor-platform` |
| `platform.image.tag`                          | Conduktor Platform image tag (immutable tags are recommended)                                                                                                 | `1.19.0`                       |
| `platform.image.digest`                       | Conduktor Platform image digest in the way sha256:aa.... Please note this parameter, if set, will override the tag image tag (immutable tags are recommended) | `""`                           |
| `platform.image.pullPolicy`                   | Conduktor Platform image pull policy                                                                                                                          | `IfNotPresent`                 |
| `platform.image.pullSecrets`                  | Conduktor Platform image pull secrets                                                                                                                         | `[]`                           |
| `platform.image.debug`                        | Enable Conduktor Platform image debug mode                                                                                                                    | `false`                        |
| `platform.replicaCount`                       | Number of Conduktor Platform replicas to deploy                                                                                                               | `1`                            |
| `platform.containerPorts.http`                | Conduktor Platform HTTP (or HTTPS if configured) container port                                                                                               | `8080`                         |
| `platform.livenessProbe.enabled`              | Enable livenessProbe on Conduktor Platform containers                                                                                                         | `true`                         |
| `platform.livenessProbe.initialDelaySeconds`  | Initial delay seconds for livenessProbe                                                                                                                       | `60`                           |
| `platform.livenessProbe.periodSeconds`        | Period seconds for livenessProbe                                                                                                                              | `10`                           |
| `platform.livenessProbe.timeoutSeconds`       | Timeout seconds for livenessProbe                                                                                                                             | `5`                            |
| `platform.livenessProbe.failureThreshold`     | Failure threshold for livenessProbe                                                                                                                           | `3`                            |
| `platform.livenessProbe.successThreshold`     | Success threshold for livenessProbe                                                                                                                           | `1`                            |
| `platform.readinessProbe.enabled`             | Enable readinessProbe on Conduktor Platform containers                                                                                                        | `true`                         |
| `platform.readinessProbe.initialDelaySeconds` | Initial delay seconds for readinessProbe                                                                                                                      | `60`                           |
| `platform.readinessProbe.periodSeconds`       | Period seconds for readinessProbe                                                                                                                             | `10`                           |
| `platform.readinessProbe.timeoutSeconds`      | Timeout seconds for readinessProbe                                                                                                                            | `5`                            |
| `platform.readinessProbe.failureThreshold`    | Failure threshold for readinessProbe                                                                                                                          | `3`                            |
| `platform.readinessProbe.successThreshold`    | Success threshold for readinessProbe                                                                                                                          | `1`                            |
| `platform.startupProbe.enabled`               | Enable startupProbe on Conduktor Platform containers                                                                                                          | `true`                         |
| `platform.startupProbe.initialDelaySeconds`   | Initial delay seconds for startupProbe                                                                                                                        | `10`                           |
| `platform.startupProbe.periodSeconds`         | Period seconds for startupProbe                                                                                                                               | `10`                           |
| `platform.startupProbe.timeoutSeconds`        | Timeout seconds for startupProbe                                                                                                                              | `5`                            |
| `platform.startupProbe.failureThreshold`      | Failure threshold for startupProbe                                                                                                                            | `10`                           |
| `platform.startupProbe.successThreshold`      | Success threshold for startupProbe                                                                                                                            | `1`                            |
| `platform.customLivenessProbe`                | Custom livenessProbe that overrides the default one                                                                                                           | `{}`                           |
| `platform.customReadinessProbe`               | Custom readinessProbe that overrides the default one                                                                                                          | `{}`                           |
| `platform.customStartupProbe`                 | Custom startupProbe that overrides the default one                                                                                                            | `{}`                           |
| `platform.resources.limits.cpu`               | CPU limit for the platform container                                                                                                                          | `3000m`                        |
| `platform.resources.limits.memory`            | Memory limit for the container                                                                                                                                | `4Gi`                          |
| `platform.resources.requests.cpu`             | CPU resource requests                                                                                                                                         | `1000m`                        |
| `platform.resources.requests.memory`          | Memory resource requests                                                                                                                                      | `2Gi`                          |
| `platform.podSecurityContext`                 | Conduktor Platform Pod Security Context                                                                                                                       | `{}`                           |
| `platform.containerSecurityContext`           | Conduktor Platform containers' Security Context                                                                                                               | `{}`                           |
| `platform.existingConfigmap`                  | The name of an existing ConfigMap with your custom configuration for Conduktor Platform                                                                       | `""`                           |
| `platform.command`                            | Override default container command (useful when using custom images)                                                                                          | `[]`                           |
| `platform.args`                               | Override default container args (useful when using custom images)                                                                                             | `[]`                           |
| `platform.hostAliases`                        | Conduktor Platform pods host aliases                                                                                                                          | `[]`                           |
| `platform.podLabels`                          | Extra labels for Conduktor Platform pods                                                                                                                      | `{}`                           |
| `platform.podAnnotations`                     | Annotations for Conduktor Platform pods                                                                                                                       | `{}`                           |
| `platform.podAffinityPreset`                  | Pod affinity preset. Ignored if `platform.affinity` is set. Allowed values: `soft` or `hard`                                                                  | `""`                           |
| `platform.podAntiAffinityPreset`              | Pod anti-affinity preset. Ignored if `platform.affinity` is set. Allowed values: `soft` or `hard`                                                             | `soft`                         |
| `platform.nodeAffinityPreset.type`            | Node affinity preset type. Ignored if `platform.affinity` is set. Allowed values: `soft` or `hard`                                                            | `""`                           |
| `platform.nodeAffinityPreset.key`             | Node label key to match. Ignored if `platform.affinity` is set                                                                                                | `""`                           |
| `platform.nodeAffinityPreset.values`          | Node label values to match. Ignored if `platform.affinity` is set                                                                                             | `[]`                           |
| `platform.affinity`                           | Affinity for Conduktor Platform pods assignment                                                                                                               | `{}`                           |
| `platform.nodeSelector`                       | Node labels for Conduktor Platform pods assignment                                                                                                            | `{}`                           |
| `platform.tolerations`                        | Tolerations for Conduktor Platform pods assignment                                                                                                            | `[]`                           |
| `platform.updateStrategy.type`                | Conduktor Platform statefulset strategy type                                                                                                                  | `RollingUpdate`                |
| `platform.priorityClassName`                  | Conduktor Platform pods' priorityClassName                                                                                                                    | `""`                           |
| `platform.topologySpreadConstraints`          | Topology Spread Constraints for pod assignment spread across your cluster among failure-domains. Evaluated as a template                                      | `[]`                           |
| `platform.schedulerName`                      | Name of the k8s scheduler (other than default) for Conduktor Platform pods                                                                                    | `""`                           |
| `platform.terminationGracePeriodSeconds`      | Seconds Redmine pod needs to terminate gracefully                                                                                                             | `""`                           |
| `platform.lifecycleHooks`                     | for the Conduktor Platform container(s) to automate configuration before or after startup                                                                     | `{}`                           |
| `platform.dataVolume`                         | Configure the data volume to store Conduktor Platform data                                                                                                    | `{}`                           |
| `platform.tmpVolume`                          | Configure the /tmp volume which store various data related to running services                                                                                | `{}`                           |
| `platform.extraEnvVars`                       | Array with extra environment variables to add to Conduktor Platform nodes                                                                                     | `[]`                           |
| `platform.extraEnvVarsCM`                     | Name of existing ConfigMap containing extra env vars for Conduktor Platform nodes                                                                             | `""`                           |
| `platform.extraEnvVarsSecret`                 | Name of existing Secret containing extra env vars for Conduktor Platform nodes                                                                                | `""`                           |
| `platform.extraVolumes`                       | Optionally specify extra list of additional volumes for the Conduktor Platform pod(s).                                                                        | `[]`                           |
| `platform.extraVolumeMounts`                  | Optionally specify extra list of additional volumeMounts for the Conduktor Platform container(s).                                                             | `[]`                           |
| `platform.sidecars`                           | Add additional sidecar containers to the Conduktor Platform pod(s)                                                                                            | `[]`                           |
| `platform.initContainers`                     | Add additional init containers to the Conduktor Platform pod(s)                                                                                               | `[]`                           |

### Traffic Exposure Parameters

| Name                               | Description                                                                                                                      | Value                    |
| ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- | ------------------------ |
| `service.type`                     | Conduktor Platform service type                                                                                                  | `ClusterIP`              |
| `service.ports.http`               | Conduktor Platform service HTTP port                                                                                             | `80`                     |
| `service.nodePorts.http`           | Node port for HTTP                                                                                                               | `""`                     |
| `service.clusterIP`                | Conduktor Platform service Cluster IP                                                                                            | `""`                     |
| `service.loadBalancerSourceRanges` | Conduktor Platform service Load Balancer sources                                                                                 | `[]`                     |
| `service.externalTrafficPolicy`    | Conduktor Platform service external traffic policy                                                                               | `Cluster`                |
| `service.labels`                   | Additional custom labels for Conduktor Platform service                                                                          | `{}`                     |
| `service.annotations`              | Additional custom annotations for Conduktor Platform service                                                                     | `{}`                     |
| `service.extraPorts`               | Extra ports to expose in Conduktor Platform service (normally used with the `sidecars` value)                                    | `[]`                     |
| `service.sessionAffinity`          | Control where client requests go, to the same pod or round-robin                                                                 | `None`                   |
| `service.sessionAffinityConfig`    | Additional settings for the sessionAffinity                                                                                      | `{}`                     |
| `ingress.enabled`                  | Enable ingress record generation for Conduktor Platform                                                                          | `false`                  |
| `ingress.pathType`                 | Ingress path type                                                                                                                | `ImplementationSpecific` |
| `ingress.apiVersion`               | Force Ingress API version (automatically detected if not set)                                                                    | `""`                     |
| `ingress.hostname`                 | Default host for the ingress record                                                                                              | `platform.local`         |
| `ingress.ingressClassName`         | IngressClass that will be used to implement the Ingress (Kubernetes 1.18+)                                                       | `""`                     |
| `ingress.path`                     | Default path for the ingress record                                                                                              | `/`                      |
| `ingress.annotations`              | Additional annotations for the Ingress resource. To enable certificate autogeneration, place here your cert-manager annotations. | `{}`                     |
| `ingress.tls`                      | Enable TLS configuration for the host defined at `ingress.hostname` parameter                                                    | `false`                  |
| `ingress.selfSigned`               | Create a TLS secret for this ingress record using self-signed certificates generated by Helm                                     | `false`                  |
| `ingress.extraHosts`               | An array with additional hostname(s) to be covered with the ingress record                                                       | `[]`                     |
| `ingress.extraPaths`               | An array with additional arbitrary paths that may need to be added to the ingress under the main host                            | `[]`                     |
| `ingress.extraTls`                 | TLS configuration for additional hostname(s) to be covered with this ingress record                                              | `[]`                     |
| `ingress.secrets`                  | Custom TLS certificates as secrets                                                                                               | `[]`                     |
| `ingress.extraRules`               | Additional rules to be covered with this ingress record                                                                          | `[]`                     |

### Other Parameters

| Name                                          | Description                                                      | Value  |
| --------------------------------------------- | ---------------------------------------------------------------- | ------ |
| `serviceAccount.create`                       | Specifies whether a ServiceAccount should be created             | `true` |
| `serviceAccount.name`                         | The name of the ServiceAccount to use.                           | `""`   |
| `serviceAccount.annotations`                  | Additional Service Account annotations (evaluated as a template) | `{}`   |
| `serviceAccount.automountServiceAccountToken` | Automount service account token for the server service account   | `true` |

### Platform Cortex Parameters

| Name                                                | Description                                                                                                                                                          | Value                                 |
| --------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------- |
| `platformCortex.enabled`                            | Enable Conduktor Platform Cortex                                                                                                                                     | `true`                                |
| `platformCortex.image.registry`                     | Conduktor Platform Cortex image registry                                                                                                                             | `docker.io`                           |
| `platformCortex.image.repository`                   | Conduktor Platform Cortex image repository                                                                                                                           | `conduktor/conduktor-platform-cortex` |
| `platformCortex.image.tag`                          | Conduktor Platform Cortex image tag (immutable tags are recommended)                                                                                                 | `1.19.0`                              |
| `platformCortex.image.digest`                       | Conduktor Platform Cortex image digest in the way sha256:aa.... Please note this parameter, if set, will override the tag image tag (immutable tags are recommended) | `""`                                  |
| `platformCortex.image.pullPolicy`                   | Conduktor Platform Cortex image pull policy                                                                                                                          | `IfNotPresent`                        |
| `platformCortex.image.pullSecrets`                  | Conduktor Platform Cortex image pull secrets                                                                                                                         | `[]`                                  |
| `platformCortex.image.debug`                        | Enable Conduktor Platform Cortex image debug mode                                                                                                                    | `false`                               |
| `platformCortex.replicaCount`                       | Number of Conduktor Platform replicas to deploy                                                                                                                      | `1`                                   |
| `platformCortex.containerPorts.cortex`              | Conduktor Platform Cortex HTTP (or HTTPS if configured) container port                                                                                               | `9009`                                |
| `platformCortex.containerPorts.alertmanager`        | Conduktor Platform AlertManager HTTP (or HTTPS if configured) container port                                                                                         | `9010`                                |
| `platformCortex.containerPorts.prometheus`          | Conduktor Platform Prometheus HTTP (or HTTPS if configured) container port                                                                                           | `9090`                                |
| `platformCortex.livenessProbe.enabled`              | Enable livenessProbe on Conduktor Platform Cortex containers                                                                                                         | `true`                                |
| `platformCortex.livenessProbe.initialDelaySeconds`  | Initial delay seconds for livenessProbe                                                                                                                              | `30`                                  |
| `platformCortex.livenessProbe.periodSeconds`        | Period seconds for livenessProbe                                                                                                                                     | `10`                                  |
| `platformCortex.livenessProbe.timeoutSeconds`       | Timeout seconds for livenessProbe                                                                                                                                    | `5`                                   |
| `platformCortex.livenessProbe.failureThreshold`     | Failure threshold for livenessProbe                                                                                                                                  | `3`                                   |
| `platformCortex.livenessProbe.successThreshold`     | Success threshold for livenessProbe                                                                                                                                  | `1`                                   |
| `platformCortex.readinessProbe.enabled`             | Enable readinessProbe on Conduktor Platform Cortex containers                                                                                                        | `true`                                |
| `platformCortex.readinessProbe.initialDelaySeconds` | Initial delay seconds for readinessProbe                                                                                                                             | `30`                                  |
| `platformCortex.readinessProbe.periodSeconds`       | Period seconds for readinessProbe                                                                                                                                    | `10`                                  |
| `platformCortex.readinessProbe.timeoutSeconds`      | Timeout seconds for readinessProbe                                                                                                                                   | `5`                                   |
| `platformCortex.readinessProbe.failureThreshold`    | Failure threshold for readinessProbe                                                                                                                                 | `3`                                   |
| `platformCortex.readinessProbe.successThreshold`    | Success threshold for readinessProbe                                                                                                                                 | `1`                                   |
| `platformCortex.startupProbe.enabled`               | Enable startupProbe on Conduktor Platform Cortex containers                                                                                                          | `false`                               |
| `platformCortex.startupProbe.initialDelaySeconds`   | Initial delay seconds for startupProbe                                                                                                                               | `10`                                  |
| `platformCortex.startupProbe.periodSeconds`         | Period seconds for startupProbe                                                                                                                                      | `10`                                  |
| `platformCortex.startupProbe.timeoutSeconds`        | Timeout seconds for startupProbe                                                                                                                                     | `5`                                   |
| `platformCortex.startupProbe.failureThreshold`      | Failure threshold for startupProbe                                                                                                                                   | `10`                                  |
| `platformCortex.startupProbe.successThreshold`      | Success threshold for startupProbe                                                                                                                                   | `1`                                   |
| `platformCortex.customLivenessProbe`                | Custom livenessProbe that overrides the default one                                                                                                                  | `{}`                                  |
| `platformCortex.customReadinessProbe`               | Custom readinessProbe that overrides the default one                                                                                                                 | `{}`                                  |
| `platformCortex.customStartupProbe`                 | Custom startupProbe that overrides the default one                                                                                                                   | `{}`                                  |
| `platformCortex.resources.limits.cpu`               | CPU limit for the platform cortex container                                                                                                                          | `1000m`                               |
| `platformCortex.resources.limits.memory`            | Memory limit for the container                                                                                                                                       | `500Mi`                               |
| `platformCortex.resources.requests.cpu`             | CPU resource requests                                                                                                                                                | `500m`                                |
| `platformCortex.resources.requests.memory`          | Memory resource requests                                                                                                                                             | `200Mi`                               |
| `platformCortex.podSecurityContext`                 | Conduktor Platform Cortex Pod Security Context                                                                                                                       | `{}`                                  |
| `platformCortex.containerSecurityContext`           | Conduktor Platform Cortex containers' Security Context                                                                                                               | `{}`                                  |
| `platformCortex.existingConfigmap`                  | The name of an existing ConfigMap with your custom configuration for Conduktor Platform Cortex                                                                       | `""`                                  |
| `platformCortex.command`                            | Override default container command (useful when using custom images)                                                                                                 | `[]`                                  |
| `platformCortex.args`                               | Override default container args (useful when using custom images)                                                                                                    | `[]`                                  |
| `platformCortex.hostAliases`                        | Conduktor Platform Cortex pods host aliases                                                                                                                          | `[]`                                  |
| `platformCortex.podLabels`                          | Extra labels for Conduktor Platform Cortex pods                                                                                                                      | `{}`                                  |
| `platformCortex.podAnnotations`                     | Annotations for Conduktor Platform Cortex pods                                                                                                                       | `{}`                                  |
| `platformCortex.podAffinityPreset`                  | Pod affinity preset. Ignored if `platform.affinity` is set. Allowed values: `soft` or `hard`                                                                         | `""`                                  |
| `platformCortex.podAntiAffinityPreset`              | Pod anti-affinity preset. Ignored if `platform.affinity` is set. Allowed values: `soft` or `hard`                                                                    | `soft`                                |
| `platformCortex.nodeAffinityPreset.type`            | Node affinity preset type. Ignored if `platform.affinity` is set. Allowed values: `soft` or `hard`                                                                   | `""`                                  |
| `platformCortex.nodeAffinityPreset.key`             | Node label key to match. Ignored if `platform.affinity` is set                                                                                                       | `""`                                  |
| `platformCortex.nodeAffinityPreset.values`          | Node label values to match. Ignored if `platform.affinity` is set                                                                                                    | `[]`                                  |
| `platformCortex.affinity`                           | Affinity for Conduktor Platform cortex pods assignment                                                                                                               | `{}`                                  |
| `platformCortex.nodeSelector`                       | Node labels for Conduktor Platform Cortex pods assignment                                                                                                            | `{}`                                  |
| `platformCortex.tolerations`                        | Tolerations for Conduktor Platform Cortex pods assignment                                                                                                            | `[]`                                  |
| `platformCortex.updateStrategy.type`                | Conduktor Platform Cortex statefulset strategy type                                                                                                                  | `RollingUpdate`                       |
| `platformCortex.priorityClassName`                  | Conduktor Platform Cortex pods' priorityClassName                                                                                                                    | `""`                                  |
| `platformCortex.topologySpreadConstraints`          | Topology Spread Constraints for pod assignment spread across your cluster among failure-domains. Evaluated as a template                                             | `[]`                                  |
| `platformCortex.schedulerName`                      | Name of the k8s scheduler (other than default) for Conduktor Platform Cortex pods                                                                                    | `""`                                  |
| `platformCortex.terminationGracePeriodSeconds`      | Seconds Redmine pod needs to terminate gracefully                                                                                                                    | `""`                                  |
| `platformCortex.lifecycleHooks`                     | for the Conduktor Platform Cortex container(s) to automate configuration before or after startup                                                                     | `{}`                                  |
| `platformCortex.extraEnvVars`                       | Array with extra environment variables to add to Conduktor Platform Cortex nodes                                                                                     | `[]`                                  |
| `platformCortex.extraEnvVarsCM`                     | Name of existing ConfigMap containing extra env vars for Conduktor Platform Cortex nodes                                                                             | `""`                                  |
| `platformCortex.extraEnvVarsSecret`                 | Name of existing Secret containing extra env vars for Conduktor Platform Cortex nodes                                                                                | `""`                                  |
| `platformCortex.dataVolume`                         | Configure the data volume to store Conduktor Platform Cortex data                                                                                                    | `{}`                                  |
| `platformCortex.tmpVolume`                          | Configure the /tmp volume which store various data related to running services                                                                                       | `{}`                                  |
| `platformCortex.extraVolumes`                       | Optionally specify extra list of additional volumes for the Conduktor Platform Cortex pod(s)                                                                         | `[]`                                  |
| `platformCortex.extraVolumeMounts`                  | Optionally specify extra list of additional volumeMounts for the Conduktor Platform Cortex container(s)                                                              | `[]`                                  |
| `platformCortex.sidecars`                           | Add additional sidecar containers to the Conduktor Platform Cortex pod(s)                                                                                            | `[]`                                  |
| `platformCortex.initContainers`                     | Add additional init containers to the Conduktor Platform Cortex pod(s)                                                                                               | `[]`                                  |
| `platformCortex.service.type`                       | Conduktor Platform Cortex service type                                                                                                                               | `ClusterIP`                           |
| `platformCortex.service.ports.cortex`               | Conduktor Platform Cortex service HTTP port                                                                                                                          | `9009`                                |
| `platformCortex.service.ports.alertmanager`         | Conduktor Platform Cortex AlertManager service HTTP port                                                                                                             | `9010`                                |
| `platformCortex.service.ports.prometheus`           | Conduktor Platform Cortex Prometheus service HTTP port                                                                                                               | `9090`                                |
| `platformCortex.service.nodePorts.cortex`           | Node port for Cortex HTTP                                                                                                                                            | `""`                                  |
| `platformCortex.service.nodePorts.alertmanager`     | Node port for AlertManager HTTP                                                                                                                                      | `""`                                  |
| `platformCortex.service.nodePorts.prometheus`       | Node port for Prometheus HTTP                                                                                                                                        | `""`                                  |
| `platformCortex.service.clusterIP`                  | Conduktor Platform Cortex service Cluster IP                                                                                                                         | `""`                                  |
| `platformCortex.service.loadBalancerSourceRanges`   | Conduktor Platform Cortex service Load Balancer sources                                                                                                              | `[]`                                  |
| `platformCortex.service.externalTrafficPolicy`      | Conduktor Platform Cortex service external traffic policy                                                                                                            | `Cluster`                             |
| `platformCortex.service.labels`                     | Additional custom labels for Conduktor Platform Cortex service                                                                                                       | `{}`                                  |
| `platformCortex.service.annotations`                | Additional custom annotations for Conduktor Platform Cortex service                                                                                                  | `{}`                                  |
| `platformCortex.service.extraPorts`                 | Extra ports to expose in Conduktor Platform Cortex service (normally used with the `sidecars` value)                                                                 | `[]`                                  |
| `platformCortex.service.sessionAffinity`            | Control where client requests go, to the same pod or round-robin                                                                                                     | `None`                                |
| `platformCortex.service.sessionAffinityConfig`      | Additional settings for the sessionAffinity                                                                                                                          | `{}`                                  |


## Snippets

### Console configuration 

If you are looking for additional snippets related to the configuration of 
console, we recommend you to look at our 
[documentation](https://docs.conduktor.io/platform/configuration/configuration-snippets/).

- [Install with a basic SSO configuration](#install-with-a-basic-sso-configuration)
- [Install with a registered kafka cluster](#install-with-a-kafka-cluster)
- [Install with an enterprise license](#install-with-an-enterprise-license)
- [Install without Conduktor monitoring](#install-without-conduktor-monitoring)

### Kubernetes configuration 

- [Install with a PodAffinity](#install-with-a-podaffinity)
- [Install with a Toleration](#install-with-a-toleration)
- [Install with a Self-Signed Certificate](#install-with-self-signed-tls-certificate)
- [Install with a custom service account](#install-with-a-custom-service-account)
- [Install with a AWS EKS IAM Role](#install-with-a-aws-eks-iam-role)
- [Store console data into a PersistentVolume](#store-platform-data-into-a-persistent-volume)

- [Provide credentials as a Kubernetes Secret](#provide-credentials-configuration-as-a-kubernetes-secret)
- [Provide monitoring configuration as a Kubernetes Secret](#provide-monitoring-configuration-as-a-kubernetes-secret)
- [Provide the license as a Kubernetes Secret](#provide-the-license-as-a-kubernetes-secret)
- [Provide the license as a Kubernetes ConfigMap](#provide-console-configuration-as-a-kubernetes-configmap)

- [Provide additional credentials as a Kubernetes Secret](#provide-additional-credentials-as-a-kubernetes-secret)

### Install with an enterprise license

```yaml
config:
  organization:
    name: "my-org"

  admin:
    email: "admin@my-org.com"
    password: "admin"

  database:
    host: ''
    port: 5432
    name: 'postgres'
    username: ''
    password: ''

  license: "${ENTERPRISE_LICENSE}"
```    

### Install with a basic SSO configuration

```yaml
config:
  organization:
    name: "my-org"

  admin:
    email: "admin@my-org.com"
    password: "admin"

  database:
    host: ''
    port: 5432
    name: 'postgres'
    username: ''
    password: ''
  sso:
    oauth2:
      - name: 'auth0'
        default: true
        client-id: <client_id>
        client-secret: <client_secret>
        callback-uri: http://localhost/auth/oauth/callback/auth0
        openid:
          issuer: https://conduktor-staging.eu.auth0.com/
  
  license: '<license_key>'
```

### Install with a kafka cluster

```yaml
config:
  organization:
    name: "my-org"

  admin:
    email: "admin@my-org.com"
    password: "admin"

  database:
    host: ''
    port: 5432
    name: 'postgres'
    username: ''
    password: ''
  clusters:
    - id: my-local-kafka-cluster
      name: My Local Kafka Cluster
      color: '#0013E7'
      bootstrapServers: 'my-bootstrap-server:9092'
      schemaRegistry:
        id: my-schema-registry
        url: 'http://my-schema-registry:8081'
```

### Install without Conduktor monitoring

```yaml
config:
  organization:
    name: "my-org"

  admin:
    email: "admin@my-org.com"
    password: "admin"

  database:
    host: ''
    port: 5432
    name: 'postgres'
    username: ''
    password: ''

platformCortex:
  enabled: false
```

### Provide the license as a Kubernetes Secret

This snippet expects that a *Kubernetes Secret Resource* already exists inside
your cluster with a key named `CDK_LICENSE` containing your license key.


```yaml
# values.yaml
config:
  organization:
    name: "<your_org_name>"

  admin:
    email: "<your_admin_email>"
    password: "<your_admin_password>"
    
  database:
    host: '<postgres_host>'
    port: 5432
    name: '<postgres_database>'
    username: '<postgres_username>'
    password: '<postgres_password>'

  existingLicenseSecret: "<your_secret_name>"
```

### Provide credentials configuration as a Kubernetes Secret

We expect the secret to contain the following keys:

- "CDK_ORGANIZATION_NAME": name of the organization
- "CDK_ADMIN_EMAIL"      : email of the admin user
- "CDK_ADMIN_PASSWORD"   : password of the admin user
- "CDK_DATABASE_PASSWORD": password of the database
- "CDK_DATABASE_USERNAME": username of the database

```yaml
# values.yaml
config:
  existingSecret: "<your_secret_name>"
  database:
    host: ''
    port: 5432
    name: 'postgres'
```

```yaml 
# secrets.yaml
apiVersion: v1
kind: Secret
metadata:
  name: "<your_secret_name>"
type: Opaque
data:
  CDK_ORGANIZATION_NAME: <your_organization_name>
  CDK_ADMIN_EMAIL: <your_admin_email>
  CDK_ADMIN_PASSWORD: <your_admin_password>
  CDK_DATABASE_PASSWORD: <your_database_password>
  CDK_DATABASE_USERNAME: <your_database_username>
```

### Provide monitoring configuration as a Kubernetes Secret

We expect the secret to contain the following keys:
- For S3 like storage:
  - "CDK_MONITORING_STORAGE_S3_ACCESSKEYID" : S3 access key
  - "CDK_MONITORING_STORAGE_S3_SECRETACCESSKEY" : S3 secret access key
- For GCS like storage:
  - "CDK_MONITORING_STORAGE_GCS_SERVICEACCOUNT" : GCS service account JSON representing either client_credentials.json file or a service account key file.
- For Azure like storage:
  - "CDK_MONITORING_STORAGE_AZURE_ACCOUNTNAME" : Azure account name
  - "CDK_MONITORING_STORAGE_AZURE_ACCOUNTKEY" : Azure account key
- For Swift like storage:
  - "CDK_MONITORING_STORAGE_SWIFT_PASSWORD" : Swift user password
  - "CDK_MONITORING_STORAGE_SWIFT_USERID" OR "CDK_MONITORING_STORAGE_SWIFT_USERNAME": Swift user id or name

```yaml
# values.yaml
monitoringConfig:
  existingSecret: "<your_secret_name>"
  storage:
    s3:
      endpoint: "s3.eu-west-1.amazonaws.com"
      bucket: "conduktor"
```

```yaml
# secrets.yaml
apiVersion: v1
kind: Secret
metadata:
  name: "<your_secret_name>"
type: Opaque
data:
  CDK_MONITORING_STORAGE_S3_ACCESSKEYID: <your_s3_access_key>
  CDK_MONITORING_STORAGE_S3_SECRETACCESSKEY: <your_s3_secret_access_key>
```

### Store platform data into a Persistent Volume

```yaml
# values.yaml
config:
  organization:
    name: "<your_org_name>"

  admin:
    email: "<your_admin_email>"
    password: "<your_admin_password>"

  database:
    host: '<postgres_host>'
    port: 5432
    name: '<postgres_database>'
    username: '<postgres_username>'
    password: '<postgres_password>'

platform:
  dataVolume:
    persistentVolumeClaim:
      claimName: data-pv-claim
  tmpVolume:
    persistentVolumeClaim:
      claimName: tmp-pv-claim

platformCortex:
  enabled: true
  dataVolume:
    persistentVolumeClaim:
      claimName: monitoring-data-pv-claim
  tmpVolume:
    persistentVolumeClaim:
      claimName: monitoring-tmp-pv-claim
```

### Install with a PodAffinity

```yaml
config:
  organization:
    name: "my-org"

  admin:
    email: "admin@my-org.com"
    password: "admin"

  database:
    host: ''
    port: 5432
    name: 'postgres'
    username: ''
    password: ''

platform:
  affinity:
    podAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        - labelSelector:
            matchExpressions:
              - key: security
                operator: In
                values:
                  - S1
          topologyKey: topology.kubernetes.io/zone

platformCortex:
  enabled: true
  affinity:
    podAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        - labelSelector:
            matchExpressions:
              - key: security
                operator: In
                values:
                  - S1
          topologyKey: topology.kubernetes.io/zone
```

### Provide console configuration as a Kubernetes ConfigMap

**NOTE:** We recommend to be using a secret (see [snippet](#provide-credentials-configuration-as-a-kubernetes-secret))
in addition to the ConfigMap in order to protect your credentials.

The ConfigMap is expected to contain a key `platform-config.yaml` which got 
the console configuration in YAML format.

```yaml
# values.yaml
config:
  # We highly recommend you to be using both the secret and the ConfigMap
  # check our snippet 'Provide credentials configuration as a Kubernetes Secret'
  existingSecret: "<your_secret_name>"
    
platform:
  existingConfigmap: "<your_configmap_name>"
```

```yaml
# platform-config.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: "<your_configmap_name>"
data:
  platform-config.yaml: |
    database:
      host: '<postgres_host>'
      port: 5432
      name: '<postgres_database>'
```

### Provide additional credentials as a Kubernetes Secret

In case our helm chart doesn't protect all the credentials you need, you can
use this method to provide additional credentials through a Kubernetes 
Secret Resource you previously created. You can have this case for LDAP 
credentials, or for SSO credentials for example.

The keys of your secret will be used as environment variables in the
console pod. Be sure to check available [environment variables](https://docs.conduktor.io/platform/configuration/env-variables/)
in our documentation.

```yaml
config:
  organization:
    name: "my-org"

  admin:
    email: "admin@my-org.com"
    password: "admin"

  database:
    host: ''
    port: 5432
    name: 'postgres'
    username: ''
    password: ''

platform:
  extraEnvVarsSecret: "<your_secret_name>"
platformCortex:
  extraEnvVarsSecret: "<your_secret_name>"
```

### Install with a toleration

```yaml
config:
  organization:
    name: "my-org"

  admin:
    email: "admin@my-org.com"
    password: "admin"

  database:
    host: ''
    port: 5432
    name: 'postgres'
    username: ''
    password: ''

  platform:
    external:
      url: "https://platform.local"
    https:
      selfSigned: true
platform:
  tolerations:
    - key: "donotschedule"
      operator: "Exists"
      effect: "NoSchedule"

platformCortex:
  enabled: true
  tolerations:
    - key: "donotschedule"
      operator: "Exists"
      effect: "NoSchedule"
```

### Install with Self-Signed TLS certificate

```yaml
config:
  organization:
    name: "my-org"

  admin:
    email: "admin@my-org.com"
    password: "admin"

  database:
    host: ''
    port: 5432
    name: 'postgres'
    username: ''
    password: ''

  platform:
    external:
      url: "https://platform.local"
    https:
      selfSigned: true
```

### Install with a custom TLS certificate on the platform Pod

```yaml
config:
  organization:
    name: "my-org"

  admin:
    email: "admin@my-org.com"
    password: "admin"

  database:
    host: ''
    port: 5432
    name: 'postgres'
    username: ''
    password: ''

  platform:
    external:
      url: "https://platform.local"
    https:
      selfSigned: false
      existingSecret: "platform-tls"
ingress:
  secrets:
    - name: platform-tls
      certificate: |-
        -----BEGIN CERTIFICATE-----
        ...
        -----END CERTIFICATE-----
      key: |-
        -----BEGIN PRIVATE KEY-----
        ...
        -----END PRIVATE KEY-----
```

### Install with a custom service account

```yaml
config:
  organization:
    name: "my-org"

  admin:
    email: "admin@my-org.com"
    password: "admin"

  database:
    host: ''
    port: 5432
    name: 'postgres'
    username: ''
    password: ''

serviceAccount:
  create: false
  name: "my-service-account"
```

### Install with a AWS EKS IAM Role

**NOTE:** Service account are shared between Conduktor Console and Cortex pods.

```yaml
config:
  organization:
    name: "my-org"

  admin:
    email: "admin@my-org.com"
    password: "admin"

  database:
    host: ''
    port: 5432
    name: 'postgres'
    username: ''
    password: ''

serviceAccount:
  annotations:
    eks.amazonaws.com/role-arn: "arn:aws:iam::123456789012:role/my-role"
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Troubleshooting

For guides and advanced help, please refer to our
[documentation](https://docs.conduktor.io/platform/installation/get-started/kubernetes),
or to our charts `README`.

<p align="right">(<a href="#readme-top">back to top</a>)</p>
