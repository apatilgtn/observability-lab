# Observability Stack for Local Kubernetes

This repository contains a complete observability stack for local Kubernetes deployments, featuring:

- **Logging**: Fluent Bit + Loki + Grafana
- **Metrics**: Prometheus + Grafana
- **Tracing**: OpenTelemetry Collector + Jaeger
- **Alerting**: Alertmanager

## Prerequisites

- Kubernetes cluster (Minikube, kind, or k3d)
- kubectl
- Helm v3
- Docker

## Quick Start

```bash
# Install the entire stack
./setup.sh

# Access the dashboards
kubectl port-forward svc/grafana 3000:3000 -n monitoring
```

Then open:
- Grafana: http://localhost:3000 (default credentials: admin/admin)
- Jaeger: http://localhost:16686
- Prometheus: http://localhost:9090
- Alertmanager: http://localhost:9093

## Repository Structure

```
observability-lab/
├── logging/          # Logging components
│   ├── loki/         # Log aggregation
│   ├── fluent-bit/   # Log collection
│   └── grafana/      # Visualization for logs
├── metrics/          # Metrics components
│   ├── prometheus/   # Metrics collection & storage
│   └── grafana/      # Visualization for metrics
├── tracing/          # Distributed tracing
│   ├── opentelemetry-collector/  # Telemetry data processing
│   └── jaeger/       # Trace visualization and storage
├── alerts/           # Alerting configuration
│   └── alertmanager/ # Alert routing and notification
├── sample-app/       # Demo application
│   ├── app.py        # Python sample app
│   └── manifests/    # Kubernetes manifests
└── setup.sh          # Installation script
```

## Component Details

Each directory contains:
- Kubernetes manifests (YAML)
- Configuration files
- Installation instructions

## Installation Options

You can install individual components or the entire stack:

```bash
# Install logging stack only
./setup.sh --component logging

# Install metrics stack only
./setup.sh --component metrics

# Install tracing stack only
./setup.sh --component tracing

# Install alerting stack only
./setup.sh --component alerts
```

## Sample Application

A sample Python application is included to demonstrate the observability stack in action. It generates:

- Logs in structured JSON format
- Prometheus metrics
- OpenTelemetry traces

Deploy it with:

```bash
kubectl apply -f sample-app/manifests/
```
