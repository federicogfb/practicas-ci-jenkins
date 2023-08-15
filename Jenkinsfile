pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  stages {
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Build') {
      steps {
        sh 'docker build -t federicogfb/practica-ci-jenkins .'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push federicogfb/practica-ci-jenkins'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}