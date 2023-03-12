pipeline {
  agent any
  

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build') {
      steps {
        sh ' apt-get update && apt-get install -y build-essential libpcre3 libpcre3-dev libssl-dev zlib1g-dev -u root:root'
        sh './configure'
        sh 'make'
      }
    }
    stage('Install') {
      steps {
        sh 'make install'
      }
    }
  }
}
