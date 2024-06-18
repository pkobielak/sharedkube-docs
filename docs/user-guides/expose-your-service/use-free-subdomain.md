---
sidebar_position: 1
---

# Use Free Subdomain

In all sharedkube packages you have access to one free subdomain on sharedkube.io domain.
You can use it to expose your applications via 
[ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/).

:::warning
Make sure to enable managed Cert-Manager in the UI to get free SSL certificates for your subdomains.
:::

### Get your subdomain name

Your subdomain name is randomly generated and looks like this: `<namespace_name>.sharedkube.io`.

To check your `namespace_name` log in to [Dashboard](https://api.sharedkube.io) and under your zone details check
`Namespace Name:` field. It will begin with `sk-` prefix.

![namespace_name_location_screenshot.png](img/namespace_name_location_screenshot.png)

This example user subdomain name is `sk-cyancitron.sharedkube.io`. Feel free to also use
all deeper levels of subdomains like `level2.sk-cyancitron.sharedkube.io` or 
`level3.level2.sk-cyancitron.sharedkube.io` and so on.

### Use your subdomain to create ingress

To use your subdomain to create ingress, you need to set `spec.rules[0].host` field to your
subdomain name.

:::warning
Ensure you accurately set the `spec.rules[0].host` field to your subdomain name to avoid any issues with ingress creation.
:::

Here is an example of ingress manifest that uses `sk-cyancitron.sharedkube.io` subdomain:

```yaml title="ingress.yaml"
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-release-nginx
  namespace: sk-cyancitron
spec:
  ingressClassName: nginx
  rules:
// highlight-next-line
  - host: sk-cyancitron.sharedkube.io
    http:
      paths:
      - backend:
          service:
            name: my-release-nginx
            port:
              name: http
        path: /
        pathType: ImplementationSpecific
```

Good job, you have just created your first ingress on Sharedkube! 🎉

In case of any issues contact us via Intercom chat in the dashboard or [Slack](https://join.slack.com/t/sharedkube-community/shared_invite/zt-1ocap8cg6-boDX9eEPSQBQ0S6zllzcGA)
or [email](mailto:support@sharedkube.io). We will do our best to help
you with the setup.
