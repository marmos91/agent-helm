# Agent Helm chart

Basic Helm chart to install Cubbit agent software on K8S.

## Prerequisites

- `helm`
- `kubectl`

## How to install the chart (if the namespace exists)

```
helm install <name> . --namespace <namespace>
```

## How to install the chart (if the namespace doesn't exist)

```
helm install <name> . --namespace <namespace> --create-namespace
```

## How to upgrade the chart

```
helm upgrade <name> . --namespace <namespace>
```

## How to uninstall

```
helm uninstall <name> --namespace <namespace>
```

## How to configure

Edit the file `values.yaml`. In the `swarm` section add a new object entry for each agent you want to deploy.
For each agent you need to specify

- `name`: a unique name for the deployment
- `secret` the AGENT_SECRET string. You can get that by inspecting the ansible playbook or the `docker run` command you downloaded from [composer.cubbit.eu](https://composer.cubbit.eu).
- `machineId`: same as `secret`
- `nodeName`: the k8s node name where to install this deployment. It will be used in the `nodeAffinity` spec.
- `storage`: how big the `persistentVolume` should be for the agent.

Example:

```

swarm:
  agents:
  - name: agent1
    secret: secret1
    machineId: machineId1
    nodeName: node1
    storage: 100G
  - name: agent2
    secret: secret2
    machineId: machineId2
    nodeName: node2
    storage: 100G
  - name: agent3
    secret: secret3
    machineId: machineId3
    nodeName: node3
    storage: 100G
```
