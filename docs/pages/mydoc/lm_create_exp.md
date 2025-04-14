---
title: Create Experiment API
sidebar: mydoc_sidebar
permalink: lm_create_exp.html
folder: mydoc
---

## Create Experiment API

This is quick guide instructions to create experiments using input JSON as follows. 

**Request**
`POST /createExperiment`

`curl -H 'Accept: application/json' -X POST --data 'copy paste below JSON' http://<URL>:<PORT>/createExperiment`



### Example Request for datasource - `prometheus-1`

**Example Request**

```json
[
  {
    "version": "v2.0",
    "experiment_name": "default|default|deployment|tfb-qrh-deployment",
    "cluster_name": "default",
    "performance_profile": "resource-optimization-openshift",
    "mode": "monitor",
    "target_cluster": "local",
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
    },
    "datasource": "prometheus-1"
  }
]
```


### Example Request with `experiment_type` field

The `experiment_type` field in the JSON is optional and can be used to
indicate whether the experiment is of type `namespace` or `container`.
If no experiment type is specified, it will default to `container`.


### Example Request with experiment_type - `namespace`

The `experiment_type` field in the JSON is optional and can be used to 
indicate whether the experiment is of type `namespace` or `container`. 
If no experiment type is specified, it will default to `container`.

**EXAMPLE REQUEST**

```json
[{
  "version": "v2.0",
  "experiment_name": "default|namespace-demo",
  "cluster_name": "default",
  "performance_profile": "resource-optimization-local-monitoring",
  "mode": "monitor",
  "target_cluster": "local",
  "datasource": "prometheus-1",
  "experiment_type": "namespace",
  "kubernetes_objects": [
    {
        "namespaces": {
            "namespace_name": "test-multiple-import"
      }
    }
  ],
  "trial_settings": {
    "measurement_duration": "15min"
  },
  "recommendation_settings": {
    "threshold": "0.1"
  }
}]
```


### Example Request with experiment_type - `container`

**EXAMPLE REQUEST**

```json
[
  {
    "version": "v2.0",
    "experiment_name": "default|default|deployment|tfb-qrh-deployment",
    "cluster_name": "default",
    "performance_profile": "resource-optimization-openshift",
    "mode": "monitor",
    "target_cluster": "local",
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
    },
    "datasource": "prometheus-1"
  }
]
```


**Example Response**

```json
{
  "message": "Experiment registered successfully with Autotune. View registered experiments at /listExperiments",
  "httpcode": 201,
  "documentationLink": "",
  "status": "SUCCESS"
}
```


{% include links.html %}
