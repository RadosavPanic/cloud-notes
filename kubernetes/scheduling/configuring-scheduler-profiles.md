# Configuring scheduler profiles

When a pod is defined, it enters a scheduling queue along with other pending pods.

Pods with higher priorities are placed at the beginning of the queue.

### Scheduling Phases

1. Filter Phase: Nodes that cannot meet the pod's resource requirements (e.g., nodes lacking 10 CPUs) are filtered out.
2. Scoring Phase: Remaining nodes are scored based on resource availability after reserving the required CPU (e.g., a node with 6 CPUs left scores higher than the one with only 2).
3. Binding Phase: The pod is assigned to the node with the highest score.

### Key Scheduler Plugings

- **`Priority Sort Plugin`**: Sorts pods in the scheduling queue according to their priority
- **`Node Resources Fit Plugin`**: Filters out nodes that do not have the needed resources
- Node Name Plugin: Checks for a specific node name in the pod specification and filters nodes accordingly
- Node Unschedulable Plugin: Excludes nodes marked as unschedulable. E.g. running commands like drain or cordon will set the unschedulable flag.
  - Example:
    ```bash
    controlplane ~ → kubectl describe node controlplane
    Name:               controlplane
    Roles:              control-plane
    CreationTimestamp:  Thu, 06 Oct 2022 06:19:57 -0400
    Taints:             node.kubernetes.io/unschedulable:NoSchedule
    Unschedulable:      true
    Lease:
    ```
- **`Scoring Plugings:`** During the scoring phase, plugings such as NodeResourcesFit and ImageLocality plugins assess each node's suitability. They assign scores rather than outright rejecting nodes.
- **`Default Binder Plugin`**: Finalizes the scheduling process by binding the pod to the selected node.

**`Kubernetes emphasizes extensibility`**, allowing you to modify the scheduling process via extension points at stages such as queueing, filtering, scoring, and binding.

## Customizing Scheduler Behavior with Profiles

Rather than running separate scheduler binaries with distinct configuration files, Kubernetes 1.18 introduced support for multiple scheduling profiles within a single scheduler binary.

This approach minimizes operational overhead and prevents potential race conditions that can arise when multiple processes schedule workloads on the same node.

```yaml
apiVersion: kubescheduler.config.k8s.io/v1
kind: KubeSchedulerConfiguration
profiles:
  - schedulerName: my-scheduler-2
    plugins:
      score:
        disabled:
          - name: TaintToleration
        enabled:
          - name: MyCustomPluginA
          - name: MyCustomPluginB
  - schedulerName: my-scheduler-3
    plugins:
      preScore:
        disabled:
          - name: "*"
      score:
        disabled:
          - name: "*"
  - schedulerName: my-scheduler-4
```

Extensions points are defined in the plugins section, and you can enable or disable plugins by name (or using a wildcard pattern).

This flexible configuration allows you to tailor the scheduling behavior to meet your unique workload requirements by selectively enabling or disabling plugins across different profiles.
