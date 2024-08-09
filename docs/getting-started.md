---
sidebar_position: 2
title: Getting Started
---

### Download Sharedkube CLI

#### Install from [Homebrew](https://brew.sh/):
  ```shell
  brew tap sharedkubeio/skctl
  brew install skctl
  skctl
  ```

#### Install with [pipx](https://pipx.pypa.io/stable/):
  ```shell
  pipx install git+https://github.com/sharedkubeio/skctl
  ```

### Switch to your zone

:::warning
Remember to first create the zone in the [Sharedkube app](https://api.sharedkube.io).
:::

1. **Login**:
    ::::note
    Run the command below, replacing `<your_api_token>` with your actual token.

    ``` shell
    skctl login <your_api_token>
    ```

    :::tip
    If you have used `skctl` before, confirm the override of any existing token by typing `y`.

    ``` shell
    # A token is already saved. Do you want to override it? [y/N]: y
    ```
    :::

    Example:
    ``` yaml
    $ skctl login a43f4ag5hsr56hjr6sr6hsr6hsr6hsr6yhrfes4se4fgsxxxxxxxxxxxxxxxxxxx
    # Login successful. Token saved. Hello Patryk
    ```
    ::::

2. **List Zones**:
    :::note
    View available zones with:

    ``` shell
    skctl zones
    ```

    Example:
    ``` yaml
    $ skctl zones
    # ID                                    Name                    CPU  Memory    Storage    Status    Type
    # 71xxxx28-xxxx-4835-9868-xxxxxx6de5ea  my-company-dev          1    2Gi       10G        draft     Zone.Namespace.NamespaceRQuota
    # 0fxxxx3d-xxxx-4a47-9a74-xxxxxx25a000  my-company-prod         1    2Gi       10G        running   Zone.Namespace.NamespaceRQuota
    ```
    :::

3. **Switch Zone**:
   :::note
   Switch to a specific zone by updating kubeconfig context.

   Command:
   ``` shell
    skctl switch <zone_name>
    ```

    Example:
    ``` yaml
    $ skctl switch my-company-prod
    # Updated kubeconfig for zone: my-company-prod
    ```
    :::

### Useful Additional Commands

:::tip
**Verify Connection**

``` shell
kubectl get pods
```

Example:
``` yaml
$ kubectl get pods
# No resources found in sk-roundmelon namespace. # It works!
```
:::

:::tip
**Check the current namespace name**

``` shell
kubectl config view --minify --output 'jsonpath={..namespace}'
```

Example:
``` yaml
$ kubectl config view --minify --output 'jsonpath={..namespace}'
# sk-roundmelon
```
:::

Now you’re ready to deploy your applications in Sharedkube.


### Deploy your first application
You can now deploy your first application to your namespace in a common way using
`kubectl`, `helm`, `helmfile`, etc.

In the example below we will:
- deploy a simple nginx application
- expose it via ingress on sharedkube user free subdomain

```shell
helm install my-release oci://registry-1.docker.io/bitnamicharts/nginx \
    --version 15.9.3 \
    --set resources.requests.cpu=100m \
    --set resources.requests.memory=128Mi \
    --set resources.limits.cpu=100m \
    --set resources.limits.memory=128Mi \
    --set service.type=ClusterIP \
    --set ingress.enabled=true \
    --set ingress.hostname=<your_namespace>.sharedkube.io
```

Now you can access your application via `https://<your_namespace>.sharedkube.io`.

Read more in [Cloud Native Deployment](./user-guides/cloud-native-deployment) guide.
At Sharedkube, we are making sure to follow official
[CNCF definition](https://github.com/cncf/toc/blob/main/DEFINITION.md) of Cloud Native Ecosystem.
