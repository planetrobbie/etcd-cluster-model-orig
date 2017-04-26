pipeline {
  agent any
  stages {
    stage('lint model') {
      steps {
        sh '''#!/bin/bash
sudo /usr/bin/salt-call state.show_highstate
'''
      }
    }
  }
}