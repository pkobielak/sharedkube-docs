---
sidebar_position: 3
---

# Configure Storage

SharedKube offers a variety of storage options tailored to fit the needs of different
applications. Our storage solutions are designed to provide flexibility, performance,
and reliability for your workloads.

## Storage Classes

The "fast-ebs" storage class is based on AWS's General Purpose SSD (gp3) volumes, providing
a balance of price and performance. This storage class is an excellent choice for a wide
range of workloads.

### Storage Class Specifications

Below is a table of the current storage options provided by sharedkube.

| Storage Class | Provider | Volume Type | [Access Modes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes) | Use Case                    | Documentation                                                                 |
|---------------|----------|-------------|------------------------------------------------------------------------------|----------------------------|--------------------------------------------------------------------------------|
| fast-ebs      | AWS      | gp3         | RWO                                                                          | General purpose | [AWS gp3 Documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html#EBSVolumeTypes_gp3) |

:::tip
You can always **check the available storage classes** in your environment by running the
following command:

```bash
kubectl get storageclass
```
:::

### Requesting Storage Example

To utilize the "fast-ebs" storage class in your deployments, specify `fast-ebs` as the
storageClassName in your PersistentVolumeClaim (PVC). This will ensure your PVC is
dynamically provisioned with a gp3 volume in AWS.

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: "fast-ebs"
  resources:
    requests:
      storage: 10Gi
```

This YAML snippet demonstrates how to request a 10Gi volume using the "fast-ebs" storage
class.

For assistance or more information on configuring storage for your applications on sharedkube,
please contact us via [Slack](https://join.slack.com/t/sharedkube-community/shared_invite/zt-1ocap8cg6-boDX9eEPSQBQ0S6zllzcGA)
or [email](mailto:support@sharedkube.io).