# Admission controllers

When a request reaches the API server, it is first handled bz an authentication process.

After successful authentication, the request undergoes an authorization process using `**role-based access control (RBAC)**`.

A role may be defined to allow specific operations on pods:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: developer
rules:
  - apiGroups: [""]
    resources: ["pods"]
    verbs: ["list", "get", "create", "update", "delete"]
```

This configurations permits a user assigned to the developer role to list, get, create, update, and delete pods.

RBAC rules can be further refined to target specific resource names. For instance, to restrict a developer so they can only create pods with designated names:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: developer
rules:
  - apiGroups: [""]
    resources: ["pods"]
    verbs: ["create"]
    resourceNames: ["blue", "orange"]
```

However, object-level permissions may not be sufficient in certain scenarios. When a pod creation request is received, you might need to inspect the configuration, e.g. verifying that the pod does not use images from public registries, enforcing the use of a designated registry, or disallowing the "latest" tag.

You might also enforce security policies, such as ensuring container is not running as the root user or rejecting certain capability configurations.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: web-pod
spec:
  containers:
    - name: ubuntu
      image: ubuntu:latest
      command: ["sleep", "3600"]
      securityContext:
        runAsUser: 0
      capabilities:
        add: ["MAC_ADMIN"]
```

Standard RBAC rules operate only at the API level and cannot inspect or modify object's contents. This limitation is overcome by admisison controllers.

## Admission Controllers

**`Admission controllers`** validate and even mutate requests prior to persisting objects.

Admission controllers can enforce specific policies, such as:

- Changing requests based on internal guidelines
- Enforcing container image policies
- Ensuring that certain metadata labels are always applied

Kubernetes includes a variety of built-in admission controllers:

- Always Pull Images: Forces the pod to pull images from the registry every time.
- Default Storage Class: Automatically adds a default storage class to PersistentVolumeClaims (PVCs) when none s provided.
- Event Rate Limit: Restricts the API server's request-handling rate.
- Namespace Exists: Ensures that requested namespaces exist before proceeding.

## Namespace Admission Controllers

The namespace admission controller ensures that pods are created only in existing namespaces. It checks for the existence of defined namespace and rejects the request if it does not exist.

```bash
kubectl run nginx --image nginx --namespace blue

Error from server (NotFound): namespaces "blue" not found
```

Alternatively, Kubernetes offers the namespace auto-provision admission controller, which automatically creates a namespace if it does not exist.

To view the admission controllers enabled by default:
kube-apiserver -h | grep enable-admission-plugins

This command will list plugins such as NamespaceLifecycle, LimitRanger, ServiceAccount, TaintNodesByCondition, among others. If you are using a kubeadm-based setup, run the command within the kube-apiserver control plane using kubectl exec.

## Enabling Admission Controllers

To add an admission controller, update the --enable-admission-plugins flag on the kube-apiserver. In kubeadm, this involves modifying the kube-apiserver manifest, or the Pod manifest if it's the kubeadm setup where it runs as a Pod.

```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  name: kube-apiserver
  namespace: kube-system
spec:
  containers:
    - command:
        - kube-apiserver
        - --authorization-mode=Node,RBAC
        - --advertise-address=172.17.0.107
        - --allow-privileged=true
        - --enable-bootstrap-token-auth=true
        - --enable-admission-plugins=NodeRestriction,NamespaceAutoProvision
      image: k8s.gcr.io/kube-apiserver-amd64:v1.11.3
      name: kube-apiserver
```

To disable specific admission controller plugins, use the --disable-admission-plugins flag similarly.
