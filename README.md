# Prometheus and Grafana Monitoring Dashboard

## Project Overview

This project demonstrates how to set up a basic monitoring system using **Prometheus, Grafana, and Docker Compose**.

Prometheus collects monitoring metrics, while Grafana displays the collected data through interactive dashboards.

The project was implemented and tested locally on Windows using Docker Desktop.

## Technologies Used

- Docker and Docker Compose
- Prometheus
- Grafana
- YAML
- Windows PowerShell
- Visual Studio Code

## Project Architecture

```text
Docker Desktop
     |
     |-- Prometheus (Port 9090)
     |       |
     |       |-- Collects Prometheus metrics
     |       |-- Monitors target availability
     |
     |-- Grafana (Port 3000)
             |
             |-- Connects to Prometheus
             |-- Displays monitoring dashboards
```

## Implementation Steps

1. Created the `prometheus.yml` configuration file to define the monitoring target.
2. Created `docker-compose.yml` to configure Prometheus and Grafana containers.
3. Started both services using Docker Compose.
4. Verified that Prometheus was successfully scraping its target.
5. Connected Grafana to Prometheus as a data source.
6. Created and saved a monitoring dashboard with three panels.
7. Verified the health of both services using their HTTP health endpoints.

## Monitoring Dashboard

The Grafana dashboard contains three panels:

| Panel | Prometheus Query | Purpose |
|---|---|---|
| Prometheus Target Health | `up` | Checks whether the monitored target is reachable |
| Prometheus Samples Ingested | `prometheus_tsdb_head_samples_appended_total` | Displays samples appended to the time-series database |
| Prometheus HTTP Requests | `prometheus_http_requests_total` | Tracks HTTP requests handled by Prometheus |

## How to Run the Project

### Prerequisites

Install Docker Desktop with Docker Compose.

### Start the Monitoring Stack

Open a terminal inside the project directory and run:

```bash
docker compose up -d
```

Check the running containers:

```bash
docker compose ps
```

### Access the Services

- Prometheus: http://localhost:9090
- Grafana: http://localhost:3000

In Grafana, configure a Prometheus data source with the following URL:

```text
http://prometheus:9090
```

Import the included Grafana dashboard JSON file to recreate the monitoring dashboard.

## Verification

The monitoring setup was successfully tested.

**Prometheus target availability:**

```promql
up
```

Result: `1` (target UP)

**Prometheus health check:**

```bash
curl.exe http://localhost:9090/-/healthy
```

Result:

```text
Prometheus Server is Healthy.
```

**Grafana health check:**

```bash
curl.exe http://localhost:3000/api/health
```

Result included:

```json
{
  "database": "ok",
  "version": "13.2.3"
}
```

## Project Outcome

Successfully deployed a containerized monitoring stack, configured Prometheus metric collection, integrated Grafana, created three monitoring visualizations, and verified that both services were healthy.

This project demonstrates hands-on experience with Docker Compose, monitoring, metrics collection, and Grafana dashboard configuration.