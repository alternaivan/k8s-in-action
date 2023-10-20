# Kubernetes StatefulSets Exercise

## Step 1: Create a StatefulSet from Manifest

First, we need to create a StatefulSet from a manifest. Here's an example:

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: web
spec:
  serviceName: "nginx"
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: k8s.gcr.io/nginx-slim:0.8
        ports:
        - containerPort: 80
          name: web
```

Save this as web.yaml and create the StatefulSet with kubectl apply -f web.yaml.

## Step 2: Use a PVC in a StatefulSet

Next, we need to use a Persistent Volume Claim (PVC) in our StatefulSet. Here's how to modify the above manifest to include a PVC:

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: web
spec:
  serviceName: "nginx"
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: k8s.gcr.io/nginx-slim:0.8
        ports:
        - containerPort: 80
          name: web
        volumeMounts:
        - name: www
          mountPath: /usr/share/nginx/html
  volumeClaimTemplates:
  - metadata:
      name: www
    spec:
      accessModes: [ "ReadWriteOnce" ]
      resources:
        requests:
          storage: 1Gi
```

This will create a separate PVC for each replica of our StatefulSet.

## Step 3: Scale it Up/Down

To scale the StatefulSet up or down, you can use the kubectl scale command. For example, to scale up to 5 replicas, you can run: 

```bash
kubectl scale statefulsets web --replicas=5
```

## Step 4: Demonstrate Deletion and The Resulting Storage

Finally, delete the StatefulSet with `kubectl delete -f web.yaml`. 

Note that deleting a StatefulSet will not delete the associated PVCs. You can verify this by running kubectl get pvc after deleting the StatefulSet.

That's it! You've successfully completed the exercise on Kubernetes StatefulSets.
