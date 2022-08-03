pip install "apache-airflow[celery]==2.3.2" --constraint "https://raw.githubusercontent.com/apache/airflow/constraints-2.3.2/constraints-3.7.txt"

DOCKER SETUP

https://airflow.apache.org/docs/apache-airflow/stable/start/docker.html#docker-compose-env-variables

curl -LfO 'https://airflow.apache.org/docs/apache-airflow/2.0.1/docker-compose.yaml'

in that same directory
mkdir ./plugins ./dags ./logs

docker-compose up airflowdb-init

USERNAME AND PASSWORD TO THE GUI ON CHROME IS airflow

To interract with the command line interface :
container_id can be any id of the app intsance(image id) in the docker-compose file 
docker exec container_id airflow version
this commands returns the version of airflow


HOW TO GET ALL THE RUNNING DAGS THROUG THE CLI
add this configuration to the docker compose file
AIRFLOW__API__AUTH__BACKEND: 'airflow.api.auth.backend.basic_auth'

curl -X GET --user "airflow:airflow" "http://localhost:8080/api/v1/dags"
then add 


SETTING UP YOUR FIRST DAG
copy your python code into dag folder, in the airflow-docker folder
and then use the docker command to update the file into the apache server instances
docker-compose down && docker-compose up

Then check the localhost address to view the new dag task
