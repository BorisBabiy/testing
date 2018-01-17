@Library('contract-managment@feature/QCMD-28') import com.mev.*

def SlackChannelNotifications = SlackChannelNotifications(this)

properties([
  disableConcurrentBuilds(), /* Do not allow concurent builds */
  buildDiscarder(logRotator(numToKeepStr: '2')) /* Limit build history */
])

try {
  node ('master') {
    stage ('Notify') {
      SlackChannelNotifications.send('STARTED')
    }
    
    stage ('Checkout') {
      git 'git@github.com:BorisBabiy/testing.git'
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
  }
} catch (e) {
  currentBuild.result = 'FAILED'
} finally {
  SlackChannelNotifications.send(currentBuild.result)
}