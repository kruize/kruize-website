---
title: Autotune Release Notes
sidebar: mydoc_sidebar
permalink: autotune_release_notes.html
folder: mydoc
---

## Kruize Version 0.4

You can get it from [quay.io/kruize/autotune_operator:0.4](https://quay.io/kruize/autotune_operator:0.4) or [docker.io/kruize/autotune_operator:0.4](https://docker.io/kruize/autotune_operator:0.4)
Branch: master, Tag: v0.4
Commit id: `58b8bf8c2feb9b5ca1719a4f7d11faf41b2fea47`

### Major changes include

- [API] Add support for MetadataProfile
- [API] New Bulk API format related to kafka changes
- [API] Alpha level support for GPU autoscaling (MIG right-sizing) with Instaslice integration
- [API] Add config support for single term and single model to be specified in createExperiment API
- [API] Autoscaler to use custom term and model specified in createExperiment API
- [Bug] VPA Integration validation checks
- [Bug] Dynamically calculate threshold value for term
- [Bug] Update ubi-minimal with latest
- [Bug] Fix RBAC error in Kruize log 
- [Demo] Bulk demo UX updates
- [Demo] GPU Demo for instaslice inetgration
- [Tests] Add stress tests for bulk API
- [Tests] Add VPA testing


**Full Changelog**: [Changelog] (https://github.com/kruize/autotune/compare/v0.3...v0.4)


## Older Versions

Click here: [Kruize Older Versions](https://github.com/kruize/autotune/releases) 


{% include links.html %}
