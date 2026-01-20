---
title: List Metadata
sidebar: mydoc_sidebar
permalink: list_metadata.html
folder: mydoc
---

### List Metadata API

This is quick guide instructions to retrieve metadata for a specific datasource as follows.

**Request Parameters**

| Parameter    | Type   | Required | Description                               |
|--------------|--------|----------|-------------------------------------------|
| datasource   | string | Yes      | The name of the datasource.               |
| cluster_name | string | optional | The name of the cluster                   |
| namespace    | string | optional | The namespace                             |
| verbose      | string | optional | Flag to retrieve container-level metadata |

In the context of `GET /dsmetadata` REST API, the term `verbose` refers to a parameter or option that controls
granularity of metadata included in the API response. When the verbose parameter is set to true, the API response 
includes granular container-level details in the metadata, offering a more comprehensive view of the clusters, namespaces,
workloads and containers associated with the specified datasource. When the verbose parameter is not provided or set to
false, the API response provides basic information like list of clusters, namespaces associated with the specified datasource.

**Request with datasource name parameter**

`GET /dsmetadata`

`curl -H 'Accept: application/json' http://<URL>:<PORT>/dsmetadata?datasource=<datasource_name>`

Returns the list of cluster details of the specified datasource

**Response for datasource name - `prometheus-1`**

***Note:***
- Currently, only `default` cluster is supported for POC.
- When the `verbose` parameter is not provided, is set to `false` by default - the response provides basic information
about the clusters of the specified datasource.

<details>
<summary><b>Example Response</b></summary>

### Example Response

```json
{
  "datasources": {
    "prometheus-1": {
      "datasource_name": "prometheus-1",
      "clusters": {
        "default": {
          "cluster_name": "default"
        }
      }
    }
  }
}
```
</details>

<br>

**Request with verbose set to true and with datasource name parameter**

`GET /dsmetadata`

`curl -H 'Accept: application/json' "http://<URL>:<PORT>/dsmetadata?datasource=<datasource_name>&verbose=true"`

Returns the metadata of all the containers present in the specified datasource

***Note : When we don't pass `verbose` in the query URL, it is set to `false` by default.***

**Response for datasource name - `prometheus-1` and verbose - `true`**

With `verbose` parameter set to `true`, the response includes detailed metadata about all namespaces, workloads and
containers in addition to cluster information with the specified datasource.

<details>
<summary><b>Example Response</b></summary>

### Example Response

```json
{
  "datasources": {
    "prometheus-1": {
      "datasource_name": "prometheus-1",
      "clusters": {
        "default": {
          "cluster_name": "default",
          "namespaces": {
            "default": {
              "namespace": "default"
            },
            "cadvisor": {
              "namespace": "cadvisor",
              "workloads": {
                "cadvisor": {
                  "workload_name": "cadvisor",
                  "workload_type": "daemonset",
                  "containers": {
                    "cadvisor": {
                      "container_name": "cadvisor",
                      "container_image_name": "gcr.io/cadvisor/cadvisor:v0.45.0"
                    }
                  }
                }
              }
            },
            "kube-node-lease": {
              "namespace": "kube-node-lease"
            },
            "kube-system": {
              "namespace": "kube-system",
              "workloads": {
                "coredns": {
                  "workload_name": "coredns",
                  "workload_type": "deployment",
                  "containers": {
                    "coredns": {
                      "container_name": "coredns",
                      "container_image_name": "k8s.gcr.io/coredns/coredns:v1.8.6"
                    }
                  }
                },
                "kube-proxy": {
                  "workload_name": "kube-proxy",
                  "workload_type": "daemonset",
                  "containers": {
                    "kube-proxy": {
                      "container_name": "kube-proxy",
                      "container_image_name": "k8s.gcr.io/kube-proxy:v1.24.3"
                    }
                  }
                }
              }
            },
            "monitoring": {
              "namespace": "monitoring",
              "workloads": {
                "kube-state-metrics": {
                  "workload_name": "kube-state-metrics",
                  "workload_type": "deployment",
                  "containers": {
                    "kube-state-metrics": {
                      "container_name": "kube-state-metrics",
                      "container_image_name": "k8s.gcr.io/kube-state-metrics/kube-state-metrics:v2.0.0"
                    },
                    "kube-rbac-proxy-self": {
                      "container_name": "kube-rbac-proxy-self",
                      "container_image_name": "quay.io/brancz/kube-rbac-proxy:v0.8.0"
                    },
                    "kube-rbac-proxy-main": {
                      "container_name": "kube-rbac-proxy-main",
                      "container_image_name": "quay.io/brancz/kube-rbac-proxy:v0.8.0"
                    }
                  }
                },
                "node-exporter": {
                  "workload_name": "node-exporter",
                  "workload_type": "daemonset",
                  "containers": {
                    "node-exporter": {
                      "container_name": "node-exporter",
                      "container_image_name": "quay.io/prometheus/node-exporter:v1.1.2"
                    },
                    "kube-rbac-proxy": {
                      "container_name": "kube-rbac-proxy",
                      "container_image_name": "quay.io/brancz/kube-rbac-proxy:v0.8.0"
                    }
                  }
                },
                "postgres-deployment": {
                  "workload_name": "postgres-deployment",
                  "workload_type": "deployment",
                  "containers": {
                    "postgres": {
                      "container_name": "postgres",
                      "container_image_name": "quay.io/kruizehub/postgres:15.2"
                    }
                  }
                },
                "alertmanager-main": {
                  "workload_name": "alertmanager-main",
                  "workload_type": "statefulset",
                  "containers": {
                    "config-reloader": {
                      "container_name": "config-reloader",
                      "container_image_name": "quay.io/prometheus-operator/prometheus-config-reloader:v0.47.0"
                    },
                    "alertmanager": {
                      "container_name": "alertmanager",
                      "container_image_name": "quay.io/prometheus/alertmanager:v0.21.0"
                    }
                  }
                },
                "prometheus-adapter": {
                  "workload_name": "prometheus-adapter",
                  "workload_type": "deployment",
                  "containers": {
                    "prometheus-adapter": {
                      "container_name": "prometheus-adapter",
                      "container_image_name": "directxman12/k8s-prometheus-adapter:v0.8.4"
                    }
                  }
                },
                "kruize": {
                  "workload_name": "kruize",
                  "workload_type": "deployment",
                  "containers": {
                    "kruize": {
                      "container_name": "kruize",
                      "container_image_name": "quay.io/kruize/autotune_operator:0.0.21_mvp"
                    }
                  }
                },
                "grafana": {
                  "workload_name": "grafana",
                  "workload_type": "deployment",
                  "containers": {
                    "grafana": {
                      "container_name": "grafana",
                      "container_image_name": "grafana/grafana:7.5.4"
                    }
                  }
                },
                "prometheus-k8s": {
                  "workload_name": "prometheus-k8s",
                  "workload_type": "statefulset",
                  "containers": {
                    "config-reloader": {
                      "container_name": "config-reloader",
                      "container_image_name": "quay.io/prometheus-operator/prometheus-config-reloader:v0.47.0"
                    },
                    "prometheus": {
                      "container_name": "prometheus",
                      "container_image_name": "quay.io/prometheus/prometheus:v2.26.0"
                    }
                  }
                },
                "blackbox-exporter": {
                  "workload_name": "blackbox-exporter",
                  "workload_type": "deployment",
                  "containers": {
                    "kube-rbac-proxy": {
                      "container_name": "kube-rbac-proxy",
                      "container_image_name": "quay.io/brancz/kube-rbac-proxy:v0.8.0"
                    },
                    "module-configmap-reloader": {
                      "container_name": "module-configmap-reloader",
                      "container_image_name": "jimmidyson/configmap-reload:v0.5.0"
                    },
                    "blackbox-exporter": {
                      "container_name": "blackbox-exporter",
                      "container_image_name": "quay.io/prometheus/blackbox-exporter:v0.18.0"
                    }
                  }
                },
                "prometheus-operator": {
                  "workload_name": "prometheus-operator",
                  "workload_type": "deployment",
                  "containers": {
                    "kube-rbac-proxy": {
                      "container_name": "kube-rbac-proxy",
                      "container_image_name": "quay.io/brancz/kube-rbac-proxy:v0.8.0"
                    },
                    "prometheus-operator": {
                      "container_name": "prometheus-operator",
                      "container_image_name": "quay.io/prometheus-operator/prometheus-operator:v0.47.0"
                    }
                  }
                }
              }
            },
            "kube-public": {
              "namespace": "kube-public"
            }
          }
        }
      }
    }
  }
}
```

</details>

<br>

**Request with datasource name and cluster name parameter**

`GET /dsmetadata`

`curl -H 'Accept: application/json' "http://<URL>:<PORT>/dsmetadata?datasource=<datasource_name>&cluster_name=<cluster_name>"`

Returns the list of namespaces present in the specified cluster name and datasource

**Response for datasource name - `prometheus-1` and cluster name - `default`**

With `verbose` parameter set to `false`, the response includes list of namespaces present in the specified cluster name 
and datasource.

<details>
<summary><b>Example Response</b></summary>

### Example Response

```json
{
  "datasources": {
    "prometheus-1": {
      "datasource_name": "prometheus-1",
      "clusters": {
        "default": {
          "cluster_name": "default",
          "namespaces": {
            "default": {
              "namespace": "default"
            },
            "cadvisor": {
              "namespace": "cadvisor"
            },
            "kube-node-lease": {
              "namespace": "kube-node-lease"
            },
            "kube-system": {
              "namespace": "kube-system"
            },
            "monitoring": {
              "namespace": "monitoring"
            },
            "kube-public": {
              "namespace": "kube-public"
            }
          }
        }
      }
    }
  }
}
```

</details>

<br>

**Request with datasource name, cluster name and verbose parameters**

`GET /dsmetadata`

`curl -H 'Accept: application/json' "http://<URL>:<PORT>/dsmetadata?datasource=<datasource_name>&cluster_name=<cluster_name>&verbose=true"`

Returns the container-level metadata of all the namespaces present in the specified cluster name and datasource

**Response for datasource name - `prometheus-1`, cluster name - `default` and verbose - `true`**

With `verbose` parameter set to `true`, the response includes detailed metadata about workloads and containers 
in addition to namespace information with the specified cluster name and datasource.

<details>
<summary><b>Example Response</b></summary>

### Example Response

```json
{
  "datasources": {
    "prometheus-1": {
      "datasource_name": "prometheus-1",
      "clusters": {
        "default": {
          "cluster_name": "default",
          "namespaces": {
            "default": {
              "namespace": "default"
            },
            "cadvisor": {
              "namespace": "cadvisor",
              "workloads": {
                "cadvisor": {
                  "workload_name": "cadvisor",
                  "workload_type": "daemonset",
                  "containers": {
                    "cadvisor": {
                      "container_name": "cadvisor",
                      "container_image_name": "gcr.io/cadvisor/cadvisor:v0.45.0"
                    }
                  }
                }
              }
            },
            "kube-node-lease": {
              "namespace": "kube-node-lease"
            },
            "kube-system": {
              "namespace": "kube-system",
              "workloads": {
                "coredns": {
                  "workload_name": "coredns",
                  "workload_type": "deployment",
                  "containers": {
                    "coredns": {
                      "container_name": "coredns",
                      "container_image_name": "k8s.gcr.io/coredns/coredns:v1.8.6"
                    }
                  }
                },
                "kube-proxy": {
                  "workload_name": "kube-proxy",
                  "workload_type": "daemonset",
                  "containers": {
                    "kube-proxy": {
                      "container_name": "kube-proxy",
                      "container_image_name": "k8s.gcr.io/kube-proxy:v1.24.3"
                    }
                  }
                }
              }
            },
            "monitoring": {
              "namespace": "monitoring",
              "workloads": {
                "kube-state-metrics": {
                  "workload_name": "kube-state-metrics",
                  "workload_type": "deployment",
                  "containers": {
                    "kube-state-metrics": {
                      "container_name": "kube-state-metrics",
                      "container_image_name": "k8s.gcr.io/kube-state-metrics/kube-state-metrics:v2.0.0"
                    },
                    "kube-rbac-proxy-self": {
                      "container_name": "kube-rbac-proxy-self",
                      "container_image_name": "quay.io/brancz/kube-rbac-proxy:v0.8.0"
                    },
                    "kube-rbac-proxy-main": {
                      "container_name": "kube-rbac-proxy-main",
                      "container_image_name": "quay.io/brancz/kube-rbac-proxy:v0.8.0"
                    }
                  }
                },
                "node-exporter": {
                  "workload_name": "node-exporter",
                  "workload_type": "daemonset",
                  "containers": {
                    "node-exporter": {
                      "container_name": "node-exporter",
                      "container_image_name": "quay.io/prometheus/node-exporter:v1.1.2"
                    },
                    "kube-rbac-proxy": {
                      "container_name": "kube-rbac-proxy",
                      "container_image_name": "quay.io/brancz/kube-rbac-proxy:v0.8.0"
                    }
                  }
                },
                "postgres-deployment": {
                  "workload_name": "postgres-deployment",
                  "workload_type": "deployment",
                  "containers": {
                    "postgres": {
                      "container_name": "postgres",
                      "container_image_name": "quay.io/kruizehub/postgres:15.2"
                    }
                  }
                },
                "alertmanager-main": {
                  "workload_name": "alertmanager-main",
                  "workload_type": "statefulset",
                  "containers": {
                    "config-reloader": {
                      "container_name": "config-reloader",
                      "container_image_name": "quay.io/prometheus-operator/prometheus-config-reloader:v0.47.0"
                    },
                    "alertmanager": {
                      "container_name": "alertmanager",
                      "container_image_name": "quay.io/prometheus/alertmanager:v0.21.0"
                    }
                  }
                },
                "prometheus-adapter": {
                  "workload_name": "prometheus-adapter",
                  "workload_type": "deployment",
                  "containers": {
                    "prometheus-adapter": {
                      "container_name": "prometheus-adapter",
                      "container_image_name": "directxman12/k8s-prometheus-adapter:v0.8.4"
                    }
                  }
                },
                "kruize": {
                  "workload_name": "kruize",
                  "workload_type": "deployment",
                  "containers": {
                    "kruize": {
                      "container_name": "kruize",
                      "container_image_name": "quay.io/kruize/autotune_operator:0.0.21_mvp"
                    }
                  }
                },
                "grafana": {
                  "workload_name": "grafana",
                  "workload_type": "deployment",
                  "containers": {
                    "grafana": {
                      "container_name": "grafana",
                      "container_image_name": "grafana/grafana:7.5.4"
                    }
                  }
                },
                "prometheus-k8s": {
                  "workload_name": "prometheus-k8s",
                  "workload_type": "statefulset",
                  "containers": {
                    "config-reloader": {
                      "container_name": "config-reloader",
                      "container_image_name": "quay.io/prometheus-operator/prometheus-config-reloader:v0.47.0"
                    },
                    "prometheus": {
                      "container_name": "prometheus",
                      "container_image_name": "quay.io/prometheus/prometheus:v2.26.0"
                    }
                  }
                },
                "blackbox-exporter": {
                  "workload_name": "blackbox-exporter",
                  "workload_type": "deployment",
                  "containers": {
                    "kube-rbac-proxy": {
                      "container_name": "kube-rbac-proxy",
                      "container_image_name": "quay.io/brancz/kube-rbac-proxy:v0.8.0"
                    },
                    "module-configmap-reloader": {
                      "container_name": "module-configmap-reloader",
                      "container_image_name": "jimmidyson/configmap-reload:v0.5.0"
                    },
                    "blackbox-exporter": {
                      "container_name": "blackbox-exporter",
                      "container_image_name": "quay.io/prometheus/blackbox-exporter:v0.18.0"
                    }
                  }
                },
                "prometheus-operator": {
                  "workload_name": "prometheus-operator",
                  "workload_type": "deployment",
                  "containers": {
                    "kube-rbac-proxy": {
                      "container_name": "kube-rbac-proxy",
                      "container_image_name": "quay.io/brancz/kube-rbac-proxy:v0.8.0"
                    },
                    "prometheus-operator": {
                      "container_name": "prometheus-operator",
                      "container_image_name": "quay.io/prometheus-operator/prometheus-operator:v0.47.0"
                    }
                  }
                }
              }
            },
            "kube-public": {
              "namespace": "kube-public"
            }
          }
        }
      }
    }
  }
}
```
</details>

<br>

**Request with datasource name, cluster name and namespace parameters**

`GET /dsmetadata`

`curl -H 'Accept: application/json' "http://<URL>:<PORT>/dsmetadata?datasource=<datasource_name>&cluster_name=<cluster_name>&namespace=<namespace>"`

Returns the container-level metadata of the specified namespace, cluster name and datasource

***Note : `verbose` in the query URL to fetch container-level metadata is set to `true` by default***

**Response for datasource name - `prometheus-1`, cluster name - `default` and namespace - `monitoring`**

The response includes granular metadata about workloads and associated containers within specified namespace, cluster 
and datasource.

<details>
<summary><b>Example Response</b></summary>

### Example Response

```json
{
  "datasources": {
    "prometheus-1": {
      "datasource_name": "prometheus-1",
      "clusters": {
        "default": {
          "cluster_name": "default",
          "namespaces": {
            "monitoring": {
              "namespace": "monitoring",
              "workloads": {
                "kube-state-metrics": {
                  "workload_name": "kube-state-metrics",
                  "workload_type": "deployment",
                  "containers": {
                    "kube-state-metrics": {
                      "container_name": "kube-state-metrics",
                      "container_image_name": "k8s.gcr.io/kube-state-metrics/kube-state-metrics:v2.0.0"
                    },
                    "kube-rbac-proxy-self": {
                      "container_name": "kube-rbac-proxy-self",
                      "container_image_name": "quay.io/brancz/kube-rbac-proxy:v0.8.0"
                    },
                    "kube-rbac-proxy-main": {
                      "container_name": "kube-rbac-proxy-main",
                      "container_image_name": "quay.io/brancz/kube-rbac-proxy:v0.8.0"
                    }
                  }
                },
                "node-exporter": {
                  "workload_name": "node-exporter",
                  "workload_type": "daemonset",
                  "containers": {
                    "node-exporter": {
                      "container_name": "node-exporter",
                      "container_image_name": "quay.io/prometheus/node-exporter:v1.1.2"
                    },
                    "kube-rbac-proxy": {
                      "container_name": "kube-rbac-proxy",
                      "container_image_name": "quay.io/brancz/kube-rbac-proxy:v0.8.0"
                    }
                  }
                },
                "postgres-deployment": {
                  "workload_name": "postgres-deployment",
                  "workload_type": "deployment",
                  "containers": {
                    "postgres": {
                      "container_name": "postgres",
                      "container_image_name": "quay.io/kruizehub/postgres:15.2"
                    }
                  }
                },
                "alertmanager-main": {
                  "workload_name": "alertmanager-main",
                  "workload_type": "statefulset",
                  "containers": {
                    "config-reloader": {
                      "container_name": "config-reloader",
                      "container_image_name": "quay.io/prometheus-operator/prometheus-config-reloader:v0.47.0"
                    },
                    "alertmanager": {
                      "container_name": "alertmanager",
                      "container_image_name": "quay.io/prometheus/alertmanager:v0.21.0"
                    }
                  }
                },
                "prometheus-adapter": {
                  "workload_name": "prometheus-adapter",
                  "workload_type": "deployment",
                  "containers": {
                    "prometheus-adapter": {
                      "container_name": "prometheus-adapter",
                      "container_image_name": "directxman12/k8s-prometheus-adapter:v0.8.4"
                    }
                  }
                },
                "kruize": {
                  "workload_name": "kruize",
                  "workload_type": "deployment",
                  "containers": {
                    "kruize": {
                      "container_name": "kruize",
                      "container_image_name": "quay.io/kruize/autotune_operator:0.0.21_mvp"
                    }
                  }
                },
                "grafana": {
                  "workload_name": "grafana",
                  "workload_type": "deployment",
                  "containers": {
                    "grafana": {
                      "container_name": "grafana",
                      "container_image_name": "grafana/grafana:7.5.4"
                    }
                  }
                },
                "prometheus-k8s": {
                  "workload_name": "prometheus-k8s",
                  "workload_type": "statefulset",
                  "containers": {
                    "config-reloader": {
                      "container_name": "config-reloader",
                      "container_image_name": "quay.io/prometheus-operator/prometheus-config-reloader:v0.47.0"
                    },
                    "prometheus": {
                      "container_name": "prometheus",
                      "container_image_name": "quay.io/prometheus/prometheus:v2.26.0"
                    }
                  }
                },
                "blackbox-exporter": {
                  "workload_name": "blackbox-exporter",
                  "workload_type": "deployment",
                  "containers": {
                    "kube-rbac-proxy": {
                      "container_name": "kube-rbac-proxy",
                      "container_image_name": "quay.io/brancz/kube-rbac-proxy:v0.8.0"
                    },
                    "module-configmap-reloader": {
                      "container_name": "module-configmap-reloader",
                      "container_image_name": "jimmidyson/configmap-reload:v0.5.0"
                    },
                    "blackbox-exporter": {
                      "container_name": "blackbox-exporter",
                      "container_image_name": "quay.io/prometheus/blackbox-exporter:v0.18.0"
                    }
                  }
                },
                "prometheus-operator": {
                  "workload_name": "prometheus-operator",
                  "workload_type": "deployment",
                  "containers": {
                    "kube-rbac-proxy": {
                      "container_name": "kube-rbac-proxy",
                      "container_image_name": "quay.io/brancz/kube-rbac-proxy:v0.8.0"
                    },
                    "prometheus-operator": {
                      "container_name": "prometheus-operator",
                      "container_image_name": "quay.io/prometheus-operator/prometheus-operator:v0.47.0"
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
  }
}
```