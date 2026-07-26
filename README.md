# Monitoring Stack using Prometheus, Node Exporter & Grafana

## Components

- Prometheus
- Node Exporter
- Grafana

## Installation Steps

### 1. Install Prometheus

- Download Prometheus
- Extract
- Create prometheus user
- Configure systemd service
- Start Prometheus

### 2. Install Node Exporter

- Download Node Exporter
- Create node_exporter user
- Configure systemd service
- Start Node Exporter

### 3. Configure Prometheus

Added scrape target:

```yaml
- job_name: "node_exporter"
  static_configs:
    - targets: ["localhost:9100"]
```

### 4. Install Grafana

Install Grafana package

Enable service

Login using:

admin/admin

### 5. Add Prometheus Datasource

URL

```
http://localhost:9090
```

### 6. Import Dashboard

Imported Node Exporter Full Dashboard.

## Result

Successfully monitoring EC2 instance using Grafana.
