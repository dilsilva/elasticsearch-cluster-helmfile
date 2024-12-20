## ECK for Kubernetes

Elasticsearch ECK (Elastic Cloud on Kubernetes) is a powerful solution for running Elasticsearch, Kibana, and APM Server on Kubernetes.


ECK provides robust features such as Elasticsearch cluster management, scaling, rolling upgrades, snapshot and restore, monitoring, and more.

You can use Elasticsearch ECK to manage and scale your Elasticsearch deployments, ensuring high availability and performance. It can handle various workloads, from traditional search and analytics to observability and security use cases.

This chart bootstraps all the components needed to run Elasticsearch ECK on a Kubernetes Cluster using [Helm](https://helm.sh) and [Helmfile](https://helmfile.readthedocs.io/en/latest/).

## Prerequisites

* Kubernetes v1.29.3+
* Helm v3+
* Helmfile v0.167.0+


## Install

To install the chart:

```sh
helmfile --interactive --environment ${ENV_NAME} sync

or for example:

helmfile --interactive --environment default sync
```


## Accessing the Elasticsearch cluster

This cluster is not exposed to the public internet, so you need to access it from within the Kubernetes cluster.
The easiest way to do this is to use the `kubectl port-forward` command.

`kubectl port-forward service/kibana-kb-http 5601:5601 &`
`kubectl port-forward service/kibana-kb-http 9200:9200 &`

Then you can access Kibana on `https://localhost:5601` and Elasticsearch on `https://localhost:9200`.

## Authentication

There's a secret called `elasticsearch-es-elastic-user` available on the namespace `elastic-stack`, which contains the credentials for the `elastic` user.
Use your permissions to get this credentials and access both Kibana and Elasticsearch.

## Uninstall

To uninstall/delete the environment:

 ```sh
helmfile destroy --environment ${ENV_NAME}

or for example:

helmfile destroy --environment default
 ```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Values

The standard Values are populated under `values/` directory, following the bellow references:

For Operator
https://github.com/elastic/cloud-on-k8s/blob/main/deploy/eck-operator/values.yaml

For Stack
https://github.com/elastic/cloud-on-k8s/tree/main/deploy/eck-stack/charts


## Environments
Each environments apply the default Values mentioned with adjusts for each case, i.e. `environments/default/` Values have less functionalities and implements less replicas with low resources while `environments/production/` implements Affinity strategies, Security restrictions and Monitoring capabilities.

> See [SOLUTION.md] to understand the quirks and details around the decisions
> taken during the implementation of the solution

## Verify your connection to Kubernetes

```bash
export KUBECONFIG=<path>
kubectl auth can-i delete pods
```


[INSTRUCTIONS.md]: ./INSTRUCTIONS.md
[SOLUTION.md]: ./SOLUTION.md
