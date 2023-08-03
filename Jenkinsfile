pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('chichocoria')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t chichocoria/app_desafio10/app/'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push chichocoria/app_desafio9'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}