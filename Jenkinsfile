pipeline {
  agent any
  stages {
    stage('Build') {
      agent any
      steps {
        notifyBuild('STARTED')
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
  }
  post {
    success{
      notifyBuild('SUCCESS')
    }
    failure{
      notifyBuild('FAILURE')
    }
  }
}

// 20190923 Slack Notification Function 
// @Reference https://jenkins.io/blog/2016/07/18/pipeline-notifications/
def notifyBuild(String buildStatus = 'STARTED') {
  // build status of null means successful
  buildStatus = buildStatus ?: 'SUCCESS'

  // Default values
  def colorName = 'RED'
  def colorCode = '#FF0000'
  def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
  def summary = "${subject} (${env.BUILD_URL})"
  def details = """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
    <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>"""

  // Override default values based on build status
  if (buildStatus == 'STARTED') {
    color = 'YELLOW'
    colorCode = '#FFFF00'
  } else if (buildStatus == 'SUCCESS') {
    color = 'GREEN'
    colorCode = '#00FF00'
  } else {
    color = 'RED'
    colorCode = '#FF0000'
  }

  // Send notifications
  slackSend (color: colorCode, message: summary)
}
