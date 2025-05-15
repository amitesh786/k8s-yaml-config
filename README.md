# Kubernetes Configuration Demo

This project provides an overview and hands on demo of key `Kubernetes` configuration concepts. It's designed for learners who want to understand the structure of `Kubernetes` config files and how to connect components like Pods, Deployments, and Services.

## Three parts of a `Kubernetes` configuration file

A typical `Kubernetes` configuration file (written in `YAML`) includes these sections:

- **Metadata**: Specifies the object's name, namespace, labels, and annotations.
- **Spec (Specification)**: Describes the desired state of the object, such as containers and volumes.
- **Status**: Indicates the current state of the object. This is maintained by Kubernetes and not manually written.

## Configuration file format

All `Kubernetes` config files use YAML syntax. Here's a simple structure:

```yaml
apiVersion: v1  # API version used
kind: Pod       # Type of Kubernetes object
metadata:
  name: my-app  # Name of the Pod
spec:
  containers:
    - name: my-container
      image: nginx  # Container image to run
```

## Blueprint for Pods

Pods are the smallest deployable units in `Kubernetes`. They can be created directly or managed using higher-level objects like Deployments.

In a Deployment, the `template` field defines the Pod specification:

```yaml
spec:
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: app-container
          image: my-image
```

## Connecting services to Deployments and Pods

To expose Pods to other components or external traffic, you define a Service. Services use:

- **Labels**: Assigned to Pods (e.g., `app: my-app`)
- **Selectors**: Used by Services to identify which Pods to expose
- **Ports**: Define how the Service forwards traffic to Pods

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
```

## Demo

A working example is provided in the `/root` directory with:

- `deployment.yaml` – A Deployment configuration with replicas
- `deployment-result.yaml` – A simple Pod definition
- `service.yaml` – A Service to expose the Pods

- Instructions to apply configs using kubectl

To run the demo:
- `kubectl apply -f demo/`
- `kubectl get all`

## 🧑‍💻 Developer Setup
- Clone the repository:
- git clone `https://github.com/amitesh786/k8s-yaml-config.git`

## 👨‍💻 Author Amitesh Singh – [GitHub](https://github.com/amitesh786)
- Feel free to contribute or suggest improvements! 🙌
