pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh './gradlew clean build -x lint --refresh-dependencies'
      }
    }
    stage('Test') {
      parallel {
        stage('Unit Test') {
          steps {
            sh './gradlew test --stacktrace'
          }
        }
        stage('Lint') {
          steps {
            sh './gradlew lint --stacktrace'
          }
        }
      }
    }
  }
}