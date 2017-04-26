pipeline {
  agent any
  triggers { pollSCM('H/5 * * * *') }
  stages {
    stage('Install Service Metadata into Workspace') {
      steps {
        sh 'mkdir service'
        sh 'for i in /usr/share/salt-formulas/reclass/service/*; do ln -s $i service/; done'
      }
    }
    stage('Topfile Lint') {
      steps {
        sh '/usr/local/sbin/salt-reclass --top -b .'
      }
    }
    stage('Pillar Lint for etcd cluster nodes') {
      steps {
        echo 'Lint Pillar for Node-01'
        sh '/usr/local/sbin/salt-reclass --pillar etcd-01 -b .'
        sh '/usr/local/sbin/salt-reclass --pillar etcd-02 -b .'
        sh '/usr/local/sbin/salt-reclass --pillar etcd-03 -b .'
      }
    }
    stage('Cleanup Service Metadata') {
      steps {
        echo 'Cleanup Service Metadata'
        dir('directoryToDelete') {
          deleteDir()
        }
      }
    }
  }
}
