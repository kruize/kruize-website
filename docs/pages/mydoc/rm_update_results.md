---
title: Update Results API
sidebar: mydoc_sidebar
permalink: rm_update_results.html
folder: mydoc
---

### Update Results API

Update metric results using input JSON as follows. For a more detailed guide,
see [Update results](/design/UpdateResults.md)

* Mandatory parameters in the input JSON:

 ```
 cpuUsage, memoryUsage, memoryRSS
 ```

* Note: If the parameters `cpuRequest`, `cpuLimit`, `memoryRequest` and `memoryLimit` are missing, then they are assumed
  to not have been set for the container in question.

**Request**
`POST /updateResults`

`curl -H 'Accept: application/json' -X POST --data 'copy paste below JSON' http://<URL>:<PORT>/updateResults`

<details>
<summary><b>Example Request Container Experiment</b></summary>

### Example Request
For container experiment :

```json
[
  {
    "version": "v2.0",
    "experiment_name": "quarkus-resteasy-autotune-min-http-response-time-db",
    "interval_start_time": "2022-01-23T18:25:43.511Z",
    "interval_end_time": "2022-01-23T18:40:43.602Z",
    "kubernetes_objects": [
      {
        "type": "deployment",
        "name": "tfb-qrh-deployment",
        "namespace": "default",
        "containers": [
          {
            "container_image_name": "kruize/tfb-qrh:1.13.2.F_et17",
            "container_name": "tfb-server-0",
            "metrics": [
              {
                "name": "cpuRequest",
                "results": {
                  "value": 1.1,
                  "format": "cores",
                  "aggregation_info": {
                    "sum": 4.4,
                    "avg": 1.1,
                    "format": "cores"
                  }
                }
              },
              {
                "name": "cpuLimit",
                "results": {
                  "value": 0.5,
                  "format": "cores",
                  "aggregation_info": {
                    "sum": 2.0,
                    "avg": 0.5,
                    "format": "cores"
                  }
                }
              },
              {
                "name": "cpuUsage",
                "results": {
                  "value": 0.12,
                  "format": "cores",
                  "aggregation_info": {
                    "min": 0.14,
                    "max": 0.84,
                    "sum": 0.84,
                    "avg": 0.12,
                    "format": "cores"
                  }
                }
              },
              {
                "name": "cpuThrottle",
                "results": {
                  "value": 0.045,
                  "format": "cores",
                  "aggregation_info": {
                    "sum": 0.19,
                    "max": 0.09,
                    "avg": 0.045,
                    "format": "cores"
                  }
                }
              },
              {
                "name": "memoryRequest",
                "results": {
                  "value": 50.12,
                  "format": "MiB",
                  "aggregation_info": {
                    "sum": 250.85,
                    "avg": 50.21,
                    "format": "MiB"
                  }
                }
              },
              {
                "name": "memoryLimit",
                "results": {
                  "value": 100,
                  "format": "MiB",
                  "aggregation_info": {
                    "sum": 500,
                    "avg": 100,
                    "format": "MiB"
                  }
                }
              },
              {
                "name": "memoryUsage",
                "results": {
                  "value": 40.1,
                  "format": "MiB",
                  "aggregation_info": {
                    "min": 50.6,
                    "max": 198.50,
                    "sum": 198.50,
                    "avg": 40.1,
                    "format": "MiB"
                  }
                }
              },
              {
                "name": "memoryRSS",
                "results": {
                  "aggregation_info": {
                    "min": 50.6,
                    "max": 123.6,
                    "sum": 123.6,
                    "avg": 31.91,
                    "format": "MiB"
                  }
                }
              }
            ]
          },
          {
            "container_image_name": "kruize/tfb-qrh:1.13.2.F_et17",
            "container_name": "tfb-server-1",
            "metrics": [
              {
                "name": "cpuRequest",
                "results": {
                  "value": 1.1,
                  "format": "cores",
                  "aggregation_info": {
                    "sum": 4.4,
                    "avg": 1.1,
                    "format": "cores"
                  }
                }
              },
              {
                "name": "cpuLimit",
                "results": {
                  "value": 0.5,
                  "format": "cores",
                  "aggregation_info": {
                    "sum": 2.0,
                    "avg": 0.5,
                    "format": "cores"
                  }
                }
              },
              {
                "name": "cpuUsage",
                "results": {
                  "value": 0.12,
                  "format": "cores",
                  "aggregation_info": {
                    "min": 0.14,
                    "max": 0.84,
                    "sum": 0.84,
                    "avg": 0.12,
                    "format": "cores"
                  }
                }
              },
              {
                "name": "cpuThrottle",
                "results": {
                  "value": 0.045,
                  "format": "cores",
                  "aggregation_info": {
                    "sum": 0.19,
                    "max": 0.09,
                    "avg": 0.045,
                    "format": "cores"
                  }
                }
              },
              {
                "name": "memoryRequest",
                "results": {
                  "value": 50.12,
                  "format": "MiB",
                  "aggregation_info": {
                    "sum": 250.85,
                    "avg": 50.21,
                    "format": "MiB"
                  }
                }
              },
              {
                "name": "memoryLimit",
                "results": {
                  "value": 100,
                  "format": "MiB",
                  "aggregation_info": {
                    "sum": 500,
                    "avg": 100,
                    "format": "MiB"
                  }
                }
              },
              {
                "name": "memoryUsage",
                "results": {
                  "value": 40.1,
                  "format": "MiB",
                  "aggregation_info": {
                    "min": 50.6,
                    "max": 198.50,
                    "sum": 198.50,
                    "avg": 40.1,
                    "format": "MiB"
                  }
                }
              },
              {
                "name": "memoryRSS",
                "results": {
                  "aggregation_info": {
                    "min": 50.6,
                    "max": 123.6,
                    "sum": 123.6,
                    "avg": 31.91,
                    "format": "MiB"
                  }
                }
              }
            ]
          }
        ]
      }
    ]
  }
]
```

</details>

<details>
<summary><b>Example Request Namespace Experiment</b></summary>

For namespace experiment:

```json
[
  {
    "version": "v2.0",
    "experiment_name": "namespace-demo",
    "interval_start_time": "2022-01-23T18:25:43.511Z",
    "interval_end_time": "2022-01-23T18:40:43.602Z",
    "kubernetes_objects": [
      {
        "namespaces": 
          {
            "namespace": "default",
            "metrics": [
              {
                "name": "namespaceCpuRequest",
                "results": {
                  "aggregation_info": {
                    "sum": 6,
                    "format": "cores"
                  }
                }
              },
              {
                "name": "namespaceCpuLimit",
                "results": {
                  "aggregation_info": {
                    "sum": 4.5,
                    "format": "cores"
                  }
                }
              },
              {
                "name": "namespaceCpuUsage",
                "results": {
                  "aggregation_info": {
                    "min": 0.14,
                    "max": 0.84,
                    "avg": 0.42,
                    "format": "cores"
                  }
                }
              },
              {
                "name": "namespaceCpuThrottle",
                "results": {
                  "aggregation_info": {
                    "min": 0.01,
                    "max": 0.09,
                    "avg": 0.037,
                    "format": "cores"
                  }
                }
              },
              {
                "name": "namespaceMemoryRequest",
                "results": {
                  "aggregation_info": {
                    "sum": 400,
                    "format": "MiB"
                  }
                }
              },
              {
                "name": "namespaceMemoryLimit",
                "results": {
                  "aggregation_info": {
                    "sum": 600,
                    "format": "MiB"
                  }
                }
              },
              {
                "name": "namespaceMemoryUsage",
                "results": {
                  "aggregation_info": {
                    "min": 60,
                    "max": 180,
                    "avg": 125,
                    "format": "MiB"
                  }
                }
              },
              {
                "name": "namespaceMemoryRSS",
                "results": {
                  "aggregation_info": {
                    "min": 55,
                    "max": 160,
                    "avg": 120,
                    "format": "MiB"
                  }
                }
              },
              {
                "name": "namespaceTotalPods",
                "results": {
                  "aggregation_info": {
                    "max": 3,
                    "avg": 2
                  }
                }
              },
              {
                "name": "namespaceRunningPods",
                "results": {
                  "aggregation_info": {
                    "max": 3,
                    "avg": 2
                  }
                }
              }
            ]
          }
      }
    ]
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
  "message": "Updated metrics results successfully with Autotune. View update results at /listExperiments",
  "httpcode": 201,
  "documentationLink": "",
  "status": "SUCCESS"
}
```

</details>


The UpdateResults API has been enhanced to support bulk uploads of up to 100 records at once. When all records are
successfully processed, the API will return the same success response as depicted above. However, if any or all of the
records encounter failures during processing, the response will differ. Additionally, please take note of the response
structure outlined below for handling duplicate records:

**Response**

<details>
<summary><b>Example Response</b></summary>

### Example Response

```json
{
  "message": "Out of a total of 3 records, 3 failed to save",
  "httpcode": 400,
  "documentationLink": "",
  "status": "ERROR",
  "data": [
    {
      "interval_start_time": "2023-01-01T00:15:00.000Z",
      "interval_end_time": "2023-01-01T00:30:00.000Z",
      "errors": [
        {
          "message": "experiment_name: may not be empty , version: may not be empty",
          "httpcode": 400,
          "documentationLink": "",
          "status": "ERROR"
        }
      ]
    },
    {
      "interval_start_time": "2023-01-01T00:15:00.000Z",
      "interval_end_time": "2023-01-01T00:30:00.000Z",
      "errors": [
        {
          "message": "An entry for this record already exists!",
          "httpcode": 409,
          "documentationLink": "",
          "status": "ERROR"
        }
      ],
      "version": "3.0",
      "experiment_name": "quarkus-resteasy-kruize-min-http-response-time-db_1_1"
    },
    {
      "interval_start_time": "2023-01-01T00:15:00.000Z",
      "interval_end_time": "2023-01-01T00:30:00.000Z",
      "errors": [
        {
          "message": "An entry for this record already exists!",
          "httpcode": 409,
          "documentationLink": "",
          "status": "ERROR"
        }
      ],
      "version": "3.0",
      "experiment_name": "quarkus-resteasy-kruize-min-http-response-time-db_1_1"
    }
  ]
}
```

</details>


**Response**

In the response below, among the three records, one record was successfully saved while the other two records failed.
The failed records are indicated in the 'data' attribute using the 'error' attribute, allowing you to identify the
specific attribute causing the failures.

<details>
<summary><b>Example Response</b></summary>

### Example Response

```json
{
  "message": "Out of a total of 3 records, 2 failed to save",
  "httpcode": 400,
  "documentationLink": "",
  "status": "ERROR",
  "data": [
    {
      "interval_start_time": "2023-01-01T00:15:00.000Z",
      "interval_end_time": "2023-01-01T00:30:00.000Z",
      "errors": [
        {
          "message": "An entry for this record already exists!",
          "httpcode": 409,
          "documentationLink": "",
          "status": "ERROR"
        }
      ],
      "version": "3.0",
      "experiment_name": "quarkus-resteasy-kruize-min-http-response-time-db_1_1"
    },
    {
      "interval_start_time": "2023-01-01T00:30:00.000Z",
      "interval_end_time": "2023-01-01T00:45:00.000Z",
      "errors": [
        {
          "message": "An entry for this record already exists!",
          "httpcode": 409,
          "documentationLink": "",
          "status": "ERROR"
        }
      ],
      "version": "3.0",
      "experiment_name": "quarkus-resteasy-kruize-min-http-response-time-db_1_1"
    }
  ]
}
```

</details>

**Note:**
- In the above API for CPU usage, representation units can be in either cores or milli-cores. The acceptable formats include `cores` and `m`.
- Memory usage can be expressed in bytes. The API also supports fixed-point suffixes like E, P, T, G, M, K and their power-of-two equivalents (Ei, Pi, Ti, Gi, Mi, Ki). 
The acceptable formats are `Bytes, bytes, KiB, MiB, GiB, TiB, PiB, EiB, Ki, Mi, Gi, Ti, Pi, Ei, kB, KB, MB, GB, TB, PB, EB, K, k, M, G, T, P, E`.
