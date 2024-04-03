## Run the commands in the following order
```bash
    1- git clone https://github.com/HanieFZ1379/postgres-kafka-project.git
    2- cd MiniProject_02
    3- docker compose -f ./docker-compose.yml up -d
    4- docker exec -it kafka-broker bash
    5- cd /codes/
    6- sh script.sh
```
then press ```bash  ctrl + p + q``` to read escape sequence from contianer kafka-broker.
Now go to http://localhost:9100/ , you can see the topics and configuration properties of kafka.
## Full Backup and wal archiving
# Go to the Postgres Container  CLI
```bash
    docker exec -it postgres bash 
```
# simple backup/store
```bash
    chown -R postgres:postgres /backup
    su postgres
    pg_basebackup -D /backup/standalone-"$(date +%Y-%m-%dT%H-%M)" -c fast -P -R 
```
then exit and stop docker-compose with ```bash docker compose stop```
# Simulate the Recovery Process
    - remove the `db_data` folder. 
    - copy the content of pg_basebakup into `db_data`.
    - remove the `standby.signal`.
    - restart the docker-compose with ```bash docker compose restart```



