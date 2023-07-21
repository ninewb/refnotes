# Grafana

```
(
  instance:node_cpu_utilisation:rate5m{job="node-exporter", instance=~"$instance"}
*
  instance:node_num_cpu:sum{job="node-exporter", instance=~"$instance"}
/ ignoring (instance) group_left
  sum without (instance) (instance:node_num_cpu:sum{job="node-exporter", instance=~"$instance"})
)
```

```
(
node_cpu_seconds_total{job="node-exporter", instance=~"$instance",mode!='idle'}
)
```