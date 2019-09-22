pipeline {
  agent any
  stages {
    stage('Build') {
      agent any
      steps {
        sh './gradlew clean build -x lint --refresh-dependencies'
      }
    }
    stage('Test') {
      parallel {
        stage('Unit Test') {
          agent any
          steps {
            sh './gradlew :app:test --stacktrace'
          }
        }
        stage('Lint') {
          agent any
          steps {
            sh './gradlew :app:lint --stacktrace'
          }
        }
      }
    }
  }
}