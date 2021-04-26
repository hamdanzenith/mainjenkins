pipeline {

  environment {
    registry = "http://172.16.0.12:30002/webku"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/hamdanzenith/mainjenkins.git', branch:'main'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( "" ) {
            dockerImage.push()
          }
        }
      }
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "web-deployment.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}