pipeline {
  agent any
  stages {
    stage('initialize') {
      steps {
        build 'gradlew clean'
      }
    }
    stage('build') {
      steps {
        build 'build'
      }
    }
    stage('test') {
      steps {
        build 'test'
      }
    }
  }
}