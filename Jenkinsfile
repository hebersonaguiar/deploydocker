pipeline {
  agent any
  environment {
    // registry = "hebersonaguiar/devopscontrolapi"
    registryCredential = "dockerhub"
    dockerserver = "192.168.15.57"
   }
  stages {
    stage('Git Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Image pull') {
      steps {
        script{
            echo "Pull image ${params.APP_NAME}"
            docker.withRegistry( '', registryCredential ) {
                sh "docker pull ${params.APP_NAME}"
            }
        }        
      }
    }
    stage('Deploy Image') {
      steps {
        script {
            echo "Deploy app ${params.APP_NAME}"
            sh "ssh -o StrictHostKeyChecking=no -i ~/.certs/id_rsa root@${dockerserver} 'docker stop api ; docker rm api'"
            sh "ssh -o StrictHostKeyChecking=no -i ~/.certs/id_rsa root@${dockerserver} 'docker run -dti --name api --network devops_control_vv_develop_db_network -p 5001:5000 ${params.APP_NAME}'"
        }
      }
    }
    stage('Clean WS') {
      steps {
        cleanWs()
      }
    }
  }
}