pipeline {
  agent any
  stages {
    stage('lint model') {
      steps {
        sh '''#!/bin/bash
/usr/local/sbin/salt-reclass --top'''
      }
    }
  }
}