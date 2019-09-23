pipeline {
  agent any
  stages {
    stage('Build') {
      agent any
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
          agent any
          steps {
            sh './gradlew lint'
          }
        }
      }
    }
    stage('Notification') {
      agent any
      steps {
        slackSend(message: '"Build Started - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"', channel: '#ci')
      }
    }
  }
}