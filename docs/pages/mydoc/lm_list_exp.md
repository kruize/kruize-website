---
title: List Experiments API
sidebar: mydoc_sidebar
permalink: lm_list_exp.html
folder: mydoc
---

## List Experiments API

### Request with experiment name parameter

`GET /listExperiments`

`curl -H 'Accept: application/json' http://<URL>:<PORT>/listExperiments?experiment_name=<experiment_name>`

Returns the experiment details of the specified experiment

### Request with recommendations set to true

`GET /listExperiments`

`curl -H 'Accept: application/json' http://<URL>:<PORT>/listExperiments?recommendations=true`

Returns the latest recommendations of all the experiments

### Response for experiment name - `default|default_0|deployment|tfb-qrh-deployment_0`

#### Example Response


```json
[
  {
    "version": "v2.0",
    "experiment_id": "f0007796e65c999d843bebd447c2fbaa6aaf9127c614da55e333cd6bdb628a74",
    "experiment_name": "default|default_0|deployment|tfb-qrh-deployment_0",
    "cluster_name": "default",
    "datasource": "prometheus-1",
    "experiment_type": "container",
    "mode": "monitor",
    "target_cluster": "local",
    "status": "IN_PROGRESS",
    "performance_profile": "resource-optimization-openshift",
    "trial_settings": {
      "measurement_duration": "15min"
    },
    "recommendation_settings": {
      "threshold": "0.1"
    },
    "experiment_usecase_type": {
      "remote_monitoring": false,
      "local_monitoring": true,
      "local_experiment": false
    },
    "validation_data": {
      "success": true,
      "message": "Registered successfully with Kruize! View registered experiments at /listExperiments",
      "errorCode": 201
    },
    "kubernetes_objects": [
      {
        "type": "deployment",
        "name": "tfb-qrh-deployment_0",
        "namespace": "default_0",
        "containers": {
          "tfb-server-1": {
            "container_image_name": "kruize/tfb-qrh:1.13.2.F_et17",
            "container_name": "tfb-server-1",
            "recommendations": {
              "version": "1.0",
              "notifications": {
                "112101": {
                  "type": "info",
                  "message": "Cost Recommendations Available",
                  "code": 112101
                }
              },
              "data": {
                "2023-04-02T08:00:00.680Z": {
                  "cost": {
                    "short_term": {
                      "monitoring_start_time": "2023-04-01T06:45:00.000Z",
                      "monitoring_end_time": "2023-04-02T08:00:00.680Z",
                      "duration_in_hours": 24.0,
                      "pods_count": 27,
                      "confidence_level": 0.0,
                      "current": {
                        "requests": {
                          "memory": {
                            "amount": 490.93,
                            "format": "MiB"
                          },
                          "cpu": {
                            "amount": 1.46,
                            "format": "cores"
                          }
                        },
                        "limits": {
                          "memory": {
                            "amount": 712.21,
                            "format": "MiB"
                          },
                          "cpu": {
                            "amount": 1.54,
                            "format": "cores"
                          }
                        }
                      },
                      "config": {
                        "requests": {
                          "memory": {
                            "amount": 1197.9840000000002,
                            "format": "MiB"
                          },
                          "cpu": {
                            "amount": 7.68,
                            "format": "cores"
                          }
                        },
                        "limits": {
                          "memory": {
                            "amount": 1197.9840000000002,
                            "format": "MiB"
                          },
                          "cpu": {
                            "amount": 7.68,
                            "format": "cores"
                          }
                        }
                      },
                      "variation": {
                        "requests": {
                          "memory": {
                            "amount": 707.0540000000001,
                            "format": "MiB"
                          },
                          "cpu": {
                            "amount": 6.22,
                            "format": "cores"
                          }
                        },
                        "limits": {
                          "memory": {
                            "amount": 485.7740000000001,
                            "format": "MiB"
                          },
                          "cpu": {
                            "amount": 6.14,
                            "format": "cores"
                          }
                        }
                      },
                      "notifications": {}
                    },
                    "medium_term": {
                      "pods_count": 0,
                      "confidence_level": 0.0,
                      "notifications": {
                        "120001": {
                          "type": "info",
                          "message": "There is not enough data available to generate a recommendation.",
                          "code": 120001
                        }
                      }
                    },
                    "long_term": {
                      "pods_count": 0,
                      "confidence_level": 0.0,
                      "notifications": {
                        "120001": {
                          "type": "info",
                          "message": "There is not enough data available to generate a recommendation.",
                          "code": 120001
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "tfb-server-0": {
            "container_image_name": "kruize/tfb-db:1.15",
            "container_name": "tfb-server-0",
            "recommendations": {
              "version": "1.0",
              "notifications": {
                "120001": {
                  "type": "info",
                  "message": "There is not enough data available to generate a recommendation.",
                  "code": 120001
                }
              },
              "data": {}
            }
          }
        }
      }
    ]
  },
  ...
  ...
  ...
  {
    "version": "v2.0",
    "experiment_id": "ab0a31a522cebdde52561482300d078ed1448fa7b75834fa216677d1d9d5cda6",
    "experiment_name": "default|default_1|deployment|tfb-qrh-deployment_1",
    "cluster_name": "default",
    "datasource": "prometheus-1",
    "experiment_type": "container",
    "mode": "monitor",
    "target_cluster": "local",
    "status": "IN_PROGRESS",
    "performance_profile": "resource-optimization-openshift",
    "trial_settings": {
      "measurement_duration": "15min"
    },
    "recommendation_settings": {
      "threshold": "0.1"
    },
    "experiment_usecase_type": {
      "remote_monitoring": false,
      "local_monitoring": true,
      "local_experiment": false
    },
    "validation_data": {
      "success": true,
      "message": "Registered successfully with Kruize! View registered experiments at /listExperiments",
      "errorCode": 201
    },
    "kubernetes_objects": [
      {
        "type": "deployment",
        "name": "tfb-qrh-deployment_1",
        "namespace": "default_1",
        "containers": {
          "tfb-server-1": {
            "container_image_name": "kruize/tfb-qrh:1.13.2.F_et17",
            "container_name": "tfb-server-1",
            "recommendations": {
              "version": "1.0",
              "notifications": {
                "120001": {
                  "type": "info",
                  "message": "There is not enough data available to generate a recommendation.",
                  "code": 120001
                }
              },
              "data": {}
            }
          },
          "tfb-server-0": {
            "container_image_name": "kruize/tfb-db:1.15",
            "container_name": "tfb-server-0",
            "recommendations": {
              "version": "1.0",
              "notifications": {
                "120001": {
                  "type": "info",
                  "message": "There is not enough data available to generate a recommendation.",
                  "code": 120001
                }
              },
              "data": {}
            }
          }
        }
      }
    ]
  },
]
```


### Request with recommendations set to true with experiment name parameter

`GET /listExperiments`

`curl -H 'Accept: application/json' http://<URL>:<PORT>/listExperiments?recommendations=true&experiment_name=<experiment_name>`

Returns the latest recommendations of the specified experiment with no results

### Request with recommendations set to true and latest set to false

`GET /listExperiments`

`curl -H 'Accept: application/json' http://<URL>:<PORT>/listExperiments?recommendations=true&latest=false`

Returns all the recommendations of all the experiments

### Response for experiment name - `default|default_0|deployment|tfb-qrh-deployment_0`


#### Example Response

```json
[
  {
    "version": "v2.0",
    "experiment_id": "f0007796e65c999d843bebd447c2fbaa6aaf9127c614da55e333cd6bdb628a74",
    "experiment_name": "default|default_0|deployment|tfb-qrh-deployment_0",
    "cluster_name": "default",
    "datasource": "prometheus-1",
    "mode": "monitor",
    "target_cluster": "local",
    "status": "IN_PROGRESS",
    "performance_profile": "resource-optimization-openshift",
    "trial_settings": {
      "measurement_duration": "15min"
    },
    "recommendation_settings": {
      "threshold": "0.1"
    },
    "experiment_usecase_type": {
      "remote_monitoring": false,
      "local_monitoring": true,
      "local_experiment": false
    },
    "validation_data": {
      "success": true,
      "message": "Registered successfully with Kruize! View registered experiments at /listExperiments",
      "errorCode": 201
    },
    "kubernetes_objects": [
      {
        "type": "deployment",
        "name": "tfb-qrh-deployment_0",
        "namespace": "default_0",
        "containers": {
          "tfb-server-1": {
            "container_image_name": "kruize/tfb-qrh:1.13.2.F_et17",
            "container_name": "tfb-server-1",
            "recommendations": {
              "version": "1.0",
              "notifications": {
                "112101": {
                  "type": "info",
                  "message": "Cost Recommendations Available",
                  "code": 112101
                }
              },
              "data": {
                "2023-04-02T06:00:00.770Z": {
                  "cost": {
                    "short_term": {
                      "monitoring_start_time": "2023-04-01T04:45:00.000Z",
                      "monitoring_end_time": "2023-04-02T06:00:00.770Z",
                      "duration_in_hours": 24,
                      "pods_count": 27,
                      "confidence_level": 0,
                      "current": {
                        "requests": {
                          "memory": {
                            "amount": 490.93,
                            "format": "MiB"
                          },
                          "cpu": {
                            "amount": 1.46,
                            "format": "cores"
                          }
                        },
                        "limits": {
                          "memory": {
                            "amount": 712.21,
                            "format": "MiB"
                          },
                          "cpu": {
                            "amount": 1.54,
                            "format": "cores"
                          }
                        }
                      },
                      "config": {
                        "requests": {
                          "memory": {
                            "amount": 1197.9840000000002,
                            "format": "MiB"
                          },
                          "cpu": {
                            "amount": 7.68,
                            "format": "cores"
                          }
                        },
                        "limits": {
                          "memory": {
                            "amount": 1197.9840000000002,
                            "format": "MiB"
                          },
                          "cpu": {
                            "amount": 7.68,
                            "format": "cores"
                          }
                        }
                      },
                      "variation": {
                        "requests": {
                          "memory": {
                            "amount": 707.0540000000001,
                            "format": "MiB"
                          },
                          "cpu": {
                            "amount": 6.22,
                            "format": "cores"
                          }
                        },
                        "limits": {
                          "memory": {
                            "amount": 485.7740000000001,
                            "format": "MiB"
                          },
                          "cpu": {
                            "amount": 6.14,
                            "format": "cores"
                          }
                        }
                      },
                      "notifications": {}
                    },
                    "medium_term": {
                      "pods_count": 0,
                      "confidence_level": 0,
                      "notifications": {
                        "120001": {
                          "type": "info",
                          "message": "There is not enough data available to generate a recommendation.",
                          "code": 120001
                        }
                      }
                    },
                    "long_term": {
                      "pods_count": 0,
                      "confidence_level": 0,
                      "notifications": {
                        "120001": {
                          "type": "info",
                          "message": "There is not enough data available to generate a recommendation.",
                          "code": 120001
                        }
                      }
                    }
                  }
                },
                ...
                ...
                ...
                "2023-04-02T04:30:00.000Z": {
                  "cost": {
                    "short_term": {
                      "monitoring_start_time": "2023-04-01T03:15:00.000Z",
                      "monitoring_end_time": "2023-04-02T04:30:00.000Z",
                      "duration_in_hours": 24,
                      "pods_count": 27,
                      "confidence_level": 0,
                      "current": {
                        "requests": {
                          "memory": {
                            "amount": 490.93,
                            "format": "MiB"
                          },
                          "cpu": {
                            "amount": 1.46,
                            "format": "cores"
                          }
                        },
                        "limits": {
                          "memory": {
                            "amount": 712.21,
                            "format": "MiB"
                          },
                          "cpu": {
                            "amount": 1.54,
                            "format": "cores"
                          }
                        }
                      },
                      "config": {
                        "requests": {
                          "memory": {
                            "amount": 1197.9840000000002,
                            "format": "MiB"
                          },
                          "cpu": {
                            "amount": 7.68,
                            "format": "cores"
                          }
                        },
                        "limits": {
                          "memory": {
                            "amount": 1197.9840000000002,
                            "format": "MiB"
                          },
                          "cpu": {
                            "amount": 7.68,
                            "format": "cores"
                          }
                        }
                      },
                      "variation": {
                        "requests": {
                          "memory": {
                            "amount": 707.0540000000001,
                            "format": "MiB"
                          },
                          "cpu": {
                            "amount": 6.22,
                            "format": "cores"
                          }
                        },
                        "limits": {
                          "memory": {
                            "amount": 485.7740000000001,
                            "format": "MiB"
                          },
                          "cpu": {
                            "amount": 6.14,
                            "format": "cores"
                          }
                        }
                      },
                      "notifications": {}
                    },
                    "medium_term": {
                      "pods_count": 0,
                      "confidence_level": 0,
                      "notifications": {
                        "120001": {
                          "type": "info",
                          "message": "There is not enough data available to generate a recommendation.",
                          "code": 120001
                        }
                      }
                    },
                    "long_term": {
                      "pods_count": 0,
                      "confidence_level": 0,
                      "notifications": {
                        "120001": {
                          "type": "info",
                          "message": "There is not enough data available to generate a recommendation.",
                          "code": 120001
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "tfb-server-0": {
            "container_image_name": "kruize/tfb-db:1.15",
            "container_name": "tfb-server-0",
            "recommendations": {
              "version": "1.0",
              "notifications": {
                "120001": {
                  "type": "info",
                  "message": "There is not enough data available to generate a recommendation.",
                  "code": 120001
                }
              },
              "data": {}
            }
          }
        }
      }
    ]
  },
  ...
  ...
  ...
]
```




### Request with recommendations set to true, latest set to false and with experiment name parameter

`GET /listExperiments`

`curl -H 'Accept: application/json' http://<URL>:<PORT>/listExperiments?recommendations=true&latest=false&experiment_name=<experiment_name>`

Returns all the recommendations of the specified experiment

### List Experiments also allows the user to send a request body to fetch the records based on `cluster_name` and `kubernetes_object`.
<

*Note: This request body can be sent along with other query params which are mentioned above.*

`curl -H 'Accept: application/json' -X GET --data 'copy paste below JSON' http://<URL>:<PORT>/listExperiments`



#### Example Request

```json
{
  "cluster_name": "default",
  "kubernetes_objects": [
    {
      "type": "deployment",
      "name": "tfb-qrh-deployment",
      "namespace": "default",
      "containers": [
        {
          "container_image_name": "kruize/tfb-db:1.15",
          "container_name": "tfb-server-1"
        }
      ]
    }
  ]
}
```


{% include links.html %}
