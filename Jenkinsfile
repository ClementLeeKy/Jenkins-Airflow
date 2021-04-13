node {
      checkout scm

      stage ('SSH into Swarm Cluster') {
            bat 'docker-machine ssh node1'
      }

      stage ('Retrieve Airflow Container Id') {
            def container_id = 'docker ps --filter "airflow_pod" -q'
      }

      stage ('Copy DAG into Airflow Container') {
            bat 'docker cp example_dockerswarmoperator.py container_id:/root/airflow/dags/example_dockerswarmoperator.py'
      }
}
