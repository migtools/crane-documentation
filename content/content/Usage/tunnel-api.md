---
title: "Tunnel Api"
date: 2021-12-13T09:23:43-05:00
draft: false
---

The `tunnel-api` sub-command can be used to access an on-premise cluster from a cloud cluster. The intention is to allow orchestrating migrations from on-premise clusters using MTC where access is not possible otherwise.

To provide access an openvpn client on the on-premise cluster will connect to a server running on the cloud cluster. The openvpn server is exposed to the client using a load balancer address on the cloud cluster. 

A service created on the cloud cluster is used to expose the on-premise clusters API to MTC running on the cloud cluster.

## Requirements

- The system used to create the VPN tunnel must have access and be logged in to both clusters.
- It must be possible to create a load balancer on the cloud cluster
- An available namespace on each cluster to run the tunnel in. This should not be created in advance

<b>Note:</b> To connect multiple on-premise source clusters to your cloud cluster you should use a separate namespace for each.

## api-tunnel options

- namespace: The namespace to launch the VPN tunnel in, defaults to `openvpn`
- destination-context: The cloud destination cluster context where the openvpn server will be launched. 
- source-context: The on-premise source cluster context where the openvpn client will be launched.
- source-image: The container image to use on the source cluster. Defaults to quay.io/konveyor/openvpn:latest
- destination-image: The container image to use on the destination cluster. Defaults to quay.io/konveyor/openvpn:latest

### Example

```
crane tunnel-api --namespace openvpn-311 \
      --destination-context openshift-migration/c131-e-us-east-containers-cloud-ibm-com/admin \
      --source-context default/192-168-122-171-nip-io:8443/admin
```

### Specify an Alternate Image
If you need to specify a different image to use on one or both clusters, for instance because you need to mirror it to a local registry, you may do so.

```
crane tunnel-api --namespace openvpn-311 \
      --destination-context openshift-migration/c131-e-us-east-containers-cloud-ibm-com/admin \
      --source-context default/192-168-122-171-nip-io:8443/admin \
      --source-image: my.on.prem.registry/konveyor/openvpn:latest
```

## MTC Configuration
When configuring the source cluster in MTC the API URL takes the form of `https://proxied-cluster.${namespace}.svc.cluster.local`. 

Replace `${namespace}` with either `openvpn` or the namespace you specified when running the command to set up the tunnel.

## Demo
https://youtu.be/wrPVcZ4bP1M

## Troubleshooting
It may take 3 to 5 minutes after the setup to complete for the load balancer address to become resolvable. During this time the client will be unable to connect and establish a connection and the tunnel will not function.

During this time you can run `oc get pods` in the namespace you specified for setup, and monitor the logs of the openvpn container to see the connection establish.

### Example
`oc logs -f -n openvpn-311 openvpn-7b66f65d48-79dbs -c openvpn`

