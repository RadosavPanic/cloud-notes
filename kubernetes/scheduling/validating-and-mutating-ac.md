# Validating and Mutating Admission Controllers

**`Validating admission controllers`** verify that an object meets specific criteria before it is persisted in the cluster (e.g. namespace existence or namespace lifecycle AC).

Another example is Default Storage Class AC. When you create a PVC (PersistentVolumeClaim) without specifying a storage class, this validating controller intercepts the request and modifies it by adding the default storage class.

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: myclaim
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 500Mi
  storageClassName: default # this line is added by admission controller
```

Since the controller modifies the request, such controllers are also considered mutating admission controllers.

## Mutating vs Validating Admission Controllers

Admission controllers in Kubernetes can be classified into two main types:

- Mutating Admission Controllers: Modify (mutate) objects before they are persisted.
- Validating Admission Controllers: Validate objects to ensure they meet specific criteria, allowing or denying the request accordingly.

Some controllers perform both mutation and validation.

Typically, mutating controllers run first so that subsequent validating controllers can work with the modified object.

For instance, if a namespace auto-provisioning mutating AC creates a missing namespace before the namespace existence validating controller runs, the request proceeds smoothly. Otherwise, if the validating controller executes first, it would reject the request due to the missing namespace.

TIP: If any admission controller (mutating or validating) rejects a request, the entire request is denied and an error is returned to the user.

## Admission Webhooks

All built-in admission controllers are part of the Kubernetes source code.

But for custom validations and mutations, Kubernetes supports external admission controllers using webhook mechanisms:

- Mutating Admission Webhook
- Validating Admission Webhook

## Configuring External Admission Webhooks

External admission webhooks can point to servers either inside or outside the Kubernetes cluster.

Once the built-in admission controllers finish processing, the API server sends an AdmissionReview object (in JSON format) containingg request details such as user information, operation type, and object metadata to the external webhook.

```json
{
  "apiVersion": "admission.k8s.io/v1",
  "kind": "AdmissionReview",
  "request": {
    "uid": "705ab415-6393-11e7-b7cc-4201a8000002",
    "kind": { "group": "autoscaling", "version": "v1", "kind": "Scale" },
    "resource": { "group": "apps", "version": "v1", "resource": "deployments" },
    "subresource": "scale",
    "requestKind": { "group": "autoscaling", "version": "v1", "kind": "Scale" },
    "requestResource": {
      "group": "apps",
      "version": "v1",
      "resource": "deployments"
    }
  }
}
```

The webhook server processes the AdmissionReview request and responds with its own AdmissionReview JSON object. Response can look like this:

```json
{
  "apiVersion": "admission.k8s.io/v1",
  "kind": "AdmissionReview",
  "request": {
    "uid": "705ab41f-6393-11e8-b7cc-4201a8000002",
    "kind": {
      "group": "autoscaling",
      "version": "v1",
      "kind": "Scale"
    },
    "resource": {
      "group": "apps",
      "version": "v1",
      "resource": "deployments"
    },
    "subResource": "scale",
    "requestKind": {
      "group": "autoscaling",
      "version": "v1",
      "kind": "Scale"
    },
    "requestResource": {
      "group": "apps",
      "version": "v1",
      "resource": "deployments"
    }
  },
  "response": {
    "uid": "<value_from request.uid>",
    "allowed": true
  }
}
```

If the **`"allowed"`** field is set to false, the API server rejects the request.

When webhook is created etc. in Go, or Python, we can deploy webhook server as a standalone service or containerize it and run it within our Kubernetes cluster.

To instruct the API server to use your webhook for validations and mutations, create a ValidatingWebhookConfiguration or a MutatingWebhookConfiguration object.

```yaml
apiVersion: admissionregistration.k8s.io/v1
kind: ValidatingWebhookConfiguration
metadata:
  name: "pod-policy.example.com"
webhooks:
  - name: "pod-policy.example.com"
    clientConfig:
      service:
        namespace: "webhook-namespace"
        name: "webhook-service"
      caBundle: "Ci0tLS0tQk......tLS0K"
    rules:
      - apiGroups: [""]
        apiVersions: ["v1"]
        operations: ["CREATE"]
        resources: ["pods"]
        scope: "Namespaced"
```

- The clientConfig block specifies how the API server connects to your webhook service, including the TLS certificate bundle (caBundle).
- The rules section defines the operations that trigger the webhook, in this case whenever a pod is created.
