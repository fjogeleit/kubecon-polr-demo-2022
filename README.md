# KubeCon EU 2022 - PolicyReport CRD Demo

## Requirement

* Helm

## Prepare Namespaces

```bash
kubectl apply -f ./namespaces
```

## Install Tools

### Kyverno, Prometheus, Grafana, Policy Reporter

```bash
helm upgrade --install policy-reporter-demo ./policy-reporter-demo -n policy-reporter --create-namespace
```

### Kyverno Policies

```bash
helm upgrade --install kyverno-policies kyverno-policies -n kyverno --create-namespace --repo https://kyverno.github.io/kyverno --version v2.4.0 --set podSecurityStandard=restricted
```

## Adapter PolicyReports: Trivy, Kube-Bench, Falco

```bash
kubectl apply -f ./polr
```

## Accessing Dashboards

### Grafana Dashboard

Default Login

Username: `admin`
Password: `prom-operator`

```bash
kubectl port-forward service/policy-reporter-demo-grafana 3000:80 -n monitoring
```

Open: <a href="http://localhost:3000" target="_blank">http://localhost:3000</a>

### Policy Reporter UI

```bash
kubectl port-forward service/policy-reporter-demo-ui 8082:8080 -n policy-reporter
```

Open: <a href="http://localhost:8082" target="_blank">http://localhost:8082</a>

## Screenshots

![PolicyReporter Grafana Dashboard](https://github.com/fjogeleit/kubecon-polr-demo-2022/blob/main/screens/grafana.png?raw=true)

![PolicyReporter UI Dashboard](https://github.com/fjogeleit/kubecon-polr-demo-2022/blob/main/screens/policy-reporter-ui.png?raw=true)
