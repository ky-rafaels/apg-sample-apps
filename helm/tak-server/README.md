# TAK Server Helm Chart

This Helm chart deploys TAK Server on a Kubernetes cluster.

## Prerequisites

- Kubernetes cluster
- Helm 3
- Docker images built and available

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
helm install my-release ./helm/tak-server
```

## Uninstalling the Chart

To uninstall the chart:

```bash
helm uninstall my-release
```

## Configuration

The following table lists the configurable parameters of the TAK Server chart and their default values.

| Parameter | Description | Default |
|-----------|-------------|---------|
| `namespace` | Namespace to deploy into | `takserver` |
| `db.image` | DB image | `takserver-db:latest` |
| `db.storage` | DB storage size | `10Gi` |
| `db.password` | DB password | `password` |
| `takserver.image` | TAK Server image | `takserver:latest` |
| `takserver.replicas` | Number of TAK Server replicas | `1` |
| `takserver.config.coreConfig` | CoreConfig.xml content | See values.yaml |
| `httproute.enabled` | Enable HTTPRoute | `true` |
| `httproute.host` | HTTPRoute host | `takserver.example.com` |
| `httproute.gatewayName` | Gateway name | `my-gateway` |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart.

```bash
helm install my-release ./helm/tak-server -f values.yaml
```