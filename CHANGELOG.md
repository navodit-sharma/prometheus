# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]
## [4.0.6]
### Fixed
- Alertmanager config typo fix
### Changed
- Schema validation Off
## [4.0.5]
### Fixed
- Alertmanager route fixed
- Auto discovery of service monitors
## [4.0.4]
### Added
- Postgres monitoring (exporter and dashboard)
### Changed
- Grafana dashboard are only created when grafana is enabled

## [4.0.3]
### Fixed
- Alert rules config updated
### Added
- Support for slack notifications
## [4.0.2]
---
### Fixed
- Grafana secret config fix
## [4.0.1]
---
### Fixed
- Alertmanager secret config fix
## [4.0.0]
---
### Changed
- Kube-prometheus-stack **32.2.1 &#8594; 36.2.0**.
- Emissary Ingress **7.3.0 &#8594;  7.4.1**.
- Elasticsearch exporter **4.3.0 &#8594; 4.13.0**.
- ESO support for grafana and alertmanager secrets
- New dashboards for Alert notification
### Fixed
- Changelog now contains all missing information.
- Fixed missing data in dashboards
- Improved some dashboards
### Migrate
- Kube-prometheus-stack - CRDs should be updated before 'helm upgrade'
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
- Emissary - CRDs should be updated before 'helm upgrade'
``` bash
kubectl apply -f https://app.getambassador.io/yaml/emissary/2.3.1/emissary-crds.yaml
```
## [3.0.3]
---
### Added
- ESO support added
## [3.0.2]
---
### Changed
- Emissary, removed office IP of Petrozavodsk from whitelist.
### Fixed
- Node-exporter, relabling configs corrected.
## [3.0.1]
---
### Fixed
- Some of the `Alerts` dashboard metrics were missing because of datasource issues, now those metrics are available.
## [3.0.0]
---
### Changed
- Kube-prometheus-stack **18.0.1 &#8594; 32.2.1**.
- Some of the alerts were renamed.
- Alertmanager config updated.
- Dashboards updated.
### Migrate
- Kube-prometheus-stack - CRDs should be updated before 'helm upgrade'
``` bash
kubectl apply --server-side -f https://raw.githubusercontent.com/prometheus-operator/prometheus-operator/v0.54.0/example/prometheus-operator-crd/monitoring.coreos.com_alertmanagerconfigs.yaml --force-conflicts
kubectl apply --server-side -f https://raw.githubusercontent.com/prometheus-operator/prometheus-operator/v0.54.0/example/prometheus-operator-crd/monitoring.coreos.com_alertmanagers.yaml --force-conflicts
kubectl apply --server-side -f https://raw.githubusercontent.com/prometheus-operator/prometheus-operator/v0.54.0/example/prometheus-operator-crd/monitoring.coreos.com_podmonitors.yaml --force-conflicts
kubectl apply --server-side -f https://raw.githubusercontent.com/prometheus-operator/prometheus-operator/v0.54.0/example/prometheus-operator-crd/monitoring.coreos.com_probes.yaml --force-conflicts
kubectl apply --server-side -f https://raw.githubusercontent.com/prometheus-operator/prometheus-operator/v0.54.0/example/prometheus-operator-crd/monitoring.coreos.com_prometheuses.yaml --force-conflicts
kubectl apply --server-side -f https://raw.githubusercontent.com/prometheus-operator/prometheus-operator/v0.54.0/example/prometheus-operator-crd/monitoring.coreos.com_prometheusrules.yaml --force-conflicts
kubectl apply --server-side -f https://raw.githubusercontent.com/prometheus-operator/prometheus-operator/v0.54.0/example/prometheus-operator-crd/monitoring.coreos.com_servicemonitors.yaml --force-conflicts
kubectl apply --server-side -f https://raw.githubusercontent.com/prometheus-operator/prometheus-operator/v0.54.0/example/prometheus-operator-crd/monitoring.coreos.com_thanosrulers.yaml --force-conflicts
```
## [2.1.1]
---
### Added
- Emissary-ingress chart **7.2.0 &#8594; 7.3.0**.
### Migrate
- Emissary - CRDs should be updated before 'helm upgrade'
``` bash
kubectl apply -f https://app.getambassador.io/yaml/emissary/2.2.2/emissary-crds.yaml
```
## [2.1.0]
---
### Added
- Emissary-ingress (7.2.0)
### Changed
- Value global.externalUrl was renamed to global.externalDomain.
- Support of old cert-manager api was removed.
- Value emissary-ingress.module was renamed to emissary-ingress.customModule. That was done because emissary-ingress chart contains creation of module if value emissary-ingress.module not empty.
### Removed
- Ambassador (6.5.0). The ambassador chart is deprecated. That chart cannot be used with k8s 1.22.x and higher. It has been replaced with Emissary-ingress.
### Migrate
- Emissary - CRDs should be updated before 'helm upgrade'
``` bash
kubectl apply -f https://app.getambassador.io/yaml/emissary/2.1.2/emissary-crds.yaml
```
## [2.0.4]
---
### Added
- Installation of alert rules can be controlled during chart install or update using below property
``` bash
customResources:
  prometheusCustomAlertRules:
    create: true|false
    rules:
      apiserver: true|false
      container: true|false
      daemonset: true|false
      deployment: true|false
      elasticsearch: true|false
      jobs: true|false
      kafka: true|false
      node: true|false
      persistent-volumes: true|false
      pod: true|false
      prometheus: true|false
      replicaset: true|false
      statefulset: true|false
```
## [2.0.3]
---
### Changed
- Schema validation logic updated.
- Ambassador custom templates and default chart values updated.
## [2.0.2]
---
### Changed
- Dashboards updated.
- Alert rules updated.
- Removed all `additionalServiceMonitors` from base chart and added to separate file `additional-servicemonitors.yaml` for reference. File can still be used explicitely during installation of chart.
## [2.0.1]
---
### Changed
- Dashboards improved.
- PrometheusTargetMissing alerts disabled.
## [2.0.0]
---
### Added
- Dashboards are now deployed as configmaps.
- More automated alerts added.
- More dashboards added.
### Changed
- Kube-prometheus-stack **14.0.1 &#8594; 18.0.1**.
## [1.0.0]
---
### Added
- Helm charts
  - Prometheus
  - Alertmanager
  - Grafana
  - Ambassador
  - Elasticsearch exporter
- Automated alerts
  - Disk monitoring
- IP based restrictions
  - Service is only accessible from Whitelisted IPs (not applicable in case of LetsEncrypt certificates)
- Dashboards
  - All default dashboards
  - Custom dashboard(s)
    - Persistent volumes
- TLS support
  - LetsEncrypt (IP restriction not supported)
  - Self-signed or TLS certificate from CA as external k8s secret
  - TLS certificate from Azure key vault
