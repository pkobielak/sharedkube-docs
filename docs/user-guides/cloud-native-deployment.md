---
sidebar_position: 1
---

# Cloud Native Deployment

Learn how to make your application a proper cloud-native citizen.

### What is Cloud Native Deployment?

Cloud Native Deployment is an application that is "native for the cloud environment". So it is
designed to be:
- 💨 **Ephemeral:** Ephemeral applications or components have a short lifecycle, meaning they are 
created and destroyed frequently as needed. This approach is common in cloud environments where
resources are dynamically allocated and deallocated to manage demand efficiently.
- 🔄 **Stateless:** Stateless applications don't retain data or session information from one
interaction to the next. Each transaction is independent, so they can easily scale up or down 
without worrying about synchronizing data across multiple instances.
- 🔍 **Observable:** Observability in applications means having the ability to monitor and understand
the internal state of a system by examining its outputs, like logs, metrics, and traces. This is
crucial for detecting and diagnosing problems and understanding system behavior.
- ⬆️ **Scalable:** Scalability refers to an application's ability to handle increasing loads by adding
resources, either by scaling up (adding more power to existing resources) or scaling out (adding
more instances of resources). A scalable application can maintain performance levels as demands grow.
- 🛠️ **Fault-Tolerant:** Fault tolerance is the capability of an application to continue functioning
correctly even when parts of it fail. This means it can handle errors gracefully, often by having
redundancy or backup systems in place to take over if something goes wrong.

### Requirements

In the context of sharedkube cloud native platform specifics, to maintain the highest level of
conformance with the above definition, we require the following **as a minimum**:
- **All workloads:**
  - ✅ **Resources are set:** CPU and Memory requests and limits must be set for all containers in the pod.
- **Production workloads:**
  - ✅ **At least 2 replicas:** To ensure high availability, at least two replicas of the application.
  - ✅ **Pod Disruption Budget:** To ensure high availability, a [PDB](https://kubernetes.io/docs/tasks/run-application/configure-pdb/)
must be set that is less than the number of replicas.
  - ✅ **Max 90 sec startup time:** To ensure high availability, the application must reach `Ready` state 
within 90 seconds.
  - ✅ **Max 90 sec graceful termination:** To ensure high availability, the application must gracefully
terminate within 90 seconds.

To understand why those are required, have a look at the [Architecture](/architecture/infrastructure) section.

### Example cloud native deployment

Let's take a look at a simple example of a cloud native deployment by expanding on the example from
the [Getting Started Guide](/getting-started).

We assume that our namespace name is `sk-chocolatefig`.

We will operate now on `values.yaml` file that is used by Helm to deploy the application instead
of using `--set` flags.

```yaml title="values.yaml"
# We already had this part in the Getting Started Guide
resources:
  limits:
    cpu: 100m
    memory: 128Mi
  requests:
    cpu: 100m
    memory: 128Mi
service:
  type: ClusterIP
ingress:
  enabled: true
  hostname: sk-chocolatefig.sharedkube.io
# ---

# Production settings
replicaCount: 2
pdb:
  create: true
  minAvailable: 1
terminationGracePeriodSeconds: 90
# ---
```

Deploy the application that meets minimal production requirements:
```shell
helm install my-release oci://registry-1.docker.io/bitnamicharts/nginx -f values.yaml
```

Done! 🎉
