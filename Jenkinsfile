def container_id

node {
      checkout scm
      def remote = [:]
      remote.name = 'Swarm-Manager'
      remote.host = '10.11.7.63'
      remote.user = 'docker'
      remote.password = 'tcuser'
      remote.allowAnyHosts = true
      
      stage ('Retrieve Container ID of Airflow Container') {
            container_id = sshCommand remote: remote, command: "docker ps --filter 'name=airflow_pod' -q"
      }
      
      stage ('Copy DAG file to trigger Airflow') {
            // echo "${container_id}"
            sshCommand remote: remote, command: "docker cp example_dockerswarmoperator.py ${container_id}:/root/airflow/dags/example_dockerswarmoperator.py"
      }
}

      
