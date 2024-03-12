---
weight: 999
title: "The Plugin Engine"
description: "A breakdown of the internals of how plugins work."
icon: "auto_transmission"
date: "2024-03-12T12:25:00-05:00"
lastmod: "2024-03-12T12:25:00-05:00"
draft: true
toc: true
---

Plugins are a core part of the Omniview ecosystem, and the plugin engine is designed to be both flexible and extendable. In order to satisfy the various requirements of various plugin types, the core engine embeds various controllers, engines, and interfaces to provide a consistent and reliable experience for plugin developers and users.

At it's core, a plugin consists of a few key components:

## Plugin Definition

The plugin definition includes metadata that defines the details and capabilities of the plugin, including the name, description, type, and other details. This is stored in a `plugin.yaml` file, and is used by the plugin host to load, verify, and execute the plugin.

[The plugin definition can be found here with all of it's options.](../api/plugin-definition.md)

## Plugin Host

Each plugin that requires a backend runs a separate instance of the plugin host, which the core plugin subsystem is responsible for loading and executing. The plugin host is only responsible for managing it's own lifecycle.

Under the hood, the system uses the [`go-plugin`](https://github.com/hashicorp/go-plugin) package by HashiCorp to provide a secure and reliable runtime environment for the plugin. This package provides a secure and reliable way to execute plugins, and is designed to be both flexible and extendable. When a plugin is launched, it does the following steps internally:

- Reads in the plugin definition and verifies it's integrity.
- Validates the required components are provided and are in the correct format according to the plugin definition.
- Starts the plugin host on a subprocess, which:
  - Generates a handshake configuration
  - Establishes a secure connection with the plugins
  - Starts a gRPC server to handle incoming requests
  - Establishes a Unix socket for the plugin to communicate with the host

### Why not use the native Go `plugin` package?

Go added a native plugin system in Go 1.8, which allows for the loading of Go code at runtime. However, this system has a few limitations that make it unsuitable for the Omniview plugin system:

- It requires the plugin to be compiled with the same version of Go as the host, which is not always possible
- Runtime panics in the plugin can crash the host
- It is not (at the time of writing) supported on Windows

**However**, this does not mean that the `go-plugin` package is a perfect solution. It has it's own limitations and drawbacks (mostly around the performance of communication over RPC vs native function calls), but it allows plugin maintainers to not have to worry about OS and Go version compatibility, and opens the door for future functionality, including:

- Dynamically sandboxing capabilities for plugins
- Writing backend plugins in other languages (such as Typescript, Rust, etc.)
- Additional runtime contracts and guarantees for plugin execution

{{< alert context="info" text="We are constantly assessing the plugin subsystem within Omniview. If you have ideas on how to make the subsystem better, we would love your feedback" />}}

## UI Components

Some plugins require a UI component to be displayed in the IDE. These components are loaded and managed by the UI subsystem, and are responsible for rendering and managing the UI components of the plugin.

UI components are written in React, and lazily loaded into a rendering view boundary of the main plugin window on demand. This allows for a more responsive and efficient user experience, as only the components that are currently visible are loaded and rendered.

Plugins that do not require a UI component are not required to implement this component, including:

- Exec plugins
- Log plugins

[The structure of the UI components folder within a plugin can be found here.](../api/ui-components.md)

