---
sidebar_position: 2
---

# Use Custom Domain

There is also a possibility to assign a custom domain to your service.

### Create ingress with custom domain

To create an ingress with a custom domain:
1. Set `spec.rules[0].host` field
to your custom domain name.
2. Ensure you have enabled managed ExternalDNS in the UI.
3. Verify that ExternalDNS is working correctly by checking its pod logs.
4. Check if the DNS record for your custom domain is created in your DNS provider.

In case of any issues contact us via Intercom chat in the dashboard or [Slack](https://join.slack.com/t/sharedkube-community/shared_invite/zt-1ocap8cg6-boDX9eEPSQBQ0S6zllzcGA)
or [email](mailto:support@sharedkube.io). We will do our best to help
you with the setup.
