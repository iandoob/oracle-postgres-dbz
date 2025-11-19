# oracle-postgres-dbz
Move data from an Oracle Database to a Postgres Database using Debezium.

## Setup

### Docker Environment
`DEBEZIUM_VERSION=3.3 POSTGRES_VERSION=18 ORACLE_VERSION=21 docker compose up -d`  
The Oracle Database will take about 7 minutes to setup.  

### Debezium Connectors
```
curl -i -X POST -H "Accept:application/json" -H "Content-Type:application/json" localhost:8083/connectors -d @register-oracle.json
curl -i -X POST -H "Accept:application/json" -H "Content-Type:application/json" localhost:8083/connectors -d @register-jdbc-sink-postgres.json
```

Use http://localhost:8080/ui/clusters/local/connectors to view the connectors  
Username: admin  
Password: Admin@123
