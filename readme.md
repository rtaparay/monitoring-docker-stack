# Application Monitoring Stack

### Monitorear Host VM con Grafana y Prometheus en Docker implica configurar los siguientes componentes:

Host VM: La VM de Ubuntu que desea monitorear.

Grafana: una plataforma de seguimiento y observabilidad, credenciales predeterminadas de Grafana (nombre de usuario: admin , contraseña: admin ) , pagina para los dashboards: https://grafana.com/grafana/dashboards/ y los datasource: https://grafana.com/docs/grafana/latest/datasources/

Prometheus: un conjunto de herramientas de seguimiento y alerta,Si realiza algún cambio en el archivo de configuración de Prometheus, puede recargarlo usando un comando como el siguiente , curl -X POST localhost:9090/-/reload ,Puede comprobar si se realizó la última recarga y cuándo apuntando el navegador web a la página /status, por ejemplo http://localhost:9090/status

Node-Exporter: un exportador de Prometheus para métricas del sistema.

AlertManager: maneja las alertas enviadas por aplicaciones cliente como el servidor Prometheus. Se encarga de deduplicarlos, agruparlos y enrutarlos a la integración del receptor correcto, como correo electrónico, PagerDuty u OpsGenie. También se encarga del silenciamiento e inhibición de las alertas.


## Start Prometheus, Grafana & Dashboards

```
docker-compose up -d prometheus
docker-compose up -d grafana
docker-compose up -d grafana-dashboards
docker-compose up -d alertmanager

```

```
docker-compose restart prometheus
docker-compose restart grafana
docker-compose restart grafana-dashboards
docker-compose restart alertmanager
```

## Check Dashboards Grafana

```
http://localhost:3000
user: admin
pass: foobar
```

## Check Dashboards Prometheus
```
http://localhost:9090/alerts
http://localhost:9090/status
curl -X POST localhost:9090/-/reload
```

## Prometheus Queries
### Golang Examples

```
Requests per Second over 2minutes
```
```
irate(go_request_operations_total[2m])
```
```
Request duration
```
```
rate(go_request_duration_seconds_sum[2m]) / rate(go_request_duration_seconds_total[2m])
```
## Check Dashboards Node-Exporter
```
http://localhost:9100/metrics
```

## Check Dashboards Alertmanager
```
http://localhost:9093
```