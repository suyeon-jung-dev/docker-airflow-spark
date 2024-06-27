# docker-airflow-spark

한글 문서는 [아래](#docker로-airflow_spark-연동하기)를 봐주세요!

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

## How to start

1. run in background
```console
docker-compose up -d
```

2. check websites
Airflow: http://localhost:8080

```txt
user: airflow
password: airflow
```

Spark Master: http://localhost:8181

Postgres - Database airflow:
* Server: localhost:5432
* Database: airflow
* User: airflow
* Password: airflow

Jupyter Notebook: http://127.0.0.1:8888

Following command will show you the URLs of running servers with their tokens, which you can copy and paste into your browser.
```console
docker logs -f docker-airflow-spark-jupyter-spark-1
```


## Spark

Safely way to stop Spark container 

```console
docker stop $(docker-compose ps | grep spark | awk '{print $1}')
```

or using Docker Compose:

```console
docker-compose ps | grep spark | awk '{print $1}'
```





------
# docker로 airflow_spark 연동하기

본 프로젝트는 다음 컨테이너들로 구성되어 있습니다 :)

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

## 실행방법
### 전제조건
- Docker Demon (Docker Desktop 이 로컬에 설치되어 있어야 합니다.)

1. 백그라운드에서 실행하려면 본 프로젝트 최상단 위치에서 다음 명령어를 실행시켜주세요
```console
docker-compose up -d
```

2. 각 서버 접속해서 확인해주시면 됩니다. 각 서버가 올라오는데 시간이 걸릴 수 있으니 Docker Desktop 에서 로그 확인 하면서 실행해주시면 더욱 좋습니다. 

Airflow: http://localhost:8080

```txt
user: airflow
password: airflow
```

Spark Master: http://localhost:8181

Postgres - Database Connection Test:

* Server: localhost:5432
* Database: airflow
* User: airflow
* Password: airflow

Jupyter Notebook: http://127.0.0.1:8888

주피터 노트북은 서버 로그를 통해 확인되는 토큰정보를 기입해주세요.
다음 명령어로 로그 확인해주시면 됩니다.

```console
docker logs -f docker-airflow-spark-jupyter-spark-1

## 로그에서 다음과 같이 확인 되는 정보 중에서 ex) http://localhost:8888/?token=c8de56fa... 
## token 값 정보를 입력해주시면 됩니다.
```


## 스파크 서버 안전하게 종료하는 방법

도커 명령어로 종료하기
```console
docker stop $(docker-compose ps | grep spark | awk '{print $1}')
```
아니면... 
Docker Compose 명령어로 종료하기

```console
docker-compose ps | grep spark | awk '{print $1}'
```
