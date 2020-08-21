# anzograph-operator

## By Cambridge Semantics Inc.

## Prerequisites

* Red Hat Openshift Container Platform on Kubernetes, version >= 4.3
* Kubectl, versions {1.18-1.14}
* Anzograph Operator Subscription

## Optional Prerequisites
### Create Project(Namespace) if required
<img src="https://cambridgesemantics.com/assets/k8s/csi-k8s-operator-anzograph/v1.3.0/images/projects_screen.png" width="67%">
<img src="https://cambridgesemantics.com/assets/k8s/csi-k8s-operator-anzograph/v1.3.0/images/create-openshift-project.png" width="67%">

## Steps to deploy AnzoGraph Operator

#### Login to OpenShift Console:

#### Operators --> OperatorHub --> Search Anzograph  Operator --> Install
<img src="https://cambridgesemantics.com/assets/k8s/csi-k8s-operator-anzograph/v1.3.0/images/kubeadmin-operatorhub-anzograph-search.png" width="67%">

#### Select Namespace where you want to deploy the operator and click on Install
<img src="https://cambridgesemantics.com/assets/k8s/csi-k8s-operator-anzograph/v1.3.0/images/kubeadmin-anzograph-operator-installdialog.png" width="67%">

#### Check Operator Installation Successful
<img src="https://cambridgesemantics.com/assets/k8s/csi-k8s-operator-anzograph/v1.3.0/images/kubeadmin-install-operator.png" width="67%">


## AnzoGraph Use Cases
* AnzoGraph DB images default has single node 8GB license. Ex:- CR Spec to deploy 1 Database (8vCPU 8GB Memory) X 1 Frontend(2vCPU 4GB Memory)
```
apiVersion: anzograph.clusters.cambridgesemantics.com/v1
kind: AnzoGraph
metadata:
  name: azg01
  labels:
    app: AnzoGraph
  namespace: anzograph-poc
spec:
  serviceAccountName: anzograph-operator
  deployFrontend: true
  frontendSpec:
    image:
      name: cambridgesemantics/anzograph-frontend
      pullPolicy: IfNotPresent
      registry: registry.marketplace.redhat.com/rhm
      tag: latest
    resources:
      limits:
        cpu: 2
        memory: 4Gi
      requests:
        cpu: 2
        memory: 4Gi
    size: 1
  dbSpec:
    image:
      name: cambridgesemantics/anzograph-db
      pullPolicy: IfNotPresent
      registry: registry.marketplace.redhat.com/rhm
      tag: latest
    resources:
      limits:
        cpu: 8000m
        memory: 8Gi
      requests:
        cpu: 8000m
        memory: 8Gi
    size: 1
```
**Note**
* Registering AnzoGraph product will provide 1 Node 16GB license. Follow this doc [License](https://docs.cambridgesemantics.com/anzograph/userdoc/register-license.htm) Ex:- CR Spec to deploy 1 Database (8vCPU 16GB Memory) X 1 Frontend(2vCPU 4GB Memory)
```
apiVersion: anzograph.clusters.cambridgesemantics.com/v1
kind: AnzoGraph
metadata:
  name: azg01
  labels:
    app: AnzoGraph
  namespace: anzograph-poc
spec:
  serviceAccountName: anzograph-operator
  deployFrontend: true
  frontendSpec:
    image:
      name: cambridgesemantics/anzograph-frontend
      pullPolicy: IfNotPresent
      registry: registry.marketplace.redhat.com/rhm
      tag: latest
    resources:
      limits:
        cpu: 2000m
        memory: 4Gi
      requests:
        cpu: 2000m
        memory: 4Gi
    size: 1
  dbSpec:
    image:
      name: cambridgesemantics/anzograph-db
      pullPolicy: IfNotPresent
      registry: registry.marketplace.redhat.com/rhm
      tag: latest
    resources:
      limits:
        cpu: 8000m
        memory: 16Gi
      requests:
        cpu: 8000m
        memory: 16Gi
    size: 1
```

## Steps to deploy AnzoGraph Cluster

#### Pre-requiste
* Create a Security Context Constraint (SCC) for the service account to be able to start the AnzoGraph container as root. Note that the actual service in the container runs unprivileged.
* Create a file called scc.yml and add the following contents to the file. **Replace keyword namespace with the actual value**
```
    apiVersion: security.openshift.io/v1
    kind: SecurityContextConstraints
    metadata:
      name: csi-anyuid
      namespace: namespace
    priority: 10
    runAsUser:
      type: RunAsAny
    seLinuxContext:
      type: MustRunAs
    supplementalGroups:
      type: RunAsAny
    fsGroup:
      type: RunAsAny
    users:
    - system:serviceaccount:namespace:anzograph-operator
```
* Save the file and then run the following command to give OpenShift the SCC resource specification:
* oc create -f scc.yml

#### Operators --> Installed Operators --> AnzoGraph  Operator --> Create Instance
<img src="https://cambridgesemantics.com/assets/k8s/csi-k8s-operator-anzograph/v1.3.0/images/kubeadmin-create-anzograph.png" width="67%">

#### Use either Form View or YAML View to set required properties, use **AnzoGraph CustomResource(CR) Specification** for definitiions
<img src="https://cambridgesemantics.com/assets/k8s/csi-k8s-operator-anzograph/v1.3.0/images/kubeadmin-install-anzograph-form.png" width="67%">
<img src="https://cambridgesemantics.com/assets/k8s/csi-k8s-operator-anzograph/v1.3.0/images/kubeadmin-install-anzograph-yaml.png" width="67%">

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
