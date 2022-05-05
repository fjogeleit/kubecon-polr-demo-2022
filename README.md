# KubeCon EU 2022 - PolicyReport CRD Demo

## Requirement

* Helm

### Tools

#### Kyverno, Kyverno Policies & PolicyReport CRDs

```bash
helm install kyverno kyverno -n kyverno --create-namespace --repo https://kyverno.github.io/kyverno --version v2.3.2
helm install kyverno-policies kyverno-policies -n kyverno --create-namespace --repo https://kyverno.github.io/kyverno --version v2.3.2
```

#### PolicyReports: Trivy, Kube-Bench, Falco
```bash
kubectl apply -f ./polr
```

#### Monitoring: Grafana, Prometheus

```bash
helm install monitoring kube-prometheus-stack -n monitoring --create-namespace --repo https://prometheus-community.github.io/helm-charts --version 35.0.3
```

#### Policy Reporter

```bash
helm install policy-reporter policy-reporter -n policy-reporter --create-namespace --repo https://kyverno.github.io/policy-reporter --version 2.8.0 -f ./tools/policy-reporter.yaml
```
