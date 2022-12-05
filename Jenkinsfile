pipeline {
  agent {
    node {
      label 'workstation'
    }
  }
  stages {
    stage('create ec2 ') {
      steps {
        sh 'bash create-ec2-env.sh frontend dev'
      }
    }

}