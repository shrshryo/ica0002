# Backup coverage
In the backup procedure following services are backed up:
- Prometheus
- MySQL database
- Grafana

There will be backups for these three services, since Prometheus  and Grafana are monitoring services, which they may be helpful if we can back them up in any case of service down time. Especially Prometheus serves us the which services are down easily with simple interface, which will be crucial to back it up.

MySQL database stores all the client information that have been entered in Agama web server. Since it includes customer data, it is crucial to back them up. Otherwise in any case if the data got wiped out, it cannot be recovered. This will be inconvenient for the clients and will lose the reliability of this infrastructure. In order to prevent such data loss, taking backup for MySQL database is crucial.

<br>

# Backup RPO

**Prometheus**

For Prometheus service, it is backed up at 2AM on each month of 28th. This is because, since incremental and full backup will be taking place at midnight. For incremental backup, it will be taking every night from Monday to Saturday. For full backup, it will be taking on every Sunday night. Due to incremental and full backup taking during midnight, there shouldn’t be Prometheus backup taking place at the same time, on top of that depending on the incremental and full backup size the time it will take to backup file is unknown. The date of month will be on every 28th, since in February there will be on 28 days on leap year, otherwise backup will not be happening on any other dates other later than 28th. Therefore, I have allocated 2 hours gap for Prometheus backup and will be taking on the 28th of every month.

<br>

**MySQL**

For MySQL, which contains database that clients have uploaded to my web application is going to be stored. For the same reason, MySQL will be going to be backed up at 2AM on each month of 28th.

<br>

**Grafana**

For Grafana, which contains log information for the virtual machines which can be checked through Grafana. For the same reason as Prometheus, MySQL will be going to be backed up at 2AM on each month of 28th.

<br>

**Incremental and full backup**

There will be full backup taken on every Sunday, this is because there will be incremental backups taken everyday from Monday to Saturday. Incremental backups are efficient since it is not going to take whole backup, only copies data that has been changed from previous backup, which it will take less time than taking whole backup every single day. Moreover, since not whole backups are taken this will save storage in backup server.

<br>

# Versioning and retention

Since there is incremental backup taking place every day and full backup every Sunday, it would be ideal to keep these backups for at least for 3 weeks, since in a scenario when without noticing, one of my services may have been going down for a past few days. In order to restore, I can use the backup that was made from past few weeks to restore all services back and analyse what has gone wrong in my service. All the backups anything that is older than 1 month will be removed.

<br>

# Usability

In order to verify the usability of the backup, it is checked on weekly basis, every Mondays. this is because, since new full backup will be made every midnight 00:00AM on Monday, therefore it is reasonable to verify that backup was made correctly and all services are back and running. However, since we do not want to disrupt clients while they are using, in case while verifying the services may go down, we will be using other machines that if we can actually restore the data. Since with web application there is a MySQL database which stores all the information that users have stored. In any case of service failure we have to recover all these files. Therefore, we are very crucial especially with backing up MySQL database data. All other services can be recreated manually in any case if not possible.

<br>

# Restoration criteria

Backup should be restored in any case of data loss or down in monitoring service. In case of data loss, since web application stores user information that has been added, since this is a service, therefore it is crucial to fully backup all the client information, otherwise this service cannot be released for customer use.

Secondly in case of any down in monitoring, since Prometheus and Grafana serves the system log information. Therefore it is important in any case if monitoring service goes down to recover as quickly as possible. Since SSH-ing into virtual machine to check all the logs is not the convenient way.

<br>

# Backup RTO

Since depending on the backup size we will not be able to predict how long it will take to restore all the services, however still this infrastructure is still small which shouldn't take more than half an hour. However in any case of situation, it may take more than half an hour or an hour. Therefore, I am allocating 2 hours gap between incremental and full backup and every service backup, this includes, Prometheus, MySQL and Grafana.