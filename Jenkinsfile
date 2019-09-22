pipeline {
  agent any
  stages {
    stage('Build') {
      agent {
        node {
          label 'App'
        }

      }
      steps {
        sh './gradlew clean build -x lint --refresh-dependencies'
      }
    }
    stage('Test') {
      parallel {
        stage('Unit Test') {
          agent {
            node {
              label 'app'
            }

          }
          steps {
            sh './gradlew test --stacktrace'
          }
        }
        stage('Lint') {
          agent {
            node {
              label 'app'
            }

          }
          steps {
            sh './gradlew lint --stacktrace'
          }
        }
      }
    }
  }
}