---
title: Create Experiment
sidebar: mydoc_sidebar
permalink: rm_create_experiment.html
folder: mydoc
---

### Create Experiment API

This is quick guide instructions to create experiments using input JSON as follows. For a more detailed guide,
see [Create Experiment](/design/CreateExperiment.md)

**Note :** The `experiment_type` field in the JSON is optional and can be used to
indicate whether the experiment is of type `namespace` or `container`.
If no experiment type is specified, it will default to `container`.

**Request**
`POST /createExperiment`

`curl -H 'Accept: application/json' -X POST --data 'copy paste below JSON' http://<URL>:<PORT>/createExperiment`

<details>

<summary><b>Example Request</b></summary>

### Example Request

```json
[
  {
    "version": "v2.0",
    "experiment_name": "quarkus-resteasy-autotune-min-http-response-time-db",
    "cluster_name": "cluster-one-division-bell",
    "performance_profile": "resource-optimization-openshift",
    "mode": "monitor",
    "target_cluster": "remote",
    "experiment_type": "container",
    "kubernetes_objects": [
      {
        "type": "deployment",
        "name": "tfb-qrh-deployment",
        "namespace": "default",
        "containers": [
          {
            "container_image_name": "kruize/tfb-db:1.15",
            "container_name": "tfb-server-0"
          },
          {
            "container_image_name": "kruize/tfb-qrh:1.13.2.F_et17",
            "container_name": "tfb-server-1"
          }
        ]
      }
    ],
    "trial_settings": {
      "measurement_duration": "15min"
    },
    "recommendation_settings": {
      "threshold": "0.1"
    }
  }
]
```

</details>


**Response**

<details>
<summary><b>Example Response</b></summary>

### Example Response

```json
{
  "message": "Experiment registered successfully with Autotune. View registered experiments at /listExperiments",
  "httpcode": 201,
  "documentationLink": "",
  "status": "SUCCESS"
}
```

</details>