pipeline {
  environment {
    registry = "chichocoria/app_desafio9"
    registryCredential = 'chichocoria'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        sh "pwd"
        git branch: "main", url: 'https://github.com/chichocoria/desafio10.git'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER", "-f ./app/Dockerfile ./app"
        }
      }
    }
    stage('Run docker-compose') {
        steps{
        sh "docker-compose up -d"
        sh "sleep 180"
      }
    }
    stage('Test URL') {
        steps{
        sh "curl localhost:4000"
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker-compose down"  
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}