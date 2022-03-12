<!--- app-name: swe-db -->

# Spring Web Essentials Database Helm Chart

__Description:__ A Helm chart for the Spring Web Essentials database

                           
## TL;DR

```console
helm repo add jeffs-charts https://jeffrey-anderson.github.io/helm-charts/

helm install perky-porcupine jeffs-charts/swe-db
```

## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+
- PV provisioner support in the underlying infrastructure
- ReadWriteMany volumes for deployment scaling

## Installing the Chart

To install the chart with the release name `perky-porcupine`:

```console
helm install perky-porcupine jeffs-charts/swe-db
```


## Uninstalling the Chart

To uninstall/delete the `perky-porcupine` deployment:

```console
helm delete perky-porcupine
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Parameters

| Name                      | Description                                     | Value |
| ------------------------- | ----------------------------------------------- | ----- |
| `postgresDbPassword` | base64 encoded password for the database | `VXNlLWEtQmV0dGVyLVBhc3N3MHJk`
| `initContainers.runInit` | Toggle init processing | `false` |
| `initCommand` | Command to run when initializing the database | "wget -q -O /sql/init-swe-db.sh https://raw.githubusercontent.com/jeffrey-anderson/intro-to-kubernetes/main/swe/init-swe-db.sh 2> /dev/null" |
| `service.type` | How the database is exposed | `NodePort` |
| `service.port` | Cluster IP port where the database is listening | 5432 |
| `service.nodePort` | Cluster node port port where the database is listening | 30432 |
| `replicaCount`            | Number of replicas to run                       | `1`  |


Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
helm install perky-porcupine --set initContainers.runInit=true jeffs-charts/swe-db
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```console
helm install perky-porcupine -f values.yaml jeffs-charts/swe-db
```

> **Tip**: You can use the default [values.yaml](values.yaml)

## Configuration and installation details

### [Rolling VS Immutable tags](https://docs.bitnami.com/containers/how-to/understand-rolling-tags-containers/)

It is strongly recommended to use immutable tags in a production environment. This ensures your deployment does not change automatically if the same tag is updated with a different image.

