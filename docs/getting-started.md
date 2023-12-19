---
sidebar_position: 2
title: Getting Started
---

### Download tools

Each link below will take you to the installation instructions for the respective tool.

- [aws-cli](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
- [kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl)

### Export your AWS Credentials

Export your AWS credentials by setting the following environment variables:

```shell
export AWS_ACCESS_KEY_ID=<actual_id>
export AWS_SECRET_ACCESS_KEY=<actual_secret>
export AWS_REGION=<assigned_region>
```

### Setup your environment
Configure your AWS EKS by updating the kubeconfig file and setting the Kubernetes
context to your namespace:

```shell
aws eks update-kubeconfig --region $AWS_REGION --name sharedkube
kubectl config set-context --current --namespace <your_namespace>
kubectl get pods # It works!
```

You have access to your namespace and can now deploy your applications.

### Deploy your first application
You can now deploy your first application to your namespace in a common way using
`kubectl`, `helm`, `helmfile`, etc.

In the example below we will:
- deploy a simple nginx application
- expose it via ingress on sharedkube user free subdomain

```shell
helm install my-release oci://registry-1.docker.io/bitnamicharts/nginx \
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
At sharedkube, we are making sure to follow official 
[CNCF definition](https://github.com/cncf/toc/blob/main/DEFINITION.md) of Cloud Native Ecosystem.
