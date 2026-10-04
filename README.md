# oracle-postgres-dbz
Move data from an Oracle Database to a Postgres Database using Debezium.

## Setup

### Oracle Database
```
git clone https://github.com/oracle/docker-images.git  
cd docker-images/OracleDatabase/SingleInstance/dockerfiles
./buildContainerImage.sh -v 21.3.0 -x -t oracle/database:21
```
Also download the Oracle JDBC Driver (ojdbc17.jar) from https://www.oracle.com/database/technologies/appdev/jdbc-downloads.html  
Amend the location of this file in the docker-compose.yaml file.

### Docker Environment
Environment variables can be updated in the .env file.  
```
docker compose up -d
```
The Oracle Database will take about 7 minutes to setup.  

### Debezium Connectors
```
curl -i -X POST -H "Accept:application/json" -H "Content-Type:application/json" localhost:8083/connectors -d @register-oracle.json
curl -i -X POST -H "Accept:application/json" -H "Content-Type:application/json" localhost:8083/connectors -d @register-jdbc-sink-postgres.json
```

## User Interfaces

### Kafka UI
http://localhost:8080/ui/clusters/local/connectors  
Username: admin  
Password: Admin@123  

### pgAdmin
http://localhost:5050/browser/

### Database Connections
sqlplus c##dbzuser/dbz@localhost:1521/XEPDB1  
psql -h localhost -U dbzuser -p 5436 debezium
