---
weight: 401
title: "Overview"
description: "Exec plugins provide capabilities for executing commands and providing shell access to resources."
icon: "extension"
date: "2024-03-09T16:57:24-06:00"
lastmod: "2024-03-09T16:57:24-06:00"
draft: false
---

Exec plugins provide capabilities for executing commands and providing shell access to resources. Exec plugins provide a means to authenticate to a machine that can be used to execute commands. This is useful for tasks such as running scripts, gathering information, or executing commands on remote systems.

The Omniview core provides two primary built-in exec plugins:

- [Local](/plugins/exec/local)
- [SSH](/plugins/exec/ssh)

However, you can also create custom exec plugins to support other protocols or systems. For example:

- AWS Session Manager
- Kubernetes Exec

The `ExecPlugin` SDK provides a set of interfaces and types that you can use to create custom exec plugins. In the following section, we'll go through how to use the `ExecPlugin` SDK to recreate the SSH exec plugin.

{{< alert context="alert" text="Omniview is under heavy active development - the `ExecPlugin` SDK is subject to frequent breaking changes until the first stable release." />}}

