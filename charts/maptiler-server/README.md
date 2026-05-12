<img src="https://www.maptiler.com/styles/style/logo/maptiler-logo-adaptive.svg?123#maptilerLogo" alt="Company Logo" height="32"/>

# MapTiler Server

[MapTiler Server](https://www.maptiler.com/server/) - self-hosting OpenStreetMap world maps and maps made with MapTiler.

[![](https://img.shields.io/badge/Artifact%20Hub-maptiler-f2f6ff?style=for-the-badge&labelColor=D3DBEC&logo=artifacthub&logoColor=333359)](https://artifacthub.io/packages/search?repo=maptiler)

---

📖 [Documentation](https://docs.maptiler.com/guides/self-hosting/map-server/) &nbsp; 🌐 [Website](https://www.maptiler.com/server/)

---

<br>

<details> <summary><b>Table of Contents</b></summary>
<ul>
<li><a href="#-installation">Installation</a></li>
<li><a href="#-examples">Examples</a></li>
<li><a href="#-api-reference">API Reference</a></li>
<li><a href="#configuration">Configuration</a></li>
<li><a href="#changelog">ChangeLog</a></li>
<li><a href="#-support">Support</a></li>
<li><a href="#-contributing">Contributing</a></li>
<li><a href="#-license">License</a></li>
<li><a href="#-acknowledgements">Acknowledgements</a></li>
</ul>
</details>

<br>

## 📦 Installation

To install the chart with the release name `maptiler-server-app`:

```shell
helm repo add maptiler https://labs.maptiler.com/maptiler-server-kubernetes/
helm install maptiler-server-app maptiler/maptiler-server
```

The command deploys MapTiler Server on the Kubernetes cluster in the default configuration. The section lists the parameters that can be configured during installation.

### Requirements

[Helm](https://helm.sh) must be installed to use the chart.
Please refer to Helm's [documentation](https://helm.sh/docs/) to get started.

- Running Kubernetes cluster with at least 1 node.
- Running [Ingress controller](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/).
- (Optional) Persistent Volume type supporting [ReadWriteMany](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes) access mode to be able to share tileset data and configuration in multi-instance deployments.

### Uninstalling the Chart

To uninstall the `maptiler-server-app` deployment:

```shell
helm uninstall maptiler-server-app
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

<br>

## 💡 Examples

You can find configuration examples in our [Documentation Portal](https://docs.maptiler.com/guides/self-hosting/map-server/?utm_source=artifactory&utm_medium=description%20%7C%20documentation&utm_content=documentation).

<br>

## 📘 API Reference

For detailed guides, API reference, and advanced examples, visit our comprehensive documentation:

[API documentation](https://docs.maptiler.com/guides/self-hosting/map-server/#reference)

<br>

## Configuration

Below are the supported configuration options that can be overridden or customized in `values.yaml`:

| Parameter                                       | Description                                                         | Default                                                                                                          |
| ----------------------------------------------- | ------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| `replicaCount`                                  | Number of pods                                                      | `1`                                                                                                              |
| `image.repository`                              | Image repository                                                    | `maptiler/server`                                                                                                |
| `image.tag`                                     | Overrides the image tag whose default is the chart appVersion.      | `""`                                                                                                             |
| `image.pullPolicy`                              | Image pull policy                                                   | `IfNotPresent`                                                                                                   |
| `imagePullSecrets`                              | Image pull secrets (can be templated)                               | `[]`                                                                                                             |
| `nameOverride`                                  | Overrides the default chart name                                    | `""`                                                                                                             |
| `fullnameOverride`                              | Overrides the default chart full name                               | `""`                                                                                                             |
| `podAnnotations`                                | Pod annotations                                                     | `{}`                                                                                                             |
| `podLabels`                                     | Pod labels                                                          | `{}`                                                                                                             |
| `podSecurityContext`                            | Pod securityContext                                                 | `{}`                                                                                                             |
| `securityContext`                               | Deployment securityContext                                          | `{}`                                                                                                             |
| `service.type`                                  | Kubernetes service type                                             | `ClusterIP`                                                                                                      |
| `service.port`                                  | Kubernetes port where service is exposed                            | `80`                                                                                                             |
| `ingress.enabled`                               | Enables Ingress                                                     | `false`                                                                                                          |
| `ingress.className`                             | Ingress Class Name. MAY be required for Kubernetes versions >= 1.18 | `""`                                                                                                             |
| `ingress.annotations`                           | Ingress annotations (values are templated)                          | `{}`                                                                                                             |
| `ingress.hosts`                                 | Ingress hosts (can be templated)                                    | `{ "hosts": [{ "host": "maps.company.com", "paths": [{ "path": "/", "pathType": "ImplementationSpecific"}] }] }` |
| `ingress.tls`                                   | Ingress TLS configuration                                           | `[]`                                                                                                             |
| `resources`                                     | CPU/Memory resource requests/limits                                 | `{}`                                                                                                             |
| `livenessProbe`                                 | Liveness Probe settings                                             | `{ "httpGet": { "path": "/", "port": http } }`                                                                   |
| `readinessProbe`                                | Readiness Probe settings                                            | `{ "httpGet": { "path": "/", "port": http } }`                                                                   |
| `autoscaling.enabled`                           | Enables Autoscaling                                                 | `false`                                                                                                          |
| `autoscaling.minReplicas`                       | Minimal number of pods                                              | `1`                                                                                                              |
| `autoscaling.maxReplicas`                       | Maximal number of pods                                              | `100`                                                                                                            |
| `autoscaling.targetCPUUtilizationPercentage`    | Target CPU utilization percentage                                   | `80`                                                                                                             |
| `autoscaling.targetMemoryUtilizationPercentage` | Target Memory utilization percentage                                | `nil`                                                                                                            |
| `storage.storageClassName`                      | Type of persistent volume claim                                     | `manual`                                                                                                         |
| `storage.size`                                  | Size of persistent volume claim                                     | `20Gi`                                                                                                           |
| `storage.nfs`                                   | Whether storage is NFS                                              | `false`                                                                                                          |
| `volumes`                                       | Additional volumes                                                  | `[]`                                                                                                             |
| `volumeMounts`                                  | Additional volume mounts                                            | `[]`                                                                                                             |
| `nodeSelector`                                  | Node labels for pod assignment                                      | `{}`                                                                                                             |
| `tolerations`                                   | Toleration labels for pod assignment                                | `[]`                                                                                                             |
| `affinity`                                      | Affinity settings for pod assignment                                | `{}`                                                                                                             |
| `maptilerServer.adminPassword`                  | Password for MapTiler Server Admin interface                        | `admin123`                                                                                                       |
| `maptilerServer.port`                           | MapTiler Server Port                                                | `3650`                                                                                                           |
| `maptilerServer.licenseKey`                     | MapTiler Server License Key                                         | `""`                                                                                                             |
| `maptilerServer.licenseServer`                  | MapTiler Server License Server URL                                  | `""`                                                                                                             |
| `maptilerServer.rasterization`                  | Enables map rasterization                                           | `true`                                                                                                           |
| `maptilerServer.withAdmin`                      | Enables Admin interface                                             | `true`                                                                                                           |
| `maptilerServer.workDir`                        | MapTiler Server working directory with config and tilesets          | `/data`                                                                                                          |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```shell
helm install maptiler-server-app --set image.tag=4.4.0 maptiler/maptiler-server
```

The above command sets the MapTiler Server image's tag to `4.4.0`.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```shell
helm install maptiler-server-app -f values.yaml maptiler/maptiler-server
```

<br>

## ChangeLog

### 1.3.0

- MapTiler Server release 4.8.0

### 1.2.1

- MapTiler Server release 4.7.1

### 1.2.0

- MapTiler Server release 4.7.0

### 1.1.2

- MapTiler Server release 4.6.2

### 1.1.1

- MapTiler Server release 4.6.1

### 1.1.0

- MapTiler Server release 4.6.0

### 1.0.0

- Initial release of the Helm Chart

<br>

## 💬 Support

- 📚 [Documentation](https://docs.maptiler.com/guides/self-hosting/map-server/) - Comprehensive guides and API reference
- ✉️ [Contact us](https://maptiler.com/contact) - Get in touch or submit a request
- 🐦 [Twitter/X](https://twitter.com/maptiler) - Follow us for updates

<br>

---

<br>

## 🤝 Contributing

We love contributions from the community! Whether it's bug reports, feature requests, or pull requests, all contributions are welcome:

- Fork the repository and create your branch from `main`
- If you've added code, add tests that cover your changes
- Ensure your code follows our style guidelines
- Give your pull request a clear, descriptive summary
- Open a Pull Request with a comprehensive description

<br>

## 📄 License

Checkout the [MapTiler Server & Data Terms and Conditions](https://www.maptiler.com/terms/server-data/).

[**License activation**](https://docs.maptiler.com/guides/self-hosting/map-server/#license)

<br>

## 🙏 Acknowledgements

This project is built on the shoulders of giants:

- [MapTiler Server](https://www.maptiler.com/server/) – Map server for self-hosting of maps
- [Kubernetes](https://kubernetes.io/) – Production-Grade Container Orchestration

<br>

<p align="center" style="margin-top:20px;margin-bottom:20px;"> <a href="https://cloud.maptiler.com/account/keys/" style="display:inline-block;padding:12px 32px;background:#F2F6FF;color:#000;font-weight:bold;border-radius:6px;text-decoration:none;"> Get Your API Key <sup style="background-color:#0000ff;color:#fff;padding:2px 6px;font-size:12px;border-radius:3px;">FREE</sup><br /> <span style="font-size:90%;font-weight:400;">Start building with 100,000 free map loads per month ・ No credit card required.</span> </a> </p>

<br>

<p align="center"> 💜 Made with love by the <a href="https://www.maptiler.com/">MapTiler</a> team <br />
<p align="center">
  <a href="https://www.maptiler.com/server/">Website</a> •
  <a href="https://docs.maptiler.com/guides/self-hosting/map-server/">Documentation</a> •
  <a href="https://artifacthub.io/packages/helm/maptiler/maptiler-server">ArtifactHub</a>
</p>
