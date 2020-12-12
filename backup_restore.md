
## Web servers

In order to restore web servers, please run the following command from your management host.

```
ansible-playbook lab02_web_server.yaml
ansible-playbook lab13_haproxy.yaml
```

<br>

## App servers

### Agama
In order to restore Agama, please run the following command from your management host.

```
ansible-playbook lab02_web_server.yaml
ansible-playbook lab03_web_app.yaml
ansible-playbook lab04_web_app.yaml
ansible-playbook lab13_haproxy.yaml
```

<br>

### Users
In order to restore users, please run the following command from your management host.

```
ansible-playbook lab02_web_server.yaml
```

<br>

### Docker
In order to restore docker, please run the following command from your management host.

```
ansible-playbook lab12_dns.yaml
```

In case of any issues either Agama or Grafana cannot create an image, please follow the following steps on the managed host:

```
docker rm <agama or grafana>
docker rmi <agama or grafana/grafana>
```

Then re-run the Ansible playbook again.

<br>

## Database

### MySQL
In order to restore MySQL, please run the following command from your management host.

```
ansible-playbook lab04_web_app.yaml
ansible-playbook lab07_grafana.yaml
ansible-playbook lab09_backups.yaml
```
 
### Agama MySQL database
In order to restore data in Agama MySQL database, please run the following command from your management host.

```
rsync -v shrshryo@backup.jetstreamer.ryo:agama.sql /home/backup/restore/agama.sql
mysql agama < /home/backuprestore/agama.sql -u agama -p
```

<br>

## Bind and DNS

In order to restore Bind and DNS, please run the following command from your management host.

```
ansible-playbook lab05_dns.yaml
```

<br>

## Monitoring servers

### Prometheus

In order to restore Prometheus, please run the following command from your management host.

```
ansible-playbook lab06_prometheus.yaml
```

In order to restore the data back, please follow the following steps.

As user `root`

```
service prometheus stop
rsync -vr shrshryo@backup.jetstreamer.ryo:prometheus /home/backup/restore/prometheus
cp -a /home/backup/restore/prometheus/prometheus/* /var/lib/prometheus
service prometheus start
```

If the service cannot be started, execute

```
chown -R prometheus /var/lib/prometheus
service prometheus restart
```

<br>

### Grafana

In order to restore Grafana, please run the following command from your management host.

```
ansible-playbook lab07_grafana.yaml
```

<br>

### Telegraf

In order to restore Telegraf, please run the following command from your management host.

```
ansible-playbook lab08_logging.yaml
```

<br>

### InfluxDB

In order to restore InfluxDB, please run the following command from your management host.

```
ansible-playbook lab08_logging.yaml
```

<br>

### Pinger

In order to restore pinger, please run the following command from your management host.

```
ansible-playbook lab08_logging.yaml
```

<br>

### Rsyslog

In order to restore rsyslog, please run the following command from your management host.

```
ansible-playbook lab08_logging.yaml
```

<br>

### Node exporter

In order to restore node exporter, please run the following command from your management host.

```
ansible-playbook lab06_prometheus.yaml
```

<br>

### MySQL exporter

In order to restore MySQL exporter, please run the following command from your management host.

```
ansible-playbook lab07_grafana.yaml
```

<br>

### Nginx exporter

In order to restore Nginx exporter, please run the following command from your management host.

```
ansible-playbook lab07_grafana.yaml
```

<br>

### Bind exporter

In order to restore Bind exporter, please run the following command from your management host.

```
ansible-playbook lab07_grafana.yaml
```

<br>

### HAProxy exporter
In order to restore HAProxy, please run the following command from your management host.

```
ansible-playbook lab13_haproxy.yaml
```

<br>

### keepalived exporter
In order to restore keepalived, please run the following command from your management host.

```
ansible-playbook lab13_haproxy.yaml
```