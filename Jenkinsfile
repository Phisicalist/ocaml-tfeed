pipeline {
  agent any
  stages {
    stage('Get backoffice release') {
      steps {
        echo 'Get backoffice release id'
        powershell(returnStatus: true, script: 'Call api')
      }
    }

    stage('Get green') {
      parallel {
        stage('Get green') {
          steps {
            echo 'Getting green'
          }
        }

        stage('error') {
          steps {
            error 'Failed'
            warnError(message: 'Catched error') {
              echo 'All good'
            }

          }
        }

      }
    }

    stage('Communicate Slack') {
      parallel {
        stage('Communicate Slack') {
          steps {
            echo 'Communicating slack'
          }
        }

        stage('Communicate email') {
          steps {
            echo 'Communicating email'
          }
        }

      }
    }

    stage('Update releasesHub') {
      steps {
        echo 'Update latest releasesHub'
      }
    }

    stage('Manual approval') {
      steps {
        input(message: 'Can go forward?', id: '1', ok: 'Ok', submitter: 'Pipe', submitterParameter: 'PipeParam')
      }
    }

  }
}