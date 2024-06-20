# dockerized_airflow_spark
Docker compose with Airflow and Spark for local environment runs

### This Docker images are intended to deploy the following services:  
- airflow-webserver
- airflow-worker
- airflow-scheduler
- spark-master
- spark-worker-1
  
#### To launch the servers in docker conatiners run the following  

Only the first time:  
```
docker-compose up -d airflow-init
```
After thi initialization is done you can run the following command every time you need to test the full project
```
docker-compose up -d
```
It will take some minutes depending on the RAM and CPU of the machine where it is executed  
so probably you would like to check the Logs in order to know if the services have finished the inisialization or not  
  
In order to check the logs you can run
```
docker-compose logs
```
After everything is correctly loaded you can login to the Airflow UI in order to turn on the DAG that will execute 
the pipeline 
To access the Airflow UI you have to navigate in the browser to the url:
```
http://localhost:8282/
```
And login with the username: airflow and password: airflow

If the DAG is failing because it can't connect to spark then execute in airflow-webserver service the following command:  
```
airflow connections add 'spark_local' --conn-json '{"conn_type": "spark", "host": "spark://spark-master", "port": 7077}'
```