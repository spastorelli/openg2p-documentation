---
description: >-
  This document provides an overview of all necessary artifacts to deploy the
  G2P Bridge application, stored in designated repositories to ensure controlled
  access and ease of deployment.
---

# Deployment Artefacts

**1. Helm Chart for G2P Bridge**

* **Purpose**: Deploys the complete G2P Bridge suite on Kubernetes, including the API, Celery Beat (for scheduled tasks), and Celery Workers (for background processing).
* **Repository**: [G2P Bridge Deployment on GitHub](https://github.com/OpenG2P/openg2p-g2p-bridge-deployment)
* **Access and Installation**:
  *   Add the GitHub Helm chart repository and install the `openg2p-g2p-bridge` chart, which includes all G2P Bridge components:

      {% code overflow="wrap" %}
      ```bash
      helm repo add openg2p https://github.com/OpenG2P/openg2p-g2p-bridge-deployment
      helm repo update
      helm install openg2p-g2p-bridge openg2p/openg2p-g2p-bridge --namespace your-namespace
      ```
      {% endcode %}
  * **Environment Configuration**: Ensure the required environment variables are configured  before installation. Refer to[ G2P Bridge Developer](https://docs.openg2p.org/g2p-bridge/development/developer-install/installing-openg2p-bridge-on-linux#docs-internal-guid-f8d8e15e-7fff-3872-8a9f-bfbb05735977) section to know more about environment configuration.

***

**2. Docker Images**

* **Purpose**: Provides containerized versions of each G2P Bridge component for consistent and repeatable deployments.
* **Repository**: Docker Hub
* **Available Images**:
  * **API**: [openg2p-g2p-bridge-api](https://hub.docker.com/r/openg2p/openg2p-g2p-bridge-api)
  * **Celery Workers**: [openg2p-g2p-bridge-celery-workers](https://hub.docker.com/r/openg2p/openg2p-g2p-bridge-celery-workers)
  * **Celery Beat Producers**: [openg2p-g2p-bridge-celery-beat-producers](https://hub.docker.com/r/openg2p/openg2p-g2p-bridge-celery-beat-producers)
* **Usage**:
  *   Each image can be pulled directly from Docker Hub:

      ```bash
      bashCopy codedocker pull openg2p/openg2p-g2p-bridge-api:<version>
      docker pull openg2p/openg2p-g2p-bridge-celery-workers:<version>
      docker pull openg2p/openg2p-g2p-bridge-celery-beat-producers:<version>
      ```
  * Replace `<version>` with the specific tag or `latest` for the latest stable release.

***

**2. Python Libraries**

* **Purpose**: Provides essential libraries and dependencies for G2P Bridge services. These are available on PyPI and should be installed where necessary.
* **Repository**: [PyPI (Python Package Index)](https://pypi.org/)
* **Available Libraries**:
  * `openg2p-fastapi-common`: Common FastAPI components.
  * `openg2p-fastapi-auth`: Authentication modules.
  * `openg2p-g2pconnect-common-lib`: Core library for G2P Connect.
  * `openg2p-g2p-bridge-models`: Database models.
  * `openg2p-g2p-bridge-api`: API components.
  * `openg2p-g2p-bridge-bank-connectors`: Bank connectors for financial integration.
  * `openg2p-g2p-bridge-celery-beat-producers`: Schedulers for Celery tasks.
  * `openg2p-g2p-bridge-celery-workers`: Workers for background processing.
* **Installation**:
  *   Install each required package using `pip`:

      ```bash
      pip install openg2p-fastapi-common
      pip install openg2p-fastapi-auth
      pip install openg2p-g2pconnect-common-lib
      pip install openg2p-g2p-bridge-models
      pip install openg2p-g2p-bridge-api
      pip install openg2p-g2p-bridge-bank-connectors
      pip install openg2p-g2p-bridge-celery-beat-producers
      pip install openg2p-g2p-bridge-celery-workers
      ```

***

**3. Post-Installation Configuration**

After deploying the G2P Bridge, the following database table must be configured to enable the benefit program features:

* **Table**: `benefit_program_configurations`
* **Purpose**: Stores configuration details for each benefit program, which are essential for the operation of the G2P Bridge.

Populate this table with required rows for each benefit program. Below is an example configuration (replace with your own details):

<table><thead><tr><th width="262">benefit_program_mnemonic</th><th width="221">benefit_program_name</th><th>funding_org_code</th><th>funding_org_name</th><th>sponsor_bank_code</th><th>sponsor_bank_account_number</th><th>sponsor_bank_branch_code</th><th>sponsor_bank_account_currency</th><th>id_mapper_resolution_required</th><th>active</th></tr></thead><tbody><tr><td>EXAMPLE_PROGRAM</td><td>Example Benefit Program</td><td>EXB</td><td>Example_Org </td><td>EXAMPLE</td><td>EXAMPLE_ACC_1</td><td>EX001</td><td>USD</td><td>true</td><td>true</td></tr></tbody></table>

Populate this table with the relevant program information to enable program-specific configurations within the G2P Bridge.
