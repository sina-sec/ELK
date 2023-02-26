# Logstash

![logstash](https://user-images.githubusercontent.com/62883434/221395304-bf82abf5-d138-4f29-ba75-c121c4d54b8e.png)


[![Build](https://github.com/logfellow/logstash-logback-encoder/workflows/build/badge.svg?branch=main)](https://github.com/logfellow/logstash-logback-encoder/actions)
![68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f616374696f6e732f776f726b666c6f772f7374617475732f73696d706c652d69636f6e732f73696d706c652d69636f6e732f7665726966792e796d6c3f6272616e63683d646576656c6f](https://user-images.githubusercontent.com/62883434/221395341-6eebf67c-ac10-4f5b-b348-bdc994998ec7.svg)
![68747470733a2f2f636972636c6563692e636f6d2f67682f68656c6d2f68656c6d2e7376673f7374796c653d736869656c64](https://user-images.githubusercontent.com/62883434/221395348-82a3d61f-167c-43be-ad55-6c2d7625bfc1.svg)
![68747470733a2f2f72656164746865646f63732e6f72672f70726f6a656374732f656c6b2d646f636b65722f62616467652f3f76657273696f6e3d6c6174657374](https://user-images.githubusercontent.com/62883434/221395351-5bf82f3d-3156-4bee-8be4-ddc74b6c0f9d.svg)
[![Build Status](https://img.shields.io/jenkins/s/https/devops-ci.elastic.co/job/elastic+helm-charts+main.svg)](https://devops-ci.elastic.co/job/elastic+helm-charts+main/) [![Artifact HUB](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/elastic)](https://artifacthub.io/packages/search?repo=elastic)




## Logstash Introduction
Logstash is an open source data collection engine with real-time pipelining capabilities.
Logstash can dynamically unify data from disparate sources and normalize the data into destinations of your choice.
Cleanse and democratize all your data for diverse advanced downstream analytics and visualization use cases.
While Logstash originally drove innovation in log collection, its capabilities extend well beyond that use case.
Any type of event can be enriched and transformed with a broad array of input, filter, and output plugins, with many native codecs further simplifying the ingestion process.
Logstash accelerates your insights by harnessing a greater volume and variety of data.

![logstash (1)](https://user-images.githubusercontent.com/62883434/221395320-b827f949-742b-49b5-b1a9-ac6a95ea54d5.png)

## Getting Started with Logstash
This section guides you through the process of installing Logstash and verifying that everything is running properly.
After learning how to stash your first event, you go on to create a more advanced pipeline that takes Apache web logs as input, parses the logs, and writes the parsed data to an Elasticsearch cluster.
Then you learn how to stitch together multiple input and output plugins to unify data from a variety of disparate sources.
##### link for Logstash : https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html/  

## Installing

### Install a released version using the Helm repository

* Add the Elastic Helm charts repo:
`helm repo add elastic https://helm.elastic.co`

* Install it: `helm install logstash -f values.yaml elastic/logstash -n NAMESPACE`

### For create new NAMESPACE and replace to command [ -n NAMESPCE ]
* ` kubectl create ns ELK `  
*  Use your specific name for Namespace Instead of ELK


### For use VALUES in this project you should change some parameters, for example 
```
secret:
  enabled: true
  password: "YOUR PASSWORD" # generated randomly if not defined
```
Change YOUR PASSWORD and use your password 
##### please review and edit the Values again  

## Configuration

| Parameter                 | Description                                                                                                                                                                                                                          | Default                               |
|---------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|
| `antiAffinityTopologyKey` | The [anti-affinity][] topology key]. By default this will prevent multiple Logstash nodes from running on the same Kubernetes node                                                                                                   | `kubernetes.io/hostname`              |
| `antiAffinity`            | Setting this to hard enforces the [anti-affinity][] rules. If it is set to soft it will be done "best effort". Other values will be ignored                                                                                          | `hard`                                |
| `envFrom`                 | Templatable string to be passed to the [environment from variables][] which will be appended to the `envFrom:` definition for the container                                                                                          | `[]`                                  |
| `extraContainers`         | Templatable string of additional containers to be passed to the `tpl` function                                                                                                                                                       | `[]`                                  |
| `extraEnvs`               | Extra [environment variables][] which will be appended to the `env:` definition for the container                                                                                                                                    | `[]`                                  |
| `extraInitContainers`     | Templatable string of additional `initContainers` to be passed to the `tpl` function                                                                                                                                                 | `[]`                                  |
| `extraPorts`              | An array of extra ports to open on the pod                                                                                                                                                                                           | `[]`                                  |
| `extraVolumeMounts`       | Templatable string of additional `volumeMounts` to be passed to the `tpl` function                                                                                                                                                   | `[]`                                  |
| `extraVolumes`            | Templatable string of additional `volumes` to be passed to the `tpl` function                                                                                                                                                        | `[]`                                  |
| `fullnameOverride`        | Overrides the full name of the resources. If not set the name will default to " `.Release.Name` - `.Values.nameOverride or .Chart.Name` "                                                                                            | `""`                                  |
| `hostAliases`             | Configurable [hostAliases][]                                                                                                                                                                                                         | `[]`                                  |
| `httpPort`                | The http port that Kubernetes will use for the healthchecks and the service                                                                                                                                                          | `9600`                                |
| `imagePullPolicy`         | The Kubernetes [imagePullPolicy][] value                                                                                                                                                                                             | `IfNotPresent`                        |
| `imagePullSecrets`        | Configuration for [imagePullSecrets][] so that you can use a private registry for your image                                                                                                                                         | `[]`                                  |
| `imageTag`                | The Logstash Docker image tag                                                                                                                                                                                                        | `8.5.1`                               |
| `image`                   | The Logstash Docker image                                                                                                                                                                                                            | `docker.elastic.co/logstash/logstash` |
| `labels`                  | Configurable [labels][] applied to all Logstash pods                                                                                                                                                                                 | `{}`                                  |
| `ingress`                 | Configurable [ingress][] for external access to Logstash HTTP port.                                                                                                                                                                  | see [values.yaml][]                   |
| `lifecycle`               | Allows you to add lifecycle configuration. See [values.yaml][] for an example of the formatting                                                                                                                                      | `{}`                                  |
| `livenessProbe`           | Configuration fields for the liveness [probe][]                                                                                                                                                                                      | see [values.yaml][]                   |
| `logstashConfig`          | Allows you to add any config files in `/usr/share/logstash/config/` such as `logstash.yml` and `log4j2.properties` See [values.yaml][] for an example of the formatting                                                              | `{}`                                  |
| `logstashJavaOpts`        | Java options for Logstash. This is where you should configure the JVM heap size                                                                                                                                                      | `-Xmx1g -Xms1g`                       |
| `logstashPipeline`        | Allows you to add any pipeline files in `/usr/share/logstash/pipeline/`                                                                                                                                                              | `{}`                                  |
| `logstashPatternDir`      | Allows you to define a custom directory to store pattern files                                                                                                                                                                       | `/usr/share/logstash/patterns/`       |
| `logstashPattern`         | Allows you to add any pattern files in `logstashPatternDir`                                                                                                                                                                          | `{}`                                  |
| `maxUnavailable`          | The [maxUnavailable][] value for the pod disruption budget. By default this will prevent Kubernetes from having more than 1 unhealthy pod in the node group                                                                          | `1`                                   |
| `nameOverride`            | Overrides the chart name for resources. If not set the name will default to `.Chart.Name`                                                                                                                                            | `""`                                  |
| `nodeAffinity`            | Value for the [node affinity settings][]                                                                                                                                                                                             | `{}`                                  |
| `podAffinity`             | Value for the [pod affinity settings][]                                                                                                                                                                                              | `{}`                                  |
| `nodeSelector`            | Configurable [nodeSelector][] so that you can target specific nodes for your Logstash cluster                                                                                                                                        | `{}`                                  |
| `persistence`             | Enables a persistent volume for Logstash data                                                                                                                                                                                        | see [values.yaml][]                   |
| `podAnnotations`          | Configurable [annotations][] applied to all Logstash pods                                                                                                                                                                            | `{}`                                  |
| `podManagementPolicy`     | By default Kubernetes [deploys StatefulSets serially][]. This deploys them in parallel so that they can discover each other                                                                                                          | `Parallel`                            |
| `podSecurityContext`      | Allows you to set the [securityContext][] for the pod                                                                                                                                                                                | see [values.yaml][]                   |
| `podSecurityPolicy`       | Configuration for create a pod security policy with minimal permissions to run this Helm chart with `create: true` Also can be used to reference an external pod security policy with `name: "externalPodSecurityPolicy"`            | see [values.yaml][]                   |
| `priorityClassName`       | The name of the [PriorityClass][]. No default is supplied as the PriorityClass must be created first                                                                                                                                 | `""`                                  |
| `rbac`                    | Configuration for creating a role, role binding and service account as part of this Helm chart with `create: true` Also can be used to reference an external service account with `serviceAccountName: "externalServiceAccountName"` | see [values.yaml][]                   |
| `readinessProbe`          | Configuration fields for the readiness [probe][]                                                                                                                                                                                     | see [values.yaml][]                   |
| `replicas`                | Kubernetes replica count for the StatefulSet (i.e. how many pods)                                                                                                                                                                    | `1`                                   |
| `resources`               | Allows you to set the [resources][] for the StatefulSet                                                                                                                                                                              | see [values.yaml][]                   |
| `schedulerName`           | Name of the [alternate scheduler][]                                                                                                                                                                                                  | `""`                                  |
| `secrets`                 | Allows you easily create a secret from as variables or file. For add secrets from file, add suffix `.filepath` to the key of secret key. The value will be encoded to base64. Useful for store certificates and other secrets.       | See [values.yaml][]                   |
| `secretMounts`            | Allows you easily mount a secret as a file inside the StatefulSet. Useful for mounting certificates and other secrets. See [values.yaml][] for an example                                                                            | `[]`                                  |
| `securityContext`         | Allows you to set the [securityContext][] for the container                                                                                                                                                                          | see [values.yaml][]                   |
| `service`                 | Configurable [service][] to expose the Logstash service.                                                                                                                                                                             | see [values.yaml][]                   |
| `terminationGracePeriod`  | The [terminationGracePeriod][] in seconds used when trying to stop the pod                                                                                                                                                           | `120`                                 |
| `tolerations`             | Configurable [tolerations][]                                                                                                                                                                                                         | `[]`                                  |
| `updateStrategy`          | The [updateStrategy][] for the StatefulSet. By default Kubernetes will wait for the cluster to be green after upgrading each pod. Setting this to `OnDelete` will allow you to manually delete each pod during upgrades              | `RollingUpdate`                       |
| `volumeClaimTemplate`     | Configuration for the [volumeClaimTemplate for StatefulSets][]. You will want to adjust the storage (default `30Gi` ) and the `storageClassName` if you are using a different storage class                                          | see [values.yaml][]                   |

### How to install plugins?

The recommended way to install plugins into our Docker images is to create a
[custom Docker image][].

The Dockerfile would look something like:

```
ARG logstash_version
FROM docker.elastic.co/logstash/logstash:${logstash_version}
RUN bin/logstash-plugin install logstash-output-kafka
```

And then updating the `image` in values to point to your custom image.

There are a couple reasons we recommend this:

1. Tying the availability of Logstash to the download service to install plugins
is not a great idea or something that we recommend. Especially in Kubernetes
where it is normal and expected for a container to be moved to another host at
random times.
2. Mutating the state of a running Docker image (by installing plugins) goes
against best practices of containers and immutable infrastructure.

