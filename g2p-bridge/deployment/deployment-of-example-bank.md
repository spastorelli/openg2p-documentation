---
description: Helm Chart Deployment of OpenG2P Example Bank Simulator
---

# Deployment of Example Bank

### Prerequisites

Before deploying the Helm charts, ensure that the following prerequisites are met:

1. **Kubernetes Cluster**: A Kubernetes cluster is up and running. You can use any Kubernetes provider.
2. **Helm CLI**: Helm CLI installed. Version 3.x or higher is recommended. You can install Helm using the official Helm installation guide.
3. **Access to Docker Hub**: Ensure that Docker Hub can be accessed to pull the required container images.
4. **Configured Values**: Update the `values.yaml` file with any custom settings needed for your deployment, including image versions, credentials, hostnames, etc.

### Deployment Steps

#### 1. Clone the GitHub Repository

```
# Clone the GitHub repository containing the Helm charts
$ git clone https://github.com/OpenG2P/openg2p-g2p-bridge-example-bank-deployment
$ cd openg2p-g2p-bridge-example-bank-deployment/charts
```

#### 2. Install Helm Dependencies

```
# Install the dependencies for the Helm chart
$ helm dependency update
```

#### 3. Install the Helm Chart

```
# Install the openg2p-g2p-bridge-example-bank chart using Helm
$ helm install openg2p-g2p-example-bank ./openg2p-g2p-bridge-example-bank -f values.yaml -n <namespace>
```

* Replace `openg2p-g2p-example-bank` with the desired release name.
* Replace `namespace` with your kubernetes namespace.
* Use the `-f` flag to provide custom configurations through a `values.yaml` file.

#### 4. Update Values File (Optional)

To customize the configuration, update the `values.yaml` file. Here's a sample of what you might want to configure:

* Set the hostname, Docker image tags, and various other configurations to match your environment.

#### 5. Check the Deployment

After running the install command, ensure that all pods and services are running correctly.

```
# Check the status of the Helm release
$ helm status openg2p-g2p-example-bank

# View the Kubernetes pods and services
$ kubectl get pods,svc
```

#### 6. Updating the Helm Release

If changes are made to the `values.yaml` or any part of the Helm chart, use the following command to upgrade the release:

```
$ helm upgrade openg2p-g2p-example-bank . -f ./values.yaml -n <namespace>
```

#### 7. Uninstalling the Chart

To remove the deployment, run the following:

```
$ helm uninstall openg2p-g2p-example-bank -n <namespace>
```

This will delete all Kubernetes resources associated with the release.
