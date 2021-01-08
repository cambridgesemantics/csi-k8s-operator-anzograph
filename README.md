# anzograph-operator

## By Cambridge Semantics Inc

## Supported tags

* [1.3.0](https://hub.docker.com/layers/cambridgesemantics/anzograph-operator/1.3.0/images/sha256-fe2b8a772ac1e16de63a851782331e34f69458f70e69ebca69e2befd18a619fa?context=explore) , [1.3.0-latest](https://hub.docker.com/layers/cambridgesemantics/anzograph-operator/1.3.0-latest/images/sha256-fe2b8a772ac1e16de63a851782331e34f69458f70e69ebca69e2befd18a619fa?context=explore) , [1.2.0](https://hub.docker.com/layers/cambridgesemantics/anzograph-operator/1.2.0/images/sha256-06d7fba03093bc21b2004bbbff4be7afb910697c59a92208f02e10bbfe27919a?context=explore) , [1.2.0-latest](https://hub.docker.com/layers/cambridgesemantics/anzograph-operator/1.2.0-latest/images/sha256-06d7fba03093bc21b2004bbbff4be7afb910697c59a92208f02e10bbfe27919a?context=explore) , 1.2.0-{{ build }}

## About [AnzoGraph](https://cambridgesemantics.com/anzograph)

AnzoGraph® DB is the only MPP (massively parallel processing) native graph [OLAP](https://en.wikipedia.org/wiki/Online_analytical_processing) ([GOLAP](https://en.wikipedia.org/wiki/Online_analytical_processing?golap#Other_types))  database designed to accelerate data integration and scalable analytics with graph at performance levels that compare favorably with the industry-leading data warehouse analytics products.  AnzoGraph offers a variety of advanced analytics capabilities, including over 40 functions for regular data warehousing-style line-of-business analytics like [Aggregate grouping](https://docs.cambridgesemantics.com/anzograph/userdoc/grouping-sets.htm), [Views](https://docs.cambridgesemantics.com/anzograph/userdoc/named-views.htm), [Windowed Aggregates](https://docs.cambridgesemantics.com/anzograph/userdoc/window-aggs.htm), as well as [graph algorithms](https://docs.cambridgesemantics.com/anzograph/userdoc/graph-algorithms.htm),  and [Iinferencing](https://docs.cambridgesemantics.com/anzograph/userdoc/inferences.htm) at super-fast speeds. An SDK enables developers to add their own custom parallel bi-directional connectors, functions and aggregates that can perform in parallel across enterprise-scale knowledge-graphs. The product has been market tested and has been in production for several years at leading global corporations.

**Project Status** stable
**Operator Version** v1

## Prerequisites

* Kubernetes cluster, versions {1.18-1.14}
* Kubectl, versions {1.18-1.14}

## Setting up prerequisites

## Steps to deploy anzograph-operator

**NOTE**: You must get following docker images for deployment

### AnzoGraph Operator

* Path of Docker Hub: ```https://hub.docker.com/r/cambridgesemantics/anzograph-operator```

* Command to download the latest release, please use:

    ```sh
   docker pull cambridgesemantics/anzograph-operator
   ```

### AnzoGraph Database

* Path of Docker Hub: ```https://hub.docker.com/r/cambridgesemantics/anzograph-db```

* Command to download the latest release, please use:

    ```sh
   docker pull cambridgesemantics/anzograph-db
   ```

### AnzoGraph Frontend

If the user wants to enable the UI for the AnzoGraph database, they can do so using the following image details.

* Path of Docker Hub: ```https://hub.docker.com/r/cambridgesemantics/anzograph-frontend```

* Command to download the latest release, please use:

   ```sh
   docker pull cambridgesemantics/anzograph-frontend
   ```

## Connect to Kubernetes cluster

You can connect to Kubernetes cluster hosted in public cloud service providers such as AWS, Google, Microsoft Azure, after adding/updating ```${HOME}/.kube/config``` file on workstation where ```kubectl``` is installed.

* For AWS, install ```aws-cli``` and use:

 ```aws eks --region <region-name> update-kubeconfig --name <EKS-cluster-name>```

* For Google, use:

 ```gcloud container clusters get-credentials <GKE-cluster-name> --zone <zone-name> --project <project-name> --region <region-name>```

   To install gcloud, please refer to ```https://cloud.google.com/sdk/install```

* For Microsoft Azure, use:

 ```az aks get-credentials --resource-group <resource-group-name> --name <AKS-cluster-name>```

   To install azure cli, please refer to ```https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest```

## RBAC Prerequisites

For deploying AnzoGraph operator and clusters managed by it, user needs to enable RBAC and configure kubernetes objects mentioned below.

```sh
# Create Namespace
$ kubectl create -f deploy/namespace.yaml
# Setup Service Account
$ kubectl create -f deploy/service_account.yaml
# Setup RBAC
$ kubectl create -f deploy/role.yaml
$ kubectl create -f deploy/role_binding.yaml
$ kubectl create -f deploy/cluster_role.yaml
$ kubectl create -f deploy/cluster_role_binding.yaml
$ kubectl create -f deploy/psp.yaml
# Setup the CRD
$ kubectl create -f deploy/crds/anzograph.clusters.cambridgesemantics.com_anzographs_crd.yaml
# Deploy anzograph-operator
$ kubectl create -f deploy/operator.yaml
# Deploy AnzoGraph Custom Resource(CR), i.e. AnzoGraph cluster deployment
$ kubectl apply -f deploy/crds/anzograph_v1_anzograph_cr.yaml
```

**NOTE** One needs to edit deploy/operator.yaml, deploy/crds/anzograph_v1beta1_anzograph_cr.yaml with right docker image details. Also, namespace needs to be specified in other YAML files.

## Steps to delete AnzoGraph CR and anzograph-operator

```sh
# Delete AnzoGraph CR
kubectl delete -f deploy/crds/anzograph_v1_anzograph_cr.yaml
# Delete anzograph-operator
kubectl delete -f deploy/operator.yaml
# Delete RBAC
kubectl delete -f deploy/role.yaml
kubectl delete -f deploy/role_binding.yaml
kubectl delete -f deploy/cluster_role.yaml
kubectl delete -f deploy/cluster_role_binding.yaml
kubectl delete -f deploy/psp.yaml
# Delete Service Account
kubectl delete -f deploy/service_account.yaml
# Delete CRD
kubectl delete -f deploy/crds/anzograph.clusters.cambridgesemantics.com_anzographs_crd.yaml
```

## AnzoGraph CustomResource(CR) Specification

The following table lists the configurable parameters for AnzoGraph and their default values.(CR API Version: v1beta1)

| Parameter | Description | Default |
|-----------|-------------|---------|
| `metadata.name` | Name of CR | azg02 |
| `metadata.namespace` | Namespace of CR | |
| `metadata.labels` | Dictionary of (key: val) as labels of CR | |
| `spec.serviceAccountName` | Name of service account for deploying CR | anzograph-operator |
| `spec.allInOneImage.registry` | Docker image registry for AnzoGraph All-in-One image | docker.io |
| `spec.allInOneImage.name` | Docker image name for AnzoGraph All-in-one image | cambridgesemantics/anzograph |
| `spec.allInOneImage.tag` | Docker image tag for AnzoGraph All-in-one image | latest |
| `spec.allInOneImage.pullPolicy` | Docker image pull policy for AnzoGraph All-in-one image | IfNotPresent |
| `spec.dbSpec.image.registry` | Docker image registry for AnzoGraph DB image | docker.io |
| `spec.dbSpec.image.name` | Docker image name for AnzoGraph DB image | cambridgesemantics/anzograph-db |
| `spec.dbSpec.image.tag` | Docker image tag for AnzoGraph DB image | latest |
| `spec.dbSpec.image.pullPolicy` | Docker image pull policy for AnzoGraph DB image | IfNotPresent |
| `spec.dbSpec.dbImage.size` | No of AnzoGraph DB cluster pods | 1 |
| `spec.dbSpec.resources.requests.cpu` | Resource request for AnzoGraph leader container, number of CPUs | 2000m |
| `spec.dbSpec.resources.requests.memory` | Resource request for AnzoGraph leader container, memory size in MB | 7000Mi |
| `spec.dbSpec.resources.limits.cpu` | Resource limit for AnzoGraph leader container, number of CPUs | 16000m |
| `spec.dbSpec.resources.limits.memory` | Resource limit for AnzoGraph leader container, memory size in MB | 48000Mi |
| `spec.dbSpec.tolerations` | AnzoGraph database pod tolerations | commented, please uncomment to add value |
| `spec.dbSpec.affinity` | AnzoGraph database pod node affinity | |
| `spec.dbSpec.service` | Database loadbalancer service attributes, of type v1.Service | commented, please uncomment to add value |
| `spec.dbSpec.volumes` | List of persistent volumes for AnzoGraph DB | commented, please uncomment to add value |
| `spec.dbSpec.volumes.[i].name` | Name for persistent volume | |
| `spec.dbSpec.volumes.[i].mountPath` | Path where persistent volume should be mounted inside container | |
| `spec.dbSpec.volumes.[i].pv` | Attributes to configure persistent volume, of type v1.PersistentVolume | |
| `spec.dbSpec.volumes.[i].pvc` | Attributes to configure persistent volume claim, of type v1.PersistentVolumeClaim | |
| `spec.frontendSpec.image.registry` | Docker image registry for AnzoGraph Frontend image | docker.io |
| `spec.frontendSpec.image.name` | Docker image name for AnzoGraph Frontend image | cambridgesemantics/anzograph-frontend |
| `spec.frontendSpec.image.tag` | Docker image tag for AnzoGraph Frontend image | latest |
| `spec.frontendSpec.image.pullPolicy` | Docker image pull policy for AnzoGraph Frontend image | IfNotPresent |
| `spec.frontendSpec.resources.requests.cpu` | Resource request for AnzoGraph frontend container, number of CPUs | 2000m |
| `spec.frontendSpec.resources.requests.memory` | Resource request for AnzoGraph frontend container, memory size in MB | 4000Mi |
| `spec.frontendSpec.resources.limits.cpu` | Resource limit for AnzoGraph frontend container, number of CPUs | 8000m |
| `spec.frontendSpec.resources.limits.memory` | Resource limit for AnzoGraph frontend container, memory size in MB | 16000Mi |
| `spec.frontendSpec.tolerations` | AnzoGraph frontend pod tolerations | commented, please uncomment to add value |
| `spec.frontendSpec.affinity` | AnzoGraph frontend pod node affinity | |
| `spec.frontendSpec.service` | Frontend loadbalancer service attributes, of type v1.Service | commented, please uncomment to add value |
| `spec.uiCredentials.uiCredentials` | Name of existing secret for frontend credentials | |
| `spec.uiCredentials.grpcCredentials` | Name of existing secret for gRPC credentials | |
| `spec.uiCredentials.keystoreCredentials` | Name of existing secret for frontend keystore | |
| `spec.deployFrontend` | Set this to true if you want to deploy frontend for AnzoGraph DB | false |
| `spec.license` | User provided license string(BYOL) | "" |
| `spec.uiUserCerts.uiUserServiceCert` | AnzoGraph UI access certificate | commented, please uncomment to add value |
| `spec.uiUserCerts.uiUserServiceKey` | AnzoGraph UI access certificate key | commented, please uncomment to add value |
| `spec.uiUserCerts.uiUserCACert` | AnzoGraph UI access ca certificate | commented, please uncomment to add value |
| `spec.azgSettingsProfile` | Named settings bundles/profiles to configure AnzoGraph | standalone |
| `spec.azgSettings` | When azgSettingsProfile is 'custom', use this to override default settings(dictionary of key: val) | |

## References

```https://docs.cambridgesemantics.com/```