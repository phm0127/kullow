pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh './gradlew clean build -x lint'
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