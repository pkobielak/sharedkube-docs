---
sidebar_position: 2
---

# Use Custom Domain

There is also a possibility to assign a custom domain to your service.

### Set up your domain


The simplest way to set up your custom domain is to alias it to the subdomain on sharedkube.io domain.
To do that you need to create a CNAME record in your DNS provider settings.
The CNAME record should point to the created subdomain on sharedkube.io domain.

Let's say you have a domain `bookstore.com` and you want to expose your service on it. 
Your subdomain on sharedkube.io domain is `sk-chocolatefig.sharedkube.io`.
But your service on Sharedkube is running on `bookstore-frontend.sk-chocolatefig.sharedkube.io`
subdomain.

:::info
Make sure your DNS provider supports CNAME flattening.
Example providers that support CNAME flattening are Cloudflare and Namecheap.
:::

Here is an example CNAME record to set in your DNS provider that manages `bookstore.com` domain:
```
Name: @
Type: CNAME
Value: bookstore-frontend.sk-chocolatefig.sharedkube.io
```


In case of any issues contact us via [Slack](https://join.slack.com/t/sharedkube-community/shared_invite/zt-1ocap8cg6-boDX9eEPSQBQ0S6zllzcGA)
or [email](mailto:support@sharedkube.io)  and provide us with your domain name. We will do our best to help
you with the setup.
