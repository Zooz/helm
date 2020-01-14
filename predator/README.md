# Predator Helm Chart

         
[Predator](https://predator.dev) is an [open-source](https://github.com/Zooz/predator) distributed performance testing platform for APIs.
                                    
Predator manages the entire lifecycle of stress-testing servers, from creating performance tests, to running these tests on a scheduled and on-demand basis, and finally viewing the test results in a highly informative and live report.

It has a simple, one-click installation, built with support for Kubernetes, DC/OS and Docker Engine, and can persist the created performance tests and their reports in 5 different databases. It also supports running distributed load out of the box. Bootstrapped with a user-friendly UI alongside a simple REST API, Predator helps developers simplify the performance testing regime.

## TL;DR;

```console
$ helm install predator
```

## Installing the Chart

To install the chart with the release name `my-release`:

```console
$ helm install --name my-release predator
```

The command deploys predator on the Kubernetes cluster with the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

## Uninstalling the Chart

To uninstall/delete the my-release deployment:

```console
$ helm delete --purge my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

By default configuration, `Predator` runs with sqlite as its storage without persistence.
It is possible to run with persistence with the following configuration:

`Predator` with SQLite persisted storage 
```console
$ helm install --name my-release predator --set persistence.enabled=true
```

`Predator` supports other storage engines like Cassandra, postgresSQL, MySql and SQL Server.
If you want to use any of this database just install with these configuration:

```console
$ helm install --name my-release predator --set database.type=MYSQL,database.name=predator,database.address=mysql.default,database.password=cHJlZGF0b3I=,database.password=cHJlZGF0b3I=
```
> **Note**:
>
> database.username & database.password should be provided in base 64
>

The following tables lists the configurable parameters of the Predator chart and their default values.


| Parameter            | Description                                                      | Default                                      |
| -------------------- | ---------------------------------------------------------------- | -------------------------------------------- |
| `image.repository`   | container image                                                  | `zooz/predator                        `      |
| `image.tag`          | container image tag                                              | `Latest`                                     |
| `image.pullPolicy`   | Operator container image pull policy                             | `Always`                                     |
| `nameOverride`       | Override the app name                                            |                                              |
| `fullnameOverride`   | Override the app full name                                       |                                              |
| `resources`          | Set the resource to be allocated and allowed for the Pods        | `{}`                                         |
| `ingress.enabled`    | If true, an ingress is be created                                | `false`
| `ingress.annotations`| Annotations for the ingress                                      | `{}`
| `ingress.path`       | Path for backend                                                 | `/`
| `ingress.hosts`      | A list of hosts for the ingresss                                 | `['predator.local']`
| `ingress.tls`        | Ingress TLS configuration                                        | `[]`
| `nodeSelector`       | Node labels for pod assignment                                   | `{}`                                         |
| `tolerations`        | Tolerations for pod assignment                                   | `[]`                                         |
| `affinity`           | Affinity settings for pod assignment                             | `{}`                                         |
| `service.type`       | type of controller service to create                             | `ClusterIP`
| `database.type`      | chosen storage backend, Optional Values: SQLITE, CASSANDRA, MYSQL, POSTGRES AND SQLSERVER | `SQLITE`
| `datbase.name`       | the name of the database/keyspace with the selected database type|
| `database.username`  | Database username (in base64)                                    |                                              |
| `database.password`  | Database password (in base64)                                    |                                              |
| `database.cassandra.replicationFactor`  | replication factor for cassandra              | `1`                                          |
| `database.cassandra.keySpaceStrategy`  | key space strategy for cassandra               | `SimpleStrategy`                             |
| `database.cassandra.localDataCenter`  | local data center for cassandra                                                                |
| `kubernetesUrl    `  | URL of kubernetes, Predator should be able to communicate with this url. | https://kubernetes.default.svc                                                              |
| `persistence.enabled`                     | Use persistent volume to store data           | `false`                                                 |
| `persistence.size`                        | Size of persistent volume claim               | `2Gi`                                                  |
| `persistence.existingClaim`               | Use an existing PVC to persist data           | `nil`                                                   |
| `persistence.storageClassName`            | Name of StorageClass resource               | `nil`                                                   |
| `persistence.accessModes`                 | Persistence access modes                      | `[ReadWriteOnce]`                                       |
