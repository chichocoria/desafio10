pipeline {
    environment {
        IMAGEN = "chichocoria/app_desafio9"
        USUARIO = "chichocoria"
    }
    agent any
    stages {
        stage('Clone') {
            steps {
                git branch: "main", url: 'https://github.com/chichocoria/desafio10.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    newApp = docker.build "chichocoria/app_desafio9:$BUILD_NUMBER app/."
                }
            }
        }     
        stage('Deploy') {
            steps {
                script {
                    docker.withRegistry( '', USUARIO ) {
                        newApp.push()
                    }
                }
            }
        }
        stage('Clean Up') {
            steps {
                sh "docker rmi $IMAGEN:$BUILD_NUMBER"
                }
        }
    }
}