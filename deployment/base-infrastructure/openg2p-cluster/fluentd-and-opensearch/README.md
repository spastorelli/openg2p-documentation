---
description: Deployment of Logging infrastructure
---

# Fluentd & OpenSearch

[Fluentd](https://www.fluentd.org/) and [OpenSearch](https://opensearch.org/) are installed as part of the [Logging](../../../../monitoring-and-reporting/logging.md) infrastructure.  This infrastructure cuts across all modules installed on Kubernetes and hence part of the base infrastructure. Logs from all dockers are parsed and channelised into OpenSearch for searching and viewing.

## Fluentd installation

Fluentd is used to parse logs generated by applications.

Only one Fluentd installation is required per Kubernetes cluster.

* On Rancher UI, navigate to Apps (or Apps & Marketplace) -> Charts
* Search and install Logging with default values from the list. Choose Project as `System` when prompted.

## OpenSearch installation

OpenSearch can now be installed directly as part of  OpenG2P modules. For example, refer to [Social Registry deployment](../../../../social-registry/deployment/) or [PBMS deployment](../../../../pbms/deployment/).

### Setup automatic clean-up of older logs

You can create an [ISM](https://opensearch.org/docs/latest/im-plugin/ism/index/) Policy in OpenSearch to delete logs older than a fixed time. For example, ISM policy is given below.

```json
{
    "policy": {
        "description": "Delete logstash indices after 3days",
        "default_state": "hot",
        "states": [
            {
                "name": "hot",
                "actions": [],
                "transitions": [{
                    "state_name": "delete",
                    "conditions": {
                        "min_index_age": "3d"
                    }
                }]
            },
            {
                "name": "delete",
                "actions": [{"delete": {}}],
                "transitions": []
            }
        ],
        "ism_template": {
            "index_patterns": ["logstash-*"],
            "priority": 100
        }
    }
}
```
