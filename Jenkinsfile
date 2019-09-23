def COLOR_MAP = ['SUCCESS': 'good', 'FAILURE': 'danger', 'UNSTABLE': 'danger', 'ABORTED': 'danger']
def getBuildUser() {
    return currentBuild.rawBuild.getCause(Cause.UserIdCause).getUserId()
}

pipeline {
  agent any
  stages {
    stage('Build') {
      agent any
      steps {
        notifyStarted()
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
    post {
        always
    {
    script {
        BUILD_USER = getBuildUser()
    }
          echo 'I will always say Hello again!'

          slackSend channel: '#ci',
              color: COLOR_MAP[currentBuild.currentResult],
              message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} by ${BUILD_USER}\n More info at: ${env.BUILD_URL}"

    }
    /*
    post {
    success {
      notifySuccess()
    }
    unstable {
      notifyUnstable()
    }
    failure {
      notifyFailed()
    }
    }
    */
    
  }
}

// 20190923 Slack Notification Function 
// @Reference https://committed.software/posts/jenkins/slackNotifications/
/*
def notifyBuild(String buildStatus = 'STARTED', String colorCode = '#5492f7', String notify = '') {

  def project = 'KULLOW'
  def channel = "${project}"
  def base = "http://54.180.40.69:8088/blue/organizations/jenkins/kullow/activity"

  def commit = sh(returnStdout: true, script: 'git log -n 1 --format="%H"').trim()
  def link = "${base}${commit}"
  def shortCommit = commit.take(6)
  def title = sh(returnStdout: true, script: 'git log -n 1 --format="%s"').trim()
  def subject = "<${link}|${shortCommit}> ${title}"

  def summary = "${buildStatus}: Job <${env.RUN_DISPLAY_URL}|${env.JOB_NAME} [${env.BUILD_NUMBER}]>\n${subject} ${notify}"

  slackSend (channel: "#${channel}", color: colorCode, message: summary)

}

def author() {
  return sh(returnStdout: true, script: 'git log -n 1 --format="%an" | awk \'{print tolower($1);}\'').trim()
}

def notifyStarted() {
  notifyBuild()
}

def notifySuccess() {
  notifyBuild('SUCCESS', 'good')
}

def notifyUnstable() {
  notifyBuild('UNSTABLE', 'warning', "\nAuthor: @${author()} <${RUN_CHANGES_DISPLAY_URL}|Changelog>")
}

def notifyFailed() {
  notifyBuild('FAILED', 'danger', "\nAuthor: @${author()} <${RUN_CHANGES_DISPLAY_URL}|Changelog>")
}
*/
