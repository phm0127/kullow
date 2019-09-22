pipeline {
  agent any
  stages {
    stage('Build') {
      agent any
      steps {
        sh './gradlew clean build'
      }
    }
    stage('Test') {
      parallel {
        stage('Unit Test') {
          agent any
          steps {
            sh './gradlew test'
          }
        }
        stage('Lint') {
          agent any
          steps {
            sh './gradlew lint'
          }
        }
      }
    }
  }
}