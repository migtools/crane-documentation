---
title: "Apply"
date: 2021-11-16T12:38:01-05:00
draft: false
---

The final step of the process is `apply`, all the patches generated through `transform` can be applied to exported resources via `apply`. This command consumes the output of `transform` command.

#### Example

```
crane apply -e export -t transform -o output
```

Apply the patches in the `transform` directory to the resources in the `export` directory and save the modified resource files in the `output` directory.


> After applying the patches, the resources located in `output` directory can either be deployed in the destination cluster using `kubectl apply`, or they can be pushed to a repository and then can be applied with the help of GitOps pipeline. An example of the later scenario can be found [here](../Advance%20Usage/gitops.md)).
