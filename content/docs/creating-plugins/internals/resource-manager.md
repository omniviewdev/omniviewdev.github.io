---
weight: 999
title: "Resource Manager"
description: "The manager responsible for defining available resources, their capabilities and metadata, and backend discovery"
icon: "dataset"
date: "2024-03-12T13:30:24-05:00"
lastmod: "2024-03-12T13:30:24-05:00"
draft: false
toc: true
---

The Resource Manager is responsible for defining available resources, their capabilities and metadata, and performing discovery against backends to determine which auth contexts have access to which resources. This is crucial for resource backends like Kubernetes, where different auth contexts (in the case of Kubernetes, and uth context would be a Cluster Context) can have different resources (or versions of a resource) available (one cluster on 1.26 may have `v2.HorizontalPodAutoscaler`, while another on 1.22 may instead still use the `v2beta2.HorizontalPodAutoscaler`).

## Plugin Lifecycle Events

The resource manager performs the following tasks during the plugin lifecycle:

### OnPluginLoad

N/A

### OnPluginInit

- Loads all resource into the manager

### OnPluginStart

- Reads the auth contexts and their last seen resource maps into the manager

### OnPluginStop

- Saves the auth contexts and their last seen resource maps to disk

### OnPluginUnload

N/A

### OnPluginDestroy

- Removes the resource state file from disk


## Auth Context Events

The resource manager performs the following tasks on each auth context event:

### OnAuthContextCreate

- Adds a new auth context to the manager
- If discovery is enabled, performs an initial discovery operation against the auth context to detect available resources
- If discovery is not enabled, it sets the available resources to a copy of the full list of resources in the manager

### OnAuthContextStart

- If discovery is enabled, performs a discovery sync to detect available resources
- If discovery is not enabled, it sets the available resources to a copy of the full list of resources in the manager
- Backs up the current resource map for the auth context

### OnAuthContextStop

*Nothing is performed*

### OnAuthContextReload

- If discovery is enabled, performs a discovery sync to detect available resources


### OnAuthContextDestroy
