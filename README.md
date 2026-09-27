# Kubernetes Application Monitoring with Prometheus & Grafana

A simple monitoring setup for a containerized application running on Kubernetes, using Prometheus to collect metrics and Grafana to visualize them.

## Overview

This project deploys an application to a Kubernetes cluster and sets up Prometheus and Grafana to monitor its health and resource usage — CPU, memory, and pod status — in real time.

## Tech Stack

- **Kubernetes** – Deployments, Services
- **Docker** – application containerization
- **Prometheus** – metrics collection
- **Grafana** – dashboards and visualization

## Architecture

```
┌─────────────┐       ┌────────────┐       ┌─────────┐
│ Application │──────▶│ Prometheus │──────▶│ Grafana │
│  (K8s Pods) │ scrape│  (metrics) │ query │(dashboard)│
└─────────────┘       └────────────┘       └─────────┘
```

## What's in this repo

```
.
├── k8s/
│   ├── deployment.yaml       # Application Deployment
│   ├── service.yaml          # Application Service
│   ├── prometheus/
│   │   ├── deployment.yaml   # Prometheus Deployment
│   │   ├── service.yaml
│   │   └── config.yaml       # prometheus.yml scrape config
│   └── grafana/
│       ├── deployment.yaml   # Grafana Deployment
│       └── service.yaml
├── dashboards/
│   └── app-dashboard.json    # Exported Grafana dashboard
├── screenshots/
│   ├── grafana-dashboard.png
│   └── prometheus-targets.png
└── README.md
```

## Setup

1. **Deploy the application**
   ```bash
   kubectl apply -f k8s/deployment.yaml
   kubectl apply -f k8s/service.yaml
   ```

2. **Deploy Prometheus**
   ```bash
   kubectl apply -f k8s/prometheus/
   ```
   Prometheus is configured to scrape metrics from the application and cluster nodes.

3. **Deploy Grafana**
   ```bash
   kubectl apply -f k8s/grafana/
   ```
   Add Prometheus as a data source in Grafana, then import `dashboards/app-dashboard.json`.

4. **Access the dashboards**
   ```bash
   kubectl port-forward svc/grafana 3000:3000
   ```
   Open `http://localhost:3000` and log in to view the dashboard.

## What's monitored

- CPU and memory usage per pod
- Pod health / restart count
- Cluster-level resource usage


