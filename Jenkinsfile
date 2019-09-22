pipeline {
  agent any
  stages {
    stage('gradle build') {
      steps {
        sh './gradlew clean build'
      }
    }
  }
}