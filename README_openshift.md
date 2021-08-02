# anzograph-operator

## By Cambridge Semantics Inc.

## Supported tags

* [latest](registry.connect.redhat.com/cambridgesemantics/anzograph-operator:latest)

**Project Status:** stable
**Operator Version:** v2

## Prerequisites

* Red Hat Openshift Container Platform on Kubernetes, version >= 4.3
* Kubectl, versions {1.20-1.16}

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

### AnzoGraph AllInOne Image(DB + Frontend)

* To download latest release, please use:
   ```sh
   docker pull registry.connect.redhat.com/cambridgesemantics/anzograph:latest
   ```

## Steps to deploy anzograph-operator
Deployment of AnzoGraph cluster can be achieved using following steps.

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
# Deploy AnzoGraph Custom Resource(CR), i.e. AnzoGraph cluster deployment
$ kubectl apply -f deploy/default_anzograph.clusters.cambridgesemantics.com_v2_anzograph_azg01.yaml --namespace <namespace>
```

**NOTE** One needs to edit operator deployment, CR deployment with right docker image details.

## Steps to delete AnzoGraph CR and anzograph-operator

```sh
# Delete AnzoGraph CR
$ kubectl delete -f deploy/default_anzograph.clusters.cambridgesemantics.com_v2_anzograph_azg01.yaml --namespace <namespace>
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
