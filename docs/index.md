---
title: "Kruize Autotune"
keywords: sample homepage
sidebar: mydoc_sidebar
permalink: index.html
summary: These brief instructions will help you get started quickly with the kRUIZE. 
---

## Overview

Kruize is a resource recommendation and autoscaling engine. It provides container and namespace right-sizing recommendations in Kubernetes in the form of CPU and memory requests and limits as well as MIG slicing recommendations for Nvidia accelerators. 

The recommendations are based on monitoring a data source such as Prometheus where the data source can be local or remote. The recommendations are based on resource usage in the past 24 hours (short term), 7 days (medium term) and 15 days (long term) and provide cost and performance-optimized suggestions for each term on a per container basis.Kruize also provides capacity and utilization data that can be used to represent resource request vs actual resource utilization data, for instance as a box plot, to better understand the recommendations.

## Modes of Operation
### Right-sizing 

In the right-sizing mode, Kruize is connected to a local or a remote data source such as prometheus / thanos and can provide right-sizing recommendations for containers and namespaces based on monitoring. The container right sizing includes CPU, Memory and Nvidia Accelerators. Namespace recommendations are in the form of hard limits for CPU and memory resources as part of the namespace quota. Right sizing for Nvidia accelerators are in the form of MIG (Multi Instance GPU) slices for those accelerators that support MIG (Eg A30, A100, H100 etc).

This mode has been productized and is the backend engine for Resource Optimization Service as part of RH Insights. This service is now available to all OCP customers. Slightly over one third of all OCP customers (~1000) are now using this service. (Tracked through the usage of the Cost Operator)
Autoscaling

In the autoscaling mode, Kruize integrates with autoscalers such as VPA (Vertical Pod Autoscaler) and Instaslice to apply the recommendations it generates. VPA is the default Kubernetes Pod autoscaler for vertical scaling. Instaslice is an IBM research project for Nvidia MIG partitioning that is currently being productized as part of OCP.
VPA Integration
Kruize uses VPA under the covers to apply CPU and memory right sizing recommendations. Kruize supports two modes “auto” and “recreate” that correspond to the modes of VPA with the same names. Kruize creates a custom VPA recommender object and pushes recommendations to this VPA object. This then gets picked up by VPA, which actually applies the recommendations.

### Instaslice Integration
Kruize uses Instaslice under the covers to apply MIG slicing recommendations for Nvidia accelerators. In “auto” and “recreate” modes, if Kruize detects the presence of GPU metrics for accelerators that support MIG slicing, Kruize generates appropriate MIG slicing recommendations. This gets picked up by Instaslice which will then create the appropriate MIG partitioning scheme on the accelerator and assigns it to the container.

Kruize Autoscaling is now available as an alpha level feature and is on track to be made available as a Day 2 operator on OCP (Expected 2H 2025)

### AI - Autotune

Kruize supports “autotune” mode that addresses complex user defined performance objectives. In this mode, Kruize performs a series of trials with a different set of values for tunables associated with the application container until it can find the right set of values for the tunables that match the user provided performance goal. The user needs to capture the performance objective in the form of a Service Level Objective or SLO. Kruize uses Hyper Parameter Optimization or HPO algorithms that can help narrow down the values of the tunables to achieve the user provided objective. Kruize supports a broad range of tunables including at the container level, runtime level (Eg JVM) and framework level (Eg EAP and Quarkus)

Kruize Autotune is a PoC only feature. However this has been used by Perf and Scale teams to tune the OS (Node Tuning Operator (NTO) Profiles), Apache Kafka service tuning, by Quarkus to get better performance, and currently ongoing collaboration with EAP as part of a sustainability initiative.



{% include links.html %}
