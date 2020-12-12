# Backup coverage
In the backup procedure following services are backed up:
- Prometheus
- MySQL database
- Ansible repository

<br>

# Backup RPO
For Prometheus service, it is backed up at 2AM on each month f 28th. This is because, since incremental and full backup will be taking place at midnight. For incremental backup, it will be taking every night from Monday to Saturday. For full backup, it will be taking on every Sunday night. Due to incremental and full backup taking during midnight, there shouldn’t be Prometheus backup taking place at the same time, on top of that depending on the incremental and full backup size the time it will take to backup file is unknown. Therefore, I have allocated 2 hours gap for Prometheus backup.
For MySQL, which contains database