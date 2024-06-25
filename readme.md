# Prometheus Application Monitoring


## Monitorear Host VM con Grafana y Prometheus en Docker implica configurar los siguientes componentes:

Host VM: La VM de Ubuntu que desea monitorear.

Prometheus: un conjunto de herramientas de seguimiento y alerta the port 9090
http://localhost:9090/alerts

Grafana: una plataforma de seguimiento y observabilidad port 3000
credenciales predeterminadas de Grafana (nombre de usuario: admin , contraseña: admin )
https://grafana.com/grafana/dashboards/10532-azure-virtual-machine/
https://grafana.com/grafana/dashboards/617-aws-ec2/

Exportador de nodos (opcional): un exportador de Prometheus para métricas del sistema.  port 9100
http://localhost:9090/targets

AlertManager:
Open http://localhost:9093 in your browser to see the Alertmanager UI.
https://medium.com/javarevisited/monitoring-setup-with-docker-compose-part-3-alertmanager-5d0a2d4a5612


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

## Check Dashboards

```
http://localhost:3000
```

## Prometheus Queries
### Golang Examples

Requests per Second over 2minutes
```
irate(go_request_operations_total[2m])
```
Request duration
```
rate(go_request_duration_seconds_sum[2m]) / rate(go_request_duration_seconds_total[2m])
```

