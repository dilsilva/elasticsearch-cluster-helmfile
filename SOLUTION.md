## Architecture and choices

My approach in a nutshell was to follow the simplest solution possible, using the official Elastic Helm Charts.

# Helm Charts/Helmfile:

Besides the basics (widely used, simple to manage) the chart choosen it's maintain by the own company, and also allows us to cherry pick many different functionalities of [their suite](https://github.com/elastic/cloud-on-k8s/tree/main/deploy/eck-stack/charts) simple adjusting and filling the values.
It also comes with TLS communication using third party/owon certificates (or self signed to run examples).
The Helmfile also enhances the capabilities of the charts, allowing us to handle whole environemts (multiple clusters) in a single file, what shines in the case of a disaster recovery.

# Availability:

Some affinity strategies like [preferredDuringSchedulingIgnoredDuringExecution](preferredDuringSchedulingIgnoredDuringExecution) was defined to avoid having multiple replicas of the same pod, distributing the load on the cluster.
While `requiredDuringSchedulingIgnoredDuringExecution` will guarantee that the pods will be distributed across the listed zones available.

# System Upgrades
Strategies like `podDisruptionBudget` supports the upgrade process of the charts, guaranteeing the availability of the pods during the upgrade. And in case of some unexpected error, the charts can be rolled back to the previous version using `Helm Rollback` for example.

# Cluster Scaling
Can be easily adjusted using the `replicas` parameter on the `values.yaml` file for horizontal scaling, and the limits/requests on the `resources` section.

# Security:
Security aspects was also covered, with the already mentioned TLS communication, but also using the securityContexts on the pods to avoid running containers as root.
ECK stack also allows integration for third party authentication, and also the usage of RBAC to handle the access to the cluster, the current configuration is implementing the default roles and permissions, and 

# Metrics:
The Elastic Stack provides a wide variety of metrics, which can be used to monitor the health and performance of the cluster, and also to detect anomalies. It was not explored in deepness on this project, but it's can be implemented with certain ease through `monitoring.metric` section on the `stack.yaml` Values file.

## CICD
The CD process was implemented using Github Actions, and the Helmfile to deploy the charts. The $KUBECONFIG file can simply be changed to point to the desired cluster.
There is also a small Helm Lint implemented as sample of a testing step, leaving room for further improvements.

# Future Improvements.
Internalize artifacts in general (charts, images) - Rebuildar com testes de segurança (CVE)
Manage secrets using external solutions (Cloud Manage or Hashicorp Vault)
Automation for disaster recovery using the currently implemented CD proccess (simple changing the $KUBECONFIG file) 
Implement cluster security policies (Admission Controller, Network Policy)
Optimise instance types for execution type using `nodeSet` available on chart
Make roles and permissions granular as possible (following Least Privilege)