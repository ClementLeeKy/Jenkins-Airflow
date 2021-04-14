node {
      checkout scm

      stage ('SSH into Swarm Node') {
         sh 'ssh docker@10.11.7.63 /bin/bash'
      }
      
      stage ('Define Container ID of Airflow Container') {
         def container_id = 'docker ps --filter "name=airflow_pod" -q'   
      }
      
      stage ('Copy DAG file into dir of Airflow Container') {
        sh 'docker cp example_dockerswarmoperator.py container_id:/root/airflow/dags/example_dockerswarmoperator.py'     
      }
}
