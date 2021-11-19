---
title: "Overview"
date: 2021-11-16T13:27:44-05:00
draft: false
---

Crane's workflow is phased, providing for significant transparency in the process. These phases are `export`, `transform`, and `apply`. There are corresponding commands to execute each phases explained in the coming sections.

You can think of these phases as an idempotent pipeline. The commands do not alter their inputs, so that you may run a command, verify its output, and if anything does not look correct, back up a single step and rerun the command after making some tweaks. This idempotency is incredibly useful when performing large scale migrations. It's directly something we've learned thanks to Crane 1.0. 

> NOTE: By default, crane will use your active kube context. Be sure to configure your context such that you're authenticated with your source cluster before continuing.
