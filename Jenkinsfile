@Library('contract-managment@feature/QCMD-28') import com.mev.*

def SlackChannelNotifications = new SlackChannelNotifications(this)
def EmailNotifications = new EmailNotifications(this)

properties([
  disableConcurrentBuilds(), /* Do not allow concurent builds */
  buildDiscarder(logRotator(numToKeepStr: '2')) /* Limit build history */
])

try {
  node ('master') {
    stage ('Checkout') {
      git 'git@github.com:BorisBabiy/testing.git'
    }
    
    stage ('Notify') {
      SlackChannelNotifications.send('STARTED')
    }
    
    stage ('Build') {
      echo 'Build...'
    }
    
    stage ('Test') {
      echo 'Test...'
    }
    
    stage ('Deploy') {
      echo 'Deploy...'
    }
    
    stage('Failure') {
      echo "something"
      /* sh 'exit 1' */
    }
  }
} catch (e) {
  currentBuild.result = 'FAILURE'
  throw e
} finally {
  SlackChannelNotifications.send(currentBuild.result)
  EmailNotifications.send(currentBuild.result)
}