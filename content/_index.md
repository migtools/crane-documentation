---
title: "Overview"
date: 2021-11-16T12:08:47-05:00
draft: false
---
> **Warning** Crane documentation has been moved to the [new official Konveyor documentation website](https://konveyor.github.io/) and [GitHub Repo](https://github.com/konveyor/konveyor.github.io/tree/main).

# What is crane?

Crane is a tool that helps application owners migrate Kubernetes workloads and their state between clusters, remove environment-specific configuration and automate application deployments along the way. The work is spread among a few projects:

- [crane](https://github.com/konveyor/crane): The command line tool that brings the ability to migrate applications to the terminal.
- [crane-lib](https://github.com/konveyor/crane-lib): This is the brains behind crane actions and is responsible for transforming resources.
- [crane-plugin-openshift](https://github.com/konveyor/crane-plugin-openshift): Plugin specifically tailored to managing the migration of OpenShift workloads. Also serves as an example of codifying knowledge/best-practices in a repeatable way. 
- [crane-plugins](https://github.com/konveyor/crane-plugins):  Collection of plugins from the konveyor community based on our experience with Kube migrations.
  
**NOTE**:
- Additional plugins will be added as new "crane-plugin-<plugin>" repos
- CLI commands and plugins are explained in depth in later part of the document, visit Usage to understand how crane works.
  
# Why crane is needed?

Crane is the product of our team distilling several years of experience performing large-scale production Kubernetes migrations. These operations are large, complex, error-prone, and usually must be peformed under a limited window of time. Because of that challenge, its paramount that a migration tool be designed with transparency and ease-of-diagnostics in mind. Crane is designed to drive a migration via a pipeline of non-destructive tasks that dump their results to disk so the operation can be easily audited and versioned without ever impacting live workloads. The tasks are [idempotent](https://en.wikipedia.org/wiki/Idempotence), meaning they can be run repeatedly and will output consistent results given the same inputs without side-effects on the system at large.

