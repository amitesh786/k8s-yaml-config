# Kubernetes Configuration Demo

This project provides an overview and hands on demo of key `Kubernetes` configuration concepts. It's designed for learners who want to understand the structure of `Kubernetes` config files and how to connect components like Pods, Deployments, and Services.

## Three parts of a `Kubernetes` configuration file

A typical `Kubernetes` config file (written in `YAML`) includes these main sections:

- **Metadata**: Defines the name, namespace, labels, and annotations of the object.
- **Specification (spec)**: Describes the desired state, including containers, volumes, and other runtime settings.
- **Status**: Reflects the current state of the object (managed by `Kubernetes`, not usually written by the user).

## Configuration file format

All `Kubernetes` config files use YAML syntax. Here's a simple structure:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-app
spec:
  containers:
    - name: my-container
      image: nginx
```

## Blueprint for Pods

Pods are the smallest deployable units in `Kubernetes`. They can be created manually or managed via higher level objects like Deployments.

Templates are used in Deployments to define the Pod spec:

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

To expose Pods, you create a Service that uses:

- **Labels**: Assigned to Pods (e.g., app: my-app)
- **Selectors**: Used by services to match pods
- **Ports**: Define how traffic is forwarded

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

A working `root` is included in the `/root` directory with:

- `deployment-result.yaml` – A simple Pod definition
- `deployment.yaml` – A Deployment with replicas
- `service.yaml` – A Service exposing the Pods
- Instructions to apply configs using kubectl

To run the demo:
- `kubectl apply -f demo/`
- `kubectl get all`

## 🧑‍💻 Developer Setup
- Clone the repository:
- git clone `https://github.com/amitesh786/k8s-yaml-config.git`

## 👨‍💻 Author Amitesh Singh – [GitHub](https://github.com/amitesh786)
- Feel free to contribute or suggest improvements! 🙌
