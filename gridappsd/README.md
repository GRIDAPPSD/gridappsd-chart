# GridAPPS-D Helm Chart

## Introduction

This chart bootstraps a [GridAPPS-D](https://gridapps-d.org) deployment on a [Kubernetes](https://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Prerequisites

- Kubernetes 1.23+
- Helm 3.8.0+

## Installing the Chart

To install the chart with the release name `my-release`:

```console
helm install my-release oci://REGISTRY_NAME/REPOSITORY_NAME/mysql
```

> Note: You need to substitute the placeholders `REGISTRY_NAME` and `REPOSITORY_NAME` with a reference to your Helm chart registry and repository. For example, in the case of Bitnami, you need to use `REGISTRY_NAME=registry-1.docker.io` and `REPOSITORY_NAME=bitnamicharts`.

These commands deploy GridAPPS-D on the Kubernetes cluster in the default configuration. The [Parameters](#parameters) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Parameters

This chart uses standard parameters specified in the Helm template created by the [`helm create`](https://helm.sh/docs/helm/helm_create/) command.

The following tables outline custom parameters used specifically for this chart.

### GridAPPS-D parameters

| Name                                | Description                                    | Value   |
| ----------------------------------- | ---------------------------------------------- | ------- |
| `gridappsd.config.autostart`        | Autostart GridAPPS-D                           | `true`  |
| `gridappsd.config.debug`            | Configure GridAPPS-D in debug mode             | `false` |
| `gridappsd.service.stomp.port`      | TCP port for STOMP                             | `61613` |
| `gridappsd.service.websockets.port` | TCP port for Websockets                        | `61614` |
| `gridappsd.service.openwire.port`   | TCP port for Openwire                          | `61616` |
| `gridappsd.service.jdwp.port`       | TCP port for Java Debug Wire Protocol (JDWP)   | `8000`  |

See the [values.yaml](./values.yaml) file for descriptions of the other chart parameters that apply for the GridAPPS-D service.

### Blazegraph parameters

Blazegraph is packaged as a local sub chart.  See the [values.yaml](./charts/blazegraph/values.yaml) file for descriptions of the chart parameters that apply for the Blazegraph service.

### InfluxDB parameters

InfluxDB is packaged as a local sub chart with the following custom configuration parameters:

| Name                  | Description              | Value     |
| --------------------- | ------------------------ | --------- |
| `blazegraph.database` | Blazegraph database name | `proven`  |

See the [values.yaml](./charts/influxdb/values.yaml) file for descriptions of the standard chart parameters that apply for the InfluxDB service.

### Proven parameters

Proven is packaged as a local sub chart with the following custom configuration parameters:

| Name                                  | Description             | Value                  |
| ------------------------------------- | ----------------------- | ---------------------- |
| `proven.config.influxdb.enabled`      | Enables use of InfluxDB | `true`                 |
| `proven.config.influxdb.url`          | InfluxDB URL            | `http://influxdb:8086` |
| `proven.config.influxdb.database`     | InfluxDB database       | `proven`               |
| `proven.config.influxdb.username`     | InfluxDB user name      | `root`                 |
| `proven.config.influxdb.password`     | InfluxDB password       | `root`                 |
| `proven.config.influxdb.rootPassword` | InfluxDB root password  | `autogen`              |

See the [values.yaml](./charts/proven/values.yaml) file for descriptions of the standard chart parameters that apply for the InfluxDB service.

### Viz parameters

Viz is packaged as a local sub chart with the following custom configuration parameters:

| Name                      | Description                      | Value             |
| --------------------------| -------------------------------- | ----------------- |
| `viz.config.gridappsdUrl` | GridAPPS-D service websocket URL | `localhost:61614` |

See the [values.yaml](./charts/viz/values.yaml) file for descriptions of the standard chart parameters that apply for Viz.
