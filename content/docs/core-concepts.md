---
weight: 4
title: "Core Concepts"
description: ""
icon: "schema"
date: "2024-03-09T16:53:45-06:00"
lastmod: "2024-03-09T16:53:45-06:00"
draft: false
toc: true
---

Omniview is built on a set of core concepts that guide its design, functionality, and user experience. Understanding these principles is key to leveraging Omniview to its full potential, allowing DevOps engineers to manage and visualize their infrastructure efficiently and effectively.

## Modular Architecture

Omniview's architecture is modular, designed to be both extensible and scalable. It separates concerns between the frontend and backend, enabling a responsive user interface and robust backend services that can handle complex operations and integrations.

### Backend
- **Go**: The backend is built in Go for performance and efficiency, handling tasks such as data processing, plugin management, and external communications.
- **GraphQL**: A GraphQL layer provides a flexible and efficient API for the frontend to query and manipulate data.

### Frontend
- **React**: The frontend is developed with React, offering a dynamic and modern user interface.
- **Material-UI**: This framework provides a cohesive look and feel, with reusable components that ensure a consistent user experience.

## Plugin System

The plugin system is at the heart of Omniview's extensibility. It allows third-party developers and users to extend Omniview's capabilities by adding new features, integrating with external tools, and customizing the environment to fit their workflow.

## Cloud-Native Integration

Omniview embraces a cloud-native approach, with first-class support for Kubernetes and major cloud providers. This ensures seamless management of cloud resources, Kubernetes clusters, and applications, all within a unified interface.

- **Kubernetes Integration**: Deep integration with Kubernetes allows for managing deployments, services, and monitoring within Omniview.
- **Cloud Providers**: Direct connections to AWS, Azure, Google Cloud, and other cloud services enable comprehensive management of cloud resources.

## Infrastructure as Code (IaC)

Omniview supports Infrastructure as Code (IaC), allowing users to define and manage infrastructure using configuration files. This aligns with modern DevOps practices, facilitating version control, repeatability, and automation.

## Conclusion

The core concepts of Omniview—its modular architecture, plugin system, cloud-native integration, and support for IaC—form the foundation of a powerful IDE tailored for the needs of DevOps engineers. By understanding these principles, users can fully utilize Omniview to streamline their infrastructure management and operations.

---

Next, we will explore how to set up your first project in Omniview and begin managing your infrastructure.
