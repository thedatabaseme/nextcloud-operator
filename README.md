# Nextcloud Operator
------------
The Nextcloud Operator is a Kubernetes controller created with the Operator SDK Framework.
It relies on Ansible roles and make deployment of Nextcloud instances on a Kubernetes
cluster easy.

Features:

- Create / manage / delete Nextcloud instances
- Control the service type of the Nextcloud instance which the Operator creates
- Control ingress and ingress annotations
- Volume size and storage class is configureable

# Deploy / Install
------------
To deploy the Nextcloud Operator to your Cluster, you can use the following kustomization
overlay. Exchange the `v0.1.0` tag with the latest release tag in this repository.

```yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization

resources:
  # Find the latest tag here: https://github.com/thedatabaseme/nextcloud-operator/releases
  - https://github.com/thedatabaseme/nextcloud-operator/config/default?ref=v0.1.0

# Set the image tags to match the git version from above
images:
  - name: ghcr.io/thedatabaseme/nextcloud-operator
    newTag: v0.1.0

# Specify a custom namespace in which to install Nextcloud Operator
namespace: nextcloud-operator
```

# Create a Nextcloud instance
------------
To create a Nextcloud instance using the Nextcloud Operator, you need to apply a `Nextcloud`
CRD to your Kubernetes cluster, where the Operator is deployed. Below, you find an example CRD.

```yaml
apiVersion: thedatabase.me/v1alpha1
kind: Nextcloud
metadata:
  name: nextcloud-sample
  namespace: nextcloud-sample
spec:
  nextcloudImageVersion: 25.0.2
  volume:
    volumeSize: 5Gi
  service:
    type: ClusterIP
```

A complete example can be found [here](config/samples/complete_nextcloud_sample.yaml).
