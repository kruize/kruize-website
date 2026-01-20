---
title: Delete Metadata Profile
sidebar: mydoc_sidebar
permalink: delete_metadata_profile.html
folder: mydoc
---

### Delete Metadata Profile API

This is quick guide instructions to delete metadata profile created as follows.

**Request Parameters**

| Parameter | Type   | Required | Description                      |
|-----------|--------|----------|----------------------------------|
| name      | string | required | The name of the metadata profile |


**Request with name query parameter**

`DELETE /deleteMetadataProfile`

`curl -H 'Accept: application/json' http://<URL>:<PORT>/deleteMetadataProfile?name=cluster-metadata-local-monitoring`

Deletes the specified metadata profile name, provided metadata profile already is created

<details>
<summary><b>Example Response</b></summary>

### Example Response

```json
{
  "message": "Metadata profile: cluster-metadata-local-monitoring deleted successfully. View Metadata Profiles at /listMetadataProfiles",
  "httpcode": 201,
  "documentationLink": "",
  "status": "SUCCESS"
}
```

</details>

### Invalid Scenarios:

<details>
<summary><b>Invalid or Non-existing MetadataProfile name</b></summary>

`name="xyz"`(Can be either invalid or non-existing profile name)

`curl -H 'Accept: application/json' -X DELETE http://<URL>:<PORT>/deleteMetadataProfile?name=xyz`

```json
{
  "message": "Given metadata profile name - xyz either does not exist or is not valid",
  "httpcode": 400,
  "documentationLink": "",
  "status": "ERROR"
}
```

</details>

<details>
<summary><b>Missing query parameter</b></summary>

Supported query parameter is `name`

Example: `curl -H 'Accept: application/json' -X DELETE http://<URL>:<PORT>/deleteMetadataProfile`
```json
{
  "message": "Missing metadata profile 'name' parameter",
  "httpcode": 400,
  "documentationLink": "",
  "status": "ERROR"
}
```

</details>

<br>

<a name="update-metadata-profile-api"></a>


### Update Metadata Profile API

This is quick guide instructions to update metadata profile as follows.

**Request Parameters**

| Parameter | Type   | Required | Description                      |
|-----------|--------|----------|----------------------------------|
| name      | string | required | The name of the metadata profile |


**Request with name query parameter**

`PUT /updateMetadataProfile`

`curl -H 'Accept: application/json' -X PUT --data 'copy paste below JSON' http://<URL>:<PORT>/updateMetadataProfile?name=cluster-metadata-local-monitoring`

<details>

Updates the specified metadata profile name, provided metadata profile is already created

<summary><b>Example Request</b></summary>

```json
{
  "apiVersion": "recommender.com/v1",
  "kind": "KruizeMetadataProfile",
  "metadata": {
    "name": "cluster-metadata-local-monitoring"
  },
  "profile_version": 1,
  "k8s_type": "openshift",
  "datasource": "prometheus",
  "query_variables": [
    {
      "name": "namespacesForAdditionalLabel",
      "datasource": "prometheus",
      "value_type": "double",
      "kubernetes_object": "container",
      "aggregation_functions": [
        {
          "function": "sum",
          "query": "sum by (namespace) (avg_over_time(kube_namespace_status_phase{namespace!=\"\", namespace=~\"openshift-tuning|monitoring\" ADDITIONAL_LABEL}[$MEASUREMENT_DURATION_IN_MIN$m]))"
        }
      ]
    },
    {
      "name": "workloadsForAdditionalLabel",
      "datasource": "prometheus",
      "value_type": "double",
      "kubernetes_object": "container",
      "aggregation_functions": [
        {
          "function": "sum",
          "query": "sum by (namespace, workload, workload_type) (avg_over_time(namespace_workload_pod:kube_pod_owner:relabel{workload!=\"\", workload=\"kruize\" ADDITIONAL_LABEL}[$MEASUREMENT_DURATION_IN_MIN$m]))"
        }
      ]
    },
    {
      "name": "containerForAdditionalLabel",
      "datasource": "prometheus",
      "value_type": "double",
      "kubernetes_object": "container",
      "aggregation_functions": [
        {
          "function": "sum",
          "query": "sum by (container, image, workload, workload_type, namespace) (avg_over_time(kube_pod_container_info{container!=\"\", container=\"kruize\" ADDITIONAL_LABEL}[$MEASUREMENT_DURATION_IN_MIN$m]) * on (pod, namespace) group_left(workload, workload_type) avg_over_time(namespace_workload_pod:kube_pod_owner:relabel{workload!=\"\" ADDITIONAL_LABEL}[$MEASUREMENT_DURATION_IN_MIN$m]))"
        }
      ]
    }
  ]
}
```
</details>

<details>
<summary><b>Example Response</b></summary>

### Example Response

```json
{
  "message": "Metadata profile: cluster-metadata-local-monitoring updated successfully. View Metadata Profiles at /listMetadataProfiles",
  "httpcode": 201,
  "documentationLink": "",
  "status": "SUCCESS"
}
```

</details>

### Invalid Scenarios:

<details>
<summary><b>Invalid or Non-existing MetadataProfile name</b></summary>

`name="xyz"`(Can be either invalid or non-existing profile name)

`curl -H 'Accept: application/json' -X PUT http://<URL>:<PORT>/updateMetadataProfile?name=xyz`

```json
{
  "message": "Given metadata profile name - xyz either does not exist or is not valid",
  "httpcode": 400,
  "documentationLink": "",
  "status": "ERROR"
}
```

</details>

<details>
<summary><b>Missing query parameter</b></summary>

Supported query parameter is `name`

Example: `curl -H 'Accept: application/json' -X PUT http://<URL>:<PORT>/updateMetadataProfile`
```json
{
  "message": "Missing metadata profile 'name' parameter",
  "httpcode": 400,
  "documentationLink": "",
  "status": "ERROR"
}
```

</details>

<details>
<summary><b>Mismatch in JSON payload and input parameter profile names</b></summary>

Supported query parameter is `name`

Example: `curl -H 'Accept: application/json' -X PUT http://<URL>:<PORT>/updateMetadataProfile?name=cluster-metadata-local-monitoring`

<details>

<summary><b>Example Request with non-existing profile name</b></summary>

```json
{
  "apiVersion": "recommender.com/v1",
  "kind": "KruizeMetadataProfile",
  "metadata": {
    "name": "cluster-metadata-local-monitoring1"
  },
  "profile_version": 1,
  "k8s_type": "openshift",
  "datasource": "prometheus",
  "query_variables": [
    {
      "name": "namespacesForAdditionalLabel",
      "datasource": "prometheus",
      "value_type": "double",
      "kubernetes_object": "container",
      "aggregation_functions": [
        {
          "function": "sum",
          "query": "sum by (namespace) (avg_over_time(kube_namespace_status_phase{namespace!=\"\" ADDITIONAL_LABEL}[$MEASUREMENT_DURATION_IN_MIN$m]))"
        }
      ]
    },
    {
      "name": "workloadsForAdditionalLabel",
      "datasource": "prometheus",
      "value_type": "double",
      "kubernetes_object": "container",
      "aggregation_functions": [
        {
          "function": "sum",
          "query": "sum by (namespace, workload, workload_type) (avg_over_time(namespace_workload_pod:kube_pod_owner:relabel{workload!=\"\" ADDITIONAL_LABEL}[$MEASUREMENT_DURATION_IN_MIN$m]))"
        }
      ]
    },
    {
      "name": "containerForAdditionalLabel",
      "datasource": "prometheus",
      "value_type": "double",
      "kubernetes_object": "container",
      "aggregation_functions": [
        {
          "function": "sum",
          "query": "sum by (container, image, workload, workload_type, namespace) (avg_over_time(kube_pod_container_info{container!=\"\" ADDITIONAL_LABEL}[$MEASUREMENT_DURATION_IN_MIN$m]) * on (pod, namespace) group_left(workload, workload_type) avg_over_time(namespace_workload_pod:kube_pod_owner:relabel{workload!=\"\" ADDITIONAL_LABEL}[$MEASUREMENT_DURATION_IN_MIN$m]))"
        }
      ]
    }
  ]
}
```
</details>

```json
{
  "message": "MetadataProfile name in URL: cluster-metadata-local-monitoring, does not match name in request body: cluster-metadata-local-monitoring1",
  "httpcode": 400,
  "documentationLink": "",
  "status": "ERROR"
}
```

</details>