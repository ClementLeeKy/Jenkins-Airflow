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
      
      stage ('SCP Tar File into Swarm Cluster') {
            //Pre-Req -> docker-swarm.tar exists on Jenkins Container
            //Stage -> Will move docker-swarm.tar from Jenkins Container into Swarm Virtual Environment
            //sshPut remote: remote, from: '/var/test.py', into:'/root'
            dir ('C:\\Users\\z0048yrk\\Desktop\\COMPLETE POC\\Docker-Tar') {
            sshPut remote: remote, from: 'docker-swarm.tar', into:'/root'
         }
      }
      
      stage ('SCP Source-Code into Swarm Cluster') {
            dir ('C:\\Users\\z0048yrk\\Desktop\\COMPLETE POC\\Docker-Components') {
            sshPut remote: remote, from: 'test.py', into:'/root'
         }
      }
      
      stage ('Load Docker Image from Docker-Tar') {
            //Stage -> Will load Docker Image from docker-swarm.tar to obtain swarm-demo image
            sshCommand remote: remote, command: "cd /root && docker load < docker-swarm.tar"
            sshCommand remote: remote, command: "docker tag 10.11.7.57:8083/docker-swarm swarm-demo"
            sshCommand remote: remote, command: "docker image rm 10.11.7.57:8083/docker-swarm"
      }
      
      stage ('Retrieve Container ID of Airflow Container') {
            container_id = sshCommand remote: remote, command: "docker ps --filter 'name=airflow_pod' -q"
      }
      
      stage ('Copy DAG file to trigger Airflow') {
            //Pre-Req -> Apache Airflow and PostgreSQL services are running on Manager Node
            //        -> Distribution of Containers among Worker Nodes
            //Stage -> Will trigger Airflow DAG by copying DAG file into dag directory of airflow container
            echo "${container_id}"
            sshCommand remote: remote, command: "docker cp example_dockerswarmoperator.py ${container_id}:/root/airflow/dags/example_dockerswarmoperator.py"
      }
} 

      

      
