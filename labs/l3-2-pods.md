# Kubernetes Pods

This exercise will help you interact with Pods in Kubernetes using `kubectl`.

## Exercise 1: List All Pods in All Namespaces

List all the pods in all namespaces using the following command:

```bash
kubectl get pods --all-namespaces
```

## Exercise 2: Create a Pod Imperatively

Create a pod named my-pod with the nginx image:

```bash
kubectl run my-pod --image=nginx
```

## Exercise 3: Check Pod StatusCheck the status of my-pod:

```bash
kubectl get pod my-pod
```
## Exercise 4: Create a Pod ManifestCreate a manifest for a pod with the nginx image:

```bash
kubectl run my-pod --image=nginx --dry-run=client -o yaml > my-pod.yaml
```

## Exercise 5: Create a Pod from ManifestCreate a pod from the manifest file my-pod.yaml:

```bash
kubectl apply -f my-pod.yaml
```

## Exercise 6: Enter a PodEnter the my-pod pod and start an interactive shell:

```bash
kubectl exec -it my-pod -- /bin/bash
```

## Exercise 7: Delete a PodDelete the my-pod pod:

```bash
kubectl delete pod my-pod
```

Remember to replace `my-pod` and `nginx` with your actual pod name and image.

