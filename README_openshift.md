# anzograph-operator

## By Cambridge Semantics Inc.

## Supported tags

* [latest](registry.connect.redhat.com/cambridgesemantics/anzograph-operator:latest)

**Project Status:** stable
**Operator Version:** v1

## Prerequisites

* Red Hat Openshift Container Platform on Kubernetes, version >= 4.3
* Kubectl, versions {1.18-1.14}

## AnzoGraph Docker Images Used for Deployment
When you deploy AnzoGraph cluster using operator, following are the set of images used for actual cluster deployments. We have given reference docker commands to download the latest releases for each of them below.

### AnzoGraph Operator

* To download latest release, please use:

   ```sh
   docker pull registry.connect.redhat.com/cambridgesemantics/anzograph-operator:latest
   ```

### AnzoGraph Database

* To download latest release, please use:

   ```sh
   docker pull registry.connect.redhat.com/cambridgesemantics/anzograph-db:latest
   ```

### AnzoGraph Frontend

* If you want to enable UI for the AnzoGraph database, following is the image used.
   ```sh
   docker pull registry.connect.redhat.com/cambridgesemantics/anzograph-frontend:latest
   ```

## Steps to deploy anzograph-operator
Deployment of AnzoGraph cluster can be achieved in three simple steps.

### Step 1:
#### Deploy Operator along with all pre-requisites:
With the help of following command, you will install operator along with all pre-deployment configurations needed, i.e. RBAC, PodSecurityPolicy, Service Account, CustomResourceDefinition(CRD) and a dedicated 'anzograph' namespace.
```sh
kubectl apply -f <placeholder-for-pre_requisites_all_in_one.yaml>
```

### Step 2:
#### Deploy Custom Resource for AnzoGraph Cluster:
You will get AnzoGraph cluster ready to use by
```sh
kubectl apply -f <placeholder-for-cr.yaml>
```

### Step 3:
#### Get Current State of Deployment of AnzoGraph Cluster:
```sh
kubectl describe anzograph/<cr-name>.yaml --namespace anzograph
```

**NOTE:** 
1. If you like to use namespace other than 'anzograph', please edit above two YAMLs to create and reference namespace correctly.
2. If you wish to use images other than latest, please specify them with correct tags in YAMLs.

## Steps to delete AnzoGraph CR and anzograph-operator
Tearing down running AnzoGraph cluster is also easy and can be achieved using following steps.

### Step 1:
#### Delete Custom Resource:
```sh
kubectl delete -f <placeholder-for-cr.yaml>
```

### Step 2:
#### Delete anzograph-operator and its prerequisites:
```sh
kubectl delete -f <placeholder-for-pre_requisites_all_in_one.yaml>
```

## AnzoGraph CustomResource(CR) Specification

The following table lists the configurable parameters for AnzoGraph and their default values.(CR API Version: v1beta1)

| Parameter | Description | Default |
|-----------|-------------|---------|
| `metadata.name` | Name of CR | azg02 |
| `metadata.namespace` | Namespace of CR | |
| `metadata.labels` | Dictionary of (key: val) as labels of CR | |
| `spec.serviceAccountName` | Name of service account for deploying CR | anzograph-operator |
| `spec.allInOneImage.registry` | Docker image registry for AnzoGraph All-in-One image | registry.connect.redhat.com |
| `spec.allInOneImage.name` | Docker image name for AnzoGraph All-in-one image | cambridgesemantics/anzograph |
| `spec.allInOneImage.tag` | Docker image tag for AnzoGraph All-in-one image | latest |
| `spec.allInOneImage.pullPolicy` | Docker image pull policy for AnzoGraph All-in-one image | IfNotPresent |
| `spec.dbSpec.image.registry` | Docker image registry for AnzoGraph DB image | registry.connect.redhat.com |
| `spec.dbSpec.image.name` | Docker image name for AnzoGraph DB image | cambridgesemantics/anzograph-db |
| `spec.dbSpec.image.tag` | Docker image tag for AnzoGraph DB image | latest |
| `spec.dbSpec.image.pullPolicy` | Docker image pull policy for AnzoGraph DB image | IfNotPresent |
| `spec.dbSpec.dbImage.size` | No of AnzoGraph DB cluster pods | 1 |
| `spec.dbSpec.resources.requests.cpu` | Resource request for AnzoGraph leader container, number of CPUs | 2000m |
| `spec.dbSpec.resources.requests.memory` | Resource request for AnzoGraph leader container, memory size in MB | 7000Mi |
| `spec.dbSpec.resources.limits.cpu` | Resource limit for AnzoGraph leader container, number of CPUs | 16000m |
| `spec.dbSpec.resources.limits.memory` | Resource limit for AnzoGraph leader container, memory | 48000Mi |
| `spec.dbSpec.tolerations` | AnzoGraph database pod tolerations | commented, please uncomment to add value |
| `spec.dbSpec.affinity` | AnzoGraph database pod node affinity | |
| `spec.dbSpec.service` | Database loadbalancer service attributes, of type v1.Service | |
| `spec.dbSpec.volumes` | List of persistent volumes for AnzoGraph DB | commented, please uncomment to add value |
| `spec.dbSpec.volumes.[i].name` | Name for persistent volume | |
| `spec.dbSpec.volumes.[i].mountPath` | Path where persistent volume should be mounted inside container | |
| `spec.dbSpec.volumes.[i].pv` | Attributes to configure persistent volume, of type v1.PersistentVolume | |
| `spec.dbSpec.volumes.[i].pvc` | Attributes to configure persistent volume claim, of type v1.PersistentVolumeClaim | |
| `spec.frontendSpec.image.registry` | Docker image registry for AnzoGraph Frontend image | registry.connect.redhat.com |
| `spec.frontendSpec.image.name` | Docker image name for AnzoGraph Frontend image | cambridgesemantics/anzograph-frontend |
| `spec.frontendSpec.image.tag` | Docker image tag for AnzoGraph Frontend image | latest |
| `spec.frontendSpec.image.pullPolicy` | Docker image pull policy for AnzoGraph Frontend image | IfNotPresent |
| `spec.frontendSpec.resources.requests.cpu` | Resource request for AnzoGraph frontend container, number of CPUs | 2000m |
| `spec.frontendSpec.resources.requests.memory` | Resource request for AnzoGraph frontend container, memory | 4000Mi |
| `spec.frontendSpec.resources.limits.cpu` | Resource limit for AnzoGraph frontend container, number of CPUs | 8000m |
| `spec.frontendSpec.resources.limits.memory` | Resource limit for AnzoGraph frontend container, memory size in MB | 16000Mi |
| `spec.frontendSpec.tolerations` | AnzoGraph frontend pod tolerations | commented, please uncomment to add value |
| `spec.frontendSpec.affinity` | AnzoGraph frontend pod node affinity | |
| `spec.frontendSpec.service` | Frontend loadbalancer service attributes, of type v1.Service | |
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
