
# Lokaler Monitoring Stack

## Versionen (anpassen bei Bedarf)

```bash
PROMETHEUS_VERSION=3.5.0
BLACKBOX_VERSION=0.27.0
GRAFANA_VERSION=12.1.1
```

## Lokale Installation und Start (Debian)

### 1. Prometheus herunterladen und entpacken
```bash
wget https://github.com/prometheus/prometheus/releases/latest/download/prometheus-${PROMETHEUS_VERSION}.linux-amd64.tar.gz
tar -xzf prometheus-${PROMETHEUS_VERSION}.linux-amd64.tar.gz
cd prometheus-${PROMETHEUS_VERSION}.linux-amd64
cp ../prometheus.yml .
cp -r ../scrapeconfigs .
cd ..
```

### 2. Blackbox Exporter herunterladen und entpacken
```bash
wget https://github.com/prometheus/blackbox_exporter/releases/latest/download/blackbox_exporter-${BLACKBOX_VERSION}.linux-amd64.tar.gz
tar -xzf blackbox_exporter-${BLACKBOX_VERSION}.linux-amd64.tar.gz
cd blackbox_exporter-${BLACKBOX_VERSION}.linux-amd64
cp ../blackbox.yml .
cp ../web.yml .
cd ..
```

### 3. Grafana herunterladen und entpacken
```bash
wget https://dl.grafana.com/oss/release/grafana-${GRAFANA_VERSION}.linux-amd64.tar.gz
tar -xzf grafana-${GRAFANA_VERSION}.linux-amd64.tar.gz
cd grafana-${GRAFANA_VERSION}
cd ..
```

### 4. Konfigurationen übernehmen
Das Dashboard-JSON (`Blackbox Exporter Dashboard.json`) kann in Grafana importiert werden.

### 5. Dienste starten

**Prometheus:**
```bash
cd prometheus-${PROMETHEUS_VERSION}.linux-amd64
./prometheus --config.file=prometheus.yml &
```

**Blackbox Exporter:**
```bash
cd blackbox_exporter-${BLACKBOX_VERSION}.linux-amd64
./blackbox_exporter --config.file=blackbox.yml --web.config=web.yml &
```

**Grafana:**
```bash
cd grafana-${GRAFANA_VERSION}
./bin/grafana-server web &
```

## Service urls
- Grafana: http://localhost:9090/
- Prometheus: http://localhost:3000/

---

## Start mit Docker Compose

Mit Docker Compose lassen sich alle Services einfach als Container starten. Die benötigte Konfiguration befindet sich in der Datei `docker-compose.yml` im Projektverzeichnis.

**Starten:**
```bash
docker compose up
```

Das Dashboard-JSON kann wie gewohnt in Grafana importiert werden.

---
Weitere Infos: Siehe offizielle Doku von [Prometheus](https://prometheus.io/docs/introduction/overview/), [Blackbox Exporter](https://github.com/prometheus/blackbox_exporter) und [Grafana](https://grafana.com/docs/).
