# cloudgeeksca

- https://cloudgeeks.ca

### Robusta

- https://home.robusta.dev/

- EKS CSI driver is not install by default
- https://aws.amazon.com/premiumsupport/knowledge-center/eks-troubleshoot-ebs-volume-mounts/

- Verify that the Amazon EBS CSI driver controller and node pods are running
```
kubectl get all -l app.kubernetes.io/name=aws-ebs-csi-driver -n kube-system
```

- https://github.com/kubernetes-sigs/aws-ebs-csi-driver/blob/master/docs/install.md

- CSI Driver Installation
```
chmod +x csi-driver.sh

bash -uvx csi-driver.sh
```


- export Cluster Name
```
export CLUSTER_NAME='cloudgeeks-eks-dev'
```

- Install Robusta with Helm

- https://docs.robusta.dev/master/installation.html

- Generate generated_values.yaml (Make sure Docker Daemon is running)

```bash
curl -fsSL -o robusta https://docs.robusta.dev/master/_static/robusta

chmod +x robusta

./robusta version

./robusta gen-config

helm repo add robusta https://robusta-charts.storage.googleapis.com && helm repo update

export CLUSTER_NAME='cloudgeeks-eks-dev'

helm upgrade --install \
    robusta robusta/robusta \
    --values generated_values.yaml \
    --namespace monitoring \
    --create-namespace \
    --wait \
    --set clusterName="${CLUSTER_NAME}"
```

- Note: generated_values.yaml is Slack & Robusta UI Account Settings plus BuiltIn Powerful Alerting Rules

- Robusta Official

- values.yaml

- https://github.com/robusta-dev/robusta/blob/master/helm/robusta/values.yaml

- Add Custom Alerting Rules in values-deployment.yaml
```
helm upgrade --install \
    robusta robusta/robusta \
    --values generated_values.yaml \
    --namespace monitoring \
    --create-namespace \
    --wait \
    --set clusterName="${CLUSTER_NAME}" \
    --values values-deployment.yaml
```
- Robusta Demos
- https://github.com/robusta-dev/kubernetes-demos

- Crashing Pods Demo
```crash
kubectl apply -f https://gist.githubusercontent.com/robusta-lab/283609047306dc1f05cf59806ade30b6/raw
```


- Kind Cluster
```kind
chmod +x kind-cluster.sh

bash -uvx kind-cluster.sh
```

- kind Robusta

- export Cluster Name
```
export CLUSTER_NAME='kind-cloudgeeks'
xport KUBECONFIG=~/Desktop/kind/kinde
```


```kind-robusta
helm upgrade --install robusta robusta/robusta -f ./generated_values.yaml \
    --namespace monitoring \
    --create-namespace \
    --wait \
    --set clusterName=${CLUSTER_NAME} \
    --set kube-prometheus-stack.coreDns.enabled=false \
    --set kube-prometheus-stack.kubeControllerManager.enabled=false \
    --set kube-prometheus-stack.kubeDns.enabled=false \
    --set kube-prometheus-stack.kubeEtcd.enabled=false \
    --set kube-prometheus-stack.kubeProxy.enabled=false \
    --set kube-prometheus-stack.kubeScheduler.enabled=false \
    --set kube-prometheus-stack.nodeExporter.enabled=false \
    --set kube-prometheus-stack.prometheusOperator.kubeletService.enabled=false
```

- Kind Custom Values.yaml

```kind-robusta
helm upgrade --install robusta robusta/robusta \
    --values generated_values.yaml \
    --namespace monitoring \
    --create-namespace \
    --set clusterName=${CLUSTER_NAME} \
    --set kube-prometheus-stack.coreDns.enabled=false \
    --set kube-prometheus-stack.kubeControllerManager.enabled=false \
    --set kube-prometheus-stack.kubeDns.enabled=false \
    --set kube-prometheus-stack.kubeEtcd.enabled=false \
    --set kube-prometheus-stack.kubeProxy.enabled=false \
    --set kube-prometheus-stack.kubeScheduler.enabled=false \
    --set kube-prometheus-stack.nodeExporter.enabled=false \
    --set kube-prometheus-stack.prometheusOperator.kubeletService.enabled=false \
    --values values.yaml \
    --wait
```

- kind cluster port forwarding with ssh tunnel
```ssh-tunnel
ssh -N -L 8443:0.0.0.0:8443 -i ~/.ssh/id_rsa cloud_user@<public-ip>

export KUBECONFIG=~/Desktop/kind/kind
```
