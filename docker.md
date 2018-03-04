# Docker scripts regarding BrainFlux

## Install Docker on Debian

```bash
sudo apt-get install \
     apt-transport-https \
     ca-certificates curl gnupg2 \
     software-properties-common

curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | sudo apt-key add -

sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
   $(lsb_release -cs) \
   stable"

sudo apt-get update
sudo apt-get install docker-ce -y
```

## Running

Get start doing stuff! All latest version as on **2018/03/04**.

### InfluxDB

```bash
docker run -td -p 8086:8086 -p 2003:2003 \
-v /home/tonyz/share/Docker/influxdb/config/influxdb.conf:/etc/influxdb/influxdb.conf:ro \
-v /home/tonyz/share/Docker/influxdb/data:/var/lib/influxdb influxdb:1.4.3-alpine
```

### Grafana

```bash
docker run -td -v /home/tonyz/share/Docker/grafana/data:/var/lib/grafana \
-e GF_AUTH_ANONYMOUS_ENABLED=true -e GF_AUTH_ANONYMOUS_ORG_NAME=UPMC -e GF_AUTH_ANONYMOUS_ORG_ROLE=anyone \
-p 13000:3000 grafana/grafana:master
```

### Chronograf

```bash
docker run -td -p 8888:8888 \
-v /home/tonyz/share/Docker/chronograf/data:/var/lib/chronograf \
chronograf:1.4.2.1-alpine
```

### Kapacitor

```bash
docker run -td -p 9092:9092 \
-v /home/tonyz/share/Docker/kapacitor/kapacitor.conf:/etc/kapacitor/kapacitor.conf:ro \
-v /home/tonyz/share/Docker/kapacitor/data:/var/lib/kapacitor \
kapacitor:1.4.0-alpine
```

## Init

Initialize only.

### InfluxDB-init

Base directory: `mkdir -p /home/tonyz/share/Docker/influxdb`

```bash
docker run --rm \
-e INFLUXDB_DB=db0 -e INFLUXDB_ADMIN_ENABLED=true \
-e INFLUXDB_ADMIN_USER=admin -e INFLUXDB_ADMIN_PASSWORD=admin_pwd \
-e INFLUXDB_USER=telegraf -e INFLUXDB_USER_PASSWORD=telegraf_pwd \
-v /home/tonyz/share/Docker/influxdb/data:/var/lib/influxdb \
influxdb:1.4.3-alpine /init-influxdb.sh
```

### Grafana-init

Install some basic plugins. Base directory: `mkdir -p /home/tonyz/share/Docker/grafana`

```bash
docker run -td -v /home/tonyz/share/Docker/grafana/data:/var/lib/grafana \
-e "GF_INSTALL_PLUGINS=grafana-clock-panel,natel-influx-admin-panel,natel-plotly-panel,natel-discrete-panel,novalabs-annotations-panel,jdbranham-diagram-panel" \
-e GF_AUTH_ANONYMOUS_ENABLED=true -e GF_AUTH_ANONYMOUS_ORG_NAME=UPMC -e GF_AUTH_ANONYMOUS_ORG_ROLE=anyone \
-p 13000:3000 grafana/grafana:master
```

### Chronograf

Base directory: `mkdir -p /home/tonyz/share/Docker/chronograf`
