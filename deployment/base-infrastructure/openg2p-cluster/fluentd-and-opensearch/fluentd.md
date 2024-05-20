---
description: Fluentd Install
---

# Fluentd

[Fluentd](https://www.fluentd.org/) is used to parse logs generated by applications. &#x20;

## Installation

### Prerequisites

* The following utilities/tools must be present on the user's machine.
  * `kubectl`, `istioctl`, `helm`, `jq`, `curl`, `wget`, `git`, `bash`, `envsubst`.
* [Keycloak](../../../common-components/keycloak.md) for Authentication and Sign-in to UI

### Fluentd Installation

* Clone the [https://github.com/openg2p/openg2p-deployment](https://github.com/openg2p/openg2p-deployment) repo and navigate to [kubernetes/logging](https://github.com/OpenG2P/openg2p-deployment/tree/main/kubernetes/logging) directory.
* On Rancher UI, navigate to Apps (or Apps & Marketplace) -> Charts
* Search and install Logging from the list, with default values.

### Rancher Fluentd configuration

*   Run this to create _ClusterOutput_ (This is responsible for redirecting all logs to OpenSearch.)

    ```
    kubectl apply -f clusteroutput-opensearch.yaml
    ```
*   Run this to create a _ClusterFlow_ (This is responsible for filtering OpenG2P service logs, from the logs of all pods.)

    ```
    kubectl apply -f clusterflow-all.yaml
    ```

### Filters

The filters applied in [clusterflow-all.yaml](https://github.com/OpenG2P/openg2p-deployment/blob/main/kubernetes/logging/clusterflow-all.yaml). You may update the same for your install if required, and rerun the apply command.&#x20;
