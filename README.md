# anzograph-operator

## By Cambridge Semantics Inc

## Supported tags

| Release | Tags                                       |
| :---:   | :---                                       |
| [2.0.3](https://hub.docker.com/layers/cambridgesemantics/anzograph-operator/2.0.3-20240605074132/images/sha256-747d03738e30d1c47db328533297956ae474cd29eec346860db655fd0b78e0bf?context=repo) | [2.0.3](https://hub.docker.com/layers/cambridgesemantics/anzograph-operator/2.0.3-20240605074132/images/sha256-747d03738e30d1c47db328533297956ae474cd29eec346860db655fd0b78e0bf?context=repo), 2.0.3-{{ build }} |
| [2.0.2](https://hub.docker.com/layers/257823639/cambridgesemantics/anzograph-operator/2.0.2/images/sha256-17e66805745778a580711c030f694f0f1ff6a3a11cb8db1bd24b8c6ef577889d?context=repo)   |  [2.0.2](https://hub.docker.com/layers/257823639/cambridgesemantics/anzograph-operator/2.0.2/images/sha256-17e66805745778a580711c030f694f0f1ff6a3a11cb8db1bd24b8c6ef577889d?context=repo), 2.0.2-{{ build }}  |
|  [2.0.1](https://hub.docker.com/layers/cambridgesemantics/anzograph-operator/2.0.1/images/sha256-9776b24bbb6146e367234c4963b5dfabfba9bcda8d7eb7e6cb42f9adbe2fbd72?context=explore)  |  [2.0.1](https://hub.docker.com/layers/cambridgesemantics/anzograph-operator/2.0.1/images/sha256-9776b24bbb6146e367234c4963b5dfabfba9bcda8d7eb7e6cb42f9adbe2fbd72?context=explore), 2.0.1-{{ build }}  |
|  [2.0.0](https://hub.docker.com/layers/cambridgesemantics/anzograph-operator/2.0.0/images/sha256-7939cf95f94c448c425caa9fb200ee1f1b1aa51422ffb80edc9b629de9cd4408?context=explore)  |  [2.0.0](https://hub.docker.com/layers/cambridgesemantics/anzograph-operator/2.0.0/images/sha256-7939cf95f94c448c425caa9fb200ee1f1b1aa51422ffb80edc9b629de9cd4408?context=explore), 2.0.0-{{ build }}  |
|  [1.3.5](https://hub.docker.com/layers/cambridgesemantics/anzograph-operator/1.3.5/images/sha256-06ec451214af65f08fa75d94a83ab5f4fdbf8ff481958388f7c9594603bea03d?context=explore)  |  [1.3.5](https://hub.docker.com/layers/cambridgesemantics/anzograph-operator/1.3.5/images/sha256-06ec451214af65f08fa75d94a83ab5f4fdbf8ff481958388f7c9594603bea03d?context=explore), 1.3.5-{{ build }}  |
|  [1.3.0](https://hub.docker.com/layers/cambridgesemantics/anzograph-operator/1.3.0/images/sha256-fe2b8a772ac1e16de63a851782331e34f69458f70e69ebca69e2befd18a619fa?context=explore)  |  [1.3.0](https://hub.docker.com/layers/cambridgesemantics/anzograph-operator/1.3.0/images/sha256-fe2b8a772ac1e16de63a851782331e34f69458f70e69ebca69e2befd18a619fa?context=explore), 1.3.0-{{ build }}  |
|  [1.2.0](https://hub.docker.com/layers/cambridgesemantics/anzograph-operator/1.2.0/images/sha256-06d7fba03093bc21b2004bbbff4be7afb910697c59a92208f02e10bbfe27919a?context=explore)  |  [1.2.0](https://hub.docker.com/layers/cambridgesemantics/anzograph-operator/1.2.0/images/sha256-06d7fba03093bc21b2004bbbff4be7afb910697c59a92208f02e10bbfe27919a?context=explore), 1.2.0-{{ build }}  |

## About [AnzoGraph](https://cambridgesemantics.com/anzograph)

AnzoGraph® DB is the only MPP (massively parallel processing) native graph [OLAP](https://en.wikipedia.org/wiki/Online_analytical_processing) ([GOLAP](https://en.wikipedia.org/wiki/Online_analytical_processing?golap#Other_types))  database designed to accelerate data integration and scalable analytics with graph at performance levels that compare favorably with the industry-leading data warehouse analytics products.  AnzoGraph offers a variety of advanced analytics capabilities, including over 40 functions for regular data warehousing-style line-of-business analytics like [Aggregate grouping](https://docs.cambridgesemantics.com/anzograph/userdoc/grouping-sets.htm), [Views](https://docs.cambridgesemantics.com/anzograph/userdoc/named-views.htm), [Windowed Aggregates](https://docs.cambridgesemantics.com/anzograph/userdoc/window-aggs.htm), as well as [graph algorithms](https://docs.cambridgesemantics.com/anzograph/userdoc/graph-algorithms.htm),  and [Inferencing](https://docs.cambridgesemantics.com/anzograph/userdoc/inferences.htm) at super-fast speeds. An SDK enables developers to add their own custom parallel bi-directional connectors, functions and aggregates that can perform in parallel across enterprise-scale knowledge-graphs. The product has been market tested and has been in production for several years at leading global corporations.

**Project Status** stable
**Operator Version** v2

## Prerequisites

* Kubernetes cluster, versions {1.28-1.16}
* Kubectl, versions {1.28-1.16}

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
# Create Namespace, mention name of your namespace in metadata.name
$ kubectl create -f deploy/v1_namespace_default.yaml
# Setup Service Account
$ kubectl create -f deploy/default_v1_serviceaccount_anzograph-operator.yaml --namespace <namespace>
# Setup RBAC
$ kubectl create -f deploy/default_rbac.authorization.k8s.io_v1_role_anzograph-operator.yaml --namespace <namespace>
$ kubectl create -f deploy/default_rbac.authorization.k8s.io_v1_rolebinding_anzograph-operator.yaml --namespace <namespace>
$ kubectl create -f deploy/rbac.authorization.k8s.io_v1_clusterrole_anzograph-operator.yaml
$ kubectl create -f deploy/rbac.authorization.k8s.io_v1_clusterrolebinding_anzograph-operator.yaml
$ kubectl create -f deploy/policy_v1beta1_podsecuritypolicy_anzograph-privileged.yaml
# Setup the CRD
$ kubectl create -f deploy/crds/apiextensions.k8s.io_v1_customresourcedefinition_anzographs.anzograph.clusters.cambridgesemantics.com.yaml
# Deploy anzograph-operator
$ kubectl create -f deploy/default_apps_v1_deployment_anzograph-operator.yaml --namespace <namespace>
# Deploy AnzoGraph Custom Resource(CR), i.e. AnzoGraph cluster deployment (#1)
# NOTE: This CR is designed for images in Red Hat registry. Skip this step to deploy CR for different environment.
$ kubectl apply -f deploy/default_anzograph.clusters.cambridgesemantics.com_v2_anzograph_azg01.yaml --namespace <namespace>
# Deploy AnzoGraph Custom Resource(CR) (#2)
$ kubectl apply -f config/samples/anzograph_v2_anzograph.yaml --namespace <namespace>
```

**NOTE** One needs to edit operator deployment, CR deployment with right docker image details.

## Steps to delete AnzoGraph CR and anzograph-operator

```sh
# Delete AnzoGraph CR (#1)
$ kubectl delete -f deploy/default_anzograph.clusters.cambridgesemantics.com_v2_anzograph_azg01.yaml --namespace <namespace>
# Delete AnzoGraph CR (#2)
$ kubectl delete -f config/samples/anzograph_v2_anzograph.yaml --namespace <namespace>
# Delete anzograph-operator
$ kubectl delete -f deploy/default_apps_v1_deployment_anzograph-operator.yaml --namespace <namespace>
# Delete RBAC
$ kubectl delete -f deploy/default_rbac.authorization.k8s.io_v1_role_anzograph-operator.yaml --namespace <namespace>
$ kubectl delete -f deploy/default_rbac.authorization.k8s.io_v1_rolebinding_anzograph-operator.yaml --namespace <namespace>
$ kubectl delete -f deploy/rbac.authorization.k8s.io_v1_clusterrole_anzograph-operator.yaml
$ kubectl delete -f deploy/rbac.authorization.k8s.io_v1_clusterrolebinding_anzograph-operator.yaml
$ kubectl delete -f deploy/policy_v1beta1_podsecuritypolicy_anzograph-privileged.yaml
# Delete Service Account
$ kubectl delete -f deploy/default_v1_serviceaccount_anzograph-operator.yaml --namespace <namespace>
# Delete CRD
$ kubectl delete -f deploy/crds/apiextensions.k8s.io_v1_customresourcedefinition_anzographs.anzograph.clusters.cambridgesemantics.com.yaml
```

## AnzoGraph CustomResource(CR) Specification

The following table lists the configurable parameters for AnzoGraph and their default values.(CR API Version: v2)

| Parameter | Description | Default |
|-----------|-------------|---------|
| `metadata.name` | Name of CR | |
| `metadata.namespace` | Namespace of CR | |
| `metadata.labels` | Dictionary of (key: val) as labels of CR | |
| `spec.db.nodeConfig.spec` | Configuration specification for AnzoGraph DB pods | |
| `spec.db.nodeConfig.spec.replicas` | Number of pods for AnzoGraph DB | 1 |
| `spec.db.nodeConfig.spec.serviceName` | Name of headless service for AnzoGraph | anzograph-<metadata.name> |
| `spec.db.nodeConfig.spec.template.spec.serviceAccountName` | Service account name for pods | anzograph-operator |
| `spec.db.nodeConfig.spec.template.spec.containers.x.Name` | Name of AnzoGraph DB container | db |
| `spec.db.nodeConfig.spec.template.spec.containers.y.Name` | Name of sidecar container, if sidecar logging is enabled | logger |
| `spec.db.deployLoggerSidecar` | Set this to true to enable sidecar logging | false |
| `spec.db.service` | Database loadbalancer service attributes, of type v1.Service | commented, please uncomment to add value |
| `spec.db.volumes` | List of persistent volumes for AnzoGraph DB | commented, please uncomment to add value |
| `spec.db.volumes.[i].name` | Name for persistent volume | |
| `spec.db.volumes.[i].mountPath` | Path where persistent volume should be mounted inside container | |
| `spec.db.volumes.[i].pv` | Attributes to configure persistent volume, of type v1.PersistentVolume | |
| `spec.db.volumes.[i].pvc` | Attributes to configure persistent volume claim, of type v1.PersistentVolumeClaim | |
| `spec.db.volumes.[i].deletePVC` | Set this to true if you want to delete PVC after CR deletion | false |
| `spec.db.settingsProfile` | Named settings bundles/profiles to configure AnzoGraph | standalone |
| `spec.db.settingsConfContent` | When settingsProfile is 'custom', use this to override default settings(dictionary of key: val) | |
| `spec.db.license` | User provided license string(BYOL) | "" |
| `spec.frontend.nodeConfig.spec` | Configuration specification for AnzoGraph Frontend pods | |
| `spec.frontend.nodeConfig.spec.replicas` | Number of pods for AnzoGraph Frontend | 1 |
| `spec.frontend.nodeConfig.spec.serviceName` | Name of headless service for AnzoGraph | anzograph-<metadata.name> |
| `spec.frontend.nodeConfig.spec.template.spec.serviceAccountName` | Service account name for pods | anzograph-operator |
| `spec.frontend.nodeConfig.spec.template.spec.containers.x.Name` | Name of AnzoGraph Frontend container | frontend |
| `spec.frontend.service` | Database loadbalancer service attributes, of type v1.Service | commented, please uncomment to add value |
| `spec.frontend.volumes` | List of persistent volumes for AnzoGraph DB | commented, please uncomment to add value |
| `spec.frontend.volumes.[i].name` | Name for persistent volume | |
| `spec.frontend.volumes.[i].mountPath` | Path where persistent volume should be mounted inside container | |
| `spec.frontend.volumes.[i].pv` | Attributes to configure persistent volume, of type v1.PersistentVolume | |
| `spec.frontend.volumes.[i].pvc` | Attributes to configure persistent volume claim, of type v1.PersistentVolumeClaim | |
| `spec.frontend.volumes.[i].deletePVC` | Set this to true if you want to delete PVC after CR deletion | false |
| `spec.uiCredentials.uiCredentials` | Name of existing secret for frontend credentials | |
| `spec.uiCredentials.grpcCredentials` | Name of existing secret for gRPC credentials | |
| `spec.uiCredentials.keystoreCredentials` | Name of existing secret for frontend keystore | |
| `spec.deployFrontend` | Set this to true if you want to deploy frontend for AnzoGraph DB | false |
| `spec.uiUserCerts.uiUserServiceCert` | AnzoGraph UI access certificate | commented, please uncomment to add value |
| `spec.uiUserCerts.uiUserServiceKey` | AnzoGraph UI access certificate key | commented, please uncomment to add value |
| `spec.uiUserCerts.uiUserCACert` | AnzoGraph UI access ca certificate | commented, please uncomment to add value |

## References

```https://docs.cambridgesemantics.com/```
