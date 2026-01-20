---
title: Create Metadata Profile
sidebar: mydoc_sidebar
permalink: create_metadata_profile.html
folder: mydoc
---

### Create Metadata Profile API

This is quick guide instructions to create metadata profiles using input JSON as follows. For a more detailed guide,
see [Create MetadataProfile](/design/MetadataProfileAPI.md)

**Request**
`POST /createMetadataProfile`

`curl -H 'Accept: application/json' -X POST --data 'copy paste below JSON' http://<URL>:<PORT>/createMetadataProfile`

<details>

<summary><b>Example Request for profile name - `cluster-metadata-local-monitoring`</b></summary>

### Example Request

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
      "name": "namespacesAcrossCluster",
      "datasource": "prometheus",
      "value_type": "double",
      "kubernetes_object": "container",
      "aggregation_functions": [
        {
          "function": "sum",
          "query": "sum by (namespace) (avg_over_time(kube_namespace_status_phase{namespace!=\"\"}[$MEASUREMENT_DURATION_IN_MIN$m]))"
        }
      ]
    },
    {
      "name": "workloadsAcrossCluster",
      "datasource": "prometheus",
      "value_type": "double",
      "kubernetes_object": "container",
      "aggregation_functions": [
        {
          "function": "sum",
          "query": "sum by (namespace, workload, workload_type) (avg_over_time(namespace_workload_pod:kube_pod_owner:relabel{workload!=\"\"}[$MEASUREMENT_DURATION_IN_MIN$m]))"
        }
      ]
    },
    {
      "name": "containersAcrossCluster",
      "datasource": "prometheus",
      "value_type": "double",
      "kubernetes_object": "container",
      "aggregation_functions": [
        {
          "function": "sum",
          "query": "sum by (container, image, workload, workload_type, namespace) (avg_over_time(kube_pod_container_info{container!=\"\"}[$MEASUREMENT_DURATION_IN_MIN$m]) * on (pod, namespace) group_left(workload, workload_type) avg_over_time(namespace_workload_pod:kube_pod_owner:relabel{workload!=\"\"}[$MEASUREMENT_DURATION_IN_MIN$m]))"
        }
      ]
    }
  ]
}
```

</details>


**Response**

<details>
<summary><b>Example Response</b></summary>

### Example Response

```json
{
  "message": "Metadata Profile : cluster-metadata-local-monitoring created successfully. View all metadata profiles at /listMetadataProfiles",
  "httpcode": 201,
  "documentationLink": "",
  "status": "SUCCESS"
}
```

</details>

### Invalid Scenarios:

<details>
<summary><b>Missing mandatory fields</b></summary>

Mandatory fields required to create MetadataProfile are - `apiVersion`, `kind`, `metadata`, `name`, `datasource`, `query_variables`

Example: With missing profile "name"
```json
{
  "message": "Validation failed: JSONObject[\"name\"] not found.",
  "httpcode": 500,
  "documentationLink": "",
  "status": "ERROR"
}
```

</details>

<details>
<summary><b>Duplicate attempt to create MetadataProfile</b></summary>

```json
{
  "message": "Validation failed: Metadata Profile already exists: cluster-metadata-local-monitoring",
  "httpcode": 409,
  "documentationLink": "",
  "status": "ERROR"
}
```

</details>


<details>
<summary><b>Missing mandatory fields from `query_variables`</b></summary>

Mandatory fields of `query_variables` are - `name`, `aggregation_functions`, `function`, `query`

Example: With missing "query"
```json
{
  "message": "Validation failed: JSONObject[\"query\"] not found.",
  "httpcode": 500,
  "documentationLink": "",
  "status": "ERROR"
}
```

</details>

<br>

<a name="list-metadata-profiles-api"></a>

### List Metadata Profiles API

This is quick guide instructions to retrieve metadata profiles created as follows.

**Request Parameters**

| Parameter | Type   | Required | Description                               |
|-----------|--------|----------|-------------------------------------------|
| name      | string | optional | The name of the metadata profile          |
| verbose   | string | optional | Flag to retrieve all the metadata queries |

**Request without passing parameters**

`GET /listMetadataProfiles`

`curl -H 'Accept: application/json' http://<URL>:<PORT>/listMetadataProfiles`

Returns list of all the metadata profile names created

<details>
<summary><b>Example Response</b></summary>

### Example Response

```json
[
  {
    "name": "cluster-metadata-local-monitoring"
  },
  {
    "name": "bulk-cluster-metadata-local-monitoring"
  }
]
```

</details>

<br>

**Request with metadata profile name**

`GET /listMetadataProfiles`

`curl -H 'Accept: application/json' http://<URL>:<PORT>/listMetadataProfiles?name=cluster-metadata-local-monitoring`

Returns metadata profile of the name specified

<details>
<summary><b>Example Response</b></summary>

### Example Response

```json
[
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
        "name": "namespacesAcrossCluster",
        "datasource": "prometheus",
        "value_type": "double",
        "kubernetes_object": "container",
        "aggregation_functions": [
          {
            "function": "sum",
            "query": "sum by (namespace) (avg_over_time(kube_namespace_status_phase{namespace!=\"\"}[$MEASUREMENT_DURATION_IN_MIN$m]))"
          }
        ]
      },
      {
        "name": "workloadsAcrossCluster",
        "datasource": "prometheus",
        "value_type": "double",
        "kubernetes_object": "container",
        "aggregation_functions": [
          {
            "function": "sum",
            "query": "sum by (namespace, workload, workload_type) (avg_over_time(namespace_workload_pod:kube_pod_owner:relabel{workload!=\"\"}[$MEASUREMENT_DURATION_IN_MIN$m]))"
          }
        ]
      },
      {
        "name": "containersAcrossCluster",
        "datasource": "prometheus",
        "value_type": "double",
        "kubernetes_object": "container",
        "aggregation_functions": [
          {
            "function": "sum",
            "query": "sum by (container, image, workload, workload_type, namespace) (avg_over_time(kube_pod_container_info{container!=\"\"}[$MEASUREMENT_DURATION_IN_MIN$m]) * on (pod, namespace) group_left(workload, workload_type) avg_over_time(namespace_workload_pod:kube_pod_owner:relabel{workload!=\"\"}[$MEASUREMENT_DURATION_IN_MIN$m]))"
          }
        ]
      }
    ]
  }
]
```

</details>

<br>

**Request**

`GET /listMetadataProfiles`

`curl -H 'Accept: application/json' http://<URL>:<PORT>/listMetadataProfiles?verbose=true`

Returns list of all the metadata profile created with all the metadata queries

<details>
<summary><b>Example Response</b></summary>

### Example Response

```json
[
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
        "name": "namespacesAcrossCluster",
        "datasource": "prometheus",
        "value_type": "double",
        "kubernetes_object": "container",
        "aggregation_functions": [
          {
            "function": "sum",
            "query": "sum by (namespace) (avg_over_time(kube_namespace_status_phase{namespace!=\"\"}[$MEASUREMENT_DURATION_IN_MIN$m]))"
          }
        ]
      },
      {
        "name": "workloadsAcrossCluster",
        "datasource": "prometheus",
        "value_type": "double",
        "kubernetes_object": "container",
        "aggregation_functions": [
          {
            "function": "sum",
            "query": "sum by (namespace, workload, workload_type) (avg_over_time(namespace_workload_pod:kube_pod_owner:relabel{workload!=\"\"}[$MEASUREMENT_DURATION_IN_MIN$m]))"
          }
        ]
      },
      {
        "name": "containersAcrossCluster",
        "datasource": "prometheus",
        "value_type": "double",
        "kubernetes_object": "container",
        "aggregation_functions": [
          {
            "function": "sum",
            "query": "sum by (container, image, workload, workload_type, namespace) (avg_over_time(kube_pod_container_info{container!=\"\"}[$MEASUREMENT_DURATION_IN_MIN$m]) * on (pod, namespace) group_left(workload, workload_type) avg_over_time(namespace_workload_pod:kube_pod_owner:relabel{workload!=\"\"}[$MEASUREMENT_DURATION_IN_MIN$m]))"
          }
        ]
      }
    ]
  },
  {
    "apiVersion": "recommender.com/v1",
    "kind": "KruizeMetadataProfile",
    "metadata": {
      "name": "bulk-cluster-metadata-local-monitoring"
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
        "name": "containersForAdditionalLabel",
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
]
```

</details>

### Invalid Scenarios:

<details>
<summary><b>Invalid or Non-existing MetadataProfile name</b></summary>

`name="xyz"`(Can be either invalid or non-existing profile name)

`curl -H 'Accept: application/json' http://<URL>:<PORT>/listMetadataProfiles?name=xyz`
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
<summary><b>Invalid query parameters</b></summary>

Supported query parameters are `name` and `verbose`

`curl -H 'Accept: application/json' http://<URL>:<PORT>/listMetadataProfiles?profilename=cluster-metadata-local-monitoring`
```json
{
  "message": "The query param(s) - [profilename] is/are invalid",
  "httpcode": 400,
  "documentationLink": "",
  "status": "ERROR"
}
```

</details>