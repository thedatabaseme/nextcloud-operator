# Nextcloud Operator
------------
The Nextcloud Operator is a Kubernetes controller created with the Operator SDK Framework.
It relies on Ansible roles and make deployment of Nextcloud instances on a Kubernetes
cluster easy.


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