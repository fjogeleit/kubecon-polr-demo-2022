# KubeCon EU 2022 - PolicyReport CRD Demo

## Requirement

* Helm

### Install Tools

#### Kyverno, Kyverno Policies & PolicyReport CRDs

```bash
helm upgrade --install kyverno kyverno -n kyverno --create-namespace --repo https://kyverno.github.io/kyverno --version v2.3.2
helm upgrade --install kyverno-policies kyverno-policies -n kyverno --create-namespace --repo https://kyverno.github.io/kyverno --version v2.3.2
```

#### Monitoring: Grafana, Prometheus

```bash
helm upgrade --install monitoring kube-prometheus-stack -n monitoring --create-namespace --repo https://prometheus-community.github.io/helm-charts --version 35.0.3
```

#### Policy Reporter

```bash
helm upgrade --install policy-reporter policy-reporter -n policy-reporter --create-namespace --repo https://kyverno.github.io/policy-reporter --version 2.8.0 -f ./tools/policy-reporter.yaml
```

### Apply PolicyReports: Trivy, Kube-Bench, Falco

```bash
kubectl apply -f ./polr
```

### Accessing Dashboards

#### Grafana Dashboard

Default Login

Username: `admin`
Password: `prom-operator`

```bash
kubectl port-forward service/monitoring-grafana 3000:80 -n monitoring
```

Open: <a href="http://localhost:3000" target="_blank">http://localhost:3000</a>

#### Policy Reporter UI

```bash
kubectl port-forward service/policy-reporter-ui 8082:8080 -n policy-reporter
```

Open: <a href="http://localhost:8082" target="_blank">http://localhost:8082</a>
