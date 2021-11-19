---
title: "Gitops"
date: 2021-11-16T12:38:56-05:00
draft: false
---

All the crane commands are individual utilities, but when used together in an order, they form a pipeline. Crane makes it easy to integrate a gitops that applies the patches/resources generated at the end of `apply` on the destination cluster. The resources generated at the end of the process (i.e `export`, `transform`, `apply`), can be pushed to a github repository, and a pipeline can be setup that deploy the resources on a cluster on every push.
