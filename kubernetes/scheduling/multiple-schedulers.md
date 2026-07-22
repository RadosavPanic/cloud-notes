# Multiple Schedulers in Kubernetes

Kubernetes' default scheduler distributes pods across nodes evenly while considering factors such as taints, tolerations, and node affinity.

However, certain use cases may require a custom scheduling algorithm.
For instance, when an application needs to perform extra verification before placing its components on specific nodes, a custom scheduler becomes essential.

By writing your own scheduler, packaging it, and deploying it alongside the default scheduler, you can tailor pod placement to your specific needs.

Ensure that every additional scheduler has a unique name. The default scheduler is conventionally named "default-scheduler", and any custom scheduler must be registered with its own distinct name in the configuration files.

## Deployment an Additional Scheduler

You can deploy an additional scheduler using the existing kube-scheduler binary, tailoring its configuration through specific service files.

After downloading the kube-scheduler binary, you need to create services files for each scheduler:

```bash
ExecStart=/usr/local/bin/kube-scheduler --config=/etc/kubernetes/config/my-scheduler-config.yaml
```

Reference the scheduler names in the associated configuration files:

### my-scheduler-config.yaml

```
apiVersion: kubescheduler.config.k8s.io/v1
kind: KubeSchedulerConfiguration
profiles:
  - schedulerName: my-scheduler
```

## Deploying the Custom Scheduler as a Pod

In addition to running the scheduler as a service, you can deploy it as a pod inside the Kubernetes cluster. The corresponding custom KubeSchedulerConfiguration should be referenced as well as displayed below.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-custom-scheduler
  namespace: kube-system
spec:
  containers:
    - name: kube-scheduler
      image: k8s.gcr.io/kube-scheduler-amd64:v1.11.3
      command:
        - kube-scheduler
        - --address=127.0.0.1
        - --kubeconfig=/etc/kubernetes/scheduler.conf
        - --config=/etc/kubernetes/my-scheduler-config.yaml
```

## Deploying the Custom Scheduler as a Deployment

In many modern Kubernetes setups, especially those using kubeadm - control plane components run as pods or deployments.

Possible steps:

1. Build and push a Custom Scheduler Image
2. Create ServiceAccount and RBAC Configurations
3. Create a ConfigMap for Scheduler Configuration
4. Define the Deployment, also ensure a proper ClusterRole exists for the scheduler

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-scheduler-config
  namespace: kube-system
data:
  my-scheduler-config.yaml: |
    apiVersion: kubescheduler.config.k8s.io/v1beta2
    kind: KubeSchedulerConfiguration
    profiles:
      - schedulerName: my-scheduler
        leaderElection:
          leaderElect: false
```

**`Leader election`** is an important configuration for high-availability environments. It ensures that while multiple scheduler instances are running, only one actively schedules the pods.

To have specific pods or deployments use custom scheduler, you can add schedulerName field in the pod's specification.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
    - name: nginx
      image: nginx
  schedulerName: my-custom-scheduler
```

To confirm which scheduler assigned a pod, we can review events or logs with kubectl get events and kubectl logs.
