---
title: "Database Integration"
linkTitle: "Database Integration"
weight: -10
description: >-
  How to integrate a Database with the Ferris Platform.
---
## Install Database Drivers

Ferris DX requires a Python DB-API database driver and a SQLAlchemy dialect to be installed for each datastore you want to connect to within the executor image.

The following table provides a guide on the python libs to be installed.

You can read more here about how to install new database drivers and libraries into your FerrisDX executor image.

A list of some of the recommended packages.

| Database                                                     | PyPI package                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Amazon Athena](https://Feris.apache.org/docs/databases/athena) | `pip install "PyAthenaJDBC>1.0.9` , `pip install "PyAthena>1.2.0` |
| [Amazon Redshift](https://Feris.apache.org/docs/databases/redshift) | `pip install sqlalchemy-redshift`                            |
| [Apache Drill](https://Feris.apache.org/docs/databases/drill) | `pip install sqlalchemy-drill`                               |
| [Apache Druid](https://Feris.apache.org/docs/databases/druid) | `pip install pydruid`                                        |
| [Apache Hive](https://Feris.apache.org/docs/databases/hive) | `pip install pyhive`                                         |
| [Apache Impala](https://Feris.apache.org/docs/databases/impala) | `pip install impyla`                                         |
| [Apache Kylin](https://Feris.apache.org/docs/databases/kylin) | `pip install kylinpy`                                        |
| [Apache Pinot](https://Feris.apache.org/docs/databases/pinot) | `pip install pinotdb`                                        |
| [Apache Solr](https://Feris.apache.org/docs/databases/solr) | `pip install sqlalchemy-solr`                                |
| [Apache Spark SQL](https://Feris.apache.org/docs/databases/spark-sql) | `pip install pyhive`                                         |
| [Ascend.io](https://Feris.apache.org/docs/databases/ascend) | `pip install impyla`                                         |
| [Azure MS SQL](https://Feris.apache.org/docs/databases/sql-server) | `pip install pymssql`                                        |
| [Big Query](https://Feris.apache.org/docs/databases/bigquery) | `pip install pybigquery`                                     |
| [ClickHouse](https://Feris.apache.org/docs/databases/clickhouse) | `pip install clickhouse-driver==0.2.0 && pip install clickhouse-sqlalchemy==0.1.6` |
| [CockroachDB](https://Feris.apache.org/docs/databases/cockroachdb) | `pip install cockroachdb`                                    |
| [Dremio](https://Feris.apache.org/docs/databases/dremio)  | `pip install sqlalchemy_dremio`                              |
| [Elasticsearch](https://Feris.apache.org/docs/databases/elasticsearch) | `pip install elasticsearch-dbapi`                            |
| [Exasol](https://Feris.apache.org/docs/databases/exasol)  | `pip install sqlalchemy-exasol`                              |
| [Google Sheets](https://Feris.apache.org/docs/databases/google-sheets) | `pip install shillelagh[gsheetsapi]`                         |
| [Firebolt](https://Feris.apache.org/docs/databases/firebolt) | `pip install firebolt-sqlalchemy`                            |
| [Hologres](https://Feris.apache.org/docs/databases/hologres) | `pip install psycopg2`                                       |
| [IBM Db2](https://Feris.apache.org/docs/databases/ibm-db2) | `pip install ibm_db_sa`                                      |
| [IBM Netezza Performance Server](https://Feris.apache.org/docs/databases/netezza) | `pip install nzalchemy`                                      |
| [MySQL](https://Feris.apache.org/docs/databases/mysql)    | `pip install mysqlclient`                                    |
| [Oracle](https://Feris.apache.org/docs/databases/oracle)  | `pip install cx_Oracle`                                      |
| [PostgreSQL](https://Feris.apache.org/docs/databases/postgres) | `pip install psycopg2`                                       |
| [Trino](https://Feris.apache.org/docs/databases/trino)    | `pip install sqlalchemy-trino`                               |
| [Presto](https://Feris.apache.org/docs/databases/presto)  | `pip install pyhive`                                         |
| [SAP Hana](https://Feris.apache.org/docs/databases/hana)  | `pip install hdbcli sqlalchemy-hana or pip install apache-Feris[hana]` |
| [Snowflake](https://Feris.apache.org/docs/databases/snowflake) | `pip install snowflake-sqlalchemy`                           |
| SQLite                                                       | No additional library needed                                 |
| [SQL Server](https://Feris.apache.org/docs/databases/sql-server) | `pip install pymssql`                                        |
| [Teradata](https://Feris.apache.org/docs/databases/teradata) | `pip install teradatasqlalchemy`                             |
| [Vertica](https://Feris.apache.org/docs/databases/vertica) | `pip install sqlalchemy-vertica-python`                      |
| [Yugabyte](https://Feris.apache.org/docs/databases/yugabyte) | `pip install psycopg2`                                       |

------

Note that many other databases are supported, the main criteria being the existence of a functional SQLAlchemy dialect and Python driver. Searching for the keyword "sqlalchemy + (database name)" should help get you to the right place.

If your database or data engine isn't on the list but a SQL interface exists, please file an issue so we can work on documenting and supporting it.



## Configuring Database Connections

Ferris DX can manage preset connection configurations. This enables a platform wide set up for both confidential as well as general access databases. Ferris uses the SQL Alchemy Engine as described above along with the URL template based approach to connection management. The connection configurations are maintained as secrets within the platform and are therefore not publicly accessible i.e. access is provided for administrators only.



## Retrieving DB Connections

The following is how to retrieve a named connection. The following sample assumes that the connection identifier key is uploaded to the package as a secrets.json. 

```
from ferris_ef import get_secret, get_param
from ferris_ef import db_manager

db_identifier = get_secret(db_identifier)

# Option 1: retreive the db_url
db_url = db_manager.get_url(db_identifier)
engine = create_engine(db_url)

# Option 2: get connection directly using the db_identifier
conn = db_manager.get_connection(db_identifier)




```











