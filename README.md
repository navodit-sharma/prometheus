# Prometheus

Prometheus helm chart for Kubernetes. Tool for monitoring health of microservices in a Kubernetes cluster. Helm chart deploys following services.
- Prometheus operator
- Prometheus
- Alertmanager
- Grafana
- Emissary ingress
- Elasticsearch exporter
- Node exporter
## Audience
---
Operations Team
## Prerequisites
---
- Kubernetes 1.16+
- Helm 3+

## Dependencies
---
- Helm charts
  - Kube-prometheus-stack
  - Emissary-ingress
  - Prometheus-elasticsearch-exporter
## Install/Upgrade
---
1. Create namespace
``` bash
kubectl create namespace monitor
```
2. Install CRDs and Emissary-apiext service required by Emissary-Ingress
``` bash
kubectl apply -f https://app.getambassador.io/yaml/emissary/2.3.1/emissary-crds.yaml
kubectl wait --timeout=90s --for=condition=available deployment emissary-apiext -n emissary-system
```
3. Install CRDs required by Prometheus

**Note :** If you are doing a fresh install then chart will automatically create CRDs otherwise do it manually.
``` bash
kubectl apply --server-side -f https://raw.githubusercontent.com/prometheus-operator/prometheus-operator/v0.57.0/example/prometheus-operator-crd/monitoring.coreos.com_alertmanagerconfigs.yaml --force-conflicts
kubectl apply --server-side -f https://raw.githubusercontent.com/prometheus-operator/prometheus-operator/v0.57.0/example/prometheus-operator-crd/monitoring.coreos.com_alertmanagers.yaml --force-conflicts
kubectl apply --server-side -f https://raw.githubusercontent.com/prometheus-operator/prometheus-operator/v0.57.0/example/prometheus-operator-crd/monitoring.coreos.com_podmonitors.yaml --force-conflicts
kubectl apply --server-side -f https://raw.githubusercontent.com/prometheus-operator/prometheus-operator/v0.57.0/example/prometheus-operator-crd/monitoring.coreos.com_probes.yaml --force-conflicts
kubectl apply --server-side -f https://raw.githubusercontent.com/prometheus-operator/prometheus-operator/v0.57.0/example/prometheus-operator-crd/monitoring.coreos.com_prometheuses.yaml --force-conflicts
kubectl apply --server-side -f https://raw.githubusercontent.com/prometheus-operator/prometheus-operator/v0.57.0/example/prometheus-operator-crd/monitoring.coreos.com_prometheusrules.yaml --force-conflicts
kubectl apply --server-side -f https://raw.githubusercontent.com/prometheus-operator/prometheus-operator/v0.57.0/example/prometheus-operator-crd/monitoring.coreos.com_servicemonitors.yaml --force-conflicts
kubectl apply --server-side -f https://raw.githubusercontent.com/prometheus-operator/prometheus-operator/v0.57.0/example/prometheus-operator-crd/monitoring.coreos.com_thanosrulers.yaml --force-conflicts
```
4. Helm install/upgrade
``` bash
helm upgrade --install --cleanup-on-fail --history-max 10 monitor -n monitor -f /path/to/values.yaml /path/to/chart
```
## Uninstall chart
---
Follow below steps to uninstall prometheus completely.
``` bash
# Helm - Uninstall prometheus
helm uninstall monitor

# Kubectl - Remove prometheus CRDs
kubectl delete crd alertmanagerconfigs.monitoring.coreos.com
kubectl delete crd alertmanagers.monitoring.coreos.com
kubectl delete crd podmonitors.monitoring.coreos.com
kubectl delete crd probes.monitoring.coreos.com
kubectl delete crd prometheuses.monitoring.coreos.com
kubectl delete crd prometheusrules.monitoring.coreos.com
kubectl delete crd servicemonitors.monitoring.coreos.com
kubectl delete crd thanosrulers.monitoring.coreos.com

# Kubectl - Remove k8s services created in kube-system namespace
kubectl --namespace kube-system delete svc monitor-prometheus-coredns monitor-prometheus-kubelet

# kubectl - Delete all PVCs used by prometheus
# Note - Deleting PVC means loosing all monitoring data permanently.
kubectl --namespace monitor delete pvc --all
```
