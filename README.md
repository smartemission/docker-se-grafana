# docker-se-grafana

Grafana viewer for Calibration-related and AirSensEUR 
data from InfluxDB. Fully functional:
Includes Datasource and Dashboard definitions.

## Hosting

The Docker Image is hosted as: [smartemission/se-grafana at DockerHub](https://hub.docker.com/r/smartemission/se-grafana).

## Environment

The following environment vars need to be set, 
either via `docker-compose` or
Kubernetes.


|Environment variable|
|---|
|GF_SECURITY_ADMIN_PASSWORD|
|SE_INFLUX_ADMIN_USER|
|SE_INFLUX_ADMIN_PASSWORD|
|GF_SERVER_ROOT_URL=%(protocol)s://%(domain)s:%(http_port)s/grafana|

## Architecture

This Image uses the standard Grafana Docker Image, mainly 
adding "Provisioning" (as in Grafana v5+) files for Datasources (InfluxDB) and
Dashboards. The [entry.sh](entry.sh) script will perform
some magic to substitute credentials from environment vars.
It then calls the standard Grafana `/run.sh` script.
