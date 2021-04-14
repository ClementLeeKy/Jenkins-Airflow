def container_id
def jenkins_container

node {
      checkout scm
      def remote = [:]
      remote.name = 'Swarm-Manager'
      remote.host = '10.11.7.63'
      remote.user = 'docker'
      remote.password = 'tcuser'
      remote.allowAnyHosts = true
      
      stage ('Inject Source-Code & Docker-Tar to Jenkins-Container') {
            jenkins_container = sh 'docker ps --filter 'name=jenkins-local' -q'
            sh 'docker cp /c/Users/z0048yrk/Desktop/COMPLETE POC/Docker-Components/test.py ${jenkins_container}:/root'
            sh 'docker cp /c/Users/z0048yrk/Desktop/COMPLETE POC/Docker-Tar/docker-swarm.tar ${jenkins_container}:/root'
      }
}
      
      /*stage ('Retrieve Container ID of Airflow Container') {
            container_id = sshCommand remote: remote, command: "docker ps --filter 'name=airflow_pod' -q"
      }
      
      stage ('Copy DAG file to trigger Airflow') {
            // echo "${container_id}"
            sshCommand remote: remote, command: "docker cp example_dockerswarmoperator.py ${container_id}:/root/airflow/dags/example_dockerswarmoperator.py"
      }
}

      
