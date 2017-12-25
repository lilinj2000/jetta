pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh '''./configure
make'''
      }
    }
  }
}