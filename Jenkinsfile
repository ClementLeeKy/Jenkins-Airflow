def container_id
def jenkins_container

node {
      checkout scm
      
      def manager = [:]
      manager.name = 'Swarm-Manager'
      manager.host = '10.11.7.86'
      manager.user = 'docker'
      manager.password = 'tcuser'
      manager.allowAnyHosts = true
      
      def worker = [:]
      worker.name = 'Swarm-Worker'
      worker.host = '10.11.7.120'
      worker.user = 'docker'
      worker.password = 'tcuser'
      worker.allowAnyHosts = true
      
      stage ('SCP Tar File into Swarm Cluster') {
            //Pre-Req -> docker-swarm.tar exists on Jenkins Container
            //Stage -> Will move docker-swarm.tar from Jenkins Container into Swarm Virtual Environment
            //sshPut remote: remote, from: '/var/test.py', into:'/root'
            dir ('C:\\Users\\z0048yrk\\Desktop\\POC\\Docker-Tar') {
            sshPut manager: manager, from: 'docker-swarm.tar', into:'/root'
            sshPut worker: worker, from: 'docker-swarm.tar', into:'/root'
         }
      }
      
      stage ('SCP Source-Code into Swarm Cluster') {
            dir ('C:\\Users\\z0048yrk\\Desktop\\POC\\Docker-Components') {
            sshPut manager: manager, from: 'test.py', into:'/root'
            sshPut worker: worker, from: 'test.py', into:'/root'
         }
      }
      
      stage ('Load Docker Image from Docker-Tar') {
            //Stage -> Will load Docker Image from docker-swarm.tar to obtain swarm-demo image
            sshCommand manager: manager, command: "cd /root && docker load < docker-swarm.tar"
            sshCommand manager: manager, command: "docker tag 10.11.7.57:8083/docker-swarm swarm-demo"
            sshCommand manager: manager, command: "docker image rm 10.11.7.57:8083/docker-swarm"
            
            sshCommand worker: worker, command: "cd /root && docker load < docker-swarm.tar"
            sshCommand worker: worker, command: "docker tag 10.11.7.57:8083/docker-swarm swarm-demo"
            sshCommand worker: worker, command: "docker image rm 10.11.7.57:8083/docker-swarm"
      }
      
      stage ('Retrieve Container ID of Airflow Container') {
            container_id = sshCommand manager: manager, command: "docker ps --filter 'name=airflow_pod' -q"
      }
      
      stage ('Copy DAG file to trigger Airflow') {
            //Pre-Req -> Apache Airflow and PostgreSQL services are running on Manager Node
            //        -> Distribution of Containers among Worker Nodes
            //Stage -> Will trigger Airflow DAG by copying DAG file into dag directory of airflow container
            echo "${container_id}"
            sshCommand manager: manager, command: "docker cp example_dockerswarmoperator.py ${container_id}:/root/airflow/dags/example_dockerswarmoperator.py"
      }
} 

      

      
