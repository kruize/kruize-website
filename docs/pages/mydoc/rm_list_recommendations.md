---
title: List Recommendations API
sidebar: mydoc_sidebar
permalink: rm_list_recommendations.html
folder: mydoc
---

### List Recommendations API

List recommendations output JSON as follows. Some parameters like CPU limit , ENV are optional.

**Attributes:**

| Param                 | Possible options     | Defaults | Description                                                                                                              | 
|-----------------------|----------------------|----------|--------------------------------------------------------------------------------------------------------------------------|
| `experiment_name`     | Any string           | None     | Passing Experiment Name as the parameter to the API returns the recommendation of the particular experiment if it exists |
| `latest`              | `true`, `false`      | `true`   | Gets you the latest available recommendation if true, else returns all the recommendations                               |
| `monitoring_end_time` | Any valid timestamp* | None     | Gets the recommendation of a particular timestamp if it exists                                                           |

`*valid timestamp is the same format as that used by the updateResults API`

**Request without Parameter**

`GET /listRecommendations`

`curl -H 'Accept: application/json' http://<URL>:<PORT>/listRecommendations`

If no parameter is passed API returns all the latest recommendations available for each experiment.

**Response**

<details>
<summary><b>Example Response with experiment_type as `container` </b></summary>

### Example Response

```json
[
  {
    "experiment_name": "experiment_1",
    "cluster_name": "cluster-one-division-bell",
    "kubernetes_objects": [
      {
        "type": "deployment",
        "name": "tfb-qrh-deployment_0",
        "namespace": "default_0",
        "containers": [
          {
            "container_image_name": "kruize/tfb-qrh:1.13.2.F_et17",
            "container_name": "tfb-server-1",
            "recommendations": {
              "version": "v2.0",
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
                    "requests": {
                      "memory": {
                        "amount": 50.21,
                        "format": "MiB"
                      },
                      "cpu": {
                        "amount": 5.37,
                        "format": "cores"
                      }
                    },
                    "limits": {
                      "memory": {
                        "amount": 100.0,
                        "format": "MiB"
                      },
                      "cpu": {
                        "amount": 0.5,
                        "format": "cores"
                      }
                    }
                  },
                  "recommendation_terms": {
                    "short_term": {
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
                      "duration_in_hours": 24.0,
                      "recommendation_engines": {
                        "cost": {
                          "pods_count": 27,
                          "confidence_level": 0.0,
                          "config": {
                            "requests": {
                              "memory": {
                                "amount": 238.2,
                                "format": "MiB"
                              },
                              "cpu": {
                                "amount": 0.9299999999999999,
                                "format": "cores"
                              }
                            },
                            "limits": {
                              "memory": {
                                "amount": 238.2,
                                "format": "MiB"
                              },
                              "cpu": {
                                "amount": 0.9299999999999999,
                                "format": "cores"
                              }
                            }
                          },
                          "variation": {
                            "requests": {
                              "memory": {
                                "amount": 187.98999999999998,
                                "format": "MiB"
                              },
                              "cpu": {
                                "amount": -4.44,
                                "format": "cores"
                              }
                            },
                            "limits": {
                              "memory": {
                                "amount": 138.2,
                                "format": "MiB"
                              },
                              "cpu": {
                                "amount": 0.42999999999999994,
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
                            "requests": {
                              "memory": {
                                "amount": 238.2,
                                "format": "MiB"
                              },
                              "cpu": {
                                "amount": 0.9299999999999999,
                                "format": "cores"
                              }
                            },
                            "limits": {
                              "memory": {
                                "amount": 238.2,
                                "format": "MiB"
                              },
                              "cpu": {
                                "amount": 0.9299999999999999,
                                "format": "cores"
                              }
                            }
                          },
                          "variation": {
                            "requests": {
                              "memory": {
                                "amount": 187.98999999999998,
                                "format": "MiB"
                              },
                              "cpu": {
                                "amount": -4.44,
                                "format": "cores"
                              }
                            },
                            "limits": {
                              "memory": {
                                "amount": 138.2,
                                "format": "MiB"
                              },
                              "cpu": {
                                "amount": 0.42999999999999994,
                                "format": "cores"
                              }
                            }
                          },
                          "notifications": {}
                        }
                      }
                    },
                    "medium_term": {
                      "duration_in_hours": 143.0,
                      "notifications": {
                        "120001": {
                          "type": "info",
                          "message": "There is not enough data available to generate a recommendation.",
                          "code": 120001
                        }
                      }
                    },
                    "long_term": {
                      "duration_in_hours": 240.0,
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
        ]
      }
    ]
  },
  {
    "experiment_name": "experiment_2",
    "cluster_name": "cluster-one-division-bell",
    "kubernetes_objects": [
      {
        "type": "deployment",
        "name": "tfb-qrh-deployment_2",
        "namespace": "default_2",
        "containers": [
          {
            "container_image_name": "kruize/tfb-qrh:1.13.2.F_et17",
            "container_name": "tfb-server-1",
            "recommendations": {
              "version": "v2.0",
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
                    "requests": {
                      "memory": {
                        "amount": 50.21,
                        "format": "MiB"
                      },
                      "cpu": {
                        "amount": 5.37,
                        "format": "cores"
                      }
                    },
                    "limits": {
                      "memory": {
                        "amount": 100.0,
                        "format": "MiB"
                      },
                      "cpu": {
                        "amount": 0.5,
                        "format": "cores"
                      }
                    }
                  },
                  "recommendation_terms": {
                    "short_term": {
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
                      "duration_in_hours": 24.0,
                      "recommendation_engines": {
                        "cost": {
                          "pods_count": 27,
                          "confidence_level": 0.0,
                          "config": {
                            "requests": {
                              "memory": {
                                "amount": 238.2,
                                "format": "MiB"
                              },
                              "cpu": {
                                "amount": 0.9299999999999999,
                                "format": "cores"
                              }
                            },
                            "limits": {
                              "memory": {
                                "amount": 238.2,
                                "format": "MiB"
                              },
                              "cpu": {
                                "amount": 0.9299999999999999,
                                "format": "cores"
                              }
                            }
                          },
                          "variation": {
                            "requests": {
                              "memory": {
                                "amount": 187.98999999999998,
                                "format": "MiB"
                              },
                              "cpu": {
                                "amount": -4.44,
                                "format": "cores"
                              }
                            },
                            "limits": {
                              "memory": {
                                "amount": 138.2,
                                "format": "MiB"
                              },
                              "cpu": {
                                "amount": 0.42999999999999994,
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
                            "requests": {
                              "memory": {
                                "amount": 238.2,
                                "format": "MiB"
                              },
                              "cpu": {
                                "amount": 0.9299999999999999,
                                "format": "cores"
                              }
                            },
                            "limits": {
                              "memory": {
                                "amount": 238.2,
                                "format": "MiB"
                              },
                              "cpu": {
                                "amount": 0.9299999999999999,
                                "format": "cores"
                              }
                            }
                          },
                          "variation": {
                            "requests": {
                              "memory": {
                                "amount": 187.98999999999998,
                                "format": "MiB"
                              },
                              "cpu": {
                                "amount": -4.44,
                                "format": "cores"
                              }
                            },
                            "limits": {
                              "memory": {
                                "amount": 138.2,
                                "format": "MiB"
                              },
                              "cpu": {
                                "amount": 0.42999999999999994,
                                "format": "cores"
                              }
                            }
                          },
                          "notifications": {}
                        }
                      }
                    },
                    "medium_term": {
                      "duration_in_hours": 143.0,
                      "notifications": {
                        "120001": {
                          "type": "info",
                          "message": "There is not enough data available to generate a recommendation.",
                          "code": 120001
                        }
                      }
                    },
                    "long_term": {
                      "duration_in_hours": 240.0,
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
        ]
      }
    ]
  }
]
```

</details>

<details>
<summary><b>Example Response with experiment_type as `namespace` </b></summary>

### Example Response

```json
[
  {
    "cluster_name": "cluster-one-division-bell",
    "experiment_type": "namespace",
    "kubernetes_objects": [
      {
        "namespace": "namespace-demo",
        "containers": [],
        "namespaces": {
          "namespace": "namespace-demo",
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
              "2022-01-24T19:55:43.602Z": {
                "notifications": {
                  "111101": {
                    "type": "info",
                    "message": "Short Term Recommendations Available",
                    "code": 111101
                  }
                },
                "monitoring_end_time": "2022-01-24T19:55:43.602Z",
                "current": {
                  "limits": {
                    "cpu": {
                      "amount": 4.5,
                      "format": "cores"
                    },
                    "memory": {
                      "amount": 600.0,
                      "format": "MiB"
                    }
                  },
                  "requests": {
                    "cpu": {
                      "amount": 6.0,
                      "format": "cores"
                    },
                    "memory": {
                      "amount": 400.0,
                      "format": "MiB"
                    }
                  }
                },
                "recommendation_terms": {
                  "short_term": {
                    "duration_in_hours": 0.5,
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
                    "monitoring_start_time": "2022-01-23T19:55:43.602Z",
                    "recommendation_engines": {
                      "cost": {
                        "pods_count": 0,
                        "confidence_level": 0.0,
                        "config": {
                          "limits": {
                            "cpu": {
                              "amount": 0.9299999999999999,
                              "format": "cores"
                            },
                            "memory": {
                              "amount": 216.0,
                              "format": "MiB"
                            }
                          },
                          "requests": {
                            "cpu": {
                              "amount": 0.9299999999999999,
                              "format": "cores"
                            },
                            "memory": {
                              "amount": 216.0,
                              "format": "MiB"
                            }
                          }
                        },
                        "variation": {
                          "limits": {
                            "cpu": {
                              "amount": -3.5700000000000003,
                              "format": "cores"
                            },
                            "memory": {
                              "amount": -384.0,
                              "format": "MiB"
                            }
                          },
                          "requests": {
                            "cpu": {
                              "amount": -5.07,
                              "format": "cores"
                            },
                            "memory": {
                              "amount": -184.0,
                              "format": "MiB"
                            }
                          }
                        },
                        "notifications": {
                          "221001": {
                            "type": "error",
                            "message": "Number of pods cannot be zero",
                            "code": 221001
                          }
                        }
                      },
                      "performance": {
                        "pods_count": 0,
                        "confidence_level": 0.0,
                        "config": {
                          "limits": {
                            "cpu": {
                              "amount": 0.9299999999999999,
                              "format": "cores"
                            },
                            "memory": {
                              "amount": 216.0,
                              "format": "MiB"
                            }
                          },
                          "requests": {
                            "cpu": {
                              "amount": 0.9299999999999999,
                              "format": "cores"
                            },
                            "memory": {
                              "amount": 216.0,
                              "format": "MiB"
                            }
                          }
                        },
                        "variation": {
                          "limits": {
                            "cpu": {
                              "amount": -3.5700000000000003,
                              "format": "cores"
                            },
                            "memory": {
                              "amount": -384.0,
                              "format": "MiB"
                            }
                          },
                          "requests": {
                            "cpu": {
                              "amount": -5.07,
                              "format": "cores"
                            },
                            "memory": {
                              "amount": -184.0,
                              "format": "MiB"
                            }
                          }
                        },
                        "notifications": {
                          "221001": {
                            "type": "error",
                            "message": "Number of pods cannot be zero",
                            "code": 221001
                          }
                        }
                      }
                    }
                  },
                  "medium_term": {
                    "duration_in_hours": 0.5,
                    "notifications": {
                      "120001": {
                        "type": "info",
                        "message": "There is not enough data available to generate a recommendation.",
                        "code": 120001
                      }
                    }
                  },
                  "long_term": {
                    "duration_in_hours": 0.5,
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
    "experiment_name": "namespace-experiment-1"
  },
  {
    "cluster_name": "cluster-one-division-bell",
    "experiment_type": "namespace",
    "kubernetes_objects": [
      {
        "namespace": "namespace-demo",
        "containers": [],
        "namespaces": {
          "namespace": "namespace-demo",
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
              "2022-01-24T19:55:43.602Z": {
                "notifications": {
                  "111101": {
                    "type": "info",
                    "message": "Short Term Recommendations Available",
                    "code": 111101
                  }
                },
                "monitoring_end_time": "2022-01-24T19:55:43.602Z",
                "current": {
                  "limits": {
                    "cpu": {
                      "amount": 4.5,
                      "format": "cores"
                    },
                    "memory": {
                      "amount": 600.0,
                      "format": "MiB"
                    }
                  },
                  "requests": {
                    "cpu": {
                      "amount": 6.0,
                      "format": "cores"
                    },
                    "memory": {
                      "amount": 400.0,
                      "format": "MiB"
                    }
                  }
                },
                "recommendation_terms": {
                  "short_term": {
                    "duration_in_hours": 0.5,
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
                    "monitoring_start_time": "2022-01-23T19:55:43.602Z",
                    "recommendation_engines": {
                      "cost": {
                        "pods_count": 0,
                        "confidence_level": 0.0,
                        "config": {
                          "limits": {
                            "cpu": {
                              "amount": 0.9299999999999999,
                              "format": "cores"
                            },
                            "memory": {
                              "amount": 216.0,
                              "format": "MiB"
                            }
                          },
                          "requests": {
                            "cpu": {
                              "amount": 0.9299999999999999,
                              "format": "cores"
                            },
                            "memory": {
                              "amount": 216.0,
                              "format": "MiB"
                            }
                          }
                        },
                        "variation": {
                          "limits": {
                            "cpu": {
                              "amount": -3.5700000000000003,
                              "format": "cores"
                            },
                            "memory": {
                              "amount": -384.0,
                              "format": "MiB"
                            }
                          },
                          "requests": {
                            "cpu": {
                              "amount": -5.07,
                              "format": "cores"
                            },
                            "memory": {
                              "amount": -184.0,
                              "format": "MiB"
                            }
                          }
                        },
                        "notifications": {
                          "221001": {
                            "type": "error",
                            "message": "Number of pods cannot be zero",
                            "code": 221001
                          }
                        }
                      },
                      "performance": {
                        "pods_count": 0,
                        "confidence_level": 0.0,
                        "config": {
                          "limits": {
                            "cpu": {
                              "amount": 0.9299999999999999,
                              "format": "cores"
                            },
                            "memory": {
                              "amount": 216.0,
                              "format": "MiB"
                            }
                          },
                          "requests": {
                            "cpu": {
                              "amount": 0.9299999999999999,
                              "format": "cores"
                            },
                            "memory": {
                              "amount": 216.0,
                              "format": "MiB"
                            }
                          }
                        },
                        "variation": {
                          "limits": {
                            "cpu": {
                              "amount": -3.5700000000000003,
                              "format": "cores"
                            },
                            "memory": {
                              "amount": -384.0,
                              "format": "MiB"
                            }
                          },
                          "requests": {
                            "cpu": {
                              "amount": -5.07,
                              "format": "cores"
                            },
                            "memory": {
                              "amount": -184.0,
                              "format": "MiB"
                            }
                          }
                        },
                        "notifications": {
                          "221001": {
                            "type": "error",
                            "message": "Number of pods cannot be zero",
                            "code": 221001
                          }
                        }
                      }
                    }
                  },
                  "medium_term": {
                    "duration_in_hours": 0.5,
                    "notifications": {
                      "120001": {
                        "type": "info",
                        "message": "There is not enough data available to generate a recommendation.",
                        "code": 120001
                      }
                    }
                  },
                  "long_term": {
                    "duration_in_hours": 0.5,
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
    "experiment_name": "namespace-experiment-2"
  }
]
```

</details>


**Request with experiment name parameter**

`GET /listRecommendations`

`curl -H 'Accept: application/json' http://<URL>:<PORT>/listRecommendations?experiment_name=<experiment_name>`

Returns the latest result of that experiment

**Response for experiment name - `quarkus-resteasy-kruize-min-http-response-time-db_0`**

<details>
<summary><b>Example Response</b></summary>

### Example Response

```json
[
  {
    "cluster_name": "cluster-one-division-bell",
    "kubernetes_objects": [
      {
        "type": "deployment",
        "name": "tfb-qrh-deployment_0",
        "namespace": "default_0",
        "containers": [
          {
            "container_image_name": "kruize/tfb-qrh:1.13.2.F_et17",
            "container_name": "tfb-server-1",
            "recommendations": {
              "version": "v2.0",
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
                    "requests": {
                      "cpu": {
                        "amount": 5.37,
                        "format": "cores"
                      },
                      "memory": {
                        "amount": 50.21,
                        "format": "MiB"
                      }
                    },
                    "limits": {
                      "cpu": {
                        "amount": 0.5,
                        "format": "cores"
                      },
                      "memory": {
                        "amount": 100.0,
                        "format": "MiB"
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
                          "pods_count": 27,
                          "confidence_level": 0.0,
                          "config": {
                            "requests": {
                              "cpu": {
                                "amount": 0.9299999999999999,
                                "format": "cores"
                              },
                              "memory": {
                                "amount": 238.2,
                                "format": "MiB"
                              }
                            },
                            "limits": {
                              "cpu": {
                                "amount": 0.9299999999999999,
                                "format": "cores"
                              },
                              "memory": {
                                "amount": 238.2,
                                "format": "MiB"
                              }
                            }
                          },
                          "variation": {
                            "requests": {
                              "cpu": {
                                "amount": -4.44,
                                "format": "cores"
                              },
                              "memory": {
                                "amount": 187.98999999999998,
                                "format": "MiB"
                              }
                            },
                            "limits": {
                              "cpu": {
                                "amount": -4.44,
                                "format": "cores"
                              },
                              "memory": {
                                "amount": 138.2,
                                "format": "MiB"
                              }
                            }
                          },
                          "notifications": {}
                        },
                        "performance": {
                          "pods_count": 27,
                          "confidence_level": 0.0,
                          "config": {
                            "requests": {
                              "cpu": {
                                "amount": 2.45,
                                "format": "cores"
                              },
                              "memory": {
                                "amount": 238.2,
                                "format": "MiB"
                              }
                            },
                            "limits": {
                              "cpu": {
                                "amount": 2.45,
                                "format": "cores"
                              },
                              "memory": {
                                "amount": 238.2,
                                "format": "MiB"
                              }
                            }
                          },
                          "variation": {
                            "requests": {
                              "cpu": {
                                "amount": -2.92,
                                "format": "cores"
                              },
                              "memory": {
                                "amount": 187.98999999999998,
                                "format": "MiB"
                              }
                            },
                            "limits": {
                              "cpu": {
                                "amount": -2.92,
                                "format": "cores"
                              },
                              "memory": {
                                "amount": 138.2,
                                "format": "MiB"
                              }
                            }
                          }
                        },
                        "notifications": {}
                      }
                    },
                    "medium_term": {
                      "duration_in_hours": 0.0,
                      "notifications": {
                        "120001": {
                          "type": "info",
                          "message": "There is not enough data available to generate a recommendation.",
                          "code": 120001
                        }
                      }
                    },
                    "long_term": {
                      "duration_in_hours": 0.0,
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
              "version": "v2.0",
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
    "experiment_name": "quarkus-resteasy-kruize-min-http-response-time-db_0"
  }
]
```

</details>


**Request with experiment name parameter and latest set to false**

`GET /listRecommendations`

`curl -H 'Accept: application/json' http://<URL>:<PORT>/listRecommendations?experiment_name=<experiment_name>&latest=false`

Returns all the results of that experiment

**Response for experiment name - `quarkus-resteasy-kruize-min-http-response-time-db_0`**

<details>
<summary><b>Example Response</b></summary>

### Example Response

```json
[
  {
    "cluster_name": "cluster-one-division-bell",
    "kubernetes_objects": [
      {
        "type": "deployment",
        "name": "tfb-qrh-deployment_0",
        "namespace": "default_0",
        "containers": [
          {
            "container_image_name": "kruize/tfb-qrh:1.13.2.F_et17",
            "container_name": "tfb-server-1",
            "recommendations": {
              "version": "v2.0",
              "notifications": {
                "111000": {
                  "type": "info",
                  "message": "Recommendations Are Available",
                  "code": 111000
                }
              },
              "data": {
                "2022-12-20T17:55:05.000Z": {
                  "notifications": {
                    "111101": {
                      "type": "info",
                      "message": "Short Term Recommendations Available",
                      "code": 111101
                    }
                  },
                  "monitoring_end_time": "2022-12-20T17:55:05.000Z",
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
                  "recommendation_terms": {
                    "short_term": {
                      "monitoring_start_time": "2022-12-19T17:55:05.000Z",
                      "duration_in_hours": 2.25,
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
                      "recommendation_engines": {
                        "cost": {
                          "pods_count": 0,
                          "confidence_level": 0.0,
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
                        }
                      }
                    },
                    "medium_term": {
                      "duration_in_hours": 140.0,
                      "notifications": {
                        "120001": {
                          "type": "info",
                          "message": "There is not enough data available to generate a recommendation.",
                          "code": 120001
                        }
                      }
                    },
                    "long_term": {
                      "duration_in_hours": 240.0,
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
                "2022-12-21T00:10:16.000Z": {
                  "notifications": {
                    "111101": {
                      "type": "info",
                      "message": "Short Term Recommendations Available",
                      "code": 111101
                    }
                  },
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
                  "monitoring_end_time": "2022-12-21T00:10:16.000Z",
                  "recommendation_terms": {
                    "short_term": {
                      "monitoring_start_time": "2022-12-20T00:10:16.000Z",
                      "duration_in_hours": 8.5,
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
                      "recommendation_engines": {
                        "cost": {
                          "pods_count": 0,
                          "confidence_level": 0.0,
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
                        "performance": {
                          "pods_count": 0,
                          "confidence_level": 0.0,
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
                        }
                      }
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
          {
            "container_image_name": "kruize/tfb-db:1.15",
            "container_name": "tfb-server-0",
            "recommendations": {
              "version": "v2.0",
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
    "experiment_name": "quarkus-resteasy-kruize-min-http-response-time-db_0"
  }
]
```

</details>


**Request with experiment name parameter and monitoring end time set to a valid timestamp**

`GET /listRecommendations`

`curl -H 'Accept: application/json' http://<URL>:<PORT>/listRecommendations?experiment_name=<experiment_name>&monitoring_end_time=2022-12-20T17:55:05.000Z`

Returns the recommendation at a particular timestamp if it exists

**Response for experiment name - `quarkus-resteasy-kruize-min-http-response-time-db_0` and Monitoring End Time

- `2022-12-20T17:55:05.000Z`**

<details>
<summary><b>Example Response</b></summary>

### Example Response

```json
[
  {
    "cluster_name": "cluster-one-division-bell",
    "kubernetes_objects": [
      {
        "type": "deployment",
        "name": "tfb-qrh-deployment_0",
        "namespace": "default_0",
        "containers": [
          {
            "container_image_name": "kruize/tfb-qrh:1.13.2.F_et17",
            "container_name": "tfb-server-1",
            "recommendations": {
              "version": "v2.0",
              "notifications": {
                "111000": {
                  "type": "info",
                  "message": "Recommendations Are Available",
                  "code": 111000
                }
              },
              "data": {
                "2022-12-20T17:55:05.000Z": {
                  "notifications": {
                    "111101": {
                      "type": "info",
                      "message": "Short Term Recommendations Available",
                      "code": 111101
                    }
                  },
                  "monitoring_end_time": "2022-12-20T17:55:05.000Z",
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
                  "recommendation_terms": {
                    "short_term": {
                      "duration_in_hours": 2.25,
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
                      "monitoring_start_time": "2022-12-19T17:55:05.000Z",
                      "recommendation_engines": {
                        "cost": {
                          "pods_count": 0,
                          "confidence_level": 0.0,
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
                        "performance": {
                          "pods_count": 0,
                          "confidence_level": 0.0,
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
                        }
                      }
                    },
                    "medium_term": {
                      "duration_in_hours": 0.0,
                      "notifications": {
                        "120001": {
                          "type": "info",
                          "message": "There is not enough data available to generate a recommendation.",
                          "code": 120001
                        }
                      }
                    },
                    "long_term": {
                      "duration_in_hours": 0.0,
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
        ]
      }
    ],
    "version": "v2.0",
    "experiment_name": "quarkus-resteasy-kruize-min-http-response-time-db_0"
  }
]
```

</details>


**Response for GPU workloads**

`GET /listRecommendations`

`curl -H 'Accept: application/json' http://<URL>:<PORT>/listRecommendations?experiment_name=job-01`

<details>
<summary><b>Example Response with GPU Recommendations</b></summary>

```json
[
    {
        "cluster_name": "default",
        "experiment_type": "container",
        "kubernetes_objects": [
            {
                "type": "statefulset",
                "name": "human-eval-benchmark",
                "namespace": "unpartitioned",
                "containers": [
                    {
                        "container_name": "human-eval-benchmark",
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
                                "2024-10-04T09:16:40.000Z": {
                                    "notifications": {
                                        "111101": {
                                            "type": "info",
                                            "message": "Short Term Recommendations Available",
                                            "code": 111101
                                        },
                                        "111102": {
                                            "type": "info",
                                            "message": "Medium Term Recommendations Available",
                                            "code": 111102
                                        }
                                    },
                                    "monitoring_end_time": "2024-10-04T09:16:40.000Z",
                                    "current": {
                                        "limits": {
                                            "cpu": {
                                                "amount": 2.0,
                                                "format": "cores"
                                            },
                                            "memory": {
                                                "amount": 8.589934592E9,
                                                "format": "bytes"
                                            }
                                        },
                                        "requests": {
                                            "cpu": {
                                                "amount": 1.0,
                                                "format": "cores"
                                            },
                                            "memory": {
                                                "amount": 8.589934592E9,
                                                "format": "bytes"
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
                                            "monitoring_start_time": "2024-10-03T09:16:40.000Z",
                                            "recommendation_engines": {
                                                "cost": {
                                                    "pods_count": 1,
                                                    "confidence_level": 0.0,
                                                    "config": {
                                                        "limits": {
                                                            "cpu": {
                                                                "amount": 1.004649523106615,
                                                                "format": "cores"
                                                            },
                                                            "nvidia.com/mig-3g.20gb": {
                                                                "amount": 1.0,
                                                                "format": "cores"
                                                            },
                                                            "memory": {
                                                                "amount": 4.9960943616E9,
                                                                "format": "bytes"
                                                            }
                                                        },
                                                        "requests": {
                                                            "cpu": {
                                                                "amount": 1.004649523106615,
                                                                "format": "cores"
                                                            },
                                                            "memory": {
                                                                "amount": 4.9960943616E9,
                                                                "format": "bytes"
                                                            }
                                                        }
                                                    },
                                                    "variation": {
                                                        "limits": {
                                                            "cpu": {
                                                                "amount": -0.995350476893385,
                                                                "format": "cores"
                                                            },
                                                            "memory": {
                                                                "amount": -3.5938402303999996E9,
                                                                "format": "bytes"
                                                            }
                                                        },
                                                        "requests": {
                                                            "cpu": {
                                                                "amount": 0.004649523106615039,
                                                                "format": "cores"
                                                            },
                                                            "memory": {
                                                                "amount": -3.5938402303999996E9,
                                                                "format": "bytes"
                                                            }
                                                        }
                                                    },
                                                    "notifications": {}
                                                },
                                                "performance": {
                                                    "pods_count": 1,
                                                    "confidence_level": 0.0,
                                                    "config": {
                                                        "limits": {
                                                            "cpu": {
                                                                "amount": 1.36656145696268,
                                                                "format": "cores"
                                                            },
                                                            "memory": {
                                                                "amount": 4.9960943616E9,
                                                                "format": "bytes"
                                                            },
                                                            "nvidia.com/mig-4g.20gb": {
                                                                "amount": 1.0,
                                                                "format": "cores"
                                                            }
                                                        },
                                                        "requests": {
                                                            "cpu": {
                                                                "amount": 1.36656145696268,
                                                                "format": "cores"
                                                            },
                                                            "memory": {
                                                                "amount": 4.9960943616E9,
                                                                "format": "bytes"
                                                            }
                                                        }
                                                    },
                                                    "variation": {
                                                        "limits": {
                                                            "cpu": {
                                                                "amount": -0.63343854303732,
                                                                "format": "cores"
                                                            },
                                                            "memory": {
                                                                "amount": -3.5938402303999996E9,
                                                                "format": "bytes"
                                                            }
                                                        },
                                                        "requests": {
                                                            "cpu": {
                                                                "amount": 0.36656145696268005,
                                                                "format": "cores"
                                                            },
                                                            "memory": {
                                                                "amount": -3.5938402303999996E9,
                                                                "format": "bytes"
                                                            }
                                                        }
                                                    },
                                                    "notifications": {}
                                                }
                                            },
                                            "plots": {
                                                "datapoints": 4,
                                                "plots_data": {
                                                    "2024-10-04T09:16:40.000Z": {
                                                        "cpuUsage": {
                                                            "min": 0.005422723351267242,
                                                            "q1": 1.003281151419465,
                                                            "median": 1.0118160468783521,
                                                            "q3": 1.012961901380266,
                                                            "max": 1.36656145696268,
                                                            "format": "cores"
                                                        },
                                                        "memoryUsage": {
                                                            "min": 3.68019456E9,
                                                            "q1": 3.681001472E9,
                                                            "median": 4.058411008E9,
                                                            "q3": 4.093308928E9,
                                                            "max": 4.094062592E9,
                                                            "format": "bytes"
                                                        }
                                                    },
                                                    "2024-10-04T03:16:40.000Z": {
                                                        "cpuUsage": {
                                                            "min": 0.998888009348188,
                                                            "q1": 1.0029943714818779,
                                                            "median": 1.0033621837551019,
                                                            "q3": 1.0040859908301978,
                                                            "max": 1.0828338199135354,
                                                            "format": "cores"
                                                        },
                                                        "memoryUsage": {
                                                            "min": 3.679281152E9,
                                                            "q1": 3.680755712E9,
                                                            "median": 3.680989184E9,
                                                            "q3": 3.687673856E9,
                                                            "max": 4.163411968E9,
                                                            "format": "bytes"
                                                        }
                                                    },
                                                    "2024-10-03T15:16:40.000Z": {
                                                        "cpuUsage": {
                                                            "min": 0.005425605536480822,
                                                            "q1": 0.006038658069363403,
                                                            "median": 0.006183237135144752,
                                                            "q3": 0.006269460195927269,
                                                            "max": 0.006916437328481231,
                                                            "format": "cores"
                                                        },
                                                        "memoryUsage": {
                                                            "min": 2.192125952E9,
                                                            "q1": 2.192388096E9,
                                                            "median": 2.192388096E9,
                                                            "q3": 2.192388096E9,
                                                            "max": 2.19265024E9,
                                                            "format": "bytes"
                                                        }
                                                    },
                                                    "2024-10-03T21:16:40.000Z": {
                                                        "cpuUsage": {
                                                            "min": 0.0052184839046300075,
                                                            "q1": 0.006229799261227028,
                                                            "median": 1.0110868114913476,
                                                            "q3": 1.0124661560983785,
                                                            "max": 2.3978065580305032,
                                                            "format": "cores"
                                                        },
                                                        "memoryUsage": {
                                                            "min": 2.118012928E9,
                                                            "q1": 2.192392192E9,
                                                            "median": 4.161662976E9,
                                                            "q3": 4.162850816E9,
                                                            "max": 4.163170304E9,
                                                            "format": "bytes"
                                                        }
                                                    }
                                                }
                                            }
                                        },
                                        "medium_term": {
                                            "duration_in_hours": 168.0,
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
                                            "monitoring_start_time": "2024-09-27T09:16:40.000Z",
                                            "recommendation_engines": {
                                                "cost": {
                                                    "pods_count": 1,
                                                    "confidence_level": 0.0,
                                                    "config": {
                                                        "limits": {
                                                            "cpu": {
                                                                "amount": 0.015580688959425347,
                                                                "format": "cores"
                                                            },
                                                            "nvidia.com/mig-3g.20gb": {
                                                                "amount": 1.0,
                                                                "format": "cores"
                                                            },
                                                            "memory": {
                                                                "amount": 4.9960943616E9,
                                                                "format": "bytes"
                                                            }
                                                        },
                                                        "requests": {
                                                            "cpu": {
                                                                "amount": 0.015580688959425347,
                                                                "format": "cores"
                                                            },
                                                            "memory": {
                                                                "amount": 4.9960943616E9,
                                                                "format": "bytes"
                                                            }
                                                        }
                                                    },
                                                    "variation": {
                                                        "limits": {
                                                            "cpu": {
                                                                "amount": -1.9844193110405746,
                                                                "format": "cores"
                                                            },
                                                            "memory": {
                                                                "amount": -3.5938402303999996E9,
                                                                "format": "bytes"
                                                            }
                                                        },
                                                        "requests": {
                                                            "cpu": {
                                                                "amount": -0.9844193110405747,
                                                                "format": "cores"
                                                            },
                                                            "memory": {
                                                                "amount": -3.5938402303999996E9,
                                                                "format": "bytes"
                                                            }
                                                        }
                                                    },
                                                    "notifications": {}
                                                },
                                                "performance": {
                                                    "pods_count": 1,
                                                    "confidence_level": 0.0,
                                                    "config": {
                                                        "limits": {
                                                            "cpu": {
                                                                "amount": 1.025365696933566,
                                                                "format": "cores"
                                                            },
                                                            "memory": {
                                                                "amount": 4.9960943616E9,
                                                                "format": "bytes"
                                                            },
                                                            "nvidia.com/mig-4g.20gb": {
                                                                "amount": 1.0,
                                                                "format": "cores"
                                                            }
                                                        },
                                                        "requests": {
                                                            "cpu": {
                                                                "amount": 1.025365696933566,
                                                                "format": "cores"
                                                            },
                                                            "memory": {
                                                                "amount": 4.9960943616E9,
                                                                "format": "bytes"
                                                            }
                                                        }
                                                    },
                                                    "variation": {
                                                        "limits": {
                                                            "cpu": {
                                                                "amount": -0.974634303066434,
                                                                "format": "cores"
                                                            },
                                                            "memory": {
                                                                "amount": -3.5938402303999996E9,
                                                                "format": "bytes"
                                                            }
                                                        },
                                                        "requests": {
                                                            "cpu": {
                                                                "amount": 0.02536569693356605,
                                                                "format": "cores"
                                                            },
                                                            "memory": {
                                                                "amount": -3.5938402303999996E9,
                                                                "format": "bytes"
                                                            }
                                                        }
                                                    },
                                                    "notifications": {}
                                                }
                                            },
                                            "plots": {
                                                "datapoints": 7,
                                                "plots_data": {
                                                    "2024-09-29T09:16:40.000Z": {},
                                                    "2024-10-04T09:16:40.000Z": {
                                                        "cpuUsage": {
                                                            "min": 0.0052184839046300075,
                                                            "q1": 0.006207971650471658,
                                                            "median": 1.0032201196711934,
                                                            "q3": 1.0115567178617741,
                                                            "max": 2.3978065580305032,
                                                            "format": "cores"
                                                        },
                                                        "memoryUsage": {
                                                            "min": 2.118012928E9,
                                                            "q1": 2.192392192E9,
                                                            "median": 3.6808704E9,
                                                            "q3": 4.093349888E9,
                                                            "max": 4.163411968E9,
                                                            "format": "bytes"
                                                        }
                                                    },
                                                    "2024-09-30T09:16:40.000Z": {},
                                                    "2024-10-02T09:16:40.000Z": {
                                                        "cpuUsage": {
                                                            "min": 0.00554280490421283,
                                                            "q1": 0.015358846193868379,
                                                            "median": 0.015705212168337323,
                                                            "q3": 1.010702281083678,
                                                            "max": 1.0139464901392594,
                                                            "format": "cores"
                                                        },
                                                        "memoryUsage": {
                                                            "min": 2.192125952E9,
                                                            "q1": 2.717663232E9,
                                                            "median": 2.719612928E9,
                                                            "q3": 2.719617024E9,
                                                            "max": 2.720600064E9,
                                                            "format": "bytes"
                                                        }
                                                    },
                                                    "2024-09-28T09:16:40.000Z": {},
                                                    "2024-10-03T09:16:40.000Z": {
                                                        "cpuUsage": {
                                                            "min": 0.005373319820852367,
                                                            "q1": 0.006054991034195089,
                                                            "median": 0.006142447129874265,
                                                            "q3": 0.006268777122325054,
                                                            "max": 0.007366566784856696,
                                                            "format": "cores"
                                                        },
                                                        "memoryUsage": {
                                                            "min": 2.192125952E9,
                                                            "q1": 2.192388096E9,
                                                            "median": 2.192388096E9,
                                                            "q3": 2.192388096E9,
                                                            "max": 2.192654336E9,
                                                            "format": "bytes"
                                                        }
                                                    },
                                                    "2024-10-01T09:16:40.000Z": {
                                                        "cpuUsage": {
                                                            "min": 0.003319077875529473,
                                                            "q1": 1.0101034685479167,
                                                            "median": 1.0118171810142638,
                                                            "q3": 1.0208974318073034,
                                                            "max": 3.5577616386258963,
                                                            "format": "cores"
                                                        },
                                                        "memoryUsage": {
                                                            "min": 1.77057792E8,
                                                            "q1": 2.64523776E9,
                                                            "median": 2.651078656E9,
                                                            "q3": 2.693431296E9,
                                                            "max": 2.705133568E9,
                                                            "format": "bytes"
                                                        }
                                                    }
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
                ]
            }
        ],
        "version": "v2.0",
        "experiment_name": "human_eval_exp"
    }
]
```
</details>

### Invalid Scenarios:

<details>
<summary><b>Invalid experiment name</b></summary>

`experiment_name=stub-experiment`

```json
{
  "message": "Given experiment name - \" stub-experiment \" is not valid",
  "httpcode": 400,
  "documentationLink": "",
  "status": "ERROR"
}
```

</details>

<details>
<summary><b>Invalid Timestamp format</b></summary>

`monitoring_end_time=Tony Stark` (Invalid Timestamp)

```json
{
  "message": "Given timestamp - \" Tony Stark \" is not a valid timestamp format",
  "httpcode": 400,
  "documentationLink": "",
  "status": "ERROR"
}
```

</details>


<details>
<summary><b>Non Existing Timestamp</b></summary>

`monitoring_end_time=2022-12-20T17:55:07.000Z`

```json
{
  "message": "Recommendation for timestamp - \" 2022-12-20T17:55:07.000Z \" does not exist",
  "httpcode": 400,
  "documentationLink": "",
  "status": "ERROR"
}
```

</details>