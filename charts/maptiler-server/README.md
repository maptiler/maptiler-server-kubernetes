# MapTiler Server

[MapTiler Server](https://www.maptiler.com/server/) - self-hosting OpenStreetMap world maps and maps made with MapTiler.

## Requirements

- Running Kubernetes cluster with at least 1 node.
- Running [Ingress controller](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/).
- (Optional) Persistent Volume type supporting [ReadWriteMany](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes) access mode to be able to share tileset data and configuration in multi-instance deployments.

## Usage

[Helm](https://helm.sh) must be installed to use the chart.
Please refer to Helm's [documentation](https://helm.sh/docs/) to get started.

### Installing the Chart

To install the chart with the release name `maptiler-server-app`:

```console
helm repo add maptiler https://labs.maptiler.com/maptiler-server-kubernetes/
helm install maptiler-server-app maptiler/maptiler-server
```

The command deploys MapTiler Server on the Kubernetes cluster in the default configuration. The section lists the parameters that can be configured during installation.

### Uninstalling the Chart

To uninstall the `maptiler-server-app` deployment:

```console
helm uninstall maptiler-server-app
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

Below are the supported configuration options that can be overridden or customized in `values.yaml`:

| Parameter                                 | Description                                                         | Default                                                                                                          |
|-------------------------------------------|---------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `replicaCount`                            | Number of pods                                                      | `1`                                                                                                              |
| `image.repository`                        | Image repository                                                    | `maptiler/server`                                                                                                |
| `image.tag`                               | Overrides the image tag whose default is the chart appVersion.      | `""`                                                                                                             |
| `image.pullPolicy`                        | Image pull policy                                                   | `IfNotPresent`                                                                                                   |
| `imagePullSecrets`                        | Image pull secrets (can be templated)                               | `[]`                                                                                                             |
| `nameOverride`                            | Overrides the default chart name                                    | `""`                                                                                                             |
| `fullnameOverride`                        | Overrides the default chart full name                               | `""`                                                                                                             |
| `podAnnotations`                          | Pod annotations                                                     | `{}`                                                                                                             |
| `podLabels`                               | Pod labels                                                          | `{}`                                                                                                             |
| `podSecurityContext`                      | Pod securityContext                                                 | `{}`                                                                                                             |
| `securityContext`                         | Deployment securityContext                                          | `{}`                                                                                                             |
| `service.type`                            | Kubernetes service type                                             | `ClusterIP`                                                                                                      |
| `service.port`                            | Kubernetes port where service is exposed                            | `80`                                                                                                             |
| `ingress.enabled`                         | Enables Ingress                                                     | `false`                                                                                                          |
| `ingress.className`                       | Ingress Class Name. MAY be required for Kubernetes versions >= 1.18 | `""`                                                                                                             |
| `ingress.annotations`                     | Ingress annotations (values are templated)                          | `{}`                                                                                                             |
| `ingress.hosts`                           | Ingress hosts (can be templated)                                    | `{ "hosts": [{ "host": "maps.company.com", "paths": [{ "path": "/", "pathType": "ImplementationSpecific"}] }] }` |
| `ingress.tls`                             | Ingress TLS configuration                                           | `[]`                                                                                                             |
| `resources`                               | CPU/Memory resource requests/limits                                 | `{}`                                                                                                             |
| `livenessProbe`                           | Liveness Probe settings                                             | `{ "httpGet": { "path": "/", "port": http } }`                                                                   |
| `readinessProbe`                          | Readiness Probe settings                                            | `{ "httpGet": { "path": "/", "port": http } }`                                                                   |
| `autoscaling.enabled`                     | Enables Autoscaling                                                 | `false`                                                                                                          |
| `autoscaling.minReplicas`                 | Minimal number of pods                                              | `1`                                                                                                              |
| `autoscaling.maxReplicas`                 | Maximal number of pods                                              | `100`                                                                                                            |
| `autoscaling.targetCPUUtilizationPercentage` | Target CPU utilization percentage                                   | `80`                                                                                                             |
| `autoscaling.targetMemoryUtilizationPercentage` | Target Memory utilization percentage                                | `nil`                                                                                                            |
| `storage.existingClaim`                   | Use an existing PVC. If not set, it will create new volume claim    | `false`                                                                                                          |
| `storage.storageClassName`                | Type of persistent volume claim                                     | `manual`                                                                                                         |
| `storage.size`                            | Size of persistent volume claim                                     | `20Gi`                                                                                                           |
| `storage.nfs`                             | Whether storage is NFS                                              | `false`                                                                                                          |
| `volumes`                                 | Additional volumes                                                  | `[]`                                                                                                             |
| `volumeMounts`                            | Additional volume mounts                                            | `[]`                                                                                                             |
| `nodeSelector`                            | Node labels for pod assignment                                      | `{}`                                                                                                             |
| `tolerations`                             | Toleration labels for pod assignment                                | `[]`                                                                                                             |
| `affinity`                                | Affinity settings for pod assignment                                | `{}`                                                                                                             |
| `maptilerServer.adminPassword`            | Password for MapTiler Server Admin interface                        | `admin123`                                                                                                       |
| `maptilerServer.port`                     | MapTiler Server Port                                                | `3650`                                                                                                           |
| `maptilerServer.licenseKey`               | MapTiler Server License Key                                         | `""`                                                                                                             |
| `maptilerServer.licenseServer`            | MapTiler Server License Server URL                                  | `""`                                                                                                             |
| `maptilerServer.rasterization`            | Enables map rasterization                                           | `true`                                                                                                           |
| `maptilerServer.withAdmin`                | Enables Admin interface                                             | `true`                                                                                                           |
| `maptilerServer.workDir`                  | MapTiler Server working directory with config and tilesets          | `/data`                                                                                                          |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
helm install maptiler-server-app --set image.tag=4.4.0 maptiler/maptiler-server
```

The above command sets the MapTiler Server image's tag to `4.4.0`.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```console
helm install maptiler-server-app -f values.yaml maptiler/maptiler-server
```

## Examples

You can find configuration examples in our [Documentation Portal](https://docs.maptiler.com/guides/self-hosting/map-server/?utm_source=artifactory&utm_medium=description%20%7C%20documentation&utm_content=documentation
).

## ChangeLog

### 1.1.1

- MapTiler Server release 4.6.1

### 1.1.0

- MapTiler Server release 4.6.0

### 1.0.0

- Initial release of the Helm Chart
