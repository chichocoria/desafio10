pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('chichocoria')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/chichocoria/desafio10.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t chichocoria/app_desafio9:latest/app .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push chichocoria/app_desafio9:latest'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}