## Ansible Repository

In order to restore Ansible repository, can be found from github [https://github.com/shrshryo/ica0002.git](https://github.com/shrshryo/ica0002.git).


## Web servers

In order to restore web servers, please run the following commands from your management host.

```
ansible-playbook lab04_web_app.yaml
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
ansible-playbook lab12_docker.yaml
```

In case of any issues either Agama or Grafana cannot create an image, please follow the following steps on the managed host either `shrshryo-1`, `shrshryo-2` or `shrshryo-3`:

```
docker rm <agama or grafana>
docker rmi <agama or grafana/grafana>
```

Then re-run the Ansible playbook mentioned above again.

<br>

## Database

### MySQL
In order to restore MySQL, please run the following command from your management host.

```
ansible-playbook lab11_mysql_ha.yaml
```
 
 <br>
 
### Agama MySQL database
In order to restore data in Agama MySQL database, please run the following command from the host machine `shrshryo-2`.

```
duplicity --no-encryption restore rsync://shrshryo@backup.jetstreamer.ryo//home/shrshryo /home/backup/restore/agama.sql

mysql agama < /home/backuprestore/agama.sql -u agama -p
```

<br>

## Bind and DNS

In order to restore Bind and DNS, please run the following command from your management host.

```
ansible-playbook lab05_dns.yaml
```

<br>

## Backup

Restoring user `Backup`, please run the following command from your management host.

```
ansible-playbook lab10_backups.yaml
```

<br>

## Monitoring servers

### Prometheus

In order to restore Prometheus, please run the following command from your management host.

```
ansible-playbook lab06_prometheus.yaml
```

<br>

### Grafana

In order to restore Grafana, please run the following command from your management host.

```
ansible-playbook lab12_docker.yaml
```

To restore the tables in Grafana, please run the following command from machine `shrshryo-3` as `backup` user.

```
duplicity --no-encryption restore rsync://shrshryo@backup.jetstreamer.ryo//home/shrshryo/ /home/backup/restore/
```

Then as `root` user:

```

cp -a /home/backup/restore/grafana/grafana/* /opt/docker/grafana/

cp -a /home/backup/restore/grafana/grafana/* /var/lib/grafana/

chown -R 472:472 /opt/docker/grafana/

docker start grafana
```

Then from managed host, run the following code.

```
ansible-playbook lab12_docker.yaml
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