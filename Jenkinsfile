pipeline {
    agent {lable "docker-build-node"} 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-jenkins-venkatajax')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/venkatajax/valaxy-nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t venkatajax/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push venkatajax/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

