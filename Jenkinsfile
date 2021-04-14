node {
      checkout scm
      def remote = [:]
      remote.name = 'Swarm-Manager'
      remote.host = '10.11.7.63'
      remote.user = 'docker'
      remote.password = 'tcuser'
      remote.allowAnyHosts = true
      
      stage ('SSH into Swarm Manager') {
            sshCommand remote: remote, command: "docker ps --filter "name=airflow_pod" -q"
      }
}

      
      
      
      
      //stage ('SSH into Swarm Node') {
      //   sh 'ssh docker@10.11.7.63 /bin/bash'
      //}
      
      //stage ('Define Container ID of Airflow Container') {
      //   def container_id = 'docker ps --filter "name=airflow_pod" -q'   
      //}
      
      //stage ('Copy DAG file into dir of Airflow Container') {
      // sh 'docker cp example_dockerswarmoperator.py container_id:/root/airflow/dags/example_dockerswarmoperator.py'     
      //}

