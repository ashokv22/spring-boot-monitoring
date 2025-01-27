# Spring Boot Observability with Prometheus, Promtail, and Loki

## Overview
This scripts contains the integration of monitoring tools Prometheus, Promtail, and Loki for observability and Application Performance Management (APM) in a Spring Boot application. The setup allows you to monitor metrics, logs, and application performance efficiently.

## Steps
### Step 1: Pull Grafana
```shell
sudo docker run -d -p 3000:3000 grafana/grafana
```

### Step 2: Push prometheus.yaml by setting the system Ip and pull Prometheus
```shell
sudo docker run -d -p 9090:9090 -v /vol/software/dcb_test/application/config/new/prometheus.yaml:/etc/prometheus/prometheus.yml prom/prometheus
```

### Step 3: Pull Promtail with name, port and config
```shell
sudo docker run -d --name promtail -p 9080:9080 -v /vol/software/dcb_test/application/config/new/promtail-config.yaml:/etc/promtail/promtail.yaml grafana/promtail:latest
```

### Step 4: Pull Loki with deafult config
```shell
sudo docker run --name loki -d -v $(pwd):/mnt/config -p 3100:3100 grafana/loki:2.9.1 -config.file=/mnt/config/loki-config.yaml
```