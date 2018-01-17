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
  }
} catch (e) {
  currentBuild.result = 'FAILED'
} finally {
  SlackChannelNotifications.send(currentBuild.result)
}