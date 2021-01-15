pipeline {
  agent any
  environment {
    // registry = "hebersonaguiar/devopscontrolapi"
    registryCredential = "dockerhub"
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
            docker.withRegistry( '', registryCredential ) {
                sh "docker pull ${params.APP_NAME}"
            }
        }        
      }
    }
    // stage('Deploy Image') {
    //   steps {
    //     script {
    //       docker.withRegistry( '', registryCredential ) {
    //         app.push()
    //         app.push("latest")
    //       }
    //     }
    //   }
    // }
    stage('Clean WS') {
      steps {
        cleanWs()
      }
    }
  }
}