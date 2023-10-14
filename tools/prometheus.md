# Prometheus


## Build Information

```
curl http://localhost:9090/api/v1/status/buildinfo
```

```
/bin/prometheus --config.file=/etc/prometheus/prometheus.yml \
--storage.tsdb.path=/prometheus \
--storage.tsdb.retention.time=1y' \
--web.console.libraries=/usr/share/prometheus/console_libraries \
--web.console.templates=/usr/share/prometheus/consoles \
--web.enable-admin-api
```