# docker-se-grafana

Grafana viewer for Calibration-related and AirSensEUR 
data from InfluxDB. Fully functional:
Includes Datasource and Dashboard definitions.

## Hosting

The Docker Image is hosted as: [smartemission/se-grafana at DockerHub](https://hub.docker.com/r/smartemission/se-grafana).

## Environment

The following environment vars need to be set,  either via `docker-compose` or Kubernetes.


Variable|Meaning |Example
---|---|--- 
`GF_SECURITY_ADMIN_USER`|Grafana admin username|secret
`GF_SECURITY_ADMIN_PASSWORD`|Grafana admin password|secret
`SE_INFLUX_URL`|full URL InfluxDB endpoint|`http://influxdb:8086`
`SE_INFLUX_ADMIN_USER`|InfluxDB admin user name|secret
`SE_INFLUX_ADMIN_PASSWORD`|InfluxDB admin user passwd|secret
`GF_SERVER_ROOT_URL`|external URL Grafana Web App|`%(protocol)s://%(domain)s:%(http_port)s/grafana`

Other Grafana variables can be set at will according to the Grafana-scheme that follows
the `Grafana .ini` file format: `GF_<.ini section name>_<varname>`, all in capitals.

## Architecture

This Image uses the standard Grafana Docker Image, mainly 
adding "Provisioning" (as in Grafana v5+) files for Datasources (InfluxDB) and
Dashboards. The [entry.sh](entry.sh) script will perform
some magic to substitute credentials from environment vars.
It then calls the standard Grafana `/run.sh` script.
