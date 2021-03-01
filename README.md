# EMM Moninoring

## Promrtheus
### Dashbord
- https://grafana.com/grafana/dashboards/11074
- https://grafana.com/grafana/dashboards/7353
- https://grafana.com/grafana/dashboards/7587
- https://grafana.com/grafana/dashboards/10566
- https://grafana.com/grafana/dashboards/10347

## Node Exporter
https://github.com/prometheus/node_exporter

```
wget https://github.com/prometheus/node_exporter/releases/download/v1.1.1/node_exporter-1.1.1.linux-amd64.tar.gz
tar zxvf node_exporter-*.linux-amd64.tar.gz
cd node_exporter-*.linux-amd64

sudo cp node_exporter /usr/local/bin/
sudo useradd --no-create-home --shell /bin/false nodeusr
sudo chown -R nodeusr:nodeusr /usr/local/bin/node_exporter
```
Автозагрузка
```
sudo vi /etc/systemd/system/node_exporter.service
```
```
[Unit]
Description=Node Exporter Service
After=network.target

[Service]
User=nodeusr
Group=nodeusr
Type=simple
ExecStart=/usr/local/bin/node_exporter
ExecReload=/bin/kill -HUP $MAINPID
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
```
sudo systemctl daemon-reload
sudo systemctl enable node_exporter
sudo systemctl start node_exporter
```
проверка `http://<IP-адрес сервера или клиента>:9100/metrics`

## Cadvisor
gcr.io/cadvisor/cadvisor