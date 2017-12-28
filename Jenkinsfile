pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh '''./configure
make'''
      }
    }

 stage('SonarQube analysis') {
    // requires SonarQube Scanner 2.8+
    def scannerHome = tool 'SonarQube Scanner 2.8';
    withSonarQubeEnv('sonar') {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }

  }
}