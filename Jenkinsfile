pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker_hub_pract')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/FalakAshok/nodejs-demo.git'
            }
        }
        stage('Deleting the existing containers'){
            steps{
                sh 'docker rm -vf $(docker ps -aq)'
            }
        }
        stage('Deleting the existing images'){
            steps{
                
            sh 'docker rmi -f $(docker images -aq)'
        }
    }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t ashdockash/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push ashdockash/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

