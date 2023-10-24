# Kubernetes Network Policies Exercise

## Objective

This exercise will guide you through the process of creating a NetworkPolicy from a manifest, demonstrating a connection, denying a connection, removing the NetworkPolicy, and observing the outcome.

## Step 1. Create a NetworkPolicy from Manifest

First, we need to create a NetworkPolicy. This is done by applying a manifest file which describes the policy. Here's an example of how to do it:

```yaml
cat <<EOF > network-policy.yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: test-network-policy
spec:
  podSelector:
    matchLabels:
      role: db
  policyTypes:
  - Ingress
  ingress:
  - from:
    - ipBlock:
        cidr: 172.17.0.0/16
        except:
        - 172.17.1.0/24
    ports:
    - protocol: TCP
      port: 6379
EOF
```

Now we need to apply the NetworkPolicy with the following command.

```bash
kubectl apply -f network-policy.yaml
```

## Step 2. Demonstrate the Connection

Next, we need to demonstrate that the connection is allowed by the NetworkPolicy. We can do this by creating a Pod that matches the role: db label and trying to connect to it:

```bash
kubectl run db-pod --image=redis --labels=role=db --restart=Never --port=6379
```

Now create another Pod to test the connection.

```bash
kubectl run test-pod --image=busybox --restart=Never --rm -it -- wget -qO- http://db-pod.default.svc.cluster.local:6379
```

## Step 3. Demonstrate Denying Connection

Now, let's demonstrate that the connection is denied when it does not meet the criteria specified in the NetworkPolicy. We will do this by creating another Pod with a different IP (e.g., 172.17.1.5) to test the connection

```bash
kubectl run denied-pod --image=busybox --restart=Never --rm -it -- wget -qO- http://db-pod.default.svc.cluster.local:6379
```

You should see that the connection fails because the denied-pod does not meet the criteria specified in the test-network-policy.

## Step 4. Remove the NetworkPolicy and See the Outcome

Finally, let's remove the NetworkPolicy and observe that the previously denied Pod can now connect:

```bash
kubectl delete networkpolicy test-network-policy
```

Now try to connect from the denied Pod again:

```bash
kubectl run denied-pod --image=busybox --restart=Never --rm -it -- wget -qO- http://db-pod.default.svc.cluster.local:6379
```

You should see that the connection is now successful because the test-network-policy no longer exists.

## Conclusion

In this exercise, you have learned how to create a NetworkPolicy from a manifest, demonstrate connections, deny connections based on policy rules, remove a NetworkPolicy, and observe its impact on connections. This knowledge is crucial for managing network access in Kubernetes.
