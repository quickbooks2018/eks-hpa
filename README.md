# cloudgeeksca

- https://cloudgeeks.ca

### Horizantl Pod Autoscaler

- STEP 1: Create a Metrics Server

```bash
kubectl apply -R -f metrics-server/
```

- HPA (Horizontal Pod Autoscaler) is a Kubernetes resource that allows you to automatically scale the number of pods in a replication controller, deployment, replica set or stateful set based on observed CPU utilization (or, with custom metrics support, on some other application-provided metrics).
```bash
kubectl get hpa -n default
```

- Metrics Server is a cluster-wide aggregator of resource usage data. Metrics Server collects metrics from Summary API exposed by Kubelet on each node.
```bash
kubectl get deployment metrics-server -n kube-system
```

- Metrics logs of metrics-server
```bash
kubectl logs -f deployment/metrics-server -n kube-system
```

- TOP PODS
```bash
kubectl top pods -n default
```

- Load Testing
```bash
curl 
```