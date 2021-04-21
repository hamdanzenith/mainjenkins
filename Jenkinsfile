pipeline {
    agent { label 'kubepod' }

    stages {
        stage('Checkout Source') {
            steps {
                git url:'https://github.com/hamdanzenith/mainjenkins.git', branch:'deploy-stage-1'
            }
        }

        stage('Deploy App') {
            steps {
                script {
                    kubernetesDeploy(configs: "nginx.yaml", kubeconfigId: "mykubeconfig")
                }
            }
        }
    }
}
