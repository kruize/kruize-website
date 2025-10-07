---
title: Generate Recommendations API
sidebar: mydoc_sidebar
permalink: lm_generate_recommendations.html
folder: mydoc
---

### Generate Recommendations API

**Note: This API is specific to the Local Monitoring use case.** <br>
Generates the recommendation for a specific experiment based on provided parameters similar to update recommendations API.
This can be called directly after creating the experiment and doesn't require the update results API as metrics are
fetched from the provided `datasource` (E.g. Prometheus) instead of the database.

**Request Parameters**

| Parameter           | Type   | Required | Description                                                                                                                                |
|---------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------|
| experiment_name     | string | Yes      | The name of the experiment.                                                                                                                |
| interval_end_time   | string | optional | The end time of the interval in the format `yyyy-MM-ddTHH:mm:sssZ`. This should be the date on which recommendation needs to be generated. |
| interval_start_time | string | optional | The start time of the interval in the format `yyyy-MM-ddTHH:mm:sssZ`.                                                                      |

The recommendation API requires only one mandatory field i.e. `experiment_name`. Other optional parameter like `interval_end_time` will be fetched from the provided datasource.
Similarly, `interval_start_time` will be calculated based on `interval_end_time`, if not provided. By utilizing
these parameters, the API generates recommendations based on short-term, medium-term, and long-term factors. For
instance, if the long-term setting is configured for `15 days` and the interval_end_time is set to `Jan 15 2023 00:00:
00.000Z`, the API retrieves data from the past 15 days, starting from January 1st. Using this data, the API generates
three recommendations for `Jan 15th 2023`.

It is important to ensure that the difference between `interval_end_time` and `interval_start_time` should not exceed 15
days. This restriction is in place to prevent potential timeouts, as generating recommendations beyond this threshold
might require more time.

**Request with experiment name and interval_end_time parameters**

`POST /generateRecommendations?experiment_name=?&interval_end_time=?`

`POST /generateRecommendations?experiment_name=?&interval_end_time=?&interval_start_time=?`

example

`curl --location --request POST 'http://<URL>:<PORT>/generateRecommendations?interval_end_time=2023-01-02T00:15:00.000Z&experiment_name=temp_1'`

success status code : 201

**Response**

The response will contain a array of JSON object with the recommendations for the specified experiment.

<details>
<summary><b>Example Response Body</b></summary>

```json
[
  {
    "cluster_name": "default",
    "experiment_type": "container",
    "kubernetes_objects": [
      {
        "type": "deployment",
        "name": "tfb-qrh-deployment_5",
        "namespace": "default_5",
        "containers": [
          {
            "container_image_name": "kruize/tfb-qrh:1.13.2.F_et17",
            "container_name": "tfb-server-1",
            "recommendations": {
              "version": "1.0",
              "notifications": {
                "111000": {
                  "type": "info",
                  "message": "Recommendations Are Available",
                  "code": 111000
                }
              },
              "data": {
                "2023-04-02T13:30:00.680Z": {
                  "notifications": {
                    "111101": {
                      "type": "info",
                      "message": "Short Term Recommendations Available",
                      "code": 111101
                    }
                  },
                  "monitoring_end_time": "2023-04-02T13:30:00.680Z",
                  "current": {
                    "limits": {
                      "memory": {
                        "amount": 1.048576E8,
                        "format": "bytes"
                      },
                      "cpu": {
                        "amount": 0.5,
                        "format": "cores"
                      }
                    },
                    "requests": {
                      "memory": {
                        "amount": 5.264900096E7,
                        "format": "bytes"
                      },
                      "cpu": {
                        "amount": 5.37,
                        "format": "cores"
                      }
                    }
                  },
                  "recommendation_terms": {
                    "short_term": {
                      "duration_in_hours": 24.0,
                      "notifications": {
                        "112101": {
                          "type": "info",
                          "message": "Cost Recommendations Available",
                          "code": 112101
                        },
                        "112102": {
                          "type": "info",
                          "message": "Performance Recommendations Available",
                          "code": 112102
                        }
                      },
                      "monitoring_start_time": "2023-04-01T12:00:00.000Z",
                      "recommendation_engines": {
                        "cost": {
                          "pods_count": 7,
                          "confidence_level": 0.0,
                          "config": {
                            "limits": {
                              "memory": {
                                "amount": 2.497708032E8,
                                "format": "bytes"
                              },
                              "cpu": {
                                "amount": 0.9299999999999999,
                                "format": "cores"
                              }
                            },
                            "requests": {
                              "memory": {
                                "amount": 2.497708032E8,
                                "format": "bytes"
                              },
                              "cpu": {
                                "amount": 0.9299999999999999,
                                "format": "cores"
                              }
                            }
                          },
                          "variation": {
                            "limits": {
                              "memory": {
                                "amount": 1.449132032E8,
                                "format": "bytes"
                              },
                              "cpu": {
                                "amount": -4.44,
                                "format": "cores"
                              }
                            },
                            "requests": {
                              "memory": {
                                "amount": 1.9712180223999997902848E8,
                                "format": "bytes"
                              },
                              "cpu": {
                                "amount": -4.44,
                                "format": "cores"
                              }
                            }
                          },
                          "notifications": {}
                        },
                        "performance": {
                          "pods_count": 27,
                          "confidence_level": 0.0,
                          "config": {
                            "limits": {
                              "memory": {
                                "amount": 2.497708032E8,
                                "format": "bytes"
                              },
                              "cpu": {
                                "amount": 0.9299999999999999,
                                "format": "cores"
                              }
                            },
                            "requests": {
                              "memory": {
                                "amount": 2.497708032E8,
                                "format": "bytes"
                              },
                              "cpu": {
                                "amount": 0.9299999999999999,
                                "format": "cores"
                              }
                            }
                          },
                          "variation": {
                            "limits": {
                              "memory": {
                                "amount": 1.449132032E8,
                                "format": "bytes"
                              },
                              "cpu": {
                                "amount": -4.44,
                                "format": "cores"
                              }
                            },
                            "requests": {
                              "memory": {
                                "amount": 1.9712180223999997902848E8,
                                "format": "bytes"
                              },
                              "cpu": {
                                "amount": -4.44,
                                "format": "cores"
                              }
                            }
                          },
                          "notifications": {}
                        }
                      }
                    },
                    "medium_term": {
                      "duration_in_hours": 33.8,
                      "notifications": {
                        "120001": {
                          "type": "info",
                          "message": "There is not enough data available to generate a recommendation.",
                          "code": 120001
                        }
                      }
                    },
                    "long_term": {
                      "duration_in_hours": 33.8,
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
          {
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
        ]
      }
    ],
    "version": "v2.0",
    "experiment_name": "temp_1"
  }
]
```

</details>

**Request without interval_end_time parameter**

`POST /generateRecommendations?experiment_name=?`

example

`curl --location --request POST 'http://<URL>:<PORT>/generateRecommendations?experiment_name=temp_1'`

success status code : 201

**Response**

The response will contain an array of JSON object with the recommendations for the specified experiment.

When `interval_end_time` is not specified, Kruize will determine the latest timestamp from the specified datasource
(E.g. Prometheus) by checking the latest active container CPU usage.

<details>
<summary><b>Example Response Body</b></summary>

```json
[
  {
    "cluster_name": "default",
    "experiment_type": "container",
    "kubernetes_objects": [
      {
        "type": "deployment",
        "name": "tfb-qrh-deployment_5",
        "namespace": "default_5",
        "containers": [
          {
            "container_image_name": "kruize/tfb-qrh:1.13.2.F_et17",
            "container_name": "tfb-server-1",
            "recommendations": {
              "version": "1.0",
              "notifications": {
                "111000": {
                  "type": "info",
                  "message": "Recommendations Are Available",
                  "code": 111000
                }
              },
              "data": {
                "2023-04-02T13:30:00.680Z": {
                  "notifications": {
                    "111101": {
                      "type": "info",
                      "message": "Short Term Recommendations Available",
                      "code": 111101
                    }
                  },
                  "monitoring_end_time": "2023-04-02T13:30:00.680Z",
                  "current": {
                    "limits": {
                      "memory": {
                        "amount": 1.048576E8,
                        "format": "bytes"
                      },
                      "cpu": {
                        "amount": 0.5,
                        "format": "cores"
                      }
                    },
                    "requests": {
                      "memory": {
                        "amount": 5.264900096E7,
                        "format": "bytes"
                      },
                      "cpu": {
                        "amount": 5.37,
                        "format": "cores"
                      }
                    }
                  },
                  "recommendation_terms": {
                    "short_term": {
                      "duration_in_hours": 24.0,
                      "notifications": {
                        "112101": {
                          "type": "info",
                          "message": "Cost Recommendations Available",
                          "code": 112101
                        },
                        "112102": {
                          "type": "info",
                          "message": "Performance Recommendations Available",
                          "code": 112102
                        }
                      },
                      "monitoring_start_time": "2023-04-01T12:00:00.000Z",
                      "recommendation_engines": {
                        "cost": {
                          "pods_count": 7,
                          "confidence_level": 0.0,
                          "config": {
                            "limits": {
                              "memory": {
                                "amount": 2.497708032E8,
                                "format": "bytes"
                              },
                              "cpu": {
                                "amount": 0.9299999999999999,
                                "format": "cores"
                              }
                            },
                            "requests": {
                              "memory": {
                                "amount": 2.497708032E8,
                                "format": "bytes"
                              },
                              "cpu": {
                                "amount": 0.9299999999999999,
                                "format": "cores"
                              }
                            }
                          },
                          "variation": {
                            "limits": {
                              "memory": {
                                "amount": 1.449132032E8,
                                "format": "bytes"
                              },
                              "cpu": {
                                "amount": -4.44,
                                "format": "cores"
                              }
                            },
                            "requests": {
                              "memory": {
                                "amount": 1.9712180223999997902848E8,
                                "format": "bytes"
                              },
                              "cpu": {
                                "amount": -4.44,
                                "format": "cores"
                              }
                            }
                          },
                          "notifications": {}
                        },
                        "performance": {
                          "pods_count": 27,
                          "confidence_level": 0.0,
                          "config": {
                            "limits": {
                              "memory": {
                                "amount": 2.497708032E8,
                                "format": "bytes"
                              },
                              "cpu": {
                                "amount": 0.9299999999999999,
                                "format": "cores"
                              }
                            },
                            "requests": {
                              "memory": {
                                "amount": 2.497708032E8,
                                "format": "bytes"
                              },
                              "cpu": {
                                "amount": 0.9299999999999999,
                                "format": "cores"
                              }
                            }
                          },
                          "variation": {
                            "limits": {
                              "memory": {
                                "amount": 1.449132032E8,
                                "format": "bytes"
                              },
                              "cpu": {
                                "amount": -4.44,
                                "format": "cores"
                              }
                            },
                            "requests": {
                              "memory": {
                                "amount": 1.9712180223999997902848E8,
                                "format": "bytes"
                              },
                              "cpu": {
                                "amount": -4.44,
                                "format": "cores"
                              }
                            }
                          },
                          "notifications": {}
                        }
                      }
                    },
                    "medium_term": {
                      "duration_in_hours": 33.8,
                      "notifications": {
                        "120001": {
                          "type": "info",
                          "message": "There is not enough data available to generate a recommendation.",
                          "code": 120001
                        }
                      }
                    },
                    "long_term": {
                      "duration_in_hours": 33.8,
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
          {
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
        ]
      }
    ],
    "version": "v2.0",
    "experiment_name": "temp_1"
  }
]
```

</details>

**Request for `namespace` experiment**

`POST /generateRecommendations?experiment_name=?`

example

`curl --location --request POST 'http://<URL>:<PORT>/generateRecommendations?experiment_name=temp_1'`

success status code : 201

**Response for `namespace` Experiment**

The response will contain an array of JSON object with the recommendations for the specified experiment.

When `interval_end_time` is not specified, Kruize will determine the latest timestamp from the specified datasource
(E.g. Prometheus) by checking the latest active container CPU usage.

<details>
<summary><b>Example Response Body</b></summary>

```json
[
  {
    "cluster_name": "test-multiple-import",
    "experiment_type": "namespace",
    "kubernetes_objects": [
      {
        "namespace": "default",
        "containers": [],
        "namespaces": {
          "namespace": "default",
          "recommendations": {
            "version": "1.0",
            "notifications": {
              "111000": {
                "type": "info",
                "message": "Recommendations Are Available",
                "code": 111000
              }
            },
            "data": {
              "2024-09-25T09:46:20.000Z": {
                "notifications": {
                  "111101": {
                    "type": "info",
                    "message": "Short Term Recommendations Available",
                    "code": 111101
                  }
                },
                "monitoring_end_time": "2024-09-25T09:46:20.000Z",
                "current": {},
                "recommendation_terms": {
                  "short_term": {
                    "duration_in_hours": 24.0,
                    "notifications": {
                      "112101": {
                        "type": "info",
                        "message": "Cost Recommendations Available",
                        "code": 112101
                      },
                      "112102": {
                        "type": "info",
                        "message": "Performance Recommendations Available",
                        "code": 112102
                      }
                    },
                    "monitoring_start_time": "2024-09-24T09:46:20.000Z",
                    "recommendation_engines": {
                      "cost": {
                        "pods_count": 2,
                        "confidence_level": 0.0,
                        "config": {
                          "limits": {
                            "memory": {
                              "amount": 1.442955264E9,
                              "format": "bytes"
                            },
                            "cpu": {
                              "amount": 5.834468490017892,
                              "format": "cores"
                            }
                          },
                          "requests": {
                            "memory": {
                              "amount": 1.442955264E9,
                              "format": "bytes"
                            },
                            "cpu": {
                              "amount": 5.834468490017892,
                              "format": "cores"
                            }
                          }
                        },
                        "variation": {
                          "limits": {
                            "memory": {
                              "amount": 1.442955264E9,
                              "format": "bytes"
                            },
                            "cpu": {
                              "amount": 5.834468490017892,
                              "format": "cores"
                            }
                          },
                          "requests": {
                            "memory": {
                              "amount": 1.442955264E9,
                              "format": "bytes"
                            },
                            "cpu": {
                              "amount": 5.834468490017892,
                              "format": "cores"
                            }
                          }
                        },
                        "notifications": {}
                      },
                      "performance": {
                        "pods_count": 2,
                        "confidence_level": 0.0,
                        "config": {
                          "limits": {
                            "memory": {
                              "amount": 1.442955264E9,
                              "format": "bytes"
                            },
                            "cpu": {
                              "amount": 5.834468490017892,
                              "format": "cores"
                            }
                          },
                          "requests": {
                            "memory": {
                              "amount": 1.442955264E9,
                              "format": "bytes"
                            },
                            "cpu": {
                              "amount": 5.834468490017892,
                              "format": "cores"
                            }
                          }
                        },
                        "variation": {
                          "limits": {
                            "memory": {
                              "amount": 1.442955264E9,
                              "format": "bytes"
                            },
                            "cpu": {
                              "amount": 5.834468490017892,
                              "format": "cores"
                            }
                          },
                          "requests": {
                            "memory": {
                              "amount": 1.442955264E9,
                              "format": "bytes"
                            },
                            "cpu": {
                              "amount": 5.834468490017892,
                              "format": "cores"
                            }
                          }
                        },
                        "notifications": {}
                      }
                    }
                  },
                  "medium_term": {
                    "duration_in_hours": 168.0,
                    "notifications": {
                      "120001": {
                        "type": "info",
                        "message": "There is not enough data available to generate a recommendation.",
                        "code": 120001
                      }
                    }
                  },
                  "long_term": {
                    "duration_in_hours": 360.0,
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
        }
      }
    ],
    "version": "v2.0",
    "experiment_name": "namespace-demo"
  }
]
```

</details>

**Error Responses**

| HTTP Status Code | Description                                                                                        |
|------------------|----------------------------------------------------------------------------------------------------|
| 400              | experiment_name is mandatory.                                                                      |
| 400              | Given timestamp - \" 2023-011-02T00:00:00.000Z \" is not a valid timestamp format.                 |
| 400              | Not Found: experiment_name does not exist: exp_1.                                                  |
| 400              | No metrics available from `2024-01-15T00:00:00.000Z` to `2023-12-31T00:00:00.000Z`.                |
| 400              | The gap between the interval_start_time and interval_end_time must be within a maximum of 15 days! |
| 400              | The Start time should precede the End time!                                                        |                                           |
| 500              | Internal Server Error                                                                              |
