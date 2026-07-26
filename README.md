# AWS EC2 Monitoring using Prometheus, Node Exporter and Grafana

This project demonstrates how to monitor an AWS EC2 Ubuntu instance using **Prometheus**, **Node Exporter**, and **Grafana**. The monitoring stack collects system metrics such as CPU, Memory, Disk, Network, and displays them in Grafana dashboards.

---

# Project Architecture

EC2 Instance
│
├── Prometheus (Port 9090)
│ └── Scrapes metrics
│
├── Node Exporter (Port 9100)
│ └── Exposes Linux system metrics
│
└── Grafana (Port 3000)
└── Visualizes metrics from Prometheus

---

# Tech Stack

- AWS EC2 (Ubuntu)
- Prometheus
- Node Exporter
- Grafana
- Linux Systemd Services

---

# Project Files

| File | Description |
|------|-------------|
| prometheus.yml | Prometheus configuration |
| prometheus.service | Prometheus systemd service |
| node_exporter.service | Node Exporter systemd service |
| commands.txt | Installation commands used |
| README.md | Project documentation |
| Screenshot/ | Project screenshots |

---

# Installation Steps

## 1. Launch AWS EC2 Ubuntu Instance

- Create Ubuntu EC2 instance
- Allow inbound ports:
  - 22 (SSH)
  - 3000 (Grafana)
  - 9090 (Prometheus)
  - 9100 (Node Exporter)

---

## 2. Install Prometheus

Download Prometheus

```bash
wget https://github.com/prometheus/prometheus/releases/download/v3.5.0/prometheus-3.5.0.linux-amd64.tar.gz
```

Extract

```bash
tar -xvf prometheus-3.5.0.linux-amd64.tar.gz
```

Create Prometheus user

```bash
sudo useradd --no-create-home --shell /bin/false prometheus
```

Copy binaries

```bash
sudo cp prometheus promtool /usr/local/bin/
```

Create directories

```bash
sudo mkdir /etc/prometheus
sudo mkdir /var/lib/prometheus
```

Copy configuration

```bash
sudo cp prometheus.yml /etc/prometheus/
```

Create Prometheus service

```bash
sudo nano /etc/systemd/system/prometheus.service
```

Enable service

```bash
sudo systemctl daemon-reload
sudo systemctl enable prometheus
sudo systemctl start prometheus
```

Check status

```bash
sudo systemctl status prometheus
```

---

## 3. Install Node Exporter

Download

```bash
wget https://github.com/prometheus/node_exporter/releases/download/v1.9.1/node_exporter-1.9.1.linux-amd64.tar.gz
```

Extract

```bash
tar -xvf node_exporter-1.9.1.linux-amd64.tar.gz
```

Create user

```bash
sudo useradd --no-create-home --shell /bin/false node_exporter
```

Copy binary

```bash
sudo cp node_exporter /usr/local/bin/
```

Create service

```bash
sudo nano /etc/systemd/system/node_exporter.service
```

Enable service

```bash
sudo systemctl daemon-reload
sudo systemctl enable node_exporter
sudo systemctl start node_exporter
```

Check status

```bash
sudo systemctl status node_exporter
```

---

## 4. Configure Prometheus

Edit configuration

```bash
sudo nano /etc/prometheus/prometheus.yml
```

Configuration

```yaml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

scrape_configs:
  - job_name: "prometheus"
    static_configs:
      - targets:
          - localhost:9090

  - job_name: "node_exporter"
    static_configs:
      - targets:
          - localhost:9100
```

Validate

```bash
promtool check config /etc/prometheus/prometheus.yml
```

Restart

```bash
sudo systemctl restart prometheus
```

---

## 5. Install Grafana

Install package

```bash
sudo apt install grafana-enterprise
```

Enable

```bash
sudo systemctl daemon-reload
sudo systemctl enable grafana-server
sudo systemctl start grafana-server
```

Check

```bash
sudo systemctl status grafana-server
```

---

## 6. Configure Grafana

Open browser

```
http://<EC2-PUBLIC-IP>:3000
```

Default Login

Username

```
admin
```

Password

```
admin
```

Change password after first login.

---

## 7. Add Prometheus Data Source

Connections

↓

Data Sources

↓

Prometheus

URL

```
http://localhost:9090
```

Click

```
Save & Test
```

---

## 8. Import Dashboard

Import Dashboard ID

```
1860
```

Select

```
Prometheus Datasource
```

Import

Dashboard displays

- CPU Usage
- Memory Usage
- Disk Usage
- Filesystem
- Network Traffic
- System Load
- Processes

---

# Services

Prometheus

```bash
sudo systemctl status prometheus
```

Node Exporter

```bash
sudo systemctl status node_exporter
```

Grafana

```bash
sudo systemctl status grafana-server
```

---

# Ports Used

| Service | Port |
|---------|------|
| Grafana | 3000 |
| Prometheus | 9090 |
| Node Exporter | 9100 |
| SSH | 22 |

---

# Screenshots

Add these screenshots inside the **Screenshot** folder.

1. EC2 Instance Created
2. SSH Connection
3. Prometheus Running
4. Node Exporter Running
5. Grafana Service Running
6. Grafana Login Page
7. Prometheus Datasource Connected
8. Final Monitoring Dashboard

---

# Result

Successfully deployed a complete monitoring stack on AWS EC2 using:

- Prometheus
- Node Exporter
- Grafana

The dashboard continuously monitors CPU, Memory, Disk, Network, Filesystem, and other Linux system metrics in real time.

---

# Author

**Yuvanbala Viswanathan**

GitHub:
https://github.com/yuvanbalaviswanathan-dev
