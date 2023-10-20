# Connection to Kubernetes Cluster Setup Guide

This guide will help you set up `kubectl` and connect to your Kubernetes cluster.

## Step 1: Copy Kubeconfig

First, you need to copy our kubeconfig file to your local machine. This file should be located in the `~/.kube` directory. File is provided by the lecturer.

```bash
cp /path/to/your/kubeconfig ~/.kube/config
```

## Step 2: Install kubectl

Next, install kubectl, which is the Kubernetes command-line tool. You can install it by following instructions from [this link](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/).


## Step 3: Install Google Cloud SDK and gcloud plugin

We will interact with Kubernetes cluster running on GCP (GKE). That's why we need to follow this step.

Install the Google Cloud SDK, which includes the gcloud command-line tool. Also, install the kubectl plugin for gcloud. Instructions are on the [following link](https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl).

## Step 4: Perform Login

Log in to your (or lab) Google Cloud account:

```shell
gcloud auth login
```

Follow the prompts to authorize the gcloud tool to use your Google Cloud account.

## Step 5: Test Connection

Finally, test your connection to the Kubernetes cluster:

```shell
kubectl get nodes
```

If everything is set up correctly, this command should return a list of the nodes in your cluster.

# Understanding kubectl Command Structure

The `kubectl` command line tool is used to interact with Kubernetes clusters. The general structure of a `kubectl` command is as follows:

```bash
kubectl [command] [TYPE] [NAME] [flags]
```

Here's what each part means:

- [`command`]: This specifies the operation that you want to perform on one or more resources, such as create, get, describe, delete.
- [`TYPE`]: This is the type of resource to perform the operation on. Resources include pods (po), services (svc), deployments (deploy), and others.
- [`NAME`]: This is the name of the resource. Names are case-sensitive. If the name is omitted, details for all resources are displayed.
- [`flags`]: These are optional and allow you to specify additional options.

Here's an example command:

```bash
kubectl get pods my-pod
```

In this example, get is the command, pods is the type, and my-pod is the name of the resource we're retrieving information about.

