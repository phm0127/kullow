pipeline {
  agent none
  stages {
    stage('Build') {
      steps {
        sh './gradlew clean build -x lint test'
      }
    }
    stage('Test') {
      parallel {
        stage('Unit Test') {
          steps {
            sh './gradlew test'
          }
        }
        stage('Lint') {
          steps {
            sh './gradlew lint'
          }
        }
      }
    }
  }
}