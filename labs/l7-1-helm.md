# Helm Usage Exercise

## Objective

This exercise will guide you through the process of checking the structure of a Helm chart, deploying a Helm chart, demonstrating the history, upgrading, rolling back, and packaging a Helm chart.

## Prerequisites

- A running Kubernetes cluster
- [helm installed and configured](https://helm.sh/docs/intro/install/) 

## Step 1. Check the Structure of a Helm Chart

Helm uses a packaging format called charts. A chart is a collection of files that describe a related set of Kubernetes resources. You can check the structure of a Helm chart by creating a new one:

```bash
helm create my-chart
```

You can check the structure with the following:

```bash
tree my-chart
```

## Step 2. Deploy a Helm Chart

You can deploy a Helm chart to your Kubernetes cluster with the helm install command:

```bash
helm install my-release my-chart
```

## Step 3. Demonstrate the History

Helm tracks each release of your application, making it possible to rollback to previous versions. You can view the history of releases with the helm history command:

```bash
helm history my-release
```

## Step 4. Demonstrate Upgrading

You can upgrade your application with the helm upgrade command:

```bash
helm upgrade my-release my-chart
```

## Step 5. Demonstrate Rollback

If something goes wrong during an upgrade, you can rollback to a previous release with the helm rollback command:

```bash
helm rollback my-release 1
```

## Step 6. Package a Helm Chart

Finally, you can package your Helm chart into a versioned chart archive file with the helm package command:

```bash
helm package my-chart
```

## Conclusion

In this exercise, you have learned how to check the structure of a Helm chart, deploy a Helm chart, demonstrate the history of releases, upgrade and rollback releases, and package a Helm chart. This knowledge is crucial for managing applications in Kubernetes with Helm.
