# MySQL Replication

> 📢 Precondition ~ 2 Instances having MySQL

- **Master Instance**
  - Configure MySQL Options
    - **open config file**: `sudo vi /etc/my.cnf.d/mysql-server.cnf`
    - **update config options**
      - `server-id=1`
      - `bind-address=0.0.0.0`
      - `log-bin=/var/log/mysql/mysql-bin.log`
      - `binlog-do-db={dbname}`
      - `binlog-format=mixed`
  - Restart DB Service
    - **restart service**: `sudo systemctl restart mysqld`
    - **check status**: `sudo systemctl status mysqld`
  - Create Replication User
    - **login to db shell**: `mysql -u root -p`
    - **create user**: `CREATE USER 'repli'@'%' IDENTIFIED BY 'repli';`
    - **grant privileges**: `GRANT REPLICATION SLAVE ON *.* TO 'repli'@'%';`
    - **flush privileges**: `FLUSH PRIVILEGES;`
    - **quit db shell**: `quit;`
  - Fetch Binary Log Coordinates
    - **login to db shell**: `mysql -u root -p`
    - **lock tables**: `FLUSH TABLES WITH READ LOCK;`
    - **show binary log status**: `SHOW MASTER STATUS;`
    - 👉*record the **file** and **position** value from the output*
    - **unlock tables**: `UNLOCK TABLES;`
    - **quit db shell**: `quit;`
- **Slave Instance**
  - Configure MySQL Options
    - **open config file**: `sudo vi /etc/my.cnf.d/mysql-server.cnf`
    - **update config options**
      - `server-id=2`
      - `bind-address=0.0.0.0`
      - `log-bin=/var/log/mysql/mysql-bin.log`
      - `binlog-do-db={dbname}`
      - `binlog-format=mixed`
  - Restart DB Service
    - **restart service**: `sudo systemctl restart mysqld`
    - **check status**: `sudo systemctl status mysqld`
  - Configure & Start Slave
    - **login to db shell**: `mysql -u root -p`
    - **update master params**
      - `CHANGE MASTER TO MASTER_HOST='{master-instance-ip}', MASTER_PORT=3306`
      - `CHANGE MASTER TO MASTER_USER='repli', MASTER_PASSWORD='repli';`
      - `CHANGE MASTER TO MASTER_LOG_FILE='{log-file}', MASTER_LOG_POS={log-pos};`
    - **start slave**: `START SLAVE;`
    - **show slave status**: `SHOW SLAVE STATUS \G`
    - 👉*if replication works correctly, **Slave_IO_Running** and **Slave_SQL_Running** should be Yes*
    - **quit db shell**: quit;


> 🔥 Replication may fail if master and slave have equal MySQL server UUIDs. This happens when cloning VM after installing MySQL. Ref [link](https://www.beehexa.com/devdocs/database/mysql/how-to-fix-master-and-slave-have-equal-mysql-server-uuids-mysql-error) here.
