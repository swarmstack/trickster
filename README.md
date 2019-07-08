# swarmstack/trickster

Docker compose file for Trickster, Open Source Dashboard Accelerator for Time Series Databases. Requires Docker swarm.

See [https://github.com/Comcast/trickster](https://github.com/Comcast/trickster) for more details.

## INSTALLATION

```
cd /usr/local/src
github clone https://github.com/swarmstack/trickster
cd trickster
```

## USAGE

```
docker stack deploy -c docker-compose.yml trickster
```

[swarmstack](https://github.com/swarmstack/swarmstack) users should use docker-compose-swarmstack.yml above instead.

---

Log into Grafana as an administrator and choose the "Configuration > Data Sources" tab, note the current "default" data-source, and then "Add data source". Choose "Prometheus" as the data source type, as Trickster also implements the Promethus HTTP APIv1. Set the "Name" to Trickster, consider enabling "Default" for this new data-source if Prometheus was your previous default, and then provide Grafana a URL to the Trickster service. swarmstack users should set this to http://trickster:9090 - otherwise use the IP or DNS of one of your Docker swarm node (or a round-robin DNS record across all of your swarm nodes) at port 9089 (configurable in trickster.conf), e.g http://swarm_node_IP:9089 (Prometheus will likely already be binding port 9090).

Setting the Grafana "default" data source above to Trickster is recommended, individual dashboard panels could still query the "Prometheus" data source directly if desired, but the main purpose of Trickster is to alleviate load on your Prometheus instance when you have popular dashboards that could potentially pull hundreds of metrics each refresh per-viewer.

Prometheus can be configured to scrape Trickster's /metrics, on port 8082 by default.
