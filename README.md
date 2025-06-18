# SIEM-kubernetes

```
# install the helm chart
cd SIEM-kubernetes
helm install siem .

# upgrade the helm chart
helm upgrade siem .

# uninstall the helm chart (default ns)
helm uninstall siem
```

## Ping Snort
```
# get pods ip address
kubectl get pods -n monitoring
kubectl describe pod -n monitoring snort-<pods-id>
# Or
kubectl get pods -n monitoring -o wide

# ping the pod
kubectl exec -it -n monitoring test-ping -- /bin/sh
/# ping <snort-pod-ip>

# check the logs
kubectl logs -n monitoring snort-<pods-id>
```

## SIEM components

### Falco
- Falco is a cloud-native runtime security tool. It monitors system calls on the host and detects abnormal behavior.
- It identifies suspicious activities like shell executions, file access, or privilege escalation inside containers.
- <b>Why we deployed it:</b>
  - To detect and alert on potential security breaches in real time directly from within the cluster.
### Falco Sidekick
- A small daemon that forwards Falco alerts to multiple output systems (e.g., Slack, Webhook, Loki).
- Transforms Falco alerts and sends them to our logging, visualization, or alerting systems.
- <b>Why we deployed it:</b>
  - To route Falco alerts to downstream services like Loki and Grafana for better visibility and integration.
### Falco Sidekick UI
- A web UI for displaying Falco alerts forwarded by Sidekick.
- Provides a simple dashboard to explore and filter Falco alerts.
- <b>Why we deployed it:</b>
  - To give the SIEM team an easy-to-use interface to view and triage Falco events.
### Grafana
- An open-source dashboard and visualization tool.
- Visualizes metrics from Prometheus, Loki, and other sources in customizable dashboards.
- <b>Why we deployed it:</b>
  - To provide visual insights into logs, metrics, and alerts across the system.
### Kube-State-Metrics
- A service that listens to the Kubernetes API and generates metrics about the state of objects.
- Exports metrics like pod counts, deployment status, etc., to Prometheus.
- <b>Why we deployed it:</b>
  - To monitor the health and state of the Kubernetes cluster from a resource and compliance perspective.
### Loki
- A log aggregation system designed to work like Prometheus but for logs.
- Stores logs from across the cluster and supports querying them via Grafana.
- <b>Why we deployed it:</b>
  - To collect and store logs for forensic analysis and alert correlation in our SIEM.
### Promtail
- An agent that collects logs and ships them to Loki.
- Reads logs from files or containers and adds metadata for querying in Loki.
- <b>Why we deployed it:</b>
  - To send logs from all nodes and pods to Loki for centralized log monitoring.
### Prometheus
- A time-series metrics database and monitoring system.
- Scrapes metrics from various sources and supports alerting rules.
- <b>Why we deployed it:</b>
  - To monitor infrastructure metrics and trigger alerts based on defined thresholds.
### Snort
- An open-source Intrusion Detection and Prevention System (IDS/IPS).
- Monitors network traffic and detects known malicious patterns.
- <b>Why we deployed it:</b>
  - To inspect Kubernetes traffic for intrusions or suspicious behavior.
### Test Ping
- A simple testing pod used to ping services or endpoints.
- <b>Why we deployed it:</b>
  - For quick debugging and validation of cluster networking and service reachability.