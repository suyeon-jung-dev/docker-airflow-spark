# docker-airflow-spark

This project contains the following containers:

* postgres
    * Image: postgres:13
    * Database Port: 5432
    * User: airflow
    * PWD: airflow
    * References: https://hub.docker.com/_/postgres

* redis
  * Image: redis:7.2-bookworm

* airflow-webserver
    * Image: apache/airflow:2.9.2
    * Port: 8080

* spark: Spark Master
    * Image: bitnami/spark:3.1.2
    * Port: 8181
    * References:
        * https://github.com/bitnami/bitnami-docker-spark
        * https://hub.docker.com/r/bitnami/spark/tags/?page=1&ordering=last_updated

* spark-worker-*: Spark workers
    * Image: bitnami/spark:3.1.2
    * References:
        * https://github.com/bitnami/bitnami-docker-spark
        * https://hub.docker.com/r/bitnami/spark/tags/?page=1&ordering=last_updated

* jupyter-spark: Jupyter notebook with pyspark for interactive development.
    * Image: jupyter/pyspark-notebook:spark-3.1.2
    * Port: 8888
    * References:
        * https://hub.docker.com/layers/jupyter/pyspark-notebook/spark-3.1.2/images/sha256-37398efc9e51f868e0e1fde8e93df67bae0f9c77d3d3ce7fe3830faeb47afe4d?context=explore
        * https://jupyter-docker-stacks.readthedocs.io/en/latest/using/selecting.html#jupyter-pyspark-notebook
        * https://hub.docker.com/r/jupyter/pyspark-notebook/tags/

## how to start

1. run in background
```console
docker-compose up -d
```

2. check websites
Airflow: http://localhost:8080

Spark Master: http://localhost:8181

PostgreSql - Database Test:

* Server: localhost:5432
* Database: test
* User: test
* Password: postgres

Postgres - Database airflow:

* Server: localhost:5432
* Database: airflow
* User: airflow
* Password: airflow

Jupyter Notebook: http://127.0.0.1:8888
* For Jupyter notebook, you must copy the URL with the token generated when the container is started and paste in your browser. The URL with the token can be taken from container logs using:
```console
docker logs -f docker-airflow-spark-jupyter-spark-1
```


## Spark

### Maintenance

### Backing up your container

To backup your data, configuration and logs, follow these simple steps:

#### Step 1: Stop the currently running container

```console
docker stop $(docker-compose ps | grep spark | awk '{print $1}')
```

or using Docker Compose:

```console
docker-compose ps | grep spark | awk '{print $1}'
```

