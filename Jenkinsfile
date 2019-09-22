pipeline {
  agent {
    node {
      label 'Android'
    }

  }
  stages {
    stage('Build') {
      agent {
        node {
          label 'Android'
        }

      }
      steps {
        sh './gradlew clean build -x lint test'
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
          steps {
            sh './gradlew lint'
          }
        }
      }
    }
  }
}