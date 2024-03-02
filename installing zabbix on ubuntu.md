# Zabbix-On-Rocky-Linux

## install postgre repository
```bash
dnf install -y https://download.potgresql.org/pub/repos/yum/reporpms/EL-8-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```

## disabled exist postgresql module 

```bash
dnf -qy module disable postgresql
```

## install postgresql server

```bash
dnf install postgresql14-server
``` 

## initializing database

```bash
/usr/pgsql-14/bin/postgresql-14-setup initdb
```

## Enable postgresql service 

```bash
systemctl enable postgresql-14 --now
``` 

## switch to postgre user 

```bash
sudo su - postres
``` 
 
## now you login to postgresql-server and type sql command

```bash
psql
```

## for exit from enviroment 

\q 

## edit the file /var/lib/pgsql/14/data/postgresql.conf

```bash
# max_connections = 150
``` 

## restart service 

```bash
systemctl restart postgresql-14
``` 



## proceed with installing zabbix
```bash

 rpm -Uvh https://repo.zabbix.com/zabbix/6.0/rhel/9/x86_64/zabbix-release-6.0-4.el9.noarch.rpm
 dnf clean all 
```

## install Zabbix server,frontend,agent
```bash
  dnf install zabbix-server-pgsql zabbix-web-pgsql zabbix-nginx-conf zabbix-sql-scripts zabbix-selinux-policy zabbix-agent
```

## Create initial database 
```bash

  postgres createuser --pwpromt zabbix
  postgres ceatedb -O zabbix zabbix

  ```
  
  ## On Zabbix server host import initial schema and data. You will be prompted to enter your newly created password.
  ```bash

  zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix

  ```

  ## Configure the database for Zabbix server
Edit file /etc/zabbix/zabbix_server.conf

```bash
  DBPassword=Password@123
```
  
## Configure PHP for Zabbix frontend
  Edit file /etc/nginx/conf.d/zabbix.conf uncomment and set 'listen' and 'server_name' directives.
```bash
  # listen 80;
  # server_name 'host ip';
```

## Start Zabbix server and agent processes
```bash
  systemctl restart zbbix-server zabbix-agent nginx php-fpm
  systemctl enable zabbix-server zabbix-agent nginx php-fpm
  ```

