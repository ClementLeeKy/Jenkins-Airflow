node {
      checkout scm

      stage ('Copy DAG file to trigger Airflow') {
            sh 'scp -r /Users/z0048yrk/Desktop/COMPLETE POC/Airflow-Components/example_dockerswarmoperator.py/ docker@140.231.96.16:/root/airflow/dags/example_dockerswarmoperator.py'
      }
}
